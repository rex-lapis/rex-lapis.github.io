---
layout: post
title: Fix màn hình ám tím (Force RGB)
---

Màn hình ám tím (hay còn được gọi là pink screen), là một lỗi rất hay gặp với macOS khi connect với màn hình ngoài. Lúc đó macOS sẽ nghĩ đó là màn hình TV ngoài, và sẽ sử dụng dải màu **YCbCr** thay vì **RGB**. Một số màn hình sẽ chỉ có RGB nên khi cài xong macOS sẽ bị ám tím ngay lập tức. Vì vậy lúc này chúng ta cần phải Force dải màu RGB cho nó.

1. Download file này tại [đây](https://gist.github.com/adaugherity/7435890).

2. Mở Terminal lên. Sau đó kéo thả file vừa tải về vào trong Terminal

   ![rgb1](/images/rgb1.png)

3. Nhấn Enter. Nếu có nó yêu cầu nhập password, cứ nhập pass như bình thường. Sau đó sẽ được như thế này

   ![rgb2](/images/rgb2.png)

4. Để ý giúp mình dòng **Output file**, hãy mon men đúng theo đường dẫn đó

   ![rgb3](/images/rgb3.png)

   Ở đây, mình đã có được file DisplayVendorID của màn hình đang bị ám tím.

5. Kế đến, hãy vào theo đường dẫn **/Library/Displays/Contents/Resources**. Nếu như bạn không có các thư mục tương ứng, hãy thoải mái tạo chúng trong thư mục **Library**. Trong thư mục **Resources**, tạo tiếp folder tên **Overrides**.

6. Bỏ thư mục DisplayVendor đã tạo ở bước trước vào trong thư mục **Overrides**. Nếu chính xác, sẽ được như ảnh dưới

   ![rgb4](/images/rgb4.png)

7. Restart lại máy là xong

   Lưu ý: Cách làm này áp dụng cho macOS Big Sur. Đối với các phiên bản macOS khác, các bạn có thể mount phân vùng **System** (có thể sử dụng Hackintool để mount), sau đó vẫn vào lần lượt các folder theo thứ tự **/Library/Displays/Contents/Resources/Overrides** và bỏ file DisplayVendorID vô đó là được