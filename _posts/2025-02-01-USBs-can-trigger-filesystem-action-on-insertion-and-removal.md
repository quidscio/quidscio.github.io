---
layout: default
title:  "Udev and a proper way to interact with the file system"
categories: linux
---

In building a medium-security file server I decided to put the encryption key on a usb drive.
Ideally, usb insertion mounts and unlocks an encrypted drive.
And, usb removal causes the encrypted drive to be locked.
After trial and a couple of major errors, I discovered there are obvious but definitley wrong ways before plowing through one that works. 

# One way that works 

USB insertion triggers a udev rule which triggers a service which triggers an unlock script. File system operations occur in the script.
USB removal triggers a udev rule which triggers a lock script. Again, file system operations occur in a script.

