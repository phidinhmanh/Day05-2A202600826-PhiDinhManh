# Synthesis & Decide — Nhóm RiskMap (AI Review Analyzer)

Tài liệu đúc kết từ bằng chứng thực tế sang định hướng lát cắt thiết kế (Build Slice) cho Day 06.

---

## 1. Gom evidence thành các cụm vấn đề (Pain Clusters)

Chúng tôi gom các bằng chứng thu thập được thành 2 cụm vấn đề chính:
1.  **Cụm "Alert Fatigue" (Quá tải thông báo):** Nhận quá nhiều thông báo thời gian thực về các review nhỏ lẻ dẫn đến việc chủ chuỗi tắt hết thông báo, bỏ lỡ các sự cố nghiêm trọng.
2.  **Cụm "Bị động cứu cháy":** Chủ chuỗi không có cái nhìn tổng quát về chất lượng vận hành của các chi nhánh theo thời gian, chỉ đi xử lý sự cố khi khách đã đăng bài bóc phốt công khai trên mạng xã hội.

---

## 2. Viết Insight

> Chủ chuỗi cửa hàng dịch vụ/F&B không chỉ cần biết khách hàng đang nói gì về thương hiệu của họ một cách đơn lẻ. Họ thật ra cần một **bản đồ rủi ro vận hành có tính hệ thống**, giúp họ nhận diện nhanh những chi nhánh nào đang tệ đi và các lỗi lặp đi lặp lại nhiều lần (ví dụ: máy lạnh hỏng, nhân viên ca tối thái độ kém) để kịp thời sửa đổi trước khi xảy ra khủng hoảng truyền thông.

---

## 3. Viết Opportunity

> Cơ hội là sử dụng AI để **tự động thu thập, phân nhóm (clustering) và tóm tắt (summarizing)** toàn bộ review tiêu cực trong tuần của từng chi nhánh, cô đọng thành **3 vấn đề vận hành nổi cộm nhất** gửi định kỳ vào cuối tuần, giúp chủ chuỗi chuyển từ thế bị động cứu cháy sang thế chủ động tối ưu vận hành dựa trên dữ liệu tổng hợp.

---

## 4. Đánh giá Build Slice (5 câu hỏi sàng lọc)

Chúng tôi đánh giá lát cắt đề xuất **"Báo cáo tổng hợp lỗi cuối tuần của một chi nhánh"** qua 5 tiêu chí:

| Câu hỏi | Trạng thái | Đánh giá chi tiết cho RiskMap |
|---|---|---|
| **User cụ thể chưa?** | **ĐẠT** | Chủ chuỗi cửa hàng (ví dụ chuỗi F&B, thời trang, spa) - người trực tiếp quản lý nhiều địa điểm nhưng không trực tiếp đứng cửa hàng. |
| **Task đủ hẹp chưa?** | **ĐẠT** | Demo được trong 3 phút: Nạp 30 review thô của 1 tuần -> AI xử lý -> Xuất báo cáo Markdown gồm 3 nhóm lỗi nổi bật nhất kèm tỷ lệ lặp lại và quote chứng minh gửi qua Telegram/Email. |
| **AI decision rõ chưa?** | **ĐẠT** | AI phân nhóm (Clustering) các review tiêu cực có cùng ngữ cảnh và tóm tắt (Summarization) thành nhóm lỗi vận hành cụ thể. |
| **Failure path rõ chưa?** | **ĐẠT** | Case test failure: Review quá ngắn/chung chung hoặc dùng từ lóng bản địa -> AI phân loại vào nhóm mơ hồ hoặc bỏ sót -> Demo sẽ hiển thị cách khắc phục bằng nhãn cảnh báo và nút gắn nhãn thủ công (Correction). |
| **Có evidence không?** | **ĐẠT** | Có bằng chứng từ phỏng vấn thực tế chủ chuỗi F&B mệt mỏi vì phải đi "cứu cháy" các vụ bóc phốt và quá tải thông báo vụn vặt. |

---

## 5. Quyết định chiến lược

*   **Quyết định:** **Giảm scope hệ thống Alert real-time và phản hồi tự động** -> Tập trung 100% tài nguyên vào việc xây dựng **Báo cáo tổng hợp lỗi vận hành cuối tuần cho một chi nhánh**.
*   **Lý do:** Đây là lát cắt mang lại giá trị cao nhất cho chủ chuỗi, tránh tình trạng alert fatigue và giải quyết trực tiếp bài toán chấn chỉnh chất lượng dịch vụ định kỳ.

---

## 6. Câu chốt định hướng (The Golden Sentence)

> **Dựa trên** bằng chứng chủ chuỗi bị quá tải thông báo đẩy và có xu hướng bỏ lỡ các review lỗi nghiêm trọng dẫn đến khủng hoảng, **nhóm sẽ build** một prototype tính năng **RiskMap Weekend Reporter**, **cho** chủ chuỗi cửa hàng, **để giải quyết** pain point bị động cứu cháy trong quản lý vận hành, **bằng cách** dùng AI phân nhóm và tóm tắt review để **augment** quyết định kiểm tra chi nhánh dưới dạng báo cáo Markdown gửi cuối tuần, **và sẽ test failure path** khi AI gom nhóm sai ngữ cảnh (False Correlation) bằng cách bắt buộc hiển thị 2 câu quote trích dẫn nguyên văn thô dưới mỗi nhóm lỗi để user đối chiếu nhanh.

---

## 7. Backlog (Không build trong Day 06)

*   Hệ thống gửi thông báo đẩy real-time cho các review 1 sao.
*   Chatbot AI tự động soạn thảo câu trả lời phản hồi khách hàng trên Google Maps/Facebook.
*   Tính năng tích hợp API với các phần mềm POS để đối chiếu review với hóa đơn mua hàng thực tế.
*   Bảng điều khiển (Dashboard) biểu đồ trực quan hóa dữ liệu cho toàn chuỗi theo thời gian thực.
