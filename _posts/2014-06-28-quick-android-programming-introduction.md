---
layout: news_item
title: "Quick android programming introductoin"
date: "2014-06-28 09:12:11 +0200"
author: Tomer-Ben-David 
version: 1.0.0
categories: [android]
---

Hello, so yo wanna do some android development and is bombed by `intents`, `activities`, `services` etc?  Lets tidy up the stuff in our head a bissale.  You need to understand there are a very few concepts you have to understand in order to start android development.  These concepts are very few but you must first understand them, otherwise you get lost.  So lets get done with it.

First thing you will notice is that the following components are very decoupled.  I mean the next concepts solve a problem, how to build an android app (they can also solve a generic problem on how to build an app), but they are customized for mobile apps.  So when you ask yourself why do I need an intent when I can just do something else instead, you must understand that its very nice to have an android app decoulped like that becuase it helps in many ways, instead of sending a message inside your app you use an `intent` and in the same way you can send an intent to take a picture so its a common ground the language of the mobile.

1. **Android application** - Let's treat it as a web site this is your whole application, although you can modularize your app into multiple apps (for example an app that handles the data and an app that handles the ui), for the sake of the concept an android application is similar to a whole web site.  Now an activity has multiple states (complex), `paused` for example is when its like you long click the mid button and thus you see your app partially on screen, this is the `pause` state.
1. **Activity** - treat it as a web page or a single screen that the user will interact with.
1. **Intent** - Either inside your app or external, you want to take a picture, this is an action cross component, you will not start an `intent` for every button click, but if it should trigger another app showing up like `contacts book` then this is the way to notify the android app manager this is what you wish to do.
1. **Service** - Pretty much parallel to `Activity` however without UI.  Services do not run on their own thread they run in your own UI thread, that means if you should be aware of it and you should not run long running processes in it.  If you do need your service to run in its different thread you should be using `worker threads`
1. **Broadcasts** - In this way you can get notifications about general events such as `system booted up` note that there is no notion in android for a service which starts up in startup and the `OS` will be responsible for it being up, you should do that by means of listening to broadcase system booted up and start up your service (and handle its failures).
1. **Widget** You know what a `widget` is i don't need to explain to you, what you need to be aware of is that programming model is very simple component much similar to broadcasts its listening to events and reacting.

In addition you should be aware that every app has its own process, its own `linux user` is practically created for it (app_id123).
