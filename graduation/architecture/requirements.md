---
layout: simple
title: Architectural requirements for (elastic)search
---

This document describes requirements that apply to the architecture for (elastic)search. This system will be used for querying realtime information, mostly about videos. Input into elasticsearch (ES), the software system that will run on the architecture, comes from the VideofyMe API.

>   The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119].  
>   >   [Bradner, S., "Key words for use in RFCs to Indicate Requirement Levels", BCP 14, RFC 2119, March 1997.]

[RFC 2119]: http://www.ietf.org/rfc/rfc2119.txt (Bradner, S., "Key words for use in RFCs to Indicate Requirement Levels", BCP 14, RFC 2119, March 1997.)

# Environment
This architecture should operate on Amazon Web Services (AWS). Therefore some systems, components specific to this environment may be proposed, examples of these systems are "Elastic Cloud Compute" (EC2) and "Simple Storage Service" (S3). These systems, components should have alternatives noted which can (optionally) be used on different environments.

# Single node failure
In case of single node failure, no data older than [the mean [round trip time | latency] between client and server | 1 second | 5 seconds | 20 seconds] must be lost. Nodes added to replace failing nodes should restore state from other nodes. Restoring from other nodes should not have a significant impact on the load of the nodes to prevent failure by adding resources.

# Availability
The architecture must allow for high-availability. It must not have a single point of failure unless unavoidable within reasonable efforts or is considered de facto standard.

# Complete cluster failure
Upon failure of all nodes, it is required that most data is recoverable. Most is be defined as [the mean [round trip time | latency] between client and server | 1 second | 5 seconds]. Data may also be restored using a re-import from a separate database not covered in this architecture.

# Total catastrophic failure
No means of recovery is provided within this architecture in case Amazon is not able to provide their service according to the Service Level Agreements (e.g. S3, EC2). Depending on the extent of the outage, data recovery may be available from S3.

# Response speed
Query response time should feel fast or be within acceptable standards. Opinions from colleagues will be used for this measurement.

#  Growth and Extensibility
The storage format (indices within ES) must account for growth and extensibility. 