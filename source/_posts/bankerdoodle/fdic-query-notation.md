---
title: FDIC Query Notation
date: 2016-03-14 06:50:08
comments: true
tags: 
- BankerDoodle
- FDIC
- Query Notation
categories: 
- BankerDoodle
---

BankerDoodle is an application built on top of the DataDoodler platform. It inherits all the analytical goodness of DataDoodler, but contains features specific to the banking industry.

<!-- More -->

FDIC data is in a fairly consistent format
 * Zip files containing approximately 60 csv files
 * Each CSV file covers a different grouping of FDIC variables
 * CSV files containing one record (row) per bank
 * Released Quarterly
 
 FDIC data is processed via a well-defined process (see [FDIC-ETL](/)).
 
<div style="width: 480px; height: 360px; margin: 10px; position: relative;"><iframe allowfullscreen frameborder="0" style="width:480px; height:360px" src="https://www.lucidchart.com/documents/embeddedchart/ad13c798-2b08-4e17-85b4-0a0ec72a7702" id="JSn4tVerrVnV"></iframe></div>