---
layout: post
title: Converting R code to API
tag: R, plumber
category: code
comments: True
---


I just came back from a local R meeetup and a great [talk by][MarkTalk]  Mark Sellors from Mango Solution. This is first time I heard about  [Plumber](http://plumber.trestletech.com/), which allows to convert your existing R code into an API by adding a few lines of comments to the existing code - very similar in approach to what [roxygen](http://roxygen.org/) auto-generation of user documentation directly from the source code. 

Plumber is using REST API, popular with web applications and in simplification meaning that client don't need to [know anything about API structure](http://stackoverflow.com/questions/671118/what-exactly-is-restful-programming).

What it means in practice is that by adding few lines of `#*` comments to your R code you make it API ready.  This code can be then mounted locally or on server, parsed and ready to receive calls on the specified port. It is really that simple as [Jeff Allen presentation from EARL 2015 shows](http://plumber.trestletech.com/components/earl-2015/#/).

This API can output values and graphs as well, as this [example shows](http://plumber.trestletech.com/docs/endpoints/), which makes it interesting alternative to shiny, where everything is contained inside the app. It does comes with few limitations though (all kudos to Mark Sellors, I am merely [coping my notes from the meetup][MarkTalk]):

* it is not secure, as anybody can call your API
* Input sanitisation
	* plumber is treating any input as text, so you need to cast it before using it
	* more critical are any injection attacks, for example [SQL injections](http://www.slideshare.net/billkarwin/sql-injection-myths-and-fallacies) popularised by [this xkcd webcomic](http://xkcd.com/327/)
* you need to manage and organise logging and monitoring
	* if you unix user tools like [monit](https://mmonit.com/monit/) can help
* the load balancing and state are taken care of yet it is possible to block your API with long calls - make sure functions are quick to execute

I plan to run some quick tests later this week following examples from Mark and Jeff. Will keep you posted.

[MarkTalk]: http://www.slideshare.net/sellorm/creating-apis-with-r-and-plumber-57608851
