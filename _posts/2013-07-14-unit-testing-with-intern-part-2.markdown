---
layout: post
title: "Unit Testing With Intern: Part 2"
date: 2013-07-14 21:57
comments: true
categories: ["unit testing","javascript","intern"]
---

Trying to use the Intern library I've discovered another couple of nice abilities:

## Running tests from the browser 

We've seen how to run intern from the command line but it is possible to run them in the browser outputting the results to the console. In order to do this, you have to open the client.html page shipped with intern and pass the configuration file as an option

	my-project/node_modules/intern/client.html?config=../tests/intern


## Grunt integration

As you can see from the last article I am a [Grunt](http://gruntjs.com/) user. I consider this tool essential to work so when I discovered that intern provides by default a grunt task to run the tests I had to try it.

To use it you just have to load the task in the Gruntfile

	grunt.loadNpmTasks('intern');

and then add the configuration for it:

	    intern: {
        	test: {
            	options: {
                	options: {
		                runType: 'client',
		                config: 'tests/intern',
		                reporters: [ 'console', 'lcov' ]
		            }
            	}
        	},
    	} 

All is left is to invoke it  with

	grunt intern

and you're done.

## Final considerations

Well I've tried Intern in a couple of projects and I'm impressed. It's easy to install, cofigure and use. It has a default Grunt integration which for me is a big plus and can run both form a browser and from the command line.

Still there are a couple of pain points:

1. There is no default spy/ mock implementation like sinon. Yes I know i can easily import it but it would have been nice if it was a default
2. It uses the dojo loader. This is a problem for me because I almost exclusively use RequireJS which can handle dependencies between non AMD files through the shim configuration. The dojo loader doesn't have this feature and forces you to use the order plugin to specify the correct loading order.  This is a real pain because it can introduce subtle bugs due to external libraries loading order.

All in all I have to say that Intern really merits to be used. If only it was possible to replace the dojo loader with RequireJS I would do so in a heartbeat.