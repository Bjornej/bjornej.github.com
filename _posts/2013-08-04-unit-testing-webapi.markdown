---
layout: post
title: "Unit testing WebApi"
date: 2013-08-04 21:09
comments: true
categories: ["WebApi","unit","testing","RouteData","CreateResponse","C#"]
---

Unit testing WebApi code is usually much simpler than it's MVC counterpart but can be problematic in some situations, particularly when testing routing code or code that manually creates the response so I decided to share two useful tricks.


## Mocking CreateResponse<T\> ##
When your code calls CreateResponse<T\> your unit test will usually fail with an InvalidOperationException due to the fact that this extension method is checking for HttpConfiguration which is not present when unit testing.

The solution is really simple and amounts to instantiating a new HttpConfiguration

    request.Properties.Add(HttpPropertyKeys.HttpConfigurationKey, new HttpConfiguration());

## Mocking RouteData ##
The second problem you will sometimes face is due to code that examines routeData to decide how to proceed ( this usually happens when you write a custom DefaultHttpControllerSelector ). When unit testing you have to remember that it is possible to initialize routeData and its content with a simple

	request.Properties[HttpPropertyKeys.HttpRouteDataKey] =
                    new HttpRouteData(
						new HttpRoute(), 
						new HttpRouteValueDictionary( 
							new { 
								controller = "test", 
								action ="test" 
						})
					);
