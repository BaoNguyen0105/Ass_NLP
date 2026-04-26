# Trích xuất thông tin và Phân tích ngữ nghĩa Hợp đồng Pháp lý
*(Information Extraction and Semantic Analysis of Legal Contracts)*

📌 **Đồ án môn học:** Xử lý Ngôn ngữ Tự nhiên (Natural Language Processing) - HCMUT  
👥 **Nhóm:** NLP ASSIGNMENT

---

## 📖 Giới thiệu dự án
Dự án này tập trung vào việc áp dụng các kỹ thuật Xử lý ngôn ngữ tự nhiên (NLP) để tự động hóa việc đọc hiểu, bóc tách và phân tích các văn bản hợp đồng pháp lý tiếng Việt. Thay vì rà soát thủ công, hệ thống sử dụng các mô hình học máy và học sâu (đặc biệt là **PhoBERT**) để chuyển đổi văn bản hợp đồng phi cấu trúc thành dữ liệu có cấu trúc.

### 🎯 Các chức năng chính (Tasks)

**Phần 1: Tiền xử lý và Phân tích cú pháp**
* **1.1 Tách mệnh đề (Clause Splitting):** Xử lý các câu phức tạp thành các mệnh đề độc lập bằng Dependency Parsing.
* **1.2 Phân cụm danh từ (Noun Phrase Chunking):** Trích xuất các thực thể cơ bản dựa trên tập luật POS Tagging.
* **1.3 Trích xuất Quan hệ phụ thuộc (Dependency Relation):** Xác định cấu trúc Chủ - Vị - Tân ngữ/Bổ ngữ (Subject-Verb-Object).

**Phần 2: Trích xuất thông tin nâng cao**
* **2.1 Nhận dạng Thực thể (NER):** Tinh chỉnh (Fine-tune) mô hình `vinai/phobert-base-v2` để nhận diện các bên ký kết, số tiền, ngày tháng,...
* **2.2 Phân loại Ý định (Intent Classification):** Đối chiếu hiệu năng giữa mô hình Baseline (TF-IDF + Logistic Regression) và PhoBERT trong việc phân loại mục đích của từng điều khoản (Bảo mật, Thanh toán, Phạt vi phạm,...).
* **2.3 Trích xuất thông tin có cấu trúc:** Tổng hợp dữ liệu NER và Dependency Parsing thành định dạng JSON dễ dàng truy vấn.

---

## ⚙️ Cài đặt Môi trường (Setup)

Dự án sử dụng Python và yêu cầu **Java** để chạy công cụ VnCoreNLP.

**1. Clone repository:**
```bash
git clone https://github.com/BaoNguyen0105/Ass_NLP.git
cd NLP-Assignment
```

**2. Cài đặt thư viện Python:**
Đảm bảo bạn đang sử dụng môi trường ảo (virtual environment), sau đó chạy:

```bash
pip install -r requirements.txt
```

**3. Cài đặt Java (Bắt buộc cho VnCoreNLP):**

Tải và cài đặt Java JDK 11+.

Đảm bảo biến môi trường JAVA_HOME đã được cấu hình đúng trên máy của bạn.

## 📂 Cấu trúc Repository
```
📦 NLP-Assignment
 ┣ 📂 inputs/                  # Dữ liệu hợp đồng thô đầu vào (raw_contracts.txt)
 ┣ 📂 output/                  # Kết quả xuất ra từ các script (txt, json, csv)
 ┣ 📂 report/                  # Mã nguồn LaTeX và file PDF báo cáo môn học
 ┣ 📜 1.1.ipynb                # Tác vụ tách mệnh đề
 ┣ 📜 1.2.ipynb                # Tác vụ phân cụm danh từ
 ┣ 📜 1.3.ipynb                # Tác vụ trích xuất quan hệ phụ thuộc
 ┣ 📜 2.1.ipynb                # Huấn luyện mô hình NER (PhoBERT)
 ┣ 📜 2.2.ipynb                # Phân loại ý định điều khoản
 ┣ 📜 2.3.ipynb                # Tổng hợp thông tin có cấu trúc
 ┣ 📜 dataset-update.csv       # Dataset huấn luyện mô hình
 ┣ 📜 requirements.txt         # Danh sách thư viện phụ thuộc
 ┗ 📜 README.md                # File hướng dẫn dự án
```

## 🚀 Hướng dẫn sử dụng
Các chức năng được tách thành các file Jupyter Notebook độc lập để dễ dàng đánh giá và debug. Khởi chạy Jupyter và chạy lần lượt từ 1.1.ipynb đến 2.3.ipynb. Kết quả của bước trước sẽ được lưu vào thư mục output/ để làm đầu vào cho bước sau.