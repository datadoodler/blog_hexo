---
title: FDIC Old SQL flow
date: 2014-11-01 06:50:08
author: Kent Merrell
comments: true
tags: 
  - SQL
  - FDIC
  - Process
categories: 
- BankerDoodle
---

An early approach to working with FDIC data was to put it all in a SQL database. The idea was to use dynamic sql to build tables with only the columns necessary for the current study. This approach was doomed by in static nature of sql tables and the continual need to regenerate DDL and load data.

The new approach is centered on DynamodDb.

<!-- More -->
 
 <div style="width: 600px; height: 480px; margin: 10px; position: relative;"><iframe allowfullscreen frameborder="0" style="width:600px; height:480px" src="https://www.lucidchart.com/documents/embeddedchart/73229e0a-a359-4a5f-a240-43d2f5f4ecd3" id="AUD4I_xHddUV"></iframe></div>

