---
layout: post
title: Patch framebuffer cho iGPU
---

Bảng AAPL,ig-platform-id:

#### Desktop:

![dekstop](/images/framebuffer-desktop.png)

#### Laptop:

![laptop](/images/framebuffer-laptop.png)

- Patch phổ thông:

![generic](/images/generic-patch.png)

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