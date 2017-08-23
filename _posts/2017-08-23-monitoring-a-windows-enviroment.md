---
layout: post
comments: true
published: false
title: Monitoring a Windows enviroment
categories:
  - monitoring
  - windows
  - time-series
  - metrics
  - alerting
---
Developing distributed applications in a Windows-only enviroment, with hosted Virtual machines, can present some challenges and require you to find solutions that are not so standardized due to this type of enviorment not being very common.

One of the challenges is collecting informations about your VMs, some important services (SQL Server, RabbitMQ, ElasticSearch,..) and your virtualization enviroment to be able to inspect them or be alerted in case of problems (or better before they happen).

To setup this kind of data collection and monitoring there are four area to consider. I will describe them and then propose a solution I've found works really well with minimal setup and is easy to configure.

The four areas to consider are:

- Data collection
- Data storage
- Data visualization
- Alerting

### Data collection

The first step is deciding what data you need to collect and find a program that can read it at a pre-defined interval and store where you want it. While there are many tools of this type, we need one that is able to work on Windows and adapt to it's peculiarities. This means having something able to read Windows Performance Counters.

Performance Counter are a Windows-only mechanism that is used to report values about the operating system but can be also used by applications like SQL Server. Some examples are:

- number of bytes of memory used
- number of messages in a MSMQ queue
- output troughtput for every network card 
- number of phisycal reads per seconds (SQL Server)

The full list of these counters can be seen from **Performance Monitor**, where they are divided in categories for easier navigation. The Performance Monitor interface is a throwback to the nineties but we need only the list of counters reachable when adding a new counter.

Pay attention to the fact that Performance Counter names are localized so mind the possibility that there may be a difference in name between you local computer and production servers.

### Data storage

The second and most important part is the storage of your collected data. The usual solution is using a time-series database which is a form of database specialized in saving and reading time-series (metrics). Multiple options are available that can easily run on windows like InfluxDB and Prometheus. Your choiche should be based primarily on two factors:

- can my data collector program write to the chosen storage?
- can I easily visualize data from the storage?

Availability and disaster recovery may play a part in your choiche but after running our chosen system for a year we treat this data as important but disposable, meaning we have no high availability and we accept the possibility of losing the data. We also keep only the last thirty days of data, a compromise allowing us to inspect trends in a metric but limiting the size of storage needed.

Another important factor to consider is how much data your chosen tool is able to ingest. If you collect 10 metrics per machine every ten seconds what can work with a hundred server may fail with ten thoousand. Fortunately most are able to ingest mass quantities of data and if this becames a problem you can use multiple databases, partitioning the resources by type or group of servers.

### Data visualization

The third part is data visualization, for which you need a tool that is:

- easy to use
- able to show the current status at a glance
- able to let you inspect and correlate historical data to pinpoint problems in a post-mortem
- easily configurable by everyone

While this part seems "easy" a good visualization tool **will** make the difference. It will help you correlate a spike in your response times with anomalies in your database metrics. It will help you pinpoint configuration errors in your servers. It will let you uncover stray queries that every two hours reads the entire database to generate a report. In short a good visualization tool will let you discover so much about you systems and applications than you ever thought existed.

The fourth point is also important. While creating standard visualizations is really useful it should also be possible to explore the data freely by anyone without having to ask to a central group to create a new visualization every time it is needed. This will let everyone move freely witout having to wait for someone else.

### Alerting

The last part is alerting on the collected data. Ideally you want to be able to:

- define rules about possible problems with levels of importance (at least warning and critical)
- having the ability to quickly change the defined rules
- having the possibility to define alerting destinations
- having the possibility to view at a glance the status of all your alerts and track their status over time

Defining different levels of importance will let you see problems way before they matter like full disk sotrage and give you time to cat or ignore them during the night. Having the ability to tweak these rules will let you cut down on the number of alerts which can lead you to *alert fatigue* if left unchecked making you ignore an important alert because it is buried in another thousand of les important notifications.

If you can define different alert destinations you can escalate the important things while leaving the minor ones to be handled when you have time. Having also a dashboard which lets you see all active alerts, their status and past status will let you more easily coordinate with others in your team.
