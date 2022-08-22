+++
title = "AMD GPU Screen Tearing"
date = 2022-08-21T22:09:40-04:00
lastmod = 2022-08-21T22:09:40-04:00
tags = ["AMD","GPU","Fix"]
categories = ["Linux"]
imgs = []
cover = ""  # image show on top
readingTime = true  # show reading time after article date
toc = true
comments = false
justify = false  # text-align: justify;
single = false  # display as a single page, hide navigation on bottom, like as about page.
license = ""  # CC License
+++

According to Wikipedia : 
> Screen tearing is a visual artifact in video display where a display device shows information from multiple frames in a single screen draw.
If you are on Debian or Ubuntu, and you have an AMD GPU this might fix the problem 😊

<!--more-->
#### 1. Check if the is any config 
	ls -l /etc/X11/xorg.*

{{< highlight bash-session >}}
$ ls -l /etc/X11/xorg.*
total 4
-rw-r--r-- 1 root root 108 Jul 30 11:33 20-amdgpu.conf
{{< /highlight >}}

##### Backup if found 
	mkdir ~/xorg-backup
	sudo mv -v /etc/X11/xorg.conf ~/xorg-backup/
	sudo mv -v /etc/X11/xorg.conf.d ~/xorg-backup/

#### 2. Check if the is any config

    lspci -nnk | grep -i -EA3 "3d|display|vga"

{{< highlight bash-session >}}
$ lspci -nnk | grep -i -EA3 "3d|display|vga"
09:00.0 VGA compatible controller [0300]: Advanced Micro Devices, Inc. [AMD/ATI] Cezanne [1002:1638] (rev c9)
	Subsystem: Gigabyte Technology Co., Ltd Cezanne [1458:d000]
	Kernel driver in use: amdgpu
	Kernel modules: amdgpu
{{< /highlight >}}
    
##### If you have amdgpu then 

###### create the config file 

    sudo mkdir /etc/X11/xorg.conf.d
    sudo vi /etc/X11/xorg.conf.d/20-amdgpu.conf

###### Add the following to the config file 20-amdgpu.conf</kbd>
    
    Section "Device"
            Identifier "AMD"
            Driver  "amdgpu"
            Option "TearFree" "true"
    EndSection

##### If you have Radeon then 

###### create the config file 

    sudo vi /etc/X11/xorg.conf

###### And add the following

    Section "Device"
            Identifier "Radeon"
            Driver "radeon"
        Option "TearFree" "on"
    EndSection    

#### 3. Reboot <span class="emojify">💣</span>
You can test now with <kbd> [Screen tearing test](https://www.testufo.com/stutter) </kdb>