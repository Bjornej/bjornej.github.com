---
layout: post
published: false
title: "Grunt, MsBuild and Tfs"
comments: true
categories: 
  - tfs
  - grunt
  - msbuild
  - nuget
---

One of the good developer practices that we should foolow is to have and configure a build server dedicated to the continuous integration and build of our code, helping us to avoid problems like:

- "hey I need to fix a type and publish the site" only to discover that it doesn't build and you don't know when the problem was introduced
- "magic machine syndrome" when your project can be built for release only on specific machines due to an unclear list of dependencies
- missing or forgotten build step like "Hey did I remember to update the clieside code version?" after the publication

These problems can be solved by using a continuous integration server like [teamCity](http://www.jetbrains.com/teamcity/), [Jenkins](http://jenkins-ci.org/) or [TFS](http://msdn.microsoft.com/en-us/vstudio/ff637362.aspx)

Team foundation server is one of the most common choices for a .NET shop but it's build process it's not so easy to modify as it's based on Window Workflow and relying on custom activities.

Let's say your server side code is buiilding correctly but you want to integrate all of the steps required to publish you app like 

- css minimization
- js optimization with require.js
- url cache breaking

and you usually rely on grunt to do these tasks. Well now the only thing ou have to do to integrate these activities in a build is to simply install the grunt.MsBuild nuget package.

These package uses a little known feature of nuget, the ability to add build steps in a project. By installing this package two new commands wiil be executend when building

- npm install
- grunt build$Configuration (where $Configuration will be replaced by the current build configuration allowing you to customize the build prcess when in debug mdoe or release mode)

#### Version Differences

To address all the possibilities I've created two different packages: 

- The local version assumes grunt-cli is installed as a local module and will use it to launch grunt
- the global version assumes grunt-cli is installed globally and available in your path

This separation was necessary because while it's easy to install grunt-cli globally onb your machine it could not be possible on the build server.

#### Running it 

I've used successfully the packages on a on-premise versio of tfs but if you want to use it on VisualStudioOnline it's not currently possible because it still uses node 0.6 which is not supported by grunt. 

There are to solutions to this problem:

- wait until node is updated on the build servers
- commit the node modules you depend on in TFS ( I don't recommend this solution as it can cause problems with the number of files to save)