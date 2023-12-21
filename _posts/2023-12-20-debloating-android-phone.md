---
layout: post
title:  "Removing Bloatware from your Android Phone"
date:   2023-12-20 23:22:00 +0100
categories: guides
---
<link href="//maxcdn.bootstrapcdn.com/font-awesome/4.2.0/css/font-awesome.min.css" rel="stylesheet">


| Requirements: Android Smartphone, USB Cable, Computer

TL;DR:

Install platform-tools

Install drivers (if necessary)

Enable USB Debugging

Run `adb shell`

Run `pm list packages`

Run `pm uninstall <PACKAGE_NAME>`

# Introduction

Many Android smartphones come with lots of unwanted apps preinstalled. The operating system does not give you the regular uninstall button, it merely lets you 'disable' the app.

![Screenshot of Android app option menu with three buttons: Open, Disable, Force Stop](/assets/img/disable-app.png)

This leads many users to believe that the app is somehow baked into the operating system and cannot be uninstalled. But with just a bit of trickery, you can remove all of the unnecessary apps from your phone.

| <i class="fa fa-exclamation-triangle"></i> **You will be using a command line. It is important that you always think first, then type. If you're not careful, you might end up bricking your phone or deleting something important. The command line has no safety net. Always re-read your commands before pressing enter.**

# Setting Up

The Android developers provide a set of useful utilities called the Platform Tools. You can download them from the [official mirror](https://developer.android.com/tools/releases/platform-tools#downloads) for your appropriate platform or using a package manager like [Homebrew](https://brew.sh/) (macOS) or [Chocolatey](https://chocolatey.org/) / [Winget](https://www.microsoft.com/p/app-installer/9nblggh4nns1) (Windows). You extract the .zip file to a location you can remember (preferably somewhere with a short path, such as `C:\platform-tools` or `/opt/platform-tools`). 

If you are planning on doing this often: make sure to add the platform-tools directory to `$PATH`.

If you are using Windows, you also need to install your phone's appropriate drivers for the computer to be able to communicate with the device. You can look up your vendor's drivers [here](https://developer.android.com/studio/run/oem-usb#Drivers) and instructions on the installation process [here](https://developer.android.com/studio/run/oem-usb).

If you're on macOS or Linux, you shouldn't need additional drivers. You can just continue.

# Connecting To the Phone

We are going to connect to the phone with a tool called Android Debug Bridge, **ADB** for short. This tool needs permission from your phone in order to connect. The specific permission needed is called USB debugging.

To enable USB debugging, we go into the system settings and scroll to the bottom to the *about* section. You now need to find the build number and tap it seven times. You should now see a message telling you that you have enabled developer settings. Go back to the main settings page and look for developer options. They might be at the top level or in the system category.

Within the developer settings, look for USB debugging. ![The Android debug settings panel](/assets/img/android-debug-settings.jpg)

You can now plug in your phone. If you get a notification that asks for permission to debug, confirm. If you got no such notification, a common fix is looking for the notification that asks what you want the USB connection to do and change it to something other than *No data transfer*.

If you have added the platform-tools directory to `$PATH`, you can skip the next step.

On Windows, use Shift + Right click in your platform-tools directory and click on "Open PowerShell window here".

On macOS you can open a terminal, type out `cd ` (notice the space at the end) and drag in the folder from finder.

On Linux, open a terminal and type `cd path/to/platform-tools/`, replacing the path with your actual install path.

# Uninstalling Apps

To check whether your phone is being recognized, type the following: `./adb devices`.
It should return a seemingly random string with the word "device" next to it. ![Result of adb devices with one device](/assets/img/adb-devices.png)

If your device does not show up, try reconnecting your phone and try perform the steps above again.

If everything worked, you should now be able to type `./adb shell` and have the start of the prompt change to your devices name.

![A prompt reading "kali:/ $"](/assets/img/kali-phone-prompt.png)

You are now inside of your device.

Next, we want to get a list of all the installed packages. To do that, we use the command `pm list packages`. 

![Result of `pm list packages`](/assets/img/pm-list-packages.png)

Searching through this list manually is quite tedious, so we will let the computer do the sorting. Luckily, there is a tool that does exactly that: `grep`.

We will use this command to find any package that contains a specific string of text: `pm list packages | grep <TEXT>`, replacing `<TEXT>` with the string we're looking for. For example: `pm list packages | grep facebook` returns all the packages with "facebook" in their name.

Either sift through the list manually, or search for the specific packages you want to uninstall. Copy the package identifier (usually starting with "com") to a file for every package you want to uninstall.

| <i class="fa fa-exclamation-triangle"></i> **Do NOT delete any package you don't exactly know the purpose of. Perform a full system backup beforehand.**

Now comes the destructive step: For every package in your list, run `pm uninstall --user 0 <IDENTIFIER>`.

![Result of pm list packages | grep ](/assets/img/pm-list-packages-grep.png)
![Result of pm uninstall --user 0 com.caf.fmradio](/assets/img/pm-uninstall-success.png)

If you are satisfied with the results, you can exit the shell with the `exit` command.
You can now close the terminal if you wish to do so.