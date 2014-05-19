---
layout: post
published: false
title: GruntLauncher 1.6 is out
comments: true
categories: 
  - visualstudio
  - grunt
  - npm
---

A little late, the new version of GruntLauncher is available on Visual Studio gallery.

This new version brings three new features:

- the ability to launch commands in the same directory as your gruntfile. Some people complained (rightly) that the commands were always executed at the project root and this was not always right because the gruntfile sat in a subfolder.
- support for grunt targets. Now if you have a task with at least to targets all will be shown as options to invoke directly
- npm install support thanks to [Mads Kristensen](https://github.com/MadsKristensen). Now when right clicking on you package.json file you will see the option to install all the specified packages (npm install).

As a news the next version of GruntLauncher will almost certainly get a rename as currently it does more than the name implies.

