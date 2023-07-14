# **Active Reconnaissance**

## **Introduction**

- Active Reconnaissance yêu cầu bạn thực hiện một số hình thức liên lạc với mục tiêu của mình. Liên hệ này có thể là một cuộc gọi điện thoại hoặc một chuyến viếng thăm công ty mục tiêu với lý do nào đó để thu thập thêm thông tin, thường là một phần của kỹ thuật xã hội. Ngoài ra, đó có thể là kết nối trực tiếp đến hệ thống đích, cho dù truy cập trang web của họ hay kiểm tra xem tường lửa của họ có mở cổng SSH hay không. Hãy nghĩ về nó giống như bạn đang kiểm tra chặt chẽ các cửa sổ và khóa cửa. Do đó, điều cần thiết là phải nhớ không tham gia vào công việc Active Reconnaissance trước khi nhận được sự ủy quyền hợp pháp có chữ ký từ khách hàng.

## **Web Browser**

- Trình duyệt web có thể là một công cụ tiện lợi, đặc biệt là nó có sẵn trên tất cả các hệ thống. Có một số cách mà bạn có thể sử dụng trình duyệt web để thu thập thông tin về mục tiêu.

- Dưới đây là ảnh chụp màn hình của Firefox Developer Tools. Chrome DevTools khá giống nhau.

![](./img_Arecon/Screenshot%202023-07-14%20104519.png)

