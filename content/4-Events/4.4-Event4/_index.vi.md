---
title : "Event 4"
date :  "2025-09-09" 
weight : 3
chapter : false
pre : " <b> 4.4 </b> "
---


# Báo cáo Tổng hợp: “Agentic AI & Điều phối trên AWS”

## Mục tiêu Sự kiện
* Khám phá kiến trúc cấp cao của Agentic AI (AI đại lý) sử dụng Amazon Bedrock.
* Hiểu bước chuyển từ GenAI tiêu chuẩn sang các quy trình "Agentic" có khả năng thực thi tác vụ.
* Học các kỹ thuật điều phối (orchestration) nâng cao và tối ưu hóa ngữ cảnh (cấp độ L300).
* Khảo sát các case study thực tế về triển khai agent từ Diaflow và CloudThinker.
* Có trải nghiệm thực hành xây dựng agent thông qua các phiên code tương tác.

## Diễn giả
* **Nguyen Gia Hung** – Trưởng bộ phận Kiến trúc sư Giải pháp, AWS
* **Kien Nguyen** – Kiến trúc sư Giải pháp, AWS
* **Viet Pham** – Nhà sáng lập & CEO, Diaflow
* **Thang Ton** – Đồng sáng lập & COO, CloudThinker
* **Henry Bui** – Trưởng bộ phận Kỹ thuật, CloudThinker
* **Kha Van** – Lãnh đạo Cộng đồng

## Điểm nhấn Chính

### Cốt lõi AWS Bedrock Agent
* **Nền tảng:** Đi sâu vào kỹ thuật kiến trúc của Amazon Bedrock Agents.
* **Khả năng:** Vượt ra ngoài việc tạo văn bản đơn giản để hướng tới các agent có thể lập kế hoạch, suy luận và thực thi hành động qua các lệnh gọi API.
* **Kiến trúc:** Hiểu cách bộ định tuyến agent (router), nhóm hành động (action groups) và cơ sở tri thức (knowledge bases) tương tác để giải quyết các truy vấn phức tạp của người dùng.

### Triển khai Thực tế (Diaflow)
* **Case Study:** Bài trình bày của CEO Diaflow về việc xây dựng các quy trình agentic thực tế.
* **Tự động hóa Quy trình:** Minh họa cách chuỗi các bước AI liên kết với nhau để tạo thành một quy trình kinh doanh gắn kết.
* **Thách thức:** Thảo luận về những trở ngại khi chuyển từ nguyên mẫu (prototype) sang thực tế (production) trong môi trường startup.

### Điều phối Nâng cao (CloudThinker)
* **Đi sâu Kỹ thuật L300:** Tập trung vào các thách thức kỹ thuật của việc điều phối AI.
* **Tối ưu hóa Ngữ cảnh:** Các kỹ thuật quản lý cửa sổ ngữ cảnh (context window) hiệu quả trên Amazon Bedrock để giảm chi phí và cải thiện độ chính xác.
* **Khung Điều phối:** Cách CloudThinker cấu trúc sự tương tác giữa các mô hình và công cụ khác nhau để duy trì trạng thái và ý định.

### Workshop Thực hành
* **CloudThinker Hack:** Phiên code tương tác được hướng dẫn bởi các kỹ sư.
* **Triển khai:** Chuyển từ lý thuyết sang mã, thiết lập cấu trúc cơ bản của một agent và kết nối nó với các dịch vụ AWS.

## Bài học Chính (Key Takeaways)

### Tư duy Thiết kế
* **Agents vs. Chatbots:** Sự dịch chuyển từ truy xuất thông tin thụ động (Chatbots) sang thực thi tác vụ chủ động (Agents).
* **Ngữ cảnh là Vua:** Tối ưu hóa những gì đưa vào cửa sổ ngữ cảnh quan trọng ngang với chính mô hình; quá nhiều nhiễu sẽ làm giảm hiệu suất.
* **Điều phối:** Các agent thành công cần một lớp mạnh mẽ để quản lý logic ra quyết định và trạng thái.

### Kiến trúc Kỹ thuật
* **Sử dụng Công cụ:** Các Agent chỉ tốt ngang với các công cụ (APIs/Functions) mà bạn cấp quyền truy cập cho chúng.
* **Quản lý Trạng thái:** Xử lý các cuộc hội thoại nhiều lượt (multi-turn) đòi hỏi theo dõi trạng thái cẩn thận để đảm bảo agent ghi nhớ các ràng buộc trước đó.
* **Tối ưu hóa:** Các chiến lược ngữ cảnh nâng cao là cần thiết để xử lý các cuộc hội thoại dài mà không gặp giới hạn token hoặc vấn đề về độ trễ.

### Ứng dụng vào Công việc
* **Thử nghiệm với Bedrock Agents:** Bắt đầu xây dựng một agent đơn giản kết nối với backend dự án "Meal Plan" để trả lời truy vấn người dùng (ví dụ: "Tìm cho tôi công thức dưới 500 calo").
* **Tinh chỉnh Ngữ cảnh:** Xem xét lại cách dữ liệu người dùng được truyền vào LLM; triển khai cắt tỉa ngữ cảnh (context pruning) để giữ cho các prompt hiệu quả.
* **Tích hợp Quy trình:** Khám phá việc sử dụng quy trình agentic để tự động hóa các tác vụ quản trị backend (ví dụ: phê duyệt nội dung người dùng hoặc xác minh hình ảnh).

## Trải nghiệm Sự kiện

Sự kiện **“Agentic AI & Orchestration trên AWS”** là một hành trình toàn diện từ các khái niệm cấp cao đến chi tiết kỹ thuật L300. Nó làm nổi bật sự phát triển nhanh chóng của AI từ "suy nghĩ" sang "hành động".

### Học hỏi từ chuyên gia
* Phiên L300 của Henry Bui đặc biệt sâu sắc về Tối ưu hóa Ngữ cảnh, đưa ra các chiến lược cụ thể để cải thiện hiệu suất mô hình và giảm độ trễ.
* Hiểu rõ về hệ sinh thái Amazon Bedrock và cách nó đơn giản hóa sự phức tạp của việc xây dựng các agent tùy chỉnh.

### Tiếp cận kỹ thuật thực tế
* **CloudThinker Hack:** Workshop cung cấp phần thực hành rất cần thiết, cho phép nhìn thấy code đằng sau các khái niệm.
* **Ví dụ thực tế:** Việc nhìn thấy triển khai của Diaflow đã chứng minh rằng Agentic AI đã sẵn sàng cho các trường hợp sử dụng kinh doanh thực tế, không chỉ là nghiên cứu.

### Kết nối và thảo luận
* Kết nối với đội ngũ CloudThinker trong bữa trưa buffet để thảo luận về các thách thức cụ thể trong việc điều phối hệ thống đa agent (multi-agent).
* Thảo luận với đồng nghiệp về cách tích hợp các agent này vào kiến trúc Spring Boot và React hiện có.

### Bài học rút ra
* **Action Groups** trong Bedrock là chìa khóa để mở khóa giá trị thực; việc định nghĩa các lược đồ API (API schemas) rõ ràng cho agent là rất quan trọng.
* **Điều phối** rất phức tạp; sử dụng một framework hoặc dịch vụ được quản lý như Bedrock Agents được ưu tiên hơn là tự xây dựng logic định tuyến từ đầu.
* Tương lai của phát triển ứng dụng là định hướng Agent (Agent-driven), nơi giao diện người dùng (UI) thích ứng với ý định của người dùng thay vì buộc người dùng phải điều hướng các menu tĩnh.
  
### Ảnh sự kiện