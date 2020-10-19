---
layout: article
title: 'Unlock the Bootloader on a Google Pixel Device'
subtitle: 'Information on unlocking the bootloader on a Pixel or Nexus device'
tags: [root,google,pixel,nexus]
categories: [root]
published: true
date: 18-07-2019
aside:
  toc: true
show_edit_on_github: false
---

*This information was last updated on 18/07/19.*
Please feel free to join us on [Discord](https://discord.gg/GDguYJ4) if you have any questions or need some help.

# Why Unlock the Bootloader?
Unlocking the bootloader is the gateway to rooting, flashing custom images and flashing custom ROMs. There are ways to root your phone without unlocking the bootloader, but just in case things don't work out right, having the unrestricted access via fastboot may be your only option of rescuing your device.

<!--more-->

# What happens when I Unlock the Bootloader?
Android's SafetyNet will be tripped, it's an Google Play Services API which can be used by developers for their apps to check whether the device it is running on meets a certain standard set by Google.

This means that apps which rely on using SafetyNet API to determine whether their app runs on your device, cannot be used once the bootloader is unlocked, as having an unlocked bootloader doesn't fall under Google's standard.

The following apps are just some of the many who will kick up a fuss once you unlock the bootloader.

* Pokemon GO
* Ingress Prime (Redacted Scanner [1.0] still works)
* Google Pay
* Westpac Banking App (Fingerprint login)
* Snapchat

Generally, if the app is finance related, chances are that it will be using SafetyNet, and other things to check the validity of your device.

[More Information about SafetyNet][2]

[More Information about Android Compatibility Test Suite (CTS)][3]

## What can be done about it?
Recently, for the past few years, [Magisk][1] has been used to: root, provide a system-less interface, Magisk Modules (addons and plugins), as well as the *ability to hide from integrity tests, including SafetyNet*. (Emphasis mine).

Since it is the defacto root solution being used at the moment, if you root your phone using Magisk, chances are, your phone will pass SafetyNet. This however, will not do much if the app in question (i.e. Pokemon GO or Ingress Prime) uses other file-based checks in order to detect Magisk.

Magisk Manager is the app that will be used to manage Magisk, install Modules, hide Magisk from apps via 'Magisk Hide'. 

# Can I Unlock the Bootloader?
Unfortunately, not all Nexii or Pixels were made equal. Phones with the OEM unlock toggle disabled, have generally been done at the carrier's request. Usually Verizon will have theirs permanently locked (there is a workaround for the 1st generation Google Pixels), Sprint will lock it until you pay off the phone, and there are more carriers who will do this in other countries.

Generally speaking, if OEM unlock is disabled, and you only see the message "please connect to the internet or contact your carrier", and you **don't have a Pixel 1/XL**, you're most likely out of luck.

<div class='img-row'>
<div class='img-col'>
<img src="/maowdroid/assets/images/oem-unlocking/pixel-devop-oem-unlock-disabled-carrier-lock.png" width='width:100%'/>
</div>
<div class='img-col'>
<img src="/maowdroid/assets/images/oem-unlocking/pixel-devop-oem-unlock-disabled-contact-carrier.png" width='width:100%'/>
</div>
<div class='img-col'>
<img src="/maowdroid/assets/images/oem-unlocking/pixel-devop-oem-unlock-disabled-already-unlocked.png" width='width:100%'/>
</div>
</div>

## First Gen Pixel/XL (2016) Bootloader Unlock Workaround
**This is only necessary for those who cannot enable OEM unlock.**

Follow [this guide](https://forum.xda-developers.com/pixel-xl/how-to/how-to-unlock-bootloader-verizon-pixel-t3796030) on XDA.

# Unlocking the Bootloader
You must start by enabling OEM unlock (which we had discussed earlier above) in the Developer Options.

## Enable Developer Options

<div class='img-row'>
<div class='img-col'>
<img src="/maowdroid/assets/images/oem-unlocking/settings.png" width='width:100%'/>
</div>
<div class='img-col'>
<img src="/maowdroid/assets/images/oem-unlocking/about-phone.png" width='width:100%'/>
</div>
<div class='img-col'>
<img src="/maowdroid/assets/images/oem-unlocking/build-no-tap.png" width='width:100%'/>
</div>
</div>

- Go to **Settings**
- Scroll down and tap on **About phone**
- Scroll down to the end and tap on **Build number** until you are prompted to enter your PIN/Password/Pattern (or you see a toast saying 'You are now a developer!')

## Enable OEM Unlocking

<div class='img-row'>
<div class='img-col'>
<img src="/maowdroid/assets/images/oem-unlocking/developer-now.png" width='width:100%'/>
</div>
<div class='img-col'>
<img src="/maowdroid/assets/images/oem-unlocking/devop-oem-unlocking.png" width='width:100%'/>
</div>
</div>

- Go to *Settings* and tap on **System**
- Tap on **Advanced**
- Tap on **Developer options**
- Toggle on **OEM unlocking**
- Complete the prompts to enter screen lock (only if screen lock is set)

## Reboot your Phone in to the Bootloader

You can do this one of 3 ways.

1. *Power Off* device. Hold **Power** + **Volume Down**
2. Select *Restart* from the Power Menu, when the screen turns off or freezes, press and hold **Volume Down**
3. Use the `adb` command: `adb reboot bootloader`

## Unlock the Bootloader
Once your phone is in the bootloader. You can use the command `fastboot devices` to see if your device is connected properly with the computer. If you see your device's serial number there, it means you can continue.

Use the command `fastboot flashing unlock` to bring up the bootloader unlock confirmation screen on your phone.

Then use the volume buttons to change the option to **Unlock the Bootloader** and presse the **Power** button to select the option. Your phone should reboot back into the bootloader after this. You should see that the `device state:` is now `unlocked` in red. Select **Start** using the volume buttons and the power button to boot into Android.

## Finished!
Now your phone's bootloader is unlocked! Ready to flash custom images, boot things and of course, root your phone! Now browse the XDA sub-forum for your device to get started.

[1]: https://forum.xda-developers.com/apps/magisk/official-magisk-v7-universal-systemless-t3473445
[2]: https://developer.android.com/training/safetynet
[3]: https://source.android.com/compatibility/cts/