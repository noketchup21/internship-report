---
title: "Đề xuất"
date: "2025-09-09"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Ứng dụng Web Lên Kế hoạch Bữa ăn

### 1. Tóm tắt Dự án (Executive Summary)

Nền tảng Kinh doanh Nguyên liệu Thực phẩm Cá nhân hóa tập trung vào việc cung cấp nguyên liệu tươi ngon cùng với các công thức nấu ăn tùy chỉnh để hỗ trợ các mục tiêu sức khỏe và thể hình. Người dùng đăng ký tài khoản để truy cập cơ sở dữ liệu công thức đa dạng, nhận gợi ý bữa ăn dựa trên AI theo nhu cầu dinh dưỡng (giảm cân, tăng cơ hoặc cân bằng sức khỏe) và lịch sử mua hàng. Hệ thống cho phép tùy chỉnh khẩu phần, tính toán chính xác calo/macro (dưỡng chất vĩ mô), và đặt hàng nguyên liệu trực tiếp với dịch vụ giao hàng tận nơi, đảm bảo sự tiện lợi và chất lượng. Tận dụng AWS Serverless, nền tảng đảm bảo khả năng mở rộng linh hoạt, hiệu suất cao và quản lý bảo mật.

---

### 2. Báo cáo Vấn đề (Problem Statement)

### Vấn đề là gì?

Người dùng thường gặp khó khăn trong việc lên kế hoạch cho các bữa ăn lành mạnh, tính toán lượng calo và macro, cũng như tìm nguồn nguyên liệu phù hợp với các mục tiêu thể hình như giảm cân hoặc tăng cơ. Các nền tảng hiện có cung cấp gợi ý công thức và thực đơn nhưng thiếu tính năng bán nguyên liệu trực tiếp, buộc người dùng phải tự tìm mua nguồn cung cấp, việc này tốn thời gian và dễ dẫn đến sai sót trong việc chia khẩu phần.

### Giải pháp

Nền tảng sử dụng Spring Boot cho backend REST API mạnh mẽ để xử lý đăng ký người dùng, quản lý công thức, giỏ hàng và xử lý đơn hàng; kết hợp với React mang lại frontend thân thiện với người dùng cùng các đề xuất bữa ăn do AI điều khiển. Dữ liệu được lưu trữ trong AWS RDS (PostgreSQL), hình ảnh và tài sản tĩnh (static assets) trong Amazon S3, với backend được triển khai trên Amazon EC2 trong một VPC bảo mật và Route 53 quản lý tên miền. Người dùng có thể tùy chỉnh khẩu phần, nhận gợi ý công thức cá nhân hóa và đặt mua nguyên liệu để được giao hàng. Các tính năng chính bao gồm thư viện công thức đa dạng, tính toán calo chính xác, tích hợp CI/CD qua GitHub Actions hoặc AWS CodePipeline và chi phí vận hành thấp.

### Lợi ích và Tỷ suất Hoàn vốn (ROI)

Giải pháp này thiết lập một nền tảng toàn diện cho startup về dinh dưỡng để mở rộng dịch vụ đồng thời thu thập dữ liệu người dùng nhằm nâng cao hệ thống gợi ý. Nó loại bỏ việc tính toán calo thủ công và việc mua sắm rời rạc thông qua một hệ thống tích hợp, đơn giản hóa việc lập kế hoạch dinh dưỡng và thúc đẩy doanh thu từ việc bán nguyên liệu. Chi phí hàng tháng ước tính là $17.43 (theo Công cụ tính giá AWS), tổng cộng khoảng $209 cho 12 tháng. Việc phát triển tận dụng các framework mã nguồn mở, không phát sinh thêm chi phí phần cứng. ROI dự kiến đạt được trong vòng 6–12 tháng thông qua việc tiết kiệm thời gian cho người dùng và doanh thu đơn hàng ổn định.

---

### 3. Kiến trúc Giải pháp (Solution Architecture)

