---
title: "Raspberry Pi 4 - Media Server - Featuring Plex"
date: 2019-11-16
---

## Introduction
I have successfully set up my new Raspberry Pi 4 Model B as a Plex Media Server, which I realised is something that would be required for my upcoming family holiday cruising the Whitsundays next month. Since there will effectively be no internet connection, this naturaly rules out streaming services such as Netflix, Stan and Spotify. I attempted to use my work laptop as the hardware platform to perform this media serving but unfortunately this did not end up being successful, presumably due to the fact that my work has locked down the laptop and prevented it from being able to perform this function. While writing this blog post I just realised I could have used my Ubuntu virtual machine as the host of my media server, which I might do as another exercise and report on this as a separate blog post.

Given that I cannot cart my desktop linux desktop pc up to the Whitsundays, I started researching options available, and as I have known about Raspberry Pis for some time, I thought it would be something that I should consider. As it turns out, the recently released RPi 4B was described as having enough horsepower to do the job as the new processor is capable of performing the heaving lifting that goes hand in hand with transcoding video files of varying formats.

With this in mind I set out in indentifying the hardware I would need and the following is what I settled on and placed an order with one of the two recommended [Australian distributors](https://core-electronics.com.au) of Raspberry Pi equipment.

1. Raspberry Pi Model 4 B with 4GB of memory
1. Case for RPi above, one with passive and active cooling capability as research indicated that the RPi can get very hot.
1. 1m long micro to standard HDMI cable
1. Raspberry Pi mouse and keyboard (cute red and white coloured peripherals)
1. 32GB SD card complete with NOOBS for Raspberry Pi
1. Official Raspberry Pi power suppy - USB-C 5.1V 15.3W
 
## Challenges
1. 32GB SD card would not load installer software (NOOBS) that is required to install RPi.
1. Not having a SD card reader for my laptop to troubleshoot why the SD card was not behaving as it should.
1. Formatting the new SD card that I ended up purchasing at the same time as obtaining a card reader adpater for the mirco SD card so it could be read by my laptop card reader.
 1. Reason for formatting difficulty was because SD cards greater than 32GB (I got 64GB) require special treatment regarding formatting.
1. RPi NOOBs software still not working after following all procedures as documented at [Raspberry Pi's Official](https://projects.raspberrypi.org/en/projects/raspberry-pi-setting-up/3) web site. Error seen during boot sequence was similar to the following:
````bash
sh: can't access tty; job control turned off
````
 1. The solution to this problem required adding an instruction to the end of a line in one of boot files in NOOB software. Please see [this.](https://www.youtube.com/watch?v=WqNRqa333NI)
1. Chaging the location of where Plex stores all of your media's metadata. By default is stores it on the same SD card where your RPi's operating system has been installed (Raspian, a light weight variation of Debian, which in turn is one of the many distributions of Linux). If you go with the recommended 16GB SD card, this could be a real problem even for a modest media library, whereby the metadata ended up using approximately 12GB of the SD card. Fortunately I watched this as the Plex Media Server updated the library folders that I had configured. Since I did not know how much space was going to be used, I decided to research a way to move the default location for the metadata. 
 1. The solution involved having to create an override for the plexmedia service. Please see [this.](https://forums.plex.tv/t/moving-pms-library/197342) For RPi4B, be sure to follow the 'systemd' section. Also, the warning about not moving your metadata to the /media mount point is important.
 1. In my case, I wanted to move the metadata off the RPi and onto the same external hard disk that contained my media. Initially I mounted this hard disk at /media/usb_hdd1, and moving the metadata in accordance with the method in the point above, required me to change the mount point to /disks/usb_hdd1 as part of this exercise. Once I did this, I also had to delete my two plex media libraries and create new ones that pointed at the new locations. Doing all of this removed allowed me to remove all of the metadata of the RPi's SD card and left me with a very respectable amount of unused space.
1. Loading the script that the Argon ONE RPi case requires to control the fan speed and power button. Not a big deal or that difficult, but something that had to be done and I am glad I did as the RPi can get hot and the aluminium case was getting warm to touch, but with the fan kicking in in accordance with the temperatures that I specified, I was satisfied as I never observed the temperature increasing above 55 deg C.
 1. There is a command that you can run from terminal that returns the CPU temperature. It is:
````bash
/opt/vc/bin/vcgencmd measure_temp
````
1. Setting up VNC server (comes pre-installed on RPi) on the RPi and VNC viewer on my laptop so that I can have the RPi powered up and headless but still can access it.
1. Confirming that I can cast to Chromecast from any Plex client. The results of this are as follows:
 1. Without an internet connection, at best all you can do is mirror your screen using the browser's casting capability. This wasn't perfect, but is better than nothing.
 1. With an internet connection, you can cast from a mobile app installed on your platform of choice (iOS or Android), using the cast icon that is native to the app. If you want to use the browser web client's native cast icon, then you need to be connected to and signed into Plex's website. If you have established a web client connection via the local host (127.0.0.1:32400/web) or media server's IP address (eg. 192.168.1.20:32400/web), then the cast icon will not allow you to cast to a chromecast. I guess there is no surprises it has always been my experience that Chromecast needs an internet connection to work even in you are attempting to stream content from within your local network with what would appear logically to not need an internet connection.
1. Make sure it is possible to lock the RPi requiring a password to gain access. I needed this to prevent my son spending all day and night interacting with the RPi and the media that it so nicely presents and makes available. The surprising this is that even though the content is quite old on my hard disk, it is presented with all the latest posters and media art, it makes the content a lot more appealing to watch than my earlier attempts of using serviio on my linux desktop where the presentation was not quite as impressive as Plex.
 1. I followed an online instruction to add this screen lock function to the RPi menu and this did not work. The command worked, but not when using it in the context of the configuration file that was suggested to modify. In the end, I created my own bash shell script with this command in it, and added a menu item myself to the menu that called this bash script and this worked a treat.
1. Making sure that on booting the RPi that you are also asked for a user name and password. This was achieved with the help of the raspi-config utility that allows you to customise various aspects of the RPi's behaviour, including the presentation of a login splash window when RPi boots up.

The verdict is in and I can confirm that the RPi 4B can in fact do the job of serving media to multiple users running Plex Media Server and having multiple local and remote client applications running simultaneously. And when combined with Plex Media Server, it really is awesome. I am very happy with this end result. And my family can look forward to many days and nights of music and video entertainment as we cruise around the Whitsundays.

In my next blog post I will explain why I have been a little less active on my road to becoming a full stack developer. Basically it involves preparations for the sailing trip next month which has taken up all of my spare time (well almost, I did manage to listen to some coding podcasts driving to and from work). Stay tuned. 
