---
layout: post
title: Tạo bộ cài macOS online trên Windows
---

Ở thời điểm hiện tại, việc tạo bộ cài macOS trực tiếp trên USB đã dễ dàng hơn rất nhiều. Nó sẽ giúp bạn download được data của phiên bản OS một các sạch sẽ nhất từ trang chủ Apple về máy trong quá trình cài. Nhưng bên cạnh đó, do là bộ cài online, nên bạn phải chắc chắn một điều là máy được kết nối internet trong quá trình cài đặt. Đồng nghĩa là phải có kext cho mạng LAN, hoặc Wi-Fi.

- Để bắt đầu, bạn cần chuẩn bị các thứ sau:

1. Tải phiên bản OpenCore mới tại [đây](https://github.com/acidanthera/OpenCorePkg/releases).

2. Chuẩn bị sẵn một USB, chỉ cần 4GB là đủ, và format nó với định dạng **FAT32**.

   Với USB 16GB trở lên, hãy dùng **Rufus**. Chi tiết đọc ở dưới

3. Hãy chắc chắn rằng Windows đã được cài [Python](https://www.python.org/downloads/).

   Lưu ý: Bắt buộc thay thế ba tập tin này nếu muốn update OpenCore.

#### Tải macOS Recovery

1. Trong thư mục OpenCore vừa tải ở trên, tìm đến Utilities/macosrecovery

![macrecovery](/images/macrecovery.png)

2. Bấm chọn thư mục **macrecovery**, sau đó chọn **Copy path**.
3. Mở **Command Prompt** với quyền Admin, gõ **cd**, dấu cách, rồi chuột phải để paste path của folder **macrecovery** ở trên. Sau đó nhấn **Enter**.

![cmd](/images/cmd.png)

4. Khi đó trong cmd sẽ trỏ đến thư mục **macrecovery**. Tiếp đến, chọn phiên bản macOS bạn muốn tải theo danh sách sau:

   - High Sierra:

     - ```
       python macrecovery.py -b Mac-7BA5B2D9E42DDD94 -m 00000000000J80300 download
       ```

       ```
       python macrecovery.py -b Mac-BE088AF8C5EB4FA2 -m 00000000000J80300 download
       ```

   - Mojave:

     - ```
       python macrecovery.py -b Mac-7BA5B2DFE22DDD8C -m 00000000000KXPG00 download
       ```

   - Catalina:

     - ```
       python macrecovery.py -b Mac-00BE6ED71E35EB86 -m 00000000000000000 download
       ```

   - Big Sur:

     - ```
       python macrecovery.py -b Mac-E43C1C25D4880AD6 -m 00000000000000000 download
       ```

   Giả dụ ở đây mình chọn Big Sur. Khi đó, copy paste đoạn script của Big Sur và chuột phải vào cửa sổ Command Prompt, nó sẽ tự paste luôn giúp mình. Sau đó Enter. Quá trình tải sẽ bắt đầu.

   ![mac_download](/images/mac_download.png)

   

   Với Big Sur thì file recovery của nó chỉ khoảng hơn 600 MB. Nên mọi thứ diễn ra nhanh hay không thì tuỳ vào tốc độ mạng của bạn. Ở đây khi mình viết xong dòng này thì nó đã tải xong rồi...

   ![mac_finished](/images/mac_finished.png)

   

   Kiểm tra trong thư mục macrecovery, các bạn sẽ thấy có 2 files là **BaseSystem.chunklist** và **BaseSystem.dmg**. Một số phiên bản macOS khác sẽ hiện thị là **RecoveryImage.chunklist** và **RecoveryImage.dmg**.

   ![basesystem](/images/basesystem.png)

#### Tạo USB bộ cài macOS

- Cách 1: Sử dụng **Disk Management**

1. Chuột phải This PC, chọn Manage

![computer_management](/images/computer_management.png)

2. Chọn Disk Management, và nhìn vào USB của bạn. Ở đây USB của mình là 4 GB và đang có **một** phân vùng duy nhất là USB-BOOT.

   - Với những ai nếu USB hiện nhiều phân vùng, hãy chuột phải từng phân vùng và chọn Delete hết chúng đi

   ![usb](/images/usb.png)

3. Chuột phải vào phân vùng USB, chọn **Format**

![usb_format](/images/usb_format.png)

- Volume lable: **RECOVERY**

- File system: **FAT32**

- Allocation unit size: **Default**

  Sau đó click OK để format USB.

4. Tiếp đến vào phân vùng trên USB, tạo folder có tên là **com.apple.recovery.boot**.

![com_apple](/images/com_apple.png)

5. Trong thư mục **com.apple.recovery.boot**, hãy bỏ 2 files **BaseSystem.chunklist** và **BaseSystem.dmg** đã tải ở trên vào. Nếu đúng, sẽ giống như hình dưới.

![recovery_files](/images/recovery_files.png)

6. Quay lại ra bên ngoài, trong phân vùng USB, hãy bỏ tiếp thư mục bootloader **EFI** mà các bạn đã chuẩn bị để cho bộ cài macOS. Nếu đúng, trong USB sẽ chỉ có hai thư mục là **com.apple.recovery.boot** và **EFI**.

![usb_final](/images/usb_final.png)



- Cách 2: Sử dụng Rufus. Cách này sẽ dành cho ai đang có USB từ 32 GB trở lên. Hãy format USB đúng theo hình mẫu ở phía dưới.

![rufus](/images/rufus.png)

- Sau khi format xong, hãy làm theo từ bước tạo folder **com.apple.recovery.boot** là được.

#### Ưu điểm, nhược điểm

1. Ưu điểm

   - Bộ cài được download một cách sạch sẽ nhất từ trang chủ Apple.
   - Chỉ cần một chiếc USB 4 GB là đủ.

   - Tiết kiệm được rất nhiều thời gian cho việc tạo USB chứa bộ cài.
   - Cách tạo đơn giản, dễ hiểu.

2. Nhược điểm

   - Do là bộ cài online nên khi cài đặt cũng cần phải có tốc độ mạng khoẻ và thực sự ổn định.
   - Yêu cầu cần có kiến thức cơ bản trong việc tìm hiểu phần cứng của máy, để xác định được chipset mạng LAN hoặc Wi-Fi. Từ đó tìm kext cho đúng để có thể có internet, hỗ trợ trong quá trình cài đặt.
   - Yêu cầu phải biết tạo bootloader. Bởi vậy nó sẽ không dành cho những người lười nhác.
