---
layout: news_item
title: "Book review - functional programming in scala"
date: "2014-05-14 02:12:52 +0200"
author: Tomer-Ben-David 
version: 1.0.0
categories: [scala, functional-programming]
---

This is the book we have been waiting for. By saying the book is a university level course I mean you have the do the exercises to understand it, so treat it as a course.

The good: It provides what you wanted and what it's title is - "Functional programming in Scala - indeed."
The bad: No jokes, no real fun. I like books with jokes and fun, the author does a good job in describing the issue in a very clear way, but hey couldn't they put some fun into the book? (kinda learn you a Haskell for a great good), its explaining everything yes i just wonder if it can be explained in a simpler way, I think it can be I saw a few lectures were it was explained in a simpler manner, but as the book goes such a long way its an excellent reference for functional programming in scala, it will dive into all subjects, consider stuff not explained before so its plain extended reference.

CHAPTER 1: Introduction to functional programming, an example of how he pushes out the printing action from the actual computation function.

CHAPTER 2: A very good job in describing functions. In currying, partial functions, how generics or polymorphic functions as they are named play a big role. Why most of framework functions are like someFunc(A, B, C). Does a real good job on this. It's still an introduction to the whole subject, but overall, by the end of this chapter, you will get to know tail recursion, generics (or type parameters) currying, partial functions, how to compose functions, why its like solving equations and stuff like that.

CHAPTER 3: Lot of exercises in this chapter. You have to decide at this point if you are going to go through all exercises which will take a huge amount of time, but you will definitely profit from them they are great for getting familiar and understanding this hard material. Now as for the chapter, again, it does a good job explaining ADT, *abstract data types*. While is does not go a long way to describe this vague *ADT* theoretical concept, or the concept itself, it describes how you define such ADT in Scala. You then have to do some deduction in order to understand this generic ADT concept. Now as for the examples these are List, Tree. Basically in List you have some multiple constructors where you can create such lists, and do some operations on them like Cons. It does some work on describing how to keep the implementation efficient as you want, does it in tail recursion, and the implementations are clean. In general it also emphasizes on the concept that whenever you see some repeating code you should generalize it and in case of functional programming you do it with extracting the operations which *look alike* let it be add or multiplication and extract it into a function parameter 'f' which you pass into the function any local variables you would use go into arguments into that 'f'.

CHAPTER 4: Handling errors: The author acclaims we are getting back to C style error handling which is return values instead of exceptiosn in java, however as we get much powerful tools to handle these "return codes" and to force callers to handle them, it appears to be the correct path. This item has bugged me a lot when I read in "It may be easy to jump to the conclusion that once we start using Option , it
infects our entire code base" Now I was delighted to see the author has referenced, that, I wouldn't expect that in a book really, usually books deals with the trivial examples or how can I call them the straight forward path and not what the extreme people would think about.

CHAPTER 5: Strictness and Laziness: Well in functional programming you focus on declarative code, so its best if you would not know when the stuff is evaluated, it helps streams (infinite) what is strict and non strict.

CHAPTER 6: Purely functional state: A random number generator as an example (it kina non pure has internal state mutates stuff after all every time you call its its just crazy returning you a different number) , so you'll make a pure version of it, curious to know how? hmm well its simple, a bit of lie, but that's how it goes, the API will just compute the next random number return you with new number and state you provide it in with the state here yes we are now declared as pure.

CHAPTER 7: How do you design FP parallel API in scala? how explicit is your API about allowing clients to control the forks and joins of the parallel computation? What are the trade offs of this API? The chapter aims to answer this. A challenging chapter, I had to digest it a couple of times before getting it. There was an effort to describe it in a clear way, thanks for the effort, result not so clear.