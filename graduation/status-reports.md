---
layout: simple
title: Status reports
---

These reports contain a fortnightly summary of the activities and their results, according to my [performance plan — PI05](performance-plan.html#ref-PI05).

# 2012-11-01 — Woah, I'm late!
Implementing the design has gone good. <small>Ruby proves to be an amazing tool</small>. Unfortunately I didn't manage to write about the end-clause of my graduation. I do want this done before the 60% mark.  
While implementing the design I felt my knowledge of the [elasticsearch query language][Query-DSL] was severely lacking. Therefore I devoted time to this.

It may seem I didn't get much done in this time-frame; I can't argue against it. However, I feel that the time was well-spent. I had (and at the time of writing still have) an injury to my right thumb which limits my ability to effectively use a keyboard. But I have also been procrastinating implementing stuff because the query language was awesome.

# 2012-10-08 — Video conference
<small>This is just a quick update.</small>
In this video conference we talked about my current progress and how to continue. We discussed contents of the [performance plan]. A lot of details regarding my graduation were made clear today. Two examples are the fact that there is no end-clause defined (in my assignment), as well as the issues regarding the date of my graduation at school.

# 2012-10-02 — Not supported? Open source!
During the last week I worked on my [architecture proposals]. It is **important** to also read my own [musings] about this design and the [requirements]. Patrick has given me an *OK* to add this support to Tire. I've established contact with [Karmi](http://karmi.cz/en), the author of the library.  
I heard from Rianne! Later this week we're having a videoconference to talk about my [performance plan]. It took a while to get her to look at my performance plan, I guess she was busy. I'll also discuss the other documents in [graduation]: [development process], [time management].

[architecture proposals]: architecture/design.html
[musings]: architecture/musings.html
[requirements]: architecture/requirements.html
[graduation]: index.html
[time management]: time-management.html


# 2012-09-18 — Shit, this is a lot of work!
In the first few weeks I worked on several things supporting the deprecation of the old search and moving towards the new system. I was pleasantly surprised how easy it was to get elasticsearch active and populated. Once that was up and running I added support for pagination through the API. I now feel that I have a clear idea of what I will be doing and  I defined my concrete [internship assignment]. I sent this for approval and got positive feedback.  
I experimented with different [lucene analyzers] to provide a short term solution for searching with spaces, keyword filter doesn't tokenize. Following this there was a deadline from the App-team, requiring search on hashtags. I implemented hashtag-search, and worked on my [performance plan]. Borrowing some of the functionality I created earlier, hashtag-search was easy to implement, though it had its quirks. I continued with the performance plan.  
Hell, this plan was a lot of more work than I expected. I am still awaiting feedback from Rianne, but have gotten approval from Patrick. I also set up a proposal for my [development process].

[internship assignment]: graduation-assignment.html
[lucene analyzers]: http://lucene.apache.org/core/old_versioned_docs/versions/3_0_1/api/all/org/apache/lucene/analysis/Analyzer.html
[performance plan]: performance-plan.html
[development process]: development-process.html