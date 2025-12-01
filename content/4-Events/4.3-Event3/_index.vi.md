---
title : "Event 3"
date :  "2025-09-09" 
weight : 3
chapter : false
pre : " <b> 4.3 </b> "
---


# Báo cáo tổng hợp: “Trụ cột Bảo mật AWS Well-Architected”

## Mục tiêu Sự kiện
* Nắm vững 5 lĩnh vực của Trụ cột Bảo mật (Security Pillar) trong Khung AWS Well-Architected.
* Hiểu các nguyên tắc bảo mật cốt lõi: Zero Trust (Không tin cậy bất kỳ ai), Least Privilege (Đặc quyền tối thiểu), và Defense in Depth (Phòng thủ chiều sâu).
* Học cách thiết kế quản lý danh tính (IAM) an toàn và bảo vệ cơ sở hạ tầng.
* Triển khai các chiến lược phát hiện liên tục và phản ứng sự cố tự động.
* Khám phá các kỹ thuật bảo vệ dữ liệu sử dụng KMS và các thực hành tốt nhất về mã hóa.

## Diễn giả
* **Các Kiến trúc sư Giải pháp Bảo mật AWS**
* **Các Chuyên gia Bảo mật Đám mây**

## Điểm nhấn Chính

### Nền tảng Bảo mật & Danh tính (IAM)
* **Nguyên tắc Cốt lõi:** Áp dụng tư duy "Zero Trust" và "Phòng thủ chiều sâu" (tạo nhiều lớp kiểm soát bảo mật).
* **Bối cảnh Mối đe dọa:** Phân tích các mối đe dọa bảo mật đám mây hàng đầu đặc thù tại thị trường Việt Nam.
* **IAM Hiện đại:** Chuyển từ việc sử dụng thông tin xác thực dài hạn (access keys) sang thông tin xác thực tạm thời sử dụng IAM Roles.
* **Kiểm soát Truy cập:** Triển khai IAM Identity Center cho SSO và sử dụng Service Control Policies (SCPs) để thiết lập ranh giới quyền hạn trong môi trường đa tài khoản (multi-account).
* **Xác thực:** Sử dụng IAM Access Analyzer để xác minh các chính sách và quyền hạn.

### Phát hiện & Bảo vệ Hạ tầng
* **Giám sát Liên tục:** Tập trung hóa khả năng quan sát với **CloudTrail** (cấp độ tổ chức), GuardDuty (phát hiện mối đe dọa), và Security Hub.
* **Chiến lược Ghi nhật ký (Logging):** Bật log tại mọi tầng—VPC Flow Logs cho lưu lượng mạng và ALB/S3 logs cho các mẫu truy cập.
* **An ninh Mạng:** Triển khai phân đoạn VPC (subnet public vs. private) và kết hợp Security Groups (stateful - có trạng thái) với NACLs (stateless - không trạng thái).
* **Bảo vệ Biên:** Sử dụng AWS WAF và AWS Shield để bảo vệ chống lại DDoS và các khai thác web.

### Bảo vệ Dữ liệu & Phản ứng Sự cố
* **Mã hóa:** Quản lý khóa với AWS KMS (xoay vòng khóa, chính sách) và đảm bảo mã hóa dữ liệu khi lưu trữ (EBS, RDS, S3) và khi truyền tải.
* **Quản lý Bí mật:** Thay thế thông tin xác thực được gắn cứng (hardcoded) bằng AWS Secrets Manager và Parameter Store.
* **Kịch bản Phản ứng Sự cố (IR Playbooks):** Định nghĩa các quy trình chuẩn cho các tình huống như lộ IAM key, vô tình public S3, và sự cố malware trên EC2.
* **Tự động hóa:** Sử dụng Lambda và Step Functions để tự động khắc phục mối đe dọa (ví dụ: cách ly một instance bị xâm nhập).

## Bài học Chính (Key Takeaways)

