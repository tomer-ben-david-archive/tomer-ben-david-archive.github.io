---
layout: news_item
title: "Scala flat and flatMap revisited"
date: "2014-10-03 03:32:11 +0200"
author: Tomer-Ben-David 
version: 1.0.0
comments: true
categories: [scala,functional-programming]
---

Scala map and flatMap are surely mixing map, I mean mixing map, I  mean mixing up.

Let's start simple;  All of those `map`, `flatMap` are methods of some `classes` (for the sake of explanation classes, interfaces, whatever).  So they all work on some kind of an encapsulation.  `map` and `flatMap` are methods of `Option`, of `List`, of `Future`.

If you look at `map` and `flatMap` method signatures you will see:
{% highlight scala %}
// for `Future`

    def map[S](f: (T) ⇒ S)(implicit executor: ExecutionContext): Future[S]
    def flatMap[S](f: (T) ⇒ Future[S])(implicit executor: ExecutionContext): Future[S]

// for `List`

    def map[B](f: (A) ⇒ B): List[B]
    def flatMap[B](f: (A) ⇒ GenTraversableOnce[B]): List[B]

// and for `Option`

	def map[B](f: (A) ⇒ B): Option[B]
    def flatMap[B](f: (A) ⇒ Option[B]): Option[B]
{% endhighlight %}

