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

The second choice to make regarded the storage layer. While using Telegraf allows a great degree of flexibility we had to choose a solution with a good Windows support, low hardware requirements and able to be queried by the toosl we chose for data visualization and alerting.

The choice was simple, we choose [InfluxDb](https://www.influxdata.com/time-series-platform/influxdb/) which can be installed as a WIndows service, has low requirements and integrates well with the other tools in the stack.

Notably it has also a concept of data retention allowing you to specify an automatic cleanup of your data  after 30 days.

### Data visualization

To visualize the collected data we chose to use [Grafana](https://grafana.com/) which is able to plot graphs reading directly from InfluxDb and from a lot of other data sources giving you a lot of flexibility and allowing you to easily navigate and correlate your data.

### Alerting

Initially we tried to use for this part Grafana new support for alerts but we soon realized it was too limited to work well (no multiple levels, no different alerting rules, ...) so we switched later to [Bosun](https://bosun.org/), a monitoring and alerting tool created by Stack Exchange. This tool can easily query InfluxDb, allows you to define complex rules and tweak them over time.

Also it has a dashboard with all active alerts where you can handle them byacknowledging them or closing when solved.
