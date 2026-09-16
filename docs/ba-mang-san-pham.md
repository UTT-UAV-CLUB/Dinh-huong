# Ba mảng sản phẩm

Nền là **nghề của bạn**. Mảng là **sản phẩm CLB làm ra**. File này nói mỗi mảng cần nền nào, và bạn sẽ làm gì ở đó.

Đọc file này để chọn nền theo sản phẩm bạn thấy hấp dẫn — hoặc để biết nền mình đang học sẽ dùng vào việc gì.

---

## Bản đồ nhanh

| | Firmware STM32 | ESP32 & Kết nối | Hardware | Thị giác máy |
|---|:---:|:---:|:---:|:---:|
| **UAV** | Chính | Phụ | Chính | Chính |
| **IoT** | Phụ | Chính | Chính | — |
| **AIoT** | — | Chính | Phụ | Chính |

*Chính = nền cốt lõi của mảng. Phụ = có dùng nhưng không bắt buộc.*

---

## Mảng UAV — Máy bay không người lái

### Sản phẩm

Drone bay được thật: tự giữ thăng bằng, bay theo lộ trình đặt trước, và ở mức cao hơn là tự nhận diện, tự bám mục tiêu, tự hạ cánh chính xác.

### Các phần ghép lại thế nào

```
        ┌─────────────────────────────────┐
        │   Camera + Board nhúng          │  ← Thị giác máy
        │   Nhận diện → ra quyết định     │
        └───────────────┬─────────────────┘
                        │  lệnh điều khiển (MAVLink)
                        ▼
        ┌─────────────────────────────────┐
        │   Flight Controller (STM32)     │  ← Firmware STM32
        │   Giữ thăng bằng, chạy động cơ  │
        └───────────────┬─────────────────┘
                        │  tín hiệu điện
                        ▼
        ┌─────────────────────────────────┐
        │   Mạch nguồn, ESC, khung bay    │  ← Hardware
        └─────────────────────────────────┘
```

### Bạn làm gì ở đây

| Nền | Việc cụ thể |
|-----|-------------|
| **Firmware STM32** | Driver cảm biến, vòng điều khiển ổn định, tích hợp ArduPilot/PX4, xử lý failsafe |
| **Hardware** | Mạch nguồn, mạch điều khiển, chống nhiễu từ ESC và tích hợp điện–cơ chịu rung |
| **Thị giác máy** | Bám mục tiêu, hạ cánh chính xác, bay theo thị giác khi tín hiệu vệ tinh yếu |
| **ESP32 & Kết nối** | Truyền dữ liệu từ drone về trạm mặt đất |

### Đặc thù phải biết trước

Đây là mảng có rủi ro vật lý cao nhất trong ba mảng và hoạt động bay chịu quản lý pháp luật.

- Cánh quạt quay ở tốc độ đủ để gây thương tích nặng
- Pin LiPo hỏng có thể cháy, sinh khói độc và tái bùng phát
- Bay không phép là vi phạm pháp luật, không phải "nghịch dại"

**Bắt buộc đọc trước khi tham gia:** [An toàn & pháp lý](an-toan-va-phap-ly.md).

Quy tắc dành cho thành viên mới rất đơn giản: **không tự ý cấp nguồn động cơ có gắn cánh và không tự mang drone đi bay**. Người phụ trách phải kiểm tra các yêu cầu hiện hành về đăng ký, tình trạng kỹ thuật, người điều khiển và cấp phép bay cùng nhà trường trước mỗi hoạt động.

Thiết kế khung và cơ khí là một chuyên môn riêng chưa có lộ trình đầy đủ trong repo này. Thành viên Hardware vẫn cần hiểu tích hợp cơ khí, nhưng không nên mặc định một người mới phải tự làm cả PCB lẫn toàn bộ khung bay.

---

## Mảng IoT — Thiết bị kết nối

### Sản phẩm

Thiết bị đo một thứ gì đó ngoài đời thật rồi đưa số liệu về nơi cần dùng: đo môi trường, giám sát thiết bị, điều khiển từ xa, ...

### Các phần ghép lại thế nào

```
   ┌──────────────┐    ┌──────────────┐    ┌──────────────┐
   │  Cảm biến    │───▶│    ESP32     │───▶│   Server     │
   │  (đo đạc)    │    │ (đọc + gửi)  │    │ (lưu + hiện) │
   └──────────────┘    └──────────────┘    └──────────────┘
          ▲                    ▲                    │
          │                    │                    ▼
     ┌────┴────────────────────┴────┐        ┌──────────────┐
     │  Board do mình thiết kế      │        │  Điện thoại  │
     └──────────────────────────────┘        └──────────────┘
```

