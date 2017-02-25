---
layout: post
comments: true
published: true
title: Ten thousand deploys
categories:
  - continuous integration
  - continuous delivery
  - Bazooka
  - automated deploy
---
Less than two years. 

I started developing professionally six years ago and got a job fresh out of university. At the time I didn't know much about all the topics surrounding development: continuous integration, continuous delivery, capacity planning, etc.. .

When I started developing my first application what was taught to me was: verify that it builds and deploy it to a network folder with the Visual Studio *Publish* option. It worked fine as I was working alone but it had numerous problems:

- a build was not reproducible exactly, as it didn't match exactly what was in source control but what was on my computer
- I had to remember to build and deploy the correct configuration which was different from the one used to develop
- in a strange case my computer was the only one able to build the application due to specific version of a compiler only I had installed

All these things summed up to many little problems so I started looking for better solutions, reading books about continuous delivery and deployment. At the same time the number of applications we were working one augmented magnifying the problems we had so I started working on Bazooka a tool to automate application deployments.

Last week I was looking at its statistics page and noticed one thing: in less than two years (from June 2015 to February 2017) over thirty developers worked on ninety applications making over ten thousand deploys.


![graficoDeploy.png](/images/graficoDeploy.png)

As you can see usage has been steady with an increase during summer months as many of our applications have a usage peak in the summer.

Over 90 applications were published some of which are very active while others are in maintenance mode and experience only a few deploys per year

![grafico2.png](/images/grafico2.png)

During these two years many bugs have been fixed and features added but there still are some that could make for an easier deployment experience like release promotion through enviroments but this is an argument for another post

