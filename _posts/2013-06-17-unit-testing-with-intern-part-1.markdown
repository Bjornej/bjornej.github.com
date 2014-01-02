---
layout: post
title: "Unit testing with Intern: part 1"
date: 2013-06-17 21:47
comments: true
categories: ["unit testing","javascript","intern"]
---


Some time ago i read a tweet mentioning a new library to write unit tests in Javascript, [Intern](http://theintern.io/). 

At the moment I didn't have much time and I already had a working solution ( a combination of [mocha](http://visionmedia.github.io/mocha/), [chai](http://chaijs.com/) and [sinon](http://sinonjs.org/) ) so I filed the information away for future reference.

Yesterday I finally had the time to try this library so I decided to create a simple example that you can download [here](https://github.com/Bjornej/intern-example).

First of all I created a new folder for the example and installed the library ( this step assumes you have a working node.js installation).

	mkdir intern-example
	cd intern-example
	npm install intern

Now the intern library is installed in the *node_modules* folder and we can begin to work. First of all let's create a *src* folder and a simple AMD module that defines two simple functions: **add** and **diff**.

	mkdir src
	cd src


<!--more-->

Then create a file library.js with this content


	define([],function () {
    	
		var sum = function (a, b) {
        	return a + b;
    	};

    	var diff = function (a, b) {
        	return a - b;
    	};    
	
		return {
        	sum : sum,
        	diff: diff
    	};
	});


This is the example library we are gonna test with Intern ( nothing complicated it's just a simple AMD module to have something working).

Now let's create a *tests* folder and copy the example  intern configuration file.

	mkdir tests ;
	cp node_modules/intern/tests/example.intern.js tests/intern.js


Now we are ready to write our first test. Intern uses the *chai* library to define the assertions so I opted for my preferred style, [should](http://chaijs.com/guide/styles/#should). The test are really simple and are meant just as examples:


	define([
		'intern!bdd',
		'intern/chai!should',
		'../src/library'
	], function (bdd, should, library) {
    	should();
    	with (bdd) {
        	describe("sum", function () {
        	    it("should sum two numbers", function () {
                	library.diff(3, 2).should.equal(1);
            	});
        	});
    	}
	});



The next step is to configure intern to load this file and try to run them. First of all open the intern configuration file we copied before and replace the *suites* line with

	suites: ["tests/test"],

Save the modifications and you are ready to launch the tests on the command line with

	node node_modules/intern/client.js config=tests/intern

This is all for this simple example. One thing I really like of this library is the fact that it can run easily both from the browser and the command line which is a big plus if you have to integrate it with a build process.