# Ngày 1 — Bài Tập & Phản Ánh
## Nền Tảng LLM API | Phiếu Thực Hành

**Thời lượng:** 1:30 giờ  
**Cấu trúc:** Lập trình cốt lõi (60 phút) → Bài tập mở rộng (30 phút)

---

## Phần 1 — Lập Trình Cốt Lõi (0:00–1:00)

Chạy các ví dụ trong Google Colab tại: https://colab.research.google.com/drive/172zCiXpLr1FEXMRCAbmZoqTrKiSkUERm?usp=sharing

Triển khai tất cả TODO trong `template.py`. Chạy `pytest tests/` để kiểm tra tiến độ.

**Điểm kiểm tra:** Sau khi hoàn thành 4 nhiệm vụ, chạy:
```bash
python template.py
```
Bạn sẽ thấy output so sánh phản hồi của GPT-4o và GPT-4o-mini.

---

## Phần 2 — Bài Tập Mở Rộng (1:00–1:30)

### Bài tập 2.1 — Độ Nhạy Của Temperature
Gọi `call_openai` với các giá trị temperature 0.0, 0.5, 1.0 và 1.5 sử dụng prompt **"Hãy kể cho tôi một sự thật thú vị về Việt Nam."**

**Bạn nhận thấy quy luật gì qua bốn phản hồi?** (2–3 câu)
> Ở temperature 0.0, phản hồi rất nhất quán và mang tính thực tế, ít sáng tạo. Khi tăng dần lên 0.5 và 1.0, câu trả lời trở nên đa dạng hơn về từ ngữ và cách diễn đạt. Ở temperature 1.5, phản hồi có xu hướng sáng tạo và đôi khi lan man hơn, có thể chứa thông tin ít chính xác hoặc cấu trúc câu kém chặt chẽ hơn.

**Bạn sẽ đặt temperature bao nhiêu cho chatbot hỗ trợ khách hàng, và tại sao?**
> Tôi sẽ đặt temperature khoảng 0.2–0.3 cho chatbot hỗ trợ khách hàng. Mức thấp này đảm bảo câu trả lời nhất quán, chính xác và đáng tin cậy — điều quan trọng nhất khi xử lý thông tin sản phẩm, chính sách hoặc hướng dẫn kỹ thuật. Sự sáng tạo không cần thiết ở đây và có thể gây nhầm lẫn cho khách hàng.

---

### Bài tập 2.2 — Đánh Đổi Chi Phí
Xem xét kịch bản: 10.000 người dùng hoạt động mỗi ngày, mỗi người thực hiện 3 lần gọi API, mỗi lần trung bình ~350 token.

**Ước tính xem GPT-4o đắt hơn GPT-4o-mini bao nhiêu lần cho workload này:**
> Workload: 10.000 người dùng × 3 lần gọi × 350 token = 10.500.000 token/ngày (giả sử input/output bằng nhau: ~175K input + ~175K output).
> - GPT-4o: (175 × $5.00 + 175 × $20.00) / 1.000 ≈ $4.375/ngày
> - GPT-4o-mini: (175 × $0.15 + 175 × $0.60) / 1.000 ≈ $0.131/ngày
>
> GPT-4o đắt hơn khoảng **33 lần** so với GPT-4o-mini cho workload này.

**Mô tả một trường hợp mà chi phí cao hơn của GPT-4o là xứng đáng, và một trường hợp GPT-4o-mini là lựa chọn tốt hơn:**
> GPT-4o xứng đáng khi xây dựng công cụ phân tích pháp lý hoặc y tế — nơi độ chính xác cao và khả năng suy luận phức tạp là bắt buộc, sai sót có thể gây hậu quả nghiêm trọng. Ngược lại, GPT-4o-mini phù hợp hơn cho chatbot FAQ đơn giản, phân loại nội dung, hoặc tóm tắt email thông thường — các tác vụ không đòi hỏi suy luận sâu và cần tối ưu chi phí ở quy mô lớn.

---

### Bài tập 2.3 — Trải Nghiệm Người Dùng với Streaming
**Streaming quan trọng nhất trong trường hợp nào, và khi nào thì non-streaming lại phù hợp hơn?** (1 đoạn văn)
> Streaming quan trọng nhất khi phản hồi dài và người dùng cần thấy kết quả ngay lập tức — ví dụ chatbot hội thoại, công cụ viết nội dung, hoặc giải thích code theo từng bước. Việc hiển thị token ngay khi được sinh ra tạo cảm giác tương tác tức thì, giảm perceived latency đáng kể dù tổng thời gian xử lý không đổi. Ngược lại, non-streaming phù hợp hơn khi output cần được xử lý hoàn chỉnh trước khi dùng — chẳng hạn phân tích sentiment, phân loại văn bản, gọi API hàng loạt (batch processing), hoặc khi kết quả phải được validate/parse toàn bộ trước khi hiển thị cho người dùng.


## Danh Sách Kiểm Tra Nộp Bài
- [ ] Tất cả tests pass: `pytest tests/ -v`
- [ ] `call_openai` đã triển khai và kiểm thử
- [ ] `call_openai_mini` đã triển khai và kiểm thử
- [ ] `compare_models` đã triển khai và kiểm thử
- [ ] `streaming_chatbot` đã triển khai và kiểm thử
- [ ] `retry_with_backoff` đã triển khai và kiểm thử
- [ ] `batch_compare` đã triển khai và kiểm thử
- [ ] `format_comparison_table` đã triển khai và kiểm thử
- [ ] `exercises.md` đã điền đầy đủ
- [ ] Sao chép bài làm vào folder `solution` và đặt tên theo quy định 
