---
layout: post
published: false
title: Preventing double clicks in angular
comments: true
categories: 
  - angular
  - directive
  - javascript
---

Last week I was working on a new project and decided to use angular  instead of Backbone, to learn how it works beyond the simple examples.

After the first  the first iteratoion was complete we proceeded to test the site and found a classic bug: the double click.

You know the problem: when a button is clicked a call is made to the server to do something like create a new order or modify the details of something but if the acction is done two times with the same parameters it can return an error or even worse create two objects.

After a little thinking I decided that angular directives could help me solve the problem in a simple way so after some digging I created angular-single-click.

This directive allows you to use it like ng-click but if the invoked expression returns something similar to a Promise (meaning it has a finally function) it will automatically ignore all the clicks on the elemnet done between the start of the promise and its fulfillment or rejection.

If you want to try it you can download the github repo with the sample.

PS: After some test I noticed that stopping clicks without giving the user a hint that work is currently being done is not a good user experience so I created a second version of this directive that adapts ladda-button to show a working animation in the clicked button.
