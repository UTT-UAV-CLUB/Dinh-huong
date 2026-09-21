# Nền: Thị giác máy nhúng

> Cho máy "nhìn". Chạy model thị giác trên board nhúng, đủ nhanh để dùng được thật.

---

## Đọc đoạn này trước, nó tiết kiệm thời gian cho cả hai bên

Nền này bị hiểu nhầm nhiều nhất. Phần lớn người mới nghe chữ "AI" rồi nghĩ tới một thứ, trong khi CLB đang làm một thứ khác hẳn. Nên phải nói thật rõ sự khác nhau đó ngay từ đầu.

### Hai kiểu công việc thường bị gọi chung là "AI"

| | **AI chạy trên máy chủ / đám mây** | **Thị giác máy nhúng — hướng ở CLB** |
|---|---|---|
| **Chạy ở đâu** | Trên máy chủ mạnh hoặc dịch vụ đám mây | Trên board nhỏ gắn ngay trên thiết bị, chạy bằng pin |
| **Sức tính toán** | Có thể mở rộng nhưng phải trả chi phí và chấp nhận độ trễ mạng | Cố định, hạn chế; quá nhiệt còn có thể làm giảm tốc độ |
| **Đầu vào** | Thường có thể xử lý tập trung trước khi suy luận | Hình từ camera thực tế có thể rung, ngược sáng, mờ hoặc lệch góc |
| **Đầu ra** | Một câu trả lời, một con số, một đoạn văn | Một **hành động vật lý**: drone bay lệch trái, van đóng lại, còi kêu |
| **Thế nào là thành công** | Chất lượng đầu ra, chi phí và độ trễ dịch vụ đạt yêu cầu | Đủ chính xác **và** đủ nhanh **và** đủ ổn định trong giới hạn điện, nhiệt và bộ nhớ |
| **Khi có lỗi** | Thường dễ ghi log, cập nhật tập trung hoặc thử lại; mức hậu quả vẫn tùy ứng dụng | Có thể tác động ngay tới thiết bị vật lý nên cần trạng thái an toàn |
| **Thời gian dồn vào đâu** | Dữ liệu, model và vận hành dịch vụ | Camera, tối ưu tốc độ, xử lý lỗi và ghép với phần cứng |

Hai bên có nhiều kỹ năng chung về dữ liệu và học máy, nhưng tiêu chí hoàn thành khác nhau. Ở nền này, model phải trở thành một phần đáng tin cậy của thiết bị thật.

### Cụ thể hơn

**Nền này KHÔNG phải:**

- **LLM, chatbot, AI tạo sinh.** Một số kỹ năng Python, triển khai và tối ưu có thể dùng chung, nhưng đây không phải trọng tâm của nền này.
- **Chỉ train model rồi dừng ở một chỉ số.** Độ chính xác, tốc độ, độ trễ, bộ nhớ và mức tiêu thụ điện phải được đánh giá cùng nhau theo yêu cầu của sản phẩm.
- **Nghiên cứu kiến trúc mạng nơ-ron mới ngay từ đầu.** Thành viên thường bắt đầu từ kiến trúc có sẵn, tinh chỉnh bằng dữ liệu của CLB rồi tập trung vào đánh giá và triển khai.

**Nền này LÀ:**

- Chạy model thị giác **trên board nhúng (VD: Pi 5, K230) gắn ngay trên thiết bị**, với điện năng và sức tính toán hạn chế
- Giữ đủ tốc độ khung hình để thiết bị phản ứng kịp lúc
- Lấy được hình ảnh dùng được từ camera gắn trên vật đang rung, đang di chuyển
- Và quan trọng nhất: **biến kết quả nhận diện thành một hành động thật**

### Điều khiến nhiều người bất ngờ

Cái khó của nền này **không chỉ nằm ở model**. Chọn, huấn luyện và đánh giá model vẫn cần làm nghiêm túc; phần triển khai lên thiết bị mới là nơi xuất hiện thêm nhiều ràng buộc.

Có ba nhóm khó khăn nghiêng nhiều về kỹ thuật hệ thống nhúng:

1. **Làm cho nó chạy nổi trên phần cứng yếu.** Thứ chạy mượt trên laptop có thể chậm hơn nhiều lần trên board nhúng.
2. **Làm cho nó chạy ổn định lâu dài.** Chạy tốt 5 phút thì dễ. Chạy tốt 5 ngày liên tục ngoài trời là chuyện khác hẳn.
3. **Làm cho thiết bị thật sự hành động theo nó.** Từ một khung màu trên ảnh tới một lệnh gửi xuống flight controller là cả một quãng đường.

**Nói gọn: nếu model của bạn chính xác 99% nhưng chạy quá chậm để thiết bị dùng được, bạn chưa làm xong việc.**

Nếu phần mô tả này khác điều bạn đang tìm, hãy quay lại [ba mảng sản phẩm](ba-mang-san-pham.md) và thử nền khác. Đổi hướng sau khi hiểu công việc rõ hơn là bình thường. Nếu đây đúng là bài toán bạn thích, hãy đọc tiếp.


---

## Hợp với ai, cần gì trước

**Hợp nếu** bạn thích Python và sẵn sàng học C++ khi cần tối ưu tốc độ, thích bài toán "làm sao cho nó chạy nổi trên phần cứng yếu" hơn là "làm sao cho chỉ số đẹp hơn", và chịu được việc thứ chạy mượt trên laptop lại bò trên board nhúng.

**Điều kiện vào:** xong [Nền chung](00-ban-dang-o-dau.md#nền-chung--ai-cũng-phải-có), đặc biệt **Linux/SSH** và **Python** — bạn sẽ sống trên dòng lệnh của board. Toán cần dùng: đại số tuyến tính cơ bản, ma trận và biến đổi toạ độ; học dần trong lúc làm cũng được.

---

## Chưa có board? Tập Linux trên WSL trước

Máy Windows, chưa mượn được Pi hay K230? Cài **WSL** với Ubuntu — có môi trường Linux thật ngay trên máy mình, không cần cài song song hệ điều hành.

Làm được: quen dòng lệnh, quản lý môi trường Python, cài thư viện xử lý ảnh, chạy thử code trên ảnh và video có sẵn. Gần hết Chặng 2 học được theo cách này.

Nhưng **WSL không phải board nhúng.** Máy bạn mạnh hơn Pi nhiều lần, nên tốc độ khung hình đo trên đó **không nói lên điều gì** về tốc độ thật trên thiết bị. Camera, GPIO và bộ tăng tốc phần cứng cũng không có ở đây.

WSL dạy bạn **cách làm**. Chỉ board thật trả lời được câu hỏi trọng tâm của nền này — *nó có chạy đủ nhanh không*. Hỏi CLB mượn board sớm.

---

## Không biết học ở đâu? AI là cộng sự của bạn

Nhìn bốn chặng ở dưới thấy nản là chuyện bình thường. **Không ai học hết một lúc, và bạn không cần đợi ai rảnh để được chỉ.**

Cách dùng: lấy **một dòng** trong bảng, đưa cho AI, rồi hỏi. Ví dụ:

> *"Giải thích không gian màu HSV cho người mới, vì sao tách vật theo màu thì dùng nó chứ không dùng RGB?"*
>
> *"Tôi muốn đo FPS trong vòng lặp đọc camera bằng Python. Viết ví dụ nhỏ nhất và giải thích từng dòng."*
>
> *"Chương trình của tôi chạy 5 FPS trên Pi. Gợi ý những chỗ có thể đang làm chậm và cách kiểm tra từng chỗ."*

Riêng nền này có một lưu ý: AI quen với code chạy trên máy mạnh, nên giải pháp nó đưa ra có thể quá nặng cho board nhúng. Cách kiểm tra luôn giống nhau và chỉ bạn làm được — **đo FPS trên board thật**.

Hãy bắt AI **giải thích và chia nhỏ**, đừng chỉ xin code — xem [nguyên tắc chung](00-ban-dang-o-dau.md#dùng-ai-làm-cộng-sự).

Mentor dành thời gian cho những chỗ bạn đã thử mà vẫn tắc. Còn phần "cái này là gì, học thế nào" thì AI làm được ngay bây giờ.

---

## Phải học gì

### Chặng 1 — Làm chủ board nhúng

Trước khi nói tới AI, phải điều khiển được cái máy sẽ chạy nó.

- Cài đặt và làm chủ một board nhúng (CLB đã có repo hướng dẫn set up Pi 5)
- SSH vào board, làm việc hoàn toàn qua dòng lệnh, không cắm màn hình
- Quản lý môi trường Python, xử lý khi phiên bản thư viện xung đột
- Hiểu tài nguyên board: bao nhiêu bộ nhớ, nóng tới đâu thì chậm lại, nguồn có đủ không

### Chặng 2 — Xử lý ảnh, chưa cần AI

Rất nhiều bài toán thật giải được ở chặng này mà không cần model nào. Đừng bỏ qua.

| Chủ đề | Làm được gì |
|--------|-------------|
| Lấy khung hình từ camera | Ổn định, liên tục, không rớt hình |
| Không gian màu, lọc ngưỡng | Tách vật thể theo màu |
| Tìm đường viền, hình dạng | Xác định vị trí vật thể |
| Phát hiện marker | Cách đơn giản và đáng tin để định vị |
| **Đo tốc độ khung hình thật** | Và biết chỗ nào đang làm chậm |

**Bài tập nhỏ rất có ích:** phát hiện một vật màu rõ, in toạ độ tâm theo thời gian thực. Nghe đơn giản, nhưng chạy ổn định ở tốc độ cao thì không.

### Chặng 3 — Model học sâu trên board nhúng

| Chủ đề | Làm được gì |
|--------|-------------|
| Huấn luyện hoặc tinh chỉnh model phát hiện vật thể | Trên dữ liệu của CLB, không phải dữ liệu mẫu |
| **Tối ưu cho nhúng** | Lượng tử hoá, chuyển sang định dạng chạy nhanh trên phần cứng đích |
| Bộ tăng tốc phần cứng | Nếu CLB có |
| **Đo và so sánh** | Model gốc và model đã tối ưu: nhanh hơn bao nhiêu, mất bao nhiêu độ chính xác |

Phần tối ưu là **cốt lõi của nền này** — chỗ bạn tạo ra giá trị mà người chỉ biết train model không tạo ra được.

### Chặng 4 — Biến kết quả thành hành động

Chặng nối nền của bạn với phần còn lại của CLB. Thiếu nó thì bạn chỉ đang làm xử lý ảnh.

- Chuyển toạ độ pixel trên ảnh sang hướng trong không gian thật
- Giao tiếp xuống vi điều khiển hoặc flight controller để gửi lệnh
- Bám mục tiêu ổn định qua các khung hình, xử lý khi mục tiêu bị che khuất
- **Xử lý khi hỏng:** model nhận nhầm, camera mất tín hiệu, xử lý chậm quá thì sao

> **Quy tắc tuyệt đối:** mọi hành vi tự động phải chạy đúng trong mô phỏng trước khi đụng tới thiết bị thật. Không ai thử code tự động lần đầu trên drone thật. Hệ thống phải luôn có đường lui về chế độ an toàn.

---

## Bài đầu tiên — 1 đến 2 buổi

Trên board CLB có: đọc camera và hiển thị khung hình, in ra tốc độ khung hình đo được. Ghi lại tên board, camera, và một lỗi bạn đã gặp.

Chưa cần model nào. Mục tiêu là đi trọn vòng: SSH vào board → chạy code → thấy hình → đo được tốc độ.

---

## Tự chấm: bạn đã có nền chưa

> **Bám một vật thể, trên board nhúng, đo được tốc độ thật.**
>
> Viết chương trình đọc camera thời gian thực, phát hiện một vật thể, in toạ độ tâm cùng **tốc độ khung hình đo được** ở mỗi khung.
>
> Nộp kèm: code, video màn hình chạy thật trên board, và đoạn ghi rõ **tốc độ đo được là bao nhiêu, nút thắt cổ chai ở đâu, và bạn biết điều đó bằng cách nào**.

Phần cuối quan trọng nhất — nó phân biệt người chạy được code mẫu với người hiểu hệ thống mình đang chạy.

Chú ý: bài này **không yêu cầu dùng AI**. Làm bằng xử lý ảnh thông thường là đạt. Thấy bất ngờ vì điều đó thì đọc lại đoạn đầu file.

---

## Tài nguyên

- **Tài liệu thư viện thị giác và framework suy luận bạn dùng** — đọc đúng bản của phiên bản bạn cài
- [MAVLink Developer Guide](https://mavlink.io/en/) — nếu đi vào mảng UAV. Đây là thứ nối nền của bạn với con drone
- Repo `a.i-set-up-pi5` của CLB — hướng dẫn set up Pi 5

**Dùng ở mảng:** AIoT (camera tự nhận diện tại chỗ), UAV (bám mục tiêu, hạ cánh chính xác) — xem [Ba mảng sản phẩm](ba-mang-san-pham.md).

**Thị trường tuyển gì:** tìm tin có *Edge AI*, *Computer Vision*, *Embedded Linux*. Bạn sẽ nhận ra phần lớn yêu cầu là **kỹ năng nhúng**, không phải kỹ năng AI — đó là lý do file này bắt làm chủ board trước khi chạm vào model. Cách làm ở [README](../README.md#học-tới-đâu-thì-thị-trường-nhận).

**Mentor phụ trách:** `<cần điền>`
