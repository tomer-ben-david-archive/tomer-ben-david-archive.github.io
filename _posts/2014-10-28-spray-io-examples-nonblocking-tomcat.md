---
layout: news_item
title: "spray.io examples, nonblocking, tomcat, and more"
date: "2014-10-28 02:21:12 +0200"
author: Tomer-Ben-David 
version: 1.0.0
comments: true
categories: [functional-programming,scala,spray,akka]
---
akka-spray-tomcat-example
=========================

akka spray tomcat example in scala

## Having serialization done by json spray for you

Lets say you have the following case class (important its a case class for regular classes you will need something a little different)

{% highlight scala %}
case class Person(val name: String)
{% endhighlight %}

and you want json-spray to serialize it you will need the define the following implicit
you can just define it beside your case class in the same file.

{% highlight scala %}
object PersonJsonImplicits extends DefaultJsonProtocol {
  implicit val impPerson = jsonFormat1(Person)
}
{% endhighlight %}

Then you can use toJson on your pimped class:
** You must import spray.json._ otherwise `toJson` won't be recognized! **
{% highlight scala %}
import spray.json._
new Person("somename").toJson
{% endhighlight %}

note the `1` in `jsonFormat1` this means your case class has single parameter if it had 2  you would use... `jsonFormat2` :)

## Async with Future
Remember: spray uses a single actor to handle incoming requests.  This means you cannot run any blocking code in the handling actor.

{% highlight scala %}
// In spray main request handler actor.,
complete {
  // NO BLOCKING CODE HERE
}
{% endhighlight %}

So you have two options (or 3).
1. Route the request to another actor handle it there, use ask `?` pattern to get back a future.  `complete {}` will then know to handle the `Future`. (nothing special required).
2. Use directly a future - I like that one better its more clear.

{% highlight scala %}
complete {
  Future {
    Thread.sleep(5000) // blocking example.
    "tada.."
  }
}
{% endhighlight %}

you may need to define above the `implicit executionContext` that the `Future` will run in and also the `implicit timeout`

## Async with `detach`
now if you want to handle your request in an async way you don't really need to create actors
spray can do that for you just wrap your handling with `detach {` as following:

{% highlight scala %}
       detach() { // this make the below operation async (note for your app to really be async you should  not block the underlying thread!)
          respondWithMediaType(`text/html`) { // XML is marshalled to `text/xml` by default, so we simply override here
            complete {
              <html>
{% endhighlight %}
Note that although we called `detach()` if you have inside the code which detach calls some blocking code
this would still mean it would block the thread on which detach is running therefore if you do any blocking `get` you should

still wrap it in a future and have a callback for it (same as you should not block from within handling of a message in an actor).

source code available at: [github source code](https://github.com/tomer-ben-david/akka-spray-tomcat-example)