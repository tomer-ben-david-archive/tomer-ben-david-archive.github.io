---
layout: news_item
title: "Log failures in scala getorelse, try, future"
date: "2014-06-28 21:12:11 +0200"
author: Tomer-Ben-David 
version: 1.0.0
categories: [scala,functional-programming]
---

Hello, so yo wanna log a failure in a less intrusive way than `pattern-matching` and in a more elegant way in scala but don't know how?  Read below...

Pattern matching is good, but, its for newbies.  If you are a serious scala developer you should use the more advanced `fp` programming tools provided.  For example - `for` :)  

But, you may ask, when I use the plain `fors` I loose the ability to do something with the failures, and, yes, its not straight forward, and indeed when using `for comprehension` its not immediate to get the failure, but only successes.  Fortunately the previous sentence is incorrect, and `for comprehension` in scala provides you a way to get the failure.  So here is an example of how to use `for` doing something with the `successful` value and printing to log the errornous value.

{% highlight scala %}
    for {
      futureResult <- Try(Future[MyResponse](doSomeOp())) // get back the value of the try which is a future.
    } yield {
      futureResult // if successful we get to here, and we return the future result.
    } recover {
      case e => LOG.warn(e.getMessage) // in case of an error we get to recover and we print the exception. vwalla!
    }	
{% endhighlight %}