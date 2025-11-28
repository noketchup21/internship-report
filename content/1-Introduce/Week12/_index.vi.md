---
title : "Tuần 12"
date :  "2025-09-09" 
weight : 2 
chapter : false
pre : " <b>12. </b> "
---

# NHẬT KÝ CÔNG VIỆC

## Mục tiêu Tuần 12
- Viết bài cảm nhận về sự kiện AWS Cloud Mastery #2.
- Cấu hình lại đăng nhập Cognito với trường **sub** mới được ánh xạ vào cơ sở dữ liệu.
- Triển khai chức năng đăng xuất an toàn với AWS Cognito.
- Sửa lỗi logic xác thực liên quan đến tên người dùng khi tạo tài khoản.
- Thêm chức năng cho Admin bật/tắt tài khoản người dùng ở cả cơ sở dữ liệu nội bộ và AWS Cognito.
- Nghiên cứu quy trình deploy dự án lên AWS.
- Cấu hình lại routing sau khi đăng nhập bằng Cognito.
- Refactor logic đăng xuất và routing.

---

## Công Việc Thực Hiện Trong Tuần

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
|------|-----------|--------------|------------------|---------------------|
| 2 | - Viết bài cảm nhận AWS Cloud Mastery #2 <br> - Cấu hình lại đăng nhập Cognito với trường **sub** mới trong database | 24/11/2025 | 24/11/2025 | https://luma.com/39t066sy |
| 3 | - Triển khai chức năng đăng xuất Cognito <br> - Sửa logic xác thực liên quan đến tên người dùng khi tạo tài khoản | 25/11/2025 | 25/11/2025 | |
| 4 | - Tiếp tục triển khai logout handler của Cognito <br> - Thêm chức năng Admin bật/tắt tài khoản người dùng ở local DB và AWS Cognito | 26/11/2025 | 26/11/2025 | |
| 5 | - Nghiên cứu cách deploy dự án lên AWS <br> - Cấu hình lại routing sau khi đăng nhập bằng Cognito | 27/11/2025 | 27/11/2025 | https://cloudjourney.awsstudygroup.com/ |
| 6 | - Refactor chức năng đăng xuất với AWS Cognito <br> - Sửa routing cho chức năng đăng nhập | 28/11/2025 | 28/11/2025 | |

---

## Thành Tựu Tuần 12
- Hoàn thành bài cảm nhận về AWS Cloud Mastery #2.
- Cập nhật luồng đăng nhập để xử lý đúng trường **sub** mới từ Cognito.
- Triển khai và tối ưu chức năng đăng xuất an toàn với Cognito.
- Sửa lỗi logic xác thực khi tạo mới tên người dùng.
- Thêm chức năng Admin bật/tắt tài khoản người dùng trên cả Cognito và cơ sở dữ liệu nội bộ.
- Nghiên cứu quy trình deploy dự án lên AWS để chuẩn bị cho môi trường production.
- Cải thiện routing cho luồng đăng nhập và đăng xuất nhằm tối ưu trải nghiệm người dùng.  