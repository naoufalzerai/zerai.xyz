+++
title = "Gnome Application Theme"
date = 2022-08-28T13:42:37-04:00
lastmod = 2022-08-28T13:42:37-04:00
tags = [
    "gtk",
    "cusomisation"
]
categories = ["Linux"]
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

GTK+ ≥ 3.12 allows you to theme specific applications, such as nevolution.
<!--more-->

You can use the <kbd>GTK_THEME=[theme-name]  [application]</kbd> command to run a specific application with a specific theme. For example, you can enter <kbd>GTK_THEME=Yaru-dark evolution</kbd> in the terminal to run the evolution of the Yaru dark theme.

If you want to keep this theme permanently in a program,

You should go to <kbd>/usr/share/applications</kbd> and find and copy the application's .desktop file, in this case mine was org.gnome.Evolution.desktop. Then paste it into <kbd>~/.local/share/applications</kbd> and open it with a text editor,

Then after <kbd>=</kbd> add env <kbd>GTK_THEME=<theme-name></kbd> look for each line starting with <kbd>Exec=</kbd> and put a space after it so the rest of the line comes before it, eg: <kbd>Exec=env GTK_THEME= Yaru-Dark Evolution -c stream</kbd>

All done 😄
