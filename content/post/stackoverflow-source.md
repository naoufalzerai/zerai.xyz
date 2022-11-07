+++
title = "Stackoverflow Source"
date = 2022-11-06T18:39:54-05:00
lastmod = 2022-11-06T18:39:54-05:00
tags = ["Markdown"]
categories = ["Markdown"]
imgs = []
cover = ""  # image show on top
readingTime = true  # show reading time after article date
toc = true
comments = false
justify = false  # text-align: justify;
single = false  # display as a single page, hide navigation on bottom, like as about page.
license = ""  # CC License
draft = false
+++
##### 1. If you have a particular StackOverflow question such as:
<!--more-->
+ https://stackoverflow.com/questions/69419055/find-the-pseudo-version-of-the-current-main-module

##### 2. When you click on the little recylcing symbol next to a question or answer "Show activity on this post", you will get to the timeline:

https://stackoverflow.com/posts/69419917/timeline#history_9281a690-64c3-4302-bb36-1ebb6dfd3ecf

##### 3. Take the post ID that is exposed in the timeline url as above 
Go to Question revision history:

https://sitename.stackexchange.com/posts/{post-id}/revisions

+ shown as the “history” link for questions and answers with at least two revisions
+ contains links to individual revisions and their source code, as well as summaries of a number of other events such as closing, reopening, (un)deleting, bounty start/end, (un)locking, tweeting, marked (not) community wiki, and merging.

##### 4. So then you will have a URL like this:
https://stackoverflow.com/posts/69419917/revisions

##### 5. And then the source code looks like this:
https://stackoverflow.com/revisions/9281a690-64c3-4302-bb36-1ebb6dfd3ecf/view-source



Source : https://gist.github.com/StevenACoffman/14487c47b7b15c8889ae1c8f12a25d43