Nền tảng tận dụng **kiến trúc AWS** bảo mật, có khả năng mở rộng và tự động hóa để lưu trữ và triển khai các ứng dụng web theo các phương pháp **CI/CD** tốt nhất. Nó tích hợp tự động hóa cơ sở hạ tầng, tính sẵn sàng cao và phân phối nội dung toàn cầu bằng các dịch vụ AWS. Mã nguồn được quản lý trong **GitLab** và tự động triển khai đến các instance **EC2** riêng tư thông qua **CodePipeline** và **CodeDeploy**. Bảo mật được thực thi ở nhiều lớp thông qua **IAM**, **WAF** và **Secrets Manager**, trong khi **CloudFront**, **ALB** và **Auto Scaling** đảm bảo hiệu suất và khả năng phục hồi. Giám sát và ghi nhật ký được quản lý thông qua **CloudWatch** và **CloudTrail**. Kiến trúc được chi tiết dưới đây:

![Sơ đồ Kiến trúc](/images/AWS_Architecture.drawio_6.png)

## Các Dịch vụ AWS Được Sử dụng

- **Amazon Route 53:** Quản lý DNS và định tuyến lưu lượng người dùng đến CloudFront.
- **AWS WAF:** Bảo vệ ứng dụng khỏi DDoS và các lỗ hổng web phổ biến.
- **Amazon CloudFront:** Lưu trữ bộ nhớ đệm (cache) và phân phối nội dung toàn cầu để giảm thiểu độ trễ.
- **Application Load Balancer (ALB):** Phân phối các yêu cầu đến trên các instance EC2 trong nhiều Vùng sẵn sàng (Availability Zones).
- **Amazon EC2 (Auto Scaling Group):** Chạy khối lượng công việc ứng dụng với khả năng mở rộng linh hoạt để đạt hiệu suất cao và chi phí hiệu quả.
- **Amazon S3 (Media Storage):** Lưu trữ nội dung tĩnh, hình ảnh, video và các tài sản phương tiện khác.
- **Amazon S3 (Code Storage):** Lưu trữ các bản tạo phẩm (build artifacts) và các gói triển khai được tạo bởi quy trình CI/CD.
- **AWS CodePipeline:** Tự động hóa quy trình tích hợp và triển khai liên tục.
- **AWS CodeBuild:** Xây dựng (build) và kiểm thử mã nguồn trước khi triển khai.
- **AWS CodeDeploy:** Tự động hóa việc triển khai ứng dụng lên các instance EC2.
- **AWS IAM:** Quản lý kiểm soát truy cập và quyền hạn một cách bảo mật trên các dịch vụ AWS.
- **AWS Secrets Manager:** Lưu trữ và bảo vệ các thông tin nhạy cảm như mật khẩu và khóa API.
- **Amazon Cognito:** Cung cấp quản lý xác thực và ủy quyền người dùng.
- **Amazon CloudWatch:** Giám sát các chỉ số hệ thống và ứng dụng, kích hoạt cảnh báo và thu thập nhật ký (logs).
- **AWS CloudTrail:** Ghi lại tất cả hoạt động API cho mục đích kiểm toán và tuân thủ.
- **VPC (Virtual Private Cloud):** Cung cấp môi trường mạng biệt lập để triển khai ứng dụng an toàn.
- **NAT Gateway:** Cho phép truy cập Internet chiều đi từ các subnet riêng tư (private subnets) một cách có kiểm soát và an toàn.
- **Internet Gateway (IGW):** Kết nối VPC với Internet công cộng để định tuyến và truy cập dịch vụ.
- **VPC Endpoints:** Cho phép kết nối riêng tư giữa các tài nguyên VPC và các dịch vụ AWS (như S3 và CloudWatch) mà không cần đi qua Internet.

## Thiết kế Thành phần

### Mạng (Networking)

Cơ sở hạ tầng được triển khai trong một **VPC** trải rộng trên nhiều **Vùng sẵn sàng (Availability Zones - AZ)** để đảm bảo tính sẵn sàng cao.  
Mỗi AZ bao gồm:

- Một **Public Subnet** chứa **NAT Gateway** và **Internet Gateway (IGW)** cho truy cập Internet chiều đi.
- Một **Private Subnet** chạy **Tầng Ứng dụng (Application Tier)** và **Tầng Dữ liệu (Data Tier)**, được cách ly khỏi lưu lượng công cộng.

