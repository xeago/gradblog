---
layout: simple
title: Test results for the proposed design
---


# Overview
This document describes the test results for the [proposed design]. It first covers recovering in case of a big outage. The testing environment is second as the environment has no impact on recovery. Node outages are covered next, finishing with migrations.

# Glossary
This report contains phrases that should be read in a context.

Term        | Explanation
:-----------|:-------
Cluster     | The set of machines running nodes of [Elasticsearch]
Node        | A machine running Elasticsearch
ES          | Elasticsearch
disk seeks  | The time it takes to get the requested data from disk.
shard       | A single lucene index
σ           | [Standard deviation](https://en.wikipedia.org/wiki/Standard_deviation)
CPU         | CPU resource usage, usually measured in percentage
Mem/memory  | Memory resource usage, usually measured in percentage or in (this case in) mebibytes

# Recovery
In case of disaster recovery the design provides two options: reindex from database and restore from backups. Re-indexing is costly on database access, bandwidth, and cpu/mem on the cluster. On the other hand there can be no trusted backup, updates occurring to the database must be replayed against the backup after a successful restore. Recommended practices for these backups are as follows: do not use a shared gateway, backup data-folder normally (link to source). The author of Elasticsearch commented the following on irc: "Use rsync to backup to S3 instead of the shared gateway, shared gateways are not intended for backup and are poorly implemented.". Clarification was needed if this was a bad implementation in Elasticsearch or bad implementation in systems-design, his reply was both.

In conclusion data was gathered about both options.

## Reindexing
Logs at the current Elasticsearch node running in production reveal the time, cpu-cost and memory load before normal operation. This was not extensively tested as I do not want to put load on the database unnecessarily. Re-indexing lasts around 11 minutes varying by 30 seconds, high cpu load and moderate memory load. The memory load increases from under 15MiB to 160MiB, depending on the garbage collector a tad lower. This lowers to 140MiB to 150MiB at normal usage.  
Unfortunately I did not acquire data for the database side of things. However some things can be said. The query which is used to gather the data for reindexing is not computationally-expensive, therefore the most limiting factors are bandwidth and disk seeks.

During reindexing available data will be served, albeit with a higher latency. Data is considered available 1 second after being stored in ES.

## Restore from backup
<small>This is where things get ugly.</small>

### Making a backup
There are several ways to do a backup, some of which rely on a deprecated feature and there is no restore API in ES *yet*. The deprecation happened late in testing, a week before the start of writing this document.

+ S3 — shared gateway (using cloud-aws plugin) (deprecated)
+ Hadoop
+ Rsync (recommended)
+ Local gateway (recommended)
+ Shared file system (deprecated)

#### S3
I tested backups on S3 and found these to be unreliable. During normal operation of the cluster, exceptions were thrown from the cloud-aws plugin. These exceptions slowly corrupted shards resulting in ± 10% data loss and a tedious shard recovery process. This behavior was easy to repeat; I therefore considered it broken.

#### Hadoop
Not tested; it is hard to set up and requires deep knowledge of the hadoop-filesystem.

#### Rsync
To prepare the shards for backup a sequence of actions should be submitted to the cluster: "flush, optimize, and close index". The [flush](http://www.elasticsearch.org/guide/reference/api/admin-indices-flush.html) command forces the transaction log to be emptied. The [optimize](http://www.elasticsearch.org/guide/reference/api/admin-indices-optimize.html) command optimizes the indices and merges segments; merging segments is necessary for 100% reliable on disk representation. Finally [closing the index](http://www.elasticsearch.org/guide/reference/api/admin-indices-open-close.html) makes sure that there are no more merges going on, this step is necessary in high write environments as than the only way that the index will be silent (no merge operations) is by not having it available. Opening and closing index are fairly quick operations.
After that sequence, ES_DATA can be safely transferred to other media.  
Recovering can be done by overwriting ES_DATA with the backup and starting the cluster.

#### Local gateway
**The default option for the gateway setting.**  
The local gateway allows a node to be restarted to initiate a recovery sequence. Failing shards will be recovered from the local gateway which is persisted on local disk.

#### Shared file system
Not tested; it is hard to set up and now deprecated.

# Test environment
All tests have been done using the [AWS free usage tier](https://aws.amazon.com/free/) on EU (Ireland) region. EC2 m1.small instances running [Ubuntu 10.04 LTS Lucid Lynx](http://cloud-images.ubuntu.com/releases/10.04/release/) were used for all tests. Results were similar with the expected variance and are therefore omitted. This is similar to the current instance running a single ES node.

Tests were done with a cluster size of 1, 2 and 5. Twice the amount of nodes in the cluster were used to establish load. All tests used a 90/10 ratio of read/write operations using [httperf](http://www.hpl.hp.com/research/linux/httperf/); initially [ab](https://httpd.apache.org/docs/2.2/programs/ab.html) was used but it lacked support for post requests (only put was supported).

# Outage
We distinguish between a single node failure and multiple node failure. Depending on the cluster size both shouldn't be problematic for data but might make the data inaccessible as clients can only be configured with a single endpoint (there is a work in progress to allow for multiple endpoints).

To combat this restriction the use of a proxy or load balancer was used. Elasticsearch could also act as a load balancer with the right configuration. This has certain benefits: automatic discovery of new nodes in the cluster and caching.

## Single
In case of a single node failure, no data is lost. The cluster will redistribute the shards to maintain the configured number of replicas and remain a green status. Redistributing shards is a cheap operation and involves only transferring of raw bytes.  
If there are not enough nodes available, the cluster will enter a yellow state. A yellow state means that all shards are available but do not have the configured replication.

However, if the application is configured to contact the failing endpoint, the application will not reach the cluster and error out. This can be solved with a load balancer or proxy. A summary can be found later in this report.

## Multiple
Elasticsearch as a system provides measures that assist with multiple shard outages. It is possible to dynamically increase the amount of nodes and the amount replica's of shards. It is not possible to change the amount of shards an index has after it has been created; the standard amount of 5 shards suits most use-cases.  
The "number_of_replicas" can be increased or decreased anytime, by using the Index Update Settings API. Elasticsearch takes care about load balancing, relocating, gathering the results from nodes, etc.  

# Migration
Migrations can be seen on two levels, index and cluster level. The mapping of an index can be modified on the fly, but only as long as no conflicts occur in the index.  
If the need arises to modify the mapping with such that reindexing is necessary or changing the shard count it is advised to reindex data from the *true* datasource, in VideofyMe's case this is the database.

The most common cluster level migrations are Elasticsearch version updates. In most cases this can be done with a quick restart of Elasticsearch. This can be done as follows:

1.  Install the new version
2.  Configure the data path to point to the correct *(shared)* location
3.  Optionally modify the monitor process to point to the new location such that upon a shutdown the new version gets launched
4.  Take the cluster down (optionally using [shutdown API](http://www.elasticsearch.org/guide/reference/api/admin-cluster-nodes-shutdown.html)) <small>The shutdown API can be disabled.</small>
5.  Relaunch the cluster or rely on the monitor process

In the unlikely case data migration is not possible reindexing from the *true* datasource is required. To facilitate this it is possible to start indexing on a secondary cluster and swap clusters when this is done.

# Proxies & load balancers
Three systems were tested: HAProxy, Nginx and Elasticsearch; [ELB](http://aws.amazon.com/elasticloadbalancing/) was not tested. Results are noted below. HAProxy and Nginx were configured with a simple *least connections*-based configuration file (provided by fine folks at Freenode). Elasticsearch load balancer is by default able to deliver cached results; no configuration for caching with HAProxy or Nginx was done. Elasticsearch load balancer also automatically discovers new nodes automatically.

CPU and memory usage were not the limiting factor during the tests; it was limited by network, Elasticsearch or both.

## HAProxy
With a throughput of almost 18k/s (σ): 335) this has the highest requests forwarded per second with the least amount of resource consumption.

| 
:-----------|:-------
CPU         | 30%
Memory      | 13%
Requests/s  | 18k/s (σ: 335)
Latency     | 83ms (σ: 46)

## Nginx

| 
:-----------|:-------
CPU         | 34%
Memory      | 15%
Requests/s  | 15k/s (σ: 281)
Latency     | 93ms (σ: 41)

## Elasticsearch
The only system to provide automatic discovery of new nodes. It is also the only system that requires the least amount of configuration. Surprisingly it uses less resources than Nginx while still having higher throughput. The lower latency is most likely by using an *(optimized)* binary protocol between ES nodes.

| 
:-----------|:-------
CPU         | 34%
Memory      | 12% to 18%
Requests/s  | 17k/s (σ: 130)
Latency     | 78ms (σ: 34)

[proposed design]: design.html