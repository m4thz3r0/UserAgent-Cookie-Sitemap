 # <div align="center"><p> UserAgent, Cookie, Sitemap </p></div>
 ## Họ và tên: Mai Thị Hoàng Yến
 ## Ngày báo cáo: Ngày 8/5/2022
 ### MỤC LỤC
 1. [User agent](#gioithieu)
 
     1.1 [Phương pháp manual](#tc)
      
     1.2 [Phương pháp sử dụng sqlmap](#pp)
 
     1.3 [Phương pháp sử dụng công cụ BurpSuite](#p3)
     
 2. [website để kiểm tra UA](#mp) 
       
 3. [Tìm kiếm, cài đặt, chụp ảnh thực tế một vài Extension/Addon dùng để thay đổi UA](#lv)

     3.1 [Code sửa lỗi sqli cho level2](#code1)
      
     3.2 [Code sửa lỗi sqli cho level1](#code2)
     
     3.3 [Các hàm sử dụng](#chsd)
 4. [Tìm hiểu về sitemap](#lv)


 5. [Tạo sitemap trên web cá nhân của mình](#lv)


 6. [Tìm hiểu về Cookie](#lv)

 7. [Tìm kiếm, cài đặt, chụp ảnh thực tế một vài Extension/Addon dùng để xem và thay đổi Cookie ](#lv)


### Nội dung báo cáo 
#### 1. User agent là gì? <a name="gioithieu"></a>
<br> 1.1 User agent là gì? <a name="tc"></a></br>
  - User agent thì nó là một chuỗi nhận dạng của trình duyệt khi gửi yêu cầu đến Web Server (máy chủ web). Khi trình duyệt web của bạn truy cập 1 trang Web bất kỳ, trình duyệt web của bạn có thể gửi một HTTP Request bao gồm chuỗi UA đến Web Server. Nội dung của UA tùy thuộc vào trình duyệt web các bạn dùng, mỗi trình duyệt đều có riêng 1 chuỗi UA nhất định. 
  
<br> 1.2 User agent sử dụng trong HTTP <a name="tc"></a></br>
 - chuỗi User-Agent thường được sử dụng để thương lượng nội dung , trong đó máy chủ gốc chọn nội dung hoặc thông số hoạt động phù hợp cho phản hồi. Như với nhiều tiêu đề yêu cầu HTTP khác, thông tin trong chuỗi " User-Agent " góp phần vào thông tin mà máy khách gửi đến máy chủ, vì chuỗi này có thể khác nhau đáng kể từ người dùng này sang người dùng khác.
   - Định dạng cho các trình duyệt web do con người vận hành:
     - Định dạng của chuỗi User-Agent trong HTTP là danh sách các mã thông báo sản phẩm (từ khóa) với các nhận xét tùy chọn.  Ví dụ: nếu sản phẩm của người dùng được gọi là WikiBrowser, thì chuỗi User-Agent của họ có thể là WikiBrowser / 1.0 Gecko / 1.0 . Thành phần sản phẩm "quan trọng nhất" được liệt kê đầu tiên. Các phần của chuỗi này như sau:

       ` Tên và phiên bản sản phẩm ( WikiBrowser / 1.0 )`
       ` Công cụ bố trí và phiên bản ( Gecko / 1.0 )`
       
   - Định dạng cho tác nhân tự động (bot):
     - Các công cụ thu thập thông tin web tự động có thể sử dụng biểu mẫu đơn giản hóa, trong đó trường quan trọng là thông tin liên hệ trong trường hợp có sự cố. Theo quy ước từ "bot" được bao gồm trong tên của agent. Ví dụ:
       `Googlebot / 2.1 (+ http: //www.google.com/bot.html)`
     
   - User agent spoofing:
   
     - Các trang web thường bao gồm mã để phát hiện phiên bản trình duyệt để điều chỉnh thiết kế trang được gửi theo chuỗi tác nhân người dùng nhận được. Điều này có thể có nghĩa là các trình duyệt ít phổ biến hơn không được gửi nội dung phức tạp (mặc dù chúng có thể xử lý nó một cách chính xác) hoặc trong những trường hợp nghiêm trọng đã từ chối tất cả nội dung. Do đó, các trình duyệt khác nhau có tính năng che giấu hoặc giả mạo nhận dạng của chúng để buộc nội dung phía máy chủ nhất định. Ví dụ: trình duyệt Android tự nhận mình là Safari để hỗ trợ khả năng tương thích.
     - Các chương trình khách HTTP khác, như trình quản lý tải xuống và trình duyệt ngoại tuyến , thường có khả năng thay đổi chuỗi tác nhân người dùng.
     - Kết quả của việc giả mạo tác nhân người dùng có thể là số liệu thống kê được thu thập về việc sử dụng trình duyệt Web không chính xác.
     
   - User agent sniffing:
     - User agent sniffing là việc các trang web hiển thị nội dung khác nhau hoặc được điều chỉnh khi được xem với một số tác nhân người dùng nhất định.
     - User agent sniffing  được coi là hành vi kém, vì nó khuyến khích thiết kế dành riêng cho trình duyệt và phạt các trình duyệt mới có nhận dạng tác nhân người dùng không được công nhận. 
     - Chúng ta nên tạo đánh dấu HTML tiêu chuẩn, ho phép hiển thị chính xác trong nhiều trình duyệt nhất có thể và để kiểm tra các tính năng của trình duyệt cụ thể hơn là các phiên bản hoặc nhãn hiệu trình duyệt cụ thể.
     
   - Ký hiệu độ mạnh mã hóa:
     -  Trước đây đã sử dụng các chữ cái U, I và N để chỉ định độ mạnh mã hóa trong chuỗi tác nhân người dùng. "U" là viết tắt của "USA" (dành cho phiên bản có mã hóa 128 bit), "I" là viết tắt của "International" - trình duyệt có mã hóa 40 bit và có thể được sử dụng ở mọi nơi trên thế giới - và "N" là viết tắt của ( de facto ) cho "None" (không mã hóa). 
     -  Bây giờ, hầu hết các nhà cung cấp đều hỗ trợ mã hóa 256-bit.

   - Ngừng sử dụng tiêu đề User agent:
     - Google tuyên bố rằng một tính năng mới có tên là Client Hints sẽ thay thế chức năng của chuỗi User-Agent.

  
