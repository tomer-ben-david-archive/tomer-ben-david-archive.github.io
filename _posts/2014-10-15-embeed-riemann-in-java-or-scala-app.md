---
layout: news_item
title: "Embeed riemann in java or scala app"
date: "2014-10-15 02:22:12 +0200"
author: Tomer-Ben-David 
version: 1.0.0
comments: true
categories: [monitoring]
---

Have you been finding yourself lately coding complex logic for deciding when to send an `alert`? If yes `riemann` is for you.  You can define cewl `DSL`s for `CEP` logic for when to send an alert (or whatever else).

Only two caveats with it are:

1. It's not distributed.  Meaning ofcourse you can `shard` your data and have multiple `riemann` servers, however I would rather it be a cluster.
2. What if for whatever reason I cannot reach `riemann` server, this means alerts are not sent.  For that reason you want also some `alert` sending logic in your client code.  So instead of coding your own alert logic in your client code, I would suggest `embeeding` riemann in your local process.  That would mean however that you have no control over which `DSL` users which be coding into your local riemann server thus it will consume `memory/cpu` based on `DSL`s defined, currently no way over it except for convention, use simpler rules on client.  Do not query for events 5 weeks ago.

Embeeding riemann with an example:

1. Including riemann in your maven dependencies.

{% highlight xml %}
        <dependency>
            <groupId>riemann</groupId>
            <artifactId>riemann</artifactId>
            <version>0.2.6</version>
        </dependency>
{% endhighlight %}

place `riemann.conf` in project root folder.

example `riemann.conf`

{% highlight clojure %}
; -*- mode: clojure; -*-
; vim: filetype=clojure

(logging/init {:file "riemann.log"})

; Listen on the local interface over TCP (5555), UDP (5555), and websockets
; (5556)
(let [host "127.0.0.1"]
  (tcp-server {:host host})
  (udp-server {:host host})
  (ws-server  {:host host}))

; Expire old events from the index every 5 seconds.
(periodically-expire 5)

(let [index (index)]
  ; Inbound events will be passed to these streams:
  (streams
    (default :ttl 60
      ; Index all events immediately.
      index

      ; Log expired events.
      (expired
        (fn [event] (info "expired" event))))))
{% endhighlight %}
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

