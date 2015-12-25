---
layout: post
title: Making git repos small again
tag: git, data
category: blog,code
comments: True
---

I have been recently struggling with large git repo - it contained large data files I did not longer needed. Up to this point I preferred not to add data files to repo to avoid problems like this. This can't be avoided if you share your code with other uses, without datasets, or fork exisitng repos. I was also looking at using something that is not destructive - end of the day you want your git to contain all the history so you can always replicated previous code.

To cut the story short I have located excellent package to do so [BFG](https://rtyley.github.io/bfg-repo-cleaner/) written in Scala. It is  lightning fast (according to author it is 100x faster than `git-filter-branch`). After downloading java package, if you want to remove all files bigger then 30M from your git repo just type

```
cd your-repo-dir\
java -jar bfg.jar --strip-blobs-bigger-than 30M
```

This will not remove the files, it merely makes it for deletion. To alter your database

##Aliases in DOS

As a side note above code can be simplified using aliases. Following [this post](http://superuser.com/questions/560519/how-to-set-an-alias-in-windows-command-line) all you need to do is

```
doskey bfg="java -jar d:\tmp\Dropbox\Programming\skrypty\bfg-1.12.8.jar"
doskey /MACROS:ALL
```
And then above code becomes 

```
bfg --strip-blobs-bigger-than 30M
```

For more info check `doskey /?`.

##Running it against git hub

This approach will not work if your code is already on remote repo (for ex github). As above approach change history, you wont be able to `push` and `pull` will just restore your changes.
Instead we need to make a local bare repo, change it and then push, as in code below

```
git clone --mirror git://example.com/some-big-repo.git
bfg --strip-blobs-bigger-than 30M
bfg --strip-blobs-bigger-than 30M
git push
```

This will shrink both local and remote copy.
