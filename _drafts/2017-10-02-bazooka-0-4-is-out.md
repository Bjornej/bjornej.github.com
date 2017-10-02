---
layout: post
comments: true
published: true
title: Bazooka 0.4 is out
---
After more than nine months a new version of Bazooka is ready!

What's new this time? **Task Templates**.

While deploy tasks allow you a certain degree of flexibility thanks to the optional *Install* and *Uninstall* powershell scripts sometimes this is not enough. Covering all these possibilietes by creating always new task types was not efficient (like mialTask or DataBaseDeployTask) so we opted for a generic structure that allows you to create a task template by compiling

- list of parameters 
- script to execute

