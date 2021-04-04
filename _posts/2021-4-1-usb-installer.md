---
layout: post
title: Creating USB Installer
---

Steps to create macOS USB installer.

### Choose macOS version which you want to install:

> Windows user

### Flash image file to the USB

- Download [balenaEtcher](https://www.balena.io/etcher/)

    ![Creating%20USB%20Installer%20ed93339978fe4194b19173fa69f4b9aa/Untitled.png](/images/usb9.png)

    - Flash from file: Select the macOS DMG file which is downloaded
    - Select target: Choose your USB device

    Then click Flash! to flash macOS image file to your USB.

### Mount EFI partition

- Download and install [MiniTool Partition Wizard](https://www.partitionwizard.com/free-partition-manager.html)

![Creating%20USB%20Installer%20ed93339978fe4194b19173fa69f4b9aa/Untitled%201.png](/images/usb1.png)

For example, my USB is Disk 3, which has EFI partition. If you flashed DMG file correctly, EFI partition will show in the list.

![Creating%20USB%20Installer%20ed93339978fe4194b19173fa69f4b9aa/Untitled%202.png](/images/usb2.png)

Next, right click EFI partition, choose Change Letter.

![Creating%20USB%20Installer%20ed93339978fe4194b19173fa69f4b9aa/Untitled%203.png](/images/usb3.png)

Choose any letter, for example I choose F. Then click OK.

![Creating%20USB%20Installer%20ed93339978fe4194b19173fa69f4b9aa/Untitled%204.png](/images/usb4.png)

You can see now the letter of EFI partition is F, but it's still pending. You have to click Apply button to finish.

Next, we will put the EFI bootloader folder to that EFI partition.

- Download [Explorer++](https://explorerplusplus.com/download)
    - Right click Explorer++, open it as Administrator

    Note: Every below steps have to do inside Explorer++

    - Find EFI folder which is prepared before, copy it
    - Go to the USB's EFI partition
    - Then paste

If correct, the EFI partition should be like this:

> macOS user

- Open Disk Utility

![Creating%20USB%20Installer%20ed93339978fe4194b19173fa69f4b9aa/Untitled%205.png](/images/usb6.png)

- On the left corner, choose View → Show All Devices

    ![Creating%20USB%20Installer%20ed93339978fe4194b19173fa69f4b9aa/Screen_Shot_2021-02-08_at_15.42.47.png](/images/usb0.png)

- You will see there are all devices connected to the machine

![Creating%20USB%20Installer%20ed93339978fe4194b19173fa69f4b9aa/Untitled%206.png](/images/usb6.png)

- Next choose your USB device, then select Erase

![Creating%20USB%20Installer%20ed93339978fe4194b19173fa69f4b9aa/Untitled%207.png](/images/usb7.png)

Edit the following things:

- Name: install_osx
- Format: Mac OS Extended (Journaled)
- Scheme: GUID Partition Map

Then click Erase.

- Open Terminal
- Type this command to Terminal:

```docker
diskutil list
```

- Now let find the USB path. For example, my USB is /dev/disk3

![Creating%20USB%20Installer%20ed93339978fe4194b19173fa69f4b9aa/Untitled%208.png](/images/usb8.png)

- Next, run this command to format your USB. Replace /dev/disk3 with your USB path, like /dev/disk2,...

```docker
diskutil partitionDisk /dev/disk3 1 GPT HFS+J "install_osx" R
```

- After that, run the following command to create the USB installer
    1. High Sierra

    ```docker
    sudo "/Applications/Install macOS High Sierra.app/Contents/Resources/createinstallmedia" --volume  /Volumes/install_osx --nointeraction
    ```

    2. Mojave

    ```docker
    sudo "/Applications/Install macOS Mojave.app/Contents/Resources/createinstallmedia" --volume  /Volumes/install_osx --nointeraction
    ```

    3. Catalina

    ```docker
    sudo "/Applications/Install macOS Catalina.app/Contents/Resources/createinstallmedia" --volume  /Volumes/install_osx --nointeraction
    ```

    4. Big Sur

    ```docker
    sudo "/Applications/Install macOS Big Sur.app/Contents/Resources/createinstallmedia" --volume  /Volumes/install_osx --nointeraction
    ```
