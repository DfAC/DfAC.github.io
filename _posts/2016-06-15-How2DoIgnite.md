---
layout: post
title: Enlighten Us, But Make It Quick
tag: public speaking, conference, programming
category: blog, advice
comments: True
---


[Ignite](http://www.ignitetalks.io/)  is a series of fast 5 minute long talks on any topic, from technology to culture to business to philosophy. The goal of the talk is to entertain and educate the audience. The event is either stand alone or part of large conferences.  A great example is [Scott Berkun one](https://www.youtube.com/watch?v=rRa1IPkBFbg) discussing the spirit and technicalities of Ignite.

![](http://cdn.oreillystatic.com/en/assets/1/eventprovider/1/ignite_logo_white_bg.gif "Ignite logo")

The most interesting is the layout of presentation: every speaker has exactly 20 slides, which will auto-advance every 15 seconds. This makes it both exciting and intimidating at the same time. As one of my co-speakers, [Alistair Croll](http://solveforinteresting.com), put it "its the closest things to stand up comedy in public speaking". To sum it up, the main selling points behind [Ignite](http://www.ignitetalks.io/) are:

* taking your presentation skills to next level (or at least showing you how to get there);
* it is great fun and its good starting point for any networking;
* it gets you places (more on it later...).

## Why have I done it?

Strata+Hadoop World is one of the biggest events in the data scientist diary - it is an opportunity to listen to the line-up of speakers and to learn what is behind the horizon. This year attending the [accompanying Ignite event](http://conferences.oreilly.com/strata/hadoop-big-data-eu/public/cfp/477) provided speaker with a free bronze ticket. I felt this was a great opportunity: not only could I gain access to a great conference, but also try to create a markdown presentation, get  very useful public speaking experience and good starting point for networking.

## Why should you read this blog

There is already a large number of blogs and articles focusing on Ignite preparation. I felt that adding to this corpus will be useful for two reasons:

* I have presented an advanced technical topic, related to my current academic research, but aimed at general audience;
* I wanted to create my presentation in a distraction-free environment and within a specific time limit: two days for the abstract and a week for the presentation and practice.

The second goal sprang from reading [Deep Work by Cal Newport](https://www.amazon.co.uk/Deep-Work-Focused-Success-Distracted/dp/0349411905) and aim to create a distraction-free environment. To do so I focused on using the very versatile[markdown](https://daringfireball.net/projects/markdown/), which I use it to [write my blog](http://dfac.github.io/), take notes or create fully working reports in Word, for details see my [February post](http://dfac.github.io/blog,code/2016/02/16/Writing-Articles-with-Markdown/). OOn this occasion I wanted to use the same approach to create a fully working presentation. BTW, if you not familiar with markdown, [this guide](https://guides.github.com/features/mastering-markdown/) is a good starting point.


#  Ignite talk takeaways and advice


Let me start with the takeaways: I really enjoyed my talk - it was stressful yet very rewarding. I met great people and I felt that all the hard work really paid off. My main advice, if you want to do it (and I recommend you do):


* Five minute talks are very easy to get wrong on the day despite all preparations - **make slides visual and limit amount of text**;
	* This gives you flexibility if things go a bit wrong;
	* As you practice you should not feel the need to change slides, but your talk;
	* You will feel more confident as the audience is not likely to notice if things got slightly out of hand.
* **Less is more**. Focus on one main idea and hammer it home;
	* Be very strict - one message per slide;
	* Be consistent and talk slowly. It makes it easier for the audience to understand, you appear more confident and have enough time to plan ahead.
* **Pauses are extremely useful** - it allows you to:
	* Control the flow of your presentation;
	* Bring the attention of the audience back to yourself;
	* Have time to recover and relax if things go wrong.
* **You get what you give**. The more you prepare the better you feel and the more you will take from this experience. *This is probably the universal truth*.


## How long does preparation take?

It took me about a week to prepare the talk and the split was:

* One evening (2-3 hours) to prepare the abstract;
* Two evenings (5-8 hours) to prepare and send the presentation itself;
	* I fenced off time from 17:00 every evening and I used my workflow to limit any distractions;
	* I spend about 2 hours on the first evening goofing around.
* Long weekend (3 days) to rehearse my presentation, demo it to a friend and finalise everything;
	* A lot of time was spend on taking a breaks and working on other things. You need to spread your attempts over few days and take larger breaks to memorise properly. It is better to take an hour over few days than try to cram everything in one day.
* I took an hour on the presentation day to practice it again.

Let's get down to technical details.

# Getting the talk ready

## Prepare talk abstract

* Start with an idea that is interesting for other to listen to, and write it down in a  few sentences.
	* The nature of the talk is quite unforgiving so you need to be well versed in the topic.
	* I think it’s easier to start with a topic you are really familiar with and enthusiastic about. It will show in your talk and also help you focus.
	* Make sure that topic is interesting for non-expert audience.
* Think **why** someone would be interested and what will be their main **takeaway** from the talk, this [blog post might help](http://www.markpollard.net/8-tips-for-your-ignite-presentation/). Discuss your topic with somebody outside of your field to check if this is really the case.
* Consider your topic as a story, think of your idea (topic) as one of the [hero archetype](http://www.soulcraft.co/essays/the_12_common_archetypes.html) and follow story cycle from [Park Howell blog](http://businessofstory.com/the-story-cycle-a-simple-10-step-storytelling-process-to-create-abundance-in-your-business/).

<img src="http://29jedk1t4b4k3o7vu2867f4z.wpengine.netdna-cdn.com/wp-content/uploads/2014/08/Screen-Shot-2014-08-20-at-11.08.35-AM.png" alt="Story cycle" style="width: 350px;"/ alight = "left">

This should be enough to write a short summary and describe what you are going to present. My abstract can be found on [S+H World London Ignite schedule page](http://conferences.oreilly.com/strata/hadoop-big-data-eu/public/schedule/detail/51480). Apart from it I wrote 300 words summary.


# Getting the presentation ready

As described in the introduction, I wanted to fully replace PowerPoint with markdown, but mostly due to time restrictions (I had just over a week) I decided to go half way: prepare initial drafts in markdown and the final product in Microsoft PowerPoint (and Libre Office). I felt that making a good visual presentation with 15 seconds per slide  might be too much of a challenge at this stage. This also gave me the time to focus on rehearsing the talk itself. I would like to note that my work-flow was strongly influenced by [Olivia Mitchell's post](http://www.speakingaboutpresenting.com/content/fast-ignite-presentation/).

## Layout

I used markdown to prepare a mockup of the presentation - first I split the talk into 4 parts, based on the storytelling example. Then, using text only markdown, I noted one idea per slide. Even if you have an existing PowerPoint presentation I strongly suggest to start from scratch as an Ignite slide deck will be different. I also set up a clock and limited myself to 30 min to finish this task.

The first five slides of my mock up file (*outline.md*) looked like this:

```
# Navigation
# Hidden utility
# Example why we use
# Hidden utility
# GPS
```

The easiest way to compile a presentation is either to use [RStudio](http://rmarkdown.rstudio.com/beamer_presentation_format.html) or the amazing [pandoc](http://pandoc.org/). I suggest pandoc and using  `pandoc -t beamer outline.md -o presentation.pdf` to create the PDF presentation.

## Talking it through

[Presentation voice and writing voice are very different](http://userfirstweb.com/328/successful-ignite-presentations/). I use my compiled presentation and stopwatch to talk through my presentation at a slow speed. I used this to fine tune presentation and pin down the main point for each slide. Interestingly, this exercise lead to restricting my talk and making it more focused on the main topic. I  changed the text of the presentation accordingly and tested again. It will take a few trials and eventually you will feel that presentation is flowing nicely. Remember the [80-20 rule](https://en.wikipedia.org/wiki/Pareto_principle) and don't overdo it - it should be fit for purpose and that's it.


## Adding graphics

Ignite is a very rapid affair and it takes a lot of effort to make a [good looking presentation with text](http://www.slideshare.net/otikik/how-to-make-awesome-diagrams-for-your-slides). Once I got my slides' idea sorted out I focused on making them very visual to:

* make audience focus on what I was talking about;
* emphasis one point per slide;
* give me flexibility if things go a bit wrong. You will also feel more confident - audience is not likely to notice that things got slightly out of hand.

For graphics I wanted to use either my (or University) art, public domain images or ones under [creative commons licence](https://creativecommons.org/licenses/). From experience and [Lifehacker post](http://lifehacker.com/197538/geek-to-live--6-ways-to-find-reusable-media) I would recommend:

* <https://pixabay.com/>
* <http://www.everystockphoto.com/>
* <https://commons.wikimedia.org/wiki/Main_Page>

To maintain proper attribution I have placed links and descriptions directly into my markdown file. In case you lost references, the easiest way to find it is reverse search, for example [Google one](https://images.google.com/) - upload your picture and similar will be found.

My final  *outline.md* looked like that:


```
I suspect nobody came here using  traditional maps. The mapping applications are so useful.
![pixelcreatures/CC0](https://pixabay.com/static/uploads/photo/2015/09/14/23/36/compass-940370_960_720.jpg)

---

it easy to follow directions, allowing us to focus on important parts of the day.
![Dean Hochman/CC BY 2.0](https://upload.wikimedia.org/wikipedia/commons/a/a2/Arrows_%2816064489288%29.jpg)
Dean Hochman / [CC BY 2.0](https://commons.wikimedia.org/w/index.php?curid=44742195)

---

We are transient society, we want to things quick - this is becoming a habit.
Mapping applications act as butler, leading us to interesting places, allowing to meet friends or see famous landmarks.
Craftsmanship of facade make us think about humanity brain child behind it. Knowledge as corner stone.

![vifra/CC0](https://pixabay.com/static/uploads/photo/2015/09/07/09/54/rome-928325_960_720.jpg)

---

what drives forward is position provided by the **hidden utility**, working behind the scenes. It allows is to create a lot of amazing applications.

![SomeDriftwood/CC BY 3.0](https://upload.wikimedia.org/wikipedia/commons/thumb/2/2f/Clock_Cogs.jpg/800px-Clock_Cogs.jpg)
SomeDriftwood / [CC BY 3.0](https://commons.wikimedia.org/wiki/File%3AClock_Cogs.jpg)

# GPS

32 SV 20,200 km away in MEO. Not so old, created in '70.
Uni fig
```

## Making final PowerPoint presentation

O'Reilly requested presentation in Microstoft PowerPoint format. As discussed before, I didn’t  create the final presentation from my markdown document, I was aiming for distraction free working environment, and trying to make the presentation  look good and advance every 15s was too difficult on this occasion.

My final presentation can be found at [Slideshare](http://www.slideshare.net/LukaszKosmaBonenberg/superhero-gps). You might notice I put the title and my name on last slide. I did this to improve the flow at the beginning of the presentation and to give myself time to wrap up and reiterate the main takeaway. Before sending it to the organisers I had practised my talk on two screens. The last few days before the conference I   spent  practising it.


<iframe src="//www.slideshare.net/slideshow/embed_code/key/rslWAughvGQpk5" width="595" height="485" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC; border-width:1px; margin-bottom:5px; max-width: 100%;" allowfullscreen> </iframe>


# Rehearsing presentation

## Preparing the ground

At this stage of the presentation your slide deck is completed and you are ready to focus on practising delivering the presentation. As you practice you might notice that certain things don't work after all. Don't worry about changing the slides, focus on telling the story. To do so I:

* Practised the whole presentation a few times, noticing areas where I stumbled or made a mistake;
* I created anchor points every 2-3 slides - places where I should be able to make a pause before moving to another part;
* I practised both identified problematic areas and anchor points only, no less than three slides at a  time;
* Based on those I noted key concepts and words I wanted to use on each slide in my *outline.md*.


I cannot state it well enough - repetition is a key here. As [Jason Grigsby notices](http://userfirstweb.com/328/successful-ignite-presentations/) you are not memorising your presentation - you are practising delivery and adjusting it on the fly. Five minutes presentation are brutal and you have to be quick on your feet to recover it. To support that I purposely separated notes from slides - I didn't want to develop any habits.

## Finalising the preparation

With those ready:

* I practised the full presentation, focusing on recovery, should I make any mistakes;
* I aimed to speak slowly and clearly and to give myself a five second pause before key slides - I recorded myself to check it;
* I arranged a presentation to a friend - it is different when you talk to somebody. He also provided me with feedback leading to changes in the presentation and removing unnecessary references;
* I practised it a few times more and went to bed early.


# Delivering the talk

## Before the talk


It goes without saying - be there early. Most of my co-speakers had been on pre-conference workshops while I arrived about 20 minutes before agreed time. This gave me an opportunity to wind down, talk to others and prepare mentally. With five minutes you don't have the luxury of  repetition or graceful recovery - give yourself time to get in the peak state. You worked hard for it.

* A few people checked their slides before the talk. I didn't but in retrospect, this is a great idea;
* Talk to other speakers - its nice to have friendly faces next to you;
* Make sure you learn how everything works.

# Talk itself

Talks are 5 minutes long so it takes about 40 minutes to run through them and time will fly fast.

* Take pictures for others, tweet and have great time;
* You know your anchors, use them;
* Use pause for dramatic effect or just to recover;
* You will rush so try to speak slowly and take breaks;
* When it’s your turn - take a deep breath and relax, you practised hard.


![**My Ignite lineup**](https://c5.staticflickr.com/8/7537/27138322420_108f6018b3_z.jpg "Ignite lineup")

## Feedback

Take a few minutes after the event to get some feedback. It might be difficult to get it from others - just try to think what you would do differently if you  did it again. On my occasion it was:

* I held microphone too low;
* I moved a bit too much on the stage - it allowed me to relax but prevented me from having a good photo taken and caused problems with the microphone;
* I hardly looked at my slides as I faced the audience at all times. This would prevent me from reading any helpful notes, should I have any;
* Next time I would stay a bit back on the stage and move in the centre axis of the stage.


# What next

* I would like to do another Ignite talk within 4-6 months.
*I want to fully develop a workflow to create PowerPoint presentations from markdown. I would like to make it similar to my [existing Beamer presentations](https://github.com/DfAC/TeachingSlides) and have the ability for full size graphics and text overlay.
	* some existing resources:
		* [Customising Beamer in markdown](http://andrewgoldstone.com/blog/2014/12/24/slides/);
		* [Customising Beamer in markdown via pandoc](http://jeromyanglim.blogspot.co.uk/2012/07/beamer-pandoc-markdown.html);
		* [Pandoc examples](http://pandoc.org/demos.html);
		* [RStudio presentations](http://rmarkdown.rstudio.com/beamer_presentation_format.html).
* [Swipe](https://www.swipe.to/markdown/) looks like an interesting alternative.