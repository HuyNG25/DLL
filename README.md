# Dự Án Khai Phá Dữ Liệu Chẩn Đoán Bệnh Tim (Heart Disease Data Mining)
# Giới thiệu chung
  Dự án này tập trung vào việc áp dụng các kỹ thuật khai phá dữ liệu (Data Mining) trên bộ dữ liệu tim mạch nhằm tìm ra các nhóm bệnh nhân có đặc điểm tương đồng và các luật kết hợp giữa các triệu chứng lâm sàng.
  # Mục tiêu chính:
    Phân nhóm bệnh nhân bằng thuật toán K-Means.
    Khám phá các luật kết hợp bằng thuật toán Apriori.
    Hỗ trợ ra quyết định trong chẩn đoán y khoa dựa trên dữ liệu thực tế.
# 1. Nguồn dữ liệu (Data Source)
  Dự án sử dụng bộ dữ liệu chẩn đoán bệnh tim mạch từ tệp HeartDiseaseTrain-Test.csv. Tập dữ liệu này bao gồm 1025 bản ghi lâm sàng của các bệnh nhân, với 14 thuộc tính quan trọng như độ tuổi, giới tính, loại đau ngực, huyết áp lúc nghỉ, chỉ số cholesterol, và kết quả điện tâm đồ. Đây là nguồn dữ liệu đa chiều, chứa cả các biến định lượng (số học) và định danh (phân loại), cung cấp cái nhìn toàn diện về tình trạng sức khỏe của bệnh nhân phục vụ cho việc khai phá tri thức.
# 2. Tiền xử lý dữ liệu (Data Preprocessing)
  Trước khi đưa vào mô hình, dữ liệu thô đã được xử lý qua nhiều bước nghiêm ngặt. Đối với các biến liên tục như tuổi, huyết áp và nhịp tim, chúng tôi thực hiện kỹ thuật "rời rạc hóa" (Binning) để chuyển đổi chúng thành các nhóm đặc trưng (Ví dụ: Thấp, Trung bình, Cao). Đồng thời, các thuộc tính số học được chuẩn hóa bằng StandardScaler để đảm bảo các biến có cùng thang đo, tránh gây sai lệch cho thuật toán phân cụm. Cuối cùng, kỹ thuật One-Hot Encoding được áp dụng để chuyển đổi dữ liệu danh mục thành dạng nhị phân, sẵn sàng cho việc tìm luật kết hợp.
# 3. Khai phá luật kết hợp bằng thuật toán Apriori
  Sau khi dữ liệu đã được rời rạc hóa, thuật toán Apriori được áp dụng để tìm kiếm các mối liên hệ tiềm ẩn giữa các triệu chứng. Với ngưỡng độ hỗ trợ (Support) tối thiểu 0.2 và độ tin cậy (Confidence) tối thiểu 0.7, chúng tôi đã trích xuất được nhiều luật có giá trị y khoa cao. Ví dụ, kết quả từ tệp heart_disease_association_rules.csv cho thấy những bệnh nhân bị đau thắt ngực khi gắng sức thường có tỷ lệ cao thuộc nhóm không mắc bệnh nặng (target 0) với chỉ số Lift lên tới 2.0. Điều này giúp các bác sĩ nhanh chóng nhận diện các tập hợp triệu chứng thường đi kèm với nhau.
# 4. Phân cụm dữ liệu bằng K-Means
  Dựa trên các đặc trưng lâm sàng đã chuẩn hóa, thuật toán K-Means được triển khai để phân nhóm bệnh nhân một cách tự động. Mục tiêu của bước này là tìm ra các phân khúc bệnh nhân có hồ sơ sức khỏe tương đồng mà không cần biết trước nhãn bệnh. Kết quả phân cụm được lưu trong tệp HeartDisease_Clustered.csv, chia dữ liệu thành các nhóm riêng biệt. Việc này cho phép xác định rõ ràng sự khác biệt về chỉ số sinh tồn và mức độ nguy hiểm giữa các nhóm đối tượng khác nhau trong tập dữ liệu.
# 5. Đánh giá kết quả (Evaluation)
  Chất lượng của mô hình được kiểm chứng thông qua hai phương pháp là Elbow (Khuỷu tay) và Silhouette Score, được trực quan hóa trong file clustering_evaluation.png. Biểu đồ cho thấy giá trị Silhouette đạt đỉnh cao nhất khi số lượng cụm $k=2$, minh chứng cho việc dữ liệu được phân tách một cách rõ ràng và ổn định nhất. Kết quả đánh giá này khẳng định tính tin cậy của việc phân loại bệnh nhân, giúp đảm bảo rằng các nhóm được tạo ra có sự đồng nhất cao về mặt đặc điểm sinh học và bệnh lý.
