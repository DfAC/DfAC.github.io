---
layout: post
title: Making git repos small again
tag: git, data
category: code
comments: True
---

I have been recently struggling with large git repo - it contained large data files I did not longer needed. Up to this point I preferred not to add data files to repo to avoid problems like this. This can't be avoided if you share your code with other uses, without datasets, or fork exisitng repos. I was also looking at using something that is not destructive - end of the day you want your git to contain all the history so you can always replicated previous code.

To cut the story short I have located excellent package to do so [BFG](https://rtyley.github.io/bfg-repo-cleaner/) written in Scala. It is  lightning fast (according to author it is 100x faster than `git-filter-branch`). After downloading java package, if you want to remove all files bigger then 30M from your git repo just type

```
cd your-repo-dir\
java -jar bfg.jar --strip-blobs-bigger-than 30M
```

This will not remove the files, it merely makes it for deletion. To alter your database you need to prune database yourself

```
git reflog expire --expire=now --all && git gc --prune=now --aggressive
```



##Aliases in DOS

As a side note above code can be simplified using aliases. Following [this post](http://superuser.com/questions/560519/how-to-set-an-alias-in-windows-command-line) all you need to do is

```
doskey bfg="java -jar d:\DIR-to-SOFT\bfg-1.12.8.jar"
doskey /MACROS:ALL
```
And then above code becomes 

```
bfg --strip-blobs-bigger-than 30M
```

For more info check `doskey /?`.

##Running it against git hub

This approach will not work if the history you are chanching is already on remote repo (for ex github). As above approach change history, you wont be able to `push` and `pull` will just restore your changes.
Instead we need to make a local bare repo, pack it, change it and then push. A bit more work indeed, yet we usuall as in code below

```
git clone --mirror git://example.com/some-big-repo.git
cd some-big-repo.git
git gc --auto
git repack -d -l
bfg -b 30M
git reflog expire --expire=now --all && git gc --prune=now --aggressive
git push
```

This will force push to master and shrink both local and remote copy.
