# Ba mảng sản phẩm

Nền là **nghề của bạn**. Mảng là **sản phẩm CLB làm ra**. File này nói mỗi mảng cần nền nào và bạn sẽ làm gì ở đó.

---

## Bản đồ nhanh

| | Firmware STM32 | ESP32 & Kết nối | Hardware | Thị giác máy |
|---|:---:|:---:|:---:|:---:|
| **UAV** | Chính | Phụ | Chính | Chính |
| **IoT** | Phụ | Chính | Chính | — |
| **AIoT** | — | Chính | Phụ | Chính |

*Chính = nền cốt lõi. Phụ = có dùng nhưng không bắt buộc.*

---

## UAV — Máy bay không người lái

Drone bay được thật: tự giữ thăng bằng, bay theo lộ trình đặt trước, và ở mức cao hơn là tự nhận diện, tự bám mục tiêu, tự hạ cánh chính xác.

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

| Nền | Việc cụ thể |
|-----|-------------|
| **Firmware STM32** | Driver cảm biến, vòng điều khiển ổn định, tích hợp ArduPilot/PX4, xử lý failsafe |
| **Hardware** | Mạch nguồn, mạch điều khiển, chống nhiễu từ ESC, tích hợp điện–cơ chịu rung |
| **Thị giác máy** | Bám mục tiêu, hạ cánh chính xác, bay theo thị giác khi tín hiệu vệ tinh yếu |
| **ESP32 & Kết nối** | Truyền dữ liệu từ drone về trạm mặt đất |

### Phải biết trước khi tham gia

Đây là mảng có rủi ro vật lý cao nhất, và hoạt động bay chịu quản lý của pháp luật. Cánh quạt quay đủ nhanh để gây thương tích nặng; pin LiPo hỏng có thể cháy, sinh khói độc và tái bùng phát.

**Bắt buộc đọc:** [An toàn & pháp lý](an-toan-va-phap-ly.md).

Quy tắc cho thành viên mới rất đơn giản: **không tự ý cấp nguồn động cơ có gắn cánh, và không tự mang drone đi bay.** Người phụ trách phải làm việc với nhà trường về đăng ký, tình trạng kỹ thuật và cấp phép bay trước mỗi hoạt động.

*Ghi chú: thiết kế khung và cơ khí là chuyên môn riêng, chưa có lộ trình trong repo này. Thành viên Hardware cần hiểu tích hợp cơ khí, nhưng đừng mặc định một người mới phải tự làm cả PCB lẫn toàn bộ khung bay.*

---

## IoT — Thiết bị kết nối

Thiết bị đo một thứ gì đó ngoài đời thật rồi đưa số liệu về nơi cần dùng: đo môi trường, giám sát thiết bị, điều khiển từ xa.

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

| Nền | Việc cụ thể |
|-----|-------------|
| **ESP32 & Kết nối** | Đọc cảm biến, kết nối Wi-Fi hoặc mạng di động, gửi qua MQTT, xử lý mất kết nối |
| **Hardware** | Board thiết bị, mạch tiết kiệm điện để chạy pin lâu, vỏ chịu được môi trường đặt |
| **Firmware STM32** | Khi thiết bị cần tiết kiệm điện tối đa hoặc phản ứng thời gian thực |

**Vì sao nên bắt đầu ở đây nếu chưa biết chọn gì:** vòng phản hồi ngắn — đọc cảm biến, gửi dữ liệu, thấy kết quả sớm. An toàn hơn UAV nhiều, không có gì bay. Và kỹ năng chuyển sang hai mảng kia rất dễ.

---

## AIoT — Thiết bị tự xử lý

Thiết bị IoT nhưng **tự nhận diện, tự quyết định tại chỗ**, không gửi dữ liệu thô lên server rồi chờ trả lời. Ví dụ: camera đếm số lượng ngay trên thiết bị và chỉ gửi con số về, thay vì gửi cả luồng video.

**Vì sao phải xử lý tại chỗ** — đây là lý do tồn tại của cả mảng:

- **Băng thông** — gửi luồng video liên tục thì tốn mạng và tốn tiền
- **Độ trễ** — chờ server trả lời thì quá chậm cho thứ cần phản ứng ngay
- **Hoạt động độc lập** — mất mạng thì thiết bị vẫn phải làm việc
- **Riêng tư** — dữ liệu hình ảnh không rời khỏi thiết bị

| Nền | Việc cụ thể |
|-----|-------------|
| **Thị giác máy** | Model nhận diện chạy trên board nhúng, tối ưu cho đủ nhanh |
| **ESP32 & Kết nối** | Gửi kết quả đã xử lý lên mạng, nhận lệnh cấu hình từ xa |
| **Hardware** | Board mang board nhúng và camera, tản nhiệt, cấp nguồn đủ |

**Phải biết trước:** đây là mảng **dễ đánh giá sai công sức nhất**. Chạy được model trên laptop mất một buổi; làm cho nó chạy đủ nhanh trên board nhúng và ổn định suốt nhiều ngày có thể mất vài tháng. Phần lớn thời gian của bạn sẽ dành cho tối ưu và xử lý lỗi, không phải cho phần AI.

---

Chưa biết chọn nền nào? Xem phần chọn nền trong [Bạn đang ở đâu](00-ban-dang-o-dau.md). Và nhớ: lựa chọn đầu tiên chỉ là một phép thử — làm một bài nhỏ, ghi lại phần mình thích và phần làm mình mệt, rồi mới quyết định đi sâu hay đổi hướng.
