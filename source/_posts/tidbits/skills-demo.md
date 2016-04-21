---
title: Skills Demo - A Few Examples
date: 2016-04-21 06:50:08
author: Kent Merrell
comments: true
tags: 
  - Angular
  - Node
  - ECMAScript 6
  - Directives
  - NPM
  - Demo
categories: 
  - Tidbits
---


This document is intended to be a guided tour through some of my code. It will provide some insight into my skill set, coding style, and overall approach to developing apps. Scroll through this docuement to find the following examples:
- fdic-sdi-manager (node-based ETL with lots of cool es6 features)
- Blooming Menu Directive (angular directive, animation)
- Address Verification Directive (angular directive, promise-based DOM manipulation)

<!-- More -->

# Example: fdic-sdi-manager
The purpose of this project is to extract data from quarterly zip files and persist it to a nosql database in an 'on-demand' fashion. I don't want to persist *all* the data, but I don't know before-hand which variables I want to persist. 

### Source code:
https://github.com/datadoodler/fdic-sdi-manager.git 

### Technical highlights:
- nodejs
- tdd with mocha/chai/wallaby
- es6 classes
- es6 generators
- factory pattern
- nosql database
- npm package publish, consume

I will provide an overview of the data then address each of the above highlights individually.

### Data:
The FDIC releases data for public consumption in the form of quarterly zip files. Each zip file normally contains 65 .csv files. Each .csv file contains anywhere from 40 to 150 variables (columns) for approximately 8500 banks (rows).

### NodeJS
I'm using node version 5.3.0, which has native support for all the es6 features I was compelled to use. Though this project is published to an npm repository it is not meant for general distribution and will be  consumed in a setting where I have explicit control of the node environment (namely, my own AWS EC2 instance).
### tdd with mocha/chai/wallaby
I'm addicted to test-first development. It is how I know what to code, without getting too sidetracked (and overwhelmed) with "it *might* need to to *x* someday" mindset. It helps me organize my thoughts and more expeditiously arrive at an efficient architecture.

![](/blog/static/TDD-Fdic.png )
### es6 classes
Yes, I know es6 classes are syntactic sugar, but I'm finding that it helps with conceptualizing underlying architecture.
#### FdicSdiManager Class 
- this is the main entrypoint of the ETL application
- has a collection of FdicSdiQuarter instances
- controls instantiation of and comparison between quarterly data


#### FdicSdiQuarter Class
- properties for processing state (state is held in local nosql table)
- methods to extract zip file, reset, clean, and persist data

#### QDate Class
- contains properties and methods neccessary for consistent naming conventions for handling quarterly datafiles, as well as an iteration mechanism to get QDate instances for the  next and previous quarters.

### es6 generators

I use the factory pattern in conjunction with an es6 generator function to return an instance of FdicSdiQuarter with all it's initial *asynchronous* properties filled. 

```
function *FdicSdiQuarter_factory(options) {
    
    const date = new Date();
    
    try {
        options = resolveOptions(options);

        var fdicSdiQuarter = new FdicSdiQuarter(options.year, options.quarter);

        // GET INITIAL STATE - FILL ASYNC PROPERTIES FOR THIS INSTANCE

        fdicSdiQuarter._successfulActions = yield database.getPersistedSuccessfulActions(options.year, options.quarter);

        fdicSdiQuarter._csvFileMetadata = yield getCsvFileMetadata(options.year, options.quarter);

        return fdicSdiQuarter;
    }

    catch (e) {
        logger.error("SOME ASYNC FUNCTION IN FdicSdiQuarter_factory GENERATOR", e)
    }
};
```


### nosql database
I use nedb quite liberally to persist state. I tend to use many smaller tables that can  be scoped to a particular quarter and easily reset if needed. (It's no fun to have to start processing *all* quarters if there's an error in just one quarter.)



### npm package publish, consume
This project is published as an npm repo. Though it's not really necessary, it's a really nice convenience to be able to include it wherever I want. These classes will eventually be used in admin ui screens. 



# Example: Blooming Menu Directive
###### Source code:
https://github.com/duke83/ts-04-blooming-menu


![](/blog/static/bloomingMenu2.gif )

This particular code is an early prototype of a new navigation paradigm my client wanted to use. Though none of this code made it to production, it demonstrates a rapid development effort built in an angular environment.

Much of the magic behind this has to do with css transformations and a little html trickery. The buttons are on a totally different tree as the button text. This is because the buttons had to be transparent, while the button text had to be opaque.



# Example: Address Verification Directive

###### Live demo:
http://datadoodler.github.io/ts-00-address-suggestion-directive/

###### Source code:
https://github.com/datadoodler/ts-00-address-suggestion-directive


The workings of this directive are illustrated in the following 3 scenarios. In each scenario, after the user initially presses 'save', the directive makes a call to the address validation service, injects appropriate html (if needed), waits for a user response, and updates the address fields accordingly.

 ![Address fields on a page before user presses save](/blog/static/address-validation-directive-1.png )

#### The three scenarios this directive handles:
1. User enters an invalid address and the service returns a suggested address
2. User enters a invalid address and the service doesn't return a suggested address
3. User enters a valid address

#### Case 1
Upon pressing Save, the address service is not able to find an address that matches what the user entered. But it <em>is</em> able to find a <em>possible</em> match, and returns it as a suggestion. The user is given the option to select the suggested address or force the save with the original address.
![After pressing Save, directive calls validation service and returns a suggested address if it can't find a perfect match](/blog/static/address-validation-directive-2.png )
 
 
![After address is validated and/or has user approval normal processing continues](/blog/static/address-validation-directive-3.png )


