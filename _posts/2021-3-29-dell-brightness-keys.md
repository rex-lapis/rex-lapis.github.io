---
layout: post
title: Mapping phím chỉnh độ sáng cho laptop Dell
---

Với hầu hết laptop Dell, sau khi cài xong macOS, hai phím chỉnh độ sáng màn hình sẽ mặc định là Fn + B (giảm) và Fn + S (tăng) (nếu phím Fn được sử dụng với dạng function). Method BRT6 từ xa xưa được Rehabman tìm ra đã khắc phục được vấn đề này, đưa hai phím chỉnh sáng về đúng vị trí Fn + F11/F12, nhưng nó lại phải cần đến 2 rename đi kèm là _OSI và OSID, và yêu cầu phải sắp xếp đúng theo thứ tự thì nó mới nhận.

Hiện nay, với sự phát triển vượt bậc của Hackintosh, các nhà phát triển đã tìm ra được phương pháp tự động mapping phím chỉnh độ sáng bằng kext BrightnessKeys. Nhưng với một số mẫu laptop Dell mới hiện nay, sẽ xảy ra trường hợp mặc dù đã có kext nhưng hai phím chỉnh sáng vẫn không hoạt động. Sau đây sẽ là cách khắc phục

1. Check trong file DSDT gốc các **Device** và **Method** sau:

   - **Device** ECDV【PNP0C09】
   - **Device** LID0【PNP0C0D】
   - **Method** OSID
   - **Method** BTNV

   Nếu có **đầy đủ** cả 4, hãy đọc tiếp guide. Nếu không, hãy bỏ qua guide này và quay lại sử dụng Method BRT6.

2. Download file này tại [đây](https://cdn.discordapp.com/attachments/719556350161584179/830066699038359583/SSDT-DELL-SPECIAL.aml). Copy file và bỏ vô theo đường dẫn **/EFI/OC/ACPI**.

3. Download kext BrightnessKeys tại [đây](https://github.com/acidanthera/BrightnessKeys). Copy và bỏ vào theo đường dẫn **/EFI/OC/Kexts**.

4. Mở **config.plist**, snapshot lại OC để nó add thêm cái SSDT và kext BrightnessKeys vừa tải ở trên. Sau đấy phần **ACPI/Patch**, add rename ACPI sau:

   - Comment: **Change PNLF to XNLF**
   - Find: **504E4C46**
   - Replace: **584E4C46**

5. Restart lại máy là xong.

Nguồn: daliansky

