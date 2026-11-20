# Báo cáo Ngày 11 — Road Elements & SVM

**Họ tên:** Nguyễn Ngọc Đông · **Mã học viên:** 2A202603291  
**Guideline:** Road v1.0 · **Manifest:** revision 1  
**Trạng thái:** đang kiểm tra; chưa xác nhận đủ điều kiện nộp hoặc điểm thưởng.

## Nguồn dữ liệu và phạm vi

- Gói dữ liệu được cung cấp có 28 ảnh: A01–A16 và B01–B12. Ảnh không nằm trong các tệp nhãn bên dưới.
- Bản front gốc của học viên được giữ riêng nguyên byte. Bản front đã rà soát trong gói hiện tại gồm 16 ảnh A và có các sửa đổi: đảo chiều hai lane A06/A08; A13 đổi vị trí lane trắng từ L1 sang R1 và thêm L1 vàng; A16 thêm hai lane L1/R1. Các điểm mới cần kiểm lại trên CVAT vì chưa so với GT. Một phần nhãn trong quá trình làm đã có sự hỗ trợ của trợ lý; cần kiểm tra và chịu trách nhiệm về toàn bộ nội dung trước khi nộp.
- Phần fisheye B01–B12 được trích từ tệp XML do một bạn cung cấp, không phải kết quả tự gán nhãn của học viên. Tệp XML mới được dựng từ các đối tượng B, không mang metadata cá nhân của project nguồn. Nguồn dữ liệu cần được công khai phù hợp với quy định của lớp.
- Với bộ B, đã sửa bốn giá trị tag camera theo hậu tố tên ảnh, bốn giá trị position của lane camera bên thành `other`, và ba giá trị `edge_zone` theo phép kiểm bán kính trong guideline. Tọa độ, số lượng và loại hình của các đối tượng B được giữ nguyên. Việc này không thay thế kiểm tra ảnh trực quan.

## 1. Kiểm project và định dạng

| Mục | Kết quả | Ghi chú |
| --- | --- | --- |
| Sáu label hình học, bốn tag | Có trong metadata của bản front | Kiểu và giá trị cần đối chiếu lại trong project CVAT thực tế. |
| Bốn tag cho mỗi ảnh | Có trong cả 28 mục ảnh | Các camera B đã sửa theo tên tệp; các tag khác cần rà soát theo ảnh. |
| File zip | Mỗi zip chứa `annotations.xml`, không chứa ảnh; đọc lại bằng script | File fisheye được dựng lại, chưa xác nhận import vào CVAT. |
| CVAT và trạng thái job | Chưa xác minh | Chưa có xác nhận các job completed. |

## 2. Thống kê nhãn trong XML

Thống kê là số đối tượng có trong file, không khẳng định đầy đủ hay chính xác theo GT.

| Tập | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| Front A01–A12 | 12 | 28 | 3 | 3 | 26 | 39 | 44 |
| Front thêm A13–A16 | 4 | 8 | 2 | 4 | 8 | 13 | 23 |
| Fisheye B01–B08 | 8 | 8 | 11 | 8 | 8 | 2 | 1 |
| Fisheye thêm B09–B12 | 4 | 0 | 2 | 5 | 4 | 0 | 0 |

Việc có nhãn trên ảnh thêm không chứng minh ảnh đó đạt tiêu chí điểm thưởng; cần kiểm đủ nhãn yêu cầu và độ lệch theo guideline.

## 3. Ca cần kiểm tra

