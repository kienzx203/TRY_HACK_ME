# **Protocols and Servers 2**

## **Introduction**

- Các máy chủ thực hiện các giao thức này phải chịu các loại tấn công khác nhau. Để đặt tên cho một số, hãy xem xét:
  - Sniffing Attack (Network Packet Capture)
  - Man-in-the-Middle (MITM) Attack
  - Password Attack (Authentication Attack)
  - Vulnerabilities

- Biết rằng chúng tôi đang bảo vệ Tính bảo mật, Tính toàn vẹn và Tính khả dụng (CIA), một cuộc tấn công nhằm mục đích gây Tiết lộ, Thay đổi và Phá hủy (DAD). Các số liệu dưới đây phản ánh điều này.

![](./img_pas2/Screenshot%202023-07-14%20152515.png)

## **Sniffing Attack**

- Sniffing attack đề cập đến việc sử dụng một công cụ chụp gói mạng để thu thập thông tin về mục tiêu. Khi một giao thức giao tiếp ở dạng văn bản rõ ràng, bên thứ ba có thể thu thập dữ liệu được trao đổi để phân tích. Việc chụp gói mạng đơn giản có thể tiết lộ thông tin, chẳng hạn như nội dung của tin nhắn riêng tư và thông tin xác thực đăng nhập, nếu dữ liệu không được mã hóa khi truyền.

- Có rất nhiều công cụ có sẵn để chụp các gói mạng. Chúng tôi xem xét những điều sau đây:
  - `Tcpdump` là một chương trình giao diện dòng lệnh (CLI) mã nguồn mở miễn phí đã được chuyển sang hoạt động trên nhiều hệ điều hành.
  - `Wireshark` là chương trình giao diện người dùng đồ họa (GUI) mã nguồn mở miễn phí có sẵn cho một số hệ điều hành, bao gồm Linux, macOS và MS Windows.
  - `Tshark` là một thay thế CLI cho Wireshark.

![](./img_pas2/Screenshot%202023-07-14%20153526.png)

![](./img_pas2/Screenshot%202023-07-14%20154023.png)

## **Man-in-the-Middle (MITM) Attack**

- Một cuộc tấn công Man-in-the-Middle (MITM) xảy ra khi nạn nhân (A) tin rằng họ đang liên lạc với một đích đến hợp pháp (B) nhưng lại vô tình liên lạc với kẻ tấn công (E). Trong hình bên dưới, chúng ta có A yêu cầu chuyển $20 cho M; tuy nhiên, E đã thay đổi thông báo này và thay thế giá trị ban đầu bằng một giá trị mới. B đã nhận được tin nhắn đã sửa đổi và hành động theo nó.

![](./img_pas2/Screenshot%202023-07-14%20155113.png)

- Cuộc tấn công này tương đối đơn giản để thực hiện nếu hai bên không xác nhận tính xác thực và tính toàn vẹn của mỗi tin nhắn. Trong một số trường hợp, giao thức đã chọn không cung cấp xác thực an toàn hoặc kiểm tra tính toàn vẹn; hơn nữa, một số giao thức có tính không an toàn cố hữu khiến chúng dễ bị tấn công kiểu này.

