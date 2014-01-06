---
layout: post
published: false
title: GruntLauncher 1.1 is out
comments: true
---

As the title says GruntLauncher 1.1 is out and available on VisualStudio Gallery to update.

### What's new

This version brings two improvements: 

1. execution of grunt task is no more blocking (this was due to a bug in node for windows but newer version have solved it so make sure to have a recent version installed for example I work with 0.10.22)
2. long running tasks like grunt watch can be started and continue to run in background. The command will be checked and clicking again on it will stop the process 