### Tư duy Bảo mật
* **Dịch chuyển sang trái (Shift Left):** Bảo mật phải được tích hợp sớm trong giai đoạn thiết kế, không phải thêm vào sau khi đã hoàn thành.
* **Danh tính là Vành đai mới:** Trong thế giới cloud-native, quản lý danh tính mạnh mẽ (IAM) quan trọng hơn tường lửa mạng truyền thống.
* **Giả định vi phạm (Assume Breach):** Thiết kế hệ thống với giả định rằng kẻ tấn công đã ở bên trong; tập trung vào việc giới hạn phạm vi ảnh hưởng (blast radius).

### Kiến trúc Kỹ thuật
* **Đặc quyền tối thiểu (Least Privilege):** Chỉ cấp cho người dùng và dịch vụ những quyền cần thiết để thực hiện tác vụ của họ, không hơn.
* **Phát hiện dưới dạng Mã (Detection-as-Code):** Định nghĩa các quy tắc bảo mật và cảnh báo bằng mã để đảm bảo tính nhất quán và kiểm soát phiên bản.
* **Xoay vòng Tự động:** Tự động hóa việc xoay vòng thông tin xác thực cơ sở dữ liệu và API keys để giảm thiểu tác động khi lộ thông tin.

### Ứng dụng vào Công việc
* **Kiểm toán IAM:** Rà soát IAM roles của dự án hiện tại để loại bỏ các quyền không sử dụng và bắt buộc dùng MFA cho tất cả người dùng.
* **Bảo mật Bí mật:** Di chuyển thông tin xác thực cơ sở dữ liệu từ file application.properties sang AWS Secrets Manager trong các ứng dụng Spring Boot.
* **Bật GuardDuty:** Bật GuardDuty trên tất cả các tài khoản để bắt đầu phát hiện hành vi bất thường ngay lập tức.
* **Soạn thảo Kế hoạch IR:** Tạo kịch bản Phản ứng Sự cố cơ bản cho các tình huống dễ xảy ra nhất (ví dụ: khai thác ứng dụng).

## Trải nghiệm Sự kiện

Phiên làm việc “Trụ cột Bảo mật AWS Well-Architected” đã cung cấp cái nhìn sâu sắc về việc bảo mật workload trên đám mây, cân bằng giữa các khung lý thuyết và triển khai thực tế trong bối cảnh Việt Nam.

### Học hỏi từ chuyên gia
* Hiểu sâu hơn về Mô hình Trách nhiệm Chia sẻ, làm rõ chính xác khía cạnh bảo mật nào AWS xử lý so với những gì khách hàng phải tự bảo vệ.
* Học được về những sai lầm phổ biến tại Việt Nam, chẳng hạn như vô tình để lộ dữ liệu công khai, và cách phòng tránh.

### Tiếp cận kỹ thuật thực tế
* **Mô phỏng Chính sách IAM:** Bản demo nhỏ về xác thực chính sách đã chỉ ra cách mô phỏng yêu cầu truy cập để đảm bảo quyền hạn được cấu hình chính xác trước khi triển khai.
* **Vòng đời IR:** Đi qua kịch bản "Lộ IAM Key" đã làm nổi bật tầm quan trọng của tốc độ và tự động hóa trong việc phản ứng với sự cố.

### Kết nối và thảo luận
* Thảo luận về những thách thức khi triển khai Zero Trust trong các kiến trúc ứng dụng cũ (legacy).
* Trao đổi mẹo để chuẩn bị cho kỳ thi AWS Certified Security – Specialty.

### Bài học rút ra
* **Ghi log mọi thứ:** Bạn không thể phát hiện những gì bạn không ghi lại. VPC Flow Logs và CloudTrail là thiết yếu cho việc điều tra số (forensics).
* **Tránh Key dài hạn:** Các IAM access keys tĩnh là rủi ro lớn; chuyển sang dùng IAM Roles cho EC2/Lambda là ưu tiên hàng đầu.
* **Tự động hóa là Bảo mật:** Các kiểm tra bảo mật thủ công khó mở rộng quy mô; tự động hóa sử dụng EventBridge và Lambda cho phép khắc phục theo thời gian thực.

### Ảnh sự kiện
![Photo](/images/aws3.jpg)
![Photo](/images/aws32.jpg)
![Photo](/images/aws33.jpg)