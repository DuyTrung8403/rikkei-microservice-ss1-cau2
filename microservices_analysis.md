
### Bảng Phân Tích Ưu Điểm & Thách Thức Của Microservices

| Tiêu chí đánh giá | Điểm sáng (Ưu điểm) | Góc khuất (Nhược điểm & Thách thức) |
| :--- | :--- | :--- |
| **Lựa chọn Công nghệ** | **Độc lập công nghệ (Polyglot):** Mỗi service có thể tự do chọn ngôn ngữ và DB phù hợp nhất (VD: Golang cho xử lý luồng, Python cho AI, Java cho Core Banking). | **Áp lực kỹ năng:** Đòi hỏi team phải có kiến thức sâu rộng về hệ thống phân tán. Việc maintain (bảo trì) nhiều loại ngôn ngữ cùng lúc có thể gây khủng hoảng nhân sự. |
| **Khả năng mở rộng (Scale)** | **Mở rộng linh hoạt (Independent Scaling):** Chỉ cần đổ thêm tài nguyên cho service nào đang bị quá tải (VD: Dồn server cho service Thanh toán ngày Sale) thay vì scale cả cục. | **Chi phí hạ tầng khổng lồ:** Phải thiết lập và duy trì hàng loạt container, máy chủ, API Gateway, Service Mesh... đắt đỏ và tốn tài nguyên hơn Monolith rất nhiều. |
| **Toàn vẹn Dữ liệu** | Mỗi service làm chủ DB riêng, không sợ bị team khác query nhầm làm chết DB, tránh bottleneck dữ liệu. | **Tính nhất quán dữ liệu (Data Consistency):** Đau đầu với giao dịch phân tán (Distributed Transactions). Mất đi tính ACID truyền thống, buộc phải xử lý bù trừ phức tạp bằng Saga Pattern / Eventual Consistency. |
| **Hiệu năng & Ổn định** | **Phân lập lỗi (Fault Isolation):** Nếu service Đánh giá sập, người dùng vẫn có thể xem sản phẩm và Mua hàng bình thường, không kéo sập toàn hệ thống. | **Độ trễ mạng (Network Latency):** Các hàm gọi nhau trong bộ nhớ (RAM) nay biến thành gọi qua mạng (HTTP/gRPC). Nếu các service gọi chéo nhau quá nhiều sẽ gây độ trễ cực lớn. |
| **Triển khai & Vận hành** | **Triển khai độc lập:** Từng team có thể tự build, tự test và tự deploy service của mình mà không cần đợi lịch release chung của cả công ty. | **Vận hành cực kỳ phức tạp:** Lỗi xảy ra ở đâu khi 1 request chạy xuyên qua 10 services? Việc giám sát (Monitor), ghi log tập trung (Centralized Logging) và theo vết (Distributed Tracing) là bắt buộc và cực khó setup. |
