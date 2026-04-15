[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=23573962&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** 26ai.khapd@vinuni.edu.vn
**Name:** Phạm Đan Kha

---

## Bài lab: Xây dựng ETL Pipeline

Mục tiêu của bài lab là xây dựng một quy trình trích xuất, biến đổi và nạp dữ liệu (ETL) hoàn chỉnh, sau đó thực hiện thí nghiệm để đánh giá hiệu quả của AI Agent.

---

### Các bước trong ETL Pipeline

* **Extract (Trích xuất):** Đọc dữ liệu đầu vào từ định dạng **JSON**.
* **Validate (Xác thực):** Kiểm tra và loại bỏ các dữ liệu không hợp lệ dựa trên các điều kiện:
    * Giá tiền (`price`) phải lớn hơn **0** (loại bỏ nếu $\text{price} \le 0$).
    * Danh mục (`category`) không được để trống.
* **Transform (Biến đổi):**
    * Tính toán giá sau khi giảm **10%**.
    * Chuẩn hóa định dạng danh mục sang dạng **Title Case** (Viết hoa chữ cái đầu).
    * Thêm mốc thời gian (**timestamp**) xử lý dữ liệu.
* **Load (Nạp):** Lưu kết quả cuối cùng ra tệp **CSV**.

---

### Thí nghiệm (Experiment)

Thực hiện so sánh hiệu suất và độ chính xác của **AI Agent** trong hai trường hợp:
1.  Sử dụng **dữ liệu sạch** (Dữ liệu đã qua xử lý ETL).
2.  Sử dụng **dữ liệu rác** (Dữ liệu thô chưa qua lọc và chuẩn hóa).

---

## Cach chay (How to Run)

### Prerequisites
```bash
pip install pandas
```

### Chay ETL Pipeline
```bash
python solution.py
```

### Chay Agent Simulation (Stress Test)
```bash
python agent_simulation.py
```

---

## Cau truc thu muc

```
├── solution.py              # ETL Pipeline script
├── processed_data.csv       # Output cua pipeline
├── experiment_report.md     # Bao cao thi nghiem
└── README.md                # File nay
```

---

## Ket qua

---

### Kết quả thí nghiệm (Experiment Results)

Dưới đây là bảng so sánh hiệu suất của AI Agent dựa trên chất lượng dữ liệu đầu vào:

| Trình trạng dữ liệu | Kết quả của AI Agent | Điểm số (Score) | Chi tiết phản hồi |
| :--- | :--- | :--- | :--- |
| **Dữ liệu sạch (Clean Data)** | Trả lời chính xác | **10/10** | Chọn đúng **Laptop** với giá **$1200**. |
| **Dữ liệu rác (Garbage Data)** | Trả lời sai | **1/10** | Chọn nhầm **Lò phản ứng hạt nhân (Nuclear Reactor)** với giá **$999,999**. |

### Các vấn đề phát hiện trong Dữ liệu rác

Việc AI Agent đưa ra kết quả sai lệch là do các lỗi phổ biến sau trong dữ liệu thô:
* **Trùng lặp ID (Duplicate IDs):** Gây nhiễu loạn định danh đối tượng.
* **Sai kiểu dữ liệu (Wrong data types):** Ví dụ giá tiền ghi bằng chữ là `"ten dollars"` thay vì số `10`, khiến hệ thống không thể tính toán.
* **Dữ liệu ngoại lai (Outliers):** Các giá trị quá lớn hoặc quá nhỏ bất thường (như giá lò phản ứng hạt nhân) làm sai lệch logic lựa chọn.
* **Giá trị trống (Null values):** Thiếu thông tin quan trọng khiến Agent phải "đoán" hoặc xử lý lỗi.



---

### Kết luận (Conclusion)

* **Nguyên lý cốt lõi:** Dữ liệu chất lượng kém dẫn đến kết quả sai lệch — hay còn gọi là nguyên lý **"Garbage in, garbage out"** (Rác đầu vào, rác đầu ra).
* **Vai trò của ETL:** Quy trình **ETL Pipeline** đóng vai trò quyết định trong việc làm sạch và chuẩn hóa dữ liệu, giúp AI Agent đưa ra các quyết định chính xác và đáng tin cậy hơn.

---
