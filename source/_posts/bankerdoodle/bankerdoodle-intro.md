---
title: BankerDoodle Intro
date: 2017-03-14 06:50:08
author: Kent Merrell
comments: false
tags: 
- BankerDoodle
- Wireframes
- Git
categories: 
- BankerDoodle
---

BankerDoodle is an application built on top of the DataDoodler platform. It inherits all the analytical goodness of DataDoodler, but contains features specific to the banking industry. It is a closed/commercial product that will be the initial means to monetize the DataDoodler platform. It is conceivable that any number of applications (open or closed) will be built on top of the DataDoodler platform. 
<!-- More -->
The BankerDoodle repository is a private repo at [github.com/duke83](https://github.com/duke83)

FDIC SDI context consists of an array of VarNames, and Array of CertIds, and an Array of QDates.
``` bash
var context = {vars:['var1', 'var2',...], certs:[1230,3324,...], qDates:['2012Q1', '2013Q1']}
```


``` bash
$ hexo server
```


BankerDoodle Features:
 * FDIC SDI data is a 1st class citizen. This data is comprised of over 14 billion datapoints.
 * Pulling data from BankerDoodle is a vastly improved user experience over pulling directly from the FDIC website.
 * The steep learning curve of working with FDIC data is all but eliminated.
 
 
 
 <div style="width: 600px; height: 480px; margin: 10px; position: relative;"><iframe allowfullscreen frameborder="0" style="width:600px; height:480px" src="https://www.lucidchart.com/documents/embeddedchart/35c03798-d57c-43f8-a951-99deb63a9ce4" id="_TP43X1-tWrg"></iframe></div>
 
 
<div style="width: 480px; height: 360px; margin: 10px; position: relative;"><iframe allowfullscreen frameborder="0" style="width:480px; height:360px" src="https://www.lucidchart.com/documents/embeddedchart/8f6ddd1b-c9da-41c5-b61f-8de4a2f50133" id="Bdn4h32lctgt"></iframe></div>