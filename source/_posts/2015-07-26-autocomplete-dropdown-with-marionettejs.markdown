---
layout: post
title: "Autocomplete dropdown with MarionetteJS"
date: 2015-06-24 21:27:37 +0800
comments: true
categories: [tutorial,marionette,autocomplete]
---

In this article, I will create [typeahead](https://twitter.github.io/typeahead.js/) style dropdown using MarionetteJS.

<!-- More -->

**Note**: Marionette is a Backbone.js library which includes a number of useful extended views. For more information on Marionette, I recommend starting with Ben McCormick's excellent introduction [here](http://benmccormick.org/2014/12/02/the-case-for-marionette-js/).

## Why use Marionette?

There are several existing solutions for the autocomplete functionionality, such as [jQuery UI autocomplete](https://jqueryui.com/autocomplete/), and [typeahead](https://twitter.github.io/typeahead.js/). In particular, typeahead is both powerful and flexible. However, I have chosen Backbone.Marionette for the gentler learning curve.

Our autocomplete implemented with Marionette comes with the following features:

1. **Datasource changes with user input.**

   CollectionView can use any collection as the data source, and automatically listens to `add` and `destroy` events.

2. **Complex UI interaction within the dropdown menu.**

   Use event hashes like you would in any other Backbone.Views.

## Working Example

<img src="/images/201506autocomplete.png" width="600">

Play around with it [here](http://plnkr.co/9SX5OphViYSE1txQbEFR).

## Walkthrough

Let's divide our autocomplete into two sections:

* The input, which is controlled by a Backbone View.
* The dropdown menu, which is controlled by a CollectionView.

When a keyword is typed into the input, the dropdown menu is filtered. The key part of our implementation is this [filter method](http://marionettejs.com/docs/marionette.collectionview.html#collectionviews-filter).

### Filter Behavior

I have separated the filter logic into a Marionette.Behavior, as shown below: 

<script src="https://gist.github.com/gracesusanchen/f6640993d2cc171f7230.js?file=FilterBehavior.js"></script>

Notice we have instantiated the `onFilter` method. This method is triggered by the view's `filter` event.

Upon filtering, we reset the view's filter function based on the current search keyword. The filter function matches the keyword against fields specified by the `filter_keys` options. If at least one match is found, the item is shown.

### Views

The rest of the code is quite straightforward. We define our CollectionView and make it filterable with default `filter_keys`, like so:

<script src="https://gist.github.com/gracesusanchen/f6640993d2cc171f7230.js?file=ResultView.js"></script>

The ItemView here is very simple (*line 3~7* above). In a real life project, we can use its own event hash to bind user interactions.

For our example, we are only interested in keyword changes. This event is handled by the main view, which is defined in the code below.

<script src="https://gist.github.com/gracesusanchen/f6640993d2cc171f7230.js?file=MainView.js"></script>

The main view listens `keyup` events on the search bar, and updates the dropdown menu by triggering `filter` events on the collection view.

## Wrapping Up

For clarity, I have removed the code for highlighting in the above explanation, despite it a common feature in autocomplete. If you are interested in my implementation of highlighting, feel free to visit [the working example](http://plnkr.co/9SX5OphViYSE1txQbEFR).