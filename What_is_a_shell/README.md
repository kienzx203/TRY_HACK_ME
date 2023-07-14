
# **Types of Shell**

- `Reverse shells :` khi mục tiêu buộc phải thực thi mã kết nối trở lại máy tính của bạn. Trên máy tính của mình, bạn sẽ sử dụng một trong những công cụ được đề cập trong tác vụ trước để thiết lập một bộ nghe sẽ được sử dụng để nhận kết nối. Shell đảo ngược là một cách tốt để vượt qua các quy tắc tường lửa có thể ngăn bạn kết nối với các cổng tùy ý trên mục tiêu; tuy nhiên, nhược điểm là khi nhận shell từ một máy trên internet, bạn sẽ cần định cấu hình mạng của riêng mình để chấp nhận shell. Tuy nhiên, đây sẽ không phải là vấn đề trên mạng TryHackMe do phương pháp mà chúng tôi kết nối vào mạng.

- `Bind shells :` khi mã được thực thi trên mục tiêu được sử dụng để khởi động trình nghe được gắn vào trình bao trực tiếp trên mục tiêu. Điều này sau đó sẽ được mở ra internet, nghĩa là bạn có thể kết nối với cổng mà mã đã mở và thực thi mã từ xa theo cách đó. Điều này có lợi thế là không yêu cầu bất kỳ cấu hình nào trên mạng của riêng bạn, nhưng có thể bị ngăn chặn bởi tường lửa bảo vệ mục tiêu.

![](./img_shell/Screenshot%202023-07-14%20220847.png)

![](./img_shell/Screenshot%202023-07-14%20220933.png)
