# **Vulnerabilities 101**

## **Introduction to Vulnerabilities**

- Một lỗ hổng trong an ninh mạng được định nghĩa là một điểm yếu hoặc lỗ hổng trong thiết kế, triển khai hoặc hành vi của một hệ thống hoặc ứng dụng. Kẻ tấn công có thể khai thác những điểm yếu này để giành quyền truy cập vào thông tin trái phép hoặc thực hiện các hành động trái phép. Thuật ngữ “lỗ hổng” có nhiều định nghĩa bởi các cơ quan an ninh mạng. Tuy nhiên, có sự khác biệt tối thiểu giữa tất cả chúng.

![](./img_101/Screenshot%202023-07-14%20163516.png)

![](./img_101/Screenshot%202023-07-14%20163719.png)

## **Scoring Vulnerabilities (CVSS & VPR)**

> `Common Vulnerability Scoring System`

- Được giới thiệu lần đầu tiên vào năm 2005, Hệ thống chấm điểm lỗ hổng chung (hay CVSS) là một khuôn khổ rất phổ biến để chấm điểm lỗ hổng và có ba lần lặp lại chính. Như hiện tại, phiên bản hiện tại là CVSSv3.1 (với phiên bản 4.0 hiện đang ở dạng nháp), điểm số về cơ bản được xác định bởi một số yếu tố sau (nhưng còn nhiều yếu tố khác):

1. Lỗ hổng dễ bị khai thác như thế nào?

2. Có khai thác cho việc này không?

3. Lỗ hổng này can thiệp vào bộ ba CIA như thế nào?

![](./img_101/Screenshot%202023-07-14%20164056.png)

> `Vulnerability Priority Rating (VPR)`

- Khung VPR là một khung hiện đại hơn nhiều trong quản lý lỗ hổng - được phát triển bởi Tenable, nhà cung cấp giải pháp công nghiệp để quản lý lỗ hổng. Khuôn khổ này được coi là định hướng rủi ro; có nghĩa là các lỗ hổng được cho điểm tập trung nhiều vào rủi ro mà lỗ hổng gây ra cho chính tổ chức, thay vì các yếu tố như tác động (như với CVSS).

- Không giống như CVSS, điểm VPR tính đến mức độ liên quan của lỗ hổng. Ví dụ: không có rủi ro nào được xem xét liên quan đến lỗ hổng nếu lỗ hổng đó không áp dụng cho tổ chức (nghĩa là họ không sử dụng phần mềm dễ bị tổn thương). VPR cũng rất năng động trong việc chấm điểm, trong đó rủi ro mà lỗ hổng bảo mật có thể gây ra có thể thay đổi gần như hàng ngày khi nó cũ đi.

- VPR sử dụng phạm vi tính điểm tương tự như CVSS mà tôi cũng đã đưa vào bảng bên dưới. Tuy nhiên, có hai điểm khác biệt đáng chú ý là VPR không có hạng mục "Không/Thông tin" và do VPR sử dụng cách tính điểm khác nên cùng một lỗ hổng sẽ có điểm khi sử dụng VPR khác với khi sử dụng CVSS.

![](./img_101/Screenshot%202023-07-14%20164404.png)

![](./img_101/Screenshot%202023-07-14%20164453.png)

## **Vulnerability Databases**

- Trong suốt hành trình của mình trong lĩnh vực an ninh mạng, bạn sẽ thường bắt gặp rất nhiều ứng dụng và dịch vụ khác nhau. Ví dụ: một CMS trong khi tất cả chúng đều có cùng mục đích, thường có thiết kế và hành vi rất khác nhau (và do đó, các lỗ hổng tiềm ẩn khác nhau).

- Rất may cho chúng tôi, có những tài nguyên trên internet theo dõi các lỗ hổng cho tất cả các loại phần mềm, hệ điều hành, v.v.! Chúng tôi sẽ giới thiệu hai cơ sở dữ liệu mà chúng ta có thể sử dụng để tra cứu các lỗ hổng hiện có cho các ứng dụng được phát hiện trong hành trình bảo mật thông tin của chúng ta, cụ thể là các trang web sau:

1. [`NVD (National Vulnerability Database)`](https://nvd.nist.gov/vuln/full-listing)

2. [`Exploit-DB`](http://exploit-db.com/)

![](./img_101/Screenshot%202023-07-14%20165028.png)
