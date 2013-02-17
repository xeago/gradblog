---
layout: simple
title: Memos
---

These memos contain short reflections about skills acquired or knowledge gained, according to my [performance plan](performance-plan.html#ref-PI05).

# 2013-02-14
I have also written a document with my [reflections] around the end of my internship.

[reflections]: reflections.html

# 2013-01-14
Getting systems ready to deploy is a pain in the ass if it is a long running project. I recommend breaking big tasks up into smaller chunks than I did. While it did not cause any reasons for concern, it wasn't that fun having that much of pressure resting
needlessly on ones shoulders.

# 2012-11-26
We all know that when one designs and creates a system with certain quality aspects, one has to put these to the test. In case of networking and automatic failovers I have never had the chance to fully implement and design such a system, let alone think of testing it.  
Thankfully I get to test it here. Using [Webmock] and [Vcr] I can capture, replay and manipulate networking behaviour to simulate the desired scenarios. Before I usually resorted to 'pulling the plug' myself and seeing how the system behaves. Now I can accurately verify the behavior in a quick and concise manner.

[Webmock]: https://github.com/bblimke/webmock
[Vcr]: https://github.com/vcr-gem/vcr


# 2012-10-29
Writing DSLs in Ruby is just awesome! I took some time to study how to write DSLs in Ruby and I absolutely love it; never have I been so productive when implementing a design. **I would like to do some research on this and learn more about DSLs.**  
While implementing the design I felt my knowledge of the [elasticsearch query language][Query-DSL] was severely lacking. I spent a minor amount of time on this earlier on but I felt like I didn't grasp the constructs as well as I needed to. In hindsight, it can be compared with any other query language, like [SQL](http://www.iso.org/iso/home/store/catalogue_ics/catalogue_detail_ics.htm?csnumber=53681), [Hive](hive.apache.org), and [HBase](hbase.apache.org). You have to have expertise in the language to full take advantage of it. As I was only a bit behind schedule and I felt this was mandatory knowledge and experience, I set time apart to study the [elasticsearch query language][Query-DSL]. I tried querying the VideofyMe's test-data for every use I could find given any construct of the query language — it was a stretch. In this learning process, [Clinton] [Gormley] was of excellent assistance on [#elasticsearch]. I would like to thank him for his everlasting patience and help.

[Query-DSL]: http://www.elasticsearch.org/guide/reference/query-dsl/
[Clinton]: https://twitter.com/clintongormley
[Gormley]: https://github.com/clintongormley
[#elasticsearch]: irc://freenode.net/elasticsearch

# 2012-09-18
On my initial day working on the code in the API (this is only accessibly by other VideofyMe components), I was dumbfound on how it works. I could see it was separated according to MVC. I found no authentication, authorization nor security whatsoever. I asked about it in [campfire](http://campfirenow.com), the answer was the following: "that is done outside of the API, so we can have simple code". I thought all was well, and continued.  
While doing some early reading on distributed architectures, I came across [this blog post], more specifically the "[Platform layer]". About 3 days after reading that, I realized this is what VideofyMe used.  
Later, an issue in the adserver arose, Jesper started working on it. I asked if I could look over his shoulder and got introduced to [Hadoop] and [Elastic Map Reduce]. While I had a vague idea what Hadoop was, I could not think of a clear usecase. Jesper talked how the Hadoop-jobs worked and I was astonished by how much goes on behind the scenes at VideofyMe. I am grateful to Jesper for sharing his knowledge with me, I now have a clear insight on the uses for Hadoop.


[this blog post]: http://lethain.com/introduction-to-architecting-systems-for-scale/
[Platform layer]: http://lethain.com/introduction-to-architecting-systems-for-scale/#platform_layer
[Elastic Map Reduce]: http://aws.amazon.com/elasticmapreduce/
[Hadoop]: http://hadoop.apache.org
