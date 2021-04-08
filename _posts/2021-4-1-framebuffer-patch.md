---
layout: post
title: Patch framebuffer cho iGPU
---

Danh sách AAPL,ig-platform-id cho Desktop và Laptop

#### Desktop:
1. Haswell
- iGPU: **0300220D** (SMBIOS: **iMac14,4**)
- iGPU + dGPU: **04001204** (SMBIOS: **iMac15,1**)



2. Broadwell
- Default: **07002216** (SMBIOS: **iMac16,2**)



3. Skylake
- iGPU: **00001219** (SMBIOS: **iMac17,1**)
- iGPU + dGPU: **01001219** (SMBIOS: **iMac17,1**)
  - Lưu ý: P530 phải fake id với **device-id** = **1B190000**



4. Kabylake
- iGPU: **00001259** (SMBIOS: **iMac18,1**)
- iGPU + dGPU: **03001259** (SMBIOS: **iMac18,3**)



5. Coffeelake
- iGPU: **07009B3E**
- iGPU + dGPU: **0300913E**
  - SMBIOS:
    - **iMac19,1** nếu chạy Mojave, Catalina, Big Sur.
    - **iMac18,3** nếu chạy High Sierra.
  - Lưu ý: Nếu gặp màn hình đen với iGPU, hãy thử giá trị **00009B3E**.



6. Cometlake
- iGPU: **07009B3E**
- iGPU + dGPU: **0300C89B**
  - SMBIOS:
    - **iMac20,1** cho Core i3, i5, i7.
    - **iMac20,2** cho Core i9.
  - Lưu ý: Nếu gặp màn hình đen với iGPU, hãy thử giá trị **00009B3E**.



#### Laptop:

1. HD4200_4400_4600
  - AAPL,ig-platform-id: **0600260A**
  - device-id: **12040000**
  - SMBIOS: **MacBookPro11,1**



2. HD5000_5100_5200
  - AAPL,ig-platform-id: **0600260A**
  - device-id: N/A
  - SMBIOS: **MacBookPro11,1**



3. HD5300_5500_6000
  - AAPL,ig-platform-id: **06002616**
  - device-id: N/A
  - SMBIOS: **MacBookPro12,1**



4. HD5600
  - AAPL,ig-platform-id: **06002616**
  - device-id: **26160000**
  - SMBIOS: **MacBookPro12,1**



5. HD510
  - AAPL,ig-platform-id: **00001B19**
  - device-id: **02190000**
  - SMBIOS: **MacBookPro13,2**



6. HD515_520_530_540
  - AAPL,ig-platform-id: **00001B19**
  - device-id: N/A
  - SMBIOS: **MacBookPro13,2**



7. HD550_P530
  - AAPL,ig-platform-id: **00002619**
  - device-id: **26190000**
  - SMBIOS: **MacBookPro13,2**



8. HD615_620_630_640_650
  - AAPL,ig-platform-id: **00001B59**
  - device-id: N/A
  - SMBIOS: **MacBookPro14,1**



9. UHD617
  - AAPL,ig-platform-id: 0000C087
  - device-id:
  - SMBIOS: **MacBookPro14,2**



10. UHD620 (Kabylake Refresh)
  - AAPL,ig-platform-id: **0000C087**
  - device-id: **16590000**
  - SMBIOS: **MacBookPro14,2**



11. UHD620 (Whiskeylake)
  - AAPL,ig-platform-id: **0900A53E**
  - device-id: **A53E0000**
  - SMBIOS: **MacBookPro15,2**



12. UHD630 (Cometlake)
  - AAPL,ig-platform-id: 00009B3E
  - device-id: **9B3E0000**
  - SMBIOS: **MacBookPro16,3**



13. UHD630
  - AAPL,ig-platform-id: **00009B3E**
  - device-id: N/A
  - SMBIOS:
      - **MacBookPro15,1** (Coffeelake Gen 8th)
      - **MacBookPro16,4** (Coffeelake Gen 9th)
      - **MacBookPro16,1** (Cometlake)



14. G1_G4_G7
  - AAPL,ig-platform-id: **0000528A**
  - device-id: **528A0000**
  - SMBIOS: **MacBookAir9,1**



#### Patch phổ thông:
- framebuffer-patch-enable = 01000000
- framebuffer-stolenmem = 00003001
- framebuffer-fbmem = 00009000
- framebuffer-unifiedmem = 00000080
- hda-gfx = onboard-1
- enable-hdmi20 = 01000000
- ...



- Lưu ý:
  - Một số iGPU cần phải fake id mới có thể hoạt động được.
  - Nếu máy bạn chỉ sử dụng iGPU, và không thể set hoặc không có share memory trong BIOS, bắt buộc phải thêm **framebuffer-patch-enable** và **framebuffer-stolenmem** với desktop; **framebuffer-patch-enable**, **framebuffer-fbmem** và **framebuffer-stolenmem** với laptop (hoặc **framebuffer-cursormem** với một số model Haswell laptop).
  - Ở một số mẫu bo mạch chủ, share memory cho iGPU được hiển thị dưới dạng tên khác nhau:
    - Gigabyte: DVMT Pre-Allocated
    - Asus: DVMT Pre-Allocated
    - MSI: DVMT Pre-Allocated
    - Asrock: Share Memory
- Mẹo:
  - Nếu CPU desktop không có iGPU, nghĩa là thuộc dòng F series, và bạn có một con card VGA AMD khoẻ như là RX 580, hãy thiết lập SMBIOS như sau:
    - iMacPro1,1: Cho CPU Skylake, Kabylake.
    - MacPro7,1: Cho CPU Coffeelake, Cometlake 
      - MacPro7,1 hoạt động khá ổn với CPU của AMD.