---
layout: post
title: Writing articles with markdown
tag: R, markdown, word
category: blog,code
comments: True
---

For a few months now I have been embracing markdown as my note taking tool and recently I have decided to take things further - write a full report in Markdown. Interestingly impulse to do so came from the post discussing [shortcoming of the markdown](http://www.adamhyde.net/whats-wrong-with-markdown/). Adam have a very good point with non-standardised format yet I felt he was mistaken on the HTML front - I never expected markdown to replace web design. Then it stroke me - I did expected markdown to replace Latex with smaller documents.

## Perils of Latex

Latex is amazing tool for [writing and managing complex documents](http://tex.stackexchange.com/questions/1756/why-should-i-use-latex). I, similar with other people producing PhD thesis or any academic work, can't imagine working with anything else. I create most of my documents in Latex as well as all of presentations (beamer) and a lot of visuals (tikz).
Yet it is not without some major shortcomings:

* Learning curve is steep and using dedicated processors like [Lyx](https://www.lyx.org/) just hides complexity and severely cripple your learning
* Probably everybody agrees that its initial settings are same as Windows - needed to be changed to produce something looking nice. And it does take a while to do it.
* Missing libraries are major pain.
* There is probably a whole section of Hell where you look for missing brackets or misspelled command in large Latex document.

Online editors such as [ShareLatex](https://www.sharelatex.com/) and [Overleaf](https://www.overleaf.com/) will make any work easier. In case of presentations just use [metropolis](https://github.com/matze/mtheme) - amazing visuals straight from the box. Just check my [uni teaching slides](https://github.com/DfAC/TeachingSlides).


## Back on the track - initial approach with RStudio

So why do we discuss markdown if I prefer Latex? I am not alone in thinking that best way to produce document [is working in pure ASCII](http://ricardo.ecn.wfu.edu/~cottrell/wp.html) yet problems with Latex syntax does prevent proper deep focus. Another nudge came from reading [Deep Work by Cal Newport](http://www.amazon.co.uk/Deep-Work-Focused-Distracted/dp/0349411905) - I decided to focus on writing my next report in distraction free environment.

## Testing without RStudio

With limited time (week to go) I decided to use Rstudio as it has a [good description of R markdown](http://rmarkdown.rstudio.com/). Two things I needed to have with my document, that are not part of markdown, where:

* references - report was my teaching practice which required heavy citation
* cross references within document (I like things tidy)


### Cross references

To create cross references use HTML tag, for example top header would be `#<a name="Introduction"></a> Introduction`. I can then reference to it using `As discussed in [Introduction](#Introduction)`.


### References

including discussion about [adding references](http://rmarkdown.rstudio.com/authoring_bibliographies_and_citations.html).

I followed their approach quite literary with bibtex document created using [JabRef](https://github.com/JabRef/jabref) and downloaded cls from <https://www.zotero.org/styles>. All you need now is:

* Add citations in the text itself
```
As covered in previous research [@Nicometo2010]. @Nicometo2010 discussed that as well. 
Another aspect have been covered already [@Felder2012;@Taylor2011;@Fry2008].
```
* Amend R markdown (rmd) header (don't forget surounding --)
```
title: "Efficient teaching to the large class of engineering student"
author: "Lukasz K Bonenberg"
output:
  html_document:
    highlight: pygments
    theme: cerulean
    toc: yes
bibliography: refs.bib
csl: emerald-harvard.csl
```
* Kit in in RStudio



## Going for dark side (hey, they have cookies...)

A next stage was to create Latex template and kit to Latex. This is when I decided to take short-cut via dark side. With this setting it is extremely easy to output to [Word](http://blog.rolffredheim.com/2013/02/reproducible-research-with-r-knitr.html). This ouptut can be modified by the use of [templates](http://rmarkdown.rstudio.com/articles_docx.html). All you need to do is to amend the header

```

title: "Efficient teaching to the large class of engineering student"
author: "Lukasz K Bonenberg"
output:
  word_document:
    fig_caption: yes
    highlight: pygments
bibliography: refs.bib
csl: emerald-harvard.csl

```

And create output word document. You can then edit document to your liking, rename it *template.docx* and knit nice looking output. It will also compile any latex equations or included graphics properly.

```
title: "Efficient teaching to the large class of engineering student"
author: "Lukasz K Bonenberg"
output:
  word_document:
    fig_caption: yes
    highlight: pygments
    reference_docx: template.docx
bibliography: refs.bib
csl: emerald-harvard.csl

```

## Take two - pandoc

[**Pandoc**](http://pandoc.org/) is a conversion engine behind R markdown and knit. Just to see full picture I decided to compile my document without RStudio directly in **pandoc**.

**Pandoc** recognise citations and cross sections as well as utilise docx template. To compile my document you need to use the following command: [^1]

```
pandoc ATPreport.rmd --filter=pandoc-citeproc --biblio=refs.bib --csl=emerald-harvard.csl --reference-docx=template.docx --highlight-style=pygments --output=report.docx
  
```


Results are same as with RStudio apart from R code reduced to static text. I would strongly recommend playing with **pandoc**. Amount of different formats it can output is [simply amazing](http://pandoc.org/demos.html). For anybody experimenting with **cls** styles [this repo should be very helpful](https://github.com/KurtPfeifle/pandoc-csl-testing).


## Summary

This approach worked really well allowing me to focus directly on writing text (with references) and not being distracted by compiling errors or missing brackets. As I was using RStudio I could also generate few simple plots from data.

What I want to do next is to generate similar output in PDF using Latex. No short cuts this time.








[^1]: You can replace = with space (' ') but you can't mix it - pandoc will throw strange error. 
