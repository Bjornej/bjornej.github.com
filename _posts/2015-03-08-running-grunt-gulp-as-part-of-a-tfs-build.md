---
layout: post
published: true
title: Running Grunt/gulp as part of a TFS build
comments: true
categories: 
  - tfs
  - grunt
  - gulp
---

In the past to execute grunt as part of a TFS build I've created a nuget package that modifies the msbuild file [Grunt.MSBuild](http://bjornej.github.io/blog/2014/01/19/grunt-msbuild-and-tfs/) .

Having updated TFS to the 2013 version I've found there's an easier way to do it by leveraging it's ability to execute a Powershell script during the build. This can be done easily:

- install grunt/gulp globally on every build agent. Pay attention to the fact that it must be installed as the user that runs the build agent and the grunt/gulp location **must** be included in the PATH variable (else you won't be able to invoke grunt/gulp). 
- Add a powershell script inside your solution with the following lines

        Push-Location "$PSScriptRoot\..\Source\Web"  
        Write-Host "npm package restore"
        & "npm" install
        if ($LastExitCode -ne 0) {
          Write-Error "Npm package restore failed";
          exit 1;
        }

        Write-Host "Grunt requirejs"
        & "grunt" requirejs
        if ($LastExitCode -ne 0) {
          Write-Error "Grunt requirejs failed";
          exit 1;
        }
        Pop-Location

- Modify your build definition to include the script by going in the process Tab -> Build section -> Advanced -> PreBuild script path
- Run your newly configured build and enjoy.

The script it's really simple but sometimes must be adapted to your configuration and can be easily extended.
The first line moves the current working directory to the directory containing you package.json file and then executes an *npm install* to restore all the needed node packages. After that it exeutes *grunt requirejs* and finalyy restores the original working directory. 

This step can be easily replaced by running gulp or extended by compiling your sass etcetera... . 


  