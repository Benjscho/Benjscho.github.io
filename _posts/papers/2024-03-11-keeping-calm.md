---
layout: post
title: "Paper Summary: Keeping CALM"
date: 2024-03-11 21:00:00 +0700
mathjax: true
categories: papers
tags: software-engineering swe productivity
---

Summary of [Keeping CALM: when distributed consistency is easy](https://dl.acm.org/doi/10.1145/3369736)

This paper from Hellerstein and Alvaro centers around what we can do without coordinating. The core insight of the paper is that some distributed programs can run without coordination, as long as the output of running the program on a subset of the inputs doesn't change once you get more information.

<!--more-->

This made sense to me as kind of the core insight behind something like MapReduce. For a simple example, imagine we had a bunch of books, and we wanted to count the number of times the word "peacock" appears in all of them. We can spread that work out. If someone gets a result first, that's not going to change. We can just add all the results together at the end (a commutative operation) to get our final result, so the problem doesn't require coordination and is _monotonic_. 

In a contrary example, we could think of taking the same books and asking if the word "frangipane" occurs in any of them. Because here we're asking a question about _all_ of the books, the result can change when we get more information. That gives us an example of a program that is _non-monotonic_. 

Formally they give the definition:

> A program P is _monotonic_ if for any input sets $S, T$ where $S \subseteq T, P(S) \subseteq P(T)$

And present the theorem:

> _Consistency as Logical Monotonicity (CALM)_. A program has a consistent, coordination-free distributed implementation if and only if it is monotonic. 

So the claim of the theorem here is that if we make our applications or systems monotonic, then they can be both consistent and coordination-free. This sounds like a great deal! Instead of trading away some availability under network partitions to be consistent, as long as our program is monotonic we can have both availability and consistency. 

The key insight that helps us is that we can invert some operations to make the overall program monotonic. Here they use the example of an online shopping cart from [Dynamo](https://www.allthingsdistributed.com/files/amazon-dynamo-sosp2007.pdf). We can always add items to the cart. Adding more items doesn't change anything about the items you already have. However, we can't update or delete items, because those operations aren't monotonic - they change the outcome depending on the order they're performed. 

To make a deletion work with simultaneous operations we can instead use tombstoning, where deletes instead form a separate set and we combine them at the end. This means we don't need to wait for the delay of coordination while we're trying to put something in our cart. We can pay the coordination cost to combine the results once at the end instead during checkout.  

Representing this as a series of sets really made it click for me. You can always create more sets and add to sets without coordinating, but you can't take a difference of them. 

Another interesting highlight is the mention of Conflict-free replicated data types ([CRDTs, presented at INRIA 2011](https://pages.lip6.fr/Marc.Shapiro/papers/RR-7687.pdf)). These are types that underly systems like Figma, to enable real time collaboration. These types are primitives that provide an object-oriented way to implement monotonic patterns. The states of two CRDTs can always converge to the same state, allowing work from different users to be merged.

The paper aims to be a rare positive result in distributed systems, where a lot of papers and results center around what you can't do, or can't have. It shows us how we can constructively think about creating programs that don't require coordination, and helped me to understand how others already have. 