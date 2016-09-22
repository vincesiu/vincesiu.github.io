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

- _A Multi-perspective Analysis of Carrier-Grade NAT Deployment_
: Wow there's a lot of different groups cooperating on this paper! Anyways, this provides an interesting look into the exhaustion of the ipv4 address space, as well as an interesting solution. The idea behind normal NAT is that each home/consumer grade network is only provided a single ip-address, and the router acts as an intermediary between the real internet and the home network. The paper provides an interesting insight into the current problems faced by isp's with ip distribution today (holy moly 20:1 subscriber to address ratio?!). It's also interesting reading about the different types of NAT (ie what kind of incoming connections are allowed?) Anyways, this shows the implementation of cgn (like home NAT (aka NAT44) except with, say, 512 ports per subscriber versus all 65535 ports of an ip address, as well as the current state of ip address market and its problems due to ip address reputation and blacklisting. Also, the technique which they used to determine if a carrier has CGN was interesting. The technique that I looked at took advantage of the DHT addressing methods used to find peers, and checking if those peers had certain reserved ip addresses. It's actually pretty interesting, and ... it surprised me how the determining method felt... unclean, not as sleek as I expected for such a detection algorithm (but the techniques that they used were still impressive! Don't want to knock them on creativity!). It's just that you would think there's a way to 100% discover if someone is behind a CGN or not... Also, a little terrifying that some ISP's use non-reserved IP addresses for internal cgn routing (which, as the author rightly points out, can have catastrophic consequences due to name resolution issues.

- _Wong and Vogel: _United States Patent Publication: File Deduplication Using Copy-On-Write Storage Tiers_
: Never read a patent before. Interesting that they would enumerate their methods (how can they even enfore a patent if they can't see the internal architecture of other companies?! You're basically publishing knowledge for free... Also, patents are pretty repetitive, but I guess that's what you have to be in order to protect intellectual property. Surprising that such a simple concept to explain would require such a difficult implementation (not that it's the first time I've seen something like this though)

#### Books:

- Sam Newman: _Building Microservices_
: architecture of microservices

- Humble and Farley: _Continuous Delivery: Reliable Software Releases..._
: a dry book which relentlessly provides contradictory advice and practices. There is wisdom in this book, but you have to understand when and where to apply them. Be careful of overengineered solutions.

- Tom DeMarco: _Peopleware: Productive Projects and Teams_
: interesting perspective from management point of view

- Adam Webber: _Modern Programming Languages: A Practical Introduction_
: actually a solid book providing introduction to important language concepts.

- Kurose and Ross: _Computer Networking: A Top-Down Approach_
: networking book, a bit dry, but DANG these pages are packed with useful information. Reccomend it if you're ever interested in learning about networks. The stuff that the authors included are vital towards understanding the current network environment

- Shannon and Weaver: _The Mathematical Theory of Communication_
: math and proofs incarnate, shows how there is a limit to the amount of information that can be transported, given certain parameters. Fascinating stuff. Should reread when I have a better grasp of mathematics.

- Bryant and O'Hallaron: _Computer Systems: A Programmer's Perspective_
: brings back memories. Great book, great problems, great tests.... horrible teacher. I learned a ton about structures and systems that run on the metal, and that modern OS's are built upon (eg multithreading, bit operations, memory handling)

- Kleinberg and Tardos: _Algorithm Design_
: ... old book, not too good at explaining itself, I personally needed to run through the proofs and algorithms several times each to understand them. Content is solid though.

- Patterson and Hennessy: _Computer Organization and Design_
: gave me a healthy respect for low level systems and how they operate. I understand processors a lot more because of this book, as well as the WHY behind the specs of a computer and what the numbers mean
