---
layout: simple
title: Extended Abstract — Twan Wolthof
---

<!--
Using http://blackboard.hszuyd.nl/bbcswebdav/courses/HIO-IT4-I4-I8-stage-afstuderen/Documenten/Docs_Afst_Stage/SE/ExtendedAbstractStageEnAfstuderen.pdf as a reference.
-->

# Introduction
This extended abstract documents the internship period for Twan Wolthof at
VideofyMe. It will be the main document used in the final assessment of Twan's
graduation.

This document assumes *some* knowledge of programming, distributed systems,
cloud services and system administration.

## Twan Wolthof
This document is part of the conclusion of the *Information Technology*
education at [Zuyd Hogeschool]. Twan intends to finish his education at an
accelerated pace, in 3.5 years — instead of the usual 4 years.

## VideofyMe
Videofyme is a technology-startup doing videohosting with custom developed,
unique features.
> VideofyMe was founded April 2009 by Robert Mellberg and Oskar Glauser with
  the goal to build the smartest and easiest to use video service for blogs and
  websites.
> > From [videofy.me/about](http://videofy.me/about)

Twan applied for the position as an intern after seeing their advertisement
on [Github: Jobs](http://jobs.github.com).
<!-- The advertisement has now expired. -->

<!-- I repeatedly asked if this section was supposed to be included,
  it was not. -->
<!-- # Abstract -->

## Work environment
From August 2012 through February 2013 Twan has been operational in VideofyMe's
office; located at [Tullhus 3, Skeppsbron 111 30 Stockholm, Sweden](http://g.co/maps/2fvk8).

<!-- ## Test Results: I think the location for this node is weird. -->
<!-- Theoretic framework: I think the location for this node is weird.
                          It fits better in the next sections. -->

# Internship assignment
The internship assignment was not specific. Instead it was quite broad.
It transformed over time based on new requirements and insight. Below is a copy
of the initial document.

> # VIDEOFY.ME
> VideofyMe is a video service that connects publishers with followers and
  advertisers. The publisher uploads a video through mobile apps or our
  website and spreads it to their followers. Users then earn money on
  advertisements which we book on their videos, if desired.
  Today, VideofyMe has more than 200,000 publishers with more than
  50 million video views per month. VideofyMe is a global service that has
  paid more than 1,000,000 USD to its members.
> # YOU
  We are looking for talented developers who have worked with and build
  social media tools. We want you to have a good understanding of how
  users think and what they want to achieve. You should know what the
  important triggers in social media are, and what it is which makes
  people use them. You want to work with business logic and like to design
  your own systems. You will be working with the business logic of our
  platform and work closely with our mobile app developers. During your
  internship you will expand our existing codebase with social media
  features for a social video platform. You will work in a team of
  10 people and are a core part of the business logic development within
  the company.
> > From [http://blog.xeago.nl/assets/internship/videofyme-internship.html](http://blog.xeago.nl/assets/internship/videofyme-internship.html)

Several weeks before summer holidays Patrick communicated to Twan a common
(feature) request. Users requested higher quality search results. Staff
requested a non-critical database. Earlier investigation showed that the search
queries were hammering down the database. With a growing userbase and
inefficient search-queries the database suffered in performance. This
information further specified the [assignment](graduation-assignment.html).
In summary, Twan would be responsible for search and related functionalities at
VideofyMe.

Patrick decided to use Elasticsearch for a distributed full-text search
environment. This would remove the strain from the database and open up
possibilities to improve the quality of search results.

<!-- This paragraph below is in wrong tense. It is also in the wrong place -->
<!--
The first day at work Patrick hooked me up with some hook-in points in the
code and gave me a tour around the code. I had previously already set up my ruby
environment to be compatible with theirs, so I went on scouring their code.
Details about my first impressions can be found in my [status reports] and
[memos].
-->

Quite early on investors wanted hashtag functionality across the board. This was
the first component to be implemented that was not initiall anticipated with the
further specified assignment.

The complexity of this assignment was determined by areas of textual analysis,
distributed systems, unknown programming environment and frameworks, and
language.

# Method
Videofy works with development cycles of around 2 weeks. When work is considered
done it gets deployed to production, unless there is a desire to do so. At the
start of each cycle the previous cycle is reviewed and new work is scheduled.
This caused the assignment to evolve over time and be clearer.

We will first describe the infrastructure in use at VideofyMe and introduce new
components. After this we will discuss the changes to the infrastructure and
provide test results of this new infrastructure. We will also discuss how the
software is built up of easy to extend components.

<!-- Somehow have to incorporate these things:
# Work environment

+ Abroad
+ Working with distributed software
-->

## Infrastructure
TODO: Give a short overview of the infrastructure using diagrams.

## [Elasticsearch]
Elasticsearch is a lot of things. It uses Lucene for full text search. It is
schema free, document oriented and a NoSQL key-value store. Everything is
dynamic with out of the box scaling and failover. High availability and near
realtime search results.  
This is all accessible through beautiful APIs available in multiple formats.

### [Lucene]
Elasticsearch uses Lucene for full text search.
> Apache Lucene™ is a high-performance, full-featured text search engine library
  written entirely in Java. It is a technology suitable for nearly any
  application that requires full-text search, especially cross-platform.
>
> Apache Lucene is an open source project available for free download.
> > From [http://lucene.apache.org/core/](http://lucene.apache.org/core).

<!-- Some terms are unclear in the below paragraph. -->
Elasticsearch shards documents based on a hash of a document's unique
identifier. Each shard is a standalone Lucene-index. Multiple shards make up
a search-index in elasticsearch. An index can have multiple types. One could
compare this to databases, shards/pages/partitions and tables where a database
corresponds to a search index, shards/pages to shards/lucene-indices and tables
to types.
<!-- Maybe rephrase the above sentence: corresponding to a search index,
shards/lucene-indices and types respectively. -->

The number of shards is specified during index creation and then fixed. The
number of replicas of each shard can be changed at will.  
There is no optimal number of shards; it is dependent on the requirement of your
data. <!-- Why A instead of The --> A default of 5 shards works for most cases
but propbably won't give you the best results for your particular data.  
When it has been determined that the defaults don't suit your needs, it is
important to conduct a proper investigation into what those needs are and how
they can be accomplished. One should be careful when deviating from these
defaults.

### Plaintext search
<small>This section is anecdotal as it details Twans personal perceptions.</small>
> + First time I have to deal with search.

#### Terms
Designing good schemata to optimize your search results is completely different
than designing them in other systems I have worked with. In SQL based stores you
design a scheme based on relationships and data types. However, when optimizing
for text search, you have to go one step further. Here the lowest denominator is
a single `term`. All input gets reduced to terms, whether it is boolean,
numeric, date related or just text. It doesn't matter.

Text is special because it means different things depending on its context.
For example the format, language, spelling errors and more.
This requires careful consideration when designing a scheme. Elasticsearch helps
you by automatically guessing a scheme based on first input, and migrates to
better schemes automatically later on. This scheme is a good starting point to
attach your specific needs like [ICU](https://en.wikipedia.org/wiki/International_Components_for_Unicode)
(International Components for Unicode, software supporting internationalization)

### [API]
Elasticsearch can be configured almost completely while running via the API.
The API is well documented at the [community website][Elasticsearch]. It reveals
a multitude of useful information on a cluster, node, index or shard level.
There are plugins that make this information available in web based GUIs.
Examples of these APIs are [Head], [Bigdesk] and [Paramedic]. All of these were
used for the internship assignment.  
These proved especially helpfull as a guide to create some scripts for the
[test results].


#### [Query DSL]
Elasticsearch implements a really nice domain specific language to query the
index. The heading of this paragraph links to the official documentation.  
Using simple to understand composites it is possible to create queries tailored
for your data and usecases. The DSL has constructs like `bool`, `range`,
`query-string` and more. During the internship I constructed several of these
queries as well as built an abstraction for the common structure for queries.

#### [Other API components]
Elasticsearch also provides information about the environment it runs on. The
most important endpoint is `/`; a quick small message that either tells you
everything is `OK` `200` or requires further investigation. Other components
include Health, Stats, Nodes Info and more. Together they provide a complete
overview of the cluster, nodes on the cluster and the environment of
Elasticsearch itself.

### [Tire]
VideofyMe chose to use this client before the start of my internship. At the
time of this decision this was the only ruby client. It provides the same Query
DSL that Elasticsearch provides, but in a Ruby DSL. Therefore it is essentially
a wrapper, it does no input validations.

# Other realizations
+ Serving videos requires a lot of tracking to make it profitable

# Summary of hyperlinks
TODO: Put all references here in non-markdown format.

# Other used materials
+ TODO: Incomplete
+ **The Elasticsearch book**; official; as yet unpublished material from [Elasticsearch.com]
+ SQL turns NoSQL large scale
  [mysql is facebook scale so-why use nosql — Pandawhale]
  [Why does Quora use MySQL as the data store instead of NoSQLs such as Cassandra MongoDB or CouchDB]
  [friendfeed uses schemaless mysql]
+ [Managing large sharded topologies]





[Elasticsearch]: http://elasticsearch.org
[Elasticsearch.com]: http://elasticsearch.com
[API]: http://www.elasticsearch.org/guide/reference/api/index.html
[Query DSL]: http://www.elasticsearch.org/guide/reference/query-dsl/index.html
[Other API components]: http://www.elasticsearch.org/guide/reference/api/
[Lucene]: http://lucene.apache.org/core/
[Tire]: http://karmi.github.com/tire/


[test results]: architecture/test-results.html
[status reports]: status-reports.html
[memos]: memos.html

[mysql is facebook scale so-why use nosql — Pandawhale]: http://pandawhale.com/convo/383/mysql-is-facebook-scale-so-why-use-nosql
[Why does Quora use MySQL as the data store instead of NoSQLs such as Cassandra MongoDB or CouchDB — Quora]: http://www.quora.com/Quora-Infrastructure/Why-does-Quora-use-MySQL-as-the-data-store-instead-of-NoSQLs-such-as-Cassandra-MongoDB-or-CouchDB/answers/39928
[friendfeed uses schemaless mysql — backchannel]: http://backchannel.org/blog/friendfeed-schemaless-mysql
[Managing large sharded topologies]: http://www.percona.com/files/presentations/percona-live/nyc-2012/PLNY12-managing-large-sharded-topologies-jetpants.pdf
