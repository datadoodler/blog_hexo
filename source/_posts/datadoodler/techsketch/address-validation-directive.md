---
title: address-validation-directive
date: 2014-11-01 06:50:08
author: Kent Merrell
comments: true
tags: 
  - Angular
  - Asynchronous
  - Promise
categories: 
- Tech Sketch
---

The workings of this directive are illustrated in the following 3 scenarios. In each scenario, after the user initially presses 'save', the directive makes a call to the address validation service, injects appropriate html (if needed), waits for a user response, and updates the address fields accordingly.

``` javascript
<address-suggestion ng-attr-address="address"></address-suggestion>
```
<!-- more -->


 {% iframe http://datadoodler.github.io/ts-00-address-suggestion-directive/ [600] [480] %}

 

