---
layout: post
published: true
title: Supporting multiple Visual Studio versions in a single extension
comments: true
categories: 
  - visual studio
  - gruntlauncher
  - vssdk
---

When you create a Visual Studio extension to maximise its usefulness you try to make it work in all the most common Visual Studio versions which usually means VS 2012, 2013 and 2015.

This is not a big problem if you extension doesn't target specific capabilities introduced only in the latest versions as every Visual Studio versions install the preceding versions libraries.

Sometimes, when you upgrade your extensions to target the new visual studio versions, you receive a complaint from someone that your extensions doesn't work anymore. Further this seems to happen only if you have only an old VS version (usually only 2012) installed so you're left to ponder what happened.

Searching on the internet for the specific message you find the likely cause, using newer versions of visual studio updated your project references to target the new dll versions which can't be found in a system that only has vs 2012 installed. 

A better search finds many results [here](https://github.com/jfromaniello/nestin/issues/2), [here](http://stackoverflow.com/questions/25606632/how-can-a-vs-extension-target-multiple-versions-in-regard-to-microsoft-visualstu) and [here](https://connect.microsoft.com/VisualStudio/feedback/details/794961/previous-version-assemblies-cannot-load-in-visual-studio-2013-preview) suggesting some options :

- creating two separate extensions to target VS2012 and VS2013
- load dynamically the required library
- manually edit you csproj to remove the new reference and pay attention to the fact that VS will always try to update them

Solution 1 is a no-go as I'm lazy and for a simple extension like Gruntlauncher I don't want to mantain two separate version. Option 2 is doable but a little complex while solution 3 is the easiest but feels a lot like battling with Visual studio.

Luckily I found another options in the form of the [VSSDK nuget pakages](https://github.com/tunnelvisionlabs/vsxdeps). These packages when installed allow you to always reference the correct version of the library without having to mantain separate version or resort tu ugly hacks.
