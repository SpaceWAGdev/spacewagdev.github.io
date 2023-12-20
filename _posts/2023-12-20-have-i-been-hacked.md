---
layout: post
title:  "Have I been hacked?"
date:   2023-12-20 17:18:00 +0100
categories: guides
---

# The 'You Have Been Hacked' Website

![Screenshot of a typical "Your device has been hacked message on iOS"](/assets/img/haveibeenhacked.jpeg)

Chances are, you've come across one of these websites at least once. All of them try to convince you to download some app or give them your information. 

Do not do that. **You have not been hacked**. They are fake. Yes, all of them. No, nothing bad will happen if you just close the browser tab. I promise. 

# Downloaded something fishy?
Unless you're trying to buy malware (don't do that, please) or your friend sent you their malware sample (if your friends send you their malware samples, I'm pretty sure you already know what you're doing),
uploading the file to [VirusTotal](https://www.virustotal.com/gui/home/upload) is always a good idea if you're unsure. It checks the file [hash](https://en.wikipedia.org/wiki/Hash_function) against a database of known malware by lots of antivirus services. If your sample is found in the database, it will show you.

Do you often download files you're unsure about and are running Windows? [VirusTotalUploader](https://github.com/SamuelTulach/VirusTotalUploader/releases) lets you upload your files directly from the File Explorer.

An [official utility](https://support.virustotal.com/hc/en-us/articles/115002179065-Desktop-Apps#mac-osx-uploader) which essentially lets you do the same thing also exists for macOS.

Linux users are advised to build the macOS uploader from source. (If you know how to do that, you might as well use the [CLI](https://virustotal.github.io/vt-cli/).) 