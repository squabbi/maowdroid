---
title: 'Update a Rooted Pixel 3 & Pixel 3 XL to Android 10 November Security Update'
tags: [pixel 3,pixel 3 xl,update,rooted,android 10,november]
categories: [update]
published: true
date: 10-11-2019
---

This month's update included a few fixes for us Pixel users, including being able to use bluetooth Xbox Controllers now. We also have a few fixes for the Pixel 3s as listed below.

<!--more-->

# Video

<div>{%- include extensions/youtube.html id='CwcOi6rEDLY' -%}</div>

# Functional Patches

| Category        | Improvements                                      | Devices        |
| --------------- | ------------------------------------------------- | -------------- |
| Assistant       | Improved hotword detection for Google Assistant   | Pixel 3 & 3 XL |
| Audio           | Bottom speaker quality improvements               | Pixel 3        |
| Stability       | Additional fixes for devices stuck during boot    | Pixel 3 & 3 XL |
| Keyboards/Input | Add support for Xbox Bluetooth controller mapping | Pixel 3 & 3 XL |

# Updating

We'll be using `fastboot` and the factory images to update our phone, and using Magisk Manager to pre-patch the November Factory Image's `boot.img`.

## Factory Images
They can be downloaded from these links:

[Crosshatch - Pixel 3 XL Factory Images](https://developers.google.com/android/images#crosshatch)

[Blueline - Pixel 3 Factory Images](https://developers.google.com/android/images#blueline)

## TWRP
As of 10 November 2019, TWRP is still largely incompatible with Android 10 on the Pixel 3 and 3 XL. We won't be using TWRP until it has been updated, which will take a while as the TWRP lead developer has mentioned, due to a number of large changes to source files.

We'll continue to use Magisk Manager to patch the stock `boot.img` and flash that after updating via the factory images to maintain root.

## Magisk

Download the latest version of Magisk Manager here, but since you're rooted already you should already have that.

Ensure that you remove modules that may prevent you from booting up, such as ones that replace system applications or modify/hook onto the system in some way (i.e. EdXposed).
{:.warning}

[Download Magisk Manager here.](https://forum.xda-developers.com/apps/magisk/official-magisk-v7-universal-systemless-t3473445)