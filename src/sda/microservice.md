# Microservice

## Benefits of gRPC Microservices

trong một mônlithic application, việc gọi một business action như payment service từ checkout service có nghĩa là truy cập
một method trong một module khác rất dễ dàng. Nếu sử dụng microservice

## 1.2 Monolithic architecture

Trong kiến trúc Monolithic, các components khác nhau của một Monolithic application được kết hợp thành một software application
thống nhất và single-tiered (một tầng). Nó có thể chứa các module UI, module database, module server được quản lý cùng một nơi.
Monolithic là một lựa chọn tốt, đặc biệt trong khi phát triển phiên bản đầu của sản phẩm. vì nó giúp bạn tập trung vào business domain
mà không phải giải quyết bất kỳ thách thức phi chức năng nào. Tuy nhiên, ta nên đánh giá sản phẩm định kỳ để hiểu liệu đây có phải là thời
điểm thích hợp để chuyển sang Microservice architecture hay không.

### Development

Tất cả IDE hiện đại được thiết kế để hỗ trợ monolithic applications. Tuy nhiên các vấn đề phát sinh khi codebase của ta phát triển.
Ví dụ nếu ta có hàng chục modules trong một monolithic-architecture IDE có thể giảm năng suất và overload mặc dù chúng ta không cần
sử dụng hết các modules.

Ngoài ra nếu ta không có sự cô lập các test cases ta có thể sẽ chạy hết tất cả các test cases bất cứ khi nào có sự thay đổi code base
mặc nhỏ một thay đổi nhỏ. Code base càng lớn thời gian compile và test càng lâu.

### Deployment

Triển khi một monolithic application có nghĩa copy một standalone package hoặc folder hierarchy đến server hoặc một container runtime.
Tuy nhiên khi nói đến continuous deployment (triển khai liên tục), monolithic có thể là một trở ngại cho việc triển khai thường xuyên
vò rất khó để triển khai và thử nghiệm trong một khoảng thời gian hợp lý. Ta cần deploy toàn bộ ứng dụng nagy cả khi ta chỉ thay đổi nhỏ
cho một component cụ thể. Ví dụ: giả sử ràng ta introduce một thay đổi nhỏ trong newsletter component chịu trách nhiệm phục vụ bản tin
và bay giờ ta muốn test và deploy đến production. Chúng ta cần chạy tất cả các test cases mặc dù chúng ta không thay đổi bất cứ gì trong
các component khác như payment service, product service, ...

Mặt khác việc triển khai một ứng dụng nguyên khối có thể có những vấn đề lớn hơn, đặc biệt nếu ứng dụng này được chia sẻ bởi nhiều teams.
Test sai và phá vỡ các chức năng do các nhóm khác có thể làm gián đoạn toàn bộ quá trình triển khai.

### Scaling

Monolithic application có thể dễ dàng scale bằng các đặt chúng phía sau bộ cân bằng tải. Bằng cách đó, các requests của khác hàng
sẽ proxied đến downstream monolithic application nằm trong máy chỉ vật lý hoặc container runtime. Tuy nhiên nó có thể không có ý nghĩa
từ góc độ chi phí vì các ứn dụng đó là bản sao của nhau ngay cả khi ta không cần tất cả các components được chi theo cùng tỷ lệ mức độ
ưu tiên.

Giả sử ta có một monolithic application vần 16G memory và module quan trọng nhất trong số 10 module là customer service. Khi ta scale
monolithic appication này thành 2 ta sẽ tăng lên 32G memory. Giả sử customer module cần 2G để chạy hiệu quả. Sẽ không tốt hơn nếu chúng ta
chỉ có thể mở rộng module khác hàng thêm 2G thay vì 16G.

### Scale cube

Có thể có nhiều yếu tố thúc đẩy buộc ta phải thay đổi kiến trúc của monhf và scalability là một trong số lý do performance. `Scale cube` là một là
three-dimension scalability model của một ứng dụng. các kích thước đó là X-Axis Scaling, Y-Axis Scaling, và Z-Axis Scaling.

![](../assets/scale-cube.png)

#### X-Axis Scaling

Mô hình này bao gồm chạy nhiều bản sao cùng một ứng dụng đằng sau load balancer. Trong kubernetes, load balancing được xử lý Service resource, proxies yêu cầu các backend instance có sẵn trong Pod resources. Các instance share load theo cách nếu có N bản sao mỗi instance có thể xử lý 1/N load. Một trong những nhược điểm chính của mô hình này là mỗi instance access đến all data, các instance sẽ cần nhiều memory hơn dự kiến. Ngoài ra nó không có lợi thế trong việc giảm độ phức tạp của việc phát triển codebase.

#### Z-Axis Scaling

Z-Axis Scaling cũng giống như X-Axis Scaling vì ứng dụng được copied đến instances. Sự khác biệt chính là một ứng dụng
chỉ chịu trách nhiệm cho một subset data kết thúc bằng việc tiết kiệm chi phí resources nó cũng cải thiện khả năng chịu lỗi vì chỉ một phần dữ liệu sẽ không thể truy cập được đối với user. Xây dựng một Z-Axis Scaling rất khó vì nó tạo thêm sự phức tạp cho cho ứng dụng. Ngoài ra, ta vần tìm một cách phân vùng dữ liệu thích hợp để khôi phục dữ liệu.

#### Y-Axis Scaling

Trong mô hình Y-Axis Scaling, scaling có nghĩa là là chi ứng dụng theo tính năng thay vì có nhiều bản sao của một ứng dụng. Ví dụ: ta có thể phân tách ứng dụng của ta thành một tập hợp các service có chứa một vài chức năng liên quan bên trong nó.

Microservice là một dạng của Y-Axis Scaling

### Microservice
