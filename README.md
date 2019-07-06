## My Stack Problems

Welcome to Geecko Tech Blog. 

### How to contribute article

If you wan't to contribute to the wiriting, simply fork this repo, write your article in form of MD(markdown) file and put under `_post` directory following the existing format. Then ask a pull request. That's it.

### Preview the blog locally

1. Install Ruby and Gem
You need to have jekyll installed in your machine. Jekyll rely on `ruby` and `gem` in your computer. If you are using mac, usually it's already in your computer. If your're on windows, you can follow instruction from: [Ruby Installer](https://rubyinstaller.org/). If you're on linux, I will not insult your intelligence by assuming you don't know how to install ruby.

2. Install Jekyll
Just follow [this](https://jekyllrb.com/docs/installation/macos/) instruction. Better install locally instead of globally in your machine.


3. Run Jekyll

`jekyll serve`

### Features

This particular jekyll theme that we used have a following feature.

* Sitemap and XML Feed
* Pagination in homepage
* Posts under category
* Realtime Search Posts _(title & description)_ by query.
* Related Posts
* Highlight pre
* Next & Previous Post
* Disqus comment
* Projects page & Detail Project page
* Share on social media
* Google analytics
* HTML Minify _(Compress HTML)_ using [Jekyll Compress HTML](https://github.com/penibelst/jekyll-compress-html)


### How to Use?

**a. Add new Category**

All categories saved inside path of `category/`, you can see the existed categories.

**b. Add new Posts**

* All posts bassed on markdown syntax _(please googling)_. allowed extensions is `*.markdown` or `*.md`.
* This files can found at the path of `_posts/`.
* and the name of files are following `<date:%Y-%m-%d>-<slug>.<extension>`, for example:

```
2013-09-23-welcome-to-jekyll.md

# or

2013-09-23-welcome-to-jekyll.markdown
```

Inside the file of it,

```
---
layout: post                          # (require) default post layout
title: "Your Title"                   # (require) a string title
date: 2016-04-20 19:51:02 +0700       # (require) a post date
categories: [python, django]          # (custom) some categories, but makesure these categories already exists inside path of `category/`
tags: [foo, bar]                      # (custom) tags only for meta `property="article:tag"`
image: Broadcast_Mail.png             # (custom) image only for meta `property="og:image"`, save your image inside path of `static/img/_posts`
---

# your content post with markdown syntax goes here...
```
