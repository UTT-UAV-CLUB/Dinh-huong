# Nền: Firmware STM32

> Viết code chạy trực tiếp trên vi điều khiển. Không có hệ điều hành đầy đủ, không có ai đỡ cho bạn.

---

## Nghề này là gì

Bạn viết phần mềm điều khiển phần cứng ở mức thấp nhất — đọc cảm biến, điều khiển động cơ, xử lý đúng thời điểm tính bằng micro giây. Khi con drone giữ được thăng bằng, đó là code của bạn đang chạy hàng trăm lần mỗi giây.

Đây là nghề **được trả lương cao và tuyển nhiều nhất** trong ba nền của CLB, vì ít người chịu được nó.

---

## Hợp với bạn nếu

- Bạn muốn biết máy móc hoạt động thế nào ở tầng thấp nhất, đến từng bit
- Bạn chịu được việc code sai mà **không có thông báo lỗi nào** — chỉ là thiết bị nằm im
- Bạn kiên nhẫn: một lỗi về thời điểm có thể mất ba ngày để tìm ra

**Không hợp nếu** bạn cần thấy kết quả đẹp mắt ngay. Firmware là nghề mà thành công trông giống như "không có gì xảy ra cả".

---

## Điều kiện vào

Xong [Nền chung](00-ban-dang-o-dau.md#nền-chung--ai-cũng-phải-có), đặc biệt là **C**.

Phần con trỏ và phép toán trên bit là bắt buộc, không né được. Nếu chưa vững, học C thêm hai tuần vẫn nhanh hơn là lao vào STM32 rồi mắc kẹt ở mọi thứ.

---

## Phải học gì

### Chặng 1 — Làm cho con chip nghe lời

| Chủ đề | Bạn cần làm được gì |
|--------|---------------------|
| **GPIO** | Bật tắt chân, đọc trạng thái nút bấm |
| **Clock Management** | Hiểu con chip lấy nhịp từ đâu, vì sao cấu hình sai thì mọi thứ chạy sai tốc độ |
| **UART** | In thông tin ra máy tính — **công cụ debug quan trọng nhất của bạn** |
| **Interrupts** | Phản ứng với sự kiện. Và hiểu vì sao không được làm việc nặng bên trong hàm ngắt |
| **Timers / Counters** | Làm đúng việc vào đúng thời điểm |

Song song: cài được toolchain, build được, nạp được chương trình xuống board. Nghe đơn giản nhưng đây là chỗ nhiều người bỏ cuộc — cứ kiên trì, ai cũng vượt qua.

**Kỹ năng ngầm quan trọng nhất của chặng này:** mở datasheet con chip, tìm đúng chương nói về ngoại vi bạn cần, đọc bảng thanh ghi. Đây là thứ phân biệt người làm firmware thật với người copy code mẫu.

### Chặng 2 — Nói chuyện với thế giới bên ngoài

| Chủ đề | Bạn cần làm được gì |
|--------|---------------------|
| **I2C** | Đọc cảm biến. Hiểu tín hiệu trên dây, không chỉ gọi thư viện |
| **SPI** | Giao tiếp nhanh hơn với cảm biến và bộ nhớ |
| **ADC / DAC** | Đọc tín hiệu tương tự: điện áp pin, cảm biến analog |
| **PWM** | Điều khiển động cơ, đèn, servo |
| **Watchdog** | Tự khởi động lại khi chương trình treo — thứ giữ cho thiết bị không chết giữa đường |

**Việc quan trọng nhất của chặng này:** viết driver cho một cảm biến thật, **đọc từ datasheet**, không copy thư viện có sẵn.

### Chặng 3 — Làm hệ thống chạy được lâu dài

| Chủ đề | Bạn cần làm được gì |
|--------|---------------------|
| **DMA** | Chuyển dữ liệu mà không chiếm CPU |
| **RTOS Basics** | Chia chương trình thành nhiều việc chạy song song, có độ ưu tiên |
| **Debug bằng JTAG/SWD + GDB** | Dừng chương trình giữa chừng, xem từng biến. Khi in ra UART không còn đủ |
| **Xử lý lỗi và failsafe** | Mất tín hiệu thì sao, pin yếu thì sao, một cảm biến chết thì sao |

---

## Tự chấm: bạn đã có nền chưa

> **Đọc một cảm biến bằng driver do chính bạn viết.**
>
> Chọn một cảm biến CLB đang có. Đọc datasheet của nó. Viết code C khởi tạo và đọc dữ liệu, in ra qua UART. **Không dùng thư viện driver có sẵn** — chỉ dùng hàm giao tiếp I2C hoặc SPI ở mức thấp.
>
> Nộp kèm: code, ảnh hoặc video dữ liệu chạy thật, và một đoạn ghi rõ **bạn lấy mỗi giá trị cấu hình từ trang nào của datasheet**.

Phần cuối là phần được chấm kỹ nhất. Nó chứng minh bạn tra tài liệu chứ không đoán.

Làm được bài này nghĩa là bạn có nền. Chưa làm được thì chưa có, dù đã xem bao nhiêu video.

---

## Nền này dùng ở mảng nào

- **UAV** — firmware điều khiển bay, driver cảm biến, giao tiếp với máy tính phụ
- **IoT** — vi điều khiển ở các thiết bị cần tiết kiệm điện hoặc phản ứng thời gian thực

Chi tiết: [Ba mảng sản phẩm](ba-mang-san-pham.md)

---

## Tài nguyên

Ít mà đọc kỹ, hơn nhiều mà lướt qua.

- **Datasheet và reference manual của con chip bạn đang dùng** — tài liệu quan trọng nhất, và là thứ duy nhất không ai đọc thay bạn được
- [ArduPilot Developer Documentation](https://ardupilot.org/dev/) — nếu bạn đi vào mảng UAV. Bắt đầu ở mục *Getting Started*
- [PX4 Autopilot Documentation](https://docs.px4.io/main/en/) — flight stack còn lại, mục *Development*

---

## Học tới đâu thì thị trường nhận

Vào [nhóm tuyển dụng lập trình nhúng](https://web.facebook.com/groups/775890384111054), tìm các tin tuyển **Embedded Software Engineer** hoặc **Firmware Engineer**. Đọc phần mô tả yêu cầu, liệt kê ra, đối chiếu với bảng ở trên.

Bạn sẽ thấy phần lớn yêu cầu trùng đúng với những gì trong file này. Đó là lý do file này được viết như vậy.

---

## Mentor phụ trách

`<cần điền>`
