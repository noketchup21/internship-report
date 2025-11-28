---
title : "Blog 2"
date :  "2025-09-09" 
weight : 1 
chapter : false
pre : " <b> 2. </b> "
---

## Xây dựng các agent AI tạo sinh có khả năng phục hồi


Các agent AI tạo sinh trong môi trường sản xuất đòi hỏi các chiến lược phục hồi vượt ra ngoài các mẫu phần mềm truyền thống. Các agent AI đưa ra quyết định tự chủ, tiêu thụ tài nguyên tính toán đáng kể và tương tác với các hệ thống bên ngoài theo những cách không thể đoán trước. Những đặc điểm này tạo ra các chế độ lỗi mà các phương pháp tiếp cận khả năng phục hồi thông thường có thể không giải quyết được.

Bài đăng này trình bày một khuôn khổ để phân tích rủi ro về khả năng phục hồi của agent AI áp dụng cho hầu hết các kiến trúc phát triển và triển khai AI. Chúng tôi cũng khám phá các chiến lược thực tế để giúp ngăn chặn, phát hiện và giảm thiểu các thách thức về khả năng phục hồi phổ biến nhất khi triển khai và mở rộng quy mô các agent AI.

---

### Các khía cạnh rủi ro về khả năng phục hồi của agent AI tạo sinh

Để xác định các rủi ro về khả năng phục hồi, chúng tôi chia nhỏ các hệ thống agent AI tạo sinh thành bảy khía cạnh:

