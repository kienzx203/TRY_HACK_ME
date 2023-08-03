# **Windows Privilege Escalation**

## **Windows Users**

- Hệ thống Windows chủ yếu có 2 loại người dùng:
    - `Administrators:` Người dùng có nhiều đặc quyền nhất, nó có thể thay đổi bất kì tham số nào cấu hình trên máy.
    - `Standard Users:` Những người dùng có thể truy cập máy tính nhưng chỉ thực hiện được tác vụ hạn chế.

- Ngoài ra, bạn sẽ thường nghe về một số tài khoản tích hợp đặc biệt được hệ điều hành sử dụng trong bối cảnh leo thang đặc quyền:
    - `SYSTEM / LocalSystem:` Một tài khoản được hệ điều hành sử dụng để thực hiện các tác vụ nội bộ. Nó có toàn quyền truy cập vào tất cả các tệp và tài nguyên có sẵn trên máy chủ với các đặc quyền thậm chí còn cao hơn cả quản trị viên.
    - `Local Service:` Tài khoản mặc định được sử dụng để chạy các dịch vụ Windows với các đặc quyền "tối thiểu". Nó sẽ sử dụng các kết nối ẩn danh qua mạng.
    - `Network Service:` Tài khoản mặc định được sử dụng để chạy các dịch vụ Windows với các đặc quyền "tối thiểu". Nó sẽ sử dụng thông tin đăng nhập của máy tính để xác thực thông qua mạng.

## **Harvesting Passwords from Usual Spots**

> `Unattended Windows Installations (Cài đặt Windows không giám sát)`

- Khi cài đặt Windows trên một số lượng lớn máy chủ, quản trị viên có thể sử dụng Windows Deployment Services, cho phép một hình ảnh hệ điều hành đơn lẻ được triển khai cho một số máy chủ thông qua mạng. Những loại cài đặt này được gọi là cài đặt không giám sát vì chúng không yêu cầu tương tác của người dùng. Những cài đặt như vậy yêu cầu sử dụng tài khoản quản trị viên để thực hiện thiết lập ban đầu, tài khoản này có thể sẽ được lưu trữ trong máy ở các vị trí sau:
    - `C:\Unattend.xml`
    - `C:\Windows\Panther\Unattend.xml`
    - `C:\Windows\Panther\Unattend\Unattend.xml`
    - `C:\Windows\system32\sysprep.inf`
    - `C:\Windows\system32\sysprep\sysprep.xml`
- Là một phần của các tệp này, bạn có thể gặp thông tin xác thực:

```
<Credentials>
    <Username>Administrator</Username>
    <Domain>thm.local</Domain>
    <Password>MyPassword123</Password>
</Credentials>
```

> `Powershell History`

