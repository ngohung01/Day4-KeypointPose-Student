# Peer review - bài gán nhãn của bạn cùng nhóm

Người gán được kiểm: Chưa cung cấp tên Người kiểm: Ngô Văn Hưng Ngày: 16/9/2026

Thư mục bài được kiểm: `bancungnhom/dataset/labels/train`

## Kết quả kiểm tra tự động

- Có đủ 20/20 file nhãn và 29 skeleton.
- `check_pose_labels.py` không báo lỗi định dạng.
- Visibility của bài bạn cùng nhóm: `v=2 357 | v=1 109 | v=0 27`.
- So sánh với bài của tôi cho thấy chênh lệch `%v=1` lớn nhất ở `left_hip`: bài tôi 38%, bài bạn 21%, lệch 17 điểm phần trăm.
- Đây là khác biệt guideline cần thống nhất, chưa đủ bằng chứng để kết luận một bên gán sai chỉ từ số liệu.

## Reviewer checklist

|     | Mục kiểm                                                            | Đạt?          | Ghi chú / ảnh nào                                                                                                    |
| --- | ------------------------------------------------------------------- | ------------- | -------------------------------------------------------------------------------------------------------------------- |
| 1   | Mọi người trong ảnh đều có đủ 17 điểm, không ai bị thiếu            | Đạt định dạng | Có 29 skeleton; cần đối chiếu trực quan từng người nếu muốn xác nhận hoàn toàn.                                      |
| 2   | Bật đường nối: không có xương nào cắt chéo ở vai hoặc hông          | Cần xem ảnh   | Script phát cảnh báo ở `train_02`, người 1, vai và hông; `train_13`, người 2, vai và hông có dấu hiệu đảo trái/phải. |
| 3   | Không có xương nào kéo dài sang một cơ thể khác                     | Cần xem ảnh   | Cần mở visualization để xác nhận; chưa gọi là lỗi chắc chắn chỉ từ cảnh báo số.                                      |
| 4   | Khớp bị che dùng `v = 1` và có chấm, không phải `v = 0`             | Cần xem ảnh   | Script cảnh báo có nhiều `v=0` ở `train_04`, `train_10`, `train_13` dù box người không chạm mép ảnh.                 |
| 5   | `v = 0` chỉ xuất hiện ở khớp thật sự ra ngoài mép ảnh               | Cần xem ảnh   | Cùng các cảnh báo `train_04`, `train_10`, `train_13`; cần xác định từng khớp qua ảnh.                                |
| 6   | Không có dấu hiệu dùng `Hidden`                                     | Chưa xác minh | Không thể kết luận bằng check định dạng; cần xem trực tiếp các điểm `v=2`.                                           |
| 7   | Export đúng COCO Keypoints 1.0: mảng `keypoints` có 51 số mỗi người | Chưa xác minh | Bài nhãn YOLO hợp lệ; cần xem file COCO export gốc của bạn cùng nhóm.                                                |
| 8   | Bản YOLO Pose: mỗi dòng 56 số, `kpt_shape: [17, 3]`                 | Đạt định dạng | `check_pose_labels.py` đọc được toàn bộ 20 file; `data.yaml` dùng `[17, 3]` trong route chung.                       |
| 9   | Visibility report đã nộp, và hai bảng đã được đặt cạnh nhau         | Đạt           | Có visibility report và đã so sánh với bài của tôi.                                                                  |
| 10  | Mọi ca không rõ đều được ghi trong `GUIDELINE_MINI.md`              | Chưa xác minh | Cần đọc guideline của bạn cùng nhóm.                                                                                 |
| 11  | `check_pose_labels.py` chạy 0 lỗi                                   | Đạt           | Script kết luận `ĐẠT định dạng`; còn 7 cảnh báo không chặn nộp.                                                      |

## Lỗi hoặc cảnh báo cần người gán kiểm tra

| Ảnh            | Người thứ | Khớp                          | Lỗi gì                                                  | Sửa thế nào                                                                                 |
| -------------- | --------: | ----------------------------- | ------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| `train_02.jpg` |         1 | left_shoulder, right_shoulder | Hai vai có hướng ngược với hai mắt, nghi đảo trái/phải  | Mở ảnh visualization, xác định trái/phải theo cơ thể rồi đổi cặp vai nếu cần.               |
| `train_02.jpg` |         1 | left_hip, right_hip           | Hai hông có hướng ngược với hai mắt, nghi đảo trái/phải | Kiểm tra lại hướng thân và đổi cặp hông nếu cần.                                            |
| `train_04.jpg` |         1 | 4 keypoint `v=0`              | Người nằm gọn trong ảnh nhưng có nhiều điểm Outside     | Kiểm tra từng điểm; nếu bị che nhưng còn trong khung, đặt chấm ước lượng và đổi sang `v=1`. |
| `train_10.jpg` |         1 | 4 keypoint `v=0`              | Người nằm gọn trong ảnh nhưng có nhiều điểm Outside     | Kiểm tra từng điểm; chỉ giữ `v=0` khi khớp thực sự ngoài mép ảnh.                           |
| `train_13.jpg` |         1 | 4 keypoint `v=0`              | Người nằm gọn trong ảnh nhưng có nhiều điểm Outside     | Kiểm tra từng điểm; điểm bị blur hoặc bị che nhưng còn trong ảnh phải dùng `v=1`.           |
| `train_13.jpg` |         2 | left_shoulder, right_shoulder | Hai vai có hướng ngược với hai mắt, nghi đảo trái/phải  | Kiểm tra trái/phải theo cơ thể người, không theo phía ảnh.                                  |
| `train_13.jpg` |         2 | left_hip, right_hip           | Hai hông có hướng ngược với hai mắt, nghi đảo trái/phải | Kiểm tra lại hướng thân và đổi cặp hông nếu cần.                                            |

## Hai câu kết luận


- Lỗi lặp đi lặp lại nhiều nhất của bài này: là cách quyết định visibility của hông và các keypoint bị che trong người nằm gọn giữa ảnh.

- Nó là lỗi **thao tác** hay lỗi **guideline chưa rõ**?:  Đây chủ yếu là vấn đề guideline chưa rõ, thể hiện qua chênh lệch `left_hip` 17 điểm phần trăm; các cảnh báo trái/phải ở `train_02` và `train_13` vẫn cần xác nhận trực quan trước khi kết luận là lỗi thao tác.


