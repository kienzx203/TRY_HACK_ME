# **Network Services**

## **Understanding SMB**

> `What is SMB?`

- SMB - Server Message Block Protocol là giao thức liên lạc giữa mãy chủ và máy khách. Máy chủ sử dụng để chia sẻ quyền truy cập tệp, máy in, cổng và các tài nguyên trên mạng.

- Giao thức SMB được biết đến như một giao thức yêu cầu phản hồi, nghĩa là nó truyền nhiều thông báo giữa máy khách và máy chủ để thiết lập kết nối. Máy khách kết nối với máy chủ bằng TCP/IP (thực ra là NetBIOS qua TCP/IP như được chỉ định trong RFC1001 và RFC1002), NetBEUI hoặc IPX/SPX.

![](./img_nw/Screenshot%202023-08-10%20165703.png)

- Khi họ đã thiết lập kết nối, khách hàng có thể gửi lệnh (SMB) đến máy chủ cho phép họ truy cập vào các chia sẻ, mở tệp, đọc và ghi tệp và thường thực hiện tất cả những việc bạn muốn làm với hệ thống tệp . Tuy nhiên, trong trường hợp của SMB, những việc này được thực hiện qua mạng.

## **Enumerating SMB**

- Liệt kê là quá trình thu thập thông tin về một mục tiêu để tìm ra các vectơ tấn công tiềm năng và hỗ trợ khai thác.

- Quá trình này là cần thiết để một cuộc tấn công thành công, vì lãng phí thời gian với các khai thác không hoạt động hoặc có thể làm hỏng hệ thống có thể là một sự lãng phí năng lượng. Việc liệt kê có thể được sử dụng để thu thập tên người dùng, mật khẩu, thông tin mạng, tên máy chủ, dữ liệu ứng dụng, dịch vụ hoặc bất kỳ thông tin nào khác có thể có giá trị đối với kẻ tấn công.

> `Enum4Linux`

- Enum4linux là một công cụ được sử dụng để liệt kê các cổ phiếu SMB trên cả hệ thống Windows và Linux. Về cơ bản, nó là một trình bao bọc xung quanh các công cụ trong gói Samba và giúp dễ dàng trích xuất nhanh chóng thông tin từ mục tiêu liên quan đến SMB. Nó được cài đặt theo mặc định trên Parrot và Kali.

![](./img_nw/Screenshot%202023-08-10%20172519.png)

## **Exploiting SMB**

- Mặc dù có những lỗ hổng như CVE-2017-7494 có thể cho phép thực thi mã từ xa bằng cách khai thác SMB, nhưng bạn có nhiều khả năng gặp phải tình huống mà cách tốt nhất để vào hệ thống là do cấu hình sai trong hệ thống. Trong trường hợp này, chúng tôi sẽ khai thác quyền truy cập chia sẻ SMB ẩn danh- một cấu hình sai phổ biến có thể cho phép chúng tôi lấy thông tin dẫn đến trình shell.

> `SMBClient`

- Bởi vì chúng tôi đang cố gắng truy cập vào chia sẻ SMB, nên chúng tôi cần một máy khách để truy cập tài nguyên trên máy chủ. Chúng tôi sẽ sử dụng SMBClient vì nó là một phần của bộ samba mặc định. Mặc dù nó có sẵn theo mặc định trên Kali.

![](./img_nw/Screenshot%202023-08-10%20174614.png)

![](./img_nw/Screenshot%202023-08-10%20174927.png)

