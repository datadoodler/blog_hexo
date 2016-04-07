---
title: Node App Configuration
date: 2016-04-01 06:50:08
comments: true
tags: 
  - Node
  - Configuration
categories: 
- Tidbits
---

Applications that are deployed to various physical and logical environments (AWS, Heroku, Dev, Prod, Local, Test, Debug, Language, TodayDate, etc...) will need a way to dynamically adapt to their current environment. The path to a file on AWS is definitely different than a path to a file on a disconnected development box.


### A note about supplying credentials in an application - 
Credentials for accessing outside resources (databases, s3 buckets, deployment services, etc...) should <em>not</em> be included in any source file (config or hardcoded in app) that will be checked-in to a source control system. 

### Config File
A smart module for handling config files is necessary. You can create your own, or just use one that has already been created and tested, like nodejs-config.
<code>npm install nodejs-config</code>

### Environment Variables

Sometimes, using environment variables is the way to go. Like when the application needs credentials data such as username and password. 

