# Phiếu tự kiểm — front export mới

Nguồn: `front (1).zip` do học viên cung cấp, SHA-256 `1148f20b9733d6ad78e2502e2adcd674426d50db41c56ce3ffc6796a2abd1045`. Đây là tự kiểm, không thay thế Phiếu QC 1 của người kiểm độc lập.

| Mã | Ảnh | Nhận định | Xử lý |
| --- | --- | --- | --- |
| QC1-02 | A05 | Lint báo thiếu L1 và R1 vì tìm nhãn theo khuôn, nhưng ảnh đường không có vạch phân làn nhìn thấy. Cảnh báo này không đủ căn cứ kết luận thiếu nhãn. | **Không tự vẽ thêm L1/R1.** Ghi nhận ca ngoại lệ và nhờ coach xác nhận theo đặc tả bàn giao. Ảnh CVAT do học viên cung cấp cho thấy bốn tag và một vùng drivable. |
| QC1-02/QC1-03 | A13 | XML có một lane gán L1; theo ảnh, đường trắng này dường như là ranh giới bên phải xe. Lint báo thiếu R1. | Kiểm lại vị trí L1/R1 trên CVAT; vùng vạch vàng bên trái mờ, cần đối chiếu kỹ trước khi vẽ hoặc đổi thuộc tính. |
| QC1-02 | A16 | XML không có lane L1/R1; ảnh có các đoạn sơn trắng gần xe. | Kiểm lại và gán vạch nhìn thấy theo guideline; không gán vạch ngang của lối sang đường thành lane. |
| QC1-04 | A06 và A08 | Polyline L1 có điểm đầu cao hơn điểm cuối, có thể đang theo chiều xa → gần. | Kiểm và đảo thứ tự điểm nếu đúng; giữ nguyên tọa độ. |
| QC1-02/QC1-03 | A06, A07, A14 | Bản mới đã có cả L1 và R1 nên lint không còn báo thiếu; tuy nhiên hình học của một số vạch mới chạy sát mép đường hoặc vùng tối. | Xem kỹ ảnh gốc ở độ phóng đại, xác nhận là vạch sơn và đúng vị trí, không dựa vào việc lint hết cảnh báo để kết luận đúng. |

Lint cho cả front mới và fisheye: 5 cảnh báo nặng (2 ở A05, 1 A13, 2 A16), 2 chính (A06/A08), 11 nhẹ. Không có GT để đo sai lệch; coach xác nhận ngoại lệ A05. Không khẳng định A05 đã được coach miễn khi chưa có xác nhận.

