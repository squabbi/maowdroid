---
title: 'Update a Rooted Pixel 2 & Pixel 2 XL to Android 10 November Security Update'
tags: [pixel 2,pixel 2 xl,update,rooted,android 10,november]
categories: [update]
published: true
date: 10-11-2019
---

This month's update included a few fixes for us Pixel users, including being able to use bluetooth Xbox Controllers now. We also have a few fixes for the Pixel 2s as listed below.

<!--more-->

# Video

<div>{%- include extensions/youtube.html id='5IS2SNKgxIU' -%}</div>

# Functional Patches

| Category        | Improvements                                      | Devices        |
| --------------- | ------------------------------------------------- | -------------- |
| Assistant       | Improved hotword detection for Google Assistant   | Pixel 2 & 2 XL |
| Keyboards/Input | Add support for Xbox Bluetooth controller mapping | Pixel 2 & 2 XL |

# Updating

We'll be using `fastboot` and the factory images to update our phone, and using TWRP to sideload Magisk & optionally, the TWRP installer.

## Factory Images
They can be downloaded from these links:

[Taimen - Pixel 2 XL Factory Images](https://developers.google.com/android/images#taimen)

[Walleye - Pixel 2 Factory Images](https://developers.google.com/android/images#walleye)

## TWRP
As of 10 November 2019, TWRP is still not exactly compatible with Android 10, but luckily the underlying changes of Andorid 10 on the Pixel 2s still let us use TWRP to sideload our packages to flash as TWRP 3.3.0-0 cannot decrypt `/data`.

We'll continue to use ADB to sideload the TWRP Installer and Magisk.

[Taimen - Pixel 2 XL TWRP](https://twrp.me/google/googlepixel2xl.html)

[Walleye - Pixel 2 TWRP](https://twrp.me/google/googlepixel2.html)

You **must** download the TWRP `.img` file as we use that to temporarily boot TWRP, then we use the TWRP Installer `.zip` in order to install TWRP to our `/boot` to make it persistent between reboots.

### Sideloading

You must first activate ADB Sideload in TWRP. From the main menu go to:

- Advanced
- ADB Sideload
- Leave the default options for the checkboxes (wipeing cache, etc.)
- **Swipe to start Sideload**

You should hear your device reconnect to your computer.

```powershell
adb sideload [drag zip to be flashed here]
```

## Magisk

[Download the latest version of Magisk here.](https://forum.xda-developers.com/apps/magisk/official-magisk-v7-universal-systemless-t3473445)

Ensure that you remove modules that may prevent you from booting up, such as ones that replace system applications or modify/hook onto the system in some way (i.e. EdXposed).
{:.warning}