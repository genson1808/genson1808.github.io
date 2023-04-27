# Introduction to ACID

four building blocks and fundamentals and first principles that build a database system.

## ACID 
**Atomicity**, **Consistency**, **Isolation** and **Durability** in Relational Database Sytem

`ACID` là một tập hợp các tính chất quan trọng của cơ sở dữ liệu (database) đảm bảo tính chính xác và độ tin cậy của các giao dịch. ACID là viết tắt của Atomicity, Consistency, Isolation và Durability.

`Atomicity`: Tính nguyên tử đảm bảo rằng một giao dịch được thực hiện hoàn toàn hoặc không được thực hiện. Trong trường hợp một giao dịch bị gián đoạn do lỗi hoặc sự cố phần cứng, tất cả các thao tác đã thực hiện sẽ bị hủy và database sẽ trở về trạng thái ban đầu.

`Consistency`: Tính nhất quán đảm bảo rằng database sẽ luôn ở trạng thái hợp lệ sau khi một giao dịch được thực hiện. Nếu một giao dịch vi phạm các ràng buộc hoặc quy tắc đã định nghĩa trong database, thì nó sẽ không được thực hiện và database sẽ trở về trạng thái ban đầu.

`Isolation`: Tính độc lập đảm bảo rằng một giao dịch không bị ảnh hưởng bởi các giao dịch khác đang được thực hiện đồng thời. Điều này đảm bảo tính nhất quán của database, ngay cả khi có nhiều người dùng thao tác với cùng một bảng dữ liệu.

`Durability`: Tính bền vững đảm bảo rằng dữ liệu sẽ không bị mất đi hoặc hỏng do sự cố phần cứng hoặc lỗi trong quá trình lưu trữ. Các giao dịch đã được xác nhận là thành công sẽ được lưu trữ và không bị mất đi nếu có sự cố xảy ra.

`----------------------------------------------------------------------------------------`

Ví dụ về tính chất `ACID` trong cơ sở dữ liệu có thể như sau:

Giả sử một ngân hàng lưu trữ thông tin tài khoản của khách hàng trong cơ sở dữ liệu. Khi một khách hàng thực hiện giao dịch (ví dụ: rút tiền), hệ thống sẽ thực hiện các bước sau đây để đảm bảo tính chính xác và độ tin cậy của giao dịch theo tính chất ACID:

`Atomicity`: Nếu khách hàng muốn rút 10 triệu đồng từ tài khoản, hệ thống sẽ kiểm tra tình trạng tài khoản để đảm bảo đủ số dư để thực hiện giao dịch. Nếu tài khoản không đủ số dư hoặc có lỗi trong quá trình thực hiện giao dịch, hệ thống sẽ hủy toàn bộ giao dịch và phục hồi lại trạng thái ban đầu của tài khoản.

`Consistency`: Trong trường hợp tài khoản không đủ số dư để rút tiền, hệ thống sẽ không thực hiện giao dịch và thông báo cho khách hàng biết về tình trạng này. Điều này đảm bảo rằng tài khoản sẽ không bị âm số dư hoặc bị sai lệch thông tin sau khi giao dịch được thực hiện.

`Isolation`: Trong khi một khách hàng đang rút tiền từ tài khoản của mình, các giao dịch khác của khách hàng khác sẽ không ảnh hưởng đến tiến trình rút tiền và ngược lại. Điều này đảm bảo tính nhất quán và độc lập của các giao dịch trong cơ sở dữ liệu.

`Durability`: Sau khi giao dịch rút tiền được xác nhận là thành công, thông tin về giao dịch sẽ được lưu trữ vào cơ sở dữ liệu và không bị mất đi nếu có sự cố phần cứng hoặc lỗi trong quá trình lưu trữ. Khách hàng có thể xem lại thông tin về giao dịch này sau này nếu cần thiết.


```mermaid
  graph TD;
      A-->B;
      A-->C;
      B-->D;
      C-->D;
```

