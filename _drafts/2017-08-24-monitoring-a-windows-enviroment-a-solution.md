---
layout: post
comments: true
published: true
title: 'Monitoring a Windows enviroment: a solution'
categories:
  - monitoring
  - windows
  - metrics
  - alerting
---
In the previous post I described some of the challenges in monitoring a Windows-only enviroment. Now I'll describe the solution I've chosen and has been working for almost a year without an hitch to monitor an hundred VMs.

If you remember from the previous post the four areas to consider are:

- Data collection
- Data storage
- Data visualization
- Alerting

### Data collection

As we said one of the most important things is the ability to read Windows Performance Counters and write data to our chosen storage. Here the solution was simple [Telegraf](https://www.influxdata.com/time-series-platform/telegraf/).

Telegraf can be easily installed as a Windows Service and most importantly:

- can save to numerous type of storage allowing you flexibility in choosing the storage type
- already has numerous plugins allowing you to scrape data from numerous sources (if a plugin does not exists it's simple to create a new one if you know a little Go)

### Data storage



### Data visualization
### Alerting
