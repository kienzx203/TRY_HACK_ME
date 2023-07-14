# **Security Operations**

## **Introduction to Security Operations**

- Security Operations Center (SOC) là một nhóm gồm các chuyên gia bảo mật CNTT được giao nhiệm vụ giám sát mạng và hệ thống của công ty 24 giờ một ngày, bảy ngày một tuần. Mục đích giám sát của họ là để:

  - `Find vulnerabilities on the network:` Lỗ hổng là điểm yếu mà kẻ tấn công có thể khai thác để thực hiện những việc vượt quá mức cho phép của chúng. Lỗ hổng bảo mật có thể được phát hiện trong phần mềm của bất kỳ thiết bị nào (hệ điều hành và chương trình) trên mạng, chẳng hạn như máy chủ hoặc máy tính. Chẳng hạn, SOC có thể phát hiện ra một tập hợp các máy tính MS Windows phải được vá đối với một lỗ hổng đã công bố cụ thể. Nói một cách chính xác, các lỗ hổng không nhất thiết thuộc trách nhiệm của SOC; tuy nhiên, các lỗ hổng chưa được khắc phục sẽ ảnh hưởng đến mức độ bảo mật của toàn bộ công ty.

  - `Detect unauthorized activity:` Hãy xem xét trường hợp kẻ tấn công phát hiện ra tên người dùng và mật khẩu của một trong các nhân viên và sử dụng nó để đăng nhập vào hệ thống của công ty. Điều quan trọng là phải nhanh chóng phát hiện loại hoạt động trái phép này trước khi nó gây ra bất kỳ thiệt hại nào. Nhiều manh mối có thể giúp chúng tôi phát hiện ra điều này, chẳng hạn như vị trí địa lý.

  - `Discover policy violations:` Chính sách bảo mật là một tập hợp các quy tắc và quy trình được tạo để giúp bảo vệ công ty khỏi các mối đe dọa bảo mật và đảm bảo tuân thủ. Những gì được coi là vi phạm sẽ thay đổi từ công ty này sang công ty khác; các ví dụ bao gồm tải xuống các tệp phương tiện vi phạm bản quyền và gửi các tệp bí mật của công ty một cách không an toàn.

  - `Detect intrusions:` Xâm nhập đề cập đến xâm nhập hệ thống và mạng. Một tình huống ví dụ sẽ là kẻ tấn công khai thác thành công ứng dụng web của chúng tôi. Một tình huống ví dụ khác là người dùng truy cập trang web độc hại và khiến máy tính của họ bị nhiễm virus.

  - `Support with the incident response:` Một sự cố có thể là một quan sát, vi phạm chính sách, nỗ lực xâm nhập hoặc điều gì đó gây thiệt hại hơn như vi phạm lớn. Ứng phó chính xác với một sự cố nghiêm trọng không phải là một nhiệm vụ dễ dàng. SOC có thể hỗ trợ đội ứng phó sự cố xử lý tình huống.

![](./img_so/Screenshot%202023-07-12%20205136.png)

## **Elements of Security Operations**

> `Data Sources`

- SOC sử dụng nhiều nguồn dữ liệu để giám sát mạng để tìm các dấu hiệu xâm nhập và phát hiện bất kỳ hành vi nguy hiểm nào. Một số nguồn này là

  - `Server logs:` Có nhiều loại máy chủ trên mạng, chẳng hạn như máy chủ thư, máy chủ web và bộ điều khiển miền trên mạng MS Windows. Nhật ký chứa thông tin về các hoạt động khác nhau, chẳng hạn như lần đăng nhập thành công và thất bại, trong số nhiều hoạt động khác. Có một kho thông tin có thể được tìm thấy trong nhật ký máy chủ.

  - `DNS activity:` DNS là viết tắt của Domain Name System và là giao thức chịu trách nhiệm chuyển đổi tên miền. SOC có thể thu thập thông tin về các tên miền mà các hệ thống nội bộ đang cố gắng liên lạc bằng cách chỉ kiểm tra các truy vấn DNS.

  - `Firewall logs:` Tường lửa là một thiết bị kiểm soát các gói mạng vào và ra khỏi mạng chủ yếu bằng cách cho phép chúng đi qua hoặc chặn chúng. Do đó, nhật ký tường lửa có thể tiết lộ nhiều thông tin về gói tin nào đã đi qua hoặc cố gắng đi qua tường lửa.

  - `DHCP logs:` DHCP là viết tắt của Giao thức cấu hình máy chủ động và chịu trách nhiệm gán địa chỉ IP cho các hệ thống cố gắng kết nối với mạng. Một sự tương tự của yêu cầu DHCP là khi bạn bước vào một nhà hàng sang trọng, người phục vụ chào đón bạn và hướng dẫn bạn đến một bàn trống. Biết rằng DHCP đã tự động cung cấp cho thiết bị của bạn cài đặt mạng bất cứ khi nào bạn có thể tham gia mạng mà không cần cấu hình thủ công. Bằng cách kiểm tra các giao dịch DHCP, chúng tôi có thể tìm hiểu về các thiết bị đã tham gia mạng.

![](./img_so/Screenshot%202023-07-12%20213932.png)

> `SOC Services`

- `Monitor security posture:` Đây là vai trò chính của SOC và nó bao gồm giám sát mạng và máy tính để biết các cảnh báo và thông báo bảo mật cũng như phản hồi chúng khi cần.

- `Vulnerability management:` Điều này đề cập đến việc tìm kiếm các lỗ hổng trong hệ thống của công ty và vá (sửa chữa) chúng. SOC có thể hỗ trợ thực hiện nhiệm vụ này nhưng không nhất thiết phải thực hiện nó.

- `Malware analysis:` SOC có thể khôi phục các chương trình độc hại đã xâm nhập vào mạng. SOC có thể thực hiện phân tích cơ bản bằng cách thực hiện nó trong một môi trường được kiểm soát. Tuy nhiên, phân tích nâng cao hơn yêu cầu gửi nó cho một nhóm chuyên dụng.

- `Intrusion detection:` Hệ thống phát hiện xâm nhập (IDS) được sử dụng để phát hiện và ghi lại các hành vi xâm nhập cũng như các gói đáng ngờ. Công việc của SOC là duy trì một hệ thống như vậy, theo dõi các cảnh báo của nó và xem qua nhật ký của nó khi cần thiết.

- `Reporting:` Điều cần thiết là báo cáo sự cố và báo động. Báo cáo là cần thiết để đảm bảo quy trình làm việc trôi chảy và hỗ trợ các yêu cầu tuân thủ.
