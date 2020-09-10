---
layout: post
title: The problems with my current comment system
description: A blog update meta-post kinda thingy...
modified: 2020-09-11
tags:
- commenting
- comments
- comment
- jekyll
- blog
- system
- disqus
- static
- website
- dynamic
image:
  background: prime-bg.jpg
  feature: CommentSysUpdate1/header.jpg
  credit: Volodymyr Hryshchenko
  creditlink: https://unsplash.com/@lunarts
date: 2020-03-22
---

Hey there! Welcome to yet another blog post. This one's a meta-discussion about the comment system on this blog.

You see, this is a static blog. This means there *technically* isn't any server-side thingy going on. So all that there is to it is some simple Javascript, HTML, and CSS (and of course Liquid and folks to do the hard part of generating stuff). This is beneficial and this also has some downsides to it. It's good because the site is delivered as-is. No server-side code is executed. This makes the whole process faster. At the same time, it produces difficulties in some usually wanted stuff. The one I am currently struggling with is comments.

All I could have done is just embed some code to show up some Disqus stuff and that's it. Voila! I have an awesome commenting system. The problem? Well, I imagine my commenting system to be something that feels like it belongs to this website. I don't want people to unnecessarily make accounts that they might not use at all. And on top of all that, I don't want my pages - especially blog posts - to become *slow-to-load*.

So Disqus wasn't an option. I had other options, yes. The other options sometimes were paid and not a lot different from Disqus itself. Then I find Staticman. Something that I could use to make the commenting system that would be just like I wanted it to be. And where do we end up? We end up with a fairly operative comment system - except some instances wherein Staticman refuses to take any more requests and stuff, and the user ends with a Hugo error kinda screen.

The comment system is pretty much what I had planned. However, what I want is a proper notification system. I want top-level comments to be reply-able. Of course a person needs to know that they've received a reply. Hence the redundant E-mail (optional) section in the current system. In the future, I want to make it such that a person chooses to get replies by typing in an email in that section. The candidates for this notification system? Mailchimp and boys. The problem? Well, those aren't problems to be real frank, but I need something without any sort of *plans* and something very customizable.

> **Future Sid:** I still continue my search. Okay, enough lying. I never searched for anything.
> Also, I have no idea what I meant here by customizable, so yeah.

On another similar note, I am also thinking of making/using some sort of notification system for the blog posts. Hmmm, I will think about it more. That's it for this blog post. I will see ya next time! (Okay I can't see you, but- oof okay byee!)
