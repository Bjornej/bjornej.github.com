---
layout: post
published: true
title: GruntLauncher 1.5 is out
comments: true
categories: 
  - visualstudio
  - gruntlauncher
  - grunt
  - gulp
  - bower
---

A new release of GruntLauncher is available on [VisualStudioGallery](http://visualstudiogallery.msdn.microsoft.com/dcbc5325-79ef-4b72-960e-0a51ee33a0ff) for you to download.

This new release brings a lot of improvements: 

 - better gruntfile parsing support
 - use of a submenu to group all grunt commands, useful when your gruntfile has many entries ( thanks to Mads Kristensen who did all the work )
 ![grunt](/images/grunt.png)
 
 - support for executing bower update on all your packages or on a specific package when right-clicking on it ( again thanks to Mads Kristensen )
 ![](/images/bowerall.png)
 ![](/images/bower.png)
 
 - support for gulpfile parsing in the same way it is done with gruntfiles (I've began to use gulp and support for it was easy to add )
 ![](/images/gulp.png)
 
With these new functionalities I believe I will have to change the plugin name to something more significant but it will take me some time to come up with a decent name.