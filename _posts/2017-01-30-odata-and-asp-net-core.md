---
layout: post
comments: true
published: false
title: OData and ASP.NET Core
categories:
  - OData
  - ASP.NET Core
---
At work we're in the process of migrating some applications to ASP.NET Core to take advantage of some of it's features:

- the ability to self host in process without IIS making it perfect to create standalone services
- its design based on dependency injection

While we would love to be able to use the .NET Core version there are too many libraries that have not been ported still so we are forced to run on the full .NET framework.

While this solves many problems some libraries that integrated with ASP.NET have not been ported, in our case what was missing was the OData support. Searching online you can found some informations about it:

- https://github.com/OData/WebApi/issues/772
- https://github.com/OData/WebApi/issues/229
- https://github.com/OData/WebApi/issues/744

but all signs point to the porting work being stopped due to other priorities. This was a show stopper for us as we rely on OData to easily connect a 