- **Foundation models** – Foundation models (FMs) cung cấp khả năng suy luận và lập kế hoạch cốt lõi. Lựa chọn triển khai của bạn quyết định trách nhiệm và chi phí phục hồi của bạn. Ba phương pháp triển khai là tự quản lý hoàn toàn như sử dụng [Amazon Elastic Compute Cloud](https://aws.amazon.com/ec2/  ) (Amazon EC2), các dịch vụ được quản lý dựa trên máy chủ như sử dụng [Amazon SageMaker AI](https://aws.amazon.com/sagemaker-ai/), hoặc các dịch vụ được quản lý không có máy chủ như [Amazon Bedrock](https://aws.amazon.com/bedrock/).
- **Agent orchestration** – Thành phần này kiểm soát cách nhiều agent và công cụ AI phối hợp để đạt được các mục tiêu phức tạp, chứa logic để lựa chọn công cụ, trình kích hoạt leo thang của con người và quản lý quy trình làm việc nhiều bước.
- **Agent deployment infrastructure** – Cơ sở hạ tầng bao gồm phần cứng và hệ thống cơ bản nơi các agent chạy. Các tùy chọn cơ sở hạ tầng bao gồm sử dụng các phiên bản EC2 được quản lý hoàn toàn, các dịch vụ được quản lý như [Amazon Elastic Container Services](https://aws.amazon.com/ecs/) (Amazon ECS) và các dịch vụ được quản lý chuyên biệt được thiết kế riêng cho việc triển khai agent, chẳng hạn như [Amazon Bedrock AgentCore Runtime](https://aws.amazon.com/bedrock/agentcore/).
- **Knowledge base** – Knowledge base bao gồm lưu trữ cơ sở dữ liệu vector, các mô hình nhúng và các đường ống dữ liệu tạo ra các nhúng vector, tạo thành nền tảng cho các ứng dụng Retrieval Augmented Generation (RAG). [Amazon Bedrock Knowledge Bases](https://aws.amazon.com/bedrock/knowledge-bases/) hỗ trợ các quy trình làm việc RAG được quản lý hoàn toàn.
- **Agent tools** – Điều này bao gồm các công cụ API, máy chủ Model Context Protocol (MCP), quản lý bộ nhớ và các tính năng bộ nhớ đệm nhắc lệnh giúp mở rộng khả năng của agent.
- **Security and compliance** – Thành phần này bao gồm các kiểm soát bảo mật của người dùng và agent cũng như giám sát tuân thủ nội dung, hỗ trợ xác thực, ủy quyền và xác thực nội dung phù hợp. Bảo mật bao gồm xác thực trong nước quản lý quyền truy cập của người dùng vào các agent và xác thực và ủy quyền ngoài nước quản lý quyền truy cập của các agent vào các tài nguyên khác. Ủy quyền ngoài nước phức tạp hơn vì các agent có thể [yêu cầu danh tính riêng của chúng](https://blog.christianposta.com/agent-identity-impersonation-or-delegation/). [Amazon Bedrock AgentCore Identity](https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/identity.html) là dịch vụ quản lý danh tính và thông tin xác thực được thiết kế riêng cho các agent AI, cung cấp khả năng xác thực và ủy quyền trong và ngoài nước. Để giúp ngăn chặn vi phạm tuân thủ, các tổ chức nên thiết lập các chính sách AI có trách nhiệm toàn diện. [Amazon Bedrock Guardrails](https://aws.amazon.com/bedrock/guardrails/) cung cấp các biện pháp bảo vệ có thể định cấu hình để thực hiện chính sách AI có trách nhiệm.
- **Evaluation and observability** – Các hệ thống này theo dõi các chỉ số từ thống kê cơ sở hạ tầng cơ bản đến các dấu vết cụ thể của AI chi tiết, bao gồm đánh giá hiệu suất liên tục và phát hiện các sai lệch hành vi. Đánh giá và khả năng quan sát của agent đòi hỏi sự kết hợp của các chỉ số hệ thống truyền thống và các tín hiệu dành riêng cho agent, chẳng-hạn như dấu vết suy luận và kết quả gọi công cụ. Sơ đồ sau đây minh họa các khía cạnh này. Cấu hình này cung cấp khả năng hiển thị vào các ứng dụng của agent, cho phép các phiên tiếp theo cung cấp phân tích khả năng phục hồi được nhắm mục tiêu và các khuyến nghị giảm thiểu.

Sơ đồ sau minh họa các khía cạnh này.

![Figure 1](/images/ARCH-1228-arch-diag.png)

Cấu hình này cung cấp khả năng quan sát các ứng dụng của tác nhân, cho phép các phiên làm việc sau đó đưa ra phân tích khả năng phục hồi có mục tiêu và các khuyến nghị giảm thiểu.

---

### 5 vấn đề về khả năng phục hồi hàng đầu đối với các agent và kế hoạch giảm thiểu

[Resilience Analysis Framework](https://docs.aws.amazon.com/prescriptive-guidance/latest/resilience-analysis-framework/introduction.html) xác định các chế độ lỗi cơ bản mà các hệ thống sản xuất nên tránh. Trong bài đăng này, chúng tôi xác định năm chế độ lỗi chính của các agent AI tạo sinh và cung cấp các chiến lược có thể giúp thiết lập các thuộc tính phục hồi.

#### Shared fate

Shared fate xảy ra khi một lỗi trong một thành phần của agent lan truyền qua các ranh giới hệ thống, ảnh hưởng đến toàn bộ agent. Fault isolation là thuộc tính mong muốn. Để đạt được fault isolation, bạn phải hiểu cách các thành phần của agent tương tác và xác định các phụ thuộc được chia sẻ của chúng.

Mối quan hệ giữa FMs, knowledge bases và agent orchestration đòi hỏi ranh giới cô lập rõ ràng. Ví dụ, trong các ứng dụng RAG, knowledge bases có thể trả về kết quả tìm kiếm không liên quan. Việc triển khai các biện pháp bảo vệ với kiểm tra mức độ liên quan có thể giúp ngăn các lỗi truy vấn này lan truyền qua phần còn lại của quy trình làm việc của agent.

Các công cụ phải phù hợp với ranh giới fault isolation để chứa tác động trong trường hợp có lỗi. Khi xây dựng các công cụ tùy chỉnh, hãy thiết kế mỗi công cụ như một miền ngăn chặn riêng. Khi sử dụng máy chủ MCP hoặc các công cụ hiện có, hãy đảm bảo bạn sử dụng các lược đồ yêu cầu/phản hồi nghiêm ngặt, có phiên bản và xác thực chúng ở ranh giới. Thêm các xác thực ngữ nghĩa như phạm vi ngày, quy tắc giữa các trường và kiểm tra độ mới của dữ liệu. Các công cụ nội bộ cũng có thể được triển khai trên các Vùng sẵn sàng khác nhau của AWS để có thêm khả năng phục hồi.

Ở khía cạnh orchestration, hãy triển khai các bộ ngắt mạch giám sát tỷ lệ lỗi và độ trễ, kích hoạt khi các phụ thuộc không khả dụng. Đặt giới hạn thử lại có giới hạn với backoff theo cấp số nhân và jitter để kiểm soát chi phí và tranh chấp. Để có khả năng phục hồi kết nối, hãy triển khai ánh xạ lỗi JSON-RPC mạnh mẽ và thời gian chờ cho mỗi cuộc gọi, đồng thời duy trì các nhóm kết nối lành mạnh với các công cụ, máy chủ MCP và các dịch vụ hạ nguồn. Khía cạnh orchestration cũng nên quản lý các phương án dự phòng tương thích với hợp đồng—định tuyến từ một công cụ hoặc máy chủ MCP bị lỗi sang các phương án thay thế—trong khi vẫn duy trì các lược đồ nhất quán và cung cấp chức năng bị suy giảm.

Khi ranh giới cô lập bị lỗi, bạn có thể triển khai graceful degradation để duy trì chức năng cốt lõi trong khi các tính năng nâng cao không khả dụng. Tiến hành kiểm tra khả năng phục hồi với việc tiêm lỗi dành riêng cho AI, chẳng hạn như mô phỏng lỗi suy luận mô hình hoặc sự không nhất quán của knowledge base, để kiểm tra ranh giới cô lập của bạn trước khi sự cố xảy ra trong sản xuất.

#### Insufficient capacity

Tải quá mức có thể làm quá tải ngay cả các hệ thống được cung cấp tốt, có khả năng dẫn đến suy giảm hiệu suất hoặc lỗi hệ thống. Đủ dung lượng đảm bảo hệ thống của bạn có các tài nguyên cần thiết để xử lý cả các mẫu lưu lượng truy cập dự kiến ​​và các đợt tăng đột biến bất ngờ về nhu cầu.

Lập kế hoạch dung lượng agent AI bao gồm dự báo nhu cầu, đánh giá tài nguyên và phân tích hạn ngạch. Việc xem xét chính khi lập kế hoạch dung lượng là ước tính Requests Per Minute (RPM) và Tokens Per Minute (TPM). Tuy nhiên, việc ước tính RPM và TPM đặt ra những thách thức riêng do bản chất ngẫu nhiên của các agent. Các agent AI thường sử dụng xử lý đệ quy, trong đó công cụ suy luận của agent gọi lặp đi lặp lại các FM cho đến khi đạt được câu trả lời cuối cùng. Điều này tạo ra hai khó khăn lớn trong việc lập kế hoạch. Đầu tiên, số lượng các cuộc gọi lặp lại rất khó dự đoán vì nó dựa trên độ phức tạp của nhiệm vụ và các đường dẫn suy luận. Thứ hai, độ dài token của mỗi cuộc gọi cũng khó dự đoán vì nó bao gồm lời nhắc của người dùng, hướng dẫn hệ thống, các bước suy luận do agent tạo ra và lịch sử cuộc trò chuyện. Hiệu ứng kép này làm cho việc lập kế hoạch dung lượng cho các agent trở nên khó khăn.

Thông qua phân tích heuristic trong quá trình phát triển, các nhóm có thể đặt giới hạn đệ quy hợp lý để giúp ngăn chặn các vòng lặp dư thừa và tiêu thụ tài nguyên không kiểm soát. Ngoài ra, vì đầu ra của agent trở thành đầu vào cho các lần đệ quy tiếp theo, việc quản lý các token hoàn thành tối đa giúp kiểm soát một thành phần của việc tiêu thụ token ngày càng tăng trong các chuỗi suy luận đệ quy.

Các phương trình sau đây giúp chuyển đổi cấu hình của agent thành các ước tính dung lượng này:

RPM =  Số luồng trung bình ở cấp agent mỗi phút * Số lần gọi FM trung bình mỗi phút trong một luồng <br>
        =  Số luồng trung bình ở cấp agent mỗi phút * (1 + 60/(số token hoàn thành tối đa/TPS))

Token per second (TPS) khác nhau đối với mỗi mô hình và có thể được tìm thấy trong tài liệu phát hành mô hình và kết quả benchmark nguồn mở, chẳng hạn như phân tích nhân tạo. Phép tính này giả định không có tính năng bộ nhớ đệm nhắc lệnh nào được triển khai.

TPM = RPM * Độ dài token đầu vào trung bình <br>
    = RPM * (độ dài lời nhắc hệ thống + độ dài lời nhắc người dùng + số token hoàn thành tối đa * (giới hạn đệ quy -1)/giới hạn đệ quy)

Phép tính này giả định rằng không có tính năng lưu bộ nhớ đệm prompt nào được triển khai.

Không giống như các công cụ bên ngoài nơi khả năng phục hồi được quản lý bởi các nhà cung cấp bên thứ ba, các công cụ được phát triển trong nội bộ phụ thuộc vào cấu hình phù hợp của nhóm phát triển để mở rộng quy mô dựa trên nhu-cầu. Khi nhu cầu tài nguyên tăng đột biến, chỉ các công cụ bị ảnh hưởng mới cần mở rộng quy mô.

Ví dụ, các hàm [AWS Lambda](https://aws.amazon.com/lambda/) có thể được chuyển đổi thành các công cụ tương thích với MCP bằng cách sử dụng [Amazon Bedrock AgentCore Gateway](https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/gateway.html). Nếu các công cụ phổ biến khiến các hàm Lambda đạt đến giới hạn dung lượng, bạn có thể tăng giới hạn thực thi đồng thời ở cấp tài khoản hoặc triển khai đồng thời được cung cấp để xử lý tải tăng lên.

Đối với các kịch bản liên quan đến nhiều nhóm hành động thực thi đồng thời, các kiểm soát đồng thời dành riêng của hàm Lambda cung cấp sự cô lập tài nguyên thiết yếu bằng cách phân bổ dung lượng chuyên dụng cho mỗi nhóm hành động. Điều này giúp ngăn một công cụ duy nhất tiêu thụ tất cả các tài nguyên có sẵn trong các lần gọi được dàn xếp, tạo điều kiện thuận lợi cho sự sẵn có của tài nguyên cho các chức năng có mức độ ưu tiên cao.


Khi đạt đến giới hạn dung lượng, bạn có thể sử dụng hàng đợi yêu cầu thông minh với phân bổ dựa trên mức độ ưu tiên để đảm bảo các dịch vụ thiết yếu tiếp tục hoạt động. Việc triển khai graceful degradation trong các giai đoạn tải cao có thể hữu ích. Điều này duy trì chức năng cốt lõi trong khi tạm thời giảm các tính năng không thiết yếu.


#### Excessive latency

Độ trễ quá mức làm ảnh hưởng đến trải nghiệm người dùng, giảm thông lượng và làm suy yếu giá trị thực tế của các agent AI trong sản xuất. Việc phát triển khối lượng công việc của agent đòi hỏi sự cân bằng giữa tốc độ, chi phí và độ chính xác. Độ chính xác là nền tảng để các agent AI có được lòng tin của người dùng. Để đạt được độ chính xác cao, cần cho phép các agent thực hiện nhiều lần lặp lại suy luận, điều này chắc chắn sẽ tạo ra những thách thức về độ trễ.

Việc quản lý kỳ vọng của người dùng trở nên quan trọng—thiết lập các chỉ số service level objective (SLO) trước khi bắt đầu dự án sẽ đặt ra các mục tiêu thực tế cho thời gian phản hồi của agent. Các nhóm nên xác định các ngưỡng độ trễ cụ thể cho các khả năng khác nhau của agent, chẳng hạn như phản hồi dưới giây cho các truy vấn đơn giản so với các cửa sổ dài hơn cho các tác vụ phân tích đòi hỏi nhiều tương tác công cụ hoặc các chuỗi suy luận mở rộng. Việc truyền đạt rõ ràng thời gian phản hồi dự kiến ​​giúp ngăn ngừa sự thất vọng của người dùng và cho phép đưa ra các quyết định thiết kế hệ thống phù hợp.

Prompt engineering mang lại cơ hội lớn nhất để cải thiện độ trễ bằng cách giảm các vòng lặp suy luận không cần thiết. Các lời nhắc mơ hồ đưa các agent vào các chu kỳ cân nhắc sâu rộng, trong khi các hướng dẫn rõ ràng giúp tăng tốc độ ra quyết định. Yêu cầu một agent "phê duyệt nếu trường hợp sử dụng có giá trị chiến lược" tạo ra một chuỗi suy luận phức tạp. Agent trước tiên phải xác định các tiêu chí giá trị chiến lược, sau đó đánh giá các tiêu chí nào áp dụng và cuối cùng xác định các ngưỡng ý nghĩa. Ngược lại, việc nêu rõ các tiêu chí trong lời nhắc hệ thống có thể giảm đáng kể các lần lặp lại của agent.

Sau đây là một ví dụ về hướng dẫn agent không rõ ràng:

Bạn là người phê duyệt trường hợp sử dụng AI tạo sinh.

Vai trò của bạn là đánh giá các yêu cầu xây dựng agent GenAI bằng cách phân tích cẩn thận thông tin do người dùng cung cấp và đưa ra quyết định phê duyệt. Vui lòng làm theo các hướng dẫn sau:

\<instructions>

1. Phân tích cẩn thận thông tin do người dùng cung cấp và thu thập thông tin về trường hợp sử dụng, chẳng hạn như người bảo trợ cho trường hợp sử dụng, tầm quan trọng của trường hợp sử dụng và các giá trị tiềm năng mà nó có thể mang lại.

2. Phê duyệt trường hợp sử dụng nếu nó có người bảo trợ cấp cao và có giá trị chiến lược. 
   
\</instructions>

Sau đây là một ví dụ về hướng dẫn agent rõ ràng, được định nghĩa tốt:
Bạn là người phê duyệt trường hợp sử dụng AI tạo sinh. Vai trò của bạn là đánh giá các yêu cầu xây dựng agent Gen AI bằng cách phân tích cẩn thận thông tin do người dùng cung cấp và đưa ra quyết định phê duyệt dựa trên các tiêu chí cụ thể.

Vui lòng tuân thủ nghiêm ngặt các hướng dẫn sau: 

\<instructions>  
1. Phân tích cẩn thận thông tin do người dùng cung cấp. Thu thập câu trả lời cho các câu hỏi sau:  
\<question_1>Trường hợp sử dụng có người bảo trợ kinh doanh từ cấp VP trở lên không?\</question_1>  
\<question_2>Agent này dự kiến sẽ mang lại giá trị gì? Câu trả lời có thể ở dạng số giờ tiết kiệm được mỗi tháng cho các tác vụ nhất định, hoặc các giá trị doanh thu bổ sung.\</question_2>  
\<question_3>Nếu trường hợp sử dụng dành cho khách hàng bên ngoài, vui lòng cung cấp thông tin hỗ trợ về nhu cầu.\</question_3>  

2. Đánh giá yêu cầu dựa trên các tiêu chí phê duyệt sau:  
\<criteria_1>Trường hợp sử dụng có người bảo trợ kinh doanh ở cấp VP trở lên. Đây là một tiêu chí cứng.\</criteria_1>  
\<criteria_2>Trường hợp sử dụng có thể mang lại giá trị $ đáng kể, được tính bằng mức tăng năng suất hoặc tăng doanh thu. Đây là một tiêu chí mềm.\</criteria_2>  
\<criteria_3>Có bằng chứng chắc chắn rằng trường hợp sử dụng/tính năng này được khách hàng yêu cầu. Đây là một tiêu chí mềm.\</criteria_3>  

3. Dựa trên đánh giá, đưa ra quyết định phê duyệt hoặc từ chối trường hợp sử dụng. 
- Phê duyệt: Nếu tiêu chí cứng được đáp ứng, và ít nhất một trong các tiêu chí mềm được đáp ứng  
- Từ chối: Tiêu chí cứng không được đáp ứng, hoặc không có tiêu chí mềm nào được đáp ứng.

\</instructions>

Prompt caching giúp giảm độ trễ đáng kể bằng cách lưu trữ các tiền tố lời nhắc lặp lại giữa các yêu cầu. [Amazon Bedrock prompt caching](https://aws.amazon.com/bedrock/prompt-caching/) có thể giảm độ trễ lên đến 85% cho các mô hình được hỗ trợ, đặc biệt mang lại lợi ích cho các agent có lời nhắc hệ thống dài và thông tin ngữ cảnh không thay đổi qua các phiên.

Asynchronous processing cho các agent và công cụ giúp giảm độ trễ bằng cách cho phép thực thi song song. Các quy trình làm việc đa agent đạt được tốc độ tăng đáng kể khi các agent độc lập thực thi song song thay vì chờ đợi hoàn thành tuần tự. Đối với các agent có công cụ, xử lý không đồng bộ cho phép tiếp tục suy luận và chuẩn bị các hành động tiếp theo trong khi các công cụ thực thi ở chế độ nền, tối ưu hóa quy trình làm việc bằng cách chồng chéo xử lý nhận thức với các hoạt động I/O.

Các kiểm tra bảo mật và tuân thủ phải giảm thiểu tác động đến độ trễ trong khi vẫn duy trì sự bảo vệ trên các khía cạnh. Các agent kiểm duyệt nội dung triển khai quét tuân thủ theo luồng (streaming) để đánh giá đầu ra của agent trong quá trình tạo ra thay vì chờ đợi phản hồi hoàn chỉnh, gắn cờ nội dung có khả năng gây vấn đề trong thời gian thực trong khi cho phép nội dung an toàn được lưu thông ngay lập tức.

#### Phản hồi của agent không chính xác

Đầu ra chính xác đảm bảo agent AI của bạn hoạt động đáng tin cậy trong phạm vi được xác định, cung cấp các phản hồi chính xác và nhất quán đáp ứng kỳ vọng của người dùng và yêu cầu kinh doanh. Tuy nhiên, cấu hình sai, lỗi phần mềm và hiện tượng ảo giác của mô hình có thể làm ảnh hưởng đến chất lượng đầu ra, dẫn đến các phản hồi không chính xác làm suy yếu lòng tin của người dùng.

Để cải thiện độ chính xác, hãy sử dụng các luồng điều phối xác định (deterministic) bất cứ khi nào có thể. Việc để các agent dựa vào các LLM để tự ứng biến khi thực hiện nhiệm vụ sẽ tạo cơ hội đi chệch khỏi con đường bạn đã định. Thay vào đó, hãy xác định các quy trình làm việc rõ ràng chỉ định cách các agent nên tương tác và sắp xếp thứ tự các hoạt động của chúng. Cách tiếp cận có cấu trúc này làm giảm cả lỗi gọi giữa các agent và lỗi gọi công cụ. Ngoài ra, việc triển khai các input and output guardrails giúp tăng cường đáng kể độ chính xác của agent. Amazon Bedrock Guardrails có thể quét đầu vào của người dùng để kiểm tra tuân thủ trước khi gọi mô hình, và cung cấp xác thực đầu ra để phát hiện [hiện tượng ảo giác](https://docs.aws.amazon.com/bedrock/latest/userguide/guardrails-contextual-grounding-check.html), [các phản hồi có hại](https://docs.aws.amazon.com/bedrock/latest/userguide/guardrails.html), [thông tin nhạy cảm](https://docs.aws.amazon.com/bedrock/latest/userguide/guardrails-sensitive-filters.html) và [các chủ đề bị chặn](https://docs.aws.amazon.com/bedrock/latest/userguide/guardrails-denied-topics.html).

Khi các vấn đề về chất lượng phản hồi xảy ra, bạn có thể triển khai human-in-the-loop validation (xác thực có sự can thiệp của con người) cho các quyết định quan trọng nơi độ chính xác là thiết yếu, và triển khai các cơ chế thử lại tự động với các lời nhắc được tinh chỉnh khi các phản hồi ban đầu không đáp ứng tiêu chuẩn chất lượng.

#### Single point of failure

Redundancy (sự dự phòng) tạo ra nhiều con đường dẫn đến thành công bằng cách giảm thiểu các điểm lỗi đơn lẻ có thể gây ra suy yếu trên toàn hệ thống. Các điểm lỗi đơn lẻ làm suy yếu sự dự phòng khi nhiều thành phần phụ thuộc vào một tài nguyên hoặc dịch vụ duy nhất, tạo ra các lỗ hổng vượt qua các ranh giới bảo vệ. Sự dự phòng hiệu quả đòi hỏi cả các thành phần dự phòng và các đường dẫn dự phòng, đảm bảo rằng nếu một thành phần bị lỗi, các thành phần thay thế có thể tiếp quản, và nếu một đường dẫn không khả dụng, lưu lượng truy cập có thể đi qua các tuyến đường khác nhau.

Các agent yêu cầu sự dự phòng phối hợp cho các FM của chúng. Nếu các mô hình được tự quản lý, bạn có thể triển khai multi-Region model deployment (triển khai mô hình đa Vùng) với automated failover (chuyển đổi dự phòng tự động). Khi sử dụng các dịch vụ được quản lý, Amazon Bedrock cung cấp cross-Region inference (suy luận chéo Vùng) để cung cấp sự dự phòng tích hợp sẵn cho các mô hình được hỗ trợ, tự động định tuyến các yêu cầu đến các Vùng AWS thay thế khi các điểm cuối chính gặp sự cố.

Agent sẽ tự động định tuyến đến các công cụ thay thế cung cấp chức năng tương tự, ngay cả khi chúng kém tinh vi hơn. Ví dụ, khi knowledge base của trợ lý trò chuyện nội bộ bị lỗi, nó có thể chuyển sang công cụ tìm kiếm để cung cấp đầu ra thay thế cho người dùng.

Việc duy trì tính nhất quán về quyền trên các môi trường dự phòng là điều cần thiết. Điều này giúp ngăn ngừa các lỗ hổng bảo mật trong các kịch bản chuyển đổi dự phòng. Vì các kiểm soát truy cập quá dễ dãi gây ra rủi ro bảo mật đáng kể, điều quan trọng là phải xác thực rằng cả quyền của người dùng cuối và quyền truy cập ở cấp công cụ đều giống hệt nhau giữa các thành phần chính và thành phần chuyển đổi dự phòng. Tính nhất quán này đảm bảo các ranh giới bảo mật được duy trì bất kể môi trường nào đang tích cực phục vụ các yêu cầu, giúp ngăn chặn việc leo thang đặc quyền hoặc truy cập trái phép có thể xảy ra khi hệ thống chuyển đổi giữa các mô hình quyền khác nhau trong quá trình chuyển đổi hoạt động.

---

### Operational excellence: Tích hợp các phương pháp truyền thống và các thực hành chuyên biệt cho AI.

Operational excellence trong AI của agent tích hợp các phương pháp DevOps đã được chứng minh với các yêu cầu dành riêng cho AI để chạy các hệ thống của agent một cách đáng tin cậy trong sản xuất. Các đường ống continuous integration and continuous delivery (CI/CD) điều phối toàn bộ vòng đời của agent và infrastructure as code (IaC) chuẩn hóa việc triển khai trên các môi trường, giảm lỗi thủ công và cải thiện khả năng tái tạo.

Khả năng quan sát của agent đòi hỏi sự kết hợp giữa các chỉ số truyền thống và các tín hiệu dành riêng cho agent như dấu vết suy luận và kết quả gọi công cụ. Mặc dù các chỉ số và nhật ký hệ thống truyền thống có thể được lấy từ [Amazon CloudWatch](http://aws.amazon.com/cloudwatch), nhưng việc truy tìm ở cấp agent đòi hỏi phải xây dựng phần mềm bổ sung. [Amazon Bedrock AgentCore Observability](https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/observability.html) (bản xem trước) được công bố gần đây hỗ trợ [OpenTelemetry](https://opentelemetry.io/) để tích hợp dữ liệu đo từ xa của agent với các dịch vụ quan sát hiện có, bao gồm CloudWatch, [Datadog](https://www.datadoghq.com/), [LangSmith](https://www.langchain.com/langsmith) và [Langfuse](https://langfuse.com/). Để biết thêm chi tiết về các tính năng của Amazon Bedrock AgentCore Observability, hãy xem [Ra mắt khả năng quan sát AI tạo sinh của Amazon CloudWatch](https://aws.amazon.com/blogs/mt/launching-amazon-cloudwatch-generative-ai-observability-preview/) (Bản xem trước).

Ngoài việc giám sát, việc kiểm tra và xác thực các agent cũng vượt ra ngoài các phương pháp phần mềm thông thường. Các bộ kiểm tra tự động như promptfoo giúp các nhóm phát triển định cấu hình các bài kiểm tra để đánh giá chất lượng suy luận, hoàn thành nhiệm vụ và sự mạch lạc của cuộc đối thoại. Các kiểm tra trước khi triển khai xác nhận kết nối công cụ và quyền truy cập kiến ​​thức, và việc tiêm lỗi mô phỏng tình trạng ngừng hoạt động của công cụ, lỗi API và sự không nhất quán của dữ liệu để phát hiện ra các sai sót trong suy luận trước khi chúng ảnh hưởng đến người dùng.

Khi sự cố phát sinh, việc giảm thiểu dựa vào các playbook bao gồm cả các vấn đề ở cấp cơ sở hạ tầng và dành riêng cho agent. Các playbook này hỗ trợ các phiên trực tiếp, cho phép chuyển giao liền mạch cho các agent dự phòng hoặc người vận hành mà không làm mất ngữ cảnh.

---

### Tóm tắt

Trong bài viết này, chúng tôi đã giới thiệu mô hình kiến trúc gồm bảy khía cạnh để lập bản đồ cho các tác nhân AI của bạn và phân tích nơi các rủi ro về khả năng phục hồi có thể phát sinh. Chúng tôi cũng đã xác định năm dạng lỗi phổ biến liên quan đến các tác nhân AI cùng với các chiến lược giảm thiểu tương ứng.

Các chiến lược này minh họa cách các nguyên tắc về khả năng phục hồi được áp dụng cho các khối lượng công việc tác nhân thường gặp, nhưng chúng không phải là toàn diện. Mỗi hệ thống AI đều có những đặc điểm và sự phụ thuộc riêng. Bạn cần phân tích kiến trúc cụ thể của mình dựa trên bảy khía cạnh rủi ro để xác định những thách thức về khả năng phục hồi trong khối lượng công việc của riêng bạn, đồng thời ưu tiên các khu vực dựa trên mức độ ảnh hưởng đến người dùng và tầm quan trọng với doanh nghiệp thay vì độ phức tạp kỹ thuật.

Khả năng phục hồi là một hành trình liên tục chứ không phải một điểm đến. Khi các tác nhân AI của bạn phát triển và xử lý những trường hợp sử dụng mới, các chiến lược về khả năng phục hồi của bạn cũng phải tiến hóa theo. Bạn có thể thiết lập quy trình kiểm thử, giám sát và cải tiến thường xuyên để đảm bảo các hệ thống AI của bạn luôn duy trì khả năng phục hồi khi mở rộng quy mô. Để biết thêm thông tin về các tác nhân AI tạo sinh và khả năng phục hồi trên AWS, hãy tham khảo các tài nguyên sau:

- [Chaos Engineering Scenarios for GenAI workloads](https://builder.aws.com/content/2uSMnBJb3h7JxB9SkryFvXfQWk8/chaos-engineering-scenarios-for-genai-workloads)
- [Designing generative AI workloads for resilience](https://aws.amazon.com/blogs/machine-learning/designing-generative-ai-workloads-for-resilience/)
- [Introducing Amazon Bedrock AgentCore: Securely deploy and operate AI agents at any scale (preview)](https://aws.amazon.com/blogs/aws/introducing-amazon-bedrock-agentcore-securely-deploy-and-operate-ai-agents-at-any-scale/)
- Implement effective data authorization mechanisms to secure your data used in generative AI applications: [Part 1](https://aws.amazon.com/blogs/security/implement-effective-data-authorization-mechanisms-to-secure-your-data-used-in-generative-ai-applications/) and [Part 2](https://aws.amazon.com/blogs/security/implement-effective-data-authorization-mechanisms-to-secure-your-data-used-in-generative-ai-applications-part-2/)

---

### Yiwen Zhang
<div style="display: flex; align-items: center; gap: 15px;">

<img src="/images/ARCH-1228-author1.jpeg" alt="Yiwen Zhang" width="150"/>

<div>
Yiwen Zhang là Kiến trúc sư Giải pháp GenAI cấp cao tại AWS. Cô phát triển cả các ứng dụng generative AI và chiến lược tích hợp doanh nghiệp. Với bằng Tiến sĩ về thống kê tính toán và hơn một thập niên kinh nghiệm trong phát triển và triển khai AI/ML và các pipeline dữ liệu, cô mang đến chuyên môn sâu cho chuyển đổi AI doanh nghiệp. Cô tập trung vào việc biến generative AI trở nên thực tế bằng cách xây dựng các MVP AI có hiệu quả và xử lý các vấn đề khó như ROI, tinh chỉnh hiệu năng agent AI, quản lý chi phí, bảo mật và độ bền sản xuất. Mục tiêu của cô là giúp các doanh nghiệp biến agent generative AI thành các giải pháp “kết quả như một dịch vụ”.
</div>
</div>

---

### Hechmi Khelifi
<div style="display: flex; align-items: center; gap: 15px;">
  <img src="/images/hk.jpeg" alt="Hechmi Khelifi" width="150"/>
  <div>
Hechmi Khelifi là Kiến trúc sư Giải pháp Doanh nghiệp tại AWS, chuyên về tính bền vững và độ tin cậy. Với hơn 3 năm làm việc tại AWS và bằng Tiến sĩ từ Đại học Québec, Hechmi tận dụng kinh nghiệm CNTT rộng và nền tảng học thuật để giúp khách hàng xây dựng các giải pháp vững chắc và có khả năng chịu lỗi.
  </div>
</div>

---

### Jennifer Moran
<div style="display: flex; align-items: center; gap: 15px;">

<img src="/images/Jennifer-Moran.png" alt="Jennifer Moran" width="150"/>

<div>
Jennifer Moran là Kiến trúc sư Giải pháp Chuyên gia về Resilience cao cấp tại AWS. Cô mang đến kinh nghiệm đa dạng từ nhiều vai trò kỹ thuật trong ngành phần mềm. Chuyên môn của cô tập trung vào việc thiết kế các giải pháp có độ bền cao để cải thiện “posture” độ bền tổng thể của hệ thống.
</div>
</div>