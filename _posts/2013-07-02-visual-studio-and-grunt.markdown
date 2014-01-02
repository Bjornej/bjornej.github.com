---
layout: post
title: "Visual Studio &amp; Grunt"
date: 2013-07-02 22:15
comments: true
categories: ["Visual Studio","grunt","vspackage"]
---

Developing Web applications in a .Net shop means only one thing : Visual Studio.

While VS is truly an help when you are coding in C# it leaves something to desire when you are on the other side of the fence, in particular when writing Javascript.

Let's face it support for some of the current technologies we use is at the moment not present or not well supported:

 - Intellisense for javscript exists and works, but doesn't recognize [requireJs](http://requirejs.org/) or AMD modules 
 - SASS is not supported( but it is in WebMatrix which is a free IDE by Microsoft)
 - some of the tools which are common in web development are not supported (bower, grunt,...)

This can be frustrating sometimes but some time ago I learnt how to extend Visual Studio through Vspackages, extensions that allow developers to create additional commands or tools.

 Armed with this knowledge I set out to create a simple package to better integrate Grunt in my workflow. After a week of experiments I am happy to present [GruntLauncher](https://github.com/Bjornej/GruntLauncher).

What does GruntLauncher does? Well basically when you right-click a Gruntfile in the solution explorer it parses all the defined commands and shows them in the contextual menu.

<img src="/images/GruntLauncher.png" />

If you click one of the commands the it launches them on the command line redirecting the output to VS Output Window.

Hope someone else finds it useful as I do. 

**UPDATE** : To have better error handling when unable to parse the gruntfile I just released a new version which will allow you to launch the default grunt commandin every case.