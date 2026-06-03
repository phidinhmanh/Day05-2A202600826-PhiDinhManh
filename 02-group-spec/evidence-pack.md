# Evidence Pack — Nhóm RiskMap (AI Review Analyzer)

## 1. Nhóm và track

*   **Tên nhóm:** Nhóm 05 - RiskMap
*   **Track:** AI-powered Business Tool / Operations Management
*   **Product/app đã chọn:** Ứng dụng Quản lý & Giám sát vận hành chuỗi cửa hàng tích hợp AI.
*   **Build slice đang nghĩ:** Hệ thống đọc toàn bộ review tiêu cực trong tuần của các chi nhánh, tự động gom nhóm (clustering) và đúc kết thành **3 vấn đề vận hành nổi cộm nhất** gửi định kỳ dưới dạng email/Telegram cho chủ chuỗi vào cuối tuần.

---

## 2. Self-use evidence (Bằng chứng tự trải nghiệm)

Nhóm giả lập tình huống làm chủ chuỗi 5 cửa hàng và tự theo dõi review khách hàng:

| Observation (Quan sát thực tế) | Screenshot/link | Path liên quan | Điều học được |
|---|---|---|---|
| Bật thông báo đẩy (push notification) thời gian thực mỗi khi có review trên Google Maps/Facebook của các chi nhánh -> Nhận hơn 50 thông báo mỗi ngày. | [Link ảnh minh họa 1](file:///d:/Work/project/VINAI/Batch02-Day05-AI-Product-Labs/02-group-spec/assets/self_use_1.png) | Failure Path (Alert fatigue) | Quá nhiều thông báo vụn vặt gây nhiễu và làm loãng sự tập trung. Chủ chuỗi nhanh chóng bị quá tải thông tin (alert fatigue) và có xu hướng tắt thông báo. |
| Sau khi tắt thông báo để tránh làm phiền, nhóm đã bỏ lỡ 1 review cực kỳ nghiêm trọng về việc nhân viên chi nhánh 3 phân biệt đối xử với khách. 3 ngày sau sự việc bùng nổ trên MXH mới biết. | [Link ảnh minh họa 2](file:///d:/Work/project/VINAI/Batch02-Day05-AI-Product-Labs/02-group-spec/assets/self_use_2.png) | Failure Path (Missed issues) | Việc theo dõi thủ công hoặc tắt hoàn toàn thông báo đều gây rủi ro lớn cho vận hành chuỗi. Cần một cơ chế tổng hợp có bộ lọc thay vì thông báo thời gian thực. |

---

## 3. User / review / social evidence (Bằng chứng từ nguồn ngoài)

Nhóm đã thực hiện phỏng vấn nhanh và khảo sát ý kiến của các chủ chuỗi cửa hàng dịch vụ (F&B, Spa, Bán lẻ):

| Quote / review / observation | Nguồn | User là ai? | Pain/failure mode |
|---|---|---|---|
| *"Tôi quản lý 4 quán cà phê. Mỗi ngày có hàng trăm review trên Facebook, Foody, Google Maps. Tôi không thể nào đọc hết được. Tôi chỉ biết quán có vấn đề khi khách đã viết bài bóc phốt lên hội nhóm, lúc đó đi giải quyết hậu quả vô cùng mệt mỏi."* | Phỏng vấn trực tiếp | Chủ chuỗi cafe tại Hà Nội | Pain: Bị động giải quyết khủng hoảng (cứu cháy) thay vì chủ động kiểm soát chất lượng vận hành. |
| *"Nếu hệ thống cứ có review chê là tinh tinh điện thoại thì tôi phát điên mất vì có rất nhiều review vô thưởng vô phạt hoặc chê những thứ lặt vặt. Cái tôi cần là biết trong tuần qua chi nhánh nào đang gặp lỗi hệ thống (ví dụ điều hòa hỏng liên tục hoặc thái độ nhân viên ca tối tệ) để xuống chấn chỉnh."* | Khảo sát cộng đồng chủ doanh nghiệp F&B | Chủ chuỗi cửa hàng trà sữa (3 chi nhánh) | Pain: Cần bức tranh toàn cảnh (bản đồ rủi ro) tổng hợp định kỳ hơn là thông tin thời gian thực. |

---

## 4. Competitor / analog evidence (Phân tích đối thủ)

| App / mô hình tham khảo | Họ xử lý task này thế nào? | Pattern học được | Có áp dụng trong 1 ngày không? |
|---|---|---|---|
| **Google Business Suite / Fanpage Manager** | Gửi thông báo đẩy tức thời cho từng review mới hoặc gửi email báo cáo hàng tháng chỉ ghi nhận số lượng sao trung bình. | **Hạn chế:** Số lượng sao trung bình không chỉ ra được nguyên nhân vận hành (ví dụ: điểm giảm do thái độ nhân viên hay do cơ sở vật chất). | **Có:** Chúng ta sẽ cải tiến bằng cách đi sâu vào nội dung text của review để phân nhóm lỗi thay vì chỉ đếm sao. |
| **Các công cụ Social Listening (như Buzzmetrics)** | Quét và phân tích sentiment (tích cực/tiêu cực) trên diện rộng của toàn thương hiệu. | **Hạn chế:** Quá rộng, không chỉ ra cụ thể lỗi vận hành theo từng chi nhánh/địa điểm cụ thể để chấn chỉnh. | **Có:** Thu hẹp phạm vi quét theo từng chi nhánh cụ thể của một chuỗi. |

---

## 5. Evidence -> Insight

*   **Evidence nổi bật nhất:** Chủ chuỗi bị quá tải thông tin (alert fatigue) nếu nhận thông báo đẩy liên tục và có xu hướng tắt thông báo dẫn đến bỏ sót lỗi nghiêm trọng, chỉ đi giải quyết khi sự việc đã bùng nổ (cứu cháy).
*   **Insight:** Chủ chuỗi không chỉ gặp vấn đề về mặt đọc tin nhắn. Họ thực ra cần **hỗ trợ ra quyết định mang tính chiến thuật (decision support)**. Họ không cần biết từng khách hàng lẻ tẻ phàn nàn gì vào lúc này; họ cần một **"bản đồ rủi ro"** tổng hợp vào cuối tuần để biết chi nhánh nào đang có dấu hiệu tệ đi và lỗi hệ thống nổi cộm là gì.
*   **Opportunity:** AI có thể giúp bằng cách **phân nhóm (clustering) và đúc kết (summarizing)** toàn bộ các review tiêu cực trong tuần của từng chi nhánh, chuyển từ thế bị động cứu cháy sang thế chủ động tối ưu vận hành dựa trên dữ liệu tổng hợp định kỳ.

---

## 6. Evidence đổi SPEC như thế nào?

*   [x] Đổi user chính.
*   [x] Đổi pain statement.
*   [x] Đổi build slice.
*   [x] Đổi Auto/Aug decision.
*   [x] Đổi 4 paths.
*   [x] Đổi failure mode.

**Thay đổi quan trọng:**
*   *Trước evidence, nhóm định:* Build một ứng dụng gửi alert ngay lập tức cho chủ chuỗi khi có review tiêu cực kèm chatbot AI để chủ chuỗi chat nhắn tin trực tiếp với khách hàng.
*   *Sau evidence, nhóm đổi thành:* Bỏ phần gửi alert real-time và chatbot phản hồi khách. Tập trung hoàn toàn vào **"Báo cáo tổng hợp lỗi cuối tuần (Weekend Risk Map Summary) gửi qua email/Telegram đúc kết 3 nhóm lỗi nổi cộm nhất kèm quote thực tế của khách"**.
*   *Lý do:* Tránh gây alert fatigue cho chủ chuỗi và tập trung giải quyết nhu cầu cốt lõi là kiểm soát chất lượng vận hành định kỳ của chuỗi.
