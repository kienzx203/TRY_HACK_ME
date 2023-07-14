# **Network Security**

## **Introduction**

- Mạng máy tính là một nhóm các máy tính và thiết bị được kết nối với nhau. An ninh mạng tập trung vào việc bảo vệ tính bảo mật của các thiết bị này và các liên kết kết nối chúng. (Nói một cách chính xác hơn, an ninh mạng đề cập đến các thiết bị, công nghệ và quy trình để bảo vệ tính bảo mật, tính toàn vẹn và tính khả dụng của mạng máy tính và dữ liệu trên đó.)

- An ninh mạng bao gồm các giải pháp phần cứng và phần mềm khác nhau để đạt được các mục tiêu bảo mật đã đề ra. Giải pháp phần cứng đề cập đến các thiết bị bạn thiết lập trong mạng của mình để bảo vệ an ninh mạng của bạn. Chúng là phần cứng, vì vậy bạn có thể giữ chúng theo đúng nghĩa đen. Một thiết bị phần cứng có thể trông giống như hình bên dưới.

![](./img_NS/Screenshot%202023-07-12%20141137.png)

- Ví dụ về các thiết bị phần cứng bao gồm:

  - `Firewall appliance:` Tường lửa cho phép và chặn các kết nối dựa trên một bộ quy tắc được xác định trước. Nó hạn chế những gì có thể vào và những gì có thể rời khỏi mạng.

  - `Intrusion Detection System (IDS) appliance:` Một IDS phát hiện các xâm nhập mạng và hệ thống cũng như các nỗ lực xâm nhập. Nó cố gắng phát hiện những nỗ lực của kẻ tấn công để đột nhập vào mạng của bạn.

  - `Intrusion Prevention System (IPS) appliance:`IPS chặn các xâm nhập được phát hiện và các nỗ lực xâm nhập. Nó nhằm mục đích ngăn chặn những kẻ tấn công đột nhập vào mạng của bạn.

  - `Virtual Private Network (VPN) concentrator appliance:` VPN đảm bảo rằng bên thứ ba không thể đọc hoặc thay đổi lưu lượng mạng. Nó bảo vệ tính bảo mật (secrecy) và tính toàn vẹn của dữ liệu được gửi.

![](./img_NS/Screenshot%202023-07-12%20141846.png)

- Mặt khác, chúng tôi có các giải pháp bảo mật phần mềm. Các ví dụ phổ biến là:

  - `Antivirus software:` Bạn cài đặt phần mềm chống vi-rút trên máy tính hoặc điện thoại thông minh của mình để phát hiện các tệp độc hại và chặn chúng thực thi.
  - `Host firewall:` Không giống như thiết bị tường lửa, một thiết bị phần cứng, host firewall là một chương trình vận chuyển như một phần của hệ thống của bạn hoặc đó là một chương trình mà bạn cài đặt trên hệ thống của mình. Chẳng hạn, MS Windows bao gồm Tường lửa của Bộ bảo vệ Windows và Apple macOS bao gồm tường lửa ứng dụng; cả hai đều là host firewall.

![](./img_NS/Screenshot%202023-07-12%20142458.png)

## **Methodology**

![](./img_NS/Screenshot%202023-07-12%20180443.png)

1. `Recon:` kẻ tấn công cố gắng tìm hiểu càng nhiều càng tốt về mục tiêu. Các thông tin như loại máy chủ, hệ điều hành, địa chỉ IP, tên người dùng và địa chỉ email có thể giúp cuộc tấn công thành công.
2. `Weaponization:` This step refers to preparing a file with a malicious component, for example, to provide the attacker with remote access.
3. `Delivery:` Bước này đề cập đến việc chuẩn bị một tệp có thành phần độc hại, để cung cấp cho kẻ tấn công quyền truy cập từ xa.
4. `Exploitation:` Khi người dùng mở tệp độc hại, hệ thống của họ sẽ thực thi thành phần độc hại.
5. `Installation:` Bước trước đó sẽ cài đặt phần mềm độc hại trên hệ thống đích.
6. `Command & Control (C2):` Việc cài đặt thành công phần mềm độc hại cung cấp cho kẻ tấn công khả năng ra lệnh và kiểm soát đối với hệ thống đích.
7. `Actions on Objectives:` Sau khi giành quyền kiểm soát một hệ thống đích, kẻ tấn công đã đạt được mục tiêu của chúng. Một mục tiêu ví dụ là Lọc dữ liệu (đánh cắp dữ liệu của mục tiêu).

## **Practical Example of Network Security**

- Ở đây tôi thực hiện nmap địa chỉ ip để xem có những port nào đang mở :

![](./img_NS/Screenshot%202023-07-12%20181743.png)

- Tiếp theo, chúng tôi sẽ thử đăng nhập bằng thông tin đăng nhập ẩn danh để xem máy chủ FTP này có hỗ trợ đăng nhập ẩn danh hay không. Để may mắn của chúng tôi, nó đã làm việc.

![](./img_NS/Screenshot%202023-07-12%20182219.png)

- Sau đó, tôi có thể đọc file secret là file chứa mật khẩu của root. Từ đó, tôi có thể ssh và tiếp tục khai thác dưới quyền của root.

![](./img_NS/Screenshot%202023-07-12%20184450.png)
