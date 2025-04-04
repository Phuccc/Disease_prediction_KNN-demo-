# Dự án: Phân tích và Dự đoán Khối u Vú bằng Học máy

## Tổng quan
Dự án này tập trung vào việc phân tích dữ liệu y khoa và xây dựng mô hình học máy để dự đoán tính chất của khối u vú (lành tính hoặc ác tính) dựa trên tập dữ liệu `Data_Practice.xlsx`. Tập dữ liệu bao gồm thông tin của 961 bệnh nhân với 6 thuộc tính chính: PatientID, Age, Shape, Margin, Density và Target. Mục tiêu là hỗ trợ chẩn đoán y khoa thông qua phân tích dữ liệu và dự đoán chính xác.

- **Ngôn ngữ lập trình**: Python
- **Thư viện sử dụng**: Pandas, NumPy, Matplotlib, Seaborn, Scikit-learn

## Mục tiêu
- Xây dựng mô hình học máy để phân loại khối u vú là lành tính (0) hoặc ác tính (1).
- Phân tích khám phá dữ liệu (EDA) để hiểu rõ hơn về đặc điểm của khối u và mối quan hệ với tính chất lành/ác tính.

## Tập dữ liệu
Tập dữ liệu `Data_Practice.xlsx` chứa 961 bản ghi với các thuộc tính sau:
1. **PatientID**: Mã số bệnh nhân (chuỗi ký tự).
2. **Age**: Tuổi của bệnh nhân (số thực).
3. **Shape**: Hình dạng khối u (Round, Oval, Lobular, Irregular).
4. **Margin**: Đường biên khối u (Circumscribed, Microlobulated, Obscured, Ill-defined, Spiculated).
5. **Density**: Mật độ khối u (High, Iso, Low, Fat-containing).
6. **Target**: Tính chất khối u (0 - lành tính, 1 - ác tính).

### Đặc điểm dữ liệu
- Có giá trị thiếu (NaN) trong các cột Age, Shape, Margin, Density.
- Giá trị bất thường (ví dụ: Age = 870) đã được xử lý.

## Quy trình thực hiện
### 1. Tiền xử lý dữ liệu
- Đọc dữ liệu từ file Excel bằng `Pandas`.
- Xử lý giá trị bất thường: Sửa Age = 870 thành 87.
- Xử lý giá trị thiếu bằng cách mã hóa hoặc loại bỏ.

### 2. Phân tích dữ liệu khám phá (EDA)
- Trực quan hóa dữ liệu bằng `Matplotlib` và `Seaborn`:
  - Thống kê liệu tuổi hành khách u lành|ác tính theo tuổi.
    <br>![image](https://github.com/user-attachments/assets/6add39f2-f1f7-4be5-aeca-026951ddbc64)</br>
  - Tần suất các giá trị của Shape, Margin, Density.
    <p align="center">
      <img src="https://github.com/user-attachments/assets/ec2c1c3c-dd6f-450e-8bb1-815ac8729ee8" width="250" >
      <img src="https://github.com/user-attachments/assets/807280ac-4bfb-41a3-a507-a2efd9f59f0d" width="300" >
      <img src="https://github.com/user-attachments/assets/3782735e-a8b0-4efc-8ff4-019c5981004d" width="280" >
    </p>
  - Kiểm tra các giá trị Shape, Margin, Density rồi đối chiếu với Target
- Xử lý các dữ liệu missing của từng giá trị
- Rời rạc hoá dữ liệu giúp cải thiện hiệu suất, giảm nhiễu, tránh quá khớp và làm cho mô hình dễ giải thích hơn.
### 3. Xây dựng mô hình học máy
- Kiểm tra cân bằng dữ liệu giúp cải thiện độ chính xác và khả năng tổng quát của mô hình, đồng thời tránh hiện tượng thiên lệch hoặc overfitting.
  <br>![image](https://github.com/user-attachments/assets/c1bbf57d-bb67-4b08-8379-4334337adf28)</br>
- Chia dữ liệu: 80% tập huấn luyện, 20% tập kiểm tra.
- Sử dụng thuật toán K-Nearest Neighbors (KNN) với tham số tối ưu:
  - `k=18`
  - `weights='distance'`
  - `p=1` (Manhattan distance)
  - `algorithm='brute'`
- Huấn luyện mô hình bằng `Scikit-learn`.

### 4. Đánh giá mô hình
<br>![image](https://github.com/user-attachments/assets/768388cf-8431-434c-ac74-56f38c6b76bf)</br>
- **Độ chính xác**:
  - Tập huấn luyện: 100%.
  - Tập kiểm tra: 100% (241/241 mẫu đúng).
- **Ma trận nhầm lẫn**:
  - 127 mẫu lành tính (0) dự đoán đúng.
  - 114 mẫu ác tính (1) dự đoán đúng.
- Không có dự đoán sai, cho thấy hiệu suất vượt trội trên tập dữ liệu này.

## Kết quả
- Mô hình KNN đạt độ chính xác 100%, phù hợp để dự đoán tính chất khối u vú trên tập dữ liệu hiện tại.
- Các biểu đồ trực quan hóa cung cấp thông tin chi tiết về đặc điểm khối u, hỗ trợ bác sĩ trong chẩn đoán.
- Dữ liệu được làm sạch và xử lý hiệu quả, đảm bảo chất lượng đầu vào.

## Cài đặt và sử dụng
### Yêu cầu
- Python 3.x
- Thư viện:
  ```bash
  pip install pandas numpy matplotlib seaborn scikit-learn openpyxl
