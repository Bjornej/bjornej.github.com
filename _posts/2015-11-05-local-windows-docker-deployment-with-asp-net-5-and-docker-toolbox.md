---
layout: post
categories: 
  - "null"
comments: true
published: false
title: Local Windows Docker deployment with ASP.NET 5 and Docker Toolbox
---



If you are reading this article you probably already know what Docker is and as a .NET developer you've always wanted to be able to use it to deploy your applications.

With the beta 8 of ASP.NET 5 a new deploy option is available that let's you deploy your website to a virtual machine in Azure running Docker. This is actually pretty simple and well covered by the documentation but what if you don't have an Azure Account, network access or simply prefer to try things on your local computer.

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



