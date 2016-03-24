---
title: Promise Array Binding
date: 2016-03-22 06:50:08
author: Kent Merrell
comments: true
tags: 
  - Angular
  - Promises
  - Bootstrap
  - Async
categories: 
- Tech Sketch
---
### Progressbar Bound to Promise Array

#### Scenario
The application is periodically caching images (asynchronously). Whenever images are being pulled over the wire we want to show the progressbar (angular bootstrap directive) and the percentage complete of the images. Progressbar doesn't need to show the percent downloaded of a single image, but the percentage of the list of images that have completed (or failed) download.  
![](/blog/static/ts-05-progressbar-bound-to-promise-array.png)

<!-- More -->

#### Dependencies
(Note: these dependencies are statically loaded in the vendor_local directory of this techsketch to enable disconnected editing and viewing on demo site)

* angular  AngularJS v1.3.20
* angular-animate AngularJS v1.3.20
* angular-ui-bootstrap Version: 0.12.1 - 2015-02-20
* bootstrap css (an custom edited version of v3.3.6)

#### Demo
http://datadoodler.github.io/ts-05-progressbar-bound-to-promise-array/