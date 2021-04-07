---
layout: post
title: Patch framebuffer cho iGPU
---

Bảng AAPL,ig-platform-id:

#### Desktop:

| Thế hệ CPU | Card onboard iGPU only | Cả iGPU + dGPU |                        SMBIOS                        |                             Note                             |
| :--------: | :--------------------: | :------------: | :--------------------------------------------------: | :----------------------------------------------------------: |
|  Haswell   |        0300220D        |    04001204    |      - iMac14,4 (iGPU) - iMac15,1 (iGPU + dGPU)      |                                                              |
| Broadwell  |        07002216        |                |                  - iMac16,2 (iGPU)                   |                                                              |
|  Skylake   |        00001219        |    01001219    |                      - iMac17,1                      |      P530 phải fake id với **device-id** = **1B190000**      |
|  Kabylake  |        00001259        |    03001259    |      - iMac18,1 (iGPU) - iMac18,3 (iGPU + dGPU)      |                                                              |
| Coffeelake |        07009B3E        |    0300913E    | - iMac19,1 (Mojave trở lên) - iMac18,3 (High Sierra) | Nếu gặp màn hình đen với giá trị **07009B3E**, hãy thử thay thế với **00009B3E**. |
| Cometlake  |        07009B3E        |    0300C89B    |       - iMac20,1 (i3, i5, i7) - iMac20,2 (i9)        | Nếu gặp màn hình đen với giá trị **07009B3E**, hãy thử thay thế với **00009B3E**. |

#### Laptop:

|        HD Graphics        | AAPL,ig-platform-id |                            SMBIOS                            |                       Note                        |
| :-----------------------: | :-----------------: | :----------------------------------------------------------: | :-----------------------------------------------: |
|     HD4200_4400_4600      |      0600260A       |                        MacBookPro11,1                        | Cần phải fake id với **device-id** = **12040000** |
|     HD5000_5100_5200      |      0600260A       |                        MacBookPro11,1                        |                                                   |
|     HD5300_5500_6000      |      06002616       |                        MacBookPro12,1                        |                                                   |
|          HD5600           |      06002616       |                        MacBookPro12,1                        | Cần phải fake id với **device-id** = **26160000** |
|           HD510           |      00001B19       |                        MacBookPro13,2                        | Cần phải fake id với **device-id** = **02190000** |
|     HD515_520_530_540     |      00001B19       |                        MacBookPro13,2                        |                                                   |
|        HD550_P530         |      00002619       |                        MacBookPro13,2                        | Cần phải fake id với **device-id** = **26190000** |
|   HD615_620_630_640_650   |      00001B59       |                        MacBookPro14,1                        |                                                   |
|          UHD617           |      0000C087       |                        MacBookPro14,2                        |                                                   |
| UHD620 (Kabylake Refresh) |      0000C087       |                        MacBookPro14,2                        | Cần phải fake id với **device-id** = **16590000** |
|   UHD620 (Whiskeylake)    |      0900A53E       |                        MacBookPro15,2                        | Cần phải fake id với **device-id** = **A53E0000** |
|    UHD620 (Cometlake)     |      00009B3E       |                        MacBookPro16,3                        | Cần phải fake id với **device-id** = **9B3E0000** |
|          UHD630           |      00009B3E       | - MacBookPro15,1 (Coffeelake Gen 8th)<br>- MacBookPro16,4 (Coffeelake Gen 9th)<br>- MacBookPro16,1 (Cometlake) |                                                   |
|         G1_G4_G7          |      0000528A       |                        MacBookAir9,1                         | Cần phải fake id với **device-id** = **528A0000** |

- Patch phổ thông:

  |           Key            | Type |  Value   |
  | :----------------------: | :--: | :------: |
  |   AAPL,ig-platform-id    | Data |  xxxxxx  |
  |        device-id         | Data |  zzzzzz  |
  | framebuffer-patch-enable | Data | 01000000 |
  |  framebuffer-stolenmem   | Data | 00003001 |
  |    framebuffer-fbmem     | Data | 00009000 |

- Lưu ý:
  - Một số iGPU cần phải fake id mới có thể hoạt động được.
  - Nếu máy bạn chỉ sử dụng iGPU, và không thể set hoặc không có share memory trong BIOS, bắt buộc phải thêm **framebuffer-patch-enable** và **framebuffer-stolenmem** với desktop; **framebuffer-patch-enable**, framebuffer-fbmem và **framebuffer-stolenmem** với laptop (hoặc framebuffer-cursormem với một số model Haswell laptop).
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