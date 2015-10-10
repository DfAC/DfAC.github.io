---
layout: post
title: Publishing your code online
tag: R, python, jupyter
category: coding, blog
comments: True
---

#Publishing your code online

My most popular languages for data analysis are python and R. I like them for different reasons, and while recently I use predominantly ipython with pandas, I still think ease of visualising things in R is next to none.
One extremely useful thing in both languages is the ability to display your code online:

* [ipython notebooks (jupyter)](https://jupyter.org/) for python
* [kinitr](http://yihui.name/knitr/) for R

As of recent both of those can be natively displayed in github as well.



##Rendering jupyter directly via Nbviewer

jupyter can be can be [natively displayed in github](http://blog.jupyter.org/2015/05/07/rendering-notebooks-on-github/). Why bother with rendering via Nbviewer? The quick answer is:

* it gives much better impression, with most of screen estate concentrated on displaying code
* it does hide all distracting github mechanism

How we do it then? Summarising [this stackoverflow post](http://stackoverflow.com/questions/19744286/hosting-ipython-notebooks-on-github):

* format is *http://nbviewer.ipython.org/ + github/ + USER_NAME/link2file_with_blob*
* for example  <http://nbviewer.ipython.org/urls/github/DfAC/Coursera_DataAnalysisandInterpretationSpecialization/blob/master/DataVisualisation_week03.ipynb>. 

This will cache notebook on nbviewer server, allowing for quick display but reducing update from source to every 2 hours. This might be a problem, especially if its live project. If you willing to trade the speed away, you can disable flush for almost live update

* format is *http://nbviewer.ipython.org/ + github/ + USER_NAME/link2file_with_blob + ?flush_cache=true*
* for example  <http://nbviewer.ipython.org/urls/github/DfAC/Coursera_DataAnalysisandInterpretationSpecialization/blob/master/DataVisualisation_week03.ipynb?flush_cache=true>. 

Still not feeling convinced? Compare two links to Probabilistic Programming and Bayesian Methods for Hackers:
* [directly via gihub](https://github.com/CamDavidsonPilon/Probabilistic-Programming-and-Bayesian-Methods-for-Hackers/blob/master/Chapter1_Introduction/Chapter1.ipynb)
* [via nbviewer](http://nbviewer.ipython.org/github/CamDavidsonPilon/Probabilistic-Programming-and-Bayesian-Methods-for-Hackers/blob/master/Chapter1_Introduction/Chapter1.ipynb)


I hope this convinced you. Let me know, in comments below, if you have any more tips.


##Rendering knitr

R knitr can be published via http://rpubs.com/ which [looks very much like nbviewer](http://rpubs.com/DfAC/as2) and allows to publish [directly from RStudio](https://rpubs.com/about/getting-started) which makes things easy. Unfortunately it does not allow for easy integration with github. Code will be [kept separately](https://github.com/DfAC/ReproducibleResearch/blob/master/PA_2.Rmd).

This has limited my interest in R knitr, as I couldn't just edit my github code online. This might be changing as [this article](http://www.r-bloggers.com/ipython-markdown-opportunities-in-ipython-notebooks-and-rstudio/) report that R code can be run directly in the jupyter. On my to do list.
