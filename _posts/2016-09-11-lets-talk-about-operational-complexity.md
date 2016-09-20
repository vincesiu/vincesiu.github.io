---
layout: post
title:  "Let's talk about big O notation"
date:   2016-09-11
categories: algorithms
---

One of the main things that we learn about in our computer science degree is big O notation, which is a mathematical function that analyzes features about programs. After reading [an interesting article about ram](http://www.ilikebigbits.com/blog/2014/4/21/the-myth-of-ram-part-i), it reminded me of an interesting revelation that I had about big O notation when I was taking algorithms.

Big O comes from a mathematics background, and not understanding it thoroughly can lead to a lot of miscommunication. The notation was originally used to help analyze taylor series, and to see how closely a finite series approximated a given functions. Programmers began using it to approximate running time of algorithms, and its use is widespread today. However, when I was learning it, I encountered a problem which took me a long time to understand: big O notation is ambiguous. What I mean by this is that we do not know what the input n is, or the output O(n) is. We have to use context/common sense to figure things out. 

For example, we can say a binary tree access runs in O(logn) time. What people can interpret this to mean is that given a binary tree of "n" size, then it will take a constant number multiplied by "log n" time to access the element in the worst case. However, I have not specified what the input "n" is! Let's say that I was talking about making queries against a constant size database with queries of variable length. Then, you would interpret my statement as, given a query of "n" length, then it will take "logn" time to run it. This has totally changed the meaning of the statement!

What I want to readers/my future self to understand from this example is that it is very important to understand the input and output of complexity equations before coming to conclusions. This is one of the problems addressed in the [final part of the ram series](http://www.ilikebigbits.com/blog/2015/2/9/the-myth-of-ram-part-iv) I was reading; one of the complaints was that the author was re-defining big o to mean execution time. Yes! This is the whole point! We can apply it to any input and output, and in this specific case, we have the input as the size of the memory access, and output as memory latency! This unusual usage is precisely why big o notation is so powerful - it can show us the relationship between any input and any output we want in a meaningful way.
