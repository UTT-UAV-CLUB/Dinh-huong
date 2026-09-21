# Nền: Firmware STM32

> Viết code chạy trực tiếp trên vi điều khiển.

---

## Nghề này là gì, hợp với ai

Bạn viết phần mềm điều khiển phần cứng ở mức thấp nhất — đọc cảm biến, chạy động cơ, xử lý đúng thời điểm tính bằng micro giây. Khi drone giữ được thăng bằng, đó là code của bạn đang chạy hàng trăm lần mỗi giây.

Kỹ năng này xuất hiện trong nhiều vị trí embedded: thiết bị công nghiệp, ô tô, IoT, UAV.

**Hợp nếu** bạn muốn biết máy móc chạy thế nào đến từng bit, chịu được việc code sai mà **không có thông báo lỗi nào** — chỉ là thiết bị nằm im, và đủ kiên nhẫn cho một lỗi thời điểm mất ba ngày mới tìm ra.

**Cân nhắc nếu** bạn cần kết quả đẹp mắt sớm. Thành công của firmware trông rất âm thầm: thiết bị chạy đúng lúc, không treo, xử lý lỗi an toàn.

**Điều kiện vào:** xong [Nền chung](00-ban-dang-o-dau.md#nền-chung--ai-cũng-phải-có), đặc biệt là **C**. Con trỏ và phép toán bit là bắt buộc — chưa vững thì củng cố trước hoặc học song song bằng bài nhỏ.

---

## Chưa có board? Bắt đầu trên trình mô phỏng

**[Wokwi](https://wokwi.com/stm32)** chạy thẳng trong trình duyệt, miễn phí cho cá nhân, có sẵn **STM32F103C8T6 (Blue Pill)** và vài board Nucleo. Nó mô phỏng ở mức firmware — bạn viết C thật, hoặc nạp thẳng file `.elf` đã build.

Dùng được tới đâu:

| | Ngoại vi |
|---|---|
| ✅ Đầy đủ | GPIO, USART, I2C, SPI, Timer (TIM1–4), EXTI, RCC, **GDB debugging** |
| 🟡 Một phần | ADC1 chỉ chuyển đổi cơ bản; ADC2 chưa có |
| ❌ Chưa có | **DMA**, IWDG, PWR, RTC |

Nghĩa là **Chặng 1 học được trọn vẹn**, Chặng 2 gần đủ. Có cả GDB, nên bạn tập debug được ngay cả khi chưa có mạch nạp — thứ thường bị hoãn lại vì thiếu thiết bị.

Nhưng **DMA ở Chặng 3 không mô phỏng được**, ADC chỉ ở mức cơ bản và không có RTC. Và trình mô phỏng không bao giờ tái hiện được nguồn chập chờn, nhiễu, hay dây tiếp xúc kém. **Bài tự chấm phải làm trên board thật.**

---

## Không biết học ở đâu? AI là cộng sự của bạn

Nhìn bảng ở dưới thấy nản là chuyện bình thường. **Không ai học hết cả bảng một lúc, và bạn không cần đợi ai rảnh để được chỉ.**

Cách dùng: lấy **một dòng** trong bảng, đưa cho AI, rồi hỏi. Ví dụ:

> *"Giải thích EXTI trên STM32F103 cho người mới bắt đầu. Cho tôi ví dụ nhỏ nhất chạy được, giải thích từng dòng."*
>
> *"Tôi đang học I2C. Chia nhỏ thành các bước, mỗi bước là một bài tập tôi làm được trong một buổi."*
>
> *"Code này báo lỗi [dán nguyên văn]. Giải thích lỗi nghĩa là gì và tôi nên kiểm tra gì trước."*

AI sẽ giải thích lại bao nhiêu lần cũng được, không bao giờ cáu, và trả lời lúc 2 giờ sáng. Hãy bắt nó **giải thích và chia nhỏ**, đừng chỉ xin code — xem [nguyên tắc chung](00-ban-dang-o-dau.md#dùng-ai-làm-cộng-sự).

Mentor dành thời gian cho những chỗ bạn đã thử mà vẫn tắc. Còn phần "cái này là gì, học thế nào" thì AI làm được ngay bây giờ.

---

## Phải học gì

### Chặng 1 — Làm cho con chip nghe lời

| Chủ đề | Làm được gì |
|--------|-------------|
| **GPIO** | Bật tắt chân, đọc nút bấm |
| **Clock Management** | Chip lấy nhịp từ đâu; cấu hình sai thì mọi thứ chạy sai tốc độ |
| **UART** | In thông tin ra máy tính — **công cụ debug quan trọng nhất** |
| **Interrupts** | Phản ứng với sự kiện, và vì sao không làm việc nặng trong hàm ngắt |
| **Timers / Counters** | Làm đúng việc vào đúng thời điểm |

Song song: cài toolchain, build và nạp được code xuống board. Mắc ở bước này là chuyện rất thường — lưu nguyên văn lỗi, phiên bản công cụ, tên board rồi hỏi.

**Kỹ năng ngầm quan trọng nhất:** mở datasheet, tìm đúng chương về ngoại vi cần dùng, đọc bảng thanh ghi. Đây là thứ phân biệt người làm firmware thật với người copy code mẫu.

### Chặng 2 — Nói chuyện với bên ngoài

| Chủ đề | Làm được gì |
|--------|-------------|
| **I2C** | Đọc cảm biến. Hiểu tín hiệu trên dây, không chỉ gọi thư viện |
| **SPI** | Giao tiếp nhanh hơn với cảm biến và bộ nhớ |
| **ADC / DAC** | Đọc tín hiệu tương tự: điện áp pin, cảm biến analog |
| **PWM** | Điều khiển động cơ, đèn, servo |
| **Watchdog** | Tự khởi động lại khi treo — thứ giữ thiết bị không chết giữa đường |

**Việc quan trọng nhất chặng này:** viết driver cho một cảm biến thật, đọc từ datasheet, không copy thư viện có sẵn.

### Chặng 3 — Chạy được lâu dài

| Chủ đề | Làm được gì |
|--------|-------------|
| **DMA** | Chuyển dữ liệu mà không chiếm CPU |
| **RTOS Basics** | Chia chương trình thành nhiều task có độ ưu tiên |
| **JTAG/SWD + GDB** | Dừng chương trình giữa chừng, xem từng biến. Khi in UART không còn đủ |
| **Xử lý lỗi, failsafe** | Mất tín hiệu, pin yếu, một cảm biến chết thì sao |

---

## Bài đầu tiên — 1 đến 2 buổi

Trên board CLB đang có: làm LED nhấp nháy và in một bộ đếm qua UART. Ghi lại tên board, công cụ build, cách nạp code, và một lỗi bạn đã gặp.

Mục tiêu không phải học hết STM32 — chỉ cần tự đi trọn vòng: sửa code → build → nạp → quan sát → sửa lỗi. Chưa có board thì hỏi mượn trước khi mua.

---

## Tự chấm: bạn đã có nền chưa

> **Đọc một cảm biến bằng driver do chính bạn viết.**
>
> Chọn một cảm biến CLB đang có, đọc datasheet, viết code C khởi tạo và đọc dữ liệu, in ra qua UART. **Không dùng thư viện driver có sẵn** — chỉ dùng hàm I2C/SPI mức thấp.
>
> Nộp kèm: code, ảnh hoặc video chạy thật, và đoạn ghi rõ **bạn lấy mỗi giá trị cấu hình từ trang nào của datasheet**.

Phần cuối được chấm kỹ nhất — nó chứng minh bạn tra tài liệu chứ không đoán.

---

## Tài nguyên

- **Datasheet và reference manual của con chip bạn dùng** — quan trọng nhất, và không ai đọc thay bạn được
- [ArduPilot Developer Docs](https://ardupilot.org/dev/) hoặc [PX4 Docs](https://docs.px4.io/main/en/) — nếu bạn đi vào mảng UAV

**Dùng ở mảng:** UAV (firmware điều khiển bay), IoT (thiết bị cần tiết kiệm điện hoặc phản ứng thời gian thực) — xem [Ba mảng sản phẩm](ba-mang-san-pham.md).

**Thị trường tuyển gì:** tìm tin *Embedded Software Engineer* / *Firmware Engineer*, xem yêu cầu lặp lại về vi điều khiển, RTOS, công cụ debug. Cách làm ở [README](../README.md#học-tới-đâu-thì-thị-trường-nhận).

