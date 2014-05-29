---
layout: post
published: true
title: Preventing double clicks in angular
comments: true
categories: 
  - angular
  - directive
  - javascript
---

Last week I was working on a SPA made with Angular and I was incurring in a classic problem: the double click.

You know the situation: a button is clicked, a call is made to the server to create a new order and after the call finishes the form closes. In my case if you were fast enough you could click a couple of times on the button before the call finished, resulting in multiple calls and multiple orders.

To solve this problem once and for all I decided to try my hand at creating a custom directive. Looking in Angular the source code I searched for the **ng-click** directive and modified it to create [**ng-single-click**](https://github.com/Bjornej/angular-single-click).

This directive can be used by simply substituting ng-click with ng-single-click. If the invoked expression returns something similar to a Promise (meaning it has a finally function) it will automatically ignore all the clicks on the element between the start of the promise and its fulfillment or rejection.

PS: After some tests I noticed that stopping clicks without giving the user a hint that work is currently being done is not a good user experience so I created a [second](https://github.com/Bjornej/angular-animated-click) version of this directive that adapts [ladda-button](http://lab.hakim.se/ladda/) to show a working animation in the clicked button.