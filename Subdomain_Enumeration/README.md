# **Subdomain Enumeration**

- Chúng ta sẽ khám phá ba phương pháp liệt kê tên miền phụ khác nhau: Brute Force, OSINT (Trí thông minh nguồn mở) và Máy chủ ảo.

## **OSINT - SSL/TLS Certificates**

- Khi chứng chỉ SSL/TLS (Bảo mật lớp cổng bảo mật/Bảo mật lớp truyền tải) được tạo cho một miền bởi CA (Cơ quan cấp chứng chỉ), CA sẽ tham gia vào cái được gọi là "Nhật ký minh bạch của chứng chỉ (CT)". Đây là nhật ký có thể truy cập công khai của mọi chứng chỉ SSL/TLS được tạo cho một tên miền. Mục đích của nhật ký Tính minh bạch của chứng chỉ là ngăn chặn việc sử dụng các chứng chỉ độc hại và vô tình được tạo. Chúng tôi có thể sử dụng dịch vụ này để phát hiện các tên miền phụ thuộc về một tên miền, các trang web như <https://crt.sh> và <https://ui.ctsearch.entrust.com/ui/ctsearchui> cung cấp cơ sở dữ liệu chứng chỉ có thể tìm kiếm hiển thị hiện tại và kết quả lịch sử.

![](./img_SE/Screenshot%202023-07-13%20233643.png)

## **OSINT - Search Engines**

- Các công cụ tìm kiếm chứa hàng nghìn tỷ liên kết đến hơn một tỷ trang web, đây có thể là nguồn tài nguyên tuyệt vời để tìm các tên miền phụ mới. Sử dụng các phương pháp tìm kiếm nâng cao trên các trang web như Google, chẳng hạn như trang web: bộ lọc, có thể thu hẹp kết quả tìm kiếm. Ví dụ: `"-site:www.domain.com site:*.domain.com"` sẽ chỉ chứa các kết quả dẫn đến tên miền domain.com nhưng loại trừ mọi liên kết đến <www.domain.com>; do đó, nó chỉ hiển thị cho chúng tôi các tên miền phụ thuộc domain.com.

## **DNS Bruteforce**

- Liệt kê Bruteforce DNS (Hệ thống tên miền) là phương pháp thử hàng chục, hàng trăm, hàng nghìn hoặc thậm chí hàng triệu tên miền phụ khác nhau có thể có từ danh sách tên miền phụ thường được sử dụng được xác định trước. Vì phương pháp này yêu cầu nhiều request nên chúng tôi tự động hóa phương pháp này bằng các công cụ để giúp quá trình này diễn ra nhanh hơn. Trong trường hợp này, chúng tôi đang sử dụng một công cụ gọi là dnsrecon để thực hiện việc này.
​
![](./img_SE/Screenshot%202023-07-13%20234637.png)

## **OSINT - Sublist3r**

- Để tăng tốc quá trình khám phá tên miền phụ OSINT, chúng ta có thể tự động hóa các phương pháp trên với sự trợ giúp của các công cụ như [`Sublist3r`](https://github.com/aboul3la/Sublist3r)

![](./img_SE/Screenshot%202023-07-13%20235053.png)
