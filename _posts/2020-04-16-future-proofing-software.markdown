---
layout: post
title:  "Future Proofing Software"
date:   2020-04-16 20:27:20 -0700
categories: jekyll update
---

Unfourtunantly, no one can predict the future.  However, there are certain measures an experienced software craftsman can take in order to make software easier to flex to match changing requirements and new features.  These patterns I've picked up on during my millions of hours looking over code and now stick out to me like a sore thumb.  Once you adjust your code radar to detect these anti-patterns, you'll see just how big of a differnce it makes fixing them *before* they become a problem.  Initially they might not seem like a horrible idea, but viewed through the lense of 10, 20 years of addition, it becomes a maintenance nightmare.

Lists
=====

**If you define a list somewhere in your codebase, it will grow**

Lists are a one of the necessary evils of the software development world.  No, I'm not necessarily talking about the `list` data structure common across basically every programming language.  The lists I'm talking about are hardcoded, static values pertinent directly to the domain you work in. They might look something like this:

{% highlight python %}
osVersions = {
               "iPhone": "iPhone OS 1.0",
               "iPhone 3G": "iPhone OS 2.0",
               "iPhone 3GS": "iPhone OS 3.0",
               "iPhone 4": "iOS 4.0",
               "iPhone 4s": "iOS 5.0",
               "iPhone 5":  "iOS 6.0",
             }
{% endhighlight %}

Obviously, Apple's going to continue making new iPhones and thus, this list will constantly grow.  Sure, adding a new entry when `iPhone 5c` comes out isn't a monumental effort, but becomes a problem when you have numerous of these lists scattered throughout the codebase.  The developer responsible for `iPhone 5c` must locate, understand, change, and test each list that requires adding the new phone version.  This is guaranteed work for every new phone version.  Furthermore, if the developer misses one of these lists, it might not be immediately obvious what's wrong leading to more wasted time debugging non-issues.


Versioning
==========

Default Branch Cases
====================

