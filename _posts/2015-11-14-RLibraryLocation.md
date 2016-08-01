---
layout: post
title: How to synchronise your R libraries between different PCs
tag: R,
category: code
comments: True
---


I am using my R on a few computers (sometimes in the same time) and I do find it annoying when some libraries which I installed on one are missing on other. My usual solution was to use Dropbox and synchronise between my accounts. With R I had a problem, as defining library location required changes directly to R, hidden behind RStuido. I was in hurry so I gave up. 

Recently, I have found [stackoverflow solution](http://stackoverflow.com/questions/15217758/remove-a-library-from-libpaths-permanently-without-rprofile-site) and [this blog post](http://blog.revolutionanalytics.com/2015/11/r-projects.html) which made me re-visit problem again. Workflow below, shows my current solution:

* used *.libPaths()* inside R to check current library paths;
* identified which paths to keep. In my case it keep R original library but removed link to my documents;
* found R-Home path using *R.home()* or *Sys.getenv("R_HOME")*;
	* R-Home\R-3.2.2\etc\Rprofile.site is read every time R kernel starts, so any modification will be persistent to every run of R
* edited R-Home\R-3.2.2\etc\Rprofile.site by adding[^]

```
# set library paths
.libPaths(.libPaths()[2])
```
	
* restarted R (Ctr+Shift+F10).

[^]: note that I use Unix path notation despite using windows. R always use Unix notation, regardless of operating system. Also don't add final "\".
