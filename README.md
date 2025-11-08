# 🛒 Walmart Data Pipeline

Dự án **Python** giúp tự động thu thập, lưu trữ, phân tích và trực quan hóa dữ liệu sản phẩm từ **Walmart** thông qua **SerpAPI**.  
Bạn có thể chạy toàn bộ pipeline chỉ với **một lệnh duy nhất**, hoặc mở trực tiếp bằng **VS Code Dev Container**.

---

## 📂 Cấu trúc thư mục

WalmartAPI/
│
├── src/
│ ├── call_API.py # Bước 1 - Gọi API lấy dữ liệu thô
│ ├── save_data.py # Bước 2 - Lưu dữ liệu ra CSV, JSON, Excel
│ ├── analyze_data.py # Bước 3 - Phân tích thống kê cơ bản
│ ├── clean_data.py # Bước 4 - Làm sạch dữ liệu
│ ├── eda_api.py # Bước 5 - Phân tích EDA và vẽ biểu đồ
│
├── data/
│ ├── raw_data/ # Dữ liệu gốc từ API
│ ├── save_data/ # Dữ liệu lưu lần đầu
│ ├── clean_data/ # Dữ liệu đã làm sạch
│ └── eda_pic/ # Hình ảnh và bảng phân tích EDA
│
├── pipeline.py # Chạy toàn bộ 5 bước pipeline
├── requirements.txt # Danh sách thư viện cần cài
├── Dockerfile # Định nghĩa image Docker
├── .dockerignore # Bỏ qua file/thư mục khi build image
├── .env # File chứa API_KEY (bảo mật, không push)
├── .env.example # Mẫu file .env cho người khác sử dụng
└── .devcontainer/
└── devcontainer.json # Cấu hình cho VS Code Dev Container


---

## ⚙️ Cài đặt môi trường

### 1️⃣ Tạo file `.env`

Tạo file `.env` trong thư mục gốc (hoặc copy từ mẫu):

```bash
cp .env.example .env
```
Rồi thêm API key của bạn:

API_KEY=your_serpapi_key_here

2️⃣ Cài thư viện (nếu chạy local, không dùng Docker)
```bash
pip install -r requirements.txt
```
🚀 Chạy pipeline (local)

Chỉ cần một lệnh duy nhất:

```bash
python pipeline.py
```
Pipeline sẽ tự động chạy lần lượt:

call_API.py → Gọi API và lưu raw data

save_data.py → Lưu dữ liệu thô ra file

analyze_data.py → Phân tích thống kê cơ bản

clean_data.py → Làm sạch dữ liệu

eda_api.py → Vẽ biểu đồ và lưu kết quả

Toàn bộ kết quả sẽ nằm trong thư mục data/.

🐳 Chạy bằng Docker (Cách 1 — Thủ công)
1️⃣ Build image
```bash
docker build -t walmart-pipeline .
```
2️⃣ Chạy container

Trên Linux/macOS:
```bash
docker run --env-file .env -v ${PWD}/data:/app/data walmart-pipeline
```
Trên Windows PowerShell:
```bash
docker run --env-file .env -v "%cd%/data:/app/data" walmart-pipeline
```

💻 Chạy bằng VS Code Dev Container (Cách 2 — Khuyến nghị)

Cách này đơn giản nhất cho nhóm học tập hoặc teamwork.

Chuẩn bị

Cài các extension:

🐳 Docker

🧱 Dev Containers

Clone project:
git clone https://github.com/<your-username>/WalmartAPI.git
cd WalmartAPI
cp .env.example .env


## 💻 Mở project bằng VS Code

---

### ⚙️ Thực hiện

Khi được hỏi → chọn **<span style="color:#00bfff">“Reopen in Container”</span>**

VS Code sẽ tự động:

- 🐳 **Build Docker image** từ <span style="color:#00bfff">Dockerfile</span>  
- 📦 **Cài đặt toàn bộ thư viện**  
- 📁 **Mount thư mục** <span style="color:green">data/</span>  
- 🔑 **Load file** <span style="color:#00bfff">.env</span> *(để có API_KEY)*  

---

Sau khi container mở xong, vào **Terminal trong VS Code** và chạy:

```bash
python pipeline.py
```

📊 Kết quả đầu ra

Thư mục	Nội dung
data/raw_data	Dữ liệu gốc (raw JSON) từ API
data/save_data	Dữ liệu lưu định dạng CSV, JSON, Excel
data/clean_data	Dữ liệu đã làm sạch
data/eda_pic	Hình ảnh và bảng phân tích EDA

🧩 Công nghệ sử dụng

Python 3.10+

SerpAPI

Pandas, Matplotlib, Seaborn

Docker, VS Code Dev Container

🧑‍💻 Tác giả

Ho Minh Nhien 

📬 Liên hệ: hominhnhien1805@example.com