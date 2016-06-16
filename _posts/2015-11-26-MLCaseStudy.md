---
layout: post
title: Machine Learning Case Study, Week1
tag: ipython, ML
category: ML
comments: True
---

Recently I found yet another machine learning course at Coursera - [**Machine Learning Foundations: A Case Study Approach**](https://www.coursera.org/learn/ml-foundations/home/welcome), which seems to focus on case studies not actual techniques. This is similar to [Foundations of strategic business analytics course](https://www.coursera.org/learn/strategic-business-analytics/home/welcome), repo for which you [can find on my github](https://github.com/DfAC/StrategicBusinessAnalytics), yet seems to offer more solid background in ML. I do like this approach as it allows to see the big picture and understand better a end product.

##Getting started

Course is based on the python commercial package by <https://dato.com/> called **GraphLab Create** - free for one year for academic and learning purpose. It is similar to **pandas**, with more support for online platforms.


##Installation
You can install **dato**  on your machine using your launcher. Since I have working copy of python 2.7.x I decided to install GraphLab into my existing Anaconda using [this setup](https://dato.com/download/install-graphlab-create-command-line.html), which can be summarised as creating new environment and using pip to install GraphLab-Create into it. For all not familiar with [environment concept](http://conda.pydata.org/docs/intro.html), it is directory that contains a specific collection of python packages, allowing to separate and sanitise your code - new versions of specific packages can be installed and tested without affecting your currently working setup.

So to sum it up, all we need to do is:

 ```
conda create -n dato-env python=2.7 anaconda
activate dato-env
pip install --upgrade --no-cache-dir https://get.dato.com/GraphLab-Create/1.7.1/email/LicenseNo/GraphLab-Create-License.tar.gz
conda update ipython ipython-notebook
```

##Running ipython notebooks

This approach changes slightly the way we run the notebooks. We need to fist change to proper environment aand tehn call ipython. From command line it will be 

 ```
activate dato-env
ipython notebook
```

Apart from that week 1 of the course has been very basic and I hope for more action next week.
I will keep you posted how the course goes.
