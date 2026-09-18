# Nền: ESP32 & Kết nối

> Đưa thiết bị lên mạng. Từ một cảm biến trên bàn tới một con số hiện trên điện thoại.

---

## Nghề này là gì

Bạn viết code trên vi điều khiển có sẵn Wi-Fi, đọc dữ liệu từ cảm biến, rồi đẩy nó lên mạng — tới server, tới điện thoại, tới nơi cần dùng. Và theo chiều ngược lại: nhận lệnh từ xa để điều khiển thiết bị.

Nền này có vòng phản hồi khá ngắn: bạn có thể đọc một cảm biến và xem dữ liệu trên điện thoại từ sớm. Vì vậy đây là một lựa chọn dễ thử nếu bạn chưa biết mình hợp với gì.

---

## Hợp với bạn nếu

- Bạn thích thấy hệ thống hoàn chỉnh chạy từ đầu đến cuối, không chỉ một mảnh
- Bạn muốn làm cả phần thiết bị lẫn phần mạng, không chỉ một bên
- Bạn chịu được những lỗi khó chịu kiểu "chạy được ở nhà nhưng lên trường thì mất kết nối"

---

## Điều kiện vào

Xong [Nền chung](00-ban-dang-o-dau.md#nền-chung--ai-cũng-phải-có).

Bạn có thể bắt đầu khi C mới ở mức cơ bản, rồi học tiếp trong lúc làm. Tuy vậy, càng đi sâu vào lỗi thời gian thực, bộ nhớ và driver, nền C vẫn càng quan trọng.

---

## Chưa có board? Bắt đầu trên trình mô phỏng

Không có board trong tay không phải lý do để ngồi chờ. Bạn có thể học gần hết Chặng 1 đến Chặng 3 trên **[Wokwi](https://wokwi.com)** — trình mô phỏng chạy thẳng trong trình duyệt, miễn phí cho cá nhân, không cần cài gì.

Điểm đáng dùng: Wokwi có ESP32, mô phỏng được **Wi-Fi và MQTT**, nên bạn dựng thử được gần đúng bài tự chấm ở dưới mà chưa cần mua linh kiện nào. Nối sai cũng không cháy gì, và chia sẻ bằng link để người khác xem code chạy.

Nhưng đừng dừng ở đó. Trình mô phỏng không tái hiện được thứ sẽ làm bạn mất nhiều thời gian nhất ngoài đời thật: nguồn điện chập chờn, Wi-Fi yếu lúc được lúc mất, cảm biến trả về số rác, dây tiếp xúc kém. **Dùng nó để học nhanh và thử ý tưởng, rồi chuyển sang board thật sớm nhất có thể** — bài tự chấm phải làm trên phần cứng thật.

---

## Phải học gì

### Chặng 1 — Làm chủ con chip

| Chủ đề | Bạn cần làm được gì |
|--------|---------------------|
| **GPIO** | Bật tắt chân, đọc nút bấm, điều khiển relay |
| **UART** | In thông tin ra máy tính để debug |
| **Interrupts** | Phản ứng với sự kiện bên ngoài |
| **Timers / Counters** | Đọc cảm biến theo chu kỳ đều đặn |
| **ADC** | Đọc cảm biến analog, đo điện áp pin |
| **DAC** | Tạo tín hiệu analog nếu đúng biến thể ESP32 có ngoại vi này; luôn kiểm tra datasheet |

### Chặng 2 — Đọc cảm biến

| Chủ đề | Bạn cần làm được gì |
|--------|---------------------|
| **I2C** | Giao thức phổ biến nhất để đọc cảm biến |
| **SPI** | Khi cần tốc độ cao hơn |
| **RTOS Basics** | ESP32 chạy sẵn hệ điều hành thời gian thực — bạn cần hiểu task và độ ưu tiên để chương trình không giật khi vừa đọc cảm biến vừa gửi mạng |

### Chặng 3 — Lên mạng

Đây là phần làm nên nghề này.

| Chủ đề | Bạn cần làm được gì |
|--------|---------------------|
| **Wi-Fi** | Kết nối, và **xử lý khi mất kết nối** — phần sau mới là phần khó |
| **TCP/IP, UDP** | Hiểu dữ liệu đi qua mạng thế nào, khi nào dùng cái nào |
| **MQTT** | Giao thức nhắn tin phổ biến nhất trong IoT: thiết bị gửi, server nhận, điện thoại xem |

### Chặng 4 — Khi Wi-Fi không tới được

Thiết bị đặt ngoài đồng, trên cột điện, trên xe đang chạy thì không có Wi-Fi. Lúc đó cần mạng di động:

| Chủ đề | Dùng khi nào |
|--------|--------------|
| **GSM / LTE** | Mạng di động thông thường, băng thông khá, tốn điện |
| **NB-IoT** | Thiết kế riêng cho thiết bị IoT: ít dữ liệu, rất tiết kiệm điện, phủ sóng sâu |
| **LTE-M (Cat-M1)** | IoT cần di động, băng thông và độ trễ cao hơn NB-IoT |
| **4G / 5G qua module ngoài** | Khi ứng dụng thực sự cần băng thông cao; đổi lại tốn điện và phức tạp hơn |

> **Cần tự kiểm chứng trước khi làm:** ESP32 có sẵn Wi-Fi, nhưng phần mạng di động thường phải dùng **module ngoài** nối vào chứ không tích hợp trong chip. Trước khi mua linh kiện hay thiết kế mạch, hãy mở datasheet của **đúng biến thể ESP32 CLB đang dùng** và xác nhận. Đừng tin trí nhớ của ai, kể cả của người viết file này.

---

## Bài đầu tiên — 1 đến 2 buổi

Cho board kết nối Wi-Fi và in địa chỉ IP cùng trạng thái kết nối qua UART. Sau đó tắt điểm phát Wi-Fi, bật lại và quan sát chương trình phản ứng ra sao.

Chưa cần cảm biến hay server. Mục tiêu là tự đi trọn vòng: sửa code → build → nạp → xem log → nhận ra mất kết nối. Hỏi CLB đang dùng biến thể ESP32 và framework nào trước khi cài công cụ hoặc mua board.

---

## Tự chấm: bạn đã có nền chưa

> **Một cảm biến, lên mạng, sống sót qua mất kết nối.**
>
> Đọc một cảm biến thật qua I2C, đẩy số đo lên server qua MQTT theo chu kỳ đều đặn, xem được từ máy khác hoặc điện thoại.
>
> Sau đó — phần quan trọng nhất — **rút Wi-Fi ra rồi cắm lại**. Thiết bị phải tự kết nối lại và tiếp tục gửi, không cần ai nhấn nút reset.
>
> Nộp kèm: code, video demo có cảnh ngắt và nối lại mạng, và một đoạn ghi rõ bạn xử lý mất kết nối bằng cách nào.

Phần ngắt và nối lại mạng giúp phân biệt một demo ngắn với thiết bị có thể vận hành lâu dài. Đây cũng là chỗ tốt để học retry, timeout, lưu tạm dữ liệu và quan sát trạng thái hệ thống.

---

## Nền này dùng ở mảng nào

- **IoT** — đây là nền chính của cả mảng
- **AIoT** — thiết bị vừa kết nối vừa tự xử lý
- **UAV** — truyền dữ liệu từ drone về trạm mặt đất

Chi tiết: [Ba mảng sản phẩm](ba-mang-san-pham.md)

---

## Tài nguyên

- **Datasheet và tài liệu kỹ thuật của đúng biến thể ESP32 bạn dùng** — các biến thể khác nhau khá nhiều về ngoại vi và khả năng kết nối
- Tài liệu chính thức của framework phát triển bạn chọn — đọc bản **đúng phiên bản bạn cài**, không đọc bản khác rồi thắc mắc sao hàm không tồn tại
- Tài liệu chính thức của giao thức MQTT và của server MQTT bạn dùng

---

## Học tới đâu thì thị trường nhận

Tìm 5–10 tin có chữ **IoT**, **Embedded** hoặc **Firmware** gần đây từ nhiều nguồn. Chú ý các giao thức, nền tảng đám mây và yêu cầu về độ ổn định được nhắc lặp lại; các công nghệ này thay đổi nhanh nên cần kiểm tra lại theo thời điểm. [Nhóm tuyển dụng lập trình nhúng](https://web.facebook.com/groups/775890384111054) là một nguồn tham khảo.
