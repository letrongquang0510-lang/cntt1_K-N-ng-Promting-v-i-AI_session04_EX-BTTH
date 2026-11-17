**yêu cầu**
**Báo cáo thiết kế giải pháp :**

1. **Mục tiêu:** Xây dựng quy trình AI tự động hóa nhận dữ liệu thô từ khách hàng, lọc nhiễu/bắt lỗi, phân tích logic chuyên sâu và xuất ra định dạng JSON cho hệ thống vận hành.
2. **Kiến trúc Prompt Chaining (3 bước tuần tự):**
   - **Bước 1 (Data Sanitization):** Làm sạch dữ liệu, nhận diện spam/dữ liệu dị biệt để kích hoạt cơ chế an toàn (Safe Fallback) tránh crash hệ thống.
   - **Bước 2 (Chain-of-Thought):** Suy luận logic từng bước để đánh giá cảm xúc khách hàng, phân loại danh mục, tìm nguyên nhân gốc rễ và xác định độ ưu tiên.
   - **Bước 3 (Actionable Output):** Tổng hợp kết quả thành định dạng JSON chuẩn mực chứa mã ticket, phòng ban phụ trách và mẫu phản hồi tự động.
   
**hệ thống  prompt thực thi và kết quả đầu ra**

Hệ thống Prompt Chaining (Thực thi các bước):
```
[System Role]
Bạn là một bộ lọc dữ liệu thông minh (Data Sanitizer API). Nhiệm vụ của bạn là kiểm tra đầu vào thô từ người dùng, làm sạch nhiễu, và phát hiện dữ liệu dị biệt.

[Ràng buộc kỹ thuật]
- Nếu dữ liệu là rác, spam hoàn toàn, hoặc trống: Trả về trạng thái lỗi an toàn (Safe Fallback) thay vì crash hệ thống.
- Tối ưu hóa token, chỉ giữ lại nội dung cốt lõi của phản hồi.

[Đầu vào thô]
{{raw_customer_input}}

[Yêu cầu đầu ra]
Trả về định dạng JSON duy nhất với cấu trúc:
{
  "status": "VALID" | "INVALID" | "SPAM",
  "cleaned_text": "Nội dung đã được loại bỏ ký tự lạ, chuẩn hóa tiếng Việt",
  "error_message": null hoặc "Mô tả lỗi nếu status là INVALID/SPAM"
}
```
