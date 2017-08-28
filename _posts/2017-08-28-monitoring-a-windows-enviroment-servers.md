---
layout: post
comments: true
published: true
title: 'Monitoring a Windows enviroment: servers'
categories:
  - monitoring
  - alerting
  - metrics
  - performance counters
---
Once  all the programs described in the previous post are installed we can start to familiarize with the system.

One question arises: what data to capture? This depends on the role of the server where the collecting agent is installed.

For an application server we can collect some basic data:

- we can use Telegraf inputs ***cpu***, ***disk*** e ***mem***
- some useful Performance Counters to collect are:
  - ***Processor*** : "% Idle Time", "% Interrupt Time", "% Privileged Time", "% User Time", "% Processor Time" (only _Total)
  - ***Network Interface***: "Bytes Received/sec", "Bytes Sent/sec", "Bytes Total/sec" (all istances except _Total)
  - ***LogicalDisk*** : "Disk Bytes/sec", "Disk Read Bytes/sec", "Disk Write Bytes/sec" (all istances except _Total)
  
If the server hosts web applications you can add these Performance Counters:

- ***ASP.NET*** : "Requests Queued"
- ***ASP.NET Apps v4.0.30319*** : "Requests/sec", "Sessions active"
- ***Web Service***: "Connection Attempts/sec", "Current Connections"

If you are using MSMQ:

- ***MSMQ Queue*** : "Messages in Queue" (you can read them all or specify individual queues),
- ***MSMQ Service*** : "Total bytes in all queues" (this is important as MSMQ by default has a 1GB limit for messages saved and will refuse new messages when that limit is reached)


