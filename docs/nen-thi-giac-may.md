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

## Hợp với bạn nếu

- Bạn thích Python, và sẵn sàng học C++ khi cần tối ưu tốc độ
- Bạn thích bài toán "làm sao cho nó chạy nổi trên phần cứng yếu" hơn là "làm sao cho chỉ số đẹp hơn"
- Bạn chịu được việc thứ chạy mượt trên laptop lại chạy như rùa trên board nhúng

**Không hợp nếu** bạn chỉ muốn làm AI thuần. Ở CLB này, model không gắn lên thiết bị được thì chưa tính là xong.

---

## Điều kiện vào

Xong [Nền chung](00-ban-dang-o-dau.md#nền-chung--ai-cũng-phải-có), đặc biệt là **Linux/SSH** và **Python**. Bạn sẽ sống trên dòng lệnh của board nhúng.


---

## Phải học gì

### Chặng 1 — Làm chủ board nhúng

Trước khi nói tới AI, bạn phải điều khiển được cái máy sẽ chạy nó.

- Cài đặt và làm chủ một board nhúng (Raspberry Pi — CLB đã có repo hướng dẫn set up Pi 5)
- SSH vào board, làm việc hoàn toàn qua dòng lệnh, không cắm màn hình
- Quản lý môi trường Python, cài thư viện, xử lý khi phiên bản xung đột
- Hiểu tài nguyên board: bao nhiêu bộ nhớ, nóng tới đâu thì chậm lại, nguồn điện có đủ không

### Chặng 2 — Xử lý ảnh, chưa cần AI

Rất nhiều bài toán thật giải được ở chặng này mà không cần model nào. Đừng bỏ qua.

| Chủ đề | Bạn cần làm được gì |
|--------|---------------------|
| Lấy khung hình từ camera | Ổn định, liên tục, không rớt hình |
| Không gian màu và lọc ngưỡng | Tách vật thể theo màu |
| Tìm đường viền, tìm hình dạng | Xác định vị trí vật thể |
| Phát hiện marker | Cách đơn giản và rất đáng tin để định vị |
| **Đo tốc độ khung hình thật** | Và biết chỗ nào đang làm chậm |

**Bài tập nhỏ rất có ích:** phát hiện một vật màu rõ ràng, in ra toạ độ tâm theo thời gian thực. Nghe đơn giản, nhưng làm cho nó chạy ổn định ở tốc độ cao thì không đơn giản chút nào.

### Chặng 3 — Model học sâu trên board nhúng

| Chủ đề | Bạn cần làm được gì |
|--------|---------------------|
| Huấn luyện hoặc tinh chỉnh model phát hiện vật thể | Trên dữ liệu của CLB, không phải dữ liệu mẫu |
| **Tối ưu cho nhúng** | Lượng tử hoá model, chuyển sang định dạng chạy nhanh trên phần cứng đích |
| Dùng bộ tăng tốc phần cứng | Nếu CLB có |
| **Đo và so sánh** | Model gốc so với model đã tối ưu: nhanh hơn bao nhiêu, mất bao nhiêu độ chính xác |

Phần tối ưu là **cốt lõi của nền này**. Đây là chỗ bạn tạo ra giá trị mà người chỉ biết train model không tạo ra được.

### Chặng 4 — Biến kết quả thành hành động

Đây là chặng nối nền của bạn với phần còn lại của CLB. Không có chặng này thì bạn chỉ đang làm xử lý ảnh, không phải làm thiết bị.

- Chuyển từ toạ độ pixel trên ảnh sang hướng trong không gian thật
- Giao tiếp xuống vi điều khiển hoặc flight controller để gửi lệnh
- Bám mục tiêu ổn định qua các khung hình, xử lý khi mục tiêu bị che khuất tạm thời
- **Xử lý khi hỏng:** model nhận nhầm thì sao, camera mất tín hiệu thì sao, xử lý chậm quá thì sao

> **Quy tắc tuyệt đối:** mọi hành vi tự động phải chạy đúng trong mô phỏng trước khi đụng tới thiết bị thật. Không ai được thử code tự động lần đầu trên drone thật. Hệ thống phải luôn có đường lui về chế độ an toàn — không bao giờ được bay mù.

---

## Bài đầu tiên — 1 đến 2 buổi

Trên laptop, mở camera bằng Python, hiển thị độ phân giải và đo tốc độ khung hình trong ít nhất một phút. Sau đó thay đổi độ phân giải và ghi lại tốc độ thay đổi thế nào.

Chưa cần AI và chưa cần board nhúng. Mục tiêu là làm quen với camera, đo đạc và log; khi chuyển sang board, bạn đã có số liệu trên laptop để so sánh.

---

## Tự chấm: bạn đã có nền chưa

> **Bám một vật thể, trên board nhúng, đo được tốc độ thật.**
>
> Trên Raspberry Pi hoặc board CLB có, viết chương trình đọc camera thời gian thực, phát hiện một vật thể, in ra toạ độ tâm cùng **tốc độ khung hình đo được** ở mỗi khung.
>
> Cần có: code, video màn hình chạy thật trên board, và một đoạn ghi rõ **tốc độ khung hình đo được là bao nhiêu, nút thắt cổ chai nằm ở đâu, và bạn biết điều đó bằng cách nào**.

Phần cuối là phần quan trọng nhất. Nó phân biệt người chạy được code mẫu với người hiểu hệ thống mình đang chạy.

Chú ý: bài này **không yêu cầu dùng AI**. Làm bằng xử lý ảnh thông thường là đạt. Nếu bạn thấy bất ngờ vì điều đó, hãy đọc lại đoạn đầu file.

---

## Nền này dùng ở mảng nào

- **AIoT** — camera tự nhận diện tại chỗ, không cần gửi ảnh lên server
- **UAV** — bám mục tiêu, hạ cánh chính xác, bay dựa trên thị giác khi tín hiệu vệ tinh yếu

Chi tiết: [Ba mảng sản phẩm](ba-mang-san-pham.md)

---

## Tài nguyên

- **Tài liệu chính thức của thư viện thị giác và framework suy luận bạn dùng** — đọc đúng bản của phiên bản bạn cài
- [MAVLink Developer Guide](https://mavlink.io/en/) — nếu bạn đi vào mảng UAV. Đây là thứ nối nền của bạn với con drone. Không học phần này thì bạn chỉ đang làm xử lý ảnh
- [PX4 Autopilot Documentation](https://docs.px4.io/main/en/) — mục *Development*, đọc về cách máy tính phụ ghép vào hệ thống bay
- Repo `a.i-set-up-pi5` của CLB — hướng dẫn set up Pi 5

---

## Học tới đâu thì thị trường nhận

Tìm 5–10 tin có **Edge AI**, **Computer Vision**, **Robotics** hoặc **Embedded Linux** gần đây từ nhiều nguồn. Ghi lại các yêu cầu lặp lại về Linux, C/C++, Python, camera, tối ưu suy luận và đo hiệu năng. [Nhóm tuyển dụng lập trình nhúng](https://web.facebook.com/groups/775890384111054) là một nguồn tham khảo.

Bạn thường sẽ thấy kỹ năng triển khai hệ thống xuất hiện song song với kỹ năng học máy. Đó là lý do file này yêu cầu làm chủ board và camera, không chỉ model.

---
