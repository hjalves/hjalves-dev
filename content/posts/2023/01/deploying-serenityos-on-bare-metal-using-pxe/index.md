---
title: "Deploying SerenityOS on bare-metal using PXE"
date: 2023-01-20T12:00:00Z
draft: true
categories:
- serenityos
tags:
- serenityos
- bare-metal
- pxe
---

## Introduction

Earlier this week I finally managed to boot SerenityOS on my old (but gold) Dell 
Latitude laptop. I tried a couple of times before, without much success, but this 
time I was pretty determined to get past the frozen gray screen of death.

In some past attempts with other computers, I tried using [network boot and a 
RAM disk](https://github.com/SerenityOS/serenity/blob/master/Documentation/NetworkBoot.md)
without much success, but I think 
this method of booting the system is currently broken (I may be wrong though).

The SerenityOS documentation sparked my interest in the world of PXE booting, a method 
I had never tried before. The tedious process of flashing the hard drive 
and rebooting for every small change to the source code was unappealing to me,
so I began exploring the use of PXE to create an automated alternative.

My goal is to have a way to try SerenityOS on bare-metal that is as convenient as 
running it on a VM (albeit much slower to boot). What follows is my successful experiment 
in building that. 

This process is a work-in-progress and can be improved in many ways, I think.
Still, I hope you find it interesting and useful for your own needs. [^note]

[^note]: To be honest, it was not that hard  to find the changes 
required for the system to 
finally boot ([thanks to this Linus blog post](https://linus.dev/posts/running-serenityos-on-bare-metal/)),
so I actually spent way more time doing this task than if I had decided to flash the disk manually 😅

## Requirements

1. A server with *dnsmasq* or similar for DHCP+TFTP -- like Pi-Hole
2. A machine to build SerenityOS
3. A computer (x86-64) with PXE boot and a disposable hard drive, to install SerenityOS on
4. (Optional, but nice to have) Smart plug or wake-on-lan
5. Everything properly connected in a network `:^)`


## Configuring *dnsmasq*

You could install and configure *dnsmasq* [following the instructions in the documentation](https://github.com/SerenityOS/serenity/blob/master/Documentation/NetworkBoot.md#grub2).

However, if you already have an existing configuration of *dnsmasq* (or *Pi-Hole*, which uses a fork of *dnsmasq*), you can simply 
add the DHCP-boot and TFTP relevant instructions in a new file in `/etc/dnsmasq.d/`, for example:

    /etc/dnsmasq.d/09-dhcp-boot.conf

```cfg
log-dhcp
enable-tftp
tftp-root=/srv/tftp
dhcp-boot=boot/grub/i386-pc/core.0
```

Make the directory `/srv/tftp` or change `tftp-root`. Also don't forget to reboot the DHCP server.


## Installing **grub** for network boot

This is where my instructions diverge from the official documentation.

```bash
grub2-mknetdir --net-directory /srv/tftp/
```

Edit config:

```grub
insmod all_video
insmod biosdisk

set timeout=5
set default=4

menuentry "Boot from hard drive" {
    set root=(hd0)
    chainloader +1
}
```


## Building the image

Following the SerenityOS documentation, build the system as usual, optionally add
some ports, and then run:

```bash
ninja -C Build/x86_64 grub-image
```
...to make the full disk image with grub bootloader and configuration.

