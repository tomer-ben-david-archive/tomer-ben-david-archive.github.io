---
layout: news_item
title: "Riemann in practice"
date: "2014-10-29 02:22:12 +0200"
author: Tomer-Ben-David 
version: 1.0.0
comments: true
categories: [monitoring,riemann]
---
## Run riemann locally

Running a quick clone of riemann locally is great for practice.

`git clone riemann`

change directory to the directory where riemann is.
make sure you `lein` installed.

`lein run`

## Connect to riemann REPL

in another console tab run

`lein repl :connect localhost:5557`

## Loading a plugin into riemann conf

In the directory you have cloned riemann into edit `riemann.config` and add just below `; vim: filetype=clojure`

{% highlight clojure %}
(load-plugins)
{% endhighlight %}

Now start riemann again with `lein run` and see that the plugin is loaded in console.

