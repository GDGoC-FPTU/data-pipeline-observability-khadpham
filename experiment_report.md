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

## 2. Phân tích & nhận xét
### Tại sao Agent trả lời sai khi dùng Garbage Data?
Agent trả lời sai khi dùng Garbage Data vì dữ liệu rác không được xử lý và làm cho Agent không thể đưa ra được kết quả chính xác nhất.
Phân tích các vấn đề trong `garbage_data.csv`:
- **Duplicate IDs**: 
  - ID=1 xuất hiện 2 lần (Laptop và Banana) → Agent không biết nên tin record nào
- **Wrong data types**: 
  - Giá "ten dollars" (string) thay vì số → Agent không thể tính toán so sánh
- **Outliers**: 
  - Nuclear Reactor giá $999,999 → Agent chọn max price = outlier không hợp lý
- **Null values**: 
  - Ghost Item không có id, giá=0, category rỗng → thiếu thông tin bắt buộc
---
## 3. Kết luận
### Quality Data > Quality Prompt?

Đồng ý - Dù prompt có tốt đến đâu, nếu dữ liệu đầu vào là rác (garbage in) thì kết quả đầu ra cũng sẽ là rác (garbage out). 
Dữ liệu chất lượng kém sẽ:
- Làm Agent hiểu sai ngữ cảnh
- Gây lỗi xử lý (wrong data types)
- Đưa ra kết luận sai lệch (outliers)
- Không thể tin tưởng được
ETL Pipeline giúp làm sạch dữ liệu → Agent đưa ra quyết định chính xác hơn.