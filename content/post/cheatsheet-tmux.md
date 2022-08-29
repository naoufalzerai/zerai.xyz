+++
title = "Cheatsheet Tmux"
date = 2022-08-28T19:15:25-04:00
lastmod = 2022-08-28T19:15:25-04:00
tags = ["cheatsheet","tmux"]
categories = ["Linux"]
imgs = []
cover = "https://images.pexels.com/photos/5380664/pexels-photo-5380664.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1"  # image show on top
readingTime = true  # show reading time after article date
toc = true
comments = false
justify = false  # text-align: justify;
single = false  # display as a single page, hide navigation on bottom, like as about page.
license = ""  # CC License
draft = false
+++

Tmux is a terminal multiplexer. It lets you switch easily between several programs in one terminal, detach them (they keep running in the background) and reattach them to a different terminal.

<!--more-->

|||
|---|---|
| Create window | <kbd>Ctrl + b</kbd> <kbd>c</kbd> |
| Switch window by number| <kbd>Ctrl + b</kbd> <kbd>0</kbd>...<kbd>9</kbd> |
| Previous window | <kbd>Ctrl + b</kbd> <kbd>p</kbd> |
| Next window | <kbd>Ctrl + b</kbd> <kbd>n</kbd> |
| Split pane with vertical layout | <kbd>Ctrl + b</kbd> <kbd>"</kbd> |
| Split pane with horizontal layout | <kbd>Ctrl + b</kbd> <kbd>{</kbd> |
| Switch pane | <kbd>Ctrl + b</kbd> <kbd>⬆️</kbd><kbd>⬇️</kbd><kbd>➡️</kbd><kbd>⬅️</kbd> |


#### Acknowledgement : 
- https://github.com/tmux/tmux/wiki