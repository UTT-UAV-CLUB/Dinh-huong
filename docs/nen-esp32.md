# Nền: ESP32 & Kết nối

> Đưa thiết bị lên mạng. Từ một cảm biến trên bàn tới một con số hiện trên điện thoại.

---

## Nghề này là gì, hợp với ai

Bạn viết code trên vi điều khiển có sẵn Wi-Fi: đọc cảm biến rồi đẩy dữ liệu lên mạng — tới server, tới điện thoại. Và chiều ngược lại, nhận lệnh từ xa để điều khiển thiết bị.

Nền này có vòng phản hồi ngắn: đọc được cảm biến và xem dữ liệu trên điện thoại từ khá sớm. Vì vậy đây là lựa chọn dễ thử nhất nếu bạn chưa biết mình hợp với gì.

**Hợp nếu** bạn thích thấy hệ thống chạy từ đầu đến cuối chứ không chỉ một mảnh, muốn làm cả phần thiết bị lẫn phần mạng, và chịu được lỗi kiểu "chạy ở nhà ngon mà lên trường mất kết nối".

**Điều kiện vào:** xong [Nền chung](00-ban-dang-o-dau.md#nền-chung--ai-cũng-phải-có). Bắt đầu được khi C mới ở mức cơ bản, học tiếp trong lúc làm — nhưng càng đi sâu vào lỗi thời gian thực và bộ nhớ, nền C càng quan trọng.

---

## Chưa có board? Bắt đầu trên trình mô phỏng

Không có board không phải lý do ngồi chờ. Học được gần hết Chặng 1–3 trên **[Wokwi](https://wokwi.com)** — chạy thẳng trong trình duyệt, miễn phí cho cá nhân, không cần cài gì.

Điểm đáng dùng: có ESP32, mô phỏng được cả **Wi-Fi và MQTT**, nên bạn dựng thử được gần đúng bài tự chấm ở dưới mà chưa cần mua linh kiện nào. Nối sai cũng không cháy gì.

Nhưng nó không tái hiện được thứ ngốn thời gian nhất ngoài đời thật: nguồn chập chờn, Wi-Fi lúc được lúc mất, cảm biến trả số rác, dây tiếp xúc kém. **Dùng để học nhanh, rồi chuyển sang board thật sớm nhất có thể** — bài tự chấm phải làm trên phần cứng thật.

---

## Không biết học ở đâu? AI là cộng sự của bạn

Nhìn bốn chặng ở dưới thấy nản là chuyện bình thường. **Không ai học hết một lúc, và bạn không cần đợi ai rảnh để được chỉ.**

Cách dùng: lấy **một dòng** trong bảng, đưa cho AI, rồi hỏi. Ví dụ:

> *"Giải thích MQTT cho người mới. Nó khác HTTP chỗ nào, vì sao IoT hay dùng nó?"*
>
> *"Tôi muốn ESP32 tự kết nối lại khi mất Wi-Fi. Chia nhỏ thành các bước, mỗi bước là một bài tôi làm được trong một buổi."*
>
> *"Code này báo lỗi [dán nguyên văn]. Giải thích lỗi nghĩa là gì và tôi nên kiểm tra gì trước."*

AI giải thích lại bao nhiêu lần cũng được, không bao giờ cáu, và trả lời lúc 2 giờ sáng. Hãy bắt nó **giải thích và chia nhỏ**, đừng chỉ xin code — xem [nguyên tắc chung](00-ban-dang-o-dau.md#dùng-ai-làm-cộng-sự).

Mentor dành thời gian cho những chỗ bạn đã thử mà vẫn tắc. Còn phần "cái này là gì, học thế nào" thì AI làm được ngay bây giờ.

---

## Phải học gì

### Chặng 1 — Làm chủ con chip

| Chủ đề | Làm được gì |
|--------|-------------|
| **GPIO** | Bật tắt chân, đọc nút bấm, điều khiển relay |
| **UART** | In thông tin ra máy tính để debug |
| **Interrupts** | Phản ứng với sự kiện bên ngoài |
| **Timers / Counters** | Đọc cảm biến theo chu kỳ đều |
| **ADC** | Đọc cảm biến analog, đo điện áp pin |
| **DAC** | Nếu đúng biến thể ESP32 của bạn có ngoại vi này — luôn kiểm tra datasheet |
| **Watchdog** | Tự khởi động lại khi treo. Thiết bị đặt ngoài không người trông thì gần như bắt buộc |

### Chặng 2 — Đọc cảm biến

| Chủ đề | Làm được gì |
|--------|-------------|
| **I2C** | Giao thức phổ biến nhất để đọc cảm biến |
| **SPI** | Khi cần tốc độ cao hơn |
| **RTOS Basics** | ESP32 chạy sẵn RTOS — hiểu task và độ ưu tiên để chương trình không giật khi vừa đọc cảm biến vừa gửi mạng |

### Chặng 3 — Lên mạng

Đây là phần làm nên nghề này.

| Chủ đề | Làm được gì |
|--------|-------------|
| **Wi-Fi** | Kết nối, và **xử lý khi mất kết nối** — phần sau mới khó |
| **TCP/IP, UDP** | Dữ liệu đi qua mạng thế nào, khi nào dùng cái nào |
| **MQTT** | Giao thức nhắn tin phổ biến nhất trong IoT |

### Chặng 4 — Khi Wi-Fi không tới được

Thiết bị đặt ngoài đồng, trên cột điện, trên xe chạy thì phải dùng mạng di động:

| Công nghệ | Dùng khi nào |
|--------|--------------|
| **GSM / LTE** | Mạng di động thông thường, băng thông khá, tốn điện |
| **NB-IoT** | Riêng cho IoT: ít dữ liệu, rất tiết kiệm điện, phủ sóng sâu |
| **LTE-M (Cat-M1)** | IoT cần di động, băng thông và độ trễ tốt hơn NB-IoT |
| **4G / 5G qua module ngoài** | Khi thật sự cần băng thông cao; đổi lại tốn điện và phức tạp |

> **Tự kiểm chứng trước khi làm:** ESP32 có sẵn Wi-Fi, nhưng phần mạng di động thường phải dùng **module ngoài** chứ không tích hợp trong chip. Trước khi mua linh kiện hay vẽ mạch, mở datasheet **đúng biến thể ESP32 CLB đang dùng** và xác nhận. Đừng tin trí nhớ của ai, kể cả người viết file này.

---

## Bài đầu tiên — 1 đến 2 buổi

Cho board kết nối Wi-Fi và in địa chỉ IP cùng trạng thái kết nối qua UART. Sau đó tắt điểm phát Wi-Fi, bật lại, quan sát chương trình phản ứng ra sao.

Chưa cần cảm biến hay server. Mục tiêu là tự đi trọn vòng: sửa code → build → nạp → xem log → nhận ra mất kết nối. Hỏi CLB đang dùng biến thể ESP32 và framework nào trước khi cài công cụ.

---

## Tự chấm: bạn đã có nền chưa

> **Một cảm biến, lên mạng, sống sót qua mất kết nối.**
>
> Đọc một cảm biến thật qua I2C, đẩy số đo lên server qua MQTT theo chu kỳ đều, xem được từ máy khác hoặc điện thoại.
>
> Rồi — phần quan trọng nhất — **rút Wi-Fi ra cắm lại**. Thiết bị phải tự kết nối lại và gửi tiếp, không cần ai nhấn reset.
>
> Nộp kèm: code, video có cảnh ngắt và nối lại mạng, và đoạn ghi rõ bạn xử lý mất kết nối bằng cách nào.

Phần ngắt và nối lại mạng phân biệt một demo ngắn với thiết bị vận hành được lâu dài. Đây cũng là chỗ học retry, timeout, lưu tạm dữ liệu.

---

## Tài nguyên

- **Datasheet của đúng biến thể ESP32 bạn dùng** — các biến thể khác nhau khá nhiều về ngoại vi và kết nối
- Tài liệu framework bạn chọn — đọc **đúng phiên bản bạn cài**
- Tài liệu MQTT và server MQTT bạn dùng

**Dùng ở mảng:** IoT (nền chính), AIoT, UAV (truyền dữ liệu về trạm mặt đất) — xem [Ba mảng sản phẩm](ba-mang-san-pham.md).

**Thị trường tuyển gì:** tìm tin có chữ *IoT*, *Embedded*, *Firmware*; chú ý giao thức và nền tảng đám mây được nhắc lặp lại. Cách làm ở [README](../README.md#học-tới-đâu-thì-thị-trường-nhận).