### Bạn làm gì ở đây

| Nền | Việc cụ thể |
|-----|-------------|
| **ESP32 & Kết nối** | Đọc cảm biến, kết nối Wi-Fi hoặc mạng di động, gửi dữ liệu qua MQTT, xử lý mất kết nối |
| **Hardware** | Board thiết bị, mạch nguồn tiết kiệm điện để chạy pin lâu, vỏ chịu được môi trường đặt |
| **Firmware STM32** | Khi thiết bị cần tiết kiệm điện tối đa hoặc phản ứng thời gian thực |

### Vì sao nên bắt đầu ở đây nếu bạn chưa biết chọn gì

Mảng này thường có vòng phản hồi ngắn: đọc cảm biến, gửi dữ liệu và nhìn thấy kết quả từ sớm. Vì vậy nó phù hợp để thử nếu bạn chưa biết mình thích firmware, mạng hay phần cứng hơn.

Nó cũng an toàn hơn UAV nhiều — không có gì bay, không có cánh quạt. Và kỹ năng học được ở đây chuyển sang hai mảng kia rất dễ.

---

## Mảng AIoT — Thiết bị tự xử lý

### Sản phẩm

Thiết bị IoT nhưng **tự nhận diện, tự quyết định tại chỗ**, không cần gửi dữ liệu thô lên server rồi chờ trả lời.

Ví dụ: camera đếm số lượng ngay trên thiết bị và chỉ gửi con số về, thay vì gửi cả luồng video.

### Vì sao phải xử lý tại chỗ

Đây là lý do tồn tại của cả mảng, nên cần hiểu rõ:

- **Băng thông** — gửi cả luồng video liên tục thì tốn mạng và tốn tiền
- **Độ trễ** — chờ server trả lời thì quá chậm cho thứ cần phản ứng ngay
- **Hoạt động độc lập** — mất mạng thì thiết bị vẫn phải làm việc
- **Riêng tư** — dữ liệu hình ảnh không rời khỏi thiết bị

### Bạn làm gì ở đây

| Nền | Việc cụ thể |
|-----|-------------|
| **Thị giác máy** | Model nhận diện chạy trên board nhúng, tối ưu cho đủ nhanh |
| **ESP32 & Kết nối** | Gửi kết quả đã xử lý lên mạng, nhận lệnh cấu hình từ xa |
| **Hardware** | Board mang board nhúng và camera, tản nhiệt, cấp nguồn đủ |

### Đặc thù phải biết trước

Đây là mảng **dễ đánh giá sai công sức nhất**. Việc chạy được model trên laptop mất một buổi; việc làm cho nó chạy đủ nhanh trên board nhúng, ổn định suốt nhiều ngày, có thể mất vài tháng.

Nếu bạn vào mảng này, hãy chuẩn bị tinh thần rằng **phần lớn thời gian của bạn sẽ dành cho tối ưu và xử lý lỗi**, không phải cho phần AI.

---

## Chọn thế nào

**Nếu bạn chưa biết gì và muốn thử:** bắt đầu bằng một bài **IoT** nhỏ. Kết quả dễ quan sát, rủi ro thấp hơn UAV, và nhiều kỹ năng chuyển sang mảng khác được.

**Nếu bạn thích phần cứng, thích cầm mỏ hàn:** nền **Hardware**. Nó dùng được ở cả ba mảng, nên bạn không sợ chọn sai.

**Nếu bạn thích làm việc sát phần cứng, thời gian thực và debug tới từng bit:** thử nền **Firmware STM32**. Đường vào thường dốc hơn và kết quả ít trực quan, nhưng kỹ năng dùng được trong nhiều ngành embedded.

**Nếu bạn thích dữ liệu, thích ảnh:** nền **Thị giác máy** — nhưng đọc kỹ đoạn đầu của [file nền đó](nen-thi-giac-may.md) trước, vì nó không giống thứ phần lớn người mới tưởng tượng.

Và nhớ: lựa chọn đầu tiên chỉ là một phép thử. Hãy làm một bài nhỏ, ghi lại phần mình thích và phần làm mình mệt, rồi mới quyết định đi sâu hay đổi hướng.
