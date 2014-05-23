---
layout: news_item
title: "Dear lord - yesterday I partially applied a function, why like this?"
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
extenralProps.load(new FileInputStream(new File("external.properties")))
defaultProps.load(new FileInputStream(new File("default.properties")))
{% endhighlight %}

Now lets load a properties with default - *no partially applied func here*.

{% highlight scala %}
val someValFromConf = externalProperties.get("key", defaultProperties.get("key"))
{% endhighlight %}

Now let's partially apply props to already contain the internal defaults

{% highlight scala %}
def getOrDefault(externalProps: Properties, defaultProps: Properties)(key: String) = props.externalProps.getProperty(key, props.defaultProps.getProperty(key))
val get = getOrDefault(externalProps, defaultProps) _ // nasty underscore --> partially applying alarm.
{% endhighlight %}

Well here we first defined a method named *getOrDefault* which is aware of both external and default properties, so far so good, I mean, we are talking here about *File*, *FileInputStream*, *Properties*, *def*, all is clear and nice and dandy isn't it???

**AND HERE COMES THE TWIST IN THE STORY!! THERE IS AN UNDERSCORE!**

*The story of a method called only with some of its arguments*

*getOrDefault* accepts three arguments, *externalProps* and *defaultProps*, and a *key*, what would happen if we called it with only a single argument? it would not compile right? but we added **THE UNDERSCORE**.

So as we added the underscore *scala* understands it should **PARTIALLY APPLY** meaning it calls them method with a single argument and as we have an **_** it does not run it.  Also note we are assigning the return value to a **val** so we have now got a new method called **get** and as we already passed to its origin method the first argument, we can call get only with the key.

so we can call *key* method any number of times we want, isn't that nice, its already aware of the first two arguments.  That's the *functional* way of doing so.  If we wanted to do so in *java* we would need to create an object initialize it with some members and call it, here all got shorter, and *immutable*.

So now we can call *get* like this:

{% highlight scala %}
val value = get("key1") // low and behold, the function is already aware of the external,internal props.
val value = get("key2") // low and behold, the function is already aware of the external,internal props.
{% endhighlight %}