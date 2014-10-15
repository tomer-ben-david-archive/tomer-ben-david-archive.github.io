---
layout: news_item
title: "Embeed riemann in java or scala app"
date: "2014-10-15 02:22:12 +0200"
author: Tomer-Ben-David 
version: 1.0.0
comments: true
categories: [monitoring]
---
# Introducing Riemann

Have you been finding yourself lately coding complex logic for deciding when to send an `alert`? If yes `riemann` is for you.  You can define cewl `DSL`s for `CEP` logic for when to send an alert (or whatever else).

Only two caveats with it are:

1. It's not distributed.  Meaning ofcourse you can `shard` your data and have multiple `riemann` servers, however I would rather it be a cluster.
2. What if for whatever reason I cannot reach `riemann` server, this means alerts are not sent.  For that reason you want also some `alert` sending logic in your client code.  So instead of coding your own alert logic in your client code, I would suggest `embeeding` riemann in your local process.  That would mean however that you have no control over which `DSL` users which be coding into your local riemann server thus it will consume `memory/cpu` based on `DSL`s defined, currently no way over it except for convention, use simpler rules on client.  Do not query for events 5 weeks ago.

Embeeding riemann with an example:

## Including riemann in your maven dependencies.

{% highlight xml %}
<dependency>
    <groupId>riemann</groupId>
    <artifactId>riemann</artifactId>
    <version>0.2.6</version>
</dependency>
{% endhighlight %}

## place `riemann.conf` in project root folder.

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

## In your main() method start up riemann in your process (or in your webapp)
{% highlight java %}
public static void main(String[] args) throws Exception {
    riemann.bin.main(new String[]{"riemann.config"});
}
{% endhighlight %}

## Sending example event to this local `riemann`
 
{% highlight java %}
RiemannClient c = RiemannClient.tcp("localhost", 5555);
c.connect();
c.event().
        service("fridge").
        state("running").
        metric(new Random().nextDouble()).
        tags("appliance", "cold").
        send();

c.query("tagged \"cold\" and metric > 0"); // => List<Event>;
c.disconnect();
{% endhighlight %}

## Lets view some results - Install a local riemann dash
I don't want to clutter my local environment with it so i'll just use `docker` to install `riemann-dash`

{% highlight bash %}
sudo docker run -p 4567:4567 davidkelley/riemann-dash

Unable to find image 'davidkelley/riemann-dash' locally
Pulling repository davidkelley/riemann-dash
7911459329f4: Download complete 
b2cec74ebcfd: Download complete 
b56feebb5913: Download complete 
== Sinatra/1.4.5 has taken the stage on 4567 for development with backup from Thin
{% endhighlight %}

Then navigate to: [http://localhost:4567/](http://localhost:4567/)
next this is a little tricky.  You will see a big `Riemann` word on your screen. **Click it**.  Then click `e` this will edit it.  Choose `Gauge` in the textbox type `true` this means your query filter is for everything.  Next use the client to send some more data you will see this metric changes online realtime with your data!

source code available at: [github source code](https://github.com/tomer-ben-david/TestEmbeedRiemann)