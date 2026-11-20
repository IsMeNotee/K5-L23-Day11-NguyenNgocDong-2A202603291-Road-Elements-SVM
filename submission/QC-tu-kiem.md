# Phiếu tự kiểm — front export mới

Nguồn: `front_last.zip` do học viên cung cấp, SHA-256 `dafc73ca0440ffab93154a8e5faa964fc3f598da25241306945c262fd34f6fb0`. Đây là tự kiểm, không thay thế Phiếu QC 1 của người kiểm độc lập.

| Mã | Ảnh | Nhận định | Xử lý |
| --- | --- | --- | --- |
| QC1-02 | A05 | Lint báo thiếu L1 và R1 vì tìm nhãn theo khuôn, nhưng ảnh đường không có vạch phân làn nhìn thấy. Cảnh báo này không đủ căn cứ kết luận thiếu nhãn. | **Không tự vẽ thêm L1/R1.** Ghi nhận ca ngoại lệ và nhờ coach xác nhận theo đặc tả bàn giao. Ảnh CVAT do học viên cung cấp cho thấy bốn tag và một vùng drivable. |
| QC1-02 | A13 | Lane trắng đã gán R1; lint báo thiếu L1. | Vạch vàng bên trái mờ, kiểm lại trên ảnh trước khi vẽ và xin coach xác nhận nếu không thấy rõ. |
| QC1-02 | A16 | Đã có L1 và R1. | Cần kiểm độ sát tâm vạch trong CVAT. |
| QC1-04 | A06 và A08 | Hai L1 đã đảo thứ tự điểm; lint không còn báo ngược chiều. | Kiểm trực quan. |
| QC1-02/QC1-03 | A06, A07, A14 | Bản mới đã có cả L1 và R1 nên lint không còn báo thiếu; tuy nhiên hình học của một số vạch mới chạy sát mép đường hoặc vùng tối. | Xem kỹ ảnh gốc ở độ phóng đại, xác nhận là vạch sơn và đúng vị trí, không dựa vào việc lint hết cảnh báo để kết luận đúng. |

Lint cho cả front mới và fisheye: 3 cảnh báo nặng (2 ở A05, 1 A13), 0 chính, 11 nhẹ. Không có GT để đo sai lệch; coach xác nhận ngoại lệ A05. Không khẳng định A05 đã được coach miễn khi chưa có xác nhận.

