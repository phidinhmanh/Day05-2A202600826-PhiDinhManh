# Thin SPEC — RiskMap Weekend Reporter

Bản đặc tả tối giản chốt thiết kế và phạm vi sản phẩm phục vụ cho việc lập trình prototype trong Day 06.

---

## 1. Track, product/app và user

*   **Track:** AI-powered Business Tool / Operations Management
*   **Product/app thật:** Ứng dụng Quản lý vận hành & Giám sát chất lượng dịch vụ chuỗi cửa hàng dịch vụ (F&B, Spa, Bán lẻ).
*   **User cụ thể:** Chủ chuỗi cửa hàng (Chain Owner) – người sở hữu từ 3 chi nhánh trở lên, quản lý gián tiếp qua các Quản lý cửa hàng (Store Manager), thường xuyên bận rộn và không thể tự đọc từng review của khách hàng.
*   **Nhóm có phải user thật không?** Không. Nhưng nhóm đã phỏng vấn trực tiếp chủ chuỗi cafe/trà sữa thực tế để làm nguồn đối chiếu và nắm bắt pain point.

---

## 2. Evidence summary

| Evidence (Bằng chứng) | Nguồn (Source) | User/pain nói lên điều gì? | SPEC phải đổi gì? |
|---|---|---|---|
| Bật thông báo đẩy real-time cho hàng chục review mỗi ngày dẫn đến alert fatigue, chủ chuỗi tắt hết thông báo và bỏ lỡ các review nghiêm trọng. | Self-use (Giả lập quản lý 5 cửa hàng) | Nhận thông báo lẻ tẻ quá nhiều gây loãng thông tin, chủ chuỗi cần báo cáo định kỳ hơn là thời gian thực. | Bỏ tính năng alert real-time. Thay thế bằng báo cáo tổng hợp cuối tuần định kỳ (Weekend Report). |
| Chủ chuỗi chia sẻ: *"Chỉ biết quán có vấn đề khi khách đã đăng bài bóc phốt lên hội nhóm review ăn uống."* | Phỏng vấn trực tiếp chủ chuỗi cafe | Thiếu tính chủ động kiểm soát chất lượng vận hành từ sớm, chỉ đi giải quyết hậu quả khủng hoảng (cứu cháy). | AI tập trung phân tích text review để gọi tên các lỗi vận hành cốt lõi, giúp chấn chỉnh sớm. |
| Nhiều review tiêu cực nhưng ngắn ngủi, chung chung như *"Tệ"*, *"Chán"* khiến AI khó phân loại. | Review thực tế trên Google Maps/Facebook | AI có nguy cơ phân loại sai hoặc bỏ sót nếu dữ liệu thô quá ít ngữ cảnh. | Bổ sung nhãn cảnh báo cho các review thiếu thông tin và cơ chế gán nhãn thủ công (Correction). |

---

## 3. Pain statement

> **Chủ chuỗi cửa hàng** đang gặp khó khăn ở **bước theo dõi chất lượng vận hành thực tế tại các chi nhánh**, vì **họ không thể đọc hàng trăm review mỗi ngày từ nhiều nguồn (Google Maps, Fanpage, Foody) và dễ bị quá tải thông tin (alert fatigue) dẫn đến việc bỏ sót các lỗi hệ thống nghiêm trọng**, dẫn tới **chất lượng dịch vụ đi xuống và chỉ biết sự cố khi khách hàng đã đăng bài bóc phốt công khai trên mạng xã hội**.
> Bằng chứng chính là các phỏng vấn thực tế từ chủ chuỗi quán trà sữa mệt mỏi vì đi dập khủng hoảng truyền thông và trải nghiệm tự dùng thử nhận hàng chục thông báo rác mỗi ngày.

---

## 4. Build slice (Lát cắt prototype Day 06)

```text
Cho [chủ chuỗi cửa hàng] đang cần [đọc báo cáo tổng hợp lỗi cuối tuần của một chi nhánh],
prototype sẽ dùng AI để [đọc toàn bộ review tiêu cực trong tuần, phân nhóm (clustering) và đúc kết thành 3 vấn đề vận hành nổi cộm nhất],
tạo ra [một đoạn văn bản Markdown tổng hợp gửi qua email/Telegram gồm: Tên nhóm lỗi + Tỷ lệ lặp lại + Câu quote chứng minh của khách],
và xử lý [lỗi gom nhóm sai ngữ cảnh (False Correlation)] bằng cách [bắt buộc hiển thị nguyên văn (Exact Quotes) tối thiểu 2 câu review thô dưới mỗi nhóm lỗi để đối chiếu nhanh].
```

---

## 5. Auto/Aug decision