- Ngoài ra còn có rất nhiều tiện ích bổ sung dành cho Firefox và Chrome có thể giúp kiểm tra thâm nhập. Dưới đây là một vài ví dụ:

  - `FoxyProxy` cho phép bạn nhanh chóng thay đổi máy chủ proxy mà bạn đang sử dụng để truy cập trang web mục tiêu. Tiện ích mở rộng trình duyệt này thuận tiện khi bạn đang sử dụng một công cụ như Burp Suite hoặc nếu bạn cần chuyển đổi máy chủ proxy thường xuyên. Bạn có thể tải FoxyProxy cho Firefox [`here`](https://addons.mozilla.org/en-US/firefox/addon/foxyproxy-standard).
  - `User-Agent Switcher and Manager` cung cấp cho bạn khả năng giả vờ đang truy cập trang web từ một hệ điều hành khác hoặc trình duyệt web khác. Nói cách khác, bạn có thể giả vờ đang duyệt một trang web bằng iPhone trong khi thực tế, bạn đang truy cập trang đó từ Mozilla Firefox. Bạn có thể tải xuống User-Agent Switcher and Manager cho Firefox [`here`](https://addons.mozilla.org/en-US/firefox/addon/user-agent-string-switcher).
  - `Wappalyzer` cung cấp thông tin chi tiết về các công nghệ được sử dụng trên các trang web đã truy cập. Tiện ích mở rộng như vậy rất tiện dụng, chủ yếu khi bạn thu thập tất cả thông tin này trong khi duyệt trang web giống như bất kỳ người dùng nào khác. Ảnh chụp màn hình của Wappalyzer được hiển thị bên dưới. Bạn có thể tìm Wappalyzer cho Firefox [`here`](https://addons.mozilla.org/en-US/firefox/addon/wappalyzer).

![](./img_Arecon/Screenshot%202023-07-14%20105300.png)

## **PING**

- ping là một lệnh gửi gói ICMP Echo đến một hệ thống từ xa. Nếu hệ thống từ xa đang trực tuyến và gói ping được định tuyến chính xác và không bị chặn bởi bất kỳ tường lửa nào, thì hệ thống từ xa sẽ gửi lại ICMP Echo Reply. Tương tự, phản hồi ping sẽ đến được hệ thống đầu tiên nếu được định tuyến phù hợp và không bị chặn bởi bất kỳ tường lửa nào.

- Mục tiêu của lệnh như vậy là để đảm bảo rằng hệ thống đích đang trực tuyến trước khi chúng tôi dành thời gian thực hiện các lần quét chi tiết hơn để khám phá hệ điều hành và dịch vụ đang chạy.

- Về mặt kỹ thuật, ping thuộc giao thức ICMP (Giao thức thông báo điều khiển Internet). ICMP hỗ trợ nhiều loại truy vấn, nhưng đặc biệt, chúng tôi quan tâm đến ping (ICMP echo/type 8) và ping reply (ICMP echo reply/type 0). Không bắt buộc phải truy cập chi tiết ICMP để sử dụng ping.

![](./img_Arecon/Screenshot%202023-07-14%20105708.png)

## **Traceroute**

- Traceroute command mục đích là theo dõi tìm địa chỉ IP của bộ định tuyến hoặc bước nhảy mà gói đi qua khi nó đi từ hệ thống của bạn đến máy chủ đích. Lệnh này cũng tiết lộ số lượng bộ định tuyến giữa hai hệ thống. Nó rất hữu ích vì nó cho biết số bước nhảy (bộ định tuyến) giữa hệ thống của bạn và máy chủ đích. Tuy nhiên, lưu ý rằng đường đi của các gói có thể thay đổi vì nhiều bộ định tuyến sử dụng các giao thức định tuyến động thích ứng với các thay đổi của mạng.

- Chúng tôi dựa vào ICMP để “lừa” các bộ định tuyến tiết lộ địa chỉ IP của chúng. Chúng ta có thể thực hiện điều này bằng cách sử dụng một Time To Live (TTL) nhỏ trong trường tiêu đề IP. Mặc dù T trong TTL là viết tắt của thời gian, nhưng TTL cho biết số lượng bộ định tuyến/bước nhảy tối đa mà một gói có thể đi qua trước khi bị loại bỏ; TTL không phải là số đơn vị thời gian tối đa. Khi một bộ định tuyến nhận được một gói, nó sẽ giảm TTL xuống một trước khi chuyển nó đến bộ định tuyến tiếp theo. Hình dưới đây cho thấy mỗi khi gói IP đi qua một bộ định tuyến, giá trị TTL của nó giảm đi 1. Ban đầu, nó rời khỏi hệ thống với giá trị TTL là 64; nó đến hệ thống đích với giá trị TTL là 60 sau khi đi qua 4 bộ định tuyến.

![](./img_Arecon/Screenshot%202023-07-14%20111059.png)

- Tuy nhiên, nếu TTL đạt đến 0, nó sẽ bị hủy và ICMP Time-to-Live vượt quá sẽ được gửi đến người gửi ban đầu. Trong hình dưới đây, hệ thống đặt TTL thành 1 trước khi gửi đến bộ định tuyến. Bộ định tuyến đầu tiên trên đường dẫn giảm TTL đi 1, dẫn đến TTL bằng 0. Do đó, bộ định tuyến này sẽ loại bỏ gói và gửi thông báo lỗi quá trình truyền quá thời gian ICMP. Lưu ý rằng một số bộ định tuyến được cấu hình để không gửi các thông báo ICMP như vậy khi loại bỏ một gói.

![](./img_Arecon/Screenshot%202023-07-14%20111310.png)

![](./img_Arecon/Screenshot%202023-07-14%20111336.png)

![](./img_Arecon/Screenshot%202023-07-14%20111920.png)

## **Telnet**

- Giao thức TELNET (Mạng Teletype) được phát triển vào năm 1969 để liên lạc với một hệ thống từ xa thông qua giao diện dòng lệnh (CLI). Do đó, lệnh telnet sử dụng giao thức TELNET để quản trị từ xa. Cổng mặc định được telnet sử dụng là 23. Từ góc độ bảo mật, telnet gửi tất cả dữ liệu, bao gồm tên người dùng và mật khẩu, ở dạng văn bản rõ ràng. Gửi ở dạng văn bản rõ ràng giúp bất kỳ ai có quyền truy cập vào kênh liên lạc dễ dàng đánh cắp thông tin đăng nhập. Giải pháp thay thế an toàn là giao thức SSH (Secure Shell).

- Tuy nhiên, ứng dụng khách telnet, với sự đơn giản của nó, có thể được sử dụng cho các mục đích khác. Biết rằng ứng dụng khách telnet dựa trên giao thức TCP, bạn có thể sử dụng Telnet để kết nối với bất kỳ dịch vụ nào và lấy biểu ngữ của dịch vụ đó. Sử dụng telnet MACHINE_IP PORT, bạn có thể kết nối với bất kỳ dịch vụ nào chạy trên TCP và thậm chí trao đổi một số tin nhắn trừ khi dịch vụ đó sử dụng mã hóa.

![](./img_Arecon/Screenshot%202023-07-14%20112409.png)

## **Netcat**

- Netcat hoặc đơn giản là nc có các ứng dụng khác nhau có thể có giá trị lớn đối với một pentester. Netcat hỗ trợ cả giao thức TCP và UDP. Nó có thể hoạt động như một máy khách kết nối với cổng nghe; cách khác, nó có thể hoạt động như một máy chủ lắng nghe trên cổng bạn chọn. Do đó, nó là một công cụ thuận tiện mà bạn có thể sử dụng như một máy khách hoặc máy chủ đơn giản qua TCP hoặc UDP.

![](./img_Arecon/Screenshot%202023-07-14%20112936.png)

```
Client-Side (we request over): nc <ip address> <port>
Server-Side (they request over): nc -lvnp <port>
```

- Ở phía máy chủ chúng ta có những option:

![](./img_Arecon/Screenshot%202023-07-14%20113000.png)
