---
layout: post
title: "How to Collect Wallpapers like a Pro"
date: 2016-02-06 14:36:29 +0800
---

Once in a while, I find my current wallpaper collection lacking...

<!--more-->

... and I set out to find a new one.

<img src="/images/201512browsing.jpg">

Half an hour later, I've finally got a new wallpaper! But that is half an hour more than I meant to spend on this!

And I thought, *Wouldn't it be nice to have wallpapers pop up at my proverbial doorstep?*

With the help of [IFTTT](http://ifttt.com), [wallch](http://melloristudio.com/wallch/), and some bash scripting, I have managed to solve this problem on Ubuntu and Xubuntu.

## How it works

IFTTT automatically saves updates from my favourite wallpaper sources to my local wallpaper folder. When new images come up in the wallpaper slideshow, I can decide to keep or delete them as I please! 

## You will need...

- an [IFTTT](http://ifttt.com) account
- a [Dropbox](http://dropbox.com) account
- a list of subreddits (such as [/r/earthporn](https://www.reddit.com/r/EarthPorn/))

## Follow these steps

*Step 1*: Add a folder to your Dropbox for your wallpapers; make sure it is synced to your machine.

*Step 2*: Create your own IFTTT recipes, similar to the one below.

<img src="/images/201512ifttt.png">

*Step 3*: Set your wallpaper rotation folder to your Dropbox folder. ([Mac](http://www.switchingtomac.com/tutorials/how-to-rotate-wallpapers-in-osx/)|[Win](http://windows.microsoft.com/en-us/windows7/create-a-desktop-background-slide-show)|[Gnome](http://melloristudio.com/wallch/))

And that's it!

## Managing Wallpapers

Once I had this system up and running, I quickly amassed many, many wallpapers. They become slightly problematic to organize with only system tools. (Loading thousands of HD wallpaper thumbnails is slow, to say the least.)

For removal of duplicates and images that are too small, I use my [wallpaper-trimmer](https://github.com/gracesusanchen/wallpaper-trimmer) script.

## Access the Current Wallpaper

Sometimes, I want to find out where the current wallpaper is located, without having to turn on the desktop settings, because, again, loading thousands of wallpaper thumbnails is sloooow.

Here are a few ways to access the current desktop image path:

*On Ubuntu*: Install [wallch](http://melloristudio.com/wallch/)!

*On Xubuntu*: Use [this script](https://github.com/gracesusanchen/current-xfce-desktop/).