---
layout: simple
title: Memos
---

These memos contain short reflections about skills acquired or knowledge gained, according to my [performance plan](performance-plan.html#ref-PI05).


# 2012-08-18
On my initial day working on the code in the API (this is only accessibly by other VideofyMe components), I was dumbfound on how it works. I could see it was separated according to MVC. I found no authentication, authorization nor security whatsoever. I asked about it in [campfire](http://campfirenow.com), the answer was the following: "that is done outside of the API, so we can have simple code". I thought all was well, and continued.  
While doing some early reading on distributed architectures, I came across this blog post, more specifically the "[Platform layer]". About 3 days after reading that, I realized this is what VideofyMe used.  
Later, an issue in the adserver arose, Jesper started working on it. I asked if I could look over his shoulder and got introduced to [Hadoop] and [Elastic Map Reduce]. While I had a vague idea what Hadoop was, I could not think of a clear usecase. Jesper talked how the Hadoop-jobs worked and I was astonished by how much goes on behind the scenes at VideofyMe. I am grateful to Jesper for sharing his knowledge with me, I now have a clear insight on the uses for Hadoop.


[this blog post]: http://lethain.com/introduction-to-architecting-systems-for-scale/
[Platform layer]: http://lethain.com/introduction-to-architecting-systems-for-scale/#platform_layer
[Elastic Map Reduce]: http://aws.amazon.com/elasticmapreduce/
[Hadoop]: http://hadoop.apache.org