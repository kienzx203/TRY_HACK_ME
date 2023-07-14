# **Metasploit: Introduction**

## **Introduction to Metasploit**

- Metasploit là khung khai thác được sử dụng rộng rãi nhất. Metasploit là một công cụ mạnh mẽ có thể hỗ trợ tất cả các giai đoạn của quá trình tham gia thử nghiệm thâm nhập, từ thu thập thông tin đến hậu khai thác.

- Metasploit có hai phiên bản chính:

  - Metasploit Pro: Phiên bản thương mại hỗ trợ tự động hóa và quản lý các tác vụ. Phiên bản này có giao diện người dùng đồ họa (GUI).
  - Metasploit Framework: Phiên bản mã nguồn mở hoạt động từ dòng lệnh. Phòng này sẽ tập trung vào phiên bản này, được cài đặt trên AttackBox và các bản phân phối Linux thử nghiệm thâm nhập được sử dụng phổ biến nhất.

- Các thành phần chính của Metasploit Framework có thể được tóm tắt như sau:
  - `msfconsole:` Giao diện dòng lệnh chính.
  - `Modules:` hỗ trợ các mô-đun như khai thác, máy quét, tải trọng, v.v.
  - `Tools:` Các công cụ độc lập sẽ giúp nghiên cứu lỗ hổng, đánh giá lỗ hổng hoặc kiểm tra thâm nhập. Một số công cụ này là msfvenom, pattern_create và pattern_offset. Chúng tôi sẽ đề cập đến msfvenom trong mô-đun này, nhưng pattern_create và pattern_offset là những công cụ hữu ích trong việc phát triển khai thác nằm ngoài phạm vi của mô-đun này.

## **Main Components of Metasploit**

- Trong khi sử dụng Metasploit Framework, bạn sẽ chủ yếu tương tác với bảng điều khiển Metasploit.

- Trong khi sử dụng Metasploit Framework, bạn sẽ chủ yếu tương tác với bảng điều khiển Metasploit.

- Bảng điều khiển sẽ là giao diện chính của bạn để tương tác với các mô-đun khác nhau của Metasploit Framework. Các mô-đun là các thành phần nhỏ trong khuôn khổ Metasploit được xây dựng để thực hiện một nhiệm vụ cụ thể, chẳng hạn như khai thác lỗ hổng, quét mục tiêu hoặc thực hiện một cuộc tấn công vũ phu.

> `Auxiliary`

- Có thể tìm thấy bất kỳ mô-đun hỗ trợ nào, chẳng hạn như scanners, crawlers và fuzzers tại đây.

![](./imh_mi/Screenshot%202023-07-14%20192223.png)

> `Encoders`

- Bộ mã hóa sẽ cho phép bạn mã hóa khai thác và tải trọng với hy vọng rằng giải pháp chống vi-rút dựa trên chữ ký có thể bỏ lỡ chúng.

- Các giải pháp bảo mật và chống vi-rút dựa trên chữ ký có cơ sở dữ liệu về các mối đe dọa đã biết. Họ phát hiện các mối đe dọa bằng cách so sánh các tệp đáng ngờ với cơ sở dữ liệu này và đưa ra cảnh báo nếu có sự trùng khớp. Do đó, bộ mã hóa có thể có tỷ lệ thành công hạn chế vì các giải pháp chống vi-rút có thể thực hiện các kiểm tra bổ sung.

![](./imh_mi/Screenshot%202023-07-14%20192540.png)

> `Evasion`

- Mặc dù bộ mã hóa sẽ mã hóa tải trọng nhưng chúng không được coi là nỗ lực trực tiếp để trốn tránh phần mềm chống vi-rút. Mặt khác, các mô-đun “evasion” sẽ thử điều đó, với ít nhiều thành công.

![](./imh_mi/Screenshot%202023-07-14%20192724.png)

> `Exploits`

![](./imh_mi/Screenshot%202023-07-14%20192809.png)

> `NOPs`

- NOP Chúng được đại diện trong họ CPU Intel x86, chúng được đại diện bằng 0x90, theo đó CPU sẽ không làm gì trong một chu kỳ. Chúng thường được sử dụng làm bộ đệm để đạt được kích thước tải trọng phù hợp.

![](./imh_mi/Screenshot%202023-07-14%20192936.png)

> `Payloads`

![](./imh_mi/Screenshot%202023-07-14%20193046.png)

- Bạn sẽ thấy bốn thư mục khác nhau dưới tải trọng:`adapters, singles, stagers và stages`

  - `Adapters:`Bộ điều hợp bao bọc các tải trọng đơn lẻ để chuyển đổi chúng thành các định dạng khác nhau. Ví dụ: một tải trọng đơn bình thường có thể được bọc bên trong bộ điều hợp Powershell, bộ điều hợp này sẽ tạo ra một lệnh powershell duy nhất sẽ thực thi tải trọng đó.
  - `Singles:` Tải trọng độc lập (thêm người dùng, khởi chạy notepad.exe, v.v.) không cần tải xuống thành phần bổ sung để chạy.
  - `Stagers:` Chịu trách nhiệm thiết lập kênh kết nối giữa Metasploit và hệ thống đích. Hữu ích khi làm việc với tải trọng theo giai đoạn. “Tải trọng theo giai đoạn” trước tiên sẽ tải lên một giai đoạn trên hệ thống đích, sau đó tải xuống phần còn lại của tải trọng (giai đoạn). Điều này mang lại một số lợi thế vì kích thước ban đầu của tải trọng sẽ tương đối nhỏ so với toàn bộ tải trọng được gửi cùng một lúc.
  - `Stages:` Được tải xuống bởi stager. Điều này sẽ cho phép bạn sử dụng tải trọng có kích thước lớn hơn.

> `Post`

![](./imh_mi/Screenshot%202023-07-14%20193417.png)

## **Msfconsole**

- Như đã đề cập trước đây, bảng điều khiển sẽ là giao diện chính của bạn với Metasploit Framework. Bạn có thể khởi chạy nó bằng lệnh msfconsole

![](./imh_mi/Screenshot%202023-07-14%20193647.png)

- Bảng điều khiển Metasploit (msfconsole) có thể được sử dụng giống như command-line shell

![](./imh_mi/Screenshot%202023-07-14%20193757.png)

- Sử dụng command `use` để lựa chọn mã khai thác:

![](./imh_mi/Screenshot%202023-07-14%20194257.png)

- Sử dụng lệnh `show` để liệt kê những module hoặc payload.

![](./imh_mi/Screenshot%202023-07-14%20194448.png)

![](./imh_mi/Screenshot%202023-07-14%20194501.png)

- Sử dụng lệnh `info` để biết thêm thông tin module hoặc payload.
- Một trong những lệnh hữu ích nhất trong msfconsole là `Search`. Lệnh này sẽ Search cơ sở dữ liệu Metasploit Framework cho các mô-đun liên quan đến tham số Search đã cho. Bạn có thể tiến hành Search bằng cách sử dụng số CVE, tên khai thác (eternalblue, heartbleed, v.v.) hoặc hệ thống đích.

![](./imh_mi/Screenshot%202023-07-14%20194740.png)

- Sử dụng lệnh `unset và set` để add và xóa những option.

![](./imh_mi/Screenshot%202023-07-14%20195840.png)
