# Bài nộp LAB5 — T1 Y tế · Nhóm 9999

**Lớp:** L3A · **Bàn / zone:** ____ · **Track:** T1 · Y tế (kênh chat "Hỏi dược sĩ")

| Họ và Tên | Mã Học Viên | Việc đã làm |
|---|---|---|
| Nguyễn Văn Đăng | 2A202603371 | A · dựng prototype hai màn hình, chụp và đánh số ảnh, viết §5 và chuẩn bị kịch bản demo §7 |
|  |  |  |
|  |  |  |

> Ghi cụ thể việc mỗi người làm — khi demo, ai cũng có thể bị hỏi về phần có tên mình. **Mã học viên phải đúng**: đây là căn cứ đối chiếu điểm.
>
> Mỗi mục chỉ cần đủ **bằng chứng** và **lập luận**, không phải điền đủ ô. **Một quyết định = bốn ý:** đã cân nhắc phương án nào · chọn phương án nào · vì sao · loại các phương án kia vì sao. Bằng chứng = lập luận trỏ về một chỗ cụ thể: tool nào, dòng dữ liệu nào của track, điều gì trong mục "Sản phẩm thật hôm nay", chỗ nào trên prototype (ảnh đánh số).

## §1. Lát cắt & phạm vi

- **Lát cắt (chép từ track):** Trong **kênh chat Hỏi dược sĩ của Pharmacity**, khi **khách** đang nhắn hỏi "tôi (hoặc người nhà) bị X, có thuốc gì không", **AI tự trả lời và gợi ý sản phẩm, hỏi thêm câu sàng lọc, hay chuyển dược sĩ, khuyên đi khám ngay**, để người dùng thuốc không nhận sai sản phẩm và ca nguy hiểm không nằm trong hàng chờ.

| Sản phẩm | Một người dùng | Một việc | Một quyết định của AI | Một kết quả |
|---|---|---|---|---|
| kênh chat Hỏi dược sĩ của Pharmacity | khách | nhắn hỏi "tôi (hoặc người nhà) bị X, có thuốc gì không" | tự trả lời và gợi ý sản phẩm, hỏi thêm câu sàng lọc, hay chuyển dược sĩ, khuyên đi khám ngay | người dùng thuốc không nhận sai sản phẩm và ca nguy hiểm không nằm trong hàng chờ |

- **3 việc tính năng KHÔNG làm** (mỗi việc một câu vì sao):
  1. _…_
  2. _…_
  3. _…_

## §2. Kịch bản rủi ro (chặng 2)

- ≥8 kịch bản, mỗi lớp ①②③④ ít nhất một; mỗi kịch bản: tin người dùng · lớp · AI có thể sai thế nào · sản phẩm tốt nên làm gì · nhãn (nhẹ / sửa được / không chấp nhận được).
- Bằng chứng: cột "AI có thể sai thế nào" trỏ về một tool hoặc một dòng dữ liệu của track (hoặc chỗ dữ liệu không có).

| # | Tin người dùng nhắn | Lớp | AI có thể sai thế nào | Sản phẩm tốt nên làm gì | Nhãn |
|---|---|---|---|---|---|
| 1 |  |  |  |  |  |
| 2 |  |  |  |  |  |
| 3 |  |  |  |  |  |
| 4 |  |  |  |  |  |
| 5 |  |  |  |  |  |
| 6 |  |  |  |  |  |
| 7 |  |  |  |  |  |
| 8 |  |  |  |  |  |

- **Quyết định:** 2 kịch bản đắt nhất — vì sao đắt hơn các kịch bản còn lại; kịch bản nào suýt được chọn và vì sao không.

## §3. Khi AI sai (chặng 3)

Với mỗi kịch bản đắt nhất:

- AI nói gì (nguyên văn) · người dùng thấy gì · làm gì tiếp · ai được báo, sau bao lâu.
- Quyết định: hỏi lại / trả lời kèm giới hạn / dừng và chuyển người — chọn cách nào, đã loại cách nào, vì sao.
- Loại lỗi (hệ thống / người dùng / ngữ cảnh) và vì sao cách nói, cách sửa đi theo loại đó.
- 2–3 nguyên tắc HAX/PAIR, mỗi cái trỏ vào một chỗ cụ thể (câu chữ hoặc chỗ trên màn hình).
- Lỗi nào sửa câu chữ không cứu được (nếu có), và thiết kế cứu nó thế nào.

## §4. Mức tự chủ (chặng 4)

Với mỗi tool:

- Mức của nhóm (tự làm / cần người duyệt / cấm). Nếu cần người duyệt: ai duyệt · người duyệt thấy gì · quá hạn thì sao.
- Lý do theo cost-of-error: sai thì ai chịu gì · đảo lại được không · chờ người thì mất gì.
- Phương án đã cân nhắc và vì sao loại.

| Tool | Mức | Lý do (cost-of-error) | Phương án đã loại, vì sao |
|---|---|---|---|
| `goi_y_san_pham` |  |  |  |
| `chuyen_duoc_si` |  |  |  |
| `khuyen_di_kham` |  |  |  |
| `luu_ghi_chu_suc_khoe` |  |  |  |
| `ban_thuoc_ke_don` |  |  |  |

Thêm:

- Tool khó xếp nhất: mỗi người từng chọn gì, cái giá của mỗi phía (trỏ về kịch bản ở §2), nhóm chốt thế nào.
- Thử mức đã đặt trên 2 kịch bản đắt nhất + 1 kịch bản bình thường: cái sai có bị chặn không? còn việc nào làm khi lẽ ra phải hỏi? người dùng bình thường có phải chờ vô ích không?
- Luật thêm hoặc tool tách bước (nếu có), và vì sao.
- Một mức tự chủ đã đổi lời hứa nào với người dùng.

## §5. Prototype (chặng 5)

- **File:** [`prototype/index.html`](prototype/index.html) (mở trực tiếp bằng trình duyệt). **Công cụ:** HTML/CSS/JavaScript, hai màn hình chuyển bằng tab: khách và dược sĩ. Hai ca dựng sẵn: (1) trẻ 2 tuổi sốt, thở khó, lơ mơ; (2) hỏi thuốc cho con nhưng chưa cho biết tuổi. Toàn bộ chat, thông báo và trạng thái chuyển ca đều là mock trong bộ nhớ trình duyệt. **Không có lời gọi hoặc log AI thật.**
- **Ảnh đánh số:** [`prototype/01-khan-cap.png`](prototype/01-khan-cap.png) cho ca khẩn cấp; [`prototype/02-thieu-thong-tin.png`](prototype/02-thieu-thong-tin.png) cho bước hỏi lại. Số ①: nhãn Trợ lý AI và giới hạn gợi ý (G1/G2). Số ②: dừng gợi ý khi nguy hiểm hoặc hỏi tuổi khi thiếu (G10). Số ③: thẻ “Vì sao?” chỉ đúng dữ kiện trong tin khách (G11/PAIR Explainability). Số ④: đường lui đi khám ngay, chuyển dược sĩ, hủy chuyển khi còn chờ (G8/G9/PAIR Graceful Failure). Tab dược sĩ cho thấy thông tin đã chuyển, gồm căn cứ và những việc AI chưa làm.
- **Thể hiện độ chắc:** chọn câu “chưa đủ căn cứ gợi ý thuốc” và nêu dữ kiện cụ thể (chưa biết tuổi; hoặc có “thở khó”, “lơ mơ”), không dùng phần trăm độ tin cậy giả. Cân nhắc thanh % nhưng loại vì con số không nói cho khách biết thiếu gì hay phải làm gì tiếp.
- **Điều khiển mức tự chủ:** `khuyen_di_kham` tự hiện ngay khi có dấu hiệu nguy hiểm; `chuyen_duoc_si` tự chuyển khi đã biết là trẻ nhỏ hoặc vẫn thiếu tuổi, khách hủy được khi đang chờ. `goi_y_san_pham` cần dược sĩ duyệt nên không có nút gợi ý trong hai ca này; `luu_ghi_chu_suc_khoe` không dùng; `ban_thuoc_ke_don` cấm. Cân nhắc để AI gợi ý thuốc kèm lời cảnh báo, nhưng loại vì khách có thể dùng thuốc trước khi đọc phần cảnh báo, không đảo lại được. Bảng mức này là đề xuất của A để minh họa prototype; nhóm cần chốt thống nhất với §4.
- **Đường bấm:** Ca 1 → đọc cảnh báo khẩn → bấm “Tôi đang đưa bé đi khám” hoặc “Xem thông báo cho dược sĩ” → tab dược sĩ thấy thông báo tức thì, không đưa khách vào hàng chờ. Ca 2 → AI hỏi tuổi → bấm “Bé 3 tuổi”/“Tôi chưa rõ” → cuộc chat chuyển dược sĩ → xem hồ sơ chuyển, hoặc hủy chuyển và chuyển lại. Nếu chọn “Bé thở khó hoặc lơ mơ”, luồng chuyển ngay sang cảnh báo khẩn.

## §6. Tốt là gì (chặng 6 — nhẹ, bỏ được nếu thiếu giờ)

- 3 tiêu chí Pass/Fail chấm được; thiết kế của nhóm đạt tiêu chí nào trên 2 kịch bản đắt nhất; lỗi còn lại.

## §7. Demo

- **Kịch bản A điều phối (khoảng 4 phút):** B mở đầu 30 giây bằng lát cắt. A mở `prototype/index.html`, bấm ca 1 và đọc câu AI nguyên văn; chỉ ① nhãn AI, ② khối khẩn không xếp hàng, ③ “Vì sao”, ④ hành động tiếp. A bấm “Xem thông báo cho dược sĩ” để cho thấy ca đến ngay cùng căn cứ, không có gợi ý thuốc. A đổi sang ca 2, bấm “Bé 3 tuổi”, cho thấy tự chuyển dược sĩ và nút hủy chuyển; thử nhánh “Bé thở khó hoặc lơ mơ” để quay về cảnh báo khẩn. C nêu mức tự chủ và cái giá khi sai. B giải thích câu chữ và ai được báo.
- **Ca lạ do TA/giảng viên đưa:** C trả lời theo §4; A chỉ đường tương ứng trên prototype nếu ca thuộc một trong hai nhánh dựng sẵn. Với ca khác, nhóm nói rõ giới hạn của prototype mock và mô tả quyết định, không giả vờ đã xử lý bằng AI thật. Ghi ca lạ thực tế, nhóm đã làm gì và có đổi ý gì **sau khi demo**: _chưa diễn ra_.
