---
layout: post
categories: 
  - docker
  - ASP.NET5
  - VS2015
comments: true
published: true
title: Local Windows Docker deployment with ASP.NET 5 and Docker Toolbox
---



If you are reading this article you probably already know what [Docker](https://www.docker.com/) is and as a .NET developer you've always wanted to be able to use it to deploy your applications.

With the beta 8 of ASP.NET 5 a new deploy option is available that lets you deploy your website [to a virtual machine in Azure running Docker](http://docs.asp.net/en/latest/publishing/docker.html). This is actually pretty simple and well covered by the documentation but what if you don't have an Azure Account, network access or simply prefer to try things on your local computer.

This situation is not covered by the docs so I'll cover the necessary steps. Note that I've tried this instructions on Windows 10 but there should be no problem on WIndows 7, 8 or 8.1 .

### Prerequisites

First of all make sure you've installed all of the followings:

- [docker machine](https://docs.docker.com/windows/step_one/)
- [Visual Studio 2015](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) (at least community edition)
- [Microsoft ASP.NET and Web Tools 2015 (Beta8)](https://www.microsoft.com/en-us/download/details.aspx?id=49442)
- [Visual Studio 2015 Tools for Docker - October Preview](https://visualstudiogallery.msdn.microsoft.com/0f5b2caa-ea00-41c8-b8a2-058c7da0b3e4)

and verify your docker installation is working.

### Deploying to Docker

The first thing to do is to create a new ASP.NET Web Application with the **ASP.NET Preview Templates**. Choose **Web application** as in the image and uncheck the *host in the cloud* option.

![dockercreate.png]({{site.baseurl}}/images/dockercreate.png)

Proceed with project creation and then build it by pressing **Ctrl+Shift+B**. To start the deploy simply right-click on the project and select the **Publish** option.

![dockerpublish.png]({{site.baseurl}}/images/dockerpublish.png)

Choose the **docker containers** option and then the **Custom Docker host**.

![dockerhost.png]({{site.baseurl}}/images/dockerhost.png)

Now you will have to specify the connection info for your local Docker host

![dockercustom.png]({{site.baseurl}}/images/dockercustom.png)

To obtain these info launch the **Docker quickstart terminal** installed with the Docker Tools.

![dockerterminal.png]({{site.baseurl}}/images/dockerterminal.png)

You will see, drawn in green, the name of your machine and it's IP, in this case 192.168.99.100. Return to the connection info dialog and insert ** tcp://192.168.99.100:2376 **. Then execute in the terminal 

    docker-machine config default
    
substituting default with your machine name. You will see all the config options o connect to your docker host. Copy all of it except the last parameter ( -H tcp://192.168.99.100:2376) as it is not necessary and paste it in the **Docker Advanced Options > Auth Options ** field.

Now you're done. Press **Publish** and wait until the build terminates, the browser will automatically open your website running in Docker.

![dockerrunning.png]({{site.baseurl}}/images/dockerrunning.png)

![dockerps.png]({{site.baseurl}}/images/dockerps.png)


