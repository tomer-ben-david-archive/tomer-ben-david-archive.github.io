---
layout: news_item
title: "Book review - functional programming in scala"
date: "2014-05-14 02:12:52 +0200"
author: Tomer Ben David 
version: 1.0.0
categories: [scala, functional-programming]
---

This is the book we have been waiting for.

The good: It provides what you wanted and what it's title is - "Functional programming in scala - indeed."
The bad: No jokes, no real fun.  I like books with jokes and fun, the author does a good job in describing the issue in a very clear way, but hey couldn't they put some fun into the book? (kinda learn you a haskell for a great good)

CHAPTER 2: A very good job in describing functions.  In currying, partial functions, how generics or polymorphic functions as they are named play a big role.  Why most of framework functions are like someFunc(A, B, C).  Does a real good job on this.  It's still an introduction to the whole subject, but overall, by the end of this chapter, you will get to know tail recursion, generics (or type parameters) currying, partial functions, how to compose functoins, why its like solving equations and stuff like that.

CHAPTER 3: Lot of excercies in this chapter.  You have to decide at this point if you are going to go through all excercises which will take a huge amount of time, but you will definetly profit from them they are great for getting familiar and understanding this hard material.  Now as for the chapter, again, it does a good job explaining ADT, *abstract data types*.  While is does not go a long way to describe this vauge *ADT* theorethical concept, or the concept itself, it describes how you define such ADT in scala.  You then have to do some deduction in order to understand this generic ADT concept.  Now as for the examples these are List, Tree.  Basically in List you have some multiple constructors where you can create such lists, and do some operations on them like Cons.  It does some work on describing how to keep the implementation efficient as you want, does it in tail recursion, and the impelementations are clean.  In general it also emphasizes on the concept that whenever you see some repeating code you should generalize it and in case of functional programming you do it with extracting the operations which *look alike* let it be add or mul and extract it into a function parameter 'f' which you pass into the function any local varialbles you would use go into arguments into that 'f'.