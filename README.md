# Shopping Cart Analysis

Phân tích dữ liệu bán lẻ nhằm khám phá mối quan hệ giữa các sản phẩm thường được mua cùng nhau bằng các kỹ thuật **Association Rule Mining** như **Apriori** và **FP-Growth**.  
Project triển khai pipeline đầy đủ từ xử lý dữ liệu → khai thác luật → so sánh thuật toán → trực quan hóa kết quả.

---

## Features

- Làm sạch dữ liệu & xử lý giao dịch lỗi
- Xây dựng basket matrix (transaction × product)
- Khai thác tập mục phổ biến (Frequent Itemsets)
- Sinh luật kết hợp (Association Rules)
- Hỗ trợ 2 thuật toán:
  - Apriori
  - FP-Growth
- So sánh Apriori vs FP-Growth
- Các chỉ số đánh giá:
  - Support
  - Confidence
  - Lift
- Trực quan hóa với:
  - Bar chart
  - Scatter plot
  - Network graph
  - Biểu đồ tương tác Plotly
- Tự động hóa pipeline bằng **Papermill**
- Dashboard tương tác bằng **Streamlit**

---

## Project Structure

```text
shopping_cart_advanced_analysis/
├── data/
│   ├── raw/
│   │   └── online_retail.csv
│   └── processed/
│       ├── cleaned_uk_data.csv
│       ├── basket_bool.parquet
│       ├── rules_apriori_filtered.csv
│       └── rules_fpgrowth_filtered.csv
│
├── notebooks/
│   ├── preprocessing_and_eda.ipynb
│   ├── basket_preparation.ipynb
│   ├── apriori_modelling.ipynb
│   ├── fp_growth_modelling.ipynb
│   ├── compare_apriori_fpgrowth.ipynb
│   └── runs/
│       ├── preprocessing_and_eda_run.ipynb
│       ├── basket_preparation_run.ipynb
│       ├── apriori_modelling_run.ipynb
│       ├── fp_growth_modelling_run.ipynb
│       └── compare_apriori_fpgrowth_run.ipynb
│
├── src/
│   └── apriori_library.py
│
├── dashboard/
│   ├── app.py
│   └── requirements.txt
│
├── run_papermill.py
├── requirements.txt
└── README.md
```

---

## Installation

```bash
git clone <your_repo_url>
cd shopping_cart_advanced_analysis
conda create -n shopping_env python=3.11
conda activate shopping_env
pip install -r requirements.txt
```

Data Preparation
Đặt file gốc tại:

```bash
data/raw/online_retail.csv
```
File output sẽ được sinh tự động vào:

```bash
data/processed/
```

Run Pipeline (Recommended)
Chạy toàn bộ phân tích chỉ với 1 lệnh:

```bash
python run_papermill.py
```
Kết quả sinh ra:

```bash
data/processed/
├── cleaned_uk_data.csv
├── basket_bool.parquet
├── rules_apriori_filtered.csv
└── rules_fpgrowth_filtered.csv

notebooks/runs/
├── preprocessing_and_eda_run.ipynb
├── basket_preparation_run.ipynb
├── apriori_modelling_run.ipynb
├── fp_growth_modelling_run.ipynb
└── compare_apriori_fpgrowth_run.ipynb
```

### Changing Parameters
Các tham số có thể chỉnh trong `run_papermill.py` hoặc trong cell `PARAMETERS` của mỗi notebook:

```python
MIN_SUPPORT=0.01
MAX_LEN=3
FILTER_MIN_CONF=0.3
FILTER_MIN_LIFT=1.2
```
Papermill cho phép chạy pipeline với cấu hình khác nhau mà không cần sửa notebook gốc.

### Visualization & Results
Các notebook modelling hiển thị các biểu đồ:

Top luật theo Lift

Top luật theo Confidence

Scatter Support – Confidence – Lift

Network graph giữa các sản phẩm

Biểu đồ Plotly tương tác

Có thể export notebook kết quả sang HTML:

```bash
jupyter nbconvert notebooks/runs/priori_modelling_run.ipynb --to html
```

### Ứng dụng thực tế
Product recommendation

Cross-selling strategy

Combo gợi ý sản phẩm

Phân tích hành vi mua hàng

Sắp xếp sản phẩm tại siêu thị

### Tech Stack

