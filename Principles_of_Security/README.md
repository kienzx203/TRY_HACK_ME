# **Principles of Security**

## **The CIA Triad**

- Bộ ba CIA là một mô hình bảo mật thông tin được sử dụng để xem xét trong suốt quá trình tạo chính sách bảo mật. Mô hình này có một nền tảng rộng lớn, từ khi được sử dụng vào năm 1998.

![](./img_cia/Screenshot%202023-07-13%20114038.png)

> `Confidentiality`

- Yếu tố này là bảo vệ dữ liệu khỏi truy cập trái phép và lạm dụng. Các tổ chức sẽ luôn có một số dạng dữ liệu nhạy cảm được lưu trữ trên hệ thống của họ. Cung cấp tính bảo mật là bảo vệ dữ liệu này khỏi các bên mà nó không dành cho.

> `Integrity`

- Yếu tố bộ ba CIA về tính toàn vẹn là điều kiện để thông tin được lưu giữ chính xác và nhất quán trừ khi thực hiện các thay đổi được phép. Thông tin có thể thay đổi do truy cập và sử dụng bất cẩn, lỗi trong hệ thống thông tin hoặc truy cập và sử dụng trái phép. Trong bộ ba CIA, tính toàn vẹn được duy trì khi thông tin không thay đổi trong quá trình lưu trữ, truyền và sử dụng mà không liên quan đến việc sửa đổi thông tin. Các bước phải được thực hiện để đảm bảo dữ liệu không thể bị thay đổi bởi những người không được ủy quyền (ví dụ: vi phạm tính bảo mật).

> `Availability`

- Tính khả dụng thường là một tiêu chuẩn quan trọng đối với một tổ chức. Ví dụ: có 99,99% thời gian hoạt động trên các trang web hoặc hệ thống của họ (điều này được nêu trong Thỏa thuận cấp độ dịch vụ). Khi một hệ thống không có sẵn, nó thường dẫn đến thiệt hại cho danh tiếng của tổ chức và tổn thất tài chính. Tính khả dụng đạt được thông qua sự kết hợp của nhiều yếu tố, bao gồm:

  - Có phần cứng đáng tin cậy và đã được kiểm tra tốt cho máy chủ công nghệ thông tin của họ (tức là máy chủ có uy tín)
  - Có công nghệ và dịch vụ dự phòng trong trường hợp lỗi của chính
  - Triển khai các giao thức bảo mật thành thạo để bảo vệ công nghệ và dịch vụ khỏi bị tấn công

![](./img_cia/Screenshot%202023-07-13%20114557.png)

## **Principles of Privileges**

- Mức độ tiếp cận dành cho các cá nhân được xác định dựa trên hai yếu tố chính:

  - Vai trò/chức năng của cá nhân trong tổ chức
  - Độ nhạy của thông tin được lưu trữ trên hệ thống

- Hai khái niệm chính được sử dụng để gán và quản lý quyền truy cập của các cá nhân, hai khái niệm chính được sử dụng: Quản lý nhận dạng đặc quyền (PIM - Privileged Identity Management) và Quản lý truy cập đặc quyền (PAM - Privileged Access Managemen).

- Điều cần thiết khi thảo luận về đặc quyền và kiểm soát truy cập là nguyên tắc đặc quyền tối thiểu. Đơn giản, người dùng nên được cung cấp số lượng đặc quyền tối thiểu và chỉ những đặc quyền thực sự cần thiết để họ thực hiện nhiệm vụ của mình. Những người khác sẽ có thể tin tưởng những gì mọi người viết cho.

![](./img_cia/Screenshot%202023-07-13%20115206.png)


-
