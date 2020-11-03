---
title: Setting up a minimal DEBIAN VM using QEMU
author: bt7274
date: 2020-11-03 01:20:00 +0530
categories: [Blogging, Tutorial, Systems]
tags: [qemu,debian,virtual machine]
toc: false
---

## Backstory
While there can be many reasons as to why you would need a virtual machine, maintaing clean environment and dependency is one of them. I have triple boot laptop, with windows, ubuntu and arch. I do ctf mostly while using arch. Some might say this is an overkill, I wanted to experiment with arch as I had heard a lot about it and I have been using a dual boot system with ubuntu and windows for quiet a while, and I had gotten bored of ubuntu. A few months back, I also tried fedora. It's a great alternative to ubuntu too but I was having some driver issues and I had to revert back to ubuntu. Then a few days after that, I tried the plasma and cinnamon desktop with ubuntu, while those were great, my disks filled up. And now I am using ubuntu with the default gnome and arch with kde plasma. I decided to share writeups for the ctf challenges I do, to share my knowledge and experience as well as a reference for myself in future. I had some trouble setting up the environment for jekyll on arch, so I decided to spin a minimal debian vm for it using qemu. While I could have also used docker or vagrant, I still went with qemu based vm.
## Install QEMU and download ISO for debian net installer
This tutorial assumes you have [qemu](https://www.qemu.org/download/) already installed and you are comfortable with the shell. Qemu is a generic and open source machine emulator and virtualiser. Also, I used a [debian net installer](https://www.debian.org/CD/netinst/) for this. After you have qemu installed and then net installer downloaded, we are ready to create our VM.
## Create a virtual harddisk
``` bash
qemu-img create -f qcow2 debian.qcow 10G
```
This command will create a virtual harddisk named debian.qcow with a size of 10GB in the current folder. The 10GB size is dynamically allocated.<br>
Now we are ready to spin up our vm. Make sure the net installer iso is in the current directory or change the path to point to it.
## Spin up the VM and install Debian
``` bash
qemu-system-x86_64 -hda debian.qcow -cdrom debian-10.6.0-amd64-netinst.iso -boot d -m 4000 -smp 4
```
This command will start the virtual machine with our created debian.qcow as the harddisk, the net installer iso as the cdrom and boot from it. Also, the machine will use 2 smp cores or threads and 4000 mega bytes of memory. After you run this command, a qemu window will open, with the boot options.
