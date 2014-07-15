---
layout: post
published: true
title: A Modern style checkbox
comments: true
categories: 
  - css
  - scss
  - modern
  - animations
---

As I was working on a project I had to create a personal area page when a user could set some options to tweak the behaviour of the program. 

As it always happens some of these options were of the type **enable/disable behaviour** which can be modelled with a simple checkbox. 

While the checkbox works I felt the need for a more stylish solution and decided to try to replicate in CSS the Windows 8 checkbox.

First thing I searched the internet  looking for a ready solution and found something close to what I wanted in [Metro UI](http://metroui.org.ua/forms.html), which has a checkbox with the correct style but with a major defect: when clicked the checkbox switches state immediately ruining the overall effecct.

Solving this problem was quite easy and it took only the addition of a css animation on the slider movement and the slider color change.

The result and also the modified CSS code cand be seen here:

<p data-height="213" data-theme-id="0" data-slug-hash="bszrE" data-default-tab="result" class='codepen'>See the Pen <a href='http://codepen.io/paonic/pen/bszrE/'>bszrE</a> by Paolo Nicodemo (<a href='http://codepen.io/paonic'>@paonic</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//codepen.io/assets/embed/ei.js"></script>

Two things in this example are interesting to note:

* an additional span is required to style everything correctly as some browsers don't support the *:after* pseudoselector on an input field (Firefox if I remember correctly)
* the animated transition is set not only on the span position but also on the original span so even the background color is animated thus giving a much more natural effect