Các subnet riêng tư giao tiếp an toàn với các dịch vụ AWS (như S3) thông qua **VPC Endpoints**, đảm bảo không có lưu lượng nào rời khỏi mạng AWS.

### Quản lý Lưu lượng (Traffic Management)

Người dùng truy cập ứng dụng thông qua **Route 53**, dịch vụ này định tuyến các yêu cầu DNS đến **CloudFront** để lưu trữ và phân phối nội dung toàn cầu.  
**AWS WAF** cung cấp bảo vệ web và lọc các yêu cầu độc hại trước khi lưu lượng đến **Application Load Balancer (ALB)**.  
**ALB** phân phối các yêu cầu đến các instance EC2 được quản lý trong một **Auto Scaling Group** trên nhiều Vùng sẵn sàng.

### Tầng Ứng dụng (Application Layer)

**Auto Scaling Group** trong các subnet riêng tư lưu trữ các instance ứng dụng, được quản lý tự động dựa trên nhu cầu.  
Các ứng dụng có thể tiếp cận an toàn các tài nguyên bên ngoài thông qua **NAT Gateway** để cập nhật hoặc gọi API.

### Tầng Dữ liệu (Data Tier)

Tầng dữ liệu nằm trong các subnet riêng tư để bảo mật tối đa, giao tiếp nội bộ với tầng ứng dụng và lưu trữ AWS thông qua **VPC Endpoints**.

### Lưu trữ (Storage)

Hai loại lưu trữ được sử dụng:

- **Media Storage (Amazon S3):** Lưu trữ tài sản tĩnh và tệp phương tiện có thể truy cập qua VPC Endpoint.
- **Code Storage (Amazon S3):** Lưu trữ các bản tạo phẩm và gói triển khai được tạo bởi quy trình CI/CD.

### Quy trình CI/CD

Các nhà phát triển commit mã nguồn lên **GitLab**, kích hoạt **AWS CodePipeline**.  
Quy trình tự động hóa:

1. **CodeBuild:** Xây dựng và kiểm thử mã nguồn.
2. **CodeStorage (S3):** Lưu các bản tạo phẩm (build artifacts).
3. **CodeDeploy:** Triển khai các gói ứng dụng lên các instance EC2 trong subnet riêng tư.

Thiết lập này đảm bảo tích hợp và phân phối liên tục trong môi trường AWS an toàn và tự động.

### Bảo mật (Security)

Bảo mật được thực thi ở nhiều lớp:

- **IAM** để kiểm soát truy cập và quyền hạn.
- **Cognito** để xác thực và ủy quyền người dùng.
- **WAF** để bảo vệ ứng dụng web.
- **Secrets Manager** để lưu trữ khóa API và thông tin xác thực an toàn.  
  Lưu lượng giữa các thành phần bị hạn chế bằng cách sử dụng mạng riêng, NAT Gateway và VPC Endpoints.

### Giám sát & Ghi nhật ký (Monitoring & Logging)

**CloudWatch** theo dõi các chỉ số hiệu suất và cung cấp cảnh báo thời gian thực.  
**CloudTrail** ghi lại tất cả các cuộc gọi API cho mục đích kiểm toán và tuân thủ.

### Lợi ích Kiến trúc

- **Tính sẵn sàng cao:** Triển khai Đa vùng (Multi-AZ) với ALB và Auto Scaling.
- **Bảo mật nâng cao:** Bảo vệ nhiều lớp qua WAF, IAM và Secrets Manager.
- **Tự động hóa hoàn toàn:** CI/CD kích hoạt bởi GitLab với CodePipeline, CodeBuild và CodeDeploy.
- **Mạng riêng tư:** Giao tiếp nội bộ an toàn qua VPC Endpoints và private subnets.
- **Hiệu suất tối ưu:** Bộ nhớ đệm nội dung CloudFront và định tuyến phân tán thông qua Route 53.

---

### 4. Triển khai Kỹ thuật

**Các Giai đoạn Triển khai** Dự án này có hai phần—phát triển backend Spring Boot và frontend React, sau đó triển khai trang web lên AWS bằng các dịch vụ AWS, mỗi phần tuân theo 4 giai đoạn:

