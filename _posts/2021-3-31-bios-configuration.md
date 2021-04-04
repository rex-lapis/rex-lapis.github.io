---
layout: post
title: BIOS Configuration
---

Most of these options may not be present in your firmware, I recommend matching up as closely as possible but don't be too concerned if many of these options are not available in your BIOS.

# 1. Desktop

## **Gigabyte**

### General

- Save & Exit → Load Optimized Defaults
- M.I.T. → Advanced Memory Settings Extreme Memory Profile(X.M.P.) : Profile1
- BIOS → Fast Boot : Disabled
- BIOS → LAN PXE Boot Option ROM : Disabled
- BIOS → Storage Boot Option Control : UEFI
- Peripherals → Trusted Computing → Security Device Support : Disable
- Peripherals → Network Stack Configuration → Network Stack : Disabled
- Peripherals → USB Configuration → Legacy USB Support : Auto
- Peripherals → USB Configuration → XHCI Hand-off : Enabled
- Chipset → Vt-d : Disabled

### For user who is using **DGPU**

- Peripherals → Initial Display Output : PCIe 1 Slot
- Chipset → Integrated Graphics : Disabled

### For user who is using IGPU only

- Peripherals → Initial Display Output : IGFX
- Chipset → Integrated Graphics : Enabled
- Chipset → DVMT Pre-Allocated : 128MB

## **ASRock**

### General

- OC Tweaker \ DRAM Configuration → Load XMP Setting : XMP 2.0 Profile 1
- Advanced \ CPU Configuration → Intel Virtualization Technology : Enabled
- Advanced \ Chipset Configuration → Vt-d : Disabled
- Advanced \ Storage Configuration → Sata Mode Selection: AHCI
- Advanced \ Super IO Configuration → Serial Port: Disabled
- Advanced \ USB Configuration → Legacy USB Support : Enabled
- Advanced \ USB Configuration → PS/2 Simulator : Disabled
- Advanced \ USB Configuration → XHCI Hand-off : Enabled
- Security \ Secure Boot → Secure Boot: Disabled
- Boot → Fast Boot: Disabled
- Boot → Boot From Onboard LAN: Disabled

### For user who is using **DGPU**

- Advanced \ Chipset Configuration → Primary Graphics Adapter : PCI Express
- Advanced \ Chipset Configuration → IGPU Multi-Monitor : Disabled

### For user who is using I**GPU only**

- Advanced \ Chipset Configuration → Primary Graphics Adapter : Onboard
- Advanced \ Chipset Configuration → Share Memory : 128MB
- Advanced \ Chipset Configuration → IGPU Multi-Monitor : Enabled

## **ASUS**

### General

- Exit → Load Optimized Defaults : Yes
- Advanced \ CPU Configuration → Intel Virtualizaiton Technology: Enabled
- Advanced \ System Agent (SA) Configuration → Vt-d: Disabled
- Advanced \ PCH Configuration → IOAPIC 24-119 Entries: Enabled
- Advanced \ AMP Configuration → Power On By PCI-E/PCI: Enabled
- Advanced \ Network Stack Configuration → Network Stack: Disabled
- Advanced \ USB Configuration -> Legacy USB Support: Auto
- Boot → Fast Boot : Disabled
- Boot → Secure Boot → OS Type : Other OS

### For user who is using **DGPU**

- Advanced \ System Agent (SA) Configuration \ Graphics Configuration → Primary Display: PEG

### For user who is using I**GPU only**

- Advanced \ System Agent (SA) Configuration \ Graphics Configuration → Primary Display: IGFX
- Advanced \ System Agent (SA) Configuration \ Graphics Configuration → DVMT Pre-Allocated: 128MB

## **MSI**

### General

- Save & Exit → Restore Defaults : Yes
- Settings \ Advanced \ Integrated Peripherals → Network Stack : [Disabled]
- Settings \ Advanced \Integrated Peripherals → Intel Serial IO : [Disabled]
- Settings \ Advanced \ Integrated Graphics Configuration → DVMT Pre-Allocated : 128MB or 64MB
- Settings \ Advanced \ USB Configuration → XHCI Hand-off : [Enabled]
- Settings \ Advanced \ USB Configuration → Legacy USB Support : [Auto]
- Settings \ Advanced \ Windows OS Configuration → MSI Fast Boot : [Disabled]
- Settings \ Advanced \ Windows OS Configuration → Fast Boot : [Disabled]
- Overclocking → Extreme Memory Profile(X.M.P) : [Enabled]
- Overclocking \ CPU Features → Intel Virtualization Tech : [Enabled]
- Overclocking \ CPU Features → Intel VT-D Tech : [Disabled]
- Settings \ Boot → Boot mode select : [LEGACY+UEFI]

### For user who is using **DGPU**

- Settings \ Advanced \ Integrated Graphics Configuration → Initiate Graphic Adapter : PEG

### For user who is using I**GPU only**

- Advanced \ Integrated Graphics Configuration → Initiate Graphic Adapter : IGD

# 2. Laptop

### **Disable**

- Fast Boot
- Secure Boot
- Serial/COM Port
- Parallel Port
- VT-d (if your BIOS doesn't have, please set `DisableIoMapper` to YES in config.plist)
- CSM
- Thunderbolt(For initial install, as Thunderbolt can cause issues if not setup correctly)
- Intel SGX
- Intel Platform Trust
- CFG Lock (MSR 0xE2 write protection)(**This must be off, if you can't find the option then enable `AppleXcpmCfgLock` under Kernel -> Quirks if you are using OpenCore. (In Clover, it's KernelXcpm). Your hack will not boot with CFG-Lock enabled**)

### **Enable**

- VT-x (Virtualization)
- Above 4G decoding
- Hyper-Threading
- Execute Disable Bit
- EHCI/XHCI Hand-off
- OS type: Windows 8.1/10 UEFI Mode
- DVMT Pre-Allocated(iGPU Memory): 64MB
- SATA Mode: AHCI

> AMD System

### **Disable**

- Fast Boot
- Secure Boot
- Serial/COM Port
- Parallel Port
- Compatibility Support Module (CSM)(**Must be off, GPU errors like `gIO` are common when this option in enabled**)

**Special note for 3990X users**: macOS currently does not support more than 64 threads in the kernel, and so will kernel panic if it sees more. The 3990X CPU has 128 threads total and so requires half of that disabled. We recommend disabling hyper threading in the BIOS for these situations.

### **Enable**

- Above 4G decoding(**This must be on, if you can't find the option then add `npci=0x2000` to boot-args. Do not have both this option and npci enabled at the same time.**)
    - If you are on a Gigabyte/Aorus or an AsRock motherboard, enabling this option may break certain drivers(ie. Ethernet) and/or boot failures on other OSes, if it does happen then disable this option and opt for npci instead
- EHCI/XHCI Hand-off
- OS type: Windows 8.1/10 UEFI Mode
- SATA Mode: AHCI

