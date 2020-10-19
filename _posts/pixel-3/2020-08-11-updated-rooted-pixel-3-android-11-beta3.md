---
layout: article
title: 'Update a Rooted Pixel 3 & 3 XL to Android 11 (R) Beta 3 using OTA'
tags: [pixel 3,pixel 3 xl,update,rooted,android 11,ota]
categories: [pixel-3]
published: true
date: 11-08-2020
aside:
  toc: true
show_edit_on_github: false
---

August brings us the 3rd beta of Android 11, set to release some time Q3. Since Google has blessed me with an OTA update on my device, I decide to take the OTA update instead! Please note that there are some conditions for using the System Updater (OTA) method.

<!--more-->

If you are updating from Android 10, you must change the update channel of Magisk inside Magisk Manager's settings to **canary**! Stable and beta releases (as of v20.4) are **NOT** compatible with Android 11.
{:.warning}

# Video

<div>{%- include extensions/youtube.html id='PnPq3N5OVTU' -%}</div>

# Conditions

Here is where it gets a little tricky. As mentioned, when you take OTA updates, the sytem verifies the integrity of certain partitions, mostly ones that it perceives as read-only. It includes, but is not limited to `/system` and `/vendor`. It also requires the stock `/boot` image too.

This first condition isn't as relevant nowadays since Android 10 does not allow the RW access to the `/system` partition.

When you uninstall Magisk and choose to 'Restore Images', if it says restoration failed, or for whatever reason Magisk Manager cannot restore the stock images, you may not be able to take the update.
{:.error}

If the System Updater fails and you get a general error: *Installation Failed*; you must update using the full OTA or the factory images.

# Links

[Magisk Documentation (OTA Upgrades)](https://topjohnwu.github.io/Magisk/ota.html)