- Bất cứ khi nào bạn duyệt qua HTTP, bạn đều dễ bị tấn công MITM và điều đáng sợ là bạn không thể nhận ra nó. Nhiều công cụ sẽ hỗ trợ bạn thực hiện một cuộc tấn công như vậy, chẳng hạn như [`Ettercap`](https://www.ettercap-project.org/) và [`Bettercap`](https://www.bettercap.org/).

## **Transport Layer Security (TLS)**

- SSL (Lớp cổng bảo mật) bắt đầu khi web trên toàn thế giới bắt đầu thấy các ứng dụng mới, chẳng hạn như mua sắm trực tuyến và gửi thông tin thanh toán. Netscape đã giới thiệu SSL vào năm 1994, với SSL 3.0 được phát hành vào năm 1996. Nhưng cuối cùng, cần phải bảo mật nhiều hơn và giao thức TLS (Bảo mật tầng truyền tải) đã được giới thiệu vào năm 1999. Trước khi chúng tôi giải thích TLS và SSL cung cấp những gì, hãy xem chúng phù hợp với mô hình nối mạng.

- Các giao thức phổ biến mà chúng tôi đã đề cập cho đến nay gửi dữ liệu ở dạng văn bản rõ ràng; điều này giúp bất kỳ ai có quyền truy cập vào mạng đều có thể nắm bắt, lưu và phân tích các tin nhắn được trao đổi. Hình ảnh bên dưới hiển thị các lớp mạng ISO/OSI. Các giao thức mà chúng ta đã đề cập cho đến nay trong căn phòng này nằm trên lớp ứng dụng. Hãy xem xét mô hình ISO/OSI; chúng tôi có thể thêm mã hóa vào các giao thức của mình thông qua lớp trình bày. Do đó, dữ liệu sẽ được trình bày ở định dạng được mã hóa (bản mã) thay vì ở dạng ban đầu.

![](./img_pas2/Screenshot%202023-07-14%20155901.png)

- Do mối quan hệ chặt chẽ giữa SSL và TLS, một cái có thể được sử dụng thay cho cái kia. Tuy nhiên, TLS an toàn hơn SSL và thực tế nó đã thay thế SSL. Chúng tôi có thể đã bỏ SSL và chỉ viết TLS thay vì SSL/TLS, nhưng chúng tôi sẽ tiếp tục đề cập đến cả hai để tránh bất kỳ sự mơ hồ nào vì thuật ngữ SSL vẫn được sử dụng rộng rãi. Tuy nhiên, chúng ta có thể mong đợi tất cả các máy chủ hiện đại sẽ sử dụng TLS.

- Giao thức văn bản rõ ràng hiện có có thể được nâng cấp để sử dụng mã hóa qua SSL/TLS. Chúng tôi có thể sử dụng TLS để nâng cấp HTTP, FTP, SMTP, POP3 và IMAP, v.v. Bảng sau đây liệt kê các giao thức mà chúng tôi đã đề cập và các cổng mặc định của chúng trước và sau khi nâng cấp mã hóa qua SSL/TLS. Danh sách này không đầy đủ; tuy nhiên, mục đích là để giúp chúng ta hiểu rõ hơn về quy trình.

![](./img_pas2/Screenshot%202023-07-14%20160642.png)

- HTTPS yêu cầu ít nhất ba bước sau:

  - `Thiết lập kết nối TCP`
  - `Thiết lập kết nối SSL/TLS`
  - `Gửi yêu cầu HTTP đến máy chủ web`

![](./img_pas2/Screenshot%202023-07-14%20160822.png)

- `1.`Máy khách gửi ClientHello đến máy chủ để cho biết các khả năng của nó, chẳng hạn như các thuật toán được hỗ trợ.

- `2.`Máy chủ phản hồi bằng ServerHello, cho biết các tham số kết nối đã chọn. Máy chủ cung cấp chứng chỉ của nó nếu yêu cầu xác thực máy chủ. Chứng chỉ là một tệp kỹ thuật số để nhận dạng chính nó; nó thường được ký điện tử bởi bên thứ ba. Ngoài ra, nó có thể gửi thông tin bổ sung cần thiết để tạo khóa chính, trong thông báo ServerKeyExchange của nó, trước khi gửi thông báo ServerHelloDone để cho biết rằng quá trình đàm phán đã hoàn tất.

- `3.`Máy khách phản hồi bằng ClientKeyExchange, chứa thông tin bổ sung cần thiết để tạo khóa chính. Hơn nữa, nó chuyển sang sử dụng mã hóa và thông báo cho máy chủ bằng thông báo ChangeCipherSpec.

- `4.`Máy chủ cũng chuyển sang sử dụng mã hóa và thông báo cho máy khách trong thông báo ChangeCipherSpec.
