---
layout: article
title: 'Root Pixel 4 & Pixel 4 XL on Android 10 Walkthrough'
tags: [pixel 4,pixel 4 xl,root,magisk,android 10]
category: [root]
published: false
date: 20-11-2019
---
The Pixel 4 and its larger sibiling, the Pixel 4 XL can be rooted with the latest version of Magisk. Although we don't have a custom recovery right now, we can use Magisk Manager to patch a stock `boot.img` with Magisk. The video is **long** and even includes a FAQ in the beginning. If you're a beginner, I highly recommend watching it.

<!--more-->

Anyways, here's the written rundown of what we did in the video. This will also provide updates in the cases where a comment or description change just won't do.

# Video

<div>{%- include extensions/youtube.html id='S2Ke36U2WqQ' -%}</div>

# Before You Begin

One of the steps that is required to root your Pixel 4, is unlocking the bootloader. When you do so, it will wipe your internal storage, so anything you had on your phone will * *poof* * disappear.
{:.error}

Try to give yourself as much time as possible, just in case things go wrong.

And if you run into any problems, join us on Discord and ask in one of the **#help** rooms!

<div>{%- include extensions/discord.html -%}</div>

# FAQ

Here are some frequently answered questions when it comes to rooting a phone.

## 1. Can this brick my phone?

As with anything that involves touching sensitive parts of the phone (software wise), it is possible, but in this current climate, it's very unlikely. Even back when custom development was just catching on, it's been relatively safe.

Google even provides the tools and original firmware for you to use in case you need to use it!

## 2. Will I get software updates?

You will get software updates via an OTA (over-the-air) update (*commonly referred to as OTAs*) and you'll be able to use Magisk Manager to ensure that you can keep root access after you restart to finish the update. Because you have modified your phone, you will need to do these extra steps each time you want or get an OTA.

In the case that you no longer get OTA updates sent to your phone when you check for them, since we have the bootloader **unlocked**, we can use the Google Factory Images to update our phone via `fastboot`. The next point will cover this.

## 3. Can I update after rooting?

Yes of course! You can either update via OTA and Magisk Manager, or the Factory Images and fastboot. I will have these videos come out later on throughout the year.

Although, in some rare cases you cannot keep root when updating, for example, when Android 11 developer preview is released, Magisk may not be able to support it initially, but in due course, it will have support for Android 11, but you'll just have to wait.

Otherwise, for month to month updates, you should be able to keep root after updating.

## 4. Will my apps work normally after rooting?

Maybe. Well, right now Magisk seems to be able to hide itself or the fact that your phone has been modified in some way quite well for some time now. That means you can use Google Pay, and use apps such as Pokemon GO, Ingress Prime, Snapchat, *banking apps*, and the list would go on. Most of these apps will use the SafetyNet API to determine the validity of your system, as well as their own in-house checks.

Right now, Magisk has had a big development into its hiding ability, so I think this will be the case for many moons to come.

If it's a popular app, you should be able to find support for it because there will be a lot of dedicated individuals wanting to use the app on their rooted phone too.

