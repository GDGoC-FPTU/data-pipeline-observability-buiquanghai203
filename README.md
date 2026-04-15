[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=23574030&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** 26ai.haibq@vinuni.edu.vn
**Name:** Bùi Quang Hải

---

## Mo ta

Bài lab này tập trung vào việc xây dựng một luồng xử lý dữ liệu (ETL Pipeline) cơ bản để trích xuất, làm sạch và lưu trữ dữ liệu. Đồng thời, lab thực hiện một thí nghiệm (Stress Test) nhằm minh họa khái niệm Data Observability, chứng minh tầm quan trọng cốt lõi của chất lượng dữ liệu (Data Quality) đối với tính chính xác và logic trong quá trình ra quyết định của các hệ thống AI Agent.

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
Dau tien, can chay script de tao ra file du lieu rac (`garbage_data.csv`) chua cac ban ghi bi co tinh lam nhieu (Poisoned records)
Sau do, chay script mo phong Agent. Script nay se tu dong load ca 2 tap du lieu: Clean Data (tu processed_data.csv duoc tao ra boi pipeline) va Garbage Data, sau do in ra ket qua so sanh quyet dinh cua Agent:
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

* **ETL Pipeline (Xử lý dữ liệu):**
  * **Tổng số bản ghi đã xử lý:** 5
  * **Số bản ghi giữ lại (Kept):** 3 (đã được lưu thành công vào `processed_data.csv`).
  * **Số bản ghi bị loại (Dropped):** 2.
  * **Chi tiết lỗi:** * Bản ghi ID 3 bị loại do lỗi `Price <= 0`.
    * Bản ghi ID 4 bị loại do lỗi `Missing Category`.

* **Agent Simulation (Kiểm thử AI Agent):**
  * **Với Clean Data:** Agent hoạt động chính xác, đưa ra lựa chọn hợp lý (Laptop at $1200).
  * **Với Garbage Data:** Agent bị đánh lừa bởi dữ liệu ngoại lai "đầu độc", đưa ra quyết định phi thực tế (Nuclear Reactor at $999999).
