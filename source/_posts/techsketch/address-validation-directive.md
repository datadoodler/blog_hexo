---
title: Address Validation Directive
date: 2015-11-01 06:50:08
author: Kent Merrell
comments: true
tags: 
  - Angular
  - Asynchronous
  - Promises
  - JavaScript
categories: 
- Skills Demo
---

The workings of this directive are illustrated in the following 3 scenarios. In each scenario, after the user initially presses 'save', the directive makes a call to the address validation service, injects appropriate html (if needed), waits for a user response, and updates the address fields accordingly.

 ![Address fields on a page before user presses save](/blog/static/address-validation-directive-1.png )
<!-- more -->

###  Run the [Demo](http://datadoodler.github.io/ts-00-address-suggestion-directive)

###  View the [Source Code](http://github.com/datadoodler/ts-00-address-suggestion-directive)

#### The three scenarios this directive handles:
1. User enters an invalid address and the service returns a suggested address
2. User enters a invalid address and the service doesn't return a suggested address
3. User enters a valid address

#### Case 1
Upon pressing Save, the address service is not able to find an address that matches what the user entered. But it <em>is</em> able to find a <em>possible</em> match, and returns it as a suggestion. The user is given the option to select the suggested address or force the save with the original address.
![After pressing Save, directive calls validation service and returns a suggested address if it can't find a perfect match](/blog/static/address-validation-directive-2.png )
 
 
![After address is validated and/or has user approval normal processing continues](/blog/static/address-validation-directive-3.png )


#### See the [demo](http://datadoodler.github.io/ts-00-address-suggestion-directive) for additional cases


 