- [**`Tài liệu`**](https://infosecwriteups.com/network-services-enumerating-and-exploiting-variety-of-network-services-and-misconfiguration-f9581b5a1005)

## **Understanding Telnet**

> `What is Telnet?`

- Telnet là một giao thức ứng dụng cho phép bạn, với việc sử dụng máy khách telnet, kết nối và thực thi các lệnh trên một máy từ xa đang lưu trữ máy chủ telnet.

- Máy khách telnet sẽ thiết lập kết nối với máy chủ. Sau đó, máy khách sẽ trở thành một thiết bị đầu cuối ảo - cho phép bạn tương tác với máy chủ từ xa.
- Telnet gửi tất cả các tin nhắn ở dạng văn bản rõ ràng và không có cơ chế bảo mật cụ thể. Do đó, trong nhiều ứng dụng và dịch vụ, Telnet đã được thay thế bằng SSH trong hầu hết các triển khai.

- `syntax: "telnet [ip] [port]"`

## **Understanding FTP**

> `What is FTP?`

- File Transfer Protocol (FTP) là một giao thức được sử dụng để cho phép truyền tệp từ xa qua mạng. Nó sử dụng mô hình máy khách-máy chủ để thực hiện điều này và - như chúng ta sẽ nói ở phần sau - chuyển tiếp các lệnh và dữ liệu theo một cách rất hiệu quả.

> `How does FTP work?`

- Một phiên FTP điển hình hoạt động bằng hai kênh:
    - a command (sometimes called the control) channel
    - a data channel.

> `Active vs Passive`

- Trong kết nối FTP đang hoạt động, máy khách sẽ mở một cổng và lắng nghe. Máy chủ được yêu cầu chủ động kết nối với nó.
- Trong kết nối FTP thụ động, máy chủ mở một cổng và lắng nghe (thụ động) và máy khách kết nối với nó.

## **Understanding NFS**

> `What is NFS?`

- NFS là viết tắt của "Network File System" và cho phép một hệ thống chia sẻ các thư mục và tệp với những người khác qua mạng. Bằng cách sử dụng NFS, người dùng và chương trình có thể truy cập tệp trên hệ thống từ xa gần như thể chúng là tệp cục bộ. Nó thực hiện điều này bằng cách gắn tất cả hoặc một phần của hệ thống tệp trên máy chủ. Phần của hệ thống tệp được gắn kết có thể được truy cập bởi các máy khách với bất kỳ đặc quyền nào được gán cho mỗi tệp.

> `How does NFS work?`

- Đầu tiên, máy khách sẽ yêu cầu gắn một thư mục từ một máy chủ từ xa vào một thư mục cục bộ giống như cách nó có thể gắn một thiết bị vật lý. Sau đó, dịch vụ gắn kết sẽ hoạt động để kết nối với trình nền gắn kết có liên quan bằng RPC.

- Máy chủ kiểm tra xem người dùng có quyền gắn bất kỳ thư mục nào đã được yêu cầu hay không. Sau đó, nó sẽ trả về một trình xử lý tệp xác định duy nhất từng tệp và thư mục trên máy chủ.

- Nếu ai đó muốn truy cập một tệp bằng NFS, một lệnh gọi RPC sẽ được đặt tới NFSD (daemon NFS) trên máy chủ. Cuộc gọi này có các tham số như:

    -  The file handle
    - The name of the file to be accessed
    - The user's, user ID
    - The user's group ID

- Sử dụng giao thức NFS, bạn có thể truyền tệp giữa các máy tính chạy Windows và các hệ điều hành không phải Windows khác, chẳng hạn như Linux, MacOS hoặc UNIX.

![](./img_nw/Screenshot%202023-08-10%20202703.png)

- [**`Tài Liệu`**](https://infosecwriteups.com/network-services-2-enumerating-and-exploiting-more-common-network-services-misconfigurations-e1625e1dd604)

## **Understanding SMTP**

> `What is SMTP?`

- SMTP viết tắt "Simple Mail Transfer Protocol". Nó được sử dụng để xử lý việc gửi email. Để hỗ trợ các dịch vụ email, cần có một cặp giao thức, bao gồm SMTP và POP/IMAP. Cùng với nhau, chúng cho phép người dùng gửi thư đi và truy xuất thư đến tương ứng.

- Máy chủ SMTP thực hiện ba chức năng cơ bản:

  - Nó xác minh ai đang gửi email thông qua máy chủ SMTP.
  - Nó gửi thư đi
  - Nếu thư gửi đi không thể gửi được, nó sẽ gửi lại thư cho người gửi

> `POP and IMAP`

- POP, or "Post Office Protocol" and IMAP, "Internet Message Access Protocol" à các giao thức email chịu trách nhiệm chuyển email giữa máy khách và máy chủ thư. Sự khác biệt chính là ở cách tiếp cận đơn giản hơn của POP trong việc tải hộp thư đến từ máy chủ thư về máy khách. Nơi IMAP sẽ đồng bộ hóa hộp thư đến hiện tại, với thư mới trên máy chủ, tải xuống mọi thứ mới. Điều này có nghĩa là những thay đổi đối với hộp thư đến được thực hiện trên một máy tính, qua IMAP, sẽ vẫn tồn tại nếu sau đó bạn đồng bộ hóa hộp thư đến từ một máy tính khác. Máy chủ POP/IMAP chịu trách nhiệm hoàn thành quy trình này.

![](./img_nw/Screenshot%202023-08-10%20204418.png)