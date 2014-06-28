---
layout: news_item
title: "Honey I lost the api project"
date: "2014-06-23 21:25:12 +0200"
author: Tomer-Ben-David 
version: 1.0.0
categories: [scala,software-construction]
---

If you are like me and you have some java background then you like your projects structured in this way:

{% highlight scala %}
mynice-project-api
mynice-project-impl

myothernice-project-api
myothernice-project-impl
{% endhighlight }

Because in this project construction methodology you have a clear separation between your api's and implementations.  Or
so to say you can use your favorite build tool to have your project compile against the `api` and run with the `impl`.
And for the bored programmers of our time you can event invest the time to replace your `impl1` by `impl-mock`.  However,
I'm taking you as a serious developer transitioning into a more `fp` language, like `scala`.
However if you have transitioned to `scala`.  So in scala we are very used to having `traits` everywhere, and hell, i mean
everywhere.  Not a single `impl` without an `interface`.  However if you noticed then in 99% of cases the traits are in same
`files` as the implementations.  Not to mentioned you have the `sealed` option which will force you to have it in same file.
And thus the `-api` `-impl` is gone.  So lets acknowledge it at least.

We have disregarded the sepration between the `-api` and `-impl` because we use traits all over the place.  And you know what?
So far its working well for us, i mean, any serious programmer will enforce coding to an interface, so this separation of projects
is actually redundant for us, we even got half the amount of projects to maintain.  Seriously how many times did you really replace that
`impl` project with another one? I've seen hundreds of projects with that seperation and in none of them it was actually replaced. so
lets at least acknowledge it.  And with the new programming paradigm, its so easy to create `interfaces` we do it all over, and we don't need
another project to convince us we need to create such a new interface.

And you know what? if you really really need such separation in a specific place go ahead, but no reason to have it all over the place cluttering
our project workspace.