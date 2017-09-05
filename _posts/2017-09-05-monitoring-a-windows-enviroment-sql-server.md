---
layout: post
comments: true
published: true
title: 'Monitoring a Windows enviroment: SQL Server'
categories:
  - monitoring
  - metrics
  - alerting
---
In the previous post we've seen what informations are useful to monitor a Windows application server. While useful data it won't allow a complete vision of our applications behaviour if we don't monitor also the important services, and what service is more important than your database?

If you are working in a Windows enviroment there's a good probability you are using Microsoft's SQL Server and you **will** have to monitor and fine-tune it's usage to prevent problems and identify wrong usages.

Telegraf already has a plugin for sql server that will extract information for your instance by executing a query. While this works well it has two problems:

- due to a bug it can only connect to SQL server 2008 R2 SP3 (this is a minor problem, I hope your SQL Servers are at least updated to a version which has not run out of support)
- it extracts a **lot** of data most of which is useful only in limited cases.

To make it simple we can craft a configuration which includes only the most relevant and important counters. As in the case of an application server you will need the same base data:

-  use the **disk**, **cpu** and **mem** plugins
-  **Network Interface** : 
  - "Bytes Received/sec" 
  - "Bytes Sent/sec"
  - "Bytes Total/sec"
- **Processor**: 
  - "% Idle Time"
  - "% Interrupt Time"
  - "% Privileged Time"
  - "% User Time"
  - "% Processor Time"
- **LogicalDisk** : 
  - “Disk Bytes/sec”
  - “Disk Read Bytes/sec”
  - “Disk Write Bytes/sec” (all istances except _Total)

Now to the SQL Server- specific Performance counters (replace **INSTANCE** with the name of your instance, there can be more than one on a single server):

- **MSSQL$INSTANCE:Buffer Manager** : 
  - "Buffer cache hit ratio"
  - "Database Pages"
  - "Free list stalls/sec"
  - "Page life expectancy"
  - "Page lookups/sec"
  - "Page reads/sec"
  - "Page writes/sec" 
- **MSSQL$INSTANCE:Databases**: 
  - "Active transactions"
  - "Transactions/sec"
  - "Write transactions/sec" 
- **MSSQL$INSTANCE:General Statistics**: 
  - "Processes blocked"
- **MSSQL$INSTANCE:Latches**: 
  - "Average Latch Wait Time (ms)"
  - "Latch Waits/sec"
  - "Total Latch Wait Time (ms)" 
- **MSSQL$INSTANCE:Locks**: 
  - "Average wait time (ms)"
  - "Lock Requests/sec"
  - "Timeout locks (timeout > 0)/sec"
  - "Lock Timeouts/sec"
  - "Lock Wait Time (ms)"
  - "Lock Waits/sec"
  - "Number of Deadlocks/sec" 
- **MSSQL$INSTANCE:SQL Statistics**: 
  - "Batch Requests/sec"
  - "SQL Compilations/sec"
  - "SQL Re-Compilations/sec" 
- **MSSQL$INSTANCE:Transactions**: 
  - "Free Space in tempdb (KB)"
  - "Transactions"
  - "Version Cleanup rate (KB/s)"
  - "Version Generation rate (KB/s)"
  - "Version Store Size (KB)"
  - "Version Store unit count"
  - "Version Store unit creation"
  - "Version Store unit truncation" 
- **MSSQL$INSTANCE:Wait Statistics**: 
  - "Lock waits"
  - "Log buffer waits"
  - "Log write waits"
  - "Memory grant queue waits"
  - "Network IO waits"
  - "Non-Page latch waits"
  - "Page IO latch waits"
  - "Page latch waits"
  - "Thread-safe memory objects waits"
  - "Transaction ownership waits"
  - "Wait for the worker"
  - "Workspace synchronization waits"

These performance counters will give you a pretty complete view of your SQL Server behaviour allowing you to inspect and correlate performance problems in your applications with the state of your database.
