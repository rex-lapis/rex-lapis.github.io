---
layout: post
title: Hardware Compatibility
---

List of hardware is supported by macOS.

## CPU
### Intel CPU

- Nehalem
- Lynnfield, Clarksfield **(No iGPU support 10.14+)**
- Westmere, Clarkdale, Arrandale **(No iGPU support 10.14+)**
- Sandy Bridge **(No iGPU support 10.14+)**
- Ivy Bridge **(No iGPU support 11+)**
- Haswell
- Boardwell
- Skylake
- Kabylake
- Coffeelake
- Amberlake, Whiskeylake
- Cometlake
- Icelake

### AMD CPU

- Bulldozer (15h)
- Jaguar (16h)
- Ryzen (17h)
- Threadripper (19h)

## GPU

### Intel iGPU

- 3rd Gen GMA
- 4nd Gen GMA
- Arrandale (HD Graphics 1st Gen)
- Sandy Bridge HD3000
- Ivy Bridge HD4000
- Haswell HD4xxx, 5xxx
- Broadwell HD5xxx, 6xxx
- Skylake HD5xx
- Kabylake HD6xx
- Coffeelake UHD6xx
- Icelake Gx

Note: Please check [here](https://github.com/acidanthera/WhateverGreen/blob/master/Manual/FAQ.IntelHD.en.md) for more infomations.

### About dGPU, please check the details here:

- NVIDIA GPU: [https://dortania.github.io/GPU-Buyers-Guide/modern-gpus/nvidia-gpu.html](https://dortania.github.io/GPU-Buyers-Guide/modern-gpus/nvidia-gpu.html)
- AMD GPU: [https://dortania.github.io/GPU-Buyers-Guide/modern-gpus/amd-gpu.html](https://dortania.github.io/GPU-Buyers-Guide/modern-gpus/amd-gpu.html)

## Motherboard

- For the most part, all motherboards are supported as long as the CPU is.
- Tip: If you are planning to buy a new PC or upgrade your current motherboard, I recommend let buy a mobo from Gigabyte or Asrock.

## Storage

For the most part, all SATA based drives are supported and the majority of NVMe drives as well. There are only a few exceptions:

- **Samsung PM981, PM991 and Micron 2200S NVMe SSDs**
    - These SSDs are not compatible out of the box (causing kernel panics) and therefore require **[NVMeFix.kext](https://github.com/acidanthera/NVMeFix/releases)** to fix these kernel panics. Note that these drives may still cause boot issues even with NVMeFix.kext.
    - On a related note, **Samsung 970 EVO Plus NVMe SSDs** also had the same problem but it was fixed in a latest firmware update (using **Samsung Magician** on **Windows**).
    - Also to note, laptops that use **Intel Optane Memory** or **Micron 3D XPoint** for HDD acceleration are **unsupported** in macOS.

## Ethernet

Virtually all wired network adapters have some form of support in macOS, either by the built-in drivers or community made kexts. The main exceptions:

- Intel's 2.5GBe i225 networking
    - Found on high-end Desktop Comet Lake boards
    - Workarounds are possible: **[Source](https://www.hackintosh-forum.de/forum/thread/48568-i9-10900k-gigabyte-z490-vision-d-er-l%C3%A4uft/?postID=606059#post606059)** and **[Example](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#deviceproperties)**
- Intel's server NICs
    - Workarounds are possible for **[X520 and X540 chipsets](https://www.tonymacx86.com/threads/how-to-build-your-own-imac-pro-successful-build-extended-guide.229353/)**
- Mellanox and Qlogic server NICs

## Wireless

- PCIe
    - **BCM94360CD** (ABGN+AC):
        - Fenvi FV T919 (Bluetooth 4.0)
        - Fenvi AC1900 (No Bluetooth, EOL)
        - TP-LINK Archer T9E AC1900 (No Bluetooth, EOL)
        - TP-LINK Archer T8E (No Bluetooth)
        - RNX-AC1900PCE (No Bluetooth)
        - ASUS PCE-AC66 (No Bluetooth)
        - ASUS PCE-AC68 (No Bluetooth)
    - **BCM94360CS2** (ABGN+AC):
        - Fenvi FV-HB1200 (Bluetooth 4.0)
        - AWD Wireless LAN Card (No Bluetooth)
    - **BCM94352** (ABGN+AC):
        - TP-LINK Archer T6 (No Bluetooth)
        - Rosewill RNX-AC1300PCE (No Bluetooth)
        - ASUS PCE-AC56 (No Bluetooth)
    - Note:
        - All PCIe cards above are supported in latest Big Sur
        - All cards presented here besides the Apple Airport and Fenvi cards require the following:
            - **[AirportBrcmFixup](https://github.com/acidanthera/AirportBrcmFixup/releases)**
            - **[BrcmPatchRAM](https://github.com/acidanthera/BrcmPatchRAM/releases)**
                - BrcmBluetoothInjector
                - BrcmFirmwareData
                - BrcmPatchRAM fix:
                    - BrcmPatchRAM3 for 10.14+ (must be paired with BrcmBluetoothInjector)
                    - BrcmPatchRAM2 for 10.11-10.14
                    - BrcmPatchRAM for 10.10 or older
- Mini PCIe
    - **BCM94360HMB** (ABGN+AC, BT 4.0, 3x3:3):
        - AzureWave AW-CB160H
        - Alpha Networks WMC-AC01
        - Arcadyan WN8833B-AC
        - Gemtek WMDB-150AC
        - Unex DAXB-81
        - Wistron NeWeb DNXB-C1
    - **BCM94352HMB** (ABGN+AC, BT 4.0, 2x2:2):
        - AzureWave AW-CE123H
        - Dell DW1550
        - HP TPC-Q013
        - Lenovo Lite-On WCBN606BH
    - Note:
        - All PCIe cards above are supported in latest Big Sur
        - All cards presented here require the following:
            - **[AirportBrcmFixup](https://github.com/acidanthera/AirportBrcmFixup/releases)**
            - **[BrcmPatchRAM](https://github.com/acidanthera/BrcmPatchRAM/releases)**
                - BrcmBluetoothInjector
                - BrcmFirmwareData
                - BrcmPatchRAM fix:
                    - BrcmPatchRAM3 for 10.14+ (must be paired with BrcmBluetoothInjector)
                    - BrcmPatchRAM2 for 10.11-10.14
                    - BrcmPatchRAM for 10.10 or older
- M.2

    The other thing to keep in mind is that M.2 wireless cards come in 2 variant:

    - A Key
    - E Key

    ![Hardware%20Compatibility%20bb3585ebb10e47e5bf47d4422f391c46/Untitled.png](/images/wifi-m2.png)

    - **BCM94360NG**:
        - Fenvi BCM94360NG(A+E Key, natively supported as based off of genuine Apple Airport card)(BT 4.0)
    - **BCM943602**:
        - Dell DW1830 (A+E Key, quite wide so make sure your laptop has room)(BT 4.1)
    - **BCM94352Z**:
        - Fenvi AC1200 (A+E Key, natively supported as based off of genuine Apple Airport card)(BT 4.0)
        - Dell DW1560 (A+E Key)(BT 4.0)
        - Lenovo Lite-On WCBN802B(04X6020)(E Key)(BT 4.0)
        - AzureWave AW-CB162NF(A+E Key)(BT 4.0)
    - **BCM94350ZAE**:
        - Lenovo Foxconn T77H649(A+E Key)(BT 4.1)
        - Lite-On WCBN808B(A+E Key)(BT 4.1)
        - Dell DW1820A (A+E Key)(BT 4.1)
    - Note:
        - All PCIe cards above are supported in latest Big Sur
        - All cards presented here require the following:
            - **[AirportBrcmFixup](https://github.com/acidanthera/AirportBrcmFixup/releases)**
            - **[BrcmPatchRAM](https://github.com/acidanthera/BrcmPatchRAM/releases)**
                - BrcmBluetoothInjector
                - BrcmFirmwareData
                - BrcmPatchRAM fix:
                    - BrcmPatchRAM3 for 10.14+ (must be paired with BrcmBluetoothInjector)
                    - BrcmPatchRAM2 for 10.11-10.14
                    - BrcmPatchRAM for 10.10 or older

    Attention: The BCM94350ZAE chipset doesn't support power management correctly in macOS so needs to be disabled via property injection:

    ```cpp
    pci-aspm-default | Data | <00>
    ```

    Also I don't recommend to use this card. It has some issues with Bluetooth (Wifi sometimes).

- USB
    - **RTL8188CUS**:
        - Asus USB-N 10 Nano/N150
        - TRENDnet N150 Micro
    - **RTL8192CU**:
        - EDIMAX- EW-7722UTn V2
        - EDIMAX N300
    - **RTL8192EU**:
        - TL-WN823N v2
        - TL-WN823N v3
        - TL-WN821N v6
    - **RTL8188EUS**:
        - TL-WN725N v3
        - TL-WN722N v3
    - **RTL8811AU**:
        - Archer T2U NANO
    - **RTL8812BU**:
        - Archer T4U V3
    - **RTL8814AU**:
        - Archer T9UH V2
    - **RTL8812AU**:
        - Linksys WUSB6300

    and many more.

    **Recommend**: If you are planning to buy an USB Wi-Fi, the COMFAST CF-811AC is a good choice.

    Driver: [chris1111](https://github.com/chris1111/Wireless-USB-Big-Sur-Adapter) (Big Sur only. For other macOS versions, you can check his repo)

- Intel
    - Intel wireless card now can be used on macOS. It is a good choice to replace USB Wi-Fi.
    - It is enough to use, but can't be a replacement of native supported Broadcom Cards.
    - For more information, check the compatible list [here](https://openintelwireless.github.io/itlwm/Compat.html#compatibility).
