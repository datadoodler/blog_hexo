---
title: Cost of Change vs. Cost of Understanding
date: 2016-03-14 06:50:08
author: Kent Merrell
comments: true
tags: 
- Architecture
- Maintenance
categories: 
- Tidbits
---

There are costs associated with how you write code (the patterns you utilize). Highly abstract code that relies on a high degree of inheritance, factories, and dependency injection is easier to change, but harder to understand.

Code that is less abstract is more likely to break something somewhere when you change it. Though it is harder to change, it is easier to understand.

<!-- more -->

This came from a conference where the speaker was making the case that sometimes it's better to not be super object oriented. (I need to get a reference).

<div style="width: 480px; height: 360px; margin: 10px; position: relative;"><iframe allowfullscreen frameborder="0" style="width:480px; height:360px" src="https://www.lucidchart.com/documents/embeddedchart/e0d0d3d6-c71c-4ded-a616-d58d15dd2666" id="sKB4v.v0jPgb"></iframe></div>