- **Xây dựng lý thuyết và Vẽ kiến trúc:** Thu thập yêu cầu cho trang web kế hoạch bữa ăn, thiết kế kiến trúc hệ thống (Spring Boot REST API + React frontend), và định nghĩa lược đồ cơ sở dữ liệu (Tháng 1).
- **Phát triển, Kiểm thử:** Triển khai Spring Boot backend với các REST API (xác thực, quản lý người dùng, CRUD bữa ăn/công thức, giỏ hàng, v.v.), và xây dựng React frontend (UI/UX, định tuyến, biểu mẫu, quản lý trạng thái). Thực hiện unit test cho các dịch vụ backend, integration test cho các API endpoint, và frontend test (Jest/React Testing Library). (Tháng 1–2).
- **Tính toán Giá và Kiểm tra Tính khả thi:** Sử dụng AWS Pricing Calculator để ước tính chi phí cho EC2 (lưu trữ backend), RDS (cơ sở dữ liệu), S3 (tệp tĩnh và hình ảnh), VPC (mạng), Route 53 (tên miền), sau đó điều chỉnh nếu cần (Tháng 2).
- **Tích hợp AWS:** Tích hợp các dịch vụ AWS vào ứng dụng. Triển khai trang web trên **EC2**, lưu trữ hình ảnh trên **S3**, cấu hình **Cơ sở dữ liệu trên EC2**, sử dụng **VPC** để quản lý mạng, **Route 53** cho tên miền, và thiết lập quy trình CI/CD (GitHub Actions hoặc AWS CodePipeline). Thực hiện kiểm thử staging trước khi phát hành chính thức (production). (Tháng 3).

### Yêu cầu Kỹ thuật

- **Backend (Spring Boot):** REST API cho xác thực, quản lý người dùng, CRUD bữa ăn/công thức, giỏ hàng và xử lý đơn hàng. Bao gồm bảo mật (JWT, Spring Security), xác thực dữ liệu (validation) và tích hợp với AWS RDS.
- **Frontend (React):** Ứng dụng web thích ứng (responsive) với UI/UX thân thiện, định tuyến (React Router), quản lý trạng thái (Redux hoặc Context API), và tích hợp API với Spring Boot backend.
- **Cơ sở dữ liệu (AWS EC2 Database):** Một cơ sở dữ liệu được lưu trữ trên một instance EC2 (MySQL/PostgreSQL cài đặt trên máy chủ) để lưu trữ người dùng, công thức, kế hoạch bữa ăn, giỏ hàng và dữ liệu đơn hàng.
- **Lưu trữ (AWS S3):** Được sử dụng để lưu trữ các tệp build React tĩnh và hình ảnh do người dùng tải lên (ví dụ: hình ảnh công thức, ảnh đại diện).
- **Lưu trữ & Mạng (AWS EC2 + VPC):** Backend Spring Boot được triển khai trên các instance EC2, được bảo mật và cách ly trong một VPC để kiểm soát mạng và truy cập.
- **Quản lý Tên miền (AWS Route 53):** Cấu hình tên miền tùy chỉnh và quản lý DNS cho trang web.
- **CI/CD (GitHub Actions hoặc AWS CodePipeline):** Quy trình xây dựng, kiểm thử và triển khai tự động cho cả backend và frontend.
- **Xác thực & Bảo mật:** Xác thực JWT và cấu hình HTTPS; tùy chọn AWS Cognito để quản lý truy cập người dùng.

---

### 5. Mốc thời gian & Các cột mốc quan trọng

### Mốc thời gian Dự án

- **Tiền dự án (Tháng 1):** Thành lập nhóm, phân công vai trò (backend, frontend, triển khai AWS), thu thập yêu cầu và phác thảo kiến trúc hệ thống ban đầu.
- **Thực hiện Dự án (Tháng 1–3):** 3 tháng.
  - **Tháng 1:** Xây dựng lý thuyết và vẽ kiến trúc (thiết kế backend Spring Boot + frontend React, lược đồ cơ sở dữ liệu). Bắt đầu phát triển ban đầu cho backend và frontend.
  - **Tháng 2:** Tiếp tục phát triển backend và frontend, thực hiện unit test và integration test. Sử dụng AWS Pricing Calculator để đánh giá chi phí lưu trữ và tinh chỉnh kiến trúc để tối ưu chi phí.
  - **Tháng 3:** Tích hợp các dịch vụ AWS (EC2, S3, VPC, Route 53), cấu hình quy trình CI/CD, tiến hành kiểm thử staging và triển khai trang web ra production.
