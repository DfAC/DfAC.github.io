---
layout: post
title: How can I git python notebooks?
tag: python, git
category: blog
comments: True
---

I suspect I am not the only one struggling with using git for version control of [Jupyter Notebooks](http://jupyter.org/). While intended to make it easy to publish code online they are notorious for mixing code with the output making it difficult to properly identify changes and also bloating repositories with unnecessary code output.

There are quite a few solutions discussed on the internet, mostly varying between using a filter or [pre-commit git hooks](http://githooks.com/). Both operate in roughly the same manner - output is stripped before code is being committed, focusing on changes in code only.

## So how should I do it?

So, what is the easiest way to implement those solutions? Use [Florian Rathgeber](https://github.com/kynan/nbstripout) pip package. To install it type:

```
pip install nbstripout
pip install nbconvert
```

Then, to initialise a new repo with ipython notebooks type:

```
git init
nbstripout --install
```

What is happening in the second step? We are defining [Git filter](https://git-scm.com/book/en/v2/Customizing-Git-Git-Attributes) that will be used every time we commit. This will take care of the output cells before committing. The detailed code responsible for the *git filter* can be seen by using `cat .git\config`.

From now on all you need to do is commit as usual. And the above code will work it magic behind.


## keeping certain outputs

What happens if you want to keep specific output? Use the *"Edit Metadata"* button on the [desired cell to enter](https://github.com/kynan/nbstripout) 

```
{
  "keep_output": true,
}
```
or 
```
{
  "init_cell": true,
}
```



## Other approaches

From reading other blogs it seems that [git hooks](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks) might be another approach. I will discuss it once I tired it. 
