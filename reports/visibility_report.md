# Visibility report

- Thư mục nhãn: `dataset/labels/train`
- 20 ảnh, 29 skeleton, trung bình 16.03 khớp có v > 0 mỗi người
- Tổng: v=2 335 | v=1 130 | v=0 28

| # | Khớp | v=2 | v=1 | v=0 | %v=1 |
| ---: | --- | ---: | ---: | ---: | ---: |
| 0 | nose | 22 | 7 | 0 | 24% |
| 1 | left_eye | 19 | 10 | 0 | 34% |
| 2 | right_eye | 20 | 9 | 0 | 31% |
| 3 | left_ear | 10 | 19 | 0 | 66% |
| 4 | right_ear | 15 | 14 | 0 | 48% |
| 5 | left_shoulder | 26 | 3 | 0 | 10% |
| 6 | right_shoulder | 29 | 0 | 0 | 0% |
| 7 | left_elbow | 22 | 7 | 0 | 24% |
| 8 | right_elbow | 25 | 4 | 0 | 14% |
| 9 | left_wrist | 21 | 8 | 0 | 28% |
| 10 | right_wrist | 19 | 9 | 1 | 31% |
| 11 | left_hip | 18 | 11 | 0 | 38% |
| 12 | right_hip | 22 | 6 | 1 | 21% |
| 13 | left_knee | 17 | 8 | 4 | 28% |
| 14 | right_knee | 21 | 4 | 4 | 14% |
| 15 | left_ankle | 15 | 5 | 9 | 17% |
| 16 | right_ankle | 14 | 6 | 9 | 21% |

## Đọc bảng này thế nào

1. Khớp nào có **%v=1 cao**: khớp hay bị che. Cổ tay và hông thường là hai vị trí cần xem lại guideline trước khi kết luận.
2. Khớp nào có **v=0 cao bất thường**: mọi người đang dùng Outside ở chỗ đáng lẽ là Occluded. Đó là lỗi số 3 của slide 46, và nó xoá thẳng khớp đó khỏi bảng điểm OKS.
3. Khi so hai người: **lệch lớn = bất đồng về guideline**, không phải về bức ảnh. Sửa guideline trước, sửa nhãn sau.
