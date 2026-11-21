# Phiếu QC 1 — Road v1.0 (bản tự kiểm có hỗ trợ)

**Lô được phân công kiểm:** Trần Đức Kỳ — 2A202603277  
**Người kiểm:** Nguyễn Ngọc Đồng — 2A202603291  
**Ngày:** 21/11/2026 · **Guideline:** Road v1.0  
**File đã kiểm:** `annotations.xml`, SHA-256 `33b99f77f919e074c4dfd361dd5f900e9986ffd4828ece44a12f9076e0c21ff0`; revision chưa có manifest để xác nhận. Học viên xác nhận đây là lô của Trần Đức Kỳ; metadata project trong file hiển thị tên khác, cần đối chiếu lại với người giao lô trước khi phát hành phiếu chính thức.

**Phạm vi:** 6 ảnh bắt buộc A02, A03, A04, B03, B04, B07; tổng cộng 50 shape và 24 tag trong sáu ảnh. Đã chạy lint toàn file 28 ảnh và xem ảnh chồng nhãn cho sáu ảnh; không có GT để xác nhận khoảng cách 5 px. Các phép kiểm dưới đây chỉ là phạm vi thực hiện, không khẳng định toàn bộ 74 nhãn đã được kiểm trên từng mã. AI hỗ trợ thống kê và rà soát.

## Tổng hợp theo mã

| Mã | Phạm vi kiểm đã thực hiện | Lỗi chắc chắn | Mức |
| --- | --- | ---: | --- |
| QC1-01 | Tag camera của 6 ảnh, đối chiếu danh sách camera | 2 | nặng |
| QC1-02 | L1/R1 trong 3 ảnh front được chọn qua XML | 0 cảnh báo thiếu từ lint | nặng; cần xem ảnh/GT |
| QC1-03 | Position của 3 lane B07 camera bên | 3 | nặng |
| QC1-04 | Thứ tự điểm của 11 lane trong A02/A03/A04 | 2 | chính |
| QC1-05 | Kiểm position trùng trong 3 ảnh front | Chưa kết luận; A04 có position trùng | chính |
| QC1-06 | Giá trị thuộc tính trong XML | Chưa đối chiếu toàn bộ với ảnh/GT | chính |
| QC1-07 | Xem tổng quan vùng lái trong 6 ảnh | Chưa đo/đối chiếu đầy đủ | chính |
| QC1-08 | Chưa kiểm đầy đủ sự hiện diện và màu đèn | Chưa kết luận | nặng/chính |
| QC1-09 | Chưa kiểm đầy đủ facing/type/group/biển phụ | Chưa kết luận | chính |
| QC1-10 | Chưa kiểm đủ hình in và tất cả biển | Chưa kết luận | chính |
| QC1-11 | Kiểm edge_zone một box B04 theo ngưỡng checker | 1 gợi ý cần xác nhận | chính |
| QC1-12 | File XML đọc được bằng parser | 0 lỗi đọc XML | nhẹ/nặng |

## Các lỗi xác định và gợi ý cần xác minh

| # | Mã | Ảnh | Nhãn (vị trí tham chiếu) | Mức | Mô tả |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-01 | B03 | tag `camera` | nặng | `fisheye_front`, trong khi B03 có hậu tố RV và manifest ghi `fisheye_rear`. |
| 2 | QC1-01 | B04 | tag `camera` | nặng | `fisheye_front`, trong khi B04 có hậu tố RV và manifest ghi `fisheye_rear`. |
| 3 | QC1-03 | B07 | lane#1 gần (932,283) | nặng | Camera phải nhưng position là R1; camera bên dùng `other`. |
| 4 | QC1-03 | B07 | lane#5 gần (139,693) | nặng | Camera phải nhưng position là R1; camera bên dùng `other`. |
| 5 | QC1-03 | B07 | lane#6 gần (127,510) | nặng | Camera phải nhưng position là R2; camera bên dùng `other`. |
| 6 | QC1-04 | A02 | lane#1 gần (567,398), L1 | chính | Điểm đầu ở xa/cao hơn điểm cuối: thứ tự ngược quy tắc gần → xa. |
| 7 | QC1-04 | A03 | lane#8 gần (596,384), R1 | chính | Điểm đầu ở xa/cao hơn điểm cuối: thứ tự ngược quy tắc gần → xa. |
| 8 | QC1-11 | B04 | traffic_sign#1 gần (1062,164) | chính — gợi ý | Box có tâm ngoài ngưỡng 80% theo checker nhưng `edge_zone=false`; cần kiểm lại hình tròn thực tế. |

## Ca chờ xác minh

| Ảnh | Vấn đề |
| --- | --- |
| A04 | Hai lane cùng L1 và hai lane cùng R2; kiểm xem một vạch đôi bị gán hai lần hoặc hai vạch khác nhau bị cùng position. |
| A03 | Một số position có vẻ cần so lại với vị trí xe; chưa kết luận khi chưa kiểm chi tiết từng vạch. |
| B04 | Xác minh hình tròn hợp lệ trước khi chốt `edge_zone`. |
| B07 | Sau khi sửa position, kiểm thêm các đường được gọi là lane có đúng vạch làn hay thuộc crosswalk. |

## Quyết định

**Đề xuất Rework:** có ít nhất 5 lỗi nặng xác định; hai lỗi chiều vẽ mức chính và một gợi ý vùng biên. Do chưa kiểm toàn diện từng mã và chưa xác nhận `edge_zone`, **chưa tính tỉ lệ lỗi chính**. Không coi phiếu này là xác nhận đã hoàn tất QC 1 đầy đủ; cần đối chiếu danh tính lô, hoàn tất các mã chưa kiểm và người kiểm xác nhận trước khi bàn giao.

