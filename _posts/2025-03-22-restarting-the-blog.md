---
layout: 	post
title:  	"Restarting the Blog"
date:   	2025-03-22
published:	true
tags:		[jekyll, github, ruby]
comments:   true
---

#### Picking up where I left off...
So, I finally decided to dust off the blog again. Which of course meant updating the configuration and setup, breaking everything, fixing it, and adding some fresh new things.

First, it meant setting up Jekyll again.

#### Setting up Jekyll again
Here, I wanted to try out how useful AI might be for the task. I decided to consult [Le Chat](https://chat.mistral.ai) on how to setup Jekyll on Windows. Easy enough:
> Download and install Ruby from the [RubyInstaller for Windows](https://rubyinstaller.org/)

Here we reach obstacle **#1**: Windows doesn't know the installer, and nags about whether I want to even run such un-authenticated software. I proceed and succeed in installing jekyll:

> `gem install jekyll bundler`

Since it's been a lot of years since I last updated the blog, a lot of Jekyll versions have come and gone. I decided to use the fresh jekyll builder:

> `bundle exec jekyll build`

Which generated a fresh `_config.yml` and `Gemfile` that I could reference. 

That brings us to obstacle **#2**: The latest Jekyll version, `4.4.1`, has of course meant a lot of old plugins being deprecated in favor of new ones. E.g. `jekyll-paginate` has been replaced by `jekyll-paginate-2`, etc.

So, I proceeded to remove and replace plugins. After a few rounds of trial and error, I got the fresh config to build, and everything sort of worked locally.

Everything seemed ready to go: just commit, push and refresh the website.

Alas, everything was a bit off, various pages went 404 instead of displaying like they did locally. Another obstacle has arrived (**#3**): [GitHub Pages](https://pages.github.com/versions/) doesn't support the latest Jekyll version: `4.4.1`, but only `3.10.0`.

The solution then, it's to actually run Jekyll via a GitHub action, whereby the html gets generated on GitHub and then published. Jekyll has a [guide for it here](https://jekyllrb.com/docs/continuous-integration/github-actions/).

Even that needs some adjustments, because a gemfile generated on Windows, of course has platform specific configurations, which doesn't work on Linux (which GitHub actions runs on). The Ruby version in the default GitHub action for Jekyll was also too old.

But finally, everything seems to just work now. I even added a [cool tag cloud](/tag/).