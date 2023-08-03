# **Linux Privilege Escalation**

## **Enumeration**

- Enumeration là bước đầu tiên bạn phải thực hiện khi có quyền truy cập hệ thống.

> `hostname`

- Đây là lệnh trả về tên máy chủ của máy đích. 

> `uname -a`

- Sẽ trả về thông tin hệ thống cung cấp cho chúng tôi.Điều nãy sẽ hữu ích khi tìm kiếm bất kỳ lỗ hổng kernel tiềm năng nào dẫn đến leo thang đặc quyền.

> `/proc/version`

- Hệ thống tệp proc (procfs) cung cấp thông tin về các quy trình hệ thống đích. Bạn sẽ tìm thấy proc trên nhiều hương vị Linux khác nhau, khiến nó trở thành một công cụ thiết yếu cần có trong kho vũ khí của bạn.

- Xem /proc/version có thể cung cấp cho bạn thông tin về phiên bản kernel và dữ liệu bổ sung, chẳng hạn như liệu trình biên dịch (ví dụ: GCC) có được cài đặt hay không.

> `/etc/issue`

- Hệ thống cũng có thể được xác định bằng cách xem tệp /etc/issue. Tệp này thường chứa một số thông tin về hệ điều hành nhưng có thể dễ dàng tùy chỉnh hoặc thay đổi.

> `sudo -l`

- Hệ thống đích có thể được cấu hình để cho phép người dùng chạy một số (hoặc tất cả) lệnh với quyền root. Lệnh `sudo -l` có thể được sử dụng để liệt kê tất cả các lệnh mà người dùng của bạn có thể chạy bằng sudo.

> `netstat`

- Lệnh netstat có thể được sử dụng với một số tùy chọn khác nhau để thu thập thông tin về các kết nối hiện có.

> `find Command`

- `find . -name flag1.txt:` find the file named “flag1.txt” in the current directory
- `find /home -name flag1.txt:` find the file names “flag1.txt” in the /home directory
- `find / -type d -name config:` find the directory named config under “/”
- `find / -type f -perm 0777:` find files with the 777 permissions (files readable, writable, and executable by all users)
- `find / -perm a=x:` find executable files
- `find /home -user frank:` find all files for user “frank” under “/home”
- `find / -mtime 10:` find files that were modified in the last 10 days
- `find / -atime 10:`find files that were accessed in the last 10 day
- `find / -cmin -60:` find files changed within the last hour (60 minutes)
- `find / -amin -60:`find files accesses within the last hour (60 minutes)
- `find / -size 50M:`find files with a 50 MB size
- `find / -writable -type d 2>/dev/null :` Find world-writeable folders
- `find / -perm -222 -type d 2>/dev/null:` Find world-writeable folders
- `find / -perm -o w -type d 2>/dev/null:` Find world-writeable folders

- `find / -perm -u=s -type f 2>/dev/null`: Tìm tệp có bit SUID, cho phép chúng tôi chạy tệp với mức đặc quyền cao hơn người dùng hiện tại.

![](./img_linux/Screenshot%202023-08-02%20195624.png)

## **`Privilege Escalation: SUID`**

- Ghi đè vào file /etc/shadow
![](./img_linux/Screenshot%202023-08-02%20213029.png)
![](./img_linux/Screenshot%202023-08-02%20213430.png)
![](./img_linux/Screenshot%202023-08-02%20213506.png)
## **`Privilege Escalation: sudo`**

- Kiểm tra bằng `sudo -l`

![](./img_linux/Screenshot%202023-08-02%20212653.png)
![](./img_linux/Screenshot%202023-08-02%20212720.png)
![](./img_linux/Screenshot%202023-08-02%20212741.png)

## **`Privilege Escalation: Capabilities`**

![](./img_linux/Screenshot%202023-08-02%20213538.png)

## **`Privilege Escalation: Cron Jobs`**

![](./img_linux/Screenshot%202023-08-02%20214614.png)
![](./img_linux/Screenshot%202023-08-02%20214801.png)
![](./img_linux/Screenshot%202023-08-02%20215048.png)

## **`Privilege Escalation: PATH`**

![](./img_linux/Screenshot%202023-08-02%20224429.png)
![](./img_linux/Screenshot%202023-08-02%20224606.png)
![](./img_linux/Screenshot%202023-08-02%20224635.png)
![](./img_linux/Screenshot%202023-08-02%20224728.png)

