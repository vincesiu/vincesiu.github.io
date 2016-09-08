---
layout: page
title: Bookshelf
permalink: /bookshelf/
---

### __Reading Currently:__

- Donald Knuth: _The Art of Computer Programming, Vol. 1_ (probably never to be finished)
- Brett Slatkin: _Effective Python: 59 Specific Ways to Write Better_ 
- A bunch of RFC papers

-----------------------

### __Things I've Read__:


#### Whitepapers:

- _MapReduce: Simplified Data Processing on Large Clusters_
: google whitepaper on the high level algorithm of how their map reduce algorithm works, along with use cases, challenges with real world deployment, and performance of different versions

- Burns and Oppenheimer: _Design patterns for container-based distributed systems_
: google whitepaper on interesting design patterns. My favorite are the sidecar patterns (used for logging, allows modularity, however I would be very wary of over-engineering this stuff. This sidecar pattern is useful in docker especially, due to the difficulty of handling multiple processes in one docker container). I have not worked with multi-node application patterns, but I found the idea behind leader-election and scatter/gather pretty cool. I hope one day I'll be able to apply it.


- _RFC 3164 / RFC 5424_
: syslog spec, 3164 was the first version and then 5424 came after, this details the syslog protocol and allows for separation of the application which generates messages, the system which stores messages, and the frameworks which analyze the information inside. This is useful because it allows us to create a modular system in which we can easily swap in and out pieces (like elk!!!). However, note that RFC3164 syslog is not compliant with RFC5424 syslog, so watch out when handling legacy applications.

#### Books:

- Sam Newman: _Building Microservices_
: architecture of microservices

- Humble and Farley: _Continuous Delivery: Reliable Software Releases..._
: a dry book which relentlessly provides contradictory advice and practices. There is wisdom in this book, but you have to understand when and where to apply them. Be careful of overengineered solutions.

- Tom DeMarco: _Peopleware: Productive Projects and Teams_
: interesting perspective from management point of view

- Adam Webber: _Modern Programming Languages: A Practical Introduction_
: actually a solid book providing introduction to important language concepts.
