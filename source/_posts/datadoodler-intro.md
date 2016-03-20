---
title: DataDoodler Intro
date: 2017-03-15 06:50:08
author: Kent Merrell
comments: true
tags: 
- Plans
- Requirements
categories: 
- DataDoodler
---

In a nutshell, DataDoodler is a platform for quickly 'doodling' data analytics. It aims to do for the analytics world what Plunker ([http://plnkr.co/](http://plnkr.co/)) has done for the world of application development. 

<!-- More -->

This blog works in tandem with DataDoodler Tech Sketches to support the creation of the DataDoodler Application itself. DataDoodler is an open source, non-trivial, full-stack, application. It utilizes a smattering of technologies necessary to visualize, analyze, and manage data. Since it currently has no outside funding and is being developed only as time allows, I am employing a rather liberal implementation of project management methods. Where a large, well-funded application would have a dedicated requirements repository and product/project/technical managers to manage time-lines, requirements backlogs, version dependencies, etc..., I'm taking a more 'scrappy', bootstrap approach.
 


### The Three Components of DataDoodler
1. Blog - I'm using this for requirement backlogs and high-level overviews of technologies I feel are important to this effort. Roughly it is a general roadmap to the project.
 * Why a <em>blog</em> you ask? While it's true that application requirements aren't usually specified in such a structure, this blog isn't exactly a requirements document. It's more a collection of ideas, technical methods and patterns that may one day be a part of the DataDoolder platform.
 * Online: blog.datadoodler.com
 * Repository: [https://github.com/datadoodler/datadoodler-blog](https://github.com/datadoodler/datadoodler-blog)
 * Technical Architecture: Runs on Hexo [https://hexo.io/](https://hexo.io/). This is an Open Source blog engine built on top of Node.js. It's more flexible than the github wiki pages and scaleable enough for my purposes.
2. Tech Sketches - This is for lower-level technical explanations, demonstrations, and experiments.
 * Online: techsketch.datadoodler.com
 * Repository: [https://github.com/datadoodler/datadoodler-techsketch](https://github.com/datadoodler/datadoodler-techsketch)
 * One repository for all sketches. 
 * A Tech Sketch gets it's own directory and is self-contained (for the most part) with it's own scaffolding (package.json, bower.json, etc...). Why not just put Tech Sketch content inside this blog? The answer is that there would be too much interference with the Hexo internal structure and build process. Tech Sketches need their own pristine environment.
 * Tech Sketches typically contain readme.md or readme.html files that contain more detailed explanations than blog posts.
 * May utilize more sophisticated documentation tooling such as [PrismJs](http://prismjs.com/) or [JSDoc3](https://github.com/jsdoc3/jsdoc).
3. The Application
 * Online: www.datadoodler.com
 * Repository: [https://github.com/datadoodler/datadoodler_app](https://github.com/datadoodler/datadoodler_app)
 


### Potpourri Approach
DataDoodler is currently a somewhat eclectic smattering of technologies that are generally useful to my paying clients. In this sense, it is a project I use for learning and experimenting with new technologies.