| Ảnh | Nội dung | Tình trạng |
| --- | --- | --- |
| A05, A06, A07 | Lint báo thiếu L1 hoặc R1 | Xem ảnh: chỉ bổ sung vạch nếu thực sự nhìn thấy; nếu không, ghi nhận và xin coach xác nhận. |
| A13, A16 | Vạch đã được bổ sung | Cần xem lại độ sát tâm vạch và thuộc tính; chưa có GT để chứng minh sai lệch ≤ 5 px. |
| A14 | Lint báo thiếu R1 | Không thấy rõ sơn phân làn bên phải; chờ coach xác nhận trước khi thêm. |
| A06, A08 | Chiều polyline | Đã đảo thứ tự các điểm của L1 để vẽ gần → xa; không đổi tọa độ. |
| B02, B04 | Hai đèn và một biển ở vùng biên | `edge_zone` đã sửa theo phép tính bán kính; cần kiểm thực tế theo mép ảnh fisheye. |
| B05, B08, B10, B12 | Biên polygon gần thân xe/vùng tối | Kiểm lại chi tiết để tránh gán vào thân xe hoặc vùng ngoài ảnh hợp lệ. |
| B05, B06, B09, B11 | Một số nhóm nhãn theo kế hoạch chưa thấy trong file | Kiểm ảnh và bảng kế hoạch: B05 chưa có road_curb; B06 chưa có drivable/lane; B09 chưa có lane/đèn/biển; B11 chưa có lane. Không suy ra thiếu nếu ảnh thực sự không thấy, cần coach xác nhận. |

## 4. Phiếu QC 1

Chưa có phiếu QC 1 nhận được, chưa có tên người kiểm và quyết định Release/Hold/Rework. Chưa thực hiện hoặc chưa có bằng chứng về phiếu QC 1 cho một học viên khác; không suy ra phiếu này từ lint. Cần kiểm lô được phân công theo 12 mã và điền số lượng, mức lỗi và quyết định vào mẫu của lớp.

## 5. Kiểm file export

| File | Đọc lại XML | Số ảnh / đủ 4 tag | SHA-256 |
| --- | --- | --- | --- |
| `NguyenNgocDong-front.zip` | ZIP/XML đọc được; bản đã rà soát | 16 / 16 | `6929b3573c820b52320d344e3f9096baeef07a8f5d8aa36416f010781eba43e9` |
| `NguyenNgocDong-fisheye.zip` | ZIP/XML đọc được; chưa thử import CVAT | 12 / 12 | `51512a83ac8451473ee11b3c24532c982492d4ec855353ca6a7ebe30f990acc6` |

`road_check selftest`: **PASS** trên dữ liệu tổng hợp. `road_check lint`: 28 ảnh, **5 cảnh báo nặng, 0 chính, 11 nhẹ**. Các cảnh báo nặng còn lại đều là QC1-02: A05 thiếu L1/R1, A06 thiếu R1, A07 thiếu L1 và A14 thiếu R1. Không tự thêm vạch khi không thấy rõ; cần coach xác nhận. Lint kiểm định dạng và một số quy tắc; không có GT nên không đo độ lệch 5 px, không đánh giá đầy đủ và không chứng minh đạt rubric. Chưa đối chiếu số shape trên hai ảnh giữa job CVAT và export.

## 6. Bằng chứng ảnh

Chưa có đủ bốn ảnh chụp được yêu cầu: tab Labels, ảnh front hoàn chỉnh, ảnh fisheye phóng to đường cong và đoạn XML. Cần bổ sung bằng chứng thực tế; không dùng ảnh minh họa làm bằng chứng công việc.

## 7. Tự đánh giá

Chưa có phiếu QC đã nhận nên chưa thể xác định lỗi mắc nhiều nhất hoặc khẳng định đã sửa theo phiếu. Cần ưu tiên kiểm các vạch L1/R1, chiều vẽ và ranh giới vùng lái. Ví dụ, vạch sai vị trí có thể làm nhãn huấn luyện biểu diễn sai tâm làn; model học theo đó có thể dự đoán sai vị trí làn. Tác động thực tế cần được đo bằng đánh giá mô hình, không suy ra trực tiếp từ lint.

## 8. Row-anchor (tùy chọn)

Chưa thực hiện; không có số liệu so sánh để báo cáo.

