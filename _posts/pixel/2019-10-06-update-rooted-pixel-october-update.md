---
layout: article
title: 'Update a Rooted Pixel & Pixel XL to Android 10 October Security Update'
tags: [pixel,pixel xl,update,rooted,android 10,october]
categories: [update]
published: true
date: 06-10-2019
aside:
    toc: true
show_edit_on_github: false
---
October is here, and that comes with another update! We'll be using TWRP and the factory images to update our rooted Pixel to the October Security Update.

<!--more-->

# Video

*TBU (to-be-uploaded)*

# Factory Images

[See all Google Nexus and Pixel Factory Images here.](https://developers.google.com/android/images)

# TWRP

TWRP (3.3.1-0) **can** decrypt `/data` successfully on Android 10, but that is only offered as a bootable TWRP image. The latest installer .zip is still based on 3.3.0-0. This means the image you first boot will be able to decrypt the `/data` partition (so you can see the contents of your internal storage). But once you flash the TWRP installer and reboot back into the recovery, you'll be using TWRP 3.3.0-0.

TWRP 3.3.0-0 provides a way to install a recovery image to the ramdisk, so you can install the TWRP 3.3.1-0 image via TWRP.
{:.info}

Therefore in this case, you can flash TWRP Installer & Magisk *while* booted from the TWRP 3.3.1-0 image.
{:.success}

TWRP (3.3.0-0) cannot mount the `/data` partition while it is encrypted. You can attempt to remove your screen lock before booting TWRP. But I would recommend sideloading Magisk in TWRP via ADB Sideload so you don't have to re-enroll your fingerprints and reconfigure your apps.

## Sideloading in TWRP

From TWRP's main menu, go to Advanced > ADB Sideload > Swipe to start Sideload.

Then use the ADB command:

```
adb sideload [zip you wish to sideload & flash]
```   

[TWRP for Sailfish (Pixel)](https://twrp.me/google/googlepixel.html)

[TWRP for Marlin (Pixel XL)](https://twrp.me/google/googlepixelxl.html)

# Magisk

We can use the latest stable version of Magisk (v20.0) which has been updated to support Android 10 on almost all devices. Luckily that includes the Pixel and Pixel XL.

[Download Magisk Here (XDA Thread)](https://forum.xda-developers.com/apps/magisk/official-magisk-v7-universal-systemless-t3473445)