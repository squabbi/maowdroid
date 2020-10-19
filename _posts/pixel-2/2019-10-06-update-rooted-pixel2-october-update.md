---
layout: article
title: 'Update a Rooted Pixel 2 & 2 XL to Android 10 October Security Update'
tags: [pixel 2,pixel 2 xl,update,rooted,android 10,october]
categories: [update]
published: true
date: 06-10-2019
aside:
    toc: true
show_edit_on_github: false
---
The October security update for the Pixel 2 series is out! We'll be using the factory images, with the help of TWRP to update our rooted phone, as well as being able to keep root access after updating!

<!--more-->

# Video

<div>{%- include extensions/youtube.html id='aMPRRQu1hCk' -%}</div>

# Factory Images

[See all Google Nexus and Pixel Factory Images here.](https://developers.google.com/android/images)

# TWRP

TWRP (3.3.0-0) cannot mount the `/data` partition while it is encrypted. You can attempt to remove your screen lock before booting TWRP. But I would recommend sideloading Magisk in TWRP via ADB Sideload so you don't have to re-enroll your fingerprints and reconfigure your apps.

## Sideloading in TWRP

From TWRP's main menu, go to Advanced > ADB Sideload > Swipe to start Sideload.

Then use the ADB command:

```
adb sideload [insert path of zip you wish to sideload & flash]
```

[TWRP for Walleye (Pixel 2)](https://twrp.me/google/googlepixel2.html)

[TWRP for Taimen (Pixel 2 XL)](https://twrp.me/google/googlepixel2xl.html)

# Magisk

We can use the latest stable version of Magisk (v20.0) which has been updated to support Android 10 on almost all devices. Luckily that includes the Pixel 2 and 2 XL.

[Download Magisk Here (XDA Thread)](https://forum.xda-developers.com/apps/magisk/official-magisk-v7-universal-systemless-t3473445)