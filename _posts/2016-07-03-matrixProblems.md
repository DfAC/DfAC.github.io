---
layout: post
title: Don't use pandas for matrix operations
tag: code, python, pandas, numpy
category: code
comments: True
---

## Twilight of Matlab


I am used to doing my matrix calculations in Matlab - it is a great tool to do. Yet, over the last few years, I have migrated to python and R. There are many reasons to explain the shift, with the active online discussion. For a starter, I recommend reading this [Matlab forums](https://uk.mathworks.com/matlabcentral/newsreader/view_thread/341003).

In a nutshell, Matlab is amazing for its matrix operations but has weaknesses in other areas. It has fallen behind python and R in interactive bits (especially workbooks) and with every new edition it seems to go Microsoft Office way - simplify for beginner users, make it annoying for more experienced ones. It has advantages: it is by far the easiest to learn and [Matlab simulink](http://uk.mathworks.com/products/simulink/) don't have any replacement yet.

For more in-depth comparison I also suggest [reading this post](http://www.pyzo.org/python_vs_matlab.html).

## Machine learning in python

Andrew Ng [Machine Learning course](https://www.coursera.org/learn/machine-learning/home/welcome) is based on Matlab. I decided to try to do it both in Matlab and python. I was not the first, [Lyn did it last year](http://linbug.github.io/data%20science%20tools/2015/07/07/Coursera's-machine-learning-exercise-one-(in-Python)/).

Yet as I progressed I realised that there was a problem. During the simple matrix multiplications, results which should be (m,1) become (m,m) To keep the story short - the culprit was pandas' data frame and its interaction with numpy for matrix operations.


![](https://upload.wikimedia.org/wikipedia/commons/3/3a/Su_Lin_giant_panda_bear_cub_at_the_San_Diego_Zoo.jpg "The culprit")


Let's start with example[^1]

```
import pandas as pd
import numpy as np

data = pd.read_csv('ex1data1.txt', header = None)
# assign the first and second columns to the variables X and y, respectively
X = np.c_[np.ones(data.shape[0]), data.iloc[:,0] ] 
y = data.iloc[:,1]

v = X.dot(theta) - y
v
```
This will produce (m,m) matrix (full of NaNs) instead of (m,1). Problem has to do with pandas' data frame indexes as [explained on stackoverflow](http://stackoverflow.com/questions/16472729/matrix-multiplication-in-pandas).

What would be the solutions?

## keep it simple

Matrix operations are done using numpy. It is more correct to simplify pandas data frame to numpy arrays and this way avoid all the problems later one. Let me demonstrate this: 

```
data = pd.read_csv('ex1data1.txt', header = None)
# assign the first and second columns to the variables X and y, respectively
X = np.c_[np.ones(data.shape[0]), data.iloc[:,0] ] 
y = np.c_[data.iloc[:,0]]

X.dot(theta)-y #residuals
```

This will produce results as expected.

## Takeaway

The lesson for today: 
**Use most simple variables for the functions**. Do not depend on auto-casting, there might be hidden pitfalls[^2] that you are not aware of.  Introduce forced casting in your functions or classes. Just in case.


[^1]: If you want to run example yourself, a copy of 'ex1data1.txt' can be [found in my repo](https://github.com/DfAC/Coursera-s-machine-learning-course/blob/master/ex1/ex1data1.txt)
[^2]: For more pandas gotchas [check here](http://pandas.pydata.org/pandas-docs/stable/gotchas.html)
