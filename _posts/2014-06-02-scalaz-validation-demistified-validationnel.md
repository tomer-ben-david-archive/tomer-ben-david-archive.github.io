---
layout: news_item
title: "Scalaz validation demistified (although some clouds are still upon it)"
date: "2014-07-02 20:35:11 +0200"
author: Tomer-Ben-David 
version: 1.0.0
comments: true
categories: [scala,functional-programming]
---

You can use scalaz `ValidationNel` (non empty list guaranteed) to hold one of two values, `success` or `failure `one.  Basically you will have two types involved.

The success type.
The failure type.

The success type will be the actual type you return, the one you want.
The failure type can be `String` with a message (this is what most of examples you will encounter will show), but in real life ofcourse you would not want just a `String` but a type which will hold various stuff about your error, like error type from enum maybe and more details on error, could be even the stacktrace for better debugging, and a message ofcourse.

So lets say our actual type is `Produce` (the success type).  And our failure type (i'm falling into this like the others) is `String`.

When you return something from your method you will use `successNel` for the successful type and (you guessed) `failureNel` for the failure type.  The part which might mix you up (see below example so will be clarified) is that when you return the successful type you use successNel[FailureType] - thats right you specify the failureType because the success type is already in there.  And when you return the failureType you use failNel[SuccessType] **not intuitive at all!** but it works.

{% highlight scala %}
import scalaz._
import Scalaz._

def myMethod: ValidationNel[String, RealResult] = {
	parsedVal = parseIt()
	parsedVal match {
		case Success(s) => s.successNel[String] // String is our failure type - bah that's the way it is!
		case Failure(e) => e.getMessage.failNel[RealResult] // bah! passing in type of real result on failure while failure is a string.
	}
}
{% endhighlight %}

That's all for today.  And if you want to repeat the mantra after all then, repeat after me:

ValidationNel, ValidationNel, ValidationNel, ValidationNel, ValidationNel, ValidationNel, ValidationNel, ValidationNel, ValidationNel, ValidationNel, ValidationNel, ValidationNel, ValidationNel.