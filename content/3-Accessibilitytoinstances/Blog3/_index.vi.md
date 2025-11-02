---
title : "Blog 3"
date :  "2025-09-09" 
weight : 1 
chapter : false
pre : " <b> 3. </b> "
---

## Mở rộng liền mạch các job EDA lên AWS bằng giải pháp Synopsys Cloud Hybrid

*Bài viết này được đóng góp bởi Varun Shah, Xingang Zhao (Synopsys), Dnyanesh Digraskar, Mayur Runwal (AWS)*

<div style="display: flex; align-items: flex-start; gap: 20px;">

<div style="flex: 1;">

Trong bài viết này, chúng tôi mô tả cách khách hàng có thể mở rộng (burst) khối lượng công việc Synopsys của họ lên AWS bằng [giải pháp Synopsys Cloud Hybrid](https://www.synopsys.com/blogs/chip-design/hybrid-cloud-chip-design-agility-efficiency.html). Giải pháp này đơn giản hóa quy trình làm việc bằng cách loại bỏ nhu cầu phải di chuyển dữ liệu thủ công giữa lưu trữ tại chỗ (on-premises storage) và cloud. Dữ liệu cần thiết cho một job chạy trên AWS sẽ được cache dần dần ở chế độ nền và sẵn sàng cho tiến trình. Tương tự, khi cần, dữ liệu chọn lọc được ghi bởi một job đang chạy trên cloud có thể được đẩy về hệ thống tại chỗ theo thời gian thực – giúp cho lưu trữ tại chỗ luôn được cập nhật.

</div>

<img src="/images/Seamlessly-burst-EDA-jobs-to-AWS-using-Synopsys-Cloud-Hybrid-solution.png" alt="Figure 1" width="400" style="margin-top: -5px;"/>

</div>

<div style="margin-top: -40px;">

Ngành công nghiệp bán dẫn đang chứng kiến sự tăng trưởng bùng nổ, được thúc đẩy bởi trí tuệ nhân tạo (AI), điện toán hiệu năng cao (HPC – High Performance Computing), và sự phổ biến của các hệ thống thông minh. Các kỹ sư đang đối mặt với mức độ phức tạp chưa từng có cùng tốc độ đổi mới ngày càng nhanh. Khi chip ngày càng mạnh mẽ và tinh vi hơn, vòng đời thiết kế trở nên dài hơn, chi phí tăng cao, và nguy cơ bỏ lỡ thời điểm tung sản phẩm ra thị trường (time to market) cũng lớn hơn. Trong bối cảnh này, “time to market” đã trở thành yếu tố khác biệt mang tính quyết định.

</div>

Hạ tầng dựa trên cloud mang lại khả năng mở rộng và linh hoạt để gia tăng quy mô hoạt động thiết kế chip và đáp ứng nhu cầu khách hàng. AWS cung cấp quyền truy cập dễ dàng vào tài nguyên tính toán trên cloud được tối ưu cho khối lượng công việc EDA. [Amazon Elastic Compute Cloud](https://aws.amazon.com/ec2/) (Amazon EC2) mang đến khả năng truy cập vào thế hệ [bộ xử lý](https://aws.amazon.com/ec2/instance-types/) mới nhất với dung lượng gần như không giới hạn, có thể triển khai trên toàn cầu. Các instance thế hệ mới dựa trên x86 và ARM trên AWS giúp đạt hiệu suất tối đa và cho phép khách hàng khai thác tối đa license phần mềm EDA của mình.

[Synopsys](https://www.synopsys.com/) là một AWS Partner, cung cấp giải pháp thiết kế toàn diện và đáng tin cậy từ silicon đến hệ thống cho khách hàng, bao gồm từ EDA đến silicon IP cũng như xác minh và thẩm định hệ thống (system verification and validation).

Trong bài viết này, chúng tôi sẽ minh họa việc kiểm thử khả năng mở rộng (scale-testing) một tập hợp công cụ EDA của Synopsys trên AWS và mô tả hiệu năng, chất lượng kết quả cũng như thời gian hoàn thành.

### Giải pháp Synopsys Cloud Hybrid: mở rộng các job EDA lên AWS

AWS giúp việc thiết lập hạ tầng tính toán trên cloud trở nên dễ dàng nhờ vào danh mục phần cứng và dịch vụ phong phú dành cho các luồng công việc trong [ngành bán dẫn và công nghệ cao](https://aws.amazon.com/manufacturing/semiconductor-hi-tech/). Các công ty có thể điều chỉnh nhu cầu tính toán của mình phù hợp với các workflow quan trọng về thời gian. Ở mức tổng quan, các bước để mở rộng (burst) khối lượng công việc EDA trên AWS bao gồm:

1. Xác định các khối thiết kế (design blocks)/job cần được chạy trên cloud
2. Truyền dữ liệu liên quan lên cloud
3. Cài đặt các binary ứng dụng EDA và license trên cloud
4. Chạy các job EDA
5. Truyền kết quả trở lại hệ thống tại chỗ (on-premises) để phân tích/khắc lỗi (debug)/tạo báo cáo

Hai bước đầu tiên (1 & 2) ở trên có thể gây tốn công, bởi việc đóng gói đúng tập hợp file, mã nguồn, thư viện, dependencies, script, v.v… có thể mất đến vài tuần. Synopsys Cloud Hybrid Solution cung cấp một cơ chế kích hoạt trên cloud giúp thực hiện các tác vụ này dễ dàng hơn.

### Kiến trúc và các thành phần

![Figure](/images/IMG-2025-09-23-16.23.34@2x.png)

*Hình 1: Sơ đồ kiến trúc của giải pháp Synopsys Cloud Hybrid với AWS được sử dụng cho thử nghiệm được mô tả trong blog này*

Hình 1 minh họa kiến trúc tổng thể của giải pháp Synopsys Cloud Hybrid. Các thành phần kiến trúc chính bao gồm:

1. **On-premises storage:** Đây là các điểm mount NFS với dữ liệu thiết kế, cần được cung cấp cho các compute node trên AWS. Giải pháp hybrid này hoạt động với bất kỳ giải pháp lưu trữ từ bên thứ ba hoặc ISV thương mại nào.

2. **Scheduler:** Giải pháp Hybrid hoạt động với bất kỳ job scheduler thương mại nào, như [AWS Parallel Computing Service (PCS)](https://aws.amazon.com/pcs/), [AWS ParallelCluster](https://aws.amazon.com/hpc/parallelcluster/), [AWS Batch](https://aws.amazon.com/batch/), hoặc IBM LSF, UGE, Slurm, v.v… Sơ đồ kiến trúc minh họa việc sử dụng IBM LSF multi-cluster tích hợp với [LSF resource connector](https://www.ibm.com/docs/en/spectrum-lsf/10.1.0?topic=providers-configuring-amazon-web-services-lsf-resource-connector) để cung cấp tài nguyên trên AWS.

3. **Compute farms:**
    1. **On-premises:** Trung tâm dữ liệu (datacenter) với sự kết hợp của nhiều loại máy chủ tính toán khác nhau. 
    2. **Trên AWS:** Các Amazon EC2 instance được sử dụng để chạy mô phỏng EDA. Trong thử nghiệm này, chúng tôi sử dụng instance loại 16xlarge với CPU 3.5GHz, 8GB bộ nhớ cho mỗi vCPU. Nhiều loại EC2 instance khác có thể được dùng tùy theo ứng dụng và thiết kế bán dẫn cụ thể.

4. **On Cloud NFS:** Với các job EDA ghi dữ liệu trung gian không cần thiết trên hệ thống tại chỗ, một [Amazon FSx for NetApp ONTAP](https://aws.amazon.com/fsx/netapp-ontap/) filesystem đã được cung cấp để compute resources trên AWS sử dụng.

5. **Synopsys Cloud Hybrid Solution:** Người dùng cài đặt binary này trên Amazon EC2 instance và cấu hình data-sync để xử lý việc di chuyển dữ liệu giữa on-prem và AWS.

6. **Licensing:**
    1. **Licenses cho ứng dụng EDA:** Các license ứng dụng EDA hiện có và license server tiếp tục cấp license cho các job chạy trên AWS. Các nhu cầu license bổ sung có thể được đáp ứng bằng Synopsys [FlexEDA](https://www.synopsys.com/blogs/chip-design/what-is-flexeda.html) và Pay-Per-Use metered licensing.  
    2. **License cho Hybrid solution:** Đây là một ứng dụng riêng biệt mà người dùng cần mua từ Synopsys. License được cung cấp từ hệ thống network license server do Synopsys quản lý.

### Thiết lập Synopsys Cloud Hybrid Solution

Việc thiết lập bao gồm 3 thành phần chính:

1. **Hybrid Cloud data-sync**: Bao gồm cài đặt Hybrid solution trên một loại instance được khuyến nghị trên AWS, cấu hình mạng để cho phép lưu lượng giữa on-premises và AWS cho license (của Hybrid Cloud solution), lưu trữ dữ liệu và xử lý phân tán, xác định các mount lưu trữ NFS tại chỗ cần ánh xạ, và khởi chạy Hybrid solution để thiết lập data-sync mapping.
2. **Network Connectivity**: Các kết nối mạng chuyên dụng như [AWS DirectConnect](https://aws.amazon.com/directconnect/) cung cấp băng thông cao hơn, độ trễ thấp hơn, rất phù hợp để xử lý khối lượng công việc với lượng dữ liệu lớn. Ngoài ra, có thể dùng đường hầm VPN IPsec với AWS, nhưng tốc độ và độ tin cậy kém hơn so với kết nối chuyên dụng.
3. **Scheduler setup**: Phụ thuộc vào từng scheduler cụ thể. Ví dụ, với IBM LSF, điều này bao gồm việc triển khai LSF multi-cluster, định nghĩa các cluster tham gia, cấu hình queue và xác minh rằng cluster trên AWS có thể được cung cấp động theo nhu cầu.

### Thông tin chung về nền tảng

Với , dữ liệu được chọn lọc được ghi bởi một tác vụ chạy trên đám mây có thể được ghi ngược trở lại hệ thống on-premises theo thời gian thực, giúp kho lưu trữ tại chỗ luôn được cập nhật. Lưu ý rằng việc ghi dữ liệu ngược lại sẽ phát sinh phí truyền dữ liệu ra khỏi AWS. Dữ liệu đầu ra tạm thời từ các tác vụ đang chạy không cần thiết cho on-prem hoặc dữ liệu đầu ra lớn, lưu trữ lâu dài có thể được chuyển hướng đến NFS trên đám mây. Nếu cần, dữ liệu này có thể được lập trình để ghi ngược lại sau khi tác vụ hoàn tất.

Bộ lập lịch tác vụ nên được cung cấp bởi khách hàng. Sau đó, nó sẽ tìm tài nguyên tính toán phù hợp, tại chỗ hoặc trên AWS, và Giải pháp Lai sẽ xử lý việc di chuyển dữ liệu cần thiết. Giải pháp Synopsys Cloud Hybrid có khả năng cấu hình bộ lập lịch để tự động sử dụng hết công suất tính toán tại chỗ trước, sau đó lập lịch các tác vụ trên các nút tính toán đám mây, hoặc chạy tất cả tác vụ trên các nút đám mây tùy thuộc vào ứng dụng đang chạy và kích thước/tần suất dữ liệu được chia sẻ giữa các tiến trình khác nhau của ứng dụng.

### Kiểm thử khả năng mở rộng giải pháp Synopsys Hybrid trên AWS

Các job EDA có thể rất nặng về dữ liệu, cả ở đầu vào và đầu ra. Độ trễ của mạng và lượng dữ liệu di chuyển qua lại có thể ảnh hưởng đến hiệu năng của job EDA. Để hiểu rõ giới hạn của Synopsys Hybrid Solution, chúng tôi đã sử dụng sáu ứng dụng chủ lực (flagship applications) của Synopsys vốn rất quan trọng trong quy trình thiết kế mỗi chip bán dẫn. Bao gồm:

- [PrimeLib](https://www.synopsys.com/implementation-and-signoff/signoff/primelib.html) – ứng dụng đặc tả và thẩm định thư viện
- [Synopsys VCS](https://www.synopsys.com/verification/simulation/vcs.html) – Trình mô phỏng để xác minh thiết kế bán dẫn
- [PrimeSim SPICE](https://www.synopsys.com/implementation-and-signoff/ams-simulation/primesim-spice.html) – Trình mô phỏng SPICE tăng tốc bằng GPU cho thiết kế Analog, RF, và Mixed-signal
- [Synopsys PrimeWave](https://www.synopsys.com/implementation-and-signoff/ams-simulation/primewave.html) – ứng dụng cho việc thiết lập mô phỏng và phân tích thiết kế Analog, RF, Mixed-signal, custom-digital và thiết kế bộ nhớ
- [PrimeTime](https://www.synopsys.com/implementation-and-signoff/signoff/primetime.html) – ứng dụng phân tích định thời tĩnh với khả năng tính toán hiệu quả về bộ nhớ, hỗ trợ scalar và đa nhân
- [Synopsys DSO.ai](https://www.synopsys.com/ai/ai-powered-eda/dso-ai.html) – ứng dụng tối ưu không gian thiết kế được hỗ trợ bởi AI

Tất cả các ứng dụng EDA này có đặc điểm khác nhau về pattern I/O, lượng dữ liệu sinh ra (kích thước và số lượng file), cũng như lượng và tần suất giao tiếp giữa các worker của một job. Mỗi ứng dụng được thực thi bằng Synopsys Cloud Hybrid Solution với các thiết kế và testcase chuẩn. Chúng tôi ưu tiên các job yêu cầu IOPs cao khi chọn testcase cho bài đo chuẩn.

Chúng tôi theo dõi nhiều chỉ số và so sánh chúng giữa các thử nghiệm thực hiện trên Synopsys Cloud Solution với AWS và trên hạ tầng on-premises tương đương:

1. **Hiệu năng**: Thời gian chạy là chỉ số then chốt vì nó trực tiếp tác động đến “time to market”.
2. **Chất lượng kết quả** (QoR): QoR là một chỉ số quan trọng khác, không thể bị ảnh hưởng. Các ứng dụng phân tích kết quả về coverage, bài kiểm thử pass/fail, các regression và đưa ra cách diễn giải về chất lượng tổng thể của kết quả. Với các ứng dụng được thử nghiệm, chúng tôi kỳ vọng sẽ có kết quả QoR giống hoặc tương tự giữa AWS và on-premises.
1. **Thời gian thiết lập**: Nếu hiệu năng và QoR tương đương, điểm làm cho Synopsys Cloud Hybrid Solution trở nên đáng giá chính là thời gian có thể tiết kiệm được trong việc di chuyển dữ liệu liên quan lên cloud để sử dụng hạ tầng tính toán của AWS. Dù khó đo lường với hệ thống on-premises và khác nhau đáng kể giữa các EDA flow, chúng tôi đã cố gắng ước lượng.

### Kết quả
#### Hiệu suất

![Figure](/images/IMG-2025-09-23-16.26.12@2x.png)
*Table 1: Bảng 1: Hiệu năng của các ứng dụng Synopsys chạy trên Hybrid Solution với AWS so với on-premises*

Chúng tôi chạy bộ kiểm thử baseline này trên on-premises hoặc trên AWS tùy theo tình trạng sẵn có của tài nguyên tại chỗ. Bảng 1 cho thấy hiệu năng tổng thể của tất cả các EDA flow được thử nghiệm bằng Synopsys Cloud Hybrid Solution là tương đương – hoặc trong một số trường hợp còn tốt hơn – so với baseline. Với Hybrid Setup, thời gian chạy bao gồm cả thời gian ghi dữ liệu đầu ra cuối cùng trở lại lưu trữ on-premises thông qua Hybrid Solution. Điều này làm hiệu năng tổng thể bị ảnh hưởng nhẹ khi so với việc chạy baseline trực tiếp trên cloud, như trong trường hợp PrimeLib và VCS. Dữ liệu cũng cho thấy hiệu năng tốt hơn so với baseline chạy on-premises đối với PrimeTime và PrimeSim, nhờ có sẵn CPU nhanh hơn trên AWS.

Thông qua việc phân tích IO pattern (kích thước, tần suất) của các ứng dụng EDA khác nhau, chúng tôi đã xác định một số best practices để thiết lập các ứng dụng này nhằm tận dụng tối đa Hybrid Solution.

#### Chất lượng kết quả (QoR)

Như dự đoán, không có sự suy giảm về chất lượng kết quả, PPA hay coverage khi sử dụng Hybrid Solution. Với các ứng dụng EDA như VCS, PrimeSim, kết quả khớp hoàn toàn với các lần chạy on-premises. Với các ứng dụng khác như DSO.ai, các báo cáo, PPA và QoR đều tương đương.

#### Thời gian thiết lập:

Synopsys Hybrid Cloud tiết kiệm tới vài tuần thiết lập cho mỗi dự án nhờ tự động hóa việc di chuyển dữ liệu thủ công và xác minh các design block. Ví dụ, từ thử nghiệm nội bộ của chúng tôi với QA regressions của một ứng dụng EDA, khoảng 4 tuần công sức thủ công đã được tiết kiệm nhờ Hybrid Solution loại bỏ nhu cầu "lift and shift" các workload EDA.

Tùy theo workflow, Synopsys có thể hỗ trợ đưa ra khuyến nghị best practices ở chế độ cloud-native hoặc burst mode với Synopsys Cloud Hybrid Solution. Ở chế độ burst mode đúng nghĩa, dữ liệu sẽ được ghi vào on-cloud NFS, sau đó dữ liệu chọn lọc được đồng bộ ngược lại on-premises sau khi job hoàn tất. Cách này giúp giảm thiểu chi phí data egress và ảnh hưởng đến hiệu năng. Burst mode mang lại giá trị lớn bằng cách di chuyển dần dần dữ liệu đầu vào cần thiết lên cloud để chạy job thông qua Hybrid Solution.

### Kết luận

EDA workload đòi hỏi sức mạnh tính toán khổng lồ và khả năng truy cập dữ liệu liền mạch. Khối lượng dữ liệu thiết kế rất lớn, kết hợp với tính lặp đi lặp lại và mức độ phụ thuộc cao của các tác vụ EDA, khiến việc di chuyển dữ liệu liên tục giữa lưu trữ on-premises và compute trên cloud có thể trở nên chậm và kém hiệu quả.

[Synopsys Cloud Hybrid Solution](https://www.synopsys.com/cloud.html) giải quyết vấn đề này bằng cách cung cấp phương thức liền mạch để burst các job EDA từ on-premises lên cloud với cơ chế đồng bộ dữ liệu hai chiều theo thời gian thực. Sản phẩm đã được kiểm thử tải nặng (stress-tested) với sáu ứng dụng EDA chủ lực của Synopsys. Chúng tôi nhận thấy hiệu năng của các ứng dụng ở chế độ Hybrid là tương đương với việc chạy on-premises hoặc cloud-native, đồng thời vẫn giữ nguyên chất lượng kết quả (QoR). Việc di chuyển dữ liệu được xử lý một cách “vô hình” bởi Synopsys Cloud Hybrid Solution, giúp tiết kiệm tới nhiều tuần thiết lập.

---

### Varun Shah
<div style="display: flex; align-items: center; gap: 15px;">

<img src="/images/IMG-2025-09-23-16.35.10@2x.png" alt="Varun Shah" width="150"/>

<div>
Varun Shah làm việc trong nhóm quản lý sản phẩm cho Synopsys Cloud, chịu trách nhiệm về lộ trình công nghệ, tích hợp phần mềm EDA với nền tảng đám mây và phân tích phản hồi từ khách hàng. Ông có bằng Thạc sĩ Kỹ thuật Điện từ Đại học Missouri-Rolla và là chuyên gia quản lý sản phẩm được chứng nhận từ Trường Quản lý Kellogg.
</div>
</div>

---

### Dnyanesh Digraskar
<div style="display: flex; align-items: center; gap: 15px;">
  <img src="/images/dnyanesh.png" alt="Dnyanesh Digraskar" width="150"/>
  <div>
Dnyanesh Digraskar là Kiến trúc sư Giải pháp Chủ chốt (Principal HPC Partner Solutions Architect) tại AWS. Ông dẫn dắt chiến lược triển khai HPC với các đối tác ISV để giúp họ xây dựng giải pháp theo kiến trúc tốt, có thể mở rộng. Ông có hơn 15 năm kinh nghiệm trong lĩnh vực CFD, CAE, mô phỏng số học và khoa học hiệu năng cao (HPC). Ông tốt nghiệp Thạc sĩ Kỹ thuật Cơ khí tại Đại học Massachusetts, Amherst.
  </div>
</div>

---

### Mayur Runwal
<div style="display: flex; align-items: center; gap: 15px;">

<img src="/images/IMG-2025-09-23-16.35.44@2x.png" alt="Mayur Runwal" width="150"/>

<div>
Mayur Runwal là Kiến trúc sư Giải pháp cao cấp tại AWS, chuyên về tự động hóa thiết kế điện tử (EDA). Ông thiết kế các luồng công việc thiết kế và xác minh chip cho khách hàng AWS. Trước khi gia nhập AWS, ông đã lãnh đạo các nhóm hạ tầng CNTT tại các công ty bán dẫn trong 10 năm, với kinh nghiệm bao gồm thiết kế và triển khai giải pháp máy tính hiệu năng cao cũng như hạ tầng doanh nghiệp.
</div>
</div>

---

### Xingang Zhao
<div style="display: flex; align-items: center; gap: 15px;">

<img src="/images/IMG-2025-09-23-16.35.23@2x.png" alt="Xingang Zhao" width="150"/>

<div>
Xingang Zhao là Quản lý Sản phẩm Kỹ thuật (Technical Product Manager) cho Synopsys Cloud. Anh chịu trách nhiệm đánh giá kỹ thuật và tích hợp các dịch vụ/ công cụ đám mây mới lên các nền tảng công cộng nhằm tăng hiệu năng và tiết kiệm chi phí cho các khối công việc EDA. Anh có bằng Cử nhân Kỹ thuật Điện từ Đại học Zhejiang và được chứng nhận quản lý sản phẩm tại Trường Kellogg.
</div>
</div>