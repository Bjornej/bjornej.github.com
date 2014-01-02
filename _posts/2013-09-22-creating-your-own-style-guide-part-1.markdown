---
layout: post
title: "Creating your own style guide: Part 1"
date: 2013-09-22 20:34
comments: true
categories: ["css","sass","grunt","style guide"]
---

Most of the times when you are beginning to create a site the easiest thing to do is to start from a good foundation like [Bootstrap](http://getbootstrap.com/) or [Foundation](http://foundation.zurb.com/) and proceed from there, tweaking it as needed.

In some rare cases, for example if you have to create a series of sites with the same look&feel or if you are working on something a little bigger, it's necessary to create you own css style guide.

 
In the past month I had the opportunity to create a style guide so I decided to write down some notes on how to proceed.

## Part 1: the style

The first thing to do when creating a style guide is to decide what look are we going to try to create: will it be modern? will it be classical ? Flat?.

The best thing to do in this phase is to try to browse the internet and identify the look we are trying to recreate observing blogs, news sites and other style guides.

This process can be tedious and you will feel the urge to begin working without a clear idea of how the end result should look. While you could start immediately and decide later about the details this will cause you to backtrack a lot of times and rewrite many times the same sections when changing idea ( trust me, I've redone some parts four times ).

## Part 2: The tools

First thing to do when beginning to work on the style guide is to "prepare the worktable" deciding the tools to use. You can decide to work in pure CSS but I suggest to use a CSS preprocessor, a tool that extends CSS with functions and variables, and then compiles to pure CSS.

There are three main CSS preprocessors:
 
 - **LESS** : [LESS](http://lesscss.org/) was one of the first CSS preprocessors and the one with more tools available. It can also work directly in the browser by including the less.js library in you page.
 - **SASS**: [SASS](http://sass-lang.com/) is another CSS preprocessor with two different available syntaxes: one more resembling CSS and one which is more clean. While SASS has some additional features that LESS it shines when used with [Compass](http://compass-style.org/), a library of functions that will help you developing your css easily. 
 - **Stylus** : [Stylus](http://learnboost.github.io/stylus/) is another CSS preprocess by the creator of LESS, with many more capabilities but with a syntax that differs a lot from standard CSS.

For my style guide I decided to work with SASS and Compass as I was already familiar with them and they were easy to setup on windows. Sometimes in this articles I will use Compass functions but I'll try to explain everytime what they are doing and what output they produce.

Before starting to work there's another thing to do. To facilitate the compile-reload-test cycle I strongly suggest to use grunt with the  grunt-contrib-watch plugin and another plugin to compile your css ( grunt-contrib-compass if you decided to use compass or an equivalent one ). With this setup you can configure grunt to compile your style guide every time you save and automatically reload the browser.

Now we're ready to begin, but this article ends here. Next time we will start the foundation of our style guide : the typography.   