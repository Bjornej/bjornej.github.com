---
layout: post
published: true
title: Simulating actions on many elements in Javascript
comments: true
categories: 
  - javascript
  - application development
  - spa
---

Sometimes, when developing an application, especially in certain fields you'll receive the same old request:

	I want to select all the element in the table and [print|delete|close|whatever] them

While this request is reasonable (sometimes) it carries a lot of problems that must be solved to implement it correctly:

- how many elements can be selected together ? 10, 20, 50, a thousand?
- how many users the system has that can use this feature together
- does the user have to see the status of his pending jobs?

This type of feature can easily cause problems if not tought well. Imagine a user coming in, selecting a thousand rows and clicking "Print". Now the system has to print maybe a couple thousand pages which may take some time. 

If the action can be completed in a small time usually there is no problem but imagine a user that gives the command and doesn't receive a timely response. Usually one of the thing he tries is to execute the action again which means your system is now printing double the pages. 

This problem can be even compounded if many users try to use the same function swamping your application with pending requests until it grinds to a halt, especially if these jobs are processed by a queue that cannot be emptied sufficiently fast.

In some of this cases you'll find that a really simple solution can be used that can be simply called "cheating". Suppose you have the list of elements to process and for each of these you have to make a AJAX call to the server. Instead of creating a new action to process all the element in a batch you can simply chain all the request together to execute in sequence and show an update on screen in this way:

    var d = jQuery.Deferred();
    var p = d.promise();
    var i = 0;
    for (i = 0; i < chosen.length; i++) {
      p = p.then(_.bind(function (index) {
        return $.post("youaction", function (response) {
		  "SHOW AN UPDATE ON SCREEN"
        });
       },this, i))
    }

    d.resolve();

As you can see all we do is create an initial promise through jQuery and then proceed to concatenate a Promise for each element to process. The last line simply starts the process by resolving the first request and the starting with the second and so on.

While I called this solution "cheating" as it doesn't really process in batch all the element it has some nice properties:

- it solves the user problem fully as it allows him to select some elements and apply an action to them in bulk
- it doesn't swamp the system with huge requests, as only one element at a time is processed 
- it eliminates the problem of having to stop the user from requeing the same batch because he thinks it is taking too much, or from having to implement a way to show the user the status of his pending jobs.

All in all a simple solution that pleases almost everyone. The only drawback is that if the user closes the browser not all the elements will be processed but in many cases you'll find that this doessn't matter.
