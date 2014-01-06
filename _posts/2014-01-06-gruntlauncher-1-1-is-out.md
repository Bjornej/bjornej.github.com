---
layout: post
published: true
title: GruntLauncher 1.1 is out
comments: true
categories: 
  - gruntLauncher
  - grunt
  - visual studio
---

As the title says GruntLauncher 1.1 is out and available on VisualStudio Gallery to update.

### What's new

This version brings two improvements: 

1. execution of grunt tasks is no more blocking (this was due to a bug in node for windows but newer version have solved it so make sure to have a recent version installed, for example 0.10.22)
2. long running tasks like grunt watch can be started and run in background, writing the output in the output pane. The command status will become checked and clicking again on it will stop the process 

![Running task](/images/gruntLauncherDetail.png)