| Công nghệ | Mục đích |
|----------|----------|
| Python | Ngôn ngữ chính |
| Pandas | Xử lý dữ liệu transaction |
| MLxtend | Apriori / FP-Growth association rules |
| Papermill | Chạy pipeline notebook tự động |
| Matplotlib & Seaborn | Visualization biểu đồ tĩnh |
| Plotly | Dashboard / biểu đồ tương tác |
| Jupyter Notebook | Môi trường notebook |

### Roadmap
Streamlit dashboard

Weighted association rules

Correlation-aware rule ranking


### Author
Project được thực hiện bởi:
Trang Le

📄 License
MIT — sử dụng tự do cho nghiên cứu, học thuật và ứng dụng nội bộ.
## Lab Objective

Mục tiêu của Lab 2 là áp dụng các kỹ thuật **Association Rule Mining**
để phân tích hành vi mua sắm của khách hàng từ dữ liệu bán lẻ.

Cụ thể:
- Tiền xử lý dữ liệu giao dịch thực tế
- Xây dựng basket matrix (transaction × product)
- Khai phá tập mục phổ biến bằng Apriori và FP-Growth
- Sinh và đánh giá luật kết hợp dựa trên các chỉ số:
  - Support
  - Confidence
  - Lift
- Phân tích ý nghĩa thực tiễn của các luật trong bối cảnh kinh doanh

## Dataset Description

Dữ liệu sử dụng là **Online Retail Dataset**, bao gồm các giao dịch bán lẻ
tại Vương quốc Anh.

Các trường chính:
- InvoiceNo: Mã hóa đơn
- StockCode: Mã sản phẩm
- Description: Tên sản phẩm
- Quantity: Số lượng
- UnitPrice: Giá đơn vị
- InvoiceDate: Thời gian mua
- CustomerID: Mã khách hàng
- Country: Quốc gia

Dữ liệu đã được làm sạch bằng cách:
- Loại bỏ hóa đơn hủy
- Loại bỏ giao dịch có số lượng âm
- Chỉ giữ giao dịch tại UK

## Methodology

Quy trình thực hiện gồm các bước sau:

1. Data Preprocessing
   - Làm sạch dữ liệu
   - Chuẩn hóa tên sản phẩm
   - Lọc giao dịch không hợp lệ

2. Basket Construction
   - Gom nhóm sản phẩm theo InvoiceNo
   - Chuyển sang dạng basket boolean matrix

3. Frequent Itemset Mining
   - Áp dụng Apriori và FP-Growth
   - Lọc theo min_support và max_len

4. Association Rule Generation
   - Sinh luật kết hợp
   - Đánh giá bằng support, confidence, lift

5. Visualization & Analysis
   - Biểu đồ top luật
   - Scatter plot
   - Network graph

## Evaluation Metrics

Các luật kết hợp được đánh giá dựa trên:

- Support: Tần suất xuất hiện của tập sản phẩm
- Confidence: Xác suất mua sản phẩm B khi đã mua A
- Lift:
  - Lift > 1: Mối quan hệ tích cực
  - Lift = 1: Độc lập
  - Lift < 1: Quan hệ tiêu cực

Lift là chỉ số quan trọng để đánh giá giá trị thực tế của luật.

## Results & Analysis

Kết quả cho thấy:

- Một số sản phẩm đóng vai trò **Product Hub**, xuất hiện trong nhiều luật
- Các luật có Lift cao thường liên quan đến sản phẩm quà tặng và đồ trang trí
- FP-Growth cho tốc độ nhanh hơn Apriori trên tập dữ liệu lớn
- Apriori dễ giải thích hơn và phù hợp cho mục đích học tập

## Business Implications

Các luật kết hợp có thể được ứng dụng vào:
- Gợi ý sản phẩm mua kèm (cross-selling)
- Thiết kế combo sản phẩm
- Tối ưu trưng bày sản phẩm
- Cá nhân hóa đề xuất cho khách hàng

Các luật có lift cao và support ổn định phù hợp cho đại đa số khách hàng,
trong khi các luật có support thấp nhưng giá trị cao phù hợp cho phân khúc cao cấp.

## Conclusion

Lab 2 đã minh họa hiệu quả việc sử dụng Association Rule Mining
trong phân tích hành vi mua sắm.

Kết quả cho thấy:
- Apriori và FP-Growth đều khai phá được các mối quan hệ có ý nghĩa
- FP-Growth hiệu quả hơn về hiệu năng
- Các luật kết hợp mang lại giá trị thực tiễn rõ ràng cho kinh doanh

