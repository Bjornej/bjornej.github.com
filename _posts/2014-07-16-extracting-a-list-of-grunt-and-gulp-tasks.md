---
layout: post
published: false
title: Extracting a list of grunt and gulp tasks
comments: true
categories: 
  - grunt
  - "gulp "
  - gruntlauncher
  - edge
---

I use a lot grunt and gulp when working so, to improve my workflow with Visual Studio, I created the GruntLauncher extension which can parse a *gulpfile* or *gruntfile* and extract the contained tasks.

To be able to do this I didn't have many options so I used an hack: **executing** the file in a javascript engine and reading the option object to identify the tasks.

While this works it has many unhandled corner cases:

* all the grunt utility functions must be present and defined
* all the gulp utility functions must be present and defined
* all the common node functions should be present and defined ( this is almost impossible to do as they are too many)

While this was an hack it worked quite well with just an handful of cases but everytime someone had a problem I got back to thinking to a better  and more robust solution.

The an idea dawned on me: Why should I mock all these functions and not simply ask to grunt and gulp for the defined config options? While this seems easy to do you have to remember that I cannot simply invoke the command line and look at the results as I need the whole options object for postprocessing and also because it's not a perfect solution.

WIth some experiments I came to the following results for gulp:

    var gulp = require('gulp');
    require('./gulpfile');
    console.log(Object.keys(gulp.tasks).join(' '));
    
and a similar snippet for grunt (in this case I also look for subtasks)

	var param = grunt.config.data;
	var names = [];
	for(var prop in param){
		if(param.hasOwnProperty(prop)){
			names.push(prop);
			if(param[prop] === Object(param[prop])){
			    var arr=[];
				for(var innerProp in param[prop]){
					if(param[prop].hasOwnProperty(innerProp)){
						if(innerProp!=='options'){
							arr.push(prop+":"+innerProp);
						}
					}
				}
				if(arr.length > 1){
					for (var i=0;i< arr.length;i++){
						names.push(arr[i]);
					}
				}
			}
		}
	}


With these I can let gulp and grunt do the work trusting the files to be well formed and the necessary plugins installed then simply invoke this code from .NET thanks to [Edge.js](https://github.com/tjanczuk/edge).

GruntLauncher is gonna get a seious refactoring..



