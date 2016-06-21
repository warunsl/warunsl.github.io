---
layout: post
title: 'Ubuntu on MacBook Pro'
---

This post aims to collate all of the steps I gathered and followed from around the inter-web to install Ubuntu 11.10 on my MacBook Pro 8,1 and to get the wireless working.

__Installing Ubuntu via USB stick__
I followed the instructions detailed here - www.omgubuntu.co.uk/2011/10/dual-boot-os-ubuntu. However, I ran into issues getting rEFIt to work. The installation would be successful but on restart, I wasn't able to see the rEFIt menu. Googling around, I stumbled upon this command -

`/efi/refit/enable-always.sh`

which will force the rEFIt menu on restart. My experiences with this setup has been random. I sometimes can see the rEFIt menu on restart even when I did not run this command before shutting down the previous time. However, just to be safe, I think it is better to run this command before restarting. A smarter way to do this would be to add the command in the file

`/etc/rc.shutdown.local</pre>`

You may need to create the file if it is not present already. This script makes sure the commands in the file are executed by the time the machine is up after restart.

__Creating the USB stick__
I used the following command to create the bootable USB stick -

`sudo dd if=ubuntu-11.10-desktop-amd64+mac.iso of=/dev/sdXXX`

__Setting up the wireless__
Lot of googling finally <a href="https://bugs.launchpad.net/ubuntu/+source/b43-fwcutter/+bug/912941" target="_blank">pointed</a> me to these three simple commands that got the wireless to work


    sudo add-apt-repository ppa:mpodroid/mactel
    sudo apt-get update
    sudo apt-get install linux-backports-modules-cw-3.2-3.0.0-14-generic firmware-b43-installer
