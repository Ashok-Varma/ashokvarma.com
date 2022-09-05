---
title: "ADB and Fastboot setup"
layout: post

categories: post
tags:
---

First you need to have either sdk or android-platform-tools installed in your pc.

Basic Troubleshooting connectivity issues:
- try a reboot of the PC
- try different usb cables and ports
- dont use a usb hub
- dont use usb 3.0 only usb 2.0 works
- make sure nothing capable of comunicating with the phone is enabled and running. htc sync,pdanet,easy tether,and even itunes have all been known to cause issues.
- windows 8 has been known to have issues. try a windows 7 or older machine

## What is adb?

The [Android Debug Bridge](http://en.wikipedia.org/wiki/Android_Debug_Bridge) (`adb`) is a development tool that facilitates communication between an Android device and a personal computer. This communication is most often done over a USB cable, but Wi-Fi connections are also supported. `adb` can also be used by developers to communicate with a virtual android machine running on the computer.

`adb` is like a “Swiss-army knife” of Android development. It provides numerous functions that are described in detail by the command: `adb --help` (see output [here](http://wiki.cyanogenmod.org/w/Adb_--help)). Some of the more commonly used commands are listed in the [Popular adb commands](http://wiki.cyanogenmod.org/w/Doc:_adb_intro#Popular_adb_commands) section below.

## Installing adb & fastboot

### Windows, Mac, and Linux

The best way to get `adb` and `fastboot` is to install the [Android SDK](http://wiki.cyanogenmod.org/w/Sdk) directly from Google. After you install the SDK Tools, launch the SDK Manager and install the _Android SDK Platform-tools_ package. Note that the manager automatically selects the latest _Android X.x (API YY)_ package on launch which you can safely deselect if you are only interested in `adb` and `fastboot`. Then, by running the SDK manager periodically to check for updates, you can ensure these tools are always at the latest version.

The `adb` and `fastboot` executables will be located in the `platform-tools` subdirectory of the SDK Tools. You can add this directory to your system’s PATH so that these tools are available from any Command Prompt or Terminal:

-   Windows 7/8:
    1.  From the desktop, right-click My Computer and select Properties
    2.  In the System Properties window, click on the Advanced tab
    3.  In the Advanced section, click the Environment Variables button
    4.  In the Environment Variables window, highlight the Path variable in the Systems Variable section and click the Edit button
    5.  Append `;<path-to-sdk>/platform-tools` to the end of the existing Path definition (the semi-colon separates each path entry)

-   Linux
    1.  Add the following to `~/.profile` and then logout/login: `if [ -d "<path-to-sdk>/platform-tools" ] ; then   PATH="<path-to-sdk>/platform-tools:$PATH"   fi`


-   Mac
    1.  Add the following to `~/.bash_profile` and then logout/login: `if [ -d "<path-to-sdk>/platform-tools" ] ; then   export PATH="<path-to-sdk>/platform-tools:$PATH"   fi`


### Ubuntu

An easy alternative to installing the SDK package as described above exists on Ubuntu and other debian-based Linux distributions. `adb` and `fastboot` can be installed via the following commands from the Terminal:

```bash
sudo apt-get install android-tools-adb
sudo apt-get install android-tools-fastboot
```

There is no need to manually edit your system’s Path if this method is used.

If even now your device is not being detected in adb devices or fastboot devices

1.  Verify your username is included in the plugdev group. Type `groups` from a terminal and look for `plugdev` in the listed groups. **If** you do not see `plugdev` listed, you can add your username to the group with: `sudo gpasswd -a username plugdev` where `username` should be replaced with your linux username.
2.  Copy the set of rules listed below these steps to a text file and save it as `/etc/udev/rules.d/51-android.rules`. You will need sudo/su to write to that directory. So, for instance: `sudo nano /etc/udev/rules.d/51-android.rules` These rules cover all vendors [listed by Google](http://developer.android.com/tools/device.html#VendorIds). Optionally, you can add just the vendor corresponding to the device(s) you plan to connect to your computer.
3.  Restart your computer and then test plugging in your device to the computer with USB debugging enabled.
    <details>
      <summary>Device Manufacture Based</summary>

    ```bash
    #Acer
    SUBSYSTEM=="usb", ATTR{idVendor}=="0502", MODE="0664", GROUP="plugdev"
    #ASUS
    SUBSYSTEM=="usb", ATTR{idVendor}=="0b05", MODE="0664", GROUP="plugdev"
    #Dell
    SUBSYSTEM=="usb", ATTR{idVendor}=="413c", MODE="0664", GROUP="plugdev"
    #Foxconn
    SUBSYSTEM=="usb", ATTR{idVendor}=="0489", MODE="0664", GROUP="plugdev"
    #Fujitsu & Fujitsu Toshiba
    SUBSYSTEM=="usb", ATTR{idVendor}=="04c5", MODE="0664", GROUP="plugdev"
    #Garmin-Asus
    SUBSYSTEM=="usb", ATTR{idVendor}=="091e", MODE="0664", GROUP="plugdev"
    #Google
    SUBSYSTEM=="usb", ATTR{idVendor}=="18d1", MODE="0664", GROUP="plugdev"
    #Haier
    SUBSYSTEM=="usb", ATTR{idVendor}=="201e", MODE="0664", GROUP="plugdev"
    #Hisense
    SUBSYSTEM=="usb", ATTR{idVendor}=="109b", MODE="0664", GROUP="plugdev"
    #HTC
    SUBSYSTEM=="usb", ATTR{idVendor}=="0bb4", MODE="0664", GROUP="plugdev"
    #Huawei
    SUBSYSTEM=="usb", ATTR{idVendor}=="12d1", MODE="0664", GROUP="plugdev"
    #K-Touch
    SUBSYSTEM=="usb", ATTR{idVendor}=="24e3", MODE="0664", GROUP="plugdev"
    #KT Tech
    SUBSYSTEM=="usb", ATTR{idVendor}=="2116", MODE="0664", GROUP="plugdev"
    #Kyocera
    SUBSYSTEM=="usb", ATTR{idVendor}=="0482", MODE="0664", GROUP="plugdev"
    #Lenovo
    SUBSYSTEM=="usb", ATTR{idVendor}=="17ef", MODE="0664", GROUP="plugdev"
    #LG
    SUBSYSTEM=="usb", ATTR{idVendor}=="1004", MODE="0664", GROUP="plugdev"
    #Motorola
    SUBSYSTEM=="usb", ATTR{idVendor}=="22b8", MODE="0664", GROUP="plugdev"
    #MTK
    SUBSYSTEM=="usb", ATTR{idVendor}=="0e8d", MODE="0664", GROUP="plugdev"
    #NEC
    SUBSYSTEM=="usb", ATTR{idVendor}=="0409", MODE="0664", GROUP="plugdev"
    #Nook
    SUBSYSTEM=="usb", ATTR{idVendor}=="2080", MODE="0664", GROUP="plugdev"
    #Nvidia
    SUBSYSTEM=="usb", ATTR{idVendor}=="0955", MODE="0664", GROUP="plugdev"
    #OTGV
    SUBSYSTEM=="usb", ATTR{idVendor}=="2257", MODE="0664", GROUP="plugdev"
    #Pantech
    SUBSYSTEM=="usb", ATTR{idVendor}=="10a9", MODE="0664", GROUP="plugdev"
    #Pegatron
    SUBSYSTEM=="usb", ATTR{idVendor}=="1d4d", MODE="0664", GROUP="plugdev"
    #Philips
    SUBSYSTEM=="usb", ATTR{idVendor}=="0471", MODE="0664", GROUP="plugdev"
    #PMC-Sierra
    SUBSYSTEM=="usb", ATTR{idVendor}=="04da", MODE="0664", GROUP="plugdev"
    #Qualcomm
    SUBSYSTEM=="usb", ATTR{idVendor}=="05c6", MODE="0664", GROUP="plugdev"
    #SK Telesys
    SUBSYSTEM=="usb", ATTR{idVendor}=="1f53", MODE="0664", GROUP="plugdev"
    #Samsung
    SUBSYSTEM=="usb", ATTR{idVendor}=="04e8", MODE="0664", GROUP="plugdev"
    #Sharp
    SUBSYSTEM=="usb", ATTR{idVendor}=="04dd", MODE="0664", GROUP="plugdev"
    #Sony
    SUBSYSTEM=="usb", ATTR{idVendor}=="054c", MODE="0664", GROUP="plugdev"
    #Sony Ericsson
    SUBSYSTEM=="usb", ATTR{idVendor}=="0fce", MODE="0664", GROUP="plugdev"
    #Teleepoch
    SUBSYSTEM=="usb", ATTR{idVendor}=="2340", MODE="0664", GROUP="plugdev"
    #Toshiba
    SUBSYSTEM=="usb", ATTR{idVendor}=="0930", MODE="0664", GROUP="plugdev"
    #ZTE
    SUBSYSTEM=="usb", ATTR{idVendor}=="19d2", MODE="0664", GROUP="plugdev"
    ```
    </details>

## Troubleshooting

1. Make sure your device is connected and accessible via usb. `lsusb` should show a list of connected devices. The section after ‘ID’ in the output should match one of the `idVendor` numbers from the udev rules. For example, a Nexus One with idVendor `18d1` should return something like:
    <details>
      <summary>Sample output</summary>

    ```bash
    Bus 001 Device 005: ID 17ef:480d Lenovo Integrated Webcam [R5U877]
    Bus 002 Device 002: ID 0bda:0119 Realtek Semiconductor Corp.
    Bus 002 Device 009: ID 18d1:4e12 Google Inc. Nexus One (debug)
    Bus 004 Device 003: ID 0a5c:2145 Broadcom Corp. Bluetooth with Enhanced Data Rate II
    Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
    Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
    ```
    </details>

2. If the device is detected in `lsusb`, try running `adb devices`. If you get `???????????? device`, try [reloading the udev rules](http://askubuntu.com/questions/82470/what-is-the-correct-way-to-restart-udev-in-ubuntu): `sudo sh -c "(udevadm control --reload-rules && udevadm trigger --action=change)"` You can also try disconnecting and reconnecting the usb cable to your device.

3. If you cannot access your device via adb, even after adding your linux user to the plugdev group and restarting the computer, you can try starting the `adb` service as root. This is dangerous and not recommended: `adb kill-server && sudo $(which adb) start-server && adb devices`. Similarly, if `fastboot devices` returns `no permissions`, try running `fastboot` as root: `sudo $(which fastboot) devices`