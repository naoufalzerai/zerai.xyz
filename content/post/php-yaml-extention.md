+++
title = "Install yaml extention in PHP"
date = 2024-10-01T19:18:00-05:00
lastmod = 2024-10-01T19:18:00-05:00
tags = ["php","yaml"]
categories = ["Php"]
imgs = []
cover = ""  # image show on top
readingTime = true  # show reading time after article date
toc = true
comments = true
justify = false  # text-align: justify;
single = false  # display as a single page, hide navigation on bottom, like as about page.
license = ""  # CC License
draft = false
+++


A server configuration is a set of instructions that tells a computer how to operate. The instructions can include the type of hardware to use, the software to install, and the settings to use. A server configuration can be used to set up a new computer, or to change the settings on an existing computer.
Here is the configuration I usually use for my fresh new sever:

<!--more-->
#  Step 1

    $brew uninstall libyaml
    Uninstalling /opt/homebrew/Cellar/libyaml/0.2.5... (10 files, 369.7KB)

#  Step 2

    $brew install libyaml 
    ==> Downloading https://github.com/yaml/libyaml/archive/0.2.5.tar.gz
    Already downloaded: /Users/**/Library/Caches/Homebrew/downloads/688fdcea5b88140cb83d1f72e3a77fa76b6560f0d66eabcea7d54cf9f06d5e72--libyaml-0.2.5.tar.gz
    ==> ./bootstrap
    ==> ./configure --prefix=/opt/homebrew/Cellar/libyaml/0.2.5
    ==> make install
    🍺  /opt/homebrew/Cellar/libyaml/0.2.5: 10 files, 369.7KB, built in 12 seconds

#  Step3 copy the prefix in step2.

    #In this case,It's
    /opt/homebrew/Cellar/libyaml/0.2.5

#  Step 4

    $sudo pecl install yaml
    Password:
    downloading yaml-2.2.1.tgz ...
    Starting to download yaml-2.2.1.tgz (40,977 bytes)
    ............done: 40,977 bytes
    8 source files, building
    running: phpize
    Configuring for:
    PHP Api Version:         20160303
    Zend Module Api No:      20160303
    Zend Extension Api No:   320160303
    Please provide the prefix of libyaml installation [autodetect] : 

#  Step 5
    
    Please provide the prefix of libyaml installation [autodetect] : /opt/homebrew/Cellar/libyaml/0.2.5

#  Step 6

    pecl install yaml





