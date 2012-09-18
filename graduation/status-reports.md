---
layout: simple
title: Status reports
---

These reports contain a summary of the activities and their results, according to my [performance plan](performance-plan.html#ref-PI05).

# 2012-08-18 - Shit, this a lot of work!
In the first few weeks I worked on several things supporting the deprecation of the old search and moving towards the new system. I was pleasantly surprised how easy it was to get elasticsearch active and populated. Once that was up and running I added support for pagination through the API. I now felt that I had a clear idea of what I will be doing and defined my concrete [internship assignment]. I send this for approval and got positive feedback.  
I experimented with different [lucene analyzers] to provide a short term solution for searching with spaces, keyword filter doesn't tokenize. Following this there was a deadline from the App-team, requiring search on hashtags. I implemented hashtag-search, and worked on my [performance plan]. Borrowing some of the functionality I created earlier, hashtag-search was easy to implement, though it had its quirks. I continued with the performance plan.  
Hell, this plan was a lot of more work than I expected. I am still awaiting feedback from Rianne, but have gotten approval from Patrick. I also set up a proposal for my [development process].

[internship assignment]: graduation-assignment.html
[lucene analyzers]: http://lucene.apache.org/core/old_versioned_docs/versions/3_0_1/api/all/org/apache/lucene/analysis/Analyzer.html
[performance plan]: performance-plan.html
[development process]: development-process.html