---
layout: post
title: Flashing Your LG Optimus Exceed 2 to Rootable Software VS450PP1
description: "Bypass activation, flash ROMs, root"
tags: [LG, root, Verizon, phone, tech, LG Optimus Exceed 2]
---

Quick disclaimer: Some of the advice in this post can have potentially negative effects on your device like voiding your warranty or bricking your device. Ultimately it's your decision what you do with your phone, and I am not responsible for those decisions or the results thereof.

![Verizon Setup Wizard]({{ site.url }}/images/exceed-tutorials/flash-before.png){: .center-image}

So, TowelRoot says your phone isn't supported and/or you've confirmed your software version is VS450PP2. Abandon all hope, ye who enter here. Actually, the process isn't all that bad. It took me a few hours the first time to research everything and get it all working, but now that the process is in place, I can take a new phone, flash its software, and have it rooted in about 10 minutes. I'll give you an overview of the necessary steps, then go through each one in detail. You will need a Windows box (physical or virtual, it shouldn't matter) and a USB cable (which comes with the phone).

#### To flash the old software, you must:

1. Get the necessary software on your PC
2. Put the Exceed 2 in download mode
3. Run the flash tool.
4. Reboot the phone and reap the benefits of a rootable device.

That's it. 4 steps. My coffee takes more than 4 steps to prepare, so flashing shouldn't be any trouble at all. Let's get started.

#### 1. Get the necessary software on your PC

You will need:

 * [The LG Driver](https://www.androidfilehost.com/?fid=24052804347802528)
 * [The LG Flash Tool 2014](http://www.mediafire.com/download/fwrcd3pdj0svjtb/LG+Flash+Tool+2014.zip)
 * [The VS450PP1 KDZ file](http://goo.gl/XxHrvZ)
 * [The Visual C++ Runtime Library](https://www.microsoft.com/en-us/download/details.aspx?id=48145) (only if you have problems running the LG Flash Tool 2014)

Install the LG drivers and make sure the LG Flash Tool runs for you. Also, this is IMPORTANT, put the KDZ file in the same folder as LGFlashTool2014.exe. Not doing so can cause problems with flashing, and you don't want that.

This is worth saying again. Put the KDZ file in the same folder as LGFlashTool2014.exe! Right now!

#### 2. Put the Exceed 2 in download mode

To do this, first shut down the phone. Plug your USB cable into your PC. While the phone is off, hold the volume up button and plug the other end of the USB cable into your phone. Keep holding the volume up button until the phone is in download mode. You do NOT need to press any other buttons for this to happen. Step 2 complete.

#### 3. Run the flash tool

![LG Flash Tool Main Screen]({{ site.url }}/images/exceed-tutorials/flash-tool-main.png){: .center-image}

When the software first loads you'll be presented with this window.

You don't need to change anything here. Just click the folder icon and select your KDZ file (remember, it's in the same folder as LGFlashTool2014.exe). Once you do that, the window should look like this:

![Verizon Setup Wizard]({{ site.url }}/images/exceed-tutorials/flash-tool-kdz-selected.png){: .center-image}

Once everything is good, click on CSE Flash. Normal flash does not wipe the phone, and can cause problems like endless boot loops. Don't use it.

On the next screen, click start. Don't click on anything else. Just Start. A Select Country & Language window will appear. Just click OK. I know it has information about Korea filled in. Don't worry about any of it. The app will default to doing everything in English.

Finally, the LG Mobile Support Tool will appear. It may warn you about not being able to connect to the server. Just click OK and keep an eye on your phone. You will see the progress bar fill as the software installs. The phone will automatically restart once the install finishes. With any luck, it will boot back to the Verizon setup wizard. The phone will reboot once more after being at this screen for a few seconds. When it's done booting again, feel free to bypass the screen using the super secret combination.

Go ahead and check your software version. It should now read VS450PP1. Congrats, you did it! The phone is now ready to be rooted.

![Verizon Setup Wizard]({{ site.url }}/images/exceed-tutorials/flash-after.png){: .center-image}
