# 🛡️ Phát Hiện Gian Lận Thẻ Tín Dụng Bằng XGBoost Trên Dữ Liệu Mất Cân Bằng

Đây là dự án Nghiên cứu khoa học tập trung giải quyết bài toán phân loại dữ liệu mất cân bằng (Class Imbalance) trong lĩnh vực tài chính. Mục tiêu của dự án là thiết lập bộ tham số tối ưu cho mô hình **XGBoost**, qua đó đề xuất giải pháp công nghệ giúp tối ưu hóa hệ thống quản trị rủi ro, giảm thiểu tổn thất do gian lận và bảo vệ trải nghiệm liền mạch của khách hàng.

## 🎯 Mục Tiêu Nghiên Cứu
1. **Tối ưu hóa mô hình:** Thiết lập và tinh chỉnh bộ siêu tham số tối ưu cho XGBoost trên tập dữ liệu mất cân bằng cực độ.
2. **So sánh đánh giá:** Chứng minh tính ưu việt của Gradient Boosting so với các mô hình cơ sở (Baseline Models) như Logistic Regression và Random Forest.
3. **Kiểm soát ngưỡng (Trade-off):** Cực đại hóa chỉ số **Recall** để bắt đúng tối đa giao dịch gian lận, đồng thời kiểm soát nghiêm ngặt tỷ lệ **False Positive** (tránh khóa nhầm thẻ của khách hàng).

## ⚙️ Phương Pháp & Kỹ Thuật Triển Khai
- **Ngôn ngữ & Thư viện:** Python (Jupyter Notebook), `xgboost`, `scikit-learn`, `imbalanced-learn`, `shap`, `pandas`, `seaborn`.
- **Tiền xử lý dữ liệu:** Chuẩn hóa các biến (Amount, Time) bằng `RobustScaler`/`StandardScaler`.
- **Xử lý mất cân bằng lớp:** Kết hợp kỹ thuật lấy mẫu `SMOTE` cho các mô hình truyền thống và tinh chỉnh trọng số `scale_pos_weight` cho XGBoost.
- **Tối ưu hóa siêu tham số:** Ứng dụng `GridSearchCV` và `RandomizedSearchCV` để dò tìm không gian tham số tối ưu.
- **Minh bạch mô hình (XAI):** Sử dụng `SHAP` values và Feature Importance để giải thích quyết định của mô hình.

## 📊 Đánh Giá & Kết Quả
Dự án đánh giá toàn diện hiệu năng của các mô hình thông qua:
- Ma trận nhầm lẫn (Confusion Matrix).
- Diện tích dưới đường cong: ROC-AUC, PR-AUC.
- Đánh giá tính ổn định qua Bootstrap và Kiểm định chéo phân tầng lặp lại (Repeated Stratified 5x2 CV).
- Phân tích hiện tượng học vẹt (Overfitting) qua Learning Curves.
- Điều chỉnh ngưỡng quyết định (Threshold Moving) theo mục tiêu kinh doanh (Ngân sách False Positive).

## 📂 Cấu Trúc Repository
- `PhanTich_GianLan.ipynb`: Mã nguồn E2E (End-to-End) hoàn chỉnh nhất. Từ bước phân tích khám phá (EDA) đến huấn luyện, đánh giá, kiểm định chéo và giải thích mô hình bằng SHAP. Phù hợp làm báo cáo khoa học trình Hội đồng.
- `requirements.txt`: Danh sách môi trường và các thư viện phụ thuộc.
- `xgb_fraud_final.json` và `fraud_preprocessing.joblib`: Mô hình XGBoost tối ưu cuối cùng và pipeline tiền xử lý (scaler, ngưỡng, v.v.) đã được đóng gói.
- Các file `bang*.csv` và `fig_*.png`: Các bảng biểu và đồ thị xuất ra từ quá trình huấn luyện phục vụ viết báo cáo khoa học.

## 🚀 Hướng Dẫn Sử Dụng
1. Clone repository này về máy.
2. Tải tập dữ liệu thô `creditcard.csv` từ [Kaggle](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud) và đặt vào cùng thư mục với notebook. (File này đã được thiết lập bỏ qua trong `.gitignore`).
3. Cài đặt các thư viện cần thiết:
   ```bash
   pip install -r requirements.txt
   ```
4. Mở và chạy toàn bộ các cell trong file `PhanTich_GianLan.ipynb`.