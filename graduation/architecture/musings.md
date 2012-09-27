---
layout: simple
title: Xeago's Musings
---

<small>My musings about the [design](design.html).</small>

I have become to fancy elasticsearch for it's cloud support and distributed nature in general. I would prefer support for failure/discovery in Tire.rb over the workarounds. For the workarounds, the 'clever' approach would be of my preference:

+   It requires no additional network components for management.
+   Discovery of the cluster is automatic.
+   Caching with percolation.
+   Simple configuration.
+   Portable among cloud providers.

In the argument that the application servers must now scale with ES:

+   There is no reason these nodes cannot be put on other instances.
+   It is also possible to have the lighter and heavier application servers:
    -   Heaver application servers have an elasticsearch-endpoint of localhost
    -   Lighter application servers have an elasticsearch-endpoint of a heavier application server.
    
    One could argue that this increases hosting complexity but I don't think this is an issue. If one persists, I would recommend adding support in Tire or using the 'solid' approach with a load-balancer.

Depending on the operational costs for having a no-data node at the application servers, it might be more cost-effective to add support in Tire.rb.