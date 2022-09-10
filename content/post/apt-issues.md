+++
title = "Apt Issues"
date = 2022-09-09T19:36:53-04:00
lastmod = 2022-09-09T19:36:53-04:00
tags = ["apt","DNS","error"]
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

If you get a <mark>"failed to fetch"</mark> error occurs when apt-get update is run, then try this:

<!--more-->

## Edit DNS

First try to ping any website
    
    ping zerai.xyz

If you can't resolve the DNS

{{< highlight bash-session >}}
ping: zerai.xyz: Temporary failure in name resolution
{{< /highlight >}}

Then first edit resolv.conf 
    
    sudo vi /etc/resolv.conf

Change your DNS to any DNS Server 

{{< highlight bash-session >}}
nameserver 100.64.0.7
{{< /highlight >}}

Next execute this commands : 

    sudo apt-get --download-only --reinstall install resolvconf
    sudo dpkg --purge --force-depends resolvconf
    sudo apt-get install resolvconf

Finaly if you still have DNS problems a reboot is recommended

## If you have an EOL version(Ubuntu)

Just run

    sudo sed -i -r 's/([a-z]{2}.)?archive.ubuntu.com/old-releases.ubuntu.com/g' /etc/apt/sources.list
and
    
    sudo sed -i -r 's/security.ubuntu.com/old-releases.ubuntu.com/g' /etc/apt/sources.list
