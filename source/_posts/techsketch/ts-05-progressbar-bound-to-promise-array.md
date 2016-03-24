---
title: Promise Array Binding
date: 2016-03-22 06:50:08
author: Kent Merrell
comments: true
tags: 
  - Angular
  - Promises
  - Bootstrap
  - Asynchronous
categories: 
- Tech Sketch
---


#### Progressbar Bound to Promise Array
The application is periodically caching images (asynchronously). Whenever images are being pulled over the wire we want to show the progressbar (angular bootstrap directive) and the percentage complete of the images. Progressbar doesn't need to show the percent downloaded of a single image, but the percentage of the list of images that have completed (or failed) download.  
![](/blog/static/ts-05-progressbar-bound-to-promise-array.png)

<!-- More -->

#### promise-maker.service.js
A simple factory that simulates an asynchronous method (such as retrieving images via ajax call).
``` javascript
.factory('promiseMaker', function ($q, $timeout) {
    var promiseMaker = {};

  promiseMaker.getVolley = function (cb) {
    var rtrn = [];

    // Create 10 promises
    for(var i=0;i<10;i++){
        rtrn.push($q.when($timeout(function () {
            console.log('new', new Date())
        }, 1000 + (Math.random() * 3000))));
    }

    return rtrn;
  };

  return promiseMaker;
});
```

#### controller
The getPromises function makes the call to the service, and fills the promises array with the returned promises. The number of promises returned is held in originalPromiseCount and used as the denominator. As promises are resolved (successfully or unsuccessfully) they are popped off the array. The length of this array is the denominator of percentage complete.
``` javascript
    function ctrl1(promiseMaker) {
        var vm = this;
        vm.promises = [];
        vm.showbar = false;
        vm.originalPromiseCount = 0;
    
        vm.getPromises = function () {
            vm.originalPromiseCount = 0;
            var newPromises = promiseMaker.getVolley();
            vm.showbar = true;
            vm.originalPromiseCount = newPromises.length;
            newPromises.forEach(function (prom) {
                pushPromise(prom)
            })
        };
    
        vm.getPercentComplete = function () {
            if (vm.promises.length === 0) {
                return 0;
            }
            return 100 * (vm.originalPromiseCount - vm.promises.length) / vm.originalPromiseCount;
        };
    
        function pushPromise(prom) {
            prom.finally(function () {
                // When this promise is resolved, remove it.
                removePromise(prom);
            });
            vm.promises.push(prom);
        }
    
        function removePromise(prom) {
            vm.promises.pop();
            vm.promises.length === 0 ? vm.showbar = false : vm.showbar = true;
        }
    
        return vm;
    }
```


#### Dependencies
(Note: these dependencies are statically loaded in the vendor_local directory of this techsketch to enable disconnected editing and viewing on demo site)

* angular  AngularJS v1.3.20
* angular-animate AngularJS v1.3.20
* angular-ui-bootstrap Version: 0.12.1 - 2015-02-20
* bootstrap css (an custom edited version of v3.3.6)

#### Demo
http://datadoodler.github.io/ts-05-progressbar-bound-to-promise-array/