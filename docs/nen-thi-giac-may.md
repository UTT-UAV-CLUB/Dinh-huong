# Nền: Thị giác máy nhúng

> Cho máy "nhìn". Chạy model thị giác trên board nhúng, đủ nhanh để dùng được thật.

---

## Đọc đoạn này trước, nó tiết kiệm thời gian cho cả hai bên

Nền này bị hiểu nhầm nhiều nhất, nên nói rõ ngay.

**KHÔNG phải:**
- LLM, chatbot, AI tạo sinh
- Train model trên dịch vụ đám mây rồi khoe chỉ số độ chính xác
- Nghiên cứu kiến trúc mạng nơ-ron mới

**LÀ:**
- Chạy model thị giác **trên board nhúng gắn ngay trên thiết bị**, với điện năng và sức tính toán hạn chế
- Giữ đủ tốc độ khung hình để thiết bị phản ứng kịp
- Lấy được hình ảnh dùng được từ camera gắn trên vật đang rung, đang di chuyển
- Và quan trọng nhất: **biến kết quả nhận diện thành một hành động thật**

Cái khó của nền này không nằm ở model. Model là phần dễ nhất, có sẵn đầy. Cái khó là làm cho nó chạy nổi trên phần cứng yếu, và làm cho thiết bị thật sự hành động theo nó.

**Nếu model của bạn chính xác 99% nhưng chạy quá chậm để thiết bị dùng được, bạn chưa làm xong việc.**

---

## Hợp với bạn nếu

- Bạn thích Python, và sẵn sàng học C++ khi cần tối ưu tốc độ
- Bạn thích bài toán "làm sao cho nó chạy nổi trên phần cứng yếu" hơn là "làm sao cho chỉ số đẹp hơn"
- Bạn chịu được việc thứ chạy mượt trên laptop lại chạy như rùa trên board nhúng

**Không hợp nếu** bạn chỉ muốn làm AI thuần. Ở CLB này, model không gắn lên thiết bị được thì chưa tính là xong.

---

## Điều kiện vào

Xong [Nền chung](00-ban-dang-o-dau.md#nền-chung--ai-cũng-phải-có), đặc biệt là **Linux/SSH** và **Python**. Bạn sẽ sống trên dòng lệnh của board nhúng.

Toán cần dùng: đại số tuyến tính cơ bản — ma trận, phép biến đổi toạ độ. Học dần trong lúc làm cũng được.

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

## Tự chấm: bạn đã có nền chưa

> **Bám một vật thể, trên board nhúng, đo được tốc độ thật.**
>
> Trên Raspberry Pi hoặc board CLB có, viết chương trình đọc camera thời gian thực, phát hiện một vật thể, in ra toạ độ tâm cùng **tốc độ khung hình đo được** ở mỗi khung.
>
> Nộp kèm: code, video màn hình chạy thật trên board, và một đoạn ghi rõ **tốc độ khung hình đo được là bao nhiêu, nút thắt cổ chai nằm ở đâu, và bạn biết điều đó bằng cách nào**.

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

Nền này ít tin tuyển thẳng hơn hai nền kia, nên đọc theo cách khác: vào [nhóm tuyển dụng lập trình nhúng](https://web.facebook.com/groups/775890384111054) tìm các tin có **Edge AI**, **Computer Vision** hoặc **Embedded Linux**.

Điều bạn sẽ nhận ra: phần lớn yêu cầu là **kỹ năng nhúng**, không phải kỹ năng AI. Đó là lý do file này bắt bạn làm chủ board trước khi chạm vào model.

---

## Mentor phụ trách

`<cần điền>`
