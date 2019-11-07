---
layout: article
title: 'Update a Rooted Pixel 3 & 3 XL to Android Q Beta 1'
tags: [pixel 3,pixel 3 xl,update,rooted,android q]
categories: [update]
published: true
date: 20-03-2019
aside:
  toc: true
show_edit_on_github: false
---

# Video

<div>{%- include extensions/youtube.html id='a4F1fM1Wv9A' -%}</div>

# Root

The latest builds of Magisk Canary will be able to root your Pixel 3 or 3 XL. You will need to download the Canary Build of Magisk Manager, then supply the stock boot image for Magisk Manager to patch.

[Magisk Canary - Download Magisk Manager Canary from here.][1]

## Magisk
Magisk Canary has not been updated to support the Pixel 3 or 3 XL just yet, on Android Q. Watch topjohnwu's Twitter for any further updates.

Magisk Canary builds are however, compatible with the Pixel and Pixel 2, and their associated XL variants.

 - [topjohnwu's Twitter](https://twitter.com/topjohnwu/)
 - [Magisk Canary][1]

Remove **all** Magisk Modules before updating when Magisk does support Android Q on the Pixel 3 & 3 XL. You should be able to use most substitution modules (i.e. font and emoji changers), but with all other modules, you should exercise caution.

## TWRP
TWRP can currently decrypt the data partition in the first beta of Android Q. However, this may not be the case in subsequent builds of Android Q. You can test decryption by booting the TWRP image and seeing if you're able to decrypt the /data partition when prompted.

You can try to work around this by removing your screen lock, by setting it to 'Swipe'.

[1]:https://forum.xda-developers.com/apps/magisk/dev-magisk-canary-channel-bleeding-edge-t3839337