- **Sau khi ra mắt (Post-Launch):** Lên đến 3 tháng để bảo trì, tối ưu hóa và nâng cấp tính năng (ví dụ: mở rộng backend, cải thiện UI/UX, thêm các tính năng kế hoạch bữa ăn mới).

---

### 6. Ước tính Ngân sách

### Các Dịch vụ AWS

- Amazon Route 53: $0.9/tháng (1 Hosted zone, 1 triệu truy vấn chuẩn mỗi tháng, 1 Kiểm tra cơ bản trong AWS)
- AWS WAF: $11.6/tháng (1 Web ACL, 4 Quy tắc mỗi Web ACL, 2 Nhóm quy tắc được quản lý mỗi Web ACL, 1 triệu yêu cầu web nhận được)
- Amazon CloudFront: $0.06/tháng (Châu Á Thái Bình Dương: 1 GB/tháng Truyền dữ liệu ra origin)
- Application Load Balancer (ALB): $18.63/tháng (1 ALB, 10 GB byte xử lý/tháng, 1 kết nối mới/giây, thời lượng kết nối 1 giây, 2 yêu cầu/giây, 3 quy tắc đánh giá/yêu cầu)
- Amazon EC2 Application: $21.68/tháng (Shared Instances, Linux, Lưu lượng tăng đột biến hàng ngày, Baseline 1, Peak 2, thời gian peak 3 giờ, t3.small, On-Demand)
- Amazon EC2 Data Tier: $9.78/tháng (Shared Instances, Linux, t4g.small, EC2 Instances Savings Plans)
- Amazon EC2 Nat Instances: $17.23/tháng (2 Shared Instances, Sử dụng liên tục, Linux, t3a.micro)
- Amazon S3: $3.72/tháng (1GB/tháng lưu trữ Standard, kích thước đối tượng trung bình 1MB, 10,000 yêu cầu PUT/COPY/POST/LIST, 100,000 yêu cầu GET/SELECT, 1GB Data Transfer In, 30GB Data Transfer Out)
- AWS CodePipeline: $0 (1 pipeline hoạt động loại V1, 60 phút thực thi hành động loại V2)
- AWS CodeBuild: $0 (On-Demand Lambda Compute, 3 lần build/tháng, thời gian build trung bình 10 giây, lambda.arm.2GB, Linux)
- AWS CodeDeploy: $0
- AWS Secrets Manager: $0.4/tháng (1 secret, thời gian trung bình 30 ngày, 5 cuộc gọi API/tháng)
- Amazon Cognito: $14.25/tháng (1000 người dùng hoạt động hàng tháng (MAU), tắt tính năng bảo mật nâng cao, 1000 MAU đăng nhập qua SAML/OIDC)
- Amazon CloudWatch: $4.91/tháng (7 Metrics, 7 GetMetricData, 3 GetMetricWidgetImage, 5 API requests khác, 1GB Standard Logs Ingested, 1GB Infrequent Access Logs Ingested, 2 Dashboards, 5 Alarms, 1000 khách truy cập web, 20 sự kiện RUM/lượt truy cập)
- AWS CloudTrail: $1.77/tháng (1 sự kiện quản lý ghi, 1 sự kiện quản lý đọc, 1 thao tác S3, 1GB dữ liệu nhập, 1GB lưu trữ dữ liệu)
- VPC Endpoints: $16.05/tháng (1 địa chỉ IPv4 công cộng đang sử dụng, 20GB/tháng truyền dữ liệu nội vùng, 100GB/tháng truyền dữ liệu ra ngoài)

**Tổng cộng: $120.98/tháng, $1451.76/12 tháng**

---

### 7. Đánh giá Rủi ro

### Ma trận Rủi ro

