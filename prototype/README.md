# Prototype — T1 Y tế · Nhóm 9999

- **Phụ trách A:** Nguyễn Văn Đăng · `2A202603371`.
- **Mở file:** [index.html](index.html) bằng trình duyệt trên máy. Không cần cài đặt, đăng nhập hay backend.
- **Công cụ:** HTML, CSS, JavaScript. Hai màn hình trong cùng một file: khách và dược sĩ; hai ca dựng sẵn ở thanh trên cùng.
- **Phần mock:** toàn bộ tin nhắn, dữ kiện, thông báo khẩn, hàng nhận ca, nút “đã xem” và trạng thái chuyển/hủy chuyển. Mọi thay đổi chỉ tồn tại trong bộ nhớ tab trình duyệt.
- **Lời gọi và log AI:** không có. Không dùng dữ liệu sức khỏe thật.

## Cách bấm demo

1. Chọn **Ca 1 · Dấu hiệu nguy hiểm**. Đọc câu AI, chỉ khối khẩn ② và thẻ căn cứ ③. Bấm **Tôi đang đưa bé đi khám** hoặc **Xem thông báo cho dược sĩ**. Ca khẩn không nằm trong hàng chờ.
2. Chọn **Ca 2 · Trẻ nhỏ, thiếu thông tin**. AI hỏi tuổi thay vì đoán. Bấm **Bé 3 tuổi** để chuyển dược sĩ; bấm **Hủy yêu cầu chuyển** để thấy cách sửa, hoặc mở tab **Màn hình dược sĩ** để xem dữ kiện được chuyển. Thử nút **Bé thở khó hoặc lơ mơ** để chuyển sang cảnh báo khẩn.

## Ảnh có đánh số

| Ảnh | Số | Thể hiện gì | Nguyên tắc HAX/PAIR | Mức tự chủ |
|---|---|---|---|---|
| [01-khan-cap.png](01-khan-cap.png) | ① | Nhãn Trợ lý AI, chưa chẩn đoán hoặc gợi ý thuốc | G1/G2 | Gợi ý sản phẩm cần dược sĩ duyệt |
| [01-khan-cap.png](01-khan-cap.png) | ② | Cảnh báo đi khám/cấp cứu ngay, ngoài hàng chờ | G10 | `khuyen_di_kham` tự hiện |
| [01-khan-cap.png](01-khan-cap.png) | ③ | “Vì sao?” chỉ ra “thở khó”, “lơ mơ” | G11 / PAIR Explainability | Không gọi `goi_y_san_pham` |
| [01-khan-cap.png](01-khan-cap.png) | ④ | Đường tiếp theo cho khách và thông báo cho dược sĩ | G8/G9 / PAIR Graceful Failure | Thông báo khẩn tự chuyển |
| [02-thieu-thong-tin.png](02-thieu-thong-tin.png) | ② | Hỏi đúng một câu về tuổi trước khi quyết định | G10 | Chưa gợi ý sản phẩm |
| [02-thieu-thong-tin.png](02-thieu-thong-tin.png) | ③–④ | Nêu dữ kiện thiếu và cho gặp dược sĩ | G11, G8/G9 | `chuyen_duoc_si` tự chuyển, hủy được khi chờ |

**Lưu ý khi ghép bài:** bảng mức tự chủ trong prototype là đề xuất của A. Cần đối chiếu với §4 của C trước khi nộp để hai phần nói cùng một mức.
