# 🛡️ Credit Card Fraud Detection

Đây là dự án Nghiên cứu khoa học nhóm nhằm ứng dụng Machine Learning để phát hiện các giao dịch gian lận thẻ tín dụng. Bài toán tập trung giải quyết thách thức lớn nhất trong lĩnh vực tài chính: **Dữ liệu mất cân bằng cực độ (Highly Imbalanced Data)**.

## ⚙️ Công nghệ & Kỹ thuật cốt lõi
- **Ngôn ngữ:** Python (Jupyter Notebook)
- **Thư viện chính:** `scikit-learn`, `xgboost`, `imbalanced-learn`, `pandas`, `seaborn`
- **Pipeline triển khai:**
  - **Tiền xử lý:** Chuẩn hóa các đặc trưng với `RobustScaler`.
  - **Xử lý mất cân bằng:** Áp dụng kỹ thuật sinh dữ liệu tổng hợp **SMOTE** (Synthetic Minority Over-sampling Technique) để nội suy và cân bằng nhãn.
  - **Tối ưu hóa GPU:** Tích hợp huấn luyện phần cứng (CUDA) cho thuật toán `hist` của XGBoost.
  - **Hyperparameter Tuning:** Sử dụng `GridSearchCV` để dò tìm không gian tham số tối ưu dựa trên tiêu chí `average_precision` (phù hợp cho bài toán lệch pha).

## 📊 Đánh giá Mô hình
Dự án đã tiến hành thử nghiệm và đối chiếu chéo hiệu suất của 3 mô hình học máy:
1. **Logistic Regression:** Đóng vai trò là mô hình cơ sở (Baseline).
2. **Random Forest:** Cải thiện đáng kể khả năng phân loại.
3. **Tuned XGBoost (Mô hình chọn lọc):** Qua 36 vòng huấn luyện tinh chỉnh (`learning_rate`, `max_depth`, `n_estimators`), mô hình XGBoost đạt hiệu suất tối ưu với **F1-Score lớp gian lận: 0.84** và **Accuracy: 100%**.

## 📂 Cấu trúc Repository
- `PhanTich_GianLan.ipynb`: Mã nguồn E2E từ bước khám phá dữ liệu (EDA), SMOTE đến huấn luyện và đánh giá.
- `requirements.txt`: Danh sách môi trường và thư viện phụ thuộc.
*(Lưu ý: Tập dữ liệu `creditcard.csv` được bỏ qua bằng `.gitignore` để đảm bảo chính sách bảo mật dữ liệu thô).*