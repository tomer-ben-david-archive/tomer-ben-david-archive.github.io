---
layout: news_item
title: "Partially Applied Functions - Fully Understandable Example"
date: "2014-05-23 10:25:10 +0200"
author: Tomer-Ben-David 
version: 1.0.0
comments: true
categories: [scala,functional-programming]
---

So you want to *partially apply* a function but don't know why?  This post is for you.  Here we will show you why you did need to partially apply a function (why it helped you).  And how nice and easy this process can be.

Although in *scala* the process for partially applying a function is just as complex and as encrypted as far as they could think of we will try to make it easy for you.  (they really thought hard how to make it encrypted and un-remembable).

So let's dig in.

But first I would like to ask you to repeat the mantra:

partial-applied-function, partial-applied-function, partial-applied-function, partial-applied-function, partial-applied-function, partial-applied-function, partial-applied-function, partial-applied-function, partial-applied-function.

Now that you are familiar with it let's repeat the scala partially applied function mantra.

oh-lord-its-with-space-and-underscore_, oh-lord-its-with-space-and-underscore_, oh-lord-its-with-space-and-underscore_, oh-lord-its-with-space-and-underscore_, oh-lord-its-with-space-and-underscore_, oh-lord-its-with-space-and-underscore_, oh-lord-its-with-space-and-underscore_, oh-lord-its-with-space-and-underscore_, oh-lord-its-with-space-and-underscore_.

Let's continue to dig in.

Let's say you want to load some configuration from disk and lets say this configuration is in the form of properties.  You wish to have a primary file and a secondary, like external configuration file which will override internal.
(For real life if you use java I would recommend you to use already existing mechanisms such as spring who would do that for you or scala typesafe config manager which would also do that for you).  But for the sake of the example lets use plan *properties*.  

Lets first load the configurations into our properties.

{% highlight scala %}
	val internalProps = new Properties()
	val externalProps = new Properties();
	intenralProps.load(new FileInputStream(new File("external.properties")))
	externalProps.load(new FileInputStream(new File("internal.properties")))
{% endhighlight %}

Now lets load a properties with default - *no partially applied func here*.

{% highlight scala %}
	val someValFromConf = externalProperties.get("key", internalProperties.get("key")) // note that the internal properties are serving as the default.
{% endhighlight %}

Now let's partially applly props to already contain the internal defaults