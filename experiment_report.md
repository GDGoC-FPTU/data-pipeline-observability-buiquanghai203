# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** 2A202600006
**Name:** Bui Quang Hai
**Date:** 15/04/2026

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | Agent: Based on my data, the best choice is Laptop at $1200. | 10 | Pipeline đã loại bỏ thành công các lỗi (Price <= 0, Missing Category), giúp Agent đưa ra quyết định logic.|
| Garbage Data (`garbage_data.csv`) | Agent: Based on my data, the best choice is Nuclear Reactor at $999999.| 1 |Agent bị nhiễu hoàn toàn bởi bản ghi "Poisoned", đưa ra đề xuất phi thực tế. |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

Agent đưa ra câu trả lời sai lầm với dữ liệu rác vì bản chất của các hệ thống AI Agents phụ thuộc hoàn toàn vào luồng hạ tầng dữ liệu (data pipeline) cung cấp cho nó. Khi dữ liệu đầu vào không được kiểm soát chặt chẽ, các vấn đề cốt lõi sau sẽ phá vỡ logic nội tại của hệ thống:

Outliers (Giá trị ngoại lai): Sự xuất hiện của "Nuclear Reactor" với giá cực đoan ($999999) làm sai lệch hoàn toàn trọng số phân tích của Agent. Thuật toán tối ưu hóa bị lừa để chọn giá trị "to nhất" hoặc "nổi bật nhất" thay vì giá trị phù hợp nhất.

Null Values & Wrong Data Types (Thiếu dữ liệu & Sai kiểu dữ liệu): Như log pipeline đã chỉ ra, dữ liệu thô ban đầu có chứa Price <= 0 và Missing Category. Khi thiếu các trường phân loại chuẩn hoặc sai định dạng số học, Agent không thể so sánh các mặt hàng cùng hệ quy chiếu, dẫn đến các phép tính vector hoặc query bị lỗi.

Duplicate IDs (Dữ liệu trùng lặp): Việc lặp lại các bản ghi khiến Agent đánh giá sai tần suất hoặc độ quan trọng của một đối tượng.

Thực tế này cho thấy việc thiết kế một kiến trúc backend vững chắc để làm sạch dữ liệu là nền tảng sống còn. Thay vì chỉ viết code chạy bề nổi, việc nắm rõ cơ chế xử lý thông tin từ nền tảng sẽ giúp hệ thống Agent hoạt động thực sự hiệu quả và không bị thao túng bởi dữ liệu rác.

---

## 3. Ket luan

**Quality Data > Quality Prompt?** Hoàn toàn đồng ý.

Dù bạn có xây dựng một cấu trúc prompt tinh vi hay một lớp giao diện xuất sắc đến đâu, hệ thống AI vẫn sẽ sụp đổ nếu hạ tầng dữ liệu đầu vào yếu kém ("Garbage In, Garbage Out"). Việc ưu tiên xây dựng data pipeline sạch và chuẩn hóa kiến trúc dữ liệu là điều kiện tiên quyết để Agent có thể thực hiện những suy luận logic và chính xác. Dữ liệu chất lượng chính là nền móng, còn prompt chỉ là công cụ định hướng.
