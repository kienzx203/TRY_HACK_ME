# **Passive Reconnaissance**

## **Passive Versus Active Recon**

- Trinh sát (Reconnaissance) có thể được định nghĩa là một cuộc khảo sát sơ bộ để thu thập thông tin về một mục tiêu. Đây là bước đầu tiên trong The Unified Kill Chain để giành được chỗ đứng ban đầu trên một hệ thống. Chúng tôi chia trinh sát thành:
  - `Passive Reconnaissance`
  - `Active Reconnaissance`

- Trong trinh sát thụ động (Passive Reconnaissance), bạn dựa vào kiến thức có sẵn công khai. Đó là kiến thức mà bạn có thể truy cập từ các tài nguyên có sẵn công khai mà không cần tương tác trực tiếp với mục tiêu.

- Hoạt động do thám thụ động bao gồm nhiều hoạt động, ví dụ:
  - Tra cứu bản ghi DNS của miền từ máy chủ DNS công cộng.
  - Kiểm tra quảng cáo việc làm liên quan đến trang web mục tiêu.
  - Đọc các bài báo về công ty mục tiêu.

- Mặt khác, Active Reconnaissance không thể đạt được một cách kín đáo như vậy. Nó đòi hỏi sự tham gia trực tiếp với mục tiêu.
  - Kết nối với một trong các máy chủ của công ty như HTTP, FTP và SMTP.
  - Gọi cho công ty để cố lấy thông tin (kỹ thuật xã hội).
  - Vào khuôn viên công ty giả làm thợ sửa chữa.

![](./img_Precon/Screenshot%202023-07-14%20100552.png)

## **Whois**

- WHOIS là một giao thức yêu cầu và phản hồi tuân theo thông số kỹ thuật RFC 3912. Máy chủ WHOIS lắng nghe trên cổng TCP 43 đối với các yêu cầu gửi đến. Công ty đăng ký tên miền chịu trách nhiệm duy trì hồ sơ WHOIS cho các tên miền mà họ đang cho thuê. Máy chủ WHOIS trả lời với nhiều thông tin khác nhau liên quan đến miền được yêu cầu. Quan tâm đặc biệt, chúng ta có thể tìm hiểu:

  - `Công ty đăng ký:` Tên miền được đăng ký qua công ty đăng ký nào?
  - `Thông tin liên lạc của người đăng ký:` Tên, tổ chức, địa chỉ, điện thoại, trong số những thứ khác. (trừ khi được ẩn thông qua dịch vụ bảo mật)
  - `Ngày tạo, cập nhật và ngày hết hạn:` Tên miền được đăng ký lần đầu khi nào? Nó được cập nhật lần cuối khi nào? Và khi nào thì cần đổi mới?
  - `Name Server:` Hỏi máy chủ nào để phân giải tên miền?

![](./img_Precon/Screenshot%202023-07-14%20101628.png)

![](./img_Precon/Screenshot%202023-07-14%20101941.png)

## **nslookup**

- Tìm địa chỉ IP của một tên miền bằng cách sử dụng nslookup, viết tắt của Name Server Look Up. Bạn cần ra lệnh nslookup DOMAIN_NAME, ví dụ: nslookup tryhackme.com. Hoặc, tổng quát hơn, bạn có thể sử dụng `nslookup OPTIONS DOMAIN_NAME SERVER`. Ba tham số chính này là:

- Có nhiều máy chủ DNS công cộng khác mà bạn có thể chọn nếu muốn có các lựa chọn thay thế cho máy chủ DNS của ISP: [`more public DNS servers`](https://duckduckgo.com/?q=public+dns)

![](./img_Precon/Screenshot%202023-07-14%20102251.png)

![](./img_Precon/Screenshot%202023-07-14%20102502.png)

## **DNSDumpster**

- Để tránh việc tìm kiếm tốn thời gian như vậy, người ta có thể sử dụng dịch vụ trực tuyến cung cấp câu trả lời chi tiết cho các truy vấn DNS, chẳng hạn như `DNSDumpster`. Nếu chúng tôi tìm kiếm DNSDumpster cho tryhackme.com, chúng tôi sẽ phát hiện ra tên miền phụ blog.tryhackme.com, mà một truy vấn DNS thông thường không thể cung cấp. Ngoài ra, DNSDumpster sẽ trả lại thông tin DNS đã thu thập dưới dạng bảng và biểu đồ dễ đọc. DNSDumpster cũng sẽ cung cấp mọi thông tin thu thập được về các máy chủ lắng nghe.

![](./img_Precon/Screenshot%202023-07-14%20103114.png)

![](./img_Precon/Screenshot%202023-07-14%20103141.png)

## **Shodan.io**

- Khi bạn được giao nhiệm vụ chạy thử nghiệm thâm nhập đối với các mục tiêu cụ thể, như một phần của giai đoạn trinh sát thụ động, một dịch vụ như Shodan.io có thể hữu ích để tìm hiểu nhiều thông tin khác nhau về mạng của khách hàng mà không cần chủ động kết nối với mạng đó. Hơn nữa, về mặt phòng thủ, bạn có thể sử dụng các dịch vụ khác nhau từ Shodan.io để tìm hiểu về các thiết bị được kết nối và tiếp xúc thuộc về tổ chức của bạn.

- Khi bạn được giao nhiệm vụ chạy thử nghiệm thâm nhập đối với các mục tiêu cụ thể, như một phần của giai đoạn trinh sát thụ động, một dịch vụ như Shodan.io có thể hữu ích để tìm hiểu nhiều thông tin khác nhau về mạng của khách hàng mà không cần chủ động kết nối với mạng đó. Hơn nữa, về mặt phòng thủ, bạn có thể sử dụng các dịch vụ khác nhau từ Shodan.io để tìm hiểu về các thiết bị được kết nối và tiếp xúc thuộc về tổ chức của bạn.

![](./img_Precon/Screenshot%202023-07-14%20103322.png)

![](./img_Precon/Screenshot%202023-07-14%20103509.png)
