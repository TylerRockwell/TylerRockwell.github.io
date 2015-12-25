---
layout: post
title: Gaining Complete Control Over Your LG Optimus Exceed 2
description: "Bypass activation, flash ROMs, root"
tags: [LG, root, Verizon, phone, tech, LG Optimus Exceed 2]
---

Quick disclaimer: Some of the advice in this post can have potentially negative effects on your device like voiding your warranty or bricking your device. Ultimately it's your decision what you do with your phone, and I am not responsible for those decisions or the results thereof.

The LG Optimus Exceed 2 is a pretty decent prepaid phone running Android 4.4.2 KitKat. Amazon recently had these available for $11.99, which is dirt cheap. I managed to get my hands on 4 before they ran out of stock. It took some time to get things up and running properly on them, and I wanted to share my experiences (as well as make some notes for myself) on how to gain complete control over these devices.

## Bypass Verizon Setup Wizard

![Verizon Setup Wizard]({{ site.url }}/images/exceed-tutorials/setup-wizard.png){: .center-image}

Once you turn on your new phone, you'll be greeted with this seemingly inescapable screen. Since we won't be needing Verizon's services, let's just go ahead and use the built in button combination to bypass this screen.

#### Press the following buttons one at a time in this order:
  * Volume Up
  * Volume Down
  * Back
  * Home

You should then get a popup window asking if you want to leave setup. Don't worry if it doesn't work the first time. The timing has to be just right. Too fast or too slow, and you won't get the popup. Just keep trying until it shows up. Don't worry, once bypassed, the setup wizard will no longer run on startup.

![Yes, I'm really sure]({{ site.url }}/images/exceed-tutorials/setup-wizard-leave.png){: .center-image}

## Root using TowelRoot

TowelRoot is incredibly simple to use as long as you have the correct version of software running on the phone. To check your software version, go to Menu -> Settings -> About Phone -> Software information. On the bottom of this screen, under Software version, the phone should report VS450PP1.

![The Easy Version]({{ site.url }}/images/exceed-tutorials/lg-pp1-software.png){: .center-image}

If it says VS450PP2, you will need to [flash the phone]({% post_url 2015-12-24-lg-optimus-exceed-2-rom-flash %}) to version 1 before TowelRoot will work.

Once you've confirmed the software version, there's one more preparation step before installing. You need to enable the installation of apps from unknown sources. To do this, go to Menu -> Settings -> Security -> Unknown Sources. Make sure this box is checked, read the warning (or not), and tap OK.

Now that all of that is taken care of, go ahead and open a browser and head over to towelroot.com. Click on the giant lamba in the center of the screen, ignore the security warning, and tr.apk will be downloaded to the phone.

![It's hard to miss]({{ site.url }}/images/exceed-tutorials/towelroot-download.png){: .center-image}

Run the apk, install the app, and click open when done. You will be presented with this screen:

![Towelroot!]({{ site.url }}/images/exceed-tutorials/make-it-ra1n.png){: .center-image}

Go ahead and click make it ra1n. You should get the message informing you that your phone has been rooted and no reboot is required.

![Root success!]({{ site.url }}/images/exceed-tutorials/root-success.png){: .center-image}

Congratulations, you have root! There's only one more step to control which apps have root access. If the phone reboots, just run the app and try again. 2 of my phones failed and restarted, but everything went smoothly when I tried again. Technology, amiright?

If it says your phone is not currently supported, then you likely have the version 2 software I mentioned above. Follow the instructions to [flash the older version]({% post_url 2015-12-24-lg-optimus-exceed-2-rom-flash %}) then retry the steps in this section.

Finally, you need an app to manage root privileges for other apps. Go ahead to the Play Store and download SuperSU. Install it and update the binary if necessary. The app may ask you to reboot. That's it. Your phone is fully rooted. Hurray!
