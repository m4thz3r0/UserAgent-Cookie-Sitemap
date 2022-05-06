 # <div align="center"><p> UserAgent, Cookie, Sitemap </p></div>
 ## Họ và tên: Mai Thị Hoàng Yến
 ## Ngày báo cáo: Ngày 8/5/2022
 ### MỤC LỤC
 1. [User agent](#gioithieu)
 
     1.1 [Phương pháp manual](#tc)
      
     1.2 [Phương pháp sử dụng sqlmap](#pp)
 
     1.3 [Phương pháp sử dụng công cụ BurpSuite](#p3)
     
 2. [website để kiểm tra UA](#mp) 
       
 3. [Tìm kiếm, cài đặt, chụp ảnh thực tế một vài Extension/Addon dùng để thay đổi UA trên Chrome và Firefox](#lv)

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

#### 2. website để kiểm tra UA <a name="gioithieu"></a>
 - Một số link website để kiểm tra UA:
   - https://www.whatsmyua.info
   - https://webbrowsertools.com/useragent/  
   - https://whatmyuseragent.com
   - https://dnschecker.org/user-agent-info.php
   - https://www.whatismybrowser.com
   
#### 3. Tìm kiếm, cài đặt, chụp ảnh thực tế một vài Extension/Addon dùng để thay đổi UA trên Chrome và Firefox <a name="gioithieu"></a>
 <br> 3.1 Trên Chrome <a name="tc"></a></br>
   - Đầu tiên chúng ta sẽ vào google và gõ tìm kiếm `user agent switcher and manager chrome` kết quả hiện thị như bên dưới:

     ![image](https://user-images.githubusercontent.com/101852647/167112431-5c61d2bf-4f36-46aa-9352-d774496f1680.png)
   
   - Sau đó chúng ta nhấn vào và bắt đầu tải Extension cho chrome . Chúng ta sẽ nhấn `add to chrome`.

     ![image](https://user-images.githubusercontent.com/101852647/167112651-a86adcec-475c-4fe4-a5b4-d071cfc3134c.png)

   - Tiếp theo ta sẽ nhấn `add Extension` và bắt đầu đợi cài đặt.

     ![image](https://user-images.githubusercontent.com/101852647/167112747-8aafedfd-2b5f-488d-8a8c-fa9041bb77e2.png)

   - Sau khi cài đặt xong chúng ta sẽ được giao diện như hình bên dưới:

     ![image](https://user-images.githubusercontent.com/101852647/167113155-be4d0478-065c-455b-91ae-0fb30e7a69ea.png)

   - Đầu tiên để kiểm tra thử UA của chúng ta thì nhấn vào Test UA nó sẽ hiện thị UA của chúng ta :

     ![image](https://user-images.githubusercontent.com/101852647/167113442-7e0924fb-a8ae-4229-a34b-54d06425c253.png)
     
   - Giả sử để thay đổi UA chúng ta sẽ chọn trình duyệt trình duyệt Firefox và chọn hệ điều hành là linux chẳng hạn.

     ![image](https://user-images.githubusercontent.com/101852647/167113815-6bb3e3df-502d-4b61-ae49-c41a7d223e47.png)
     
     ![image](https://user-images.githubusercontent.com/101852647/167113852-2df60ebd-f9c0-43fa-8aad-285d5faa26bc.png)
     
   - Chúng ta có thể chọn bất cứ UA nào . Ở đây , mình chọn UA thứ 4. Sau đó nhấn `Apply (active window).

     ![image](https://user-images.githubusercontent.com/101852647/167114071-f2ed84d3-248c-4ecb-a6e9-4291e65cdcc1.png)

   - Sau đó chúng ta nhấn vào Test UA để kiểm tra xem UA đã thay đổi chưa. Chúng ta có thể thấy nó đã thay đổi UA so với lúc đầu.

     ![image](https://user-images.githubusercontent.com/101852647/167114453-d0c575fa-099e-46e2-8bd8-1595626d9a51.png)

  - Nếu chúng ta muốn thay đổi về lại UA ban đầu thì có thể nhấn Reset. Nó sẽ trả về UA ban đầu cho chúng ta.

    ![image](https://user-images.githubusercontent.com/101852647/167114687-6482a3e2-0057-4d79-a187-ca5f19945408.png)

<br> 3.2 Trên Firefox <a name="tc"></a></br>

   - Đầu tiên chúng ta sẽ vào google và gõ tìm kiếm `user agent switcher and manager Firefox` kết quả hiện thị như bên dưới:

     ![image](https://user-images.githubusercontent.com/101852647/167116202-8b8098f1-c496-4a37-9a30-7307de428c99.png)
   
   - Sau đó chúng ta nhấn vào và bắt đầu tải Extension cho firefox . Chúng ta sẽ nhấn `Thêm vào firefox`.

     ![image](https://user-images.githubusercontent.com/101852647/167116281-74201de5-5bcc-4596-ab70-5507729e122c.png)

   - Tiếp theo ta sẽ nhấn `add` và bắt đầu đợi cài đặt.

     ![image](https://user-images.githubusercontent.com/101852647/167116312-b428a852-a289-41cc-9764-756659eb4178.png)

   - Sau khi cài đặt xong chúng ta sẽ được giao diện như hình bên dưới:

     ![image](https://user-images.githubusercontent.com/101852647/167116337-cf965734-84d4-4a58-8785-885b85d4d6ad.png)

   - Đầu tiên để kiểm tra thử UA của chúng ta thì nhấn vào Test UA nó sẽ hiện thị UA của chúng ta :

     ![image](https://user-images.githubusercontent.com/101852647/167116409-f34fa7bc-9575-4fe0-8e7a-8310fd58b23b.png)
     
   - Giả sử để thay đổi UA chúng ta sẽ chọn trình duyệt trình duyệt Chrome và chọn hệ điều hành là linux chẳng hạn.

     ![image](https://user-images.githubusercontent.com/101852647/167116475-a466a612-f164-4bde-a82f-fdef05a66d55.png)
     
     ![image](https://user-images.githubusercontent.com/101852647/167116500-07c3d47a-8255-4099-9178-0f039cd09084.png)
     
   - Chúng ta có thể chọn bất cứ UA nào . Ở đây , mình chọn UA thứ 3. Sau đó nhấn `Apply (active window).

     ![image](https://user-images.githubusercontent.com/101852647/167116850-d59f3e2c-6408-449c-b3f0-265da214bc9c.png)

   - Sau đó chúng ta nhấn vào Test UA để kiểm tra xem UA đã thay đổi chưa. Chúng ta có thể thấy nó đã thay đổi UA so với lúc đầu.

     ![image](https://user-images.githubusercontent.com/101852647/167116653-f3742951-2a32-4284-844f-d94091b1feac.png)

  - Nếu chúng ta muốn thay đổi về lại UA ban đầu thì có thể nhấn Reset. Nó sẽ trả về UA ban đầu cho chúng ta.

    ![image](https://user-images.githubusercontent.com/101852647/167116683-725b86b6-89a8-44fa-9270-1f73faca245f.png)

#### 4. Tìm hiểu về sitemap <a name="gioithieu"></a>
<br> 4.1 sitemap là gì? <a name="tc"></a></br>
 - Sitemap (sơ đồ website) là một file liệt kê các trang và tệp tin trên website. Danh sách liệt kê được sắp xếp theo dạng sơ đồ phân tầng (giảm dần sự quan trọng) giúp các công cụ tìm kiếm:

   - Thu thập dữ liệu trên trang web của bạn hiệu quả hơn
   - Biết những URL nào bạn muốn ưu tiên xuất hiện
   - Hiển thị kết quả trên trang tìm kiếm thông minh hơn
   
<br> 4.2 Các loại sitemap <a name="tc"></a></br>
 - Về mặt cấu trúc: 
   - Có 2 loại sitemap là XML và HTML.

     - XML (Dành cho bot của công cụ tìm kiếm) 

     - HTML (Hiển thị cho người dùng dễ truy cập trên các giao diện trang web)
     
         <table align="center">
          <tr>
            <td align="center" ><b>Sitemap</b></td>
            <td align="center"><b>XML</b></td>
            <td align="center"><b>HTML</b></td>   
          </tr>
          <tr>
            <td ><b>Đặc điểm</b></td>
            <td ><br><b>- Chứa các metadata chung với URL của website</b></br>
                 <br><b>- Chứa các thông tin về thời gian cập nhật</b></br>
            </td>  
            <td ><br><b>- Cung cấp chuyển hướng rõ ràng cho người dùng</b></br>
                 <br><b>- Dựa vào tính thân thiện thúc đẩy thứ hạng của website</b></br>
            </td> 
          </tr>
          <tr>
            <td ><b>Giống nhau</b></td>
            <td colspan="2" align="center"><b>XML và HTML đều cho phép trang web dễ dàng crawl bởi search engines</b></td>   
          </tr>
          <tr>
            <td><b>Khác nhau</b></td>
            <td><b>Dùng được cho search engine </b></td>      
            <td><b>Viết cho người dùng website</b></td>      
          </tr>

        </table>
    
- Về dạng: 

      <table align="center">
         <tr>
             <td align="center" ><b>Tên</b></td>
             <td align="center"><b>Chức năng</b></td>
         </tr>
         <tr>
             <td ><b>Sitemap Index</b></td>
             <td ><b> Tập hợp các Sitemap được đính kèm và được dùng để đặt trong file robots.txt</b></td>  
         </tr>
         <tr>
             <td ><b>Sitemap-category.xml</b></td>
             <td ><b>Tập hợp cấu trúc của các danh mục trên website.</b></td>   
         </tr>
         <tr>
             <td><b>Sitemap-products.xml</b></td>
             <td><b>Sitemap dành cho các link chi tiết về các sản phẩm trên trang. </b></td>          
         </tr>
         <tr>
             <td ><b>Sitemap-articles.xml</b></td>
             <td ><b>Giúp Google tìm thấy nội dung trên các trang web được chấp thuận cho Google Tin tức..</b></td>   
         </tr>
         <tr>
             <td ><b>Sitemap-tags.xml</b></td>
             <td ><b>Sitemap dành cho các thẻ trên website</b></td>   
         </tr>
         <tr>
             <td ><b>Sitemap-video.xml</b></td>
             <td ><b>Sitemap dành riêng cho video trên các page, website. Được sử dụng đặc biệt để giúp Google hiểu nội dung video trên trang của bạn</b></td>   
        </tr>
        <tr>
             <td ><b>Sitemap-image.xml</b></td>
             <td ><b>Giúp Google tìm thấy tất cả các hình ảnh được lưu trữ trên trang web của bạn</b></td>   
        </tr>
     </table>
  
<br> 4.3 Tại sao phải cần dùng sitemap <a name="tc"></a></br>
 - Chúng ta luôn muốn Google thu thập dữ liệu mọi trang và liên kết quan trọng trên website một cách nhanh chóng. Sitemap sẽ là bản đồ điều hướng, giúp các bot của google có thể dễ dàng và nhanh chóng thu thập được dữ liệu nội dung trên website của chúng ta.
 
 - Sitemap còn có thể chứa các siêu dữ liệu về mỗi URL, thông báo sẽ được gửi đến cho chúng ta khi nó mới được cập nhật. Toàn bộ công việc của Sitemap là hướng dẫn cho các bộ máy tìm kiếm thu thập thông tin của trang web một cách hiệu quả đồng thời cập nhật những thay đổi trên trang web của bạn.Chính lý do này thì thiết kế web chuẩn SEO bắt buộc phải có Sitemap để đảm bảo Google và các công cụ tìm kiếm có thể thu thập dữ liệu một cách nhanh nhất.