**However**, this is ultimately a [cat and mouse game](https://en.wikipedia.org/wiki/Cat_and_mouse) between the app developers, Google and [Magisk's developer, topjohnwu](https://twitter.com/topjohnwu/). One day someone will get the upper hand and you might not be able to use your apps on your rooted phone, but only time will tell.

## 5. Can I unroot?

Yes, 100% you can. Since we have the factory images, we can use those to restore the state of your phone back to the way it was immediately after unlocking the bootloader, and to top things off, we can relock the bootloader (which is the last thing you should do).

# Process

This is the process that is shown in the video:

1. Enable OEM Unlock inside the Developer Options
2. Patch a `boot.img` using Magisk Manager
3. Unlock the bootloader
4. Flash the `magisk_patched.img` to root

In hindsight, I should have done it like so:

1. Enable OEM Unlock inside the Developer Options
2. Unlock the bootloader
3. Patch a `boot.img` using Magisk Manager
4. Flash the `magisk_patched.img` to root

This will allow Magisk Manager to restore the stock images if you choose to take an OTA using Magisk Manager. However, you can go through patching the `boot.img` again after rooting so Magisk Manager has a copy of it to use for updating.

# Downloads

We need to grab a few things that we'll use when we root our Pixel, so here they are. Save them all into the same folder to avoid headaches later. 😉

[Google USB Drivers][1] | This is only really required for Windows computers, although we can usually trust Windows Update to install the right driver for us, we will install it just in case we need it.
[SDK Platform Tools (adb & fasboot)][2] | This package contains a whole bunch of binaries/executables including the ones we need the most, `adb` and `fastboot` (*and their respective DLLs on Windows*).
[Google Factory Images][3] | These are the original firmware/software that Google provides for their devices. In here, we have the **stock** images that we'll use (the `boot.img`).
[Magisk][4] | The XDA thread for Magisk and all of its related files, this will include a link for Magisk Manager too.


Once you have downloaded those files, let's continue.

[1]: https://developer.android.com/studio/run/win-usb "Google USB Drivers for Windows"
[2]: https://developer.android.com/studio/releases/platform-tools "Android SDK Platform Tools (adb & fastboot)"
[3]: https://developers.google.com/android/images "Google Factory Images"
[4]: https://forum.xda-developers.com/apps/magisk/official-magisk-v7-universal-systemless-t3473445 "Magisk XDA Thread"

# Enabling OEM Unlock

You must be able to enable OEM unlock or you can forget about rooting your phone. 😢 Keep in mind that some carriers require you to pay off the phone before they allow you to unlock the bootloader. Pixels activated on or from Verizon are not going to be able to unlock their bootloaders unless an exploit is found.
{:.warning}

## Enable Developer Options

Go to Settings, then scroll down to **About Phone** and in there scroll down to the bottom and tap on the build number 7 times (or until you get the screen where you need to enter your screen lock).

<div>{%- include extensions/single-image.html path="/assets/images/rp4/dev-op-build-no.png" -%}</div>

After you enter your PIN, pattern or passcode to enable Developer Options.

<div>{%- include extensions/single-image.html path="/assets/images/rp4/dev-op-pin.png" -%}</div>

Then head about out to the main settings screen and then tap on **System**, and then select the newly enabled **Developer options**.

<div>{%- include extensions/single-image.html path="/assets/images/rp4/sys-dev-op.png" -%}</div>

From here, enable **OEM unlock**.

**Notice:** If that toggle is disabled, read the small message underneath, it may tell you to contact your carrier, or tell you that it is not possible on network locked devices. If that is the case, you will **not** be able to unlock the bootloader, hence root, right now.
{:.info}

## Using adb & fastboot

To use these programs, we need to use them via a shell. You'll probably know these as the Command Prompt (`cmd.exe`), PowerShell (`powershell.exe`), or any flavour of a macOS & Linux terminal.

I'll be referring to this as a/the **terminal** from now on.
{:info}

As it is now, you will need to have the current directory of the terminal as the directory where the platform tools are (adb & fastboot). This is because of how the terminal interprets the commands you give it.

This is because the places where the terminal will look through to find the command to run (for example: `fastboot devices`) is the current directory and the PATH environment variable.

If you wish to be able to run `adb` & `fastboot` from any terminal, irrespective of its current directory, you will need to ensure that the location of the platform tools folder is in a permanent place (more or less, you can change the PATH environment variable if you ever move the location of the platform tools).

Take a look at this video here, a guide on adding the platform tools to the PATH environment variable on Windows. Once you follow this, you'll be able to run `adb` and `fastboot` commands from any terminal without having to change directories to where the platform tools are located each time you want to use it.

This will also enable you to use scripts that call the `adb` and `fastboot` commands without having to do anything extra.

<div>{%- include extensions/youtube.html id='43gQRruotW0' -%}</div>

## Install Google USB Drivers

This is usually necessary, but recently Windows Update has been able to source and install both the ADB and Bootloader interface drivers for Android phones. Even if that is the case, I highly recommend installing the Google ones for your computer to fall back on if needed.

### Extract the USB Drivers

Open the Google USB driver.zip that you had donwloaded earlier, and extract the `usb-driver` folder inside.

Once that is extracted, open the extracted `usb-driver` folder and locate the `.inf` file. Right-click on that file and select the **Install** option. You may have to accept a 'trust' prompt when installing the driver. You can optionally check **Trust Google LLC** so you're not asked again.

Once installed, you should see a success prompt. Once that is done we can continue!

## Unlocking the Bootloader

There are 2 ways to boot into the bootloader. First one is to restart your phone, and as soon as the screen turns black or freezes, hold **Volume Down**.

The other way to do it is to power off the phone, and then hold **Power** and **Volume Down**.
