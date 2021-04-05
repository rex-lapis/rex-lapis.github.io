---
layout: post
title: Multiboot sử dụng OpenCore
---

- OpenCore hỗ trợ multi boot khá tốt. Nhưng có một điểm trừ "chết người" của nó, là việc nó inject toàn bộ ACPI có trong folder bootloader và SMBIOS sang các hệ điều hành khác, dẫn đến việc boot sang Windows hay Linux bị lỗi, hoặc thậm chí đơn giản là BSOD huyền thoại.

- Vậy nên, để có thể chắc chắn việc multi boot thông qua OpenCore thực sự đạt ở mức độ "ổn định" nhất có thể (mình sẽ không nói là hoàn hảo bởi không có gì là hoàn hảo đến tuyệt đối cả), cần lưu ý một số vấn đề không to mà cũng chẳng hề nhỏ sau:

1. Setting trong **config.plist**

   - Nếu bạn dùng OpenCore nhưng chỉ cần multi boot ổn định và không đả động gì đến cái BootCamp utilities thì tốt nhất là nên setting như sau:

     - CustomSMIOSGuid: True/Yes hoặc tick nó ở trong OpenCore Configurator

       ![customsmbiosguid](/images/customsmbiosguid.png)

     - UpdateSMBIOSMode: Set là Custom

       ![updatesmbiosmode](/images/updatesmbiosmode.png)

   - Mục đích của việc này là "chống inject" thông tin SMBIOS sang các OSes khác (ví dụ MacBookPro15,1, iMac20,1,...). Nếu muốn kiểm tra máy có bị inject hay không thì chỉ cần chạy **dxdiag** ở Run trên Windows là được.
   - OpenCore họ cứ doạ nếu không set đúng hai cái này có thể gây lỗi BootCamp này nọ, nhưng thực tế không động đến BootCamp thì lờ nó đi, vì mục đích cuối cùng vẫn là multi boot ổn định.

2. ACPI

   - Một vấn đề nữa là việc OpenCore sẽ inject SSDT sang các OSes khác. Hiểu nôm na là bạn chỉ ăn được đồ ăn châu Á nhưng đầu bếp lại nêm gia vị theo phong cách châu Âu khiến việc cũng là món châu Á đó nhưng bạn không thể ăn được.

   - Bởi vậy, SSDT dùng cho OpenCore nó sẽ khác hoàn toàn so với Clover trước đây. Bắt buộc phải có một **Method _STA** (STA viết tắt của status, nghĩa là trạng thái) cùng condition **If (_OSI ("Darwin"))** để chắc chắn rằng SSDT sẽ **chỉ hoạt động** khi boot vào macOS (bởi kernel của macOS tên là Darwin).

     Lấy ví dụ như hình dưới là SSDT-EC, để fake EC cho macOS. Trong **Device (EC)** sẽ có một condition **If (_OSI ("Darwin"))**, giá trị sẽ trả về 0x0F, nghĩa là sẽ **Enable**. Còn **Else**, trả về **Zero**, nghĩa là không phải macOS thì sẽ không hoạt động.

   ![ec](/images/ec.png)

   - Việc xử lý SSDT này khá khó với những ai không biết code hoặc chưa có kinh nghiệm trong việc này. Vậy nên mình khuyến khích hãy sử dụng bản pre-built của Dortania, hoặc bản pre-built của mình để tránh việc lỗi multi boot. Mình sẽ không khuyến khích việc đi lấy EFI máy cần cài ở trên GitHub hoặc bạn đi xin được nó ở đâu đó, trừ khi bạn hiểu được họ đã làm gì với EFI của họ và bạn đang làm gì.
   - Link download SSDT bản pre-built của mình: [Download](https://github.com/rex-lapis/Hackintosh-Stuff)