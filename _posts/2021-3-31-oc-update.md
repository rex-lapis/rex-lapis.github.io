---
layout: post
title: Cập nhật OpenCore lên phiên bản mới
---

Việc update OpenCore cũng khá dễ dàng, nhưng bù lại thì việc này phải làm thủ công, và gần như là làm mới lại EFI. Khuyến nghị mọi người nếu muốn update OpenCore hãy thực sự rảnh tay để update, tránh sai sót dẫn đến không thể boot được vào macOS nữa.

- Các bước thực hiện update OpenCore như sau:

1. Tải phiên bản OpenCore mới tại [đây](https://github.com/acidanthera/OpenCorePkg/releases).

2. Chuẩn bị sẵn một USB, chỉ cần 4GB là đủ, và format nó với định dạng Mac OS Extended (Journaled). Nhớ phải đặt Scheme là GUID Partition Map.

   Mục đích của việc này là khi đã làm xong EFI OpenCore phiên bản mới, hãy boot vào macOS thử thông qua USB trước, giống như việc bạn làm khi cài đặt xong macOS. Nếu mọi thứ thuận lợi và không xảy ra lỗi gì, lúc đó hãy copy folder EFI từ USB vào phân vùng trên ổ SSD.

3. Thay thế ba tập tin quan trọng sau:

   - EFI/BOOT/**BOOTx64.efi**
   - EFI/OC/**OpenCore.efi**
   - EFI/OC/Drivers/**OpenRuntime**

   Lưu ý: Bắt buộc thay thế ba tập tin này nếu muốn update OpenCore.

   ![efinew](/images/efinew.png)

4. Tiếp đến, trong folder OpenCore vừa tải ở trên, tìm đến /Docs/**Sample.plist**, copy nó vào folder EFI ở ảnh trên, đổi tên thành **config.plist**.
   - Copy tiếp SSDT từ folder EFI hiện tại đang dùng bỏ vào EFI/OC/**ACPI**.
   - Copy tiếp các kexts đang có bỏ vào EFI/OC/**Kexts**.
   - Trong thư mục Drivers, xoá hết các drivers không cần thiết, chừa lại **OpenRuntime.efi** (bắt buộc) và OpenCanopy.efi (nếu đang sử dụng OpenCore Picker theme).
   - Trong thư mục Tools, xoá hết các tools có trong đó. Chưa cần dùng đến nó thì nó thực sự không cần thiết.

5. Khi chắc chắn mọi thứ đã hoàn thành, sử dụng **ProperTree** để tiến hành snapshot folder **OC** cho **config.plist**, sau đó tiến hành configure lại toàn bộ theo như file config.plist cũ. Mình khuyến nghị nên mở thêm cả guide trên Dortania để check thêm, vì mỗi khi có phiên bản mới, một số property sẽ được thêm vào, chúng có thể làm các bạn cảm thấy bối rối.

6. Khi mọi thứ hoàn thành, nhớ save file **config.plist** lại. Sau đó bỏ vào phân vùng EFI trên USB, restart lại và boot thử. Xác nhận lại toàn bộ hệ thống, nếu không có trục trặc gì thì chúc mừng, bạn đã update thành công phiên bản mới của OpenCore. Lúc này, có thể bỏ thư mục EFI ban nãy vào phân vùng EFI trên SSD và thay thế thư mục EFI cũ.

- Lưu ý:
  - OpenCore phiên bản mới sẽ được release vào tầm khoảng đêm ngày Thứ Hai thứ 2 của mỗi tháng (cũng có thể release sớm hơn một tuần, cái này tuỳ vào team Acidanthera).
  - Khi có phiên bản mới, một số kext khác cũng sẽ được update phiên bản mới. Hãy nhớ tải chúng về.
  - Mình rất khuyến khích mọi người nên tự tay làm thủ công toàn bộ EFI mới, sau đó hãy bỏ vào USB và boot thử trước, bởi lúc đó sẽ xác nhận EFI có bị lỗi hay gặp trục trặc gì không. Lý do là có một số kext ở nguồn bên ngoài, ví dụ như **VoodooI2C**, rất hay gặp lỗi dạo gần đây với macOS Big Sur hay OpenCore. Cái này mình không thể chắc chắn được nguyên do là gì. Vậy nên, hãy thử với USB trước, nếu đã ổn, bỏ vào SSD sau!