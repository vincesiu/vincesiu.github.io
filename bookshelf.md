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

- Jochen Topf: _The HTML Form Protocol Attack_
: an interesting paper on an old attack which is interesting. It involves deflecting a request. I would like to think of this as a kind of "reflected" attack, since a targeted user must be sent the page with the malicious code, and the user will initiate the HTML post request. The paper proposes either using the attack to make a scapegoat, or to use it to send data to a network which the target has access to and not the attacker.

- _A name for the null pointer: nullptr (revision 4)_
: Interesting. Provides a lot of interesting cases for why the transition from NULL (which is just a #define macro as 0) to nullptr (which is a special character). There's a lot of small nuances that language designers would go nuts over! Just read the first 2 pages for crazy cool combinations. For example, std::string s1(false) will compile since it will call char *constructor with null, but std::string s2(true) will throw a compilation error. One of the interesting notes about proposed solutions to NULL is that supporting backwards compatibility is a major concern of language developers, some of the decisions that they made early on have stayed and bit C++ development in it's butt. However, look at the divide between Python 2 and Python 3, and how long it has taken for people to move towards 3!
: Also on a side note, one of the proposed implementations for nullptr uses an anonymous class, and I researched it, and found out that one of his uses was filling the role of anonymous functions (and since C++11 have probably fallen out of favor). The biggest reason is (unsurprisingly) compatiblity reasons again, since C used a lot of typedefs on anonymous classes. In addition, I feel much better seeing the difficulty in how even veteran language designers have when looking for names for their variables.

#### Books:

- Sam Newman: _Building Microservices_
: architecture of microservices

- Humble and Farley: _Continuous Delivery: Reliable Software Releases..._
: a dry book which relentlessly provides contradictory advice and practices. There is wisdom in this book, but you have to understand when and where to apply them. Be careful of overengineered solutions.

- Tom DeMarco: _Peopleware: Productive Projects and Teams_
: interesting perspective from management point of view

- Adam Webber: _Modern Programming Languages: A Practical Introduction_
: actually a solid book providing introduction to important language concepts.
