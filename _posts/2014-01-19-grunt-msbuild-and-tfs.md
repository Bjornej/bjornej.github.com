---
layout: post
published: true
title: "Grunt, MsBuild and Tfs"
comments: true
categories: 
  - grunt
  - msbuild
  - tfs
  - nuget
---

One of the most useful features of TFS (at least for me) is the ability to set it up to build your project and output the resultin an automated fashion.

The ability to have a simple, unique  and repeatable process allows you to build and deploy your project without manual intervention.

Howewer it can be tricky to customize the build templates used by TFS to include specific additional steps like invoking grunt and executing additional tasks. For this reason I created a nuget package Grunt.MsBuild that can help you to integrate grunt execution in your TFS build by simply installing it in your projects.

#### What does it do

The Grunt.MsBuild package extends your build with a new target that sequentially invokes 

- npm install ( to install all the needed packages and dependencies )
- grunt build$Configuration (where $Configuration will be replaced by the current build configuration allowing you to customize the build process when in debug mdoe or release mode)

#### Version Differences

To address all the possibilities I've created two different packages: 

- The local version assumes grunt-cli is installed as a local module and will use it to launch grunt
- the global version assumes grunt-cli is installed globally and available in your path

This separation was necessary because while it's easy to install grunt-cli globally on your development machine it could not be possible on the build server.

#### Running it 

I've used successfully the packages on a on-premise version of tfs but if you want to use it on VisualStudioOnline it's currently not possible because it still uses node 0.6 which is not supported by grunt. 

There are to solutions to this problem:

- wait until node is updated on the build servers
- commit the node modules you depend on in TFS ( I don't recommend this solution as it can cause problems with the number of files to save)