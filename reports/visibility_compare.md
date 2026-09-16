# Visibility report

- Thư mục nhãn: `dataset/labels/train`
- 20 ảnh, 29 skeleton, trung bình 16.03 khớp có v > 0 mỗi người
- Tổng: v=2 335 | v=1 130 | v=0 28

So sánh với `bancungnhom/dataset/labels/train` (29 skeleton).
Cột **lệch** là hiệu số phần trăm v=1 - chỗ nào lệch nhiều nhất là chỗ guideline chưa nói rõ.

| # | Khớp | %v=1 (bạn) | %v=1 (đối chiếu) | lệch |
| ---: | --- | ---: | ---: | ---: |
| 11 | left_hip | 38% | 21% | 17 |
| 3 | left_ear | 66% | 55% | 10 |
| 1 | left_eye | 34% | 24% | 10 |
| 2 | right_eye | 31% | 24% | 7 |
| 10 | right_wrist | 31% | 24% | 7 |
| 16 | right_ankle | 21% | 14% | 7 |
| 4 | right_ear | 48% | 41% | 7 |
| 7 | left_elbow | 24% | 17% | 7 |
| 9 | left_wrist | 28% | 31% | 3 |
| 14 | right_knee | 14% | 17% | 3 |
| 15 | left_ankle | 17% | 14% | 3 |
| 6 | right_shoulder | 0% | 3% | 3 |
| 0 | nose | 24% | 21% | 3 |
| 13 | left_knee | 28% | 24% | 3 |
| 5 | left_shoulder | 10% | 10% | 0 |
| 8 | right_elbow | 14% | 14% | 0 |
| 12 | right_hip | 21% | 21% | 0 |

## Đọc bảng này thế nào

1. Khớp nào có **%v=1 cao**: khớp hay bị che. Cổ tay và hông thường là hai vị trí cần xem lại guideline trước khi kết luận.
2. Khớp nào có **v=0 cao bất thường**: mọi người đang dùng Outside ở chỗ đáng lẽ là Occluded. Đó là lỗi số 3 của slide 46, và nó xoá thẳng khớp đó khỏi bảng điểm OKS.
3. Khi so hai người: **lệch lớn = bất đồng về guideline**, không phải về bức ảnh. Sửa guideline trước, sửa nhãn sau.
