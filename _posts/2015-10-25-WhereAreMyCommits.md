---
layout: post
title: Where are my commits?
tag: Git, GitHub
category: code
comments: True
---
In August I have been very busy coding as a part of [S2DS](http://www.s2ds.org/london.html) but none of my hard work shown on my GitHub contribution panel. Initially I assumed this is because I used private repo. Then I realised that [Lin's commits are showing on hers](http://linbug.github.io/data%20science/2015/09/10/Takeaways-from-S2DS/). I needed to investigate.

Error was on my command line side. I commit using command line, as I find it much faster. In order to keep those commits in sync with your GitHub account your email address must match. If you followed [GitHub advice on keeping email private](https://help.github.com/articles/keeping-your-email-address-private/) then all you need to do is, [in command line](https://help.github.com/articles/setting-your-email-in-git/):

```
git config --global user.email "your_email@users.noreply.github.com"
git config --global user.email
```

You can also set up specific email for single repository, according to [help page](https://help.github.com/articles/setting-your-email-in-git/).

##Side note about Git

Git is one of the most amazing tools I know. Lin have [already reported](http://linbug.github.io/data%20science/2015/09/10/Takeaways-from-S2DS/) on her experience with it. I used for a while, yet, only proper group experience made me truly appreciate its power. Recently I found two good blogs explaining the basics:

* if you never used it, try [this page](http://rogerdudler.github.io/git-guide/)
* if you want to learn more about team work in git, try [this intro](https://www.atlassian.com/git/tutorials/syncing/git-push)

I can only recommend trying. You will love it. And remember, **commit before you pull**, or at least *stash*.
