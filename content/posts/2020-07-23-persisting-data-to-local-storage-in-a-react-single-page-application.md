---
layout: post
date: 2020-07-23 02:40:54
image: assets/1_w8qv5dbces5jizseo3ie5q.jpeg
title: Persisting Data to Local Storage in a React Single-Page Application
description: An Overview of Local Storage and Instructions for its
  Implementation in a React Application
tags:
  - react
---
<!--StartFragment-->

# Local Storage: the What, How, and Why

Local storage is a powerful method for persisting user data across browser sessions and a convenient alternative to using server-side storage that does not force a user to sign up or log in to your app.

## How Local Storage Works

Local storage is structured as a key/value pair with the key serving as a named identifier for the data stored as the value. The key is typically a string whereas the the value can be any JavaScript-supported data type, including objects, integers, and Booleans.

Local storage can be accessed at any time via the localStorage object and will not expire unless explicitly written to do so.

# Local Storage Implementation

To illustrate how to add local storage to an app, I’ll use my [*NYTimes* NewsWire](https://news-wire.herokuapp.com//) project, a Single-Page Application built with React. For the project’s full code base, please refer to its [GitHub repo](https://github.com/siobhanpmahoney/newswire-app).

## Brief Project Overview

Using the [Times Newswire API](https://developer.nytimes.com/timeswire_v3.json#/README) endpoint, my app renders the 20 most recent stories published by *The New York Times* and provides users with options to read and save articles in the feed. In addition to the wire feed, I used React state to store and display:

* user viewing history: `this.state.readNow`
* list of saved articles: `this.state.readLater`
* a list of paper sections under which the viewed and saved articles were published (used to build a supplemental recommended reading feed): `this.state.likedSections`

I was interested in using local storage to persist these three pieces of state between browser sessions.

## Instructions:

## 1. Install `local-storage`

Navigate into your project directory and install `local-storage` using `npm`or `yarn`

```

```

## 2. Import `local-storage` into your your react app:

Add the following to the top of the file in which you plan to use `local-storage`:

```

```

## 3. Load previous local storage state using ls.get()

After picking keys for the values you want to store in local storage, add `ls.get('key')` to your `componentDidMount()` function.

Here’s how this looked in my *NYTimes* NewsWire app:

```

```

***Note*:** Since I am saving arrays to local storage that need to be initialized as empty arrays and will populate or depopulate based on user actions, I included`|| []` for each piece of state retrieved using `ls.get()` so the app won’t cras for users who have not visited the page before.

## 4. Persist updates to state using ls.set()

Whenever calling `this.setState()`, add `ls.set('key', 'value')` to the function.

***Note*:** Since React’s `setState` method is async, it is wise to set your updated piece of state to a separate variable to ensure consistency across React state and localStorage state

<!--EndFragment-->