*   [x] **Augmentation:** AI đóng vai trò là Trợ lý gợi ý (Augmented Decision). AI chỉ phân tích, gom nhóm và gọi tên lỗi. Chủ chuỗi giữ toàn quyền quyết định có xuống kiểm tra chi nhánh đó hay không. AI tuyệt đối **không tự động gửi** báo cáo này cho Quản lý cửa hàng (Store Manager).
*   [ ] **Conditional automation**
*   [ ] **Automation**

*   **Lý do chọn:** Các quyết định nhân sự và chấn chỉnh cửa hàng rất nhạy cảm. AI chỉ giúp tổng hợp thông tin thô để giảm tải cho chủ chuỗi, con người vẫn phải là người ra quyết định cuối cùng dựa trên các yếu tố thực tế khác ngoài review.
*   **Human role:** **Decider & Trainer** (Chủ chuỗi duyệt thông tin và huấn luyện lại AI thông qua tính năng sửa lỗi).

---

## 6. Four paths (Thiết kế 4 kịch bản trải nghiệm)

| Path | Kịch bản Prototype phải thể hiện | Trải nghiệm UI/UX trên Báo cáo |
|---|---|---|
| **Happy** | Có 15 review chê điều hòa hỏng tại chi nhánh A. AI phân nhóm chính xác và tóm tắt thành lỗi vận hành cụ thể. | Báo cáo Markdown hiển thị: **"1. Vấn đề nổi cộm: Hạ tầng - Máy lạnh chảy nước ở tầng 2 (15 lượt nhắc)"** kèm 2 câu quote của khách. |
| **Low-confidence** | Có các review ngắn và chung chung như *"Tệ"*, *"Thái độ không tốt"* (không rõ nhân viên nào, lỗi gì cụ thể). AI phân vân. | Gom các review này vào nhóm lỗi kèm nhãn cảnh báo: **"[Hệ thống chưa đủ dữ liệu để phân loại chính xác - Cần xem thêm review thô]"** để chủ chuỗi tự bấm vào xem chi tiết nếu muốn. |
| **Failure** | Khách chê bằng văn hóa bản địa, từ lóng mới (ví dụ: *"nhân viên báo quá báo"*, *"quán phè phỡn"*). AI không hiểu ngữ cảnh và bỏ sót, không đưa vào báo cáo tuần. | Review bị trôi mất và nằm ngoài báo cáo tổng hợp. |
| **Correction** | Chủ chuỗi kiểm tra file log thô của tuần, phát hiện các review bị bỏ sót hoặc gom nhóm sai. | Chủ chuỗi bấm nút **[Gắn nhãn thủ công]** ngay bên cạnh review thô để ép review đó vào nhóm lỗi tương ứng, giúp AI tự học và nhận diện đúng cho các tuần sau. |

---

## 7. Failure mode nguy hiểm nhất

```text
Nếu AI [gom nhóm sai ngữ cảnh (False Correlation)],
AI có thể [gom các từ không liên quan thành một lỗi hệ thống nguy hiểm (Ví dụ: Khách khen "Nhân viên nhiệt tình như người nhà" và khách chê "Nhân viên nói chuyện việc nhà quá to" đều bị AI gom chung vào nhóm lỗi #nhan_vien_thieu_chuyen_nghiep)],
hậu quả là [chủ chuỗi đánh giá sai lệch năng lực của nhân viên, gây ức chế nội bộ hoặc đưa ra các quyết định phạt oan].
Prototype sẽ xử lý bằng cách [bắt buộc trích dẫn nguyên văn (Exact Quotes) tối thiểu 2 câu review thô của khách ngay dưới mỗi tiêu đề nhóm lỗi]. Chủ chuỗi chỉ cần liếc mắt qua các câu quote là có thể đối chiếu ngay AI gom nhóm đúng hay sai ngữ cảnh.
Owner kiểm thử path này là [Thành viên E - Phụ trách Test/Demo].
```

---

## 8. Owner plan cho sáng Day 06

| Thành viên | Việc phụ trách | Bằng chứng cần có trong repo |
|---|---|---|
| **Thành viên A** | Research / evidence | File `evidence-pack.md` hoàn chỉnh, chứa dữ liệu mock review thô của các cửa hàng để nạp cho AI. |
| **Thành viên B** | SPEC / Prompt engineering | File `thin-spec.md` chi tiết và các prompt system dùng để phân nhóm (clustering) và tóm tắt (summarize) review. |
| **Thành viên C** | Frontend Prototype / Telegram Integration | Giao diện mockup Telegram Bot nhận báo cáo Markdown định kỳ từ hệ thống. |
| **Thành viên D** | AI Logic / Backend Mock | Server Python/Node.js nhận review thô, chạy prompt LLM phân tích, phân loại nhóm lỗi và trả ra output Markdown. |
| **Thành viên E** | Test / Demo script | Kịch bản demo 3 phút: Nạp file review thô -> Gửi báo cáo qua Telegram -> Demo case Low-confidence và kiểm thử Correction (gán nhãn sửa đổi). |
