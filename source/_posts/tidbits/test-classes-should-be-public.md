---
title: Test Classes Should Be Public
date: 2016-03-14 06:50:08
author: Kent Merrell
comments: true
tags: 
- Unit Testing
- Visual Studio
- Notes
categories: 
- Tidbits
---

#### When creating tests in Visual Studio, the test class should be made <em>public</em>. 

By default, when you add a new class in VS, it does NOT include the <em>public</em> decorator.
<!-- more -->
This works
``` C Good
    public class CameraControllerTests : BaseTest{
        [Fact]
        public void AuthAttributes(){
            AssertIsAuthDecorated<VLogProfileController>();
        }
    }
```
This doesn't work. It will never be run by test runner.
``` C Bad
    class CameraControllerTests : BaseTest{
        [Fact]
        public void AuthAttributes(){
            AssertIsAuthDecorated<VLogProfileController>();
        }
    }
```
