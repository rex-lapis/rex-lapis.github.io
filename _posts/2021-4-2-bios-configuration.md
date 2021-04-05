---
layout: post
title: Thiết lập BIOS
---

Một số option có thể sẽ không xuất hiện trong BIOS máy bạn. Mình khuyến khích nên setting những option gần sát với danh sách, đừng quá phân vân nếu các option không có trong đó.

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

### Dành cho ai sử dụng GPU

- Peripherals → Initial Display Output : PCIe 1 Slot
- Chipset → Integrated Graphics : Disabled

### Dành cho ai sử dụng IGPU

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

### Dành cho ai sử dụng DGPU

- Advanced \ Chipset Configuration → Primary Graphics Adapter : PCI Express
- Advanced \ Chipset Configuration → IGPU Multi-Monitor : Disabled

### Dành cho ai sử dụng IGPU

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

### Dành cho ai sử dụng DGPU

- Advanced \ System Agent (SA) Configuration \ Graphics Configuration → Primary Display: PEG

### Dành cho ai sử dụng IGPU

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

### Dành cho ai sử dụng DGPU

- Settings \ Advanced \ Integrated Graphics Configuration → Initiate Graphic Adapter : PEG

### Dành cho ai sử dụng IGPU

- Advanced \ Integrated Graphics Configuration → Initiate Graphic Adapter : IGD

# 2. Laptop

### **Disable**

- Fast Boot
- Secure Boot
- Serial/COM Port
- Parallel Port
- VT-d (nếu trong BIOS máy không có, vui lòng set `DisableIoMapper` là YES trong config.plist)
- CSM
- Thunderbolt
- Intel SGX
- Intel Platform Trust
- CFG Lock (MSR 0xE2 write protection)(**Nếu bạn không tìm thấy nó trong BIOS, vui lòng enable `AppleXcpmCfgLock` trong section Kernel -> Quirks với OpenCore. (Clover là `KernelXcpm`). Nếu không sẽ không Boot được vào macOS**).

### **Enable**

- VT-x (Virtualization)
- Above 4G decoding
- Hyper-Threading
- Execute Disable Bit
- EHCI/XHCI Hand-off
- OS type: Windows 8.1/10 UEFI Mode
- DVMT Pre-Allocated(iGPU Memory): 64MB
- SATA Mode: AHCI

# 3. AMD System

### **Disable**

- Fast Boot
- Secure Boot
- Serial/COM Port
- Parallel Port
- Compatibility Support Module (CSM)(**Phải disable, nếu không sẽ gặp lỗi `gIO`**).

**Lưu ý đặc biệt cho 3990X**: Hãy tắt Hyper Threading trong BIOS!

### **Enable**

- Above 4G decoding(**Nên bật option này. Nếu không có trong BIOS, hãy thêm `npci=0x2000` vào boot-args. Đừng bật và thêm boot-arg cùng một lúc**).
    - Một số mainboard của Gigabyte/Aorus hay AsRock, khi bật option này sẽ có thể break một số driver (ie. Ethernet) và không boot được sang các hệ điều hành khác. Nếu bạn gặp hãy sử dụng boot-arg để thay thế.
- EHCI/XHCI Hand-off
- OS type: Windows 8.1/10 UEFI Mode
- SATA Mode: AHCI

### Nguồn tham khảo:
- VNO Hackintosh
- Dortania Guide