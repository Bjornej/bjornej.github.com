---
layout: post
comments: true
published: true
title: 'Monitoring a Windows enviroment: servers'
---
Once  all the programs described in the previous post are installed we can start to familiarize with the system.

One question arises: what data to capture? This depends on the role of the server where the collectiong agent is installed.

For an application server we can collect some basic data:

- we can use Telegraf inputs *cpu*, *disk* e *mem*
- some useful Performance Counters to collect are:
  - *Processor* : "% Idle Time", "% Interrupt Time", "% Privileged Time", "% User Time", "% Processor Time" (only _Total)
  - *Network Interface*: "Bytes Received/sec", "Bytes Sent/sec", "Bytes Total/sec" (all istances except _Total)
  - *LogicalDisk* : "Disk Bytes/sec", "Disk Read Bytes/sec", "Disk Write Bytes/sec" (all istances except _Total)
  
If the server hosts web applications:

If the server contains one or more instances of SQL Server