# Báo cáo Ngày 11 — Road Elements & SVM

Họ tên: Nguyễn Ngọc Đông · Mã học viên: 2A202603291  
Guideline: Road v1.0

## Bàn giao

`NguyenNgocDong-front.zip` được tạo từ `lastttt.zip` do học viên cung cấp. Bản công khai được xóa địa chỉ email trong metadata; các nhãn và tọa độ được giữ nguyên. Theo yêu cầu, bản này **chưa chạy lại lint hoặc kiểm tra nội dung**, nên chưa thể kết luận chất lượng hay xác nhận hết cảnh báo.

`NguyenNgocDong-fisheye.zip` giữ nguyên bản đã chuẩn bị từ XML do một bạn cung cấp. Các thuộc tính camera, vị trí làn camera bên và một số cờ vùng biên đã được sửa trong phiên trước; tọa độ của bộ fisheye giữ nguyên. Bộ này chưa được xác nhận import lại vào CVAT.

Manifest ghi kích thước và SHA-256 của hai tệp công khai; trường lint để trống do không chạy lại. Thống kê được ghi trước đó đối với bộ fisheye không thay thế kiểm tra chất lượng.

## Ghi chú QC

Ảnh A05 không thấy vạch phân làn: lint ở bản trước từng báo thiếu L1/R1, không nên tự vẽ thêm để làm mất cảnh báo. Theo đặc tả bàn giao, cần coach xác nhận ngoại lệ. [Phiếu tự kiểm trước đó](QC-tu-kiem.md) ghi các nhận xét cho bản export trước, không được coi là kết quả kiểm tra của `lastttt.zip`.

Chưa có bằng chứng phiếu QC 1 độc lập, xác nhận coach, đối chiếu GT hoặc đủ ảnh chụp theo mẫu. Điểm thưởng chưa được xác minh.

