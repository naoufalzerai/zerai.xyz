+++
title = "Change Files Folder Default Path"
date = 2022-09-09T20:55:58-04:00
lastmod = 2022-09-09T20:55:58-04:00
tags = ["tip","folders"]
categories = ["Linux"]
imgs = []
cover = ""  # image show on top
readingTime = true  # show reading time after article date
toc = true
comments = false
justify = false  # text-align: justify;
single = false  # display as a single page, hide navigation on bottom, like as about page.
license = ""  # CC License
draft = true
+++

First edit <mark>~/.config/user-dirs.dirs</mark> so as to change the music folder to the path of the desired folder.

You can use the following command:

    vi ~/.config/user-dirs.dirs

For example, if your music resides in <mark>/home/user/Dropbox/music</mark> you will change the file to look like this:

    XDG_MUSIC_DIR=$HOME/Dropbox/music
Execute 

    xdg-user-dirs-update --force