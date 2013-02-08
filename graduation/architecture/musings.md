---
layout: simple
title: Xeago's Musings
---

# My musings about the [design](design.html).

I have become to fancy Elasticsearch for it's cloud support and distributed nature in general. I would prefer support for failure/discovery in Tire.rb over the workarounds. For the workarounds, the 'clever' approach would be of my preference:

+   It requires no additional network components for management.
+   Discovery of the cluster is automatic.
+   Caching with percolation.
+   Simple configuration.
+   Portable among cloud providers.

In the argument that the application servers must now scale with ES:

+   There is no reason these nodes cannot be put on other instances.
+   It is also possible to have the lighter and heavier application servers:
    -   Heaver application servers have an Elasticsearch-endpoint of localhost
    -   Lighter application servers have an Elasticsearch-endpoint of a heavier application server.
    
    One could argue that this increases hosting complexity but I don't think this is an issue. If one persists, I would recommend adding support in Tire or using the 'solid' approach with a load-balancer.

Depending on the operational costs for having a no-data node at the application servers, it might be more cost-effective to add support in Tire.rb.

# My musings about the [test results](test-results.html)
Using [puppet](http://projects.puppetlabs.com/projects/puppet) to provision the servers was enormous fun to set up. Even though my tests were quite short, the error values derived from the results are low.
Therefore the values cannot be seen as a result scientific benchmarking but they do give good insight in the various options. I didn't expect Elasticsearch as a load balancer to perform this well. However, since Elasticsearch has to run on at least half the clients-nodes, it is still the most costly option: memory is measured per node and not per cluster. Regardless of this, the benefits that Elasticsearch provides — most notably automatic cluster discovery, routing and ease of configuration — far exceed the reduction in memory when choosing HAProxy or Nginx.

I have to thank all the nice folks on irc for helping me set up the various services: #elasticsearch, #haproxy, #nginx on [irc.freenode.net](http://webchat.freenode.net).