- Bất cứ khi nào người dùng chạy một lệnh bằng Powershell, nó sẽ được lưu vào một tệp lưu giữ bộ nhớ của các lệnh trước đây. Điều này hữu ích để lặp lại các lệnh bạn đã sử dụng trước đó một cách nhanh chóng. Nếu người dùng chạy một lệnh bao gồm mật khẩu trực tiếp như một phần của dòng lệnh Powershell, thì sau đó có thể truy xuất lệnh đó bằng cách sử dụng lệnh sau từ dấu nhắc cmd.exe:

    - [**CÁC LỆNH Ở ĐÂY**](https://woshub.com/powershell-commands-history/#:~:text=to%20Another%20Session%3F-,Viewing%20PowerShell%20Command%20History%20on%20Windows,all%20the%20commands%20executed%20earlier.)

> `Saved Windows Credentials`

- Windows cho phép chúng tôi sử dụng thông tin đăng nhập của người dùng khác. Chức năng này cũng cung cấp tùy chọn lưu các thông tin xác thực này trên hệ thống. Lệnh bên dưới sẽ liệt kê thông tin đăng nhập đã lưu: `cmdkey /list`

- Mặc dù bạn không thể nhìn thấy mật khẩu thực, nhưng nếu nhận thấy bất kỳ thông tin đăng nhập nào đáng để thử, bạn có thể sử dụng chúng bằng lệnh runas và tùy chọn /savecred, như bên dưới.

    - `runas /savecred /user:admin cmd.exe`

> `IIS Configuration`

- Dịch vụ thông tin Internet (IIS) là máy chủ web mặc định trên các bản cài đặt Windows. Cấu hình của các trang web trên IIS được lưu trữ trong một tệp có tên web.config và có thể lưu trữ mật khẩu cho cơ sở dữ liệu hoặc cơ chế xác thực được định cấu hình. Tùy thuộc vào phiên bản IIS đã cài đặt, chúng tôi có thể tìm thấy web.config ở một trong các vị trí sau:
    - `C:\inetpub\wwwroot\web.config`
    - `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\web.config`
- Đây là một cách nhanh chóng để tìm chuỗi kết nối cơ sở dữ liệu trên tệp:
```
type C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\web.config | findstr connectionStrings
```

## **Other Quick Wins**

> `Scheduled Tasks`

- Xem xét các tác vụ đã lên lịch trên hệ thống đích, bạn có thể thấy một tác vụ đã lên lịch bị mất tệp nhị phân hoặc nó đang sử dụng tệp nhị phân mà bạn có thể sửa đổi.

- Các tác vụ đã lên lịch có thể được liệt kê từ dòng lệnh bằng cách sử dụng lệnh scht task mà không có bất kỳ tùy chọn nào. Để truy xuất thông tin chi tiết về bất kỳ dịch vụ nào, bạn có thể sử dụng lệnh như sau:

![](./img_win/Screenshot%202023-08-03%20123243.png)

- Bạn sẽ nhận được nhiều thông tin về tác vụ, nhưng điều quan trọng đối với chúng tôi là tham số "Tác vụ cần chạy" cho biết những gì được thực thi bởi tác vụ đã lên lịch và tham số "Chạy với tư cách người dùng", hiển thị người dùng sẽ được sử dụng để thực hiện nhiệm vụ.

- Nếu người dùng hiện tại của chúng tôi có thể sửa đổi hoặc ghi đè tệp thực thi "Tác vụ cần chạy", thì chúng tôi có thể kiểm soát những gì được thực thi bởi người dùng taskusr1, dẫn đến một sự leo thang đặc quyền đơn giản. Để kiểm tra quyền truy cập tệp trên tệp thực thi, chúng tôi sử dụng icacls:

![](./img_win/Screenshot%202023-08-03%20123511.png)


- Như có thể thấy trong kết quả, nhóm BUILTIN\Users có toàn quyền truy cập (F) đối với tệp nhị phân của tác vụ. Điều này có nghĩa là chúng tôi có thể sửa đổi tệp .bat và chèn bất kỳ tải trọng nào chúng tôi muốn. Để thuận tiện cho bạn, bạn có thể tìm thấy nc64.exe trên C:\tools. Hãy thay đổi tệp bat để sinh ra một trình bao đảo ngược:

![](./img_win/Screenshot%202023-08-03%20123616.png)
![](./img_win/Screenshot%202023-08-03%20123646.png)

> `AlwaysInstallElevated`

- Các tệp trình cài đặt Windows (còn được gọi là tệp .msi) được sử dụng để cài đặt các ứng dụng trên hệ thống. Chúng thường chạy với mức đặc quyền của người dùng khởi động nó. Tuy nhiên, chúng có thể được cấu hình để chạy với các đặc quyền cao hơn từ bất kỳ tài khoản người dùng nào (ngay cả những tài khoản không có đặc quyền). Điều này có khả năng cho phép chúng tôi tạo tệp MSI độc hại chạy với đặc quyền của quản trị viên.

![](./img_win/Screenshot%202023-08-03%20125242.png)
![](./img_win/Screenshot%202023-08-03%20125310.png)

## **Abusing Service Misconfigurations**

> `Windows Services`

- Các dịch vụ Windows được quản lý bởi Service Control Manager (SCM). SCM là một quy trình chịu trách nhiệm quản lý trạng thái dịch vụ khi cần, kiểm tra trạng thái hiện tại của bất kỳ dịch vụ cụ thể nào và thường cung cấp cách định cấu hình dịch vụ.

- Mỗi dịch vụ trên máy Windows sẽ có một tệp thực thi được liên kết sẽ được SCM chạy bất cứ khi nào một dịch vụ được khởi động. Điều quan trọng cần lưu ý là các tệp thực thi của dịch vụ triển khai các chức năng đặc biệt để có thể giao tiếp với SCM và do đó, không phải bất kỳ tệp thực thi nào cũng có thể được khởi động thành công như một dịch vụ. Mỗi dịch vụ cũng chỉ định tài khoản người dùng mà dịch vụ sẽ chạy.

- Để hiểu rõ hơn về cấu trúc của một dịch vụ, hãy kiểm tra cấu hình dịch vụ apphostsvc bằng lệnh sc qc:

![](./img_win/Screenshot%202023-08-03%20134016.png)

- Ở đây, chúng ta có thể thấy rằng tệp thực thi được liên kết được chỉ định thông qua tham số BINARY_PATH_NAME và tài khoản được sử dụng để chạy dịch vụ được hiển thị trên tham số SERVICE_START_NAME.

- Dịch vụ có Danh sách kiểm soát truy cập tùy ý (DACL), cho biết ai có quyền bắt đầu, dừng, tạm dừng, trạng thái truy vấn, cấu hình truy vấn hoặc định cấu hình lại dịch vụ, trong số các đặc quyền khác. DACL có thể được nhìn thấy từ Process Hacker (có sẵn trên màn hình máy tính của bạn):

![](./img_win/Screenshot%202023-08-03%20134239.png)

> `Insecure Permissions on Service Executable`

- Nếu tệp thực thi được liên kết với một dịch vụ có các quyền yếu cho phép kẻ tấn công sửa đổi hoặc thay thế nó, thì kẻ tấn công có thể giành được các đặc quyền của tài khoản dịch vụ một cách tầm thường.

- Để hiểu cách thức hoạt động của tính năng này, hãy xem xét một lỗ hổng được tìm thấy trên Bộ lập lịch hệ thống Splinterware. Để bắt đầu, chúng tôi sẽ truy vấn cấu hình dịch vụ bằng cách sử dụng sc:

![](./img_win/Screenshot%202023-08-03%20141902.png)
![](./img_win/Screenshot%202023-08-03%20141956.png)
![](./img_win/Screenshot%202023-08-03%20142213.png)

> `Unquoted Service Paths`

![](./img_win/Screenshot%202023-08-03%20143521.png)
![](./img_win/Screenshot%202023-08-03%20143553.png)
![](./img_win/Screenshot%202023-08-03%20143626.png)
![](./img_win/Screenshot%202023-08-03%20143654.png)

> `Insecure Service Permissions`

![](./img_win/Screenshot%202023-08-03%20143856.png)
![](./img_win/Screenshot%202023-08-03%20143930.png)
![](./img_win/Screenshot%202023-08-03%20150023.png)