# **Nmap Live Host Discovery**

![](./img_nmap1/Screenshot%202023-08-01%20193327.png)

## **I. Subnetworks**

- Hãy xem lại một số thuật ngữ trước khi chuyển sang các nhiệm vụ chính. `Network segment` là một nhóm máy tính được kết nối bằng phương tiện dùng chung. Chẳng hạn, phương tiện có thể là bộ chuyển mạch Ethernet hoặc điểm truy cập WiFi. Trong mạng IP, mạng con thường tương đương với một hoặc nhiều `network segment` được kết nối với nhau và được định cấu hình để sử dụng cùng một bộ định tuyến. `network segment` đề cập đến kết nối vật lý, trong khi mạng con đề cập đến kết nối logic.

![](./img_nmap1/Screenshot%202023-08-01%20194827.png)

- Giao thức ARP (Giao thức phân giải địa chỉ). Một truy vấn ARP nhằm mục đích lấy thông tin địa chỉ phần cứng `MAC`

## **II. Discovering Live Hosts**

- Hãy xem lại các lớp TCP/IP được hiển thị trong hình tiếp theo. Chúng tôi sẽ tận dụng các giao thức để khám phá các máy chủ trực tiếp. Bắt đầu từ dưới lên trên, chúng ta có thể sử dụng:

![](./img_nmap1/Screenshot%202023-08-01%20201407.png)

> `Nmap Host Discovery Using ARP`

- Chỉ có thể quét ARP nếu bạn ở trên cùng mạng con với hệ thống đích. Trên Ethernet (802.3) và WiFi (802.11), bạn cần biết địa chỉ MAC của bất kỳ hệ thống nào trước khi có thể giao tiếp với hệ thống đó. Địa chỉ MAC là cần thiết cho tiêu đề lớp liên kết; tiêu đề chứa địa chỉ MAC nguồn và địa chỉ MAC đích trong số các trường khác. Để có được địa chỉ MAC, hệ điều hành sẽ gửi một truy vấn ARP. Một máy chủ trả lời các truy vấn ARP đã hoạt động. Truy vấn ARP chỉ hoạt động nếu mục tiêu nằm trên cùng một mạng con với bạn, tức là trên cùng một Ethernet/WiFi. Bạn sẽ thấy nhiều truy vấn ARP được tạo trong quá trình quét Nmap của mạng cục bộ. Nếu bạn chỉ muốn Nmap thực hiện quét ARP mà không quét cổng, bạn có thể sử dụng `nmap -PR -sn TARGETS`, trong đó -PR chỉ ra rằng bạn chỉ muốn quét ARP. Ví dụ sau đây cho thấy:

![](./img_nmap1/Screenshot%202023-08-01%20202425.png)

- Ta có thể sử dụng công cụ `arp-can`:

![](./img_nmap1/Screenshot%202023-08-01%20203156.png)

> `Nmap Host Discovery Using ICMP`

- Chúng tôi có thể ping mọi địa chỉ IP trên mạng mục tiêu và xem ai sẽ phản hồi các yêu cầu ping (ICMP Type 8/Echo) của chúng tôi bằng phản hồi ping (ICMP Type 0).

- Nhưng có nhiều tường lửa chặn ICMP echo; các phiên bản mới của MS Windows được cấu hình với tường lửa máy chủ chặn các yêu cầu tiếng vang ICMP theo mặc định.

![](./img_nmap1/Screenshot%202023-08-01%20204544.png)

> `Nmap Host Discovery Using TCP/UDP`

- TCP SYN Ping: `sudo nmap -PS -sn 10.10.68.220/24`
- TCP ACK Ping: `sudo nmap -PA -sn 10.10.68.220/24`
- UDP Ping: `sudo nmap -PU -sn 10.10.68.220/24`


## **TCP Flags**

- Nmap hỗ trợ các kiểu quét cổng TCP khác nhau. Để hiểu sự khác biệt giữa các lần quét cổng này, chúng ta cần xem lại tiêu đề TCP. Tiêu đề TCP là 24 byte đầu tiên của phân đoạn TCP. Hình dưới đây hiển thị tiêu đề TCP như được định nghĩa trong RFC 793. Hình này thoạt nhìn có vẻ phức tạp; tuy nhiên, nó khá đơn giản để hiểu. Ở hàng đầu tiên, chúng ta có số cổng TCP nguồn và số cổng đích. Chúng ta có thể thấy rằng số cổng được phân bổ 16 bit (2 byte). Ở hàng thứ hai và thứ ba, chúng ta có số thứ tự và số xác nhận. Mỗi hàng có 32 bit (4 byte) được phân bổ, với tổng số sáu hàng, chiếm 24 byte.

![](./img_nmap1/Screenshot%202023-08-01%20211804.png)

