---
layout: post
title:  "Future Proofing Software"
date:   2020-04-16 20:27:20 -0700
status: Need to edit
categories: jekyll update
---

# Status
This post is still a draft and will be updated in the future to

Unfourtunantly, no one can predict the future.  However, there are certain measures an experienced software craftsman can take in order to make software easier to flex to match changing requirements and new features.  These patterns I've picked up on during my millions of hours looking over code and now stick out to me like a sore thumb.  Once you adjust your code radar to detect these anti-patterns, you'll see just how big of a differnce it makes fixing them *before* they become a problem.  Initially they might not seem like a horrible idea, but viewed through the lense of 10, 20 years of addition, it becomes a maintenance nightmare.

Lists
=====

**If you define a list somewhere in your codebase, it will grow**

Lists are a one of the necessary evils of the software development world.  No, I'm not necessarily talking about the `list` data structure common across basically every programming language.  The lists I'm talking about are hardcoded, static values pertinent directly to the domain you work in. They might look something like this:

```python
osVersions = {
               "iPhone": "iPhone OS 1.0",
               "iPhone 3G": "iPhone OS 2.0",
               "iPhone 3GS": "iPhone OS 3.0",
               "iPhone 4": "iOS 4.0",
               "iPhone 4s": "iOS 5.0",
               "iPhone 5":  "iOS 6.0",
             }
```

Obviously, Apple's going to continue making new iPhones and thus, this list will constantly grow.  Sure, adding a new entry when `iPhone 5c` comes out isn't a monumental effort, but becomes a problem when you have numerous of these lists scattered throughout the codebase.  The developer responsible for `iPhone 5c` must locate, understand, change, and test each list that requires adding the new phone version.  This is guaranteed work for every new phone version.  Furthermore, if the developer misses one of these lists, it might not be immediately obvious what's wrong leading to more wasted time debugging non-issues.


Versioning
==========

**The only time you need to worry about versioning is after it becomes a problem**

A version declares when software is released.  It gaurantees different pieces will work together and is the foundation to making modular software.  In order to break apart your application into tiny, digestible pieces, you first need to be able to gaurantee those pieces will work together once reassembled into a larger machine.  Thus, versioning is a powerful tool, but it can also be a dangerous one at that.  When done wrong, versions can lead to difficult to maintain software.  Let me explain. 

**A version should not be used as a fork in your codepath.**

Let's say you're working for a company and they need a database to maintain information about horse races. You might start by defining the necessary database schema with various tables, rows, and columns to hold horse race results. Then, you build a GUI so the company can input the results of new horse races as well as perform queries over the dataset to find horse races of interest. 15 years go by and everything is going swimmingly.  Then, the company hires a new CTO who wants to revamp their internal tools.  As part of this effort, your database application is commissioned to recieve a new GUI.  There is some push-back within the company because everyone is familiar with the old GUI and sees no need to upgrade, since there's no tangible benefits (other than *what they claim* is a more friendly user interface).  The company decides to allow employees to use either the old or the new GUIs for awhile until everyone is familiar with the new interface and switches over.  This works for some time because the employees who want to keep their old familiar GUI around, can do so, but otherwise new people join and prefer using the new GUI (mainly since the company set the new GUI as the default for new employees to "encourage" the switch (they paid for it already, people should be using it right?!)).  Then times goes on, and the company grows, and with it the horse race statistics being collected.  Now, the company not only wants to store the horse race results but also information about the horse's training regime.  New database schema is added to support the collection and storage of horse training regimes.  The company decides to add a new page to the GUI so employees can access this information but since it's an internal tool and the company's been on sowewhat of a time crunch of late, it's decided to only support this functionality in the new GUI.  The old GUI still functions because it operates blissfully unaware of the new training regime tables.  Then, tragedy strikes, there's a bug in the new GUI!  For some unexplained reason, the new GUI doesn't work with horses older than 20 (this is because of a minor oversight by the contractors; at the time the tool was written, there weren't any horses older than 20 in the proffesional circuit, but that all changed after "Bee Gee"'s birthday).  You can't fix the bug because the contractors have since "pivoted" and don't associate themselves with gambling outfits anymore. Fourtunantly, the old GUI doesn't have this problem, crisis adverted; employees can revert back to the old GUI to query horses older than 20, good thing we didn't throw that old code away! You're in a fucking mess now so just leave the company.

Default Branch Cases
====================

**Leftover turd sandwich is still turd sandwich**

I listened to someone complaining about this once, and he was pretty annoyed, so it seems like something
worth mentioning.  A default case in an execution branch can be powerful, but is also very very
dangerous.  The power of the default branch is that it catches EVERYTHING.  EVERYTHING.  So who
knows what that sucker will catch.  Are you absolutely sure that everything now and one-million-
years-in-the-future-until-the-end-of-time-or-forever-hold-your-peace-amen should follow that branch?
If so, then default branch cases are for you.  Otherwise, it might be a better idea to be explicit.
Let me throw another example at ya:

```python
def amIDan():
   return name == "Dan"
```


Then, someone named Daniel who goes by Dan comes along...

```python
def amIDan():
   return name in ( "Dan", "Daniel" )
```

Then, somene named Danny who goes by Dan comes along...

```python
def amIDan():
   return name.startswith( "Dan" )
```

Uh-oh, Danielle's around the world are complaining about receiving emails to join the Dan-Fan club

```python
def amIDan():
   if name.startswith( "Danielle" ):
      print "
      return False
   else:
      return name.startswith( "Dan" )
   return name.startswith( "Dan" )
```
 
Plugins
=======

Sorry this content doesn't exist yet! Maybe one day rmayf will get around to expanding upon it.

<!--stackedit_data:
eyJoaXN0b3J5IjpbNDQ1NzYyNjEsODM3NDYxMzY0LDMyOTk4Mj
Y1NF19
-->