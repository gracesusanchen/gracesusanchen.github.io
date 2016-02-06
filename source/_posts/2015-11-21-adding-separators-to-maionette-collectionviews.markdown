---
layout: post
title: "Adding separators to a Collection using Marionette"
tags: ["marionette","separators","collection"]
date: 2015-11-21T11:21:05+08:00
---

[Separators, or dividers,](https://www.google.com/design/spec/components/dividers.html#dividers-specs) can make content more accessible by spacing it out. 

<!-- More -->

While Backbone.Marionette is ideal for rendering a collection of identical views, it is not as easy to insert separators between these. This post will describe how to add separators between ItemViews.

## The Goal

We want a collection which can be sorted by different attributes, and which uses corresponding separators depending on the current sort order. 

As new items are inserted into the collection, the separator position will remain accurate.

View the demo [here](http://plnkr.co/t1TVR2D93mZDKMo9buXT).

## Background: the CollectionView Lifecycle

The Marionette library defines the [lifecycle and triggers](http://benmccormick.org/2015/01/05/marionette-view-life-cycles/) for each view types. Below is a simplified diagram of the lifecycle of a CollectionView.

<img src="/images/201511Lifecycle.png">

The CollectionView has a *buffering mechanism*; ChildViews HTML strings are buffered until all children are "rendered" as strings. 

When the entire CollectionView HTML string is ready, the buffer is attached to the DOM in one go. This makes collection rendering much more efficient.

## Walkthrough

We will do separator-related operations in the following three stages of the view's lifecycle.

* `onAddChild`: This method is triggered when a new ItemView is rendered and added to the buffer. 

<script src="https://gist.github.com/gracesusanchen/d755b1c01b60543db8cf.js?file=collectionView.onAddChild.js"></script>

* `onRender`: This method is triggered after the CollectionView is attached to the DOM. 

<script src="https://gist.github.com/gracesusanchen/d755b1c01b60543db8cf.js?file=collectionView.onRender.js"></script>

* `onBeforeRender`: This method is triggered before the CollectionView begins rendering. 

<script src="https://gist.github.com/gracesusanchen/d755b1c01b60543db8cf.js?file=collectionView.onBeforeRender.js"></script>

## Caveats

To use the method described above, the CollectionView must be re-rendered on sort. Hence, the `reorderOnSort` option has be `false`, and this will have a slight impact on your rendering performance.

If your collection view will not be filtered or sorted, then it may be worth adding your separator logic to your models, and only update the models on `add` or `remove` events.