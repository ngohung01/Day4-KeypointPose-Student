# Báo cáo Ngày 4 - Keypoint & Pose

Họ tên: Ngô Văn Hưng, Nhóm: 201 Ngày: 16/9/2026

## 1. Nhãn của tôi

| Chỉ số                       |        Giá trị |
| ---------------------------- | -------------: |
| Số ảnh đã gán                |             20 |
| Số skeleton                  |             29 |
| v=2 / v=1 / v=0              | 335 / 130 / 28 |
| Thời gian trung bình mỗi ảnh |              9 |

Ba khớp có `%v=1` cao nhất:

1. `left_ear`: 66% (19/29)
2. `right_ear`: 48% (14/29)
3. `left_hip`: 38% (11/29)

Tai là khớp thường bị tóc hoặc vật che nên có tỷ lệ `v=1` cao. Hông có tỷ lệ `v=1` cao chủ yếu vì vị trí giải phẫu thường bị che, dù vẫn có thể ước lượng theo thắt lưng và hướng thân. Đây là điểm guideline của nhóm chưa hoàn toàn thống nhất, thể hiện qua chênh lệch `left_hip` giữa hai bảng: 38% ở bài của tôi và 21% ở bạn cùng nhóm.

## 2. Chấm với gold

| Chỉ số                | Trước rework | Sau rework |
| --------------------- | -----------: | ---------: |
| OKS trung bình        |        0.946 |     0.948 |
| OKS@0.50              |        1.000 |      1.000 |
| OKS@0.75              |        1.000 |      1.000 |
| Lỗi `dao_trai_phai`   |            0 |          0 |
| Lỗi `nham_nguoi`      |            1 |          0 |
| Lỗi `xoa_khop_bi_che` |            0 |          0 |

### Tôi đã sửa gì giữa hai lần chạy

- `train_04.jpg`, người thứ 1, `left_wrist`: sửa điểm cổ tay bị đặt nhầm sang cơ thể bên cạnh, đưa về đúng cánh tay của người thứ nhất.

Bản đánh giá sau rework ghép đúng 29/29 người, không thiếu hoặc thừa skeleton. Có 5 cảnh báo `lech_nhe`; các khác biệt visibility gồm 54 `co_khac_gold` và 73 trường hợp gold để `v=0`, đều không trừ điểm OKS theo quy định của lab.

**Lỗi đảo trái/phải:** Không có lỗi đảo trái/phải trong cả hai lần đánh giá. Hai lần chạy đều có 0 lỗi `dao_trai_phai`.

## 3. Kiểm chéo

Bạn cùng nhóm: TRƯƠNG CÔNG HOÀI NAM

| Khớp       | Bạn |  Họ |      Lệch | Nguyên nhân (guideline hay gán sai?)                   |
| ---------- | --: | --: | --------: | ------------------------------------------------------ |
| `left_hip` | 38% | 21% | 17 điểm % | Guideline về hông của người mặc quần áo dài chưa đủ rõ |

Luật mới đã bổ sung vào `GUIDELINE_MINI.md`: nếu hông còn nằm trong khung nhưng bị quần áo che, đặt chấm theo xương chậu, thắt lưng và hướng thân rồi dùng `v=1`; chỉ dùng `v=0` khi hông nằm ngoài mép ảnh.

## 4. Model

| Chỉ số         | yolo26n-pose gốc | Sau fine-tune |   Chênh |
| -------------- | ---------------: | ------------: | ------: |
| pose_mAP50     |           0.8450 |        0.8450 | +0.0000 |
| pose_mAP50-95  |           0.6853 |        0.6908 | +0.0055 |
| pose_precision |           0.9734 |        0.9792 | +0.0058 |
| pose_recall    |           0.8462 |        0.8462 | +0.0000 |
| box_mAP50-95   |           0.8119 |        0.8041 | -0.0078 |

### Trả lời năm câu hỏi ở cuối notebook

1. `pose_mAP50-95` tăng `0.0055`, từ `0.6853` lên `0.6908`. Điều này cho thấy 20 ảnh đã bổ sung một ít đặc trưng của bộ ảnh lab, đặc biệt ở các trường hợp người bị che hoặc ảnh mờ. Mức tăng nhỏ phù hợp với kích thước tập train chỉ có 20 ảnh.

2. Sau fine-tune, `box_mAP50-95` là `0.8041`, cao hơn `pose_mAP50-95` là `0.6908` một khoảng `0.1133`. Model tìm đúng người dễ hơn xác định chính xác 17 khớp, vì bbox chỉ cần bao quanh người còn pose phải đặt đúng từng keypoint, nhất là tai, hông và các điểm bị che.

3. Một ca annotation khó đã được xác nhận trong `train_04.jpg`, người thứ nhất: lỗi ban đầu là `nham_nguoi` tại `left_wrist`, tức điểm bị đặt sang cơ thể bên cạnh. Cần bổ sung tên ảnh test và loại lỗi quan sát từ ảnh dự đoán model nếu muốn mô tả riêng một lỗi của model.

4. Trong so sánh nhãn với gold, OKS thấp nhất là `train_04.jpg`, người thứ nhất trước rework (`0.856`), do lỗi `nham_nguoi` ở `left_wrist`. Sau khi sửa, kết quả cặp này tăng lên `0.9068`. Bằng chứng là danh sách lỗi gold chỉ ra đúng keypoint này; không nên kết luận về ảnh model nếu chưa xem ảnh dự đoán trong notebook.

5. Ảnh annotation có điểm thấp nhất trước rework là `train_04.jpg` người thứ nhất (`0.856`); sau rework, ảnh có cặp thấp nhất là `train_13.jpg` người thứ hai (`0.8622`). Cả hai ảnh đều có khó khăn riêng: `train_04` bị che ở cánh tay, còn `train_13` bị blur. Cần đối chiếu thêm bảng OKS model-vs-label trong notebook để kết luận có trùng với ảnh model đoán tệ nhất hay không.

## 5. Một rule evidence đã dùng

Ở `train_04.jpg`, người thứ nhất, `left_wrist` bị cánh tay hoặc vật khác che nên không xác định chắc chắn hướng bàn tay. Tôi lần theo vai, khuỷu tay và đoạn cẳng tay còn nhìn thấy để ước lượng vị trí cổ tay. Vì cổ tay vẫn còn trong khung ảnh, tôi đặt chấm tại vị trí ước lượng và dùng `v=1`, không dùng `v=0`. Nếu khớp thực sự nằm ngoài mép ảnh thì mới dùng `v=0` và không đặt chấm.
