# **John The Ripper**

## **John Who?**

- John the Ripper là một trong những công cụ bẻ khóa băm nổi tiếng, được yêu thích và linh hoạt nhất hiện có. Nó kết hợp tốc độ bẻ khóa nhanh, với một loạt các loại băm tương thích đặc biệt.

> `What are Hashes?`

- Băm là một cách lấy một phần dữ liệu có độ dài bất kỳ và biểu diễn nó ở dạng khác có độ dài cố định. Điều này che dấu giá trị ban đầu của dữ liệu. Điều này được thực hiện bằng cách chạy dữ liệu gốc thông qua thuật toán băm. Có nhiều thuật toán băm phổ biến, chẳng hạn như MD4,MD5, SHA1 và NTLM. Hãy thử và hiển thị điều này với một ví dụ:

- Nếu chúng ta lấy "polo", một chuỗi gồm 4 ký tự- và chạy nó thông qua thuật toán băm MD5, chúng ta sẽ có kết quả là: b53759f3ce692de7aff1b5779d3964da một hàm băm MD5 tiêu chuẩn gồm 32 ký tự.

- Tương tự như vậy, nếu chúng ta lấy "polymint", một chuỗi gồm 9 ký tự- và chạy nó thông qua cùng một thuật toán băm MD5, chúng ta sẽ có kết quả là: 584b6e4f4586e136bc280f27f9c64f3b một hàm băm MD5 32 ký tự tiêu chuẩn khác.

- Các thuật toán băm được thiết kế sao cho chúng chỉ hoạt động một chiều. Điều này có nghĩa là không thể đảo ngược hàm băm đã tính toán chỉ bằng cách sử dụng đầu ra đã cho. Điều này liên quan đến một vấn đề toán học cơ bản được gọi là mối quan hệ `P vs NP`.

## **Setting up John the Ripper**

![](./img_john/Screenshot%202023-08-05%20124102.png)

## **Cracking Basic Hashes**

![](./img_john/Screenshot%202023-08-05%20124853.png)
![](./img_john/Screenshot%202023-08-05%20125154.png)

## **Cracking Windows Authentication Hashes**

-  Authentication hashes là phiên bản băm của mật khẩu được hệ điều hành lưu trữ, đôi khi có thể bẻ khóa chúng bằng các phương pháp vũ phu mà chúng tôi đang sử dụng. Để có được những hàm băm này, bạn thường phải là người dùng có đặc quyền - vì vậy chúng tôi sẽ giải thích một số hàm băm mà chúng tôi dự định bẻ khóa khi thử chúng.

> `NTHash / NTLM`

- NThash là định dạng băm mà các máy Hệ điều hành Windows hiện đại sẽ lưu trữ mật khẩu của người dùng và dịch vụ. Nó cũng thường được gọi là "NTLM" tham chiếu phiên bản trước của định dạng Windows cho mật khẩu băm được gọi là "LM", do đó là "NT/LM “.

![](./img_john/Screenshot%202023-08-05%20133851.png)

## **Cracking /etc/shadow Hashes**

- Tệp /etc/shadow là tệp trên các máy Linux nơi lưu trữ các hàm băm mật khẩu. Nó cũng lưu trữ các thông tin khác, chẳng hạn như ngày thay đổi mật khẩu cuối cùng và thông tin hết hạn mật khẩu. Nó chứa một mục trên mỗi dòng cho mỗi người dùng hoặc tài khoản người dùng của hệ thống. Tệp này thường chỉ có người dùng root mới có thể truy cập được - vì vậy để có được các giá trị băm, bạn phải có đủ đặc quyền, nhưng nếu bạn làm như vậy - có khả năng là bạn sẽ có thể bẻ khóa một số giá trị băm.

> `Unshadowing`

![](./img_john/Screenshot%202023-08-05%20134938.png)
![](./img_john/Screenshot%202023-08-05%20140043.png)

## **Cracking Password Protected Zip Files**

![](./img_john/Screenshot%202023-08-05%20140646.png)
![](./img_john/Screenshot%202023-08-05%20141057.png)

## **Cracking SSH Keys with John**
![](./img_john/Screenshot%202023-08-05%20141915.png)