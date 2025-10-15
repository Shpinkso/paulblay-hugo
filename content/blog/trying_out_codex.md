+++
title = "Painful Vibe coding with Codex"
date = "2025-10-15T11:37:12+01:00"
tags = ["AI","Application","CI","LLM"]
categories = ["Delivery"]
banner = "img/banners/human_robot.jpg"
authors = ["Paul Blay"]
+++

## Use of LLMs

I've been using LLMs for a while, primarily as a buddy that can help me with ideation or noticing gaps in my thinking.

I rarely use the LLM output directly because it never feels complete or authentic. For written word, I find it can generate pretty generic wording with little impact or personality.

Anything I do take directly, I'll rework pretty heavily - and it's just a judgement of whether doing the rework is more efficient than just starting from scratch.

## Vibe coding

What about coding? 

Well, I've had over 10 years of experience as a developer, but it was a long time ago and focussed on embedded systems - so when I decided to migrate my old Wordpress website to Hugo, there was ample opportunity to vibe some of the bespoke html/css/github pipline code into existance and see what all the fuss is about.

_disclaimer:_ Based on my experience using LLMs for other things, on top of my experience with developing code in general - my expectation was that vibe coding would likely increase speed initially (I don't have to learn the subject deeply), but with a rapidly growing cost of maintenance (I didn't learn the subject deeply).

I'd used plain old chatGPT for help with a few things, such as formatting my markdown tables more clearly. It did the job, but only after many (man) iterations and me reigning it back sometimes with overly audacious changes. Regardless, it was certainly a lot quicker than me learning html, hugo and the theme I was using, well enough to solve the problem myself.

## Promting to Codex

Chat was limited in how much of my live code base it could be aware of and I'd heard a lot about Agentic AI, so decided to try out Codex.

### Prep

Getting things set up was easy enough, just connect to github and select the repo you want to work on.

### Interaction

1. Starting with asking it to help me check for broken links or image references across my site during the preview pipeline, it picks Lychee as the tool and correctly identifies the pipeline to make changes in. 👍

... but it gets the lychee syntax wrong for html return codes to accept - checking the Lychee documentation myself, it's clear that it's wrong. 👎

2. Easy fix though, now lychee moves on to not being able to find (any?) files.

and this is where Codex starts heading off into no mans land. I'm not an expert in github workflows but it seems to go ahead with an attempt to create effectively a hard coded pre-preview site that we can run the lychee tool over.

3. At this point, I just copy/paste the many pages of errors coming from the workflow - I'm not even sure what's going on now.

Ok, it thinks, we just need to change or add these 400 lines across 9 files. Repace a bunch of layout formatting across headers, footers, scripts, categories, search and tags, then our pre-preview will be well again.

4. This is a hard no from me. Replacing or altering layout formatting across my site in order to create a pre-preview sounds like a recipe for disaster. I ask it to think of other solutions, suggesting lychee checks after the preview is published or prior to the live publish step in my deployment pipeline.

It moves the lychee checks to the manual live publish workflow, which is fine-ish, but

5. I want earlier information on problems, can we add it to the preview job, just after the preview site is published? That job gets triggered on every push to origin, so I'll see problems sooner.

It adds the lychee check to my preview site workflow, at the end.

We're now duplicating the checks across both live and preview workflows. 👎

6. Let's not duplcate, get the live to check the result of the latest preview run and only permit if it passed.

Done.

7. Here's where I start to get too disillusioned to continue. Codex makes suggestions that trigger a gut feeling that it's not considering other causes for what I'm reporting. After a couple more tries, I move to manual debugging and ChatGPT support.

Here were some of the problems that Codex couldn't/didn't identify.

* The Hugo build step of the preview workflow was running asynchronously and puclished the preview site I wanted to check prior to the checks being run. Errors were always one run behind.
* Codex was pinning an old version of Lychee, chatGPT picked this up straight away and recommended using the newer one. Why didn't Codex do that?
* The Codex generated code was not scanning .md files, only html. So it was missing all my blog posts.


### Conclusion

I love that someone can make progress developing basic things without having to spend months learning the tools and languages.

**However**, accepting changes that you don't understand (at least to some level) seems highly dangerous. I found that codex struggled more than it should given it had access to the entire code base. I found that using ChatGPT with just the isolated workflow .yml files has been a better experience for me.

I worry a lot about unleashing AI/LLMs on production code, especially with inexperienced oversight. My experience here has only strengthened my thoughts on how a [policy](https://paulblay.com/blog/2025/10/07/ai_in_software_development/) should look for use of AI in software development.


If you want to see my forlorn effort (until I gave up) then it's [here](https://chatgpt.com/s/cd_68ef9219d6088191b4ccf8b0afc16b98)

Thanks for reading!