- `URG:` Cờ khẩn cấp chỉ ra rằng con trỏ khẩn cấp được gửi là quan trọng. Con trỏ khẩn cấp chỉ ra rằng dữ liệu đến là khẩn cấp và một phân đoạn TCP có cờ URG được đặt được xử lý ngay lập tức mà không cần xem xét việc phải đợi các phân đoạn TCP đã gửi trước đó.
- `ACK:` Cờ xác nhận chỉ ra rằng số xác nhận là quan trọng. Nó được sử dụng để xác nhận việc nhận một phân đoạn TCP.
- `PSH:` Đẩy cờ yêu cầu TCP chuyển dữ liệu đến ứng dụng ngay lập tức.
- `RST:` Cờ đặt lại được sử dụng để đặt lại kết nối. Một thiết bị khác, chẳng hạn như tường lửa, có thể gửi nó để xé kết nối TCP. Cờ này cũng được sử dụng khi dữ liệu được gửi đến máy chủ và không có dịch vụ nào ở đầu nhận để trả lời.
- `SYN:` Cờ đồng bộ hóa được sử dụng để bắt đầu bắt tay 3 bước TCP và đồng bộ hóa số thứ tự với máy chủ khác. Số thứ tự phải được đặt ngẫu nhiên trong quá trình thiết lập kết nối TCP.
- `FIN:` Người gửi không còn dữ liệu để gửi.

## **TCP Null Scan, FIN Scan, and Xmas Scan**

> `Null Scan`

- Quá trình quét null không đặt bất kỳ cờ nào; tất cả sáu bit cờ được đặt thành không. Bạn có thể chọn lần quét này bằng tùy chọn -sN. Một gói TCP không có cờ được đặt sẽ không kích hoạt bất kỳ phản hồi nào khi nó đến một cổng mở, như thể hiện trong hình bên dưới. Do đó, theo quan điểm của Nmap, việc thiếu phản hồi trong lần quét null cho thấy rằng cổng đang mở hoặc tường lửa đang chặn gói.

![](./img_nmap1/Screenshot%202023-08-01%20220322.png)

> `FIN Scan`

- Quá trình quét FIN sẽ gửi một gói TCP với cờ FIN được đặt. Bạn có thể chọn kiểu quét này bằng tùy chọn -sF. Tương tự, sẽ không có phản hồi nào được gửi nếu cổng TCP đang mở. Một lần nữa, Nmap không thể chắc chắn cổng đang mở hay tường lửa đang chặn lưu lượng liên quan đến cổng TCP này.

![](./img_nmap1/Screenshot%202023-08-01%20221414.png)

> `Xmas Scan`

- Quét Xmas đặt đồng thời các cờ FIN, PSH và URG. Bạn có thể chọn Xmas scan với tùy chọn -sX.Giống như quét Null và quét FIN, nếu nhận được gói RST, điều đó có nghĩa là cổng đã bị đóng. Nếu không, nó sẽ được báo cáo là đang mở|đã lọc.

![](./img_nmap1/Screenshot%202023-08-01%20221733.png)


## **TCP Maimon Scan**

- Uriel Maimon lần đầu tiên mô tả quá trình quét này vào năm 1996. Trong quá trình quét này, các bit FIN và ACK được thiết lập. Mục tiêu sẽ gửi một gói RST dưới dạng phản hồi. Tuy nhiên, một số hệ thống bắt nguồn từ BSD sẽ loại bỏ gói nếu đó là một cổng mở để lộ các cổng mở. Quá trình quét này sẽ không hoạt động trên hầu hết các mục tiêu gặp phải trong các mạng hiện đại; tuy nhiên, chúng tôi đưa nó vào phòng này để hiểu rõ hơn về cơ chế quét cổng và tư duy hack. Để chọn kiểu quét này, hãy sử dụng tùy chọn -sM.

- Hầu hết các hệ thống đích phản hồi bằng gói RST bất kể cổng TCP có mở hay không. Trong trường hợp như vậy, chúng tôi sẽ không thể khám phá các cổng đang mở. Hình dưới đây cho thấy hành vi dự kiến trong trường hợp cổng TCP mở và đóng.

![](./img_nmap1/Screenshot%202023-08-01%20223036.png)

## **Service Detection**

- Việc thêm -sV vào lệnh Nmap của bạn sẽ thu thập và xác định thông tin phiên bản và dịch vụ cho các cổng đang mở. Bạn có thể kiểm soát cường độ với --version-intensity LEVEL trong đó mức nằm trong khoảng từ 0, nhẹ nhất và 9, đầy đủ nhất. -sV --version-light có cường độ là 2, trong khi -sV --version-all có cường độ là 9.

![](./img_nmap1/Screenshot%202023-08-02%20123134.png)

## **OS Detection and Traceroute**

- Nmap có thể phát hiện Hệ điều hành (OS) dựa trên hành vi của nó và bất kỳ dấu hiệu nhận biết nào trong phản hồi của nó. Phát hiện hệ điều hành có thể được kích hoạt bằng cách sử dụng -O; đây là chữ hoa O như trong hệ điều hành.

![](./img_nmap1/Screenshot%202023-08-02%20124149.png)

- Nếu bạn muốn Nmap tìm các bộ định tuyến giữa bạn và đích, chỉ cần thêm --traceroute.

![](./img_nmap1/Screenshot%202023-08-02%20124251.png)