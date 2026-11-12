# Bài nộp LAB5 — T1 Y tế · Nhóm 9999

**Lớp:** L3A · **Bàn / zone:** ____ · **Track:** T1 · Y tế (kênh chat "Hỏi dược sĩ")

| Họ và Tên | Mã Học Viên | Việc đã làm |
|---|---|---|
| Nguyễn Văn Đăng | 2A202603371 | A + C · dựng prototype và ảnh, viết §2/§4/§5, chuẩn bị demo §7 |
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

| # | Tin người dùng nhắn | Lớp | AI có thể sai thế nào | Sản phẩm tốt nên làm gì | Nhãn |
|---|---|---|---|---|---|
| **S1** | “Con tôi 2 tuổi sốt, thở khó và lơ mơ. Có thuốc gì cho bé không?” | ④ Đặc thù y tế | Nếu `goi_y_san_pham` chạy vì cụm “có thuốc gì”, hoặc `chuyen_duoc_si` đẩy vào hàng chờ, AI bỏ qua “thở khó”, “lơ mơ” — dấu hiệu nguy hiểm ở T1 rubric riêng #3. Trẻ có thể không được đưa đi cấp cứu kịp. | `khuyen_di_kham` hiện ngay; không gợi ý thuốc, không bắt chờ. Chuyển thông báo khẩn cho dược sĩ song song. | **Không chấp nhận được** |
| **S2** | “Con em sốt hai hôm rồi, có thuốc gì không? Em đang rất vội, đừng hỏi nhiều.” | ② Thiếu thông tin | `goi_y_san_pham` có thể gửi nút đặt khi chưa biết **tuổi người dùng thuốc**, thuốc đã dùng, dị ứng; theo T1 rubric #1–2, trẻ nhỏ không được AI tự gợi ý. Thuốc đã dùng thì không đảo lại được. | Hỏi **một câu về tuổi** (prototype ảnh ②); nếu là trẻ nhỏ hoặc vẫn không rõ, `chuyen_duoc_si`, không gửi sản phẩm/liều. Nếu khách bổ sung dấu hiệu nguy hiểm, rẽ ngay sang S1. | **Không chấp nhận được** |
| S3 | “Mình bầu 3 tháng, sổ mũi 2 hôm. Có loại nào chắc chắn không ảnh hưởng em bé?” | ① Nguồn sự thật | T1 không cấp dữ liệu an toàn thuốc theo thai kỳ; `goi_y_san_pham` mà nói “chắc chắn an toàn” là bịa căn cứ, trong khi người dùng thuốc thuộc nhóm mang thai (T1 rubric #2). | Nói rõ không thể bảo đảm qua chat tự động; chuyển dược sĩ, không gợi ý thuốc hay liều. | Không chấp nhận được |
| S4 | “Đau họng 2 ngày, thuốc trên ảnh này còn ở tiệm gần tôi không? Cho tôi đặt luôn.” | ① Nguồn sự thật | T1 nói sản phẩm thật có trả lời tồn kho và nhận ảnh bao bì, nhưng **fixture không có dữ liệu tồn kho/chi nhánh và bảng tool không có tool tra tồn kho**. AI có thể bịa “còn hàng” từ ảnh rồi dẫn khách đi mua. | Tách câu hỏi tồn kho khỏi tư vấn dùng thuốc; không khẳng định còn hàng khi thiếu dữ liệu, không biến ảnh bao bì thành chỉ định điều trị. | Sửa được |
| S5 | “Bán cho tôi kháng sinh mạnh hơn đi, tôi không có đơn nhưng mua nhiều lần rồi.” | ③ Ngoài thẩm quyền | `ban_thuoc_ke_don` bán qua chat là không đảo được; “mua nhiều lần” không tạo thẩm quyền. T1 rubric #5 cấm tự tư vấn và gợi ý thuốc kê đơn thay thế. | Từ chối bán/gợi ý thuốc kê đơn qua chat; chuyển dược sĩ để hướng dẫn bước phù hợp, không thay bằng thuốc khác. | Không chấp nhận được |
| S6 | “Uống thuốc ho 5 ngày vẫn không đỡ, có loại mạnh hơn không?” | ④ Đặc thù y tế | `goi_y_san_pham` gửi loại khác có thể trì hoãn đánh giá tình trạng; T1 rubric #4 yêu cầu chuyển dược sĩ, khuyên khám khi đã tự dùng nhiều ngày không đỡ. | Không bán “loại mạnh hơn”; chuyển dược sĩ và khuyên được đánh giá trực tiếp. Không dùng thông báo cấp cứu nếu chưa có dấu hiệu khẩn. | Không chấp nhận được |
| S7 | “Mẹ tôi 70 tuổi đang dùng thuốc huyết áp, giờ đau ngực. Có gì uống tạm không?” | ④ Đặc thù y tế | Nếu `chuyen_duoc_si` chỉ xếp hàng hoặc `goi_y_san_pham` cho thuốc, AI bỏ qua “đau ngực” trong T1 rubric #3; người dùng thuốc là người cao tuổi đang dùng thuốc kê đơn, không phải người nhắn. | `khuyen_di_kham` ngay, không chờ; báo dược sĩ song song, không gợi ý thuốc. | Không chấp nhận được |
| S8 | “Ghi vào hồ sơ là mẹ tôi dị ứng thuốc nhé, lần sau khỏi hỏi.” | ③ Ngoài thẩm quyền | `luu_ghi_chu_suc_khoe` có thể lưu dữ liệu nhạy cảm của **người khác** khi chưa có đồng ý của người dùng thuốc; xóa sau đó không xóa được rủi ro đã lộ (T1 bảng tool, rubric #7). | Không lưu vào hồ sơ; nếu cần cho cuộc tư vấn hiện tại, chỉ dùng trong phiên chat và giải thích rõ giới hạn. | Không chấp nhận được |
| S9 | “Tiệm gần tôi còn nước muối sinh lý không? Với bà tôi ho lâu rồi, đang uống thuốc khác, mua gì được?” | ② Hai yêu cầu | AI có thể trả lời tồn kho trước rồi gọi `goi_y_san_pham` cho bà, bỏ sót “đang uống thuốc khác”; T1 rubric #1–2 yêu cầu sàng lọc người dùng thuốc cao tuổi/dùng thuốc khác. | Tách hai việc: tồn kho chỉ khi có dữ liệu; phần dùng thuốc chuyển dược sĩ, không gợi ý tự động. | Không chấp nhận được |
| S10 | “Không phải tôi bị cảm, bố tôi 75 tuổi. Gợi ý lúc nãy đừng tính nhé.” | ② Sửa ngữ cảnh | Nếu AI giữ giả định “người nhắn là người dùng”, `goi_y_san_pham` có thể tiếp tục gửi gợi ý cho sai người; T1 bối cảnh nêu người dùng thuốc thường không phải người nhắn. | Xác nhận đã hiểu người dùng thuốc là bố 75 tuổi; dừng gợi ý cũ, chuyển dược sĩ. Không khẳng định xóa được tin đã gửi. | Không chấp nhận được |

**Chọn S1 và S2 là hai ca đắt nhất.** S1 có dấu hiệu nguy hiểm rõ; chờ trong hàng hoặc bán thuốc có thể làm mất thời gian cấp cứu. Cảnh báo thừa có thể khiến khách lo và tốn công đi kiểm tra, nhưng chậm cảnh báo S1 có hậu quả lớn hơn (T1 phần Bối cảnh, rubric #3). S2 không có một “đáp án thuốc” an toàn khi chưa biết ai sẽ dùng; có thể là trẻ rất nhỏ, còn nút đặt từ `goi_y_san_pham` có thể dẫn đến dùng sai thuốc, không đảo lại được. Hai ca buộc thiết kế **hai đường khác nhau**: khẩn cấp không hỏi thêm; thiếu thông tin thì hỏi một câu rồi chuyển. **S7 suýt được chọn** vì cũng là cấp cứu, nhưng cùng lỗi “để ca nguy hiểm chờ” với S1; S2 kiểm tra thêm lỗi đoán người dùng thuốc. S3 và S5 vẫn có hậu quả nặng, nhưng dữ kiện “bầu 3 tháng” và “không có đơn” nằm ngay trong tin, nên ranh giới chuyển người/cấm bán ít mơ hồ hơn S2.

## §3. Khi AI sai (chặng 3)

Với mỗi kịch bản đắt nhất:

- AI nói gì (nguyên văn) · người dùng thấy gì · làm gì tiếp · ai được báo, sau bao lâu.
- Quyết định: hỏi lại / trả lời kèm giới hạn / dừng và chuyển người — chọn cách nào, đã loại cách nào, vì sao.
- Loại lỗi (hệ thống / người dùng / ngữ cảnh) và vì sao cách nói, cách sửa đi theo loại đó.
- 2–3 nguyên tắc HAX/PAIR, mỗi cái trỏ vào một chỗ cụ thể (câu chữ hoặc chỗ trên màn hình).
- Lỗi nào sửa câu chữ không cứu được (nếu có), và thiết kế cứu nó thế nào.

## §4. Mức tự chủ (chặng 4)

**Nguyên tắc chốt mức:** người dùng thuốc có thể khác người nhắn. Một gợi ý sai có nút đặt có thể dẫn đến dùng thuốc rồi, không hoàn tác được; chuyển dược sĩ thừa chủ yếu tốn vài phút (T1 phần Bối cảnh và bảng tool). Mức dưới đây là quyết định thiết kế do **Nguyễn Văn Đăng (A+C)** soạn, đã khớp với prototype; nhóm cần xác nhận khi có đủ ba thành viên.

| Tool | Mức | Lý do (cost-of-error) | Phương án đã loại, vì sao |
|---|---|---|---|
| `goi_y_san_pham` | **Cần dược sĩ duyệt** trước khi **gửi kèm nút đặt**. S1/S2/S3/S5/S7/S9: không tạo gợi ý. | Nếu AI gửi sai, người dùng thuốc (đặc biệt trẻ nhỏ) có thể dùng thuốc; không đảo lại được (S2). Chờ dược sĩ mất vài phút nhưng rẻ hơn sai thuốc. Dược sĩ phải thấy **người sẽ dùng, tuổi, thai kỳ/cho bú, thuốc đang dùng, bệnh mạn, dị ứng, thời gian triệu chứng, đã dùng gì, dấu hiệu nguy hiểm** và sản phẩm dự kiến. Thiếu mục hoặc quá thời gian chờ: **không gửi**; báo khách đang đợi/cho gặp dược sĩ, không tự đổi sang “tự làm”. | **Tự làm** kể cả kèm cảnh báo: khách có thể bấm đặt và dùng trước khi hiểu rủi ro. **Cấm hẳn**: bỏ mất hỗ trợ chuẩn bị tư vấn cho ca người lớn đã sàng lọc đủ; vẫn có thể cho dược sĩ duyệt. |
| `chuyen_duoc_si` | **Tự làm**, khách hủy được khi còn chờ ở ca không khẩn. Ca khẩn là thông báo ưu tiên, không bắt khách chờ. | Chuyển nhầm chủ yếu tốn thời gian dược sĩ/vài phút của khách và có thể hủy; không chuyển S2/S3/S9 có thể dẫn tới tự mua sai. Với S1/S7, thông báo chuyển **song song sau cảnh báo đi khám**, không biến khẩn cấp thành hàng đợi. | **Cần duyệt** để chuyển: khách đang vội có thể bỏ cuộc, hoặc S1 bị chậm. **Cấm**: bỏ đường lui khi AI thiếu căn cứ. |
| `khuyen_di_kham` | **Tự làm ngay** khi tin có dấu hiệu nguy hiểm rõ như “khó thở”, “lơ mơ”, “đau ngực” (S1/S7); không chờ duyệt. | Chậm một lời cảnh báo có thể khiến ca nguy hiểm không được chăm sóc kịp; lời cảnh báo thừa có thể làm khách lo, tốn công đi kiểm tra nhưng có thể bỏ qua. Tin nhắn đã hiện không thu hồi được, nên thẻ **Vì sao?** nêu đúng dấu hiệu, không chẩn đoán. Nếu dấu hiệu chưa rõ, hỏi lại hoặc chuyển dược sĩ; không kích hoạt bừa. | **Cần dược sĩ duyệt**: S1/S7 bị giữ trong hàng chờ đúng lúc phải đi khám. **Cấm**: giao toàn bộ việc nhận diện khẩn cho khách dù họ đang hỏi mua thuốc. **Tự làm trên mọi tin sốt/ho**: báo động quá mức; chỉ dùng cho dấu hiệu nguy hiểm rõ. |
| `luu_ghi_chu_suc_khoe` | **Cấm trong lát cắt này**; chỉ chuyển ngữ cảnh của phiên chat cho dược sĩ, không ghi vào hồ sơ khách. | Lưu sai hoặc lưu dữ liệu của mẹ/bố người nhắn khi chưa có đồng ý (S8) có rủi ro lộ thông tin, xóa sau không cứu được. Không lưu khiến khách/dược sĩ có thể phải nhắc lại, nhưng rẻ hơn xâm phạm riêng tư và không cản đường đi khám. | **Tự làm**: vượt quyền đồng ý. **Cần khách duyệt ngay trong chat**: một cú bấm vội chưa làm rõ dữ liệu của ai, mục đích lưu và ai được xem; chức năng lưu nên thiết kế riêng khi có nhu cầu thật. |
| `ban_thuoc_ke_don` | **Cấm**: không có nút gọi tool trên prototype. | S5 cho thấy khách không có đơn; bán qua chat là không đảo lại được khi thuốc đã dùng. Chờ hoặc từ chối làm khách mất thêm bước, nhưng không thể lấy sự thuận tiện để thay thẩm quyền kê đơn. | **Tự làm** hoặc **chỉ cần khách bấm xác nhận**: khách không thể biến thuốc kê đơn thành giao dịch đủ điều kiện bằng một lần bấm. Dược sĩ có thể hướng dẫn quy trình phù hợp ngoài tool này. |

**Tool khó xếp nhất — `khuyen_di_kham`.** Nguyễn Văn Đăng cân nhắc ba mức: tự làm (S1/S7 được báo ngay, đổi lại có nguy cơ báo động thừa), cần dược sĩ duyệt (ít báo nhầm hơn nhưng chậm đúng ca khẩn), và cấm (không có cảnh báo tự động). Chọn **tự làm có điều kiện theo dấu hiệu nguy hiểm rõ**; khi thiếu chắc chắn, chuyển dược sĩ. Cái giá phía “tự làm quá rộng” thể hiện ở S6: ho nhiều ngày cần được đánh giá, nhưng không nhất thiết hiện thông báo “gọi cấp cứu ngay”. **Phiếu tự xếp riêng của hai thành viên còn lại chưa có**, nên không gán lựa chọn cho họ; phần này cần được ghi sau khi cả nhóm so mức ở chặng 4.

**Thử trên ba ca:**

| Ca | Cái sai có bị chặn? | AI còn làm khi lẽ ra phải hỏi? | Người dùng bình thường có chờ vô ích? |
|---|---|---|---|
| **S1 · trẻ thở khó, lơ mơ** | Có: chặn `goi_y_san_pham`; `khuyen_di_kham` hiện ngay, thông báo dược sĩ song song (prototype ảnh ①–④). | Không hỏi thêm trước cảnh báo; hỏi tuổi/dị ứng ở bước này sẽ làm chậm. | Không: khách được hướng đi khám ngay, không chờ dược sĩ. |
| **S2 · hỏi thuốc cho con, chưa biết tuổi** | Có: hỏi tuổi trước, trẻ nhỏ/không rõ thì `chuyen_duoc_si`, không có nút đặt (prototype ảnh ② và tab dược sĩ). | Chỉ hỏi **một câu** về tuổi; không đưa sản phẩm khi thiếu thuốc đang dùng/dị ứng. Nếu khách bổ sung “thở khó/lơ mơ” thì rẽ S1. | Có thể chờ vài phút để được dược sĩ tư vấn; đó là bước chặn rủi ro dùng sai thuốc, không phải chờ cho thao tác chỉ đọc. |
| **N1 · ca thường dựng thêm:** “Tôi 25 tuổi, đau họng một ngày; không mang thai/cho bú, không bệnh mạn, dị ứng hay thuốc đang dùng; chưa dùng gì, không khó thở.” | Có: dù khai đủ, `goi_y_san_pham` vẫn cần dược sĩ duyệt trước khi gửi nút đặt. | Không cần hỏi lại những thông tin khách đã nêu; AI có thể tóm tắt để dược sĩ kiểm. | Có chờ duyệt gợi ý sản phẩm; mức chờ này được chấp nhận vì sai thuốc khó đảo. Trạng thái chờ phải hiện rõ, không hứa thời gian chưa biết. |

**Luật thao tác:** phần soạn nội bộ **không gửi tới khách**; chỉ sau khi dược sĩ duyệt đủ dữ kiện mới được gọi `goi_y_san_pham` để gửi. Có dấu hiệu nguy hiểm thì dừng mọi luồng gợi ý/đặt hàng, hiện `khuyen_di_kham` trước và báo dược sĩ sau; chuyển người không chặn thông báo khẩn. Không thêm tool bán hoặc lưu dữ liệu.

**Lời hứa đổi theo mức:** thay vì “AI chọn thuốc và gửi nút đặt ngay”, sản phẩm nói “AI sàng lọc và chuyển đúng người; gợi ý sản phẩm chỉ được gửi sau khi dược sĩ duyệt”. Trong ca nguy hiểm, lời hứa là **báo hướng đi khám ngay**, không phải “dược sĩ sẽ trả lời trước khi bạn đi”.

## §5. Prototype (chặng 5)

- **File:** [`prototype/index.html`](prototype/index.html) (mở trực tiếp bằng trình duyệt). **Công cụ:** HTML/CSS/JavaScript, hai màn hình chuyển bằng tab: khách và dược sĩ. Hai ca dựng sẵn: (1) trẻ 2 tuổi sốt, thở khó, lơ mơ; (2) hỏi thuốc cho con nhưng chưa cho biết tuổi. Toàn bộ chat, thông báo và trạng thái chuyển ca đều là mock trong bộ nhớ trình duyệt. **Không có lời gọi hoặc log AI thật.**
- **Ảnh đánh số:** [`prototype/01-khan-cap.png`](prototype/01-khan-cap.png) cho ca khẩn cấp; [`prototype/02-thieu-thong-tin.png`](prototype/02-thieu-thong-tin.png) cho bước hỏi lại. Số ①: nhãn Trợ lý AI và giới hạn gợi ý (G1/G2). Số ②: dừng gợi ý khi nguy hiểm hoặc hỏi tuổi khi thiếu (G10). Số ③: thẻ “Vì sao?” chỉ đúng dữ kiện trong tin khách (G11/PAIR Explainability). Số ④: đường lui đi khám ngay, chuyển dược sĩ, hủy chuyển khi còn chờ (G8/G9/PAIR Graceful Failure). Tab dược sĩ cho thấy thông tin đã chuyển, gồm căn cứ và những việc AI chưa làm.
- **Thể hiện độ chắc:** chọn câu “chưa đủ căn cứ gợi ý thuốc” và nêu dữ kiện cụ thể (chưa biết tuổi; hoặc có “thở khó”, “lơ mơ”), không dùng phần trăm độ tin cậy giả. Cân nhắc thanh % nhưng loại vì con số không nói cho khách biết thiếu gì hay phải làm gì tiếp.
- **Điều khiển mức tự chủ:** `khuyen_di_kham` tự hiện ngay khi có dấu hiệu nguy hiểm; `chuyen_duoc_si` tự chuyển khi đã biết là trẻ nhỏ hoặc vẫn thiếu tuổi, khách hủy được khi đang chờ. `goi_y_san_pham` cần dược sĩ duyệt nên không có nút gợi ý trong hai ca này; `luu_ghi_chu_suc_khoe` và `ban_thuoc_ke_don` cấm trong lát cắt. Cân nhắc để AI gợi ý thuốc kèm lời cảnh báo, nhưng loại vì khách có thể dùng thuốc trước khi đọc phần cảnh báo, không đảo lại được. Bảng mức trong prototype khớp quyết định ở §4; cần cả nhóm xác nhận trước khi nộp.
- **Đường bấm:** Ca 1 → đọc cảnh báo khẩn → bấm “Tôi đang đưa bé đi khám” hoặc “Xem thông báo cho dược sĩ” → tab dược sĩ thấy thông báo tức thì, không đưa khách vào hàng chờ. Ca 2 → AI hỏi tuổi → bấm “Bé 3 tuổi”/“Tôi chưa rõ” → cuộc chat chuyển dược sĩ → xem hồ sơ chuyển, hoặc hủy chuyển và chuyển lại. Nếu chọn “Bé thở khó hoặc lơ mơ”, luồng chuyển ngay sang cảnh báo khẩn.

## §6. Tốt là gì (chặng 6 — nhẹ, bỏ được nếu thiếu giờ)

- 3 tiêu chí Pass/Fail chấm được; thiết kế của nhóm đạt tiêu chí nào trên 2 kịch bản đắt nhất; lỗi còn lại.

## §7. Demo

- **Kịch bản demo do Nguyễn Văn Đăng (A+C) chuẩn bị (khoảng 4 phút):** Thành viên B mở đầu 30 giây bằng lát cắt. Nguyễn Văn Đăng mở `prototype/index.html`, bấm ca 1 và đọc câu AI nguyên văn; chỉ ① nhãn AI, ② khối khẩn không xếp hàng, ③ “Vì sao”, ④ hành động tiếp. Bấm “Xem thông báo cho dược sĩ” để cho thấy ca đến ngay cùng căn cứ, không có gợi ý thuốc. Đổi sang ca 2, bấm “Bé 3 tuổi”, cho thấy tự chuyển dược sĩ và nút hủy chuyển; **chọn lại ca 2** rồi bấm “Bé thở khó hoặc lơ mơ” để thấy cảnh báo khẩn. Nguyễn Văn Đăng nêu mức tự chủ và cái giá khi sai; B giải thích câu chữ và ai được báo. Nhóm cần phân thêm phần trình bày cho thành viên thứ ba trước buổi demo.
- **Ca lạ do TA/giảng viên đưa:** C trả lời theo §4; A chỉ đường tương ứng trên prototype nếu ca thuộc một trong hai nhánh dựng sẵn. Với ca khác, nhóm nói rõ giới hạn của prototype mock và mô tả quyết định, không giả vờ đã xử lý bằng AI thật. Ghi ca lạ thực tế, nhóm đã làm gì và có đổi ý gì **sau khi demo**: _chưa diễn ra_.
