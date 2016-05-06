---
title: Angular Slider
date: 2016-03-29 06:50:08
author: Kent Merrell
comments: true
tags: 
  - Angular
  - Directives
  - rzslider
  - Angular-ui
  - JavaScript
categories: 
  - Tech Sketch
---

Demo: [http://datadoodler.github.io/ts-06-angular-slider]

Source: [https://github.com/datadoodler/ts-06-angular-slider]



![](/blog/static/ts-06-angular-slider1.png )

<!-- More -->



Both of these sliders are bound to the same object on the backend. (See object at bottom). The first display properly when rendered. The second needs to be forced by broadcasting an event on the rootscope.


```
function clickButton() {
     this.showSpeedSlider = !this.showSpeedSlider;
     if(this.forceRender){
         // Force rendering at every iteration of the interval.
         $interval(function () {
            $rootScope.$broadcast('rzSliderForceRender');
         }, 1,500, true, $rootScope)
     }
};
```

For other examples of using rzslider, see [https://jsfiddle.net/ValentinH/954eve2L]
