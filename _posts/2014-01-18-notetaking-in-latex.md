---
layout: 	post
title:  	"Notetaking in LaTeX with TextMate 2"
date:   	2014-01-18 19:04:55
published:	true
tags:		[latex]

---

**_For the actual guide, skip to "ingredients"_**

Notetaking has always been a messy thing to do *just right* for myself. Every time I try another format or app, there's some feature missing in action or worse yet - there are unnecessary ones that destroy my workflow. Often times I almost consider exclusively using pen and paper.

For the majority of my time at gymnasium (danish equalivalent of high school, with some differences) my notetaking has been done with Google Docs. The upsides is frictionless switching between platforms and devices, my documents are simply right there, available at any time. The ability to easily share notes or even invoke a 30 person class hive mind is a fantastic thing.

But there was a problem. Subjects like math, physics and chemistry required precise notation that wasn't possible in any correct or quick way in Google Docs. Until then I used notetaking on paper, but I'd really like my stuff digitally archived and easily searchable.

The solution was found in LaTeX. A cumbersome beast, and one I'd already grown familiar with, using it before on a math class project. But the wiki system that we used was way too slow and cumbersome to fit the bill. Editing became a huge mess when we reached the end.

I found StackEdit, which seemed perfect as it could integrate seamlessly into Google Drive and run in the browser. It supported Markdown and Mathjax (essentially the math part of LaTeX), had live preview and seemed perfect. But the software felt off, and often times my notes simply wouldn't load or took too long to do so. It also couldn't handle more than one document at a time. It was beautiful to be able to write redox reactions as quickly on my keyboard as I could on paper, but I was ready to give up.

But I think I've found a recipe that makes it work.

#### The ingredients:

* [MacTeX](http://tug.org/mactex/)
* [TextMate 2](https://github.com/textmate/textmate)
* [Save-On-Focus-Lost](https://github.com/bomberstudios/Save-On-Focus-Lost.tmbundle)
* [Skim](http://skim-app.sourceforge.net) (optionable)

Now, a note: yes the exact system here will only work on Mac OS X. But, there's tons of different solutions (multi-platform too) that support live preview for LaTeX, this has just been the most optimal for my Macbook, which is my primary notetaking device. My desktop PC will be just as able to use this workflow, just using other applications and that's the true beauty - I'm not going to be locked into anything from now on. Just pure LaTeX and some nifty live preview magic.

#### The Setup
The applications themselves are fairly staightforward to setup. If you're having trouble with the template or generally using LaTeX, you need to look elsewhere for help on that.

To get started though, we need to get the Save-On-Focus-Lost bundle for TextMate up and running. Then we also need to do a bit of configuring for LaTeX in TextMate.

**Installing _Save-On-Focus-Lost_:** You can try following the installation instructions on the github page Save-On-Focus-Lost. Alternatively you can simply stay here and do this in Terminal.app:

```
cd ~/Library/Application Support/TextMate/Managed/Bundles
git clone git://github.com/bomberstudios/Save-On-Focus-Lost.tmbundle

```
Then just relaunch TextMate 2

**Setting up _Skim_ as the previewer:** If you want to use skim instead of the default previewer, just pop upon the LaTeX module preferences in TextMate and change it. Look for a gear on the bottom of the window and then find "LaTeX", and the preferences will be at the bottom of that menu. Inside, you can switch it to using Skim.

**When you open up a .tex file:** You need to make the LaTeX module "watch document", which will make it automatically refresh the preview when the file is saved. This is simply done by pressing "Ctrl+Command+W" to toggle the preview-on-save functionality.

The idea is simply to write the LaTeX you want to write, then click on the preview window to the right to make it automatically generate a new preview. Alternatively you can always press "Command-R".

#### What next?
Now the actual struggle will begin: transfering notes. Though I'm mainly seeing upsides now: my first-year notes will get a nice reorganization and a reread. If there's one thing I'm experienced with, it's fiddling with my toolbox and moving my stuff around.

Another posssible idea is to create an applescript or textmate bundle that automatically saves in periodical intervals, but it's not really necessary right now. Finding a way to make the LaTeX module automatically "watch document" upon startup would probably be useful though.