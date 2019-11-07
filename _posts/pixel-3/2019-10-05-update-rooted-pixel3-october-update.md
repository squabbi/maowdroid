---
layout: article
title: 'Update Rooted Pixel 3 & 3 XL to Android 10 October Security Update'
tags: [pixel 3,pixel 3 xl,update,rooted,android 10,october]
categories: [update]
published: true
date: 05-10-2019
aside:
  toc: true
show_edit_on_github: false
---
October is here and that brings us another update for our Pixel devices. Since TWRP doesn't support Android 10 running on the newer Pixels (partition changes), we will need to stick with using Magisk Manager to patch a stock `boot.img` for us, so we can re-root after updating!

<!--more-->

# Video

<div>{%- include extensions/youtube.html id='4Nduxj7ry3o' -%}</div>

# Factory Images

[See all Google Nexus and Pixel Factory Images here.](https://developers.google.com/android/images)

# TWRP

TWRP (3.3.0-0) cannot mount the `/system` due to new partition changes brought along with Android 10. For now we will need to use Magisk Manager to patch October's stock `boot.img` from the Factory Image.
{:.warning}

We will need to wait for TeamWin to build newer versions of TWRP to support these new changes.

[TWRP for Blueline (Pixel 3)](https://twrp.me/google/googlepixel3.html)

[TWRP for Crosshatch (Pixel 3 XL)](https://twrp.me/google/googlepixel3xl.html)

# Magisk

We can use the latest stable version of Magisk (v20.0) which has been updated to support Android 10 on almost all devices. Luckily that includes the Pixel 3 and 3 XL.

[Download Magisk Here (XDA Thread)](https://forum.xda-developers.com/apps/magisk/official-magisk-v7-universal-systemless-t3473445)