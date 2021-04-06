---
layout: post
title: Trang trí OpenCanopy
---

![canopy-minimal](/images/canopy-minimal.png)

## CHUẨN BỊ:

- OcBinaryData: [Download](https://github.com/acidanthera/OcBinaryData)

- OpenCanopy.efi (đi kèm với OpenCore)
  Note: OpenCanopy phải đi kèm đúng với phiên bản OpenCore.

## THIẾT LẬP

- Bỏ OpenCanopy.efi vào thư mục **EFI/OC/Drivers**.

- Copy thư mục **Resources** đã giải nén từ OcBinaryData và bỏ vô **EFI/OC**.
    Nếu như làm đúng thì sẽ được như hình dưới.

  ![oc-resource](/images/oc-resource.png)

- Setting **config.plist**:

  ![canopy-config](/images/canopy-config.png)

  - Mở config.plist, tìm đến:

    - Misc -> Boot -> PickerMode: Set là External

    - Misc -> Boot -> PickerAttributes: Set là 1, nếu ai mà muốn bật con trỏ chuột thì set là 17.

    - Misc -> Boot -> PickerVariant:

      - Auto: Tự động set icon

      - Default: Bộ icon mặc định

      - Modern: Bộ icon "hiện đại" (theo macOS Big Sur)

      - Old: Bộ icon "vintage"

        Note: Tất cả các value cho PickerVariant sẽ dựa theo TÊN bộ icon có bên trong thư mục Resources/Image

    - UEFI -> Drivers: Thêm OpenCanopy.efi, hoặc snapshot lại config.plist
    
    Credit: https://dortania.github.io/OpenCore.../cosmetic/gui.html

## THÊM BACKGROUND

  Note: Chỉ dành cho OC 0.6.6 trở đi

- CHUẨN BỊ:

  - Với màn hình **Full HD**, lấy ảnh độ phân giải **4K**.

  - Với màn hình **2K**, lấy ảnh độ phân giải **5K**.

    Note: Tất cả hình ảnh phải để đuôi .png

- CONVERT ẢNH .PNG SANG .ICNS

  - Tải app builder về tại [đây](https://github.com/chris1111/OpenCanopy-Generator).

  - Bỏ ảnh đã chuẩn bị vô, xong app sẽ tự convert sang đuôi .icns

  - Khi được ảnh mới, đổi tên file, ví dụ **Background.icns** (bắt buộc).

    Note: Việc đặt tên sẽ dựa theo **PickerVariant** trong config.plist, ví dụ nếu để Auto/Default nó sẽ load bộ icon mặc định, nghĩa là **Background.icns** sẽ được load cùng và sẽ có background khi hiển thị boot. Nếu PickerVariant là **Modern** thì name phải đặt là **ModernBackground.icns**. Tương tự với PickerVariant là Old.

  - Bỏ file background đã đổi tên vào thư mục EFI/OC/Resources/Image.

  - Khởi động lại máy là done.