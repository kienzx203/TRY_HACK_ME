# **Introduction to Defensive Security**

## **Giới thiệu về Defensive Security**

- Offensive security tập trung vào một điều: đột nhập hệ thống. Việc xâm nhập vào hệ thống có thể đạt được thông qua khai thác lỗi, lạm dụng các thiết lập không an toàn và lợi dụng các chính sách kiểm soát truy cập không được thực thi. Red teams và penetration testers chuyên về Offensive security.

- Blue team là một phần của defensive security.

![](./img_ds/Screenshot%202023-07-11%20200133.png)

- Một số nhiệm vụ có liên quan đến defensive security:
  - `Nhận thức về an ninh mạng của người dùng:` Đào tạo người dùng về an ninh mạng giúp bảo vệ chống lại các cuộc tấn công khác nhau nhắm vào hệ thống của họ.
  
  - `Lập tài liệu và quản lý tài sản:` Chúng ta cần biết các loại hệ thống và thiết bị mà chúng ta phải quản lý và bảo vệ đúng cách.
  
  - `Cập nhật hệ thống và vá lỗi:` Đảm bảo rằng máy tính, máy chủ và thiết bị mạng được cập nhật và vá lỗi chính xác để chống lại mọi lỗ hổng (điểm yếu) đã biết.
  
  - `Thiết lập các thiết bị bảo mật phòng ngừa:` tường lửa và hệ thống ngăn chặn xâm nhập (IPS) là những thành phần quan trọng của bảo mật phòng ngừa. Tường lửa kiểm soát lưu lượng truy cập mạng nào có thể đi vào bên trong và những gì có thể rời khỏi hệ thống hoặc mạng. IPS chặn bất kỳ lưu lượng mạng nào phù hợp với quy tắc hiện tại và chữ ký tấn công.
  
  - `Thiết lập các thiết bị bảo mật phòng ngừa:` tường lửa và hệ thống ngăn chặn xâm nhập (IPS) là những thành phần quan trọng của bảo mật phòng ngừa. Tường lửa kiểm soát lưu lượng truy cập mạng nào có thể đi vào bên trong và những gì có thể rời khỏi hệ thống hoặc mạng. IPS chặn bất kỳ lưu lượng mạng nào phù hợp với quy tắc hiện tại và chữ ký tấn công.

![](./img_ds/Screenshot%202023-07-11%20202147.png)

## **Areas of Defensive Security**

- Chúng tôi sẽ đề cập đến hai chủ đề chính liên quan đến an ninh phòng thủ:

  - Trung tâm điều hành bảo mật (SOC), nơi chúng tôi bao gồm Thông tin tình báo về mối đe dọa
  
  - Điều tra kỹ thuật số và ứng phó sự cố (DFIR), nơi chúng tôi cũng đề cập đến Phân tích phần mềm độc hại

>`Security Operations Center (SOC)`

- `Lỗ hổng bảo mật:` Bất cứ khi nào phát hiện lỗ hổng hệ thống (điểm yếu), điều cần thiết là phải khắc phục bằng cách cài đặt bản cập nhật hoặc bản vá thích hợp. Khi không có bản sửa lỗi, các biện pháp cần thiết sẽ được thực hiện để ngăn chặn kẻ tấn công khai thác nó. Mặc dù việc khắc phục các lỗ hổng là mối quan tâm sống còn đối với SOC, nhưng nó không nhất thiết phải được chỉ định cho họ.

- `Vi phạm chính sách:` Chúng ta có thể coi chính sách bảo mật là một bộ quy tắc cần thiết để bảo vệ mạng và hệ thống. Ví dụ: có thể vi phạm chính sách nếu người dùng bắt đầu tải dữ liệu bí mật của công ty lên dịch vụ lưu trữ trực tuyến.

- `Hoạt động trái phép:` Hãy xem xét trường hợp tên đăng nhập và mật khẩu của người dùng bị đánh cắp và kẻ tấn công sử dụng chúng để đăng nhập vào mạng. SOC cần phát hiện một sự kiện như vậy và chặn nó càng sớm càng tốt trước khi có thêm thiệt hại.

- `Xâm nhập mạng:` Cho dù bảo mật của bạn tốt đến đâu, luôn có cơ hội bị xâm nhập. Xâm nhập có thể xảy ra khi người dùng nhấp vào liên kết độc hại hoặc khi kẻ tấn công khai thác máy chủ công cộng. Dù bằng cách nào, khi một sự xâm nhập xảy ra, chúng ta phải phát hiện ra nó càng sớm càng tốt để ngăn chặn thiệt hại thêm.

![](./img_ds/Screenshot%202023-07-12%20094601.png)

> `Digital Forensics and Incident Response (DFIR)`

- Digital Forensics
- Incident Response
- Malware Analysis

> Digital Forensics

- Trong defensive security, trọng tâm của Digital Forensics chuyển sang phân tích bằng chứng về một cuộc tấn công và thủ phạm cũng như các lĩnh vực khác như trộm cắp tài sản trí tuệ, gián điệp mạng và sở hữu nội dung trái phép. Do đó, Digital Forensics sẽ tập trung vào các lĩnh vực khác nhau như:

  - File System: Phân tích hình ảnh pháp y kỹ thuật số (bản sao cấp thấp) của bộ lưu trữ của hệ thống cho thấy nhiều thông tin, chẳng hạn như các chương trình đã cài đặt, tệp đã tạo, tệp bị ghi đè một phần và tệp đã xóa.
  
  - System memory: Nếu kẻ tấn công đang chạy chương trình độc hại của chúng trong bộ nhớ mà không lưu nó vào đĩa, thì việc chụp ảnh pháp y (bản sao cấp thấp) của bộ nhớ hệ thống là cách tốt nhất để phân tích nội dung của nó và tìm hiểu về cuộc tấn công.
  
  - System logs: Mỗi máy khách và máy chủ duy trì các tệp nhật ký khác nhau về những gì đang xảy ra. Tệp nhật ký cung cấp nhiều thông tin về những gì đã xảy ra trên hệ thống. Một số dấu vết sẽ được để lại ngay cả khi kẻ tấn công cố xóa dấu vết của chúng.
  
  - Network logs: Nhật ký của các gói mạng đã đi qua mạng sẽ giúp trả lời nhiều câu hỏi hơn về việc liệu một cuộc tấn công có đang xảy ra hay không và nó kéo theo những gì.
  
> Incident Response

- Một sự cố thường đề cập đến vi phạm dữ liệu hoặc tấn công mạng; tuy nhiên, trong một số trường hợp, đó có thể là một vấn đề ít nghiêm trọng hơn, chẳng hạn như cấu hình sai, nỗ lực xâm nhập hoặc vi phạm chính sách. Ví dụ về một cuộc tấn công mạng bao gồm kẻ tấn công làm cho mạng hoặc hệ thống của chúng tôi không thể truy cập được, làm hỏng (thay đổi) trang web công cộng và vi phạm dữ liệu (đánh cắp dữ liệu của công ty). Làm thế nào bạn sẽ phản ứng với một cuộc tấn công mạng? Ứng phó sự cố chỉ định phương pháp nên được tuân theo để xử lý trường hợp như vậy. Mục đích là để giảm thiệt hại và phục hồi trong thời gian ngắn nhất có thể. Lý tưởng nhất là bạn sẽ phát triển một kế hoạch sẵn sàng ứng phó với sự cố.

![](./img_ds/Screenshot%202023-07-12%20100957.png)

- Bốn giai đoạn chính của quá trình ứng phó sự cố là

  - Preparation: Điều này đòi hỏi một đội ngũ được đào tạo và sẵn sàng xử lý các sự cố. Lý tưởng nhất là các biện pháp khác nhau được đưa ra để ngăn chặn sự cố xảy ra ngay từ đầu.
  
  - Detection and Analysis: Nhóm có các nguồn lực cần thiết để phát hiện bất kỳ sự cố nào; hơn nữa, điều cần thiết là phải phân tích sâu hơn bất kỳ sự cố nào được phát hiện để tìm hiểu về mức độ nghiêm trọng của nó.
  
  - Containment, Eradication, và Recovery: Khi một sự cố được phát hiện, điều quan trọng là phải ngăn không cho nó ảnh hưởng đến các hệ thống khác, loại bỏ nó và khôi phục các hệ thống bị ảnh hưởng. Ví dụ: khi chúng tôi nhận thấy rằng một hệ thống bị nhiễm vi-rút máy tính, chúng tôi muốn ngăn chặn (ngăn chặn) vi-rút lây lan sang các hệ thống khác, làm sạch (diệt trừ) vi-rút và đảm bảo khôi phục hệ thống thích hợp.
  
  - Post-Incident Activity: Sau khi khôi phục thành công, một báo cáo sẽ được tạo và bài học kinh nghiệm được chia sẻ để ngăn chặn các sự cố tương tự trong tương lai.

> Malware Analysis

- Phần mềm đề cập đến các chương trình, tài liệu và tệp mà bạn có thể lưu trên đĩa hoặc gửi qua mạng. Phần mềm độc hại bao gồm nhiều loại, chẳng hạn như:

  - Virus là một đoạn mã (một phần của chương trình) tự gắn vào một chương trình. Nó được thiết kế để lây lan từ máy tính này sang máy tính khác; hơn nữa, nó hoạt động bằng cách thay đổi, ghi đè và xóa các tệp sau khi lây nhiễm vào máy tính. Kết quả dao động từ máy tính trở nên chậm đến không sử dụng được.
  
  - Trojan Horse là một chương trình hiển thị một chức năng mong muốn nhưng ẩn bên dưới một chức năng độc hại. Ví dụ: nạn nhân có thể tải xuống trình phát video từ một trang web mờ ám cho phép kẻ tấn công kiểm soát hoàn toàn hệ thống của họ.
  
  - Ransomware là một chương trình độc hại mã hóa các tệp của người dùng. Mã hóa làm cho các tệp không thể đọc được mà không cần biết mật khẩu mã hóa. Kẻ tấn công cung cấp cho người dùng mật khẩu mã hóa nếu người dùng sẵn sàng trả “tiền chuộc”.

- Phân tích phần mềm độc hại nhằm mục đích tìm hiểu về các chương trình độc hại đó bằng nhiều cách khác nhau:

  - Phân tích tĩnh hoạt động bằng cách kiểm tra chương trình độc hại mà không chạy nó. Thông thường, điều này đòi hỏi kiến thức vững chắc về hợp ngữ (tập lệnh của bộ xử lý, tức là các lệnh cơ bản của máy tính).
  
  - Phân tích động hoạt động bằng cách chạy phần mềm độc hại trong môi trường được kiểm soát và giám sát các hoạt động của nó. Nó cho phép bạn quan sát cách phần mềm độc hại hoạt động khi chạy.

![](./img_ds/Screenshot%202023-07-12%20102622.png)