- Gián đoạn mạng (Network Outages): Tác động trung bình / Xác suất trung bình.
- Sự cố EC2 / ALB / AZ: Tác động cao / Xác suất thấp–trung bình.
- Lỗi triển khai (CodePipeline / CodeDeploy): Tác động trung bình / Xác suất trung bình.
- Rò rỉ bí mật hoặc cấu hình sai IAM: Tác động cao / Xác suất thấp–trung bình.
- Tấn công ứng dụng (OWASP / DDoS): Tác động cao / Xác suất thấp–trung bình.
- Mất mát tạo phẩm S3 hoặc phiên bản: Tác động trung bình / Xác suất thấp.
- Vượt ngân sách (Cost Overruns): Tác động trung bình / Xác suất trung bình.
- Khoảng trống giám sát (Monitoring Gaps): Tác động trung bình / Xác suất trung bình.
- Cấu hình sai VPC hoặc Endpoint: Tác động cao / Xác suất thấp.

### Chiến lược Giảm thiểu

- Mạng / Tính sẵn sàng: Đa vùng (Multi-AZ) + Auto Scaling + ALB; kiểm tra sức khỏe (health checks); bộ nhớ đệm CloudFront; chuyển đổi dự phòng Route 53. Sử dụng CloudFront caching để giảm phụ thuộc vào các dịch vụ backend.
- Tính toán / Triển khai: Triển khai Blue/Green hoặc Canary; tạo phẩm S3 bất biến; môi trường staging và kiểm thử tích hợp trong CodeBuild trước khi ra production.
- Bảo mật / Bí mật: IAM đặc quyền tối thiểu (Least-privilege); Secrets Manager với tính năng xoay vòng và ghi nhật ký truy cập; bảo vệ WAF/Shield.
- Dữ liệu / Lưu trữ: S3 versioning & replication; sao lưu/snapshot định kỳ; VPC Endpoints cho truy cập riêng tư.
- Giám sát / Phát hiện: Dashboard CloudWatch, chỉ số, cảnh báo và lưu giữ nhật ký; bật CloudTrail, GuardDuty và AWS Config; cảnh báo qua SNS hoặc Slack.
- Quản lý Chi phí: AWS Budgets & Cost Explorer; chọn đúng kích cỡ (rightsizing); sử dụng Reserved hoặc Spot instances khi phù hợp.

### Kế hoạch Dự phòng

- Tự động quay lại phiên bản trước (rollback) qua CodeDeploy hoặc CloudFormation.
- Fallback thủ công: GitLab runner → prebuilt AMIs hoặc ASGs.
- Chuyển đổi dự phòng Route 53 hoặc DNS TTL thấp cho các bản sao lưu khu vực.
- Quy trình xoay vòng khóa khẩn cấp và khôi phục bí mật.
- Diễn tập khắc phục thảm họa (DR drills) định kỳ (khôi phục S3, khôi phục snapshot EC2) và sổ tay phản ứng sự cố.

---

### 8. Kết quả Dự kiến

### Cải tiến Kỹ thuật:

- CI/CD hoàn toàn tự động (GitLab → CodePipeline → CodeBuild → CodeDeploy) để giảm thiểu lỗi thủ công.
- Triển khai Blue/Green / Canary để giảm thiểu thời gian chết; ALB + Auto Scaling + CloudFront để cải thiện độ trễ và khả năng phục hồi.
- Bảo mật đa lớp (IAM, WAF, Secrets Manager) với khả năng kiểm toán qua CloudTrail.
- Khả năng quan sát tập trung (CloudWatch) để giảm MTTR (thời gian trung bình để sửa chữa).
- Thiết kế có thể mở rộng hỗ trợ khoảng 10–15 node EC2, dễ dàng mở rộng thêm.

### Giá trị Dài hạn

- Nền tảng dữ liệu một năm cho phân tích/AI từ nhật ký CloudWatch và sự kiện CloudTrail.
- Mã hóa cơ sở hạ tầng (IaC - CloudFormation/Terraform) có thể tái sử dụng và các pipeline CI/CD cho các dự án trong tương lai.
- Tuân thủ và khả năng kiểm toán tốt hơn thông qua bảo mật và giám sát tích hợp của AWS.
- Chi phí vận hành được tối ưu hóa thông qua Auto Scaling, kiểm soát ngân sách và báo cáo chi phí.
- Hoàn thiện vận hành được cải thiện thông qua sổ tay hướng dẫn (runbooks), diễn tập DR và cảnh báo tự động.
