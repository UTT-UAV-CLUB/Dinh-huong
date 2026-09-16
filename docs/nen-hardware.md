# Nền: Hardware

> Thiết kế mạch, vẽ PCB, đặt sản xuất, hàn, đo. Làm ra cái board vật lý mà mọi nền khác chạy trên đó.

---

## Nghề này là gì

Bạn biến một ý tưởng thành một tấm mạch có thật: chọn linh kiện, vẽ sơ đồ nguyên lý, đi dây, gửi xưởng sản xuất, hàn, đo, và làm cho nó chạy.

Đây là nghề **cho ra sản phẩm cầm được trên tay**. Vừa là điểm hấp dẫn, vừa là áp lực: board sai thì phải đặt lại, mất tiền và mất vài tuần chờ. Không có nút hoàn tác.

---

## Hợp với bạn nếu

- Bạn thích nhìn thấy thứ mình làm ra tồn tại trong thế giới thật
- Bạn cẩn thận, và chịu được việc kiểm tra đi kiểm tra lại trước khi bấm nút đặt hàng
- Bạn chấp nhận rằng một linh kiện đặt sai chân là hỏng cả board

**Không hợp nếu** bạn quen kiểu sửa nhanh, thử nhanh, sai thì chạy lại. Phần cứng không cho bạn cơ hội đó.

---

## Điều kiện vào

Xong [Nền chung](00-ban-dang-o-dau.md#nền-chung--ai-cũng-phải-có).

Nghề này cần ít lập trình hơn hai nền kia, nhưng bạn vẫn phải đọc được code C — để biết board mình vẽ sẽ được điều khiển thế nào, và để nói chuyện được với người viết firmware.

---

## Phải học gì

### Chặng 1 — Nền điện tử

Không có phần này thì mọi thứ phía sau chỉ là vẽ hình.

| Chủ đề | Bạn cần hiểu gì |
|--------|-----------------|
| **Toán và giải tích cơ bản** | Đủ để tính toán mạch, không cần hơn |
| **Nguyên lý mạch điện** | Định luật Ohm, dòng và áp, mạch nối tiếp song song |
| **Điện tử cơ bản** | Điện trở, tụ, cuộn cảm, diode, transistor làm gì trong mạch |
| **Thiết kế số** | Cổng logic, mức logic, tín hiệu số |
| **Kiến trúc máy tính** | Hiểu con chip trên board bạn vẽ hoạt động ra sao |

### Chặng 2 — Đo và làm mẫu thử

Đây là chặng biến bạn từ người học lý thuyết thành người làm được việc.

| Chủ đề | Bạn cần làm được gì |
|--------|---------------------|
| **Đồng hồ vạn năng** | Đo thông mạch, đo điện áp, tìm chỗ chập. Dụng cụ đầu tiên phải thành thạo |
| **Breadboard** | Dựng mạch thử trước khi vẽ PCB |
| **Hàn tay** | Linh kiện chân cắm trước, rồi tới linh kiện dán. Kỹ năng bắt buộc, không né được |
| **Sửa chữa, câu dây** | Board về có lỗi thì cắt đường mạch và câu lại — ai cũng phải làm việc này ít nhất một lần |
| **Oscilloscope** | Nhìn thấy tín hiệu thật theo thời gian. Khi đồng hồ vạn năng không đủ |
| **Logic / Protocol Analyzer** | Soi tín hiệu số: xem đúng dữ liệu gì đang chạy trên dây I2C, SPI, UART |

> Hai dụng cụ cuối là thứ phân biệt "đoán xem sao nó không chạy" với "nhìn thấy vì sao nó không chạy". Đừng bỏ qua vì nghĩ chúng cao siêu.

### Chặng 3 — Giao tiếp giữa các thiết bị

Bạn không cần lập trình chúng, nhưng phải hiểu để vẽ mạch đúng: **UART**, **I2C**, **SPI**, **USB**.

Cụ thể cần biết: mỗi giao thức cần bao nhiêu dây, có cần điện trở kéo lên không, dây dài tối đa bao nhiêu, đi dây gần nguồn nhiễu thì sao.

### Chặng 4 — Thiết kế PCB

Đây là **nghề chính** của nền này. Mọi chặng trước là chuẩn bị cho chặng này.

| Chủ đề | Bạn cần làm được gì |
|--------|---------------------|
| **Phần mềm EDA** | Dùng thành thạo một phần mềm — KiCad, Altium hoặc EasyEDA. Hỏi mentor CLB đang dùng gì |
| **Sơ đồ nguyên lý** | Vẽ đúng, đặt tên rõ, chạy kiểm tra ERC sạch lỗi |
| **Thiết kế nguồn** | LDO và mạch buck khác nhau thế nào, chọn loại nào cho tải nào, tính toán nhiệt và dòng |
| **Đi dây nhiều lớp** | Mặt phẳng đất, tách nguồn nhiễu, đặt tụ lọc đúng chỗ |
| **EMC — nhiễu điện từ** | Đặc biệt quan trọng với drone: ESC đóng cắt dòng lớn ngay cạnh mạch cảm biến |
| **Chọn linh kiện và làm BOM** | Kiểm tra tồn kho nhà phân phối, tìm linh kiện thay thế khi hết hàng |
| **Xuất file sản xuất** | Gerber, và đọc hiểu quy tắc sản xuất của xưởng bạn định đặt |
| **Mạch bảo vệ** | Chống cắm ngược cực, chống quá áp, cầu chì |

**Quy tắc sống còn của nghề này:** mọi giá trị linh kiện phải tra từ datasheet. Không suy ra từ tên linh kiện, không lấy từ mạch mẫu trên mạng mà không hiểu vì sao. Một con tụ sai giá trị có thể làm cả board mất ổn định theo cách rất khó tìm ra.

---

## Tự chấm: bạn đã có nền chưa

> **Thiết kế một mạch nguồn nhỏ, từ đầu đến hồ sơ sản xuất.**
>
> Chọn một mạch nguồn đơn giản — ví dụ hạ áp từ pin xuống mức nuôi vi điều khiển. Vẽ sơ đồ nguyên lý và layout hoàn chỉnh, chạy ERC và DRC sạch lỗi, xuất được file Gerber.
>
> Nộp kèm: file dự án, ảnh sơ đồ và layout, và một **bảng ghi rõ mỗi giá trị linh kiện bạn chọn dựa trên trang nào của datasheet nào**.
>
> Chưa cần đặt sản xuất. Cần đúng, và giải thích được từng lựa chọn.

Bảng cuối là phần được chấm kỹ nhất. Một layout đẹp mà các con số lấy từ suy đoán thì không dùng được — và không ai nhìn ra được điều đó cho tới khi board cháy.

---

## Nền này dùng ở mảng nào

Cả ba. Mọi mảng đều cần board.

- **UAV** — mạch nguồn, mạch điều khiển bay, tích hợp cơ khí chịu rung
- **IoT** — board thiết bị, mạch tiết kiệm điện chạy pin lâu
- **AIoT** — board mang board nhúng và camera

Chi tiết: [Ba mảng sản phẩm](ba-mang-san-pham.md)

---

## Tài nguyên

- [Tài liệu chính thức KiCad](https://docs.kicad.org/) — phần mềm EDA mã nguồn mở, miễn phí, đủ sức làm board thật. Hiện chỉ có tiếng Anh
- **Datasheet của mọi linh kiện bạn đặt lên board.** Không có ngoại lệ
- **Tài liệu quy tắc sản xuất của xưởng bạn định đặt** — mỗi xưởng có giới hạn khác nhau về độ rộng đường mạch, khoảng cách, kích thước lỗ khoan. Vẽ xong mới đọc là quá muộn
- [PX4 — phần Hardware](https://docs.px4.io/main/en/) — xem cách các flight controller thương mại được thiết kế và vì sao họ chọn như vậy

---

## Học tới đâu thì thị trường nhận

Vào [nhóm tuyển dụng lập trình nhúng](https://web.facebook.com/groups/775890384111054), tìm các tin tuyển **Hardware Engineer**, **PCB Design** hoặc **Electronics Engineer**. Chú ý xem họ yêu cầu phần mềm EDA nào và số lớp board bao nhiêu — đó là thước đo trình độ rõ nhất trong nghề này.

---

## Mentor phụ trách

`<cần điền>`
