---
layout: simple
title: Architectural design for (elastic)search
---

This document describes propositional designs that comply with and fulfill the requirements described in the [architecture requirements document](requirements.html).  
All proposed designs have undergone testing by the author, results can be found in the [test results](test-results.html). The authors opinion on this and the test-results can be found in his [musings](musings.html).

# Current
There are 4 instances of the VideofyMe API. These have a connection with a central MySQL-database (ARDS), updates to rows in mysql are pushed to elasticsearch in after-hook events. All 4 API-instances
The current setup only has a single elasticsearch node. In every case of failure, data is lost. However, it may be re-imported from the database. 

![current]

<div id="ref-elasticsearch" class="ref"></div>

# Elasticsearch itself
Luckily enough, elasticsearch is relatively easy to scale. Clusters sizes of uneven/prime+1 nodes are recommended as this reduces the probability for master election conflicts. However the conditions for this to occur are very strict and rarely ever seen in production.

![focus_es]

#### Persistence
In the diagram 3 different systems of persistence are shown, so called *gateways*.  
It is arguable that RAM does not offer persistence however it persists throughout crashes of the ES-binary, allowing for very quick recoveries. The S3-gateway is shared between all nodes running, multiple nodes can restore from this at the same time. It is also possible to persist to local disk, depending on the cloud provider this may however be wiped upon instance reset/failure/termination.  
Nodes within a cluster can combine any of these gateways, however, only 1 gateway per node can be specified.

#### Response speed
The response speed can be easily influenced by the amount of nodes and the amount of replicas. Queries will be executed in a map-reduce like fashion when increasing the number of replicas.

#### Availability & scalability
Within elasticsearch it is easy to guarantee high-availability. Simply increasing the amount of nodes and the replicas of an index will make that index more available. Elasticsearch has built-in loadbalancing, routing, caching (with percolation), master failover and data replication. It has means for optimistic versioning to allow for consistent data across the cluster.  
It is possible to have nodes outside of the regional area where the cluster is hosted. However, spreading out nodes across continents does have a latency and throughput impact. Therefore, nodes outside of the regional area should not both hold data **and** participate in master election at the same time. These decisions differ on a case by case basis, extensive testing should be performed if you wish to have cross-regional clusters. A dedicated link is highly recommended.

#### Growth and Extensibility — storage format
The design proposed here makes no assumptions, nor restrictions on the storage format: the amount of indices, shards and nodes. Design (-considerations) for the indices, shards and nodes will be detailed elsewhere.

# Client Library
The ruby client, [Tire.rb](http://karmi.github.com/tire), only supports a single end-point. Hence if this end-point becomes unreachable, that client is unable to operate normally. The architectures proposed assume no changes to Tire.rb, it may be deemed necessary to alter the library. However, several work-arounds exist:

+   **Clever** — Run a no-data node of ES in front of (each of) the application-servers.  
    A no-data node handles discovery, routing and load-balancing of requests to the cluster and aids in master-election.
+   **Solid** — Set up a proxy, load-balancer in front of the ES-cluster.
    Example systems for this: HAProxy, nginx. This will, however, require management of an additional (network) component. Custom actions have to be taken to make the system aware of additional nodes.

However adding failover/discovery support to tire makes the above two workarounds more reliable and flexible.

+   Add failover/discovery support to Tire.rb.
    The community already has put some effort into this:
    -   [Two](https://github.com/karmi/tire/pull/163) [pull-requests](https://github.com/karmi/tire/pull/175) on GitHub adding basic "support for multiple url's" in the configuration of tire.
    -   An [issue](https://github.com/karmi/tire/issues/162) declaring the absence of failover/discovery a deficit in Tire.rb as a client for a distributed system.  
    The author comments:
    >   …I think that handling high-availability/failover in client “completely misses the point of elasticsearch” :)
    >   >   Karel Minařík, [karmi/tire issue#162](https://github.com/karmi/tire/issues/162#issuecomment-3096597)

# Workarounds
Both work arounds don't describe elasticsearch itself. They both work on top of the a normal elasticsearch cluster. Refer to the section [elasticsearch itself](#ref-elasticsearch) for information about elasticsearch.

## Clever approach
This approach levers the built-in discovery and load-balancing features elasticsearch. By adding a no-data node in front of the application servers, requests will automatically get routed and balanced over the cluster. This cluster is automatically discovered and can expand freely. The no-data nodes can cache certain queries, these caches get updated via percolation.  
Nodes leaving the cluster will be automatically detected and queries will not be routed to them.

![clever_1]

## Solid approach
This approach relies on a load-balancer, proxy to provide a single endpoint that is reliably available. This component needs to be made aware of nodes leaving the cluster so requests get routed to nodes still available. This also introduces a new network component. Obviously, it could be argued that this introduces a single point of failure in the stack.

![solid_1]

[current]: designs/current.jpg "The current architecture being used in production."
[focus_es]: designs/focus_es.jpg "Focusing only on elasticsearch."
[clever_1]: designs/clever_1.jpg "Using elasticsearch cleverly as a workaround."
[solid_1]: designs/solid_1.jpg "Using proven, robust technologies as a workaround."
