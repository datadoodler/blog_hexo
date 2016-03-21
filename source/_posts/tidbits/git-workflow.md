---
title: Git Workflow
date: 2014-11-01 06:50:08
comments: true
tags: 
  - Git Workflow
categories: 
- Tidbits
---

How does code get from a developer's machine through all the steps of testing and integration and deployment? A well-defined process flow is essential. Here are a couple examples of flows I designed and implemented.
<!-- more -->

<div style="width: 600px; height: 480px; margin: 10px; position: relative;"><iframe allowfullscreen frameborder="0" style="width:480px; height:360px" src="https://www.lucidchart.com/documents/embeddedchart/6f0f1f57-d5dc-4621-8ea1-45dd91292de4" id="LAC44A_IRshF"></iframe></div>


A high-level overview of a workflow I used for Enterprise Risk Manager. At the time, this was absolutely revolutionary to me coming from a .Net background and previously being constrained to TFS source control.




<div style="width: 600px; height: 480px; margin: 10px; position: relative;"><iframe allowfullscreen frameborder="0" style="width:480px; height:360px" src="https://www.lucidchart.com/documents/embeddedchart/5f048393-b661-47c8-b42c-fb236b0c31bf" id="ERm42s0kLw5Z"></iframe></div>


###  Git Flow is now part of the github/bitbucket experience.
Standardized git practices are <em>great</em>! Git Flow doesn't totally eliminate merge conflicts, but it helps alot! Each feature branch gets merged into the develop branch. After any conflicts are resolved, develop is then merged into master.
 ![Git Flow shown in Sourcetree](/blog/static/gitflow-sourcetree.png )
