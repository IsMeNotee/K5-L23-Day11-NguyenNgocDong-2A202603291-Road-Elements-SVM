# Báo cáo Ngày 11 — Road Elements & SVM

**Họ tên:** Nguyễn Ngọc Đông · **Mã học viên:** 2A202603291  
**Guideline:** Road v1.0 · **Manifest:** revision 1

## 1. Project và nguồn nhãn

Task front [#2781436](https://app.cvat.ai/tasks/2781436), job #4751015 có 16 ảnh và đã được đặt trạng thái `completed` trên CVAT. Trạng thái của task fisheye chưa có bằng chứng để xác nhận. Kiểm project front trên CVAT có sáu label hình học và bốn label tag; việc đối chiếu tất cả thuộc tính với guideline cần được hoàn tất.

Front lấy từ `lastttt.zip` của học viên; bản công khai đã xóa email trong metadata, giữ nguyên nội dung nhãn và tọa độ. Một phần thao tác được trợ lý hỗ trợ. B01–B12 được trích từ tệp XML do một bạn cung cấp, không phải nhãn tự gán; đã sửa bốn camera theo tên ảnh, bốn `position` của camera bên thành `other`, và ba `edge_zone` theo phép tính của checker. Tọa độ bộ B không thay đổi. Bản B được dựng lại và chưa được xác nhận nhập lại vào CVAT.

## 2. Số lượng trong file

| Tập | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| Front A01–A12 | 12 | 30 | 3 | 3 | 26 | 39 | 44 |
| Front thêm A13–A16 | 4 | 9 | 1 | 4 | 8 | 13 | 23 |
| Fisheye B01–B08 | 8 | 8 | 11 | 8 | 8 | 2 | 1 |
| Fisheye thêm B09–B12 | 4 | 0 | 2 | 5 | 4 | 0 | 0 |

Số lượng trong file không chứng minh nhãn đúng hoặc ảnh thưởng đạt yêu cầu.

## 3. Trường hợp cần lưu ý

| Ảnh | Nhận định | Xử lý |
| --- | --- | --- |
| A05 | Người nộp xác nhận không thấy vạch L1/R1; lint vẫn báo hai cảnh báo QC1-02. | Không tự vẽ thêm; ghi ngoại lệ trong [phiếu tự kiểm](QC-tu-kiem.md). Chưa có bằng chứng riêng về xác nhận của coach. |
| B05/B06 | Người nộp xác nhận không có L1/R1. Đây là camera bên; nếu có lane thì dùng `position=other`. | Không tự tạo L1/R1. So riêng các nhóm nhãn khác với ảnh và kế hoạch. |
| B05 | File có crosswalk, chưa có road_curb dù kế hoạch nêu nhóm này. | Kiểm ảnh để quyết định có thiếu nhãn không. |
| B06 | File có crosswalk, chưa có drivable hoặc lane dù kế hoạch nêu các nhóm đó. | Kiểm ảnh; không suy ra thiếu vạch chỉ từ lint. |
| B09/B11 | Các nhóm lane/đèn/biển theo trọng tâm ảnh thưởng chưa thấy trong file. | Kiểm trực quan và xác nhận trước khi tính thưởng. |

## 4. Phiếu QC 1

Người được phân công để học viên đánh giá: **Trần Đức Kỳ — 2A202603277**. Học viên xác nhận file XML đã cung cấp là lô của bạn Kỳ; metadata project hiển thị tên khác nên cần đối chiếu với người giao lô. Đã lập [phiếu QC 1 bản tự kiểm có hỗ trợ](NguyenNgocDong-qc1-for-TranDucKy.md) cho 6 ảnh: đề xuất Rework vì có ít nhất 5 lỗi nặng xác định. Một số mã chưa kiểm đầy đủ, chưa tính tỉ lệ lỗi chính; cần hoàn tất và xác nhận phiếu trước khi nộp.

Theo học viên, người kiểm bài của học viên là **Nguyễn Văn Nhất**; chưa có mã học viên hoặc nội dung phiếu/nhận xét và chưa xác minh quyết định Release/Hold/Rework. Không ghi đã sửa theo phiếu khi chưa có bằng chứng.

## 5. Kiểm file và manifest

| Tệp | Kích thước | SHA-256 | Số ảnh / đủ bốn tag |
| --- | ---: | --- | --- |
| `NguyenNgocDong-front.zip` | 76592 | `c61088e2ed418eb02268048944f91e5f9e6162ac58dee4b6d223ce88e671fd55` | 16 / 16 |
| `NguyenNgocDong-fisheye.zip` | 7301 | `51512a83ac8451473ee11b3c24532c982492d4ec855353ca6a7ebe30f990acc6` | 12 / 12 |

Hai zip chỉ chứa XML, không kèm ảnh; công cụ đọc được cả hai. `road_check selftest` trước đó PASS trên dữ liệu tổng hợp. Lint của bộ hiện tại: **2 cảnh báo nặng, 0 chính, 11 nhẹ**. Hai cảnh báo nặng đều là A05 thiếu L1/R1, cần xử lý theo ngoại lệ nêu trên. Lint không so GT, không đo độ lệch ≤ 5 px và không chứng minh đã đạt. Chưa đối chiếu số shape của hai ảnh giữa CVAT và file.

## 6. Bằng chứng ảnh

Bốn ảnh dưới đây được lưu trong thư mục `evidence/`:

1. [Task front trên CVAT: label và trạng thái completed](../evidence/01-front-cvat-task-completed.jpg).
2. [Front A01: chồng nhãn dựng trực tiếp từ XML export](../evidence/02-front-export-annotations.jpg).
3. [Fisheye B01/B03/B07/B10: polyline cong và các shape chồng từ XML export](../evidence/03-fisheye-export-overlays.jpg).
4. [Đoạn XML B03: hình và thuộc tính lane/drivable](../evidence/04-fisheye-xml-excerpt.jpg).

Ảnh 1 là ảnh chụp CVAT. Ba ảnh còn lại là ảnh dựng lại trực tiếp từ ZIP/XML và ảnh nguồn để làm bằng chứng export; chúng **không** thay thế việc nhập lại fisheye vào CVAT.

## 7. Tự đánh giá

Chưa có kết quả phiếu QC nhận được nên chưa xác định lỗi mắc nhiều nhất hay xác nhận đã sửa theo phiếu. Một vạch sai tâm có thể tạo nhãn huấn luyện sai và làm mô hình học vị trí làn sai; tác động định lượng phải được đánh giá riêng.

## 8. Row-anchor (tùy chọn)

Chưa thực hiện; không có số liệu so sánh.
