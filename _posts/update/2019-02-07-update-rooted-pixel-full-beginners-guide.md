---
layout: article
title: 'Update a Rooted Pixel Device using Factory Images'
tags: [pixel,update,rooted]
categories: [update]
published: true
date: 07-02-2019
aside:
    toc: true
show_edit_on_github: false
---

This is an in-depth look at how you can update your rooted Pixel device using the factory images provided by Google every month. This is just one way of doing it, but it turns out to be the most comfortable way of doing so.

Please feel free to join us on [Discord](https://discord.gg/GDguYJ4) if you have any questions or need some help.

<!--more-->

# Updates
Updates to the article are listed below, from the most recent onwards.

## Android 10, TWRP and Pixel 3 / 3 XL
*7 Nov. 2019*

**Pixel 3 / 3 XL** users, TWRP won't be working very well with **Android 10** just yet, mainly due to partition changes and of course, how they've changed the AOSP recovery sources as well. You won't be able to follow this guide all the way through. As these changes will force you to install Magisk a different way (via `boot.img` patching.)
{:.error}

All other Pixels will be OK with using TWRP. The Pixel 1 series will be able to decrypt `/data` on Android 10 with TWRP 3.3.1-0.

# Video

<div>{%- include extensions/youtube.html id='CEKXPjgYCVg' -%}</div>

# Requirements
* Unlocked bootloader
* A computer
* A USB Type A to Type C cable
* Heaps of time
* Capacity to learn

# Guide
## Tips and Tricks
You **do not need** to incrementally update when using the factory images. Since the full system images are included within the package.

You should remove the Active Edge Module used with Edge Sense Plus, developed by j to the 4n.

<img class="image image--lg" src="/maowdroid/assets/images/update-rooted-pixel/active-edge-update-dialogue.png"/>

You should also remove Substratum overlays, especially for themed `system` applications such as:
* SystemUI
* Android Framework
* etc...

If you're unsure, it's best to remove them all.

## Before Updating
Backup your data! Copy over photos, music, downloads to your computer for safekeeping.

If you want to backup your apps and appdata, you can use a root backup utility such as [Swift Backup](https://play.google.com/store/apps/details?id=org.swiftapps.swiftbackup) or [Titanium Backup](https://play.google.com/store/apps/details?id=com.keramidas.TitaniumBackup).

If you prefer having a full system backup, creating a backup in TWRP is your best choice. However, you may have issues restoring those backups through my own experience.

## Setting up SDK Platform Tools (ADB & fastboot)
I promise, once you take the time adding the platform-tools directory, which contains commonly used executables such as `adb.exe` and `fastboot.exe` (sans .exe on other platforms), it would be in your best interest to add those to the [PATH environment variable](https://superuser.com/questions/284342/what-are-path-and-other-environment-variables-and-how-can-i-set-or-use-them) on your machine.

In short, it allows you to run `adb` and `fastboot` commands without the need for changing your command prompt, terminal or PowerShell's current directory to where you have your `platform-tools` located.

I have a short video on how to do that here.

<div>{%- include extensions/youtube.html id='43gQRruotW0' -%}</div>

You should always check for updates to the platform-tools, and updating is as easy as replacing the old platform-tools you have extracted earlier, with the newer ones downloaded.

## Downloads
As usual we need to download a few things. Here are links to the files that you will typically need.

### SDK Platform Tools (adb & fastboot)
[SDK Platform Tools](https://developer.android.com/studio/releases/platform-tools) - Once again, if you have set these up as shown above, you don't need to keep using a separate instance of the platform-tools, as long as the ones you have are **up to date**.

### Factory Images
[Factory Images for Nexus and Pixel Devices](https://developers.google.com/android/images) - Official Google downloads for various factory images for almost every Google device out there.

There are entries which have 2 versions for a particular month. For example, the Pixel 3's December factory images has 2 varieties, one with *Docomo* and one without.

Version | Download | SHA-256 Checksum
------------ | ------------- | -----------------
9.0.0 (PQ1A.181205.006, Dec 2018) | Link | 3df41a2b65335bb...
9.0.0 (PQ1A.181205.006.A1, Dec 2018, Docomo) | Link | d6fefe86e203d4c...

All you need to do is think, am **I** using the Docomo network?

If yes, then I'll download the one that has Docomo in it. If no, I'll download the one that doesn't say anything extra.

The same goes for any other carrier, so just download the one that is right for **you**. It doesn't matter if you didn't buy the phone from Verizon, or Docomo in this case.

### Pixel Update Bulletin
[Pixel Update Bulletin](https://source.android.com/security/bulletin/pixel) - Here you can check out what has been patched, and what bugs have been fixed in the corresponding factory image.

### TWRP (TeamWin Recovery Project)
[TWRP (device search)](https://twrp.me/Devices) - This is TWRP.me's device search page. Start typing in your device's name, or codename and it'll return a link to its relevant TWRP page.

For most of the A/B partitioned devices out there, Pixels included. TWRP is not installed in the traditional way of flashing it to the `/recovery` partition, since that has been merged into the `/boot` with this partition layout. So if you wish to install TWRP permanently, you must download the `twrp-<device>-installer-<device-codename>-X.X.X-X.zip` flashable zip.

**Note:** Installing TWRP is optional. Completely up to you! But if you do choose to install it. You must flash it **first**. Please also realise the implications for installing TWRP to your device (*no more OTAs!*).
{:.info}

In short. If you want to re-root via TWRP. You **must** download the TWRP.img. If you want to use TWRP without needing a computer to boot the TWRP.img each time, you must also download and flash the TWRP-Installer.zip.

Regardless of whether you want to install TWRP or not, you **must** download the image to boot TWRP temporarily. I hope that clears it up! 🤗

#### TWRP Functionality
Sometimes TWRP may not be functionally on par with other devices. The best way to check is under the **Status:** header of the device's TWRP download page. This will tell you if MTP is working, or if ADB can only be used in certain conditions.

#### What's an .asc, .md5 or .sha256 file?
Those are used to check the authenticity and completeness of the TWRP image/zip you are about to download. Those are **NOT** the files you need when it comes to flashing TWRP to your phone.

If you can read this part of their download page: `Thank you for choosing TWRP. Please click the link below to start your download.` You should know which link to click. 😉

### Magisk
[Magisk](https://forum.xda-developers.com/apps/magisk/official-magisk-v7-universal-systemless-t3473445) - Our root and module manager, all systemless-ly of course. You can choose either the beta or stable versions of Magisk.

The only times where you need to be careful is when a new device is released, and the existing versions of Magisk may not be compatible with it, or when a new major version of Android is released, i.e. Android Q. You should wait for new versions of Magisk, or check the changelogs, located at the end of the XDA thread.

## Updating
Once you have the platform tools set up, you just need to extract a few more items.

Open the factory image, and go into the folder inside the archive. Now you should see a bunch of files with .img, .sh, .bat & .zip.

![Image](/maowdroid/assets/images/update-rooted-pixel/factory-image-contents.png){:.shadow}

Extract the following three (3) files to where you have everything else downloaded:

* **image**-`device`-`build`.**zip**
* **bootloader**-`device`-`version`.**img**
* **radio**-`device`-`version`.**img**

Then copy over the `twrp-installer.zip` (optional) and `Magisk.zip` to your phone.

Once you have done that, reboot your phone into the bootloader by either:
* Power off. Then hold **Power + Volume Down**.
* Restart, and when the screen turns black or freezes, hold **Volume Down**.

When your phone is in the bootloader, you can follow this command sequence.

`fastboot devices` - This will return a list of devices' serial numbers connected via fastboot. If you see a serial number there, and only one. You may continue.

`fastboot flash bootloader [drag in bootloader.img]` - This will flash the provided image to the device's current slot bootloader partition.

`fastboot reboot bootloader` - After flashing critical partitions, it's best to reboot your phone back into the bootloader.

`fastboot flash radio [drag in radio.img]` - This will flash the provided image to the device's current slot radio partition.

`fastboot reboot bootloader` - Once again, after flashing critical partitions, it's best to reboot your phone back into the bootloader.

`fastboot --skip-reboot update [drag in image.zip]` - This is where the bulk of the updating comes into play. Notice the `--skip-reboot` flag we use. This is to prevent the bootloader from rebooting the phone once the command finishes, since we still want to boot into TWRP to re-root our phone after the update.

The command should take about 60 seconds to run, depending on USB transfer and PC speed.

Once the update command has finished **successfully**, we can now boot into TWRP temporarily using the TWRP image and this fastboot command.

`fastboot boot [drag in TWRP.img]` - This command uploads the image to the device for it to boot from once. This is only temporarily as once it boots the image would have been discarded from your devices RAM. Give your device a few moments for it to boot into TWRP.

## Installing TWRP & Re-rooting
Upon booting into TWRP you may be greeted with the following screens.
- [Data Decryption](#data-decryption)
- [Keeping System Read Only](#keeping-system-read-only)

### Data Decryption
Our Pixels by default encrypt your data partition. In order for TWRP to access your internal storage or what's more commonly known now as your `sdcard`, you'll need to give TWRP your screen lock details (PIN, password or pattern).

<img class="image image--lg" src="/maowdroid/assets/images/update-rooted-pixel/twrp-decrypt.png"/>

### Keeping System Read Only
This one is a little trickier, but in short, if you are just rooting, tap the option to **Keep Read Only**. You can change it later on in the `Mount` menu in TWRP.

<img class="image image--lg" src="/maowdroid/assets/images/update-rooted-pixel/twrp-unmodified-system.png"/>


### TWRP Main Menu

<img class="image image--lg" src="/maowdroid/assets/images/update-rooted-pixel/twrp-main.png"/>

Keep this in mind as I'll be referring to it later on, throughout the guide.

### Installing TWRP
Please remember that this is optional, you **DO NOT** have to install TWRP persistently on your device for it to be rooted. Heck, you don't even need TWRP to root your phone!

But if you'd like to have TWRP, follow the following steps.

<img class="image image--lg" src="/maowdroid/assets/images/update-rooted-pixel/twrp-file-browse.png"/>

Tap `Install` on TWRP's main menu. You will now need to browse for the `twrp-installer.zip` you had copied over previously. By default, the file browser will open up to where you were last. To go up a directory, scroll to the top and select the item which says `(Up A Level)`.

<img class="image image--lg" src="/maowdroid/assets/images/update-rooted-pixel/twrp-file-browser-located.png"/>

Once you find the `twrp-installer.zip`, tap on it and then swipe to confirm flash.

<img class="image image--lg" src="/maowdroid/assets/images/update-rooted-pixel/twrp-flash-twrp-installer.png"/>
<img class="image image--lg" src="/maowdroid/assets/images/update-rooted-pixel/twrp-flash-twrp-installer-done.png"/>

Now tap the Back button, and then from the main menu, tap on `Reboot`, and select `Recovery`. This way we can test if we have successfully installed TWRP.

### Flashing Magisk
Once you are in TWRP, and you're at the main menu. Tap on `Install`, and browse for the `Magisk.zip` you had copied over earlier.

<img class="image image--lg" src="/maowdroid/assets/images/update-rooted-pixel/twrp-file-browser-located.png"/>

Then swipe to confirm flash. This will root your phone by installing Magisk to your newly updated boot image.

<img class="image image--lg" src="/maowdroid/assets/images/update-rooted-pixel/twrp-flash-magisk.png"/>
<img class="image image--lg" src="assets/images/update-rooted-pixel/twrp-flash-magisk-done.png"/>

Once Magisk has finished flashing, tap on `Reboot System` if you have nothing else to flash. It's generally a good idea to see if your phone can even boot into Android at this point, before you throw more stuff at it.

## Booting into Android
Your first boot after updating shouldn't take too long, give it a few minutes, 10 minutes at most. If it takes longer than that, you might consider your phone in a bootloop right now. Head over to the [troubleshooting](#troubleshooting) section to see what you can do.

Once you're in Android, no data should have been lost, everything should be there as you had left it. You can open up Magisk and check its install status, as well as SafetyNet. 🏁

## Ta-da 🎉
CONGRATULATIONS! You now know how to update your rooted Pixel phone using the factory images! In no time at all, you'll become a pro! 😊

# Troubleshooting
- [TWRP Related](#twrp-related)
    - [TWRP can't decrypt my data!](#twrp-cant-decrypt-my-data)
- [Boot up Related](#boot-up-related)

## TWRP Related
### TWRP can't decrypt my data!
You have four options:
1. Use ADB sideload to flash Magisk/TWRP installer without TWRP needing access to your internal storage.
2. Use a USB OTG cable/adapter to insert a USB with the required flashable files and use TWRP to flash the zips from there.
3. Reboot back into Android, remove your screen lock and boot into TWRP again with the steps above.
4. Wait for a newer version of TWRP.

## Boot up Related
### My phone can't boot into Android
There's a change that it could be either:
* You had an incompatible Magisk module installed previously.
* Just a Magisk bug.

To resolve the ones that include Magisk, boot back into TWRP and flash the `Magisk-uninstaller.zip` found on the Magisk XDA thread.

### My phone keeps booting into TWRP
I've only noticed this if you were to flash Magisk, then TWRP. When you're supposed to flash TWRP then Magisk.

So flash the stock boot image, or flash the `Magisk-uninstaller.zip` and flash the TWRP installer and Magisk in the appropriate order.

### Apps keep crashing when my phone turns on and I can't use it
You probably forgot to uninstall a system overlay installed by Substratum, silly you. Try flashing the Substratum rescue.zip found at `sdcard/substratum/SubstratumRescue.zip`, or do a factory reset in TWRP. Or painstakingly remove the overlay .apks from TWRP's file manager.

[More information can be found here (*may not be up to date*)](https://forum.xda-developers.com/showpost.php?p=76687481&postcount=6).