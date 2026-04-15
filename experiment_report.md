# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** AI20K-253
**Name:** Phạm Đan Kha 
**Date:** 15/04/2026

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | Based on my data, the best choice is Laptop at $1200. |10 |Sau khi đã dọn sạch sẽ dữ liệu, Agent đã đưa ra được kết quả chính xác nhất |
| Garbage Data (`garbage_data.csv`) | Based on my data, the best choice is Nuclear Reactor at $999999. |1 | Vì là dữ liệu rác nên Agent đã đưa ra được kết quả không chính xác nhất |

---

## 2. Phan tich & nhan xet
### Tại sao Agent trả lời sai khi dùng Garbage Data?

---

Agent trả lời sai khi dùng Garbage Data vì dữ liệu rác không được xử lý và làm cho Agent không thể đưa ra được kết quả chính xác nhất. Phân tích các vấn đề trong `garbage_data.csv`:

* **Duplicate IDs**: ID=1 xuất hiện 2 lần (Laptop và Banana) → Agent không biết nên tin record nào, dẫn đến sự mâu thuẫn trong quá trình truy xuất thông tin.
* **Wrong data types**: Giá "ten dollars" (string) thay vì số → Agent không thể thực hiện các phép tính toán so sánh hoặc tổng hợp dữ liệu số học.
* **Outliers**: Nuclear Reactor giá $999,999 → Agent chọn max price trúng ngay giá trị ngoại lai không hợp lý, làm sai lệch hoàn toàn mục tiêu tìm kiếm ban đầu.
* **Null values**: Ghost Item không có id, giá=0, category rỗng → thiếu thông tin bắt buộc khiến Agent bị "ảo giác" hoặc bỏ sót dữ liệu quan trọng.

**Kết luận:** Những lỗ hổng này khiến hệ thống mất đi tính nhất quán, buộc chúng ta phải sử dụng ETL để chuẩn hóa dữ liệu đầu vào.

---
## 3. Ket luan
### Quality Data > Quality Prompt?

Đồng ý – Dù prompt có tốt đến đâu, nếu dữ liệu đầu vào là "rác" (**Garbage In**) thì đầu ra chắc chắn là "rác" (**Garbage Out**). Dữ liệu kém chất lượng gây ra các hệ lụy:

* **Hiểu sai ngữ cảnh:** Agent bị nhiễu thông tin, dẫn đến phản hồi lạc đề.
* **Lỗi hệ thống:** Sai kiểu dữ liệu (**Wrong Data Types**) gây gián đoạn logic xử lý.
* **Kết luận sai lệch:** Các giá trị ngoại lai (**Outliers**) khiến Agent đưa ra quyết định thiếu chính xác.
* **Mất lòng tin:** Kết quả không ổn định làm giảm giá trị ứng dụng thực tế.

**Kết luận:** ETL Pipeline là bộ lọc quan trọng giúp làm sạch dữ liệu, đảm bảo Agent đưa ra quyết định chuẩn xác và đáng tin cậy.