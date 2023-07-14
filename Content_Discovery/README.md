# **Content Discovery**

## **Content Discovery là gì?**

- Khi chúng tôi nói về Content Discovery, chúng tôi không nói về những thứ hiển nhiên mà chúng tôi có thể thấy trên một trang web mà  đó là những nội dung không được trình bày.

- Có ba cách chính để khám phá nội dung trên một trang web mà chúng tôi sẽ đề cập. Thủ công, Tự động và OSINT (Trí thông minh nguồn mở).

![](./img_cd/Screenshot%202023-07-13%20153131.png)

## **Manual Discovery - Robots.txt**

- Tệp robots.txt là một tài liệu cho các công cụ tìm kiếm biết các trang đó là và không được phép hiển thị trên các kết quả của công cụ tìm kiếm hoặc cấm các công cụ tìm kiếm cụ thể thu thập dữ liệu trang web hoàn toàn. Thông thường có thể hạn chế các khu vực trang web nhất định để chúng không được hiển thị trong kết quả của công cụ tìm kiếm. Các trang này có thể là các khu vực như cổng quản trị hoặc tệp dành cho khách hàng của trang web. Tệp này cung cấp cho chúng tôi một danh sách tuyệt vời về các vị trí trên trang web mà chủ sở hữu không muốn chúng tôi phát hiện ra với tư cách là người kiểm tra thâm nhập.

![](./img_cd/Screenshot%202023-07-13%20153352.png)

![](./img_cd/Screenshot%202023-07-13%20153618.png)

## **Manual Discovery - Favicon**

- Favicon là một biểu tượng nhỏ được hiển thị trong thanh địa chỉ của trình duyệt hoặc tab được sử dụng để xây dựng thương hiệu cho một trang web.

- OWASP lưu trữ cơ sở dữ liệu gồm các biểu tượng khung phổ biến mà bạn có thể sử dụng để kiểm tra đối với favicon mục tiêu `https://wiki.owasp.org/index.php/OWASP_favicon_database`. Sau khi biết ngăn xếp khung, chúng ta có thể sử dụng các tài nguyên bên ngoài để khám phá thêm về nó (xem phần tiếp theo).

## **Manual Discovery - Sitemap.xml**

- Không giống như tệp robots.txt hạn chế những gì trình thu thập thông tin của công cụ tìm kiếm có thể xem, tệp sitemap.xml cung cấp danh sách mọi tệp mà chủ sở hữu trang web muốn được liệt kê trên công cụ tìm kiếm. Đôi khi, chúng có thể chứa các khu vực của trang web khó điều hướng hơn một chút hoặc thậm chí liệt kê một số trang web cũ mà trang web hiện tại không còn sử dụng nữa nhưng vẫn đang hoạt động ở hậu trường.

## **Manual Discovery - HTTP Headers**

- Khi chúng tôi yêu cầu máy chủ web, máy chủ sẽ trả về các tiêu đề HTTP khác nhau. Các tiêu đề này đôi khi có thể chứa thông tin hữu ích chẳng hạn như phần mềm máy chủ web và có thể là ngôn ngữ lập trình/kịch bản đang được sử dụng. Trong ví dụ dưới đây, chúng ta có thể thấy máy chủ web là NGINX phiên bản 1.18.0 và chạy phiên bản PHP 7.4.3. Sử dụng thông tin này, chúng tôi có thể tìm thấy các phiên bản phần mềm dễ bị tấn công đang được sử dụng. Hãy thử chạy lệnh curl bên dưới đối với máy chủ web, trong đó công tắc -v bật chế độ dài dòng, thao tác này sẽ xuất ra các tiêu đề (có thể có điều gì đó thú vị!).

```
user@machine$ curl http://10.10.1.84 -v
*   Trying 10.10.1.84:80...
* TCP_NODELAY set
* Connected to MACHINE_IP (MACHINE_IP) port 80 (#0)
> GET / HTTP/1.1
> Host: MACHINE_IP
> User-Agent: curl/7.68.0
> Accept: */*
> 
* Mark bundle as not supporting multiuse
< HTTP/1.1 200 OK
< Server: nginx/1.18.0 (Ubuntu)
< X-Powered-By: PHP/7.4.3
< Date: Mon, 19 Jul 2021 14:39:09 GMT
< Content-Type: text/html; charset=UTF-8
< Transfer-Encoding: chunked
< Connection: keep-alive
```

## **OSINT - Google Hacking / Dorking**

- Google hacking / Dorking sử dụng các tính năng công cụ tìm kiếm nâng cao của Google, cho phép bạn chọn ra nội dung tùy chỉnh. Ví dụ: bạn có thể chọn ra kết quả từ một tên miền nhất định bằng cách sử dụng bộ lọc site: (site:tryhackme.com), sau đó, bạn có thể khớp kết quả này với các cụm từ tìm kiếm nhất định, chẳng hạn như từ quản trị viên (trang web :tryhackme.com admin) thì điều này sẽ chỉ trả về kết quả từ trang web tryhackme.com có chứa từ quản trị viên trong nội dung của nó. Bạn cũng có thể kết hợp nhiều bộ lọc. Dưới đây là ví dụ về nhiều bộ lọc hơn mà bạn có thể sử dụng:

![](./img_cd/Screenshot%202023-07-13%20160718.png)

## **OSINT - Wayback Machine**

- Wayback Machine (`https://archive.org/web/`) là kho lưu trữ lịch sử các trang web có từ cuối những năm 90. Bạn có thể tìm kiếm một tên miền và nó sẽ hiển thị cho bạn tất cả các lần dịch vụ quét trang web và lưu nội dung. Dịch vụ này có thể giúp khám phá các trang cũ có thể vẫn đang hoạt động trên trang web hiện tại.
