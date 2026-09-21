# Nền: Hardware

> Thiết kế mạch, vẽ PCB, đặt sản xuất, hàn, đo. Làm ra cái board vật lý mà mọi nền khác chạy trên đó.

---

## Nghề này là gì, hợp với ai

Bạn biến một ý tưởng thành tấm mạch có thật: chọn linh kiện, vẽ sơ đồ nguyên lý, đi dây, gửi xưởng sản xuất, hàn, đo, và làm cho nó chạy.

Đây là nghề **cho sản phẩm cầm được trên tay** — vừa là điểm hấp dẫn, vừa là lý do phải review kỹ: board sai thì phải sửa thủ công hoặc đặt lại, tốn tiền và thời gian.

**Hợp nếu** bạn thích nhìn thấy thứ mình làm tồn tại trong thế giới thật, cẩn thận, và chịu được việc kiểm tra đi kiểm tra lại trước khi bấm nút đặt hàng.

**Nếu bạn quen sửa nhanh rồi chạy lại**, bạn sẽ cần tập thói quen kiểm tra theo checklist trước khi cấp nguồn hoặc đặt sản xuất. Đây là kỹ năng rèn được, không phải tố chất bẩm sinh.

**Điều kiện vào:** xong [Nền chung](00-ban-dang-o-dau.md#nền-chung--ai-cũng-phải-có). Nghề này cần ít lập trình hơn hai nền kia, nhưng vẫn phải đọc được code C để biết board mình vẽ sẽ được điều khiển thế nào.

---

## Không biết học ở đâu? AI là cộng sự của bạn

Nhìn bốn chặng ở dưới thấy nản là chuyện bình thường. **Không ai học hết một lúc, và bạn không cần đợi ai rảnh để được chỉ.**

Cách dùng: lấy **một dòng** trong bảng, đưa cho AI, rồi hỏi. Ví dụ:

> *"Giải thích tụ decoupling cho người mới: nó làm gì, vì sao phải đặt sát chân chip?"*
>
> *"Tôi muốn học thiết kế mạch nguồn. Chia nhỏ thành các bước, mỗi bước là một bài tôi làm được trong một buổi."*
>
> *"Đây là datasheet con [tên linh kiện]. Giải thích giúp tôi bảng thông số trang này đang nói gì."*

Câu cuối là cách dùng AI tốt nhất trong nghề này: **nhờ nó đọc datasheet cùng bạn**, thay vì hỏi nó thông số. Con số vẫn phải lấy từ datasheet — xem [nguyên tắc chung](00-ban-dang-o-dau.md#dùng-ai-làm-cộng-sự).

Mentor dành thời gian cho những chỗ bạn đã thử mà vẫn tắc, và cho việc review trước khi bạn đặt board. Còn phần "cái này là gì, học thế nào" thì AI làm được ngay bây giờ.

---

## Phải học gì

### Chặng 1 — Nền điện tử

Không có phần này thì mọi thứ phía sau chỉ là vẽ hình.

| Chủ đề | Cần hiểu gì |
|--------|-------------|
| **Số học, đại số, đơn vị đo** | Đổi đơn vị, biến đổi công thức, đọc đồ thị; giải tích học thêm khi bài toán cần |
| **Nguyên lý mạch điện** | Định luật Ohm, dòng và áp, nối tiếp song song |
| **Điện tử cơ bản** | Điện trở, tụ, cuộn cảm, diode, transistor làm gì trong mạch |
| **Thiết kế số** | Cổng logic, mức logic, tín hiệu số |
| **Kiến trúc máy tính** | Con chip trên board bạn vẽ hoạt động ra sao |

### Chặng 2 — Đo và làm mẫu thử

Chặng biến bạn từ người học lý thuyết thành người làm được việc.

| Chủ đề | Làm được gì |
|--------|-------------|
| **Đồng hồ vạn năng** | Đo thông mạch, đo áp, tìm chỗ chập. Dụng cụ đầu tiên phải thạo |
| **Breadboard** | Dựng mạch thử trước khi vẽ PCB |
| **Hàn tay** | Chân cắm trước, rồi tới linh kiện dán. Bắt buộc, không né được |
| **Sửa chữa, câu dây** | Board về có lỗi thì cắt đường mạch và câu lại — ai cũng phải làm ít nhất một lần |
| **Oscilloscope** | Nhìn tín hiệu thật theo thời gian, khi đồng hồ vạn năng không đủ |
| **Logic / Protocol Analyzer** | Soi dữ liệu đang chạy trên dây I2C, SPI, UART |

> Hai dụng cụ cuối phân biệt "đoán xem sao nó không chạy" với "nhìn thấy vì sao nó không chạy". Đừng bỏ qua vì nghĩ chúng cao siêu.

### Chặng 3 — Giao tiếp giữa các thiết bị

Không cần lập trình chúng, nhưng phải hiểu để vẽ mạch đúng: **UART**, **I2C**, **SPI**, **USB**.

Cụ thể: mỗi giao thức cần mấy dây, có cần điện trở kéo lên không, dây dài tối đa bao nhiêu, đi gần nguồn nhiễu thì sao.

### Chặng 4 — Thiết kế PCB

**Nghề chính** của nền này. Mọi chặng trước là chuẩn bị cho chặng này.

| Chủ đề | Làm được gì |
|--------|-------------|
| **Phần mềm EDA** | Thạo một phần mềm — KiCad, Altium hoặc EasyEDA. Hỏi mentor CLB đang dùng gì |
| **Sơ đồ nguyên lý** | Vẽ đúng, đặt tên rõ, chạy ERC sạch lỗi |
| **Thiết kế nguồn** | LDO và buck khác nhau thế nào, chọn loại nào cho tải nào, tính nhiệt và dòng |
| **Layout PCB** | Bắt đầu với board 2 lớp: mặt phẳng đất, đường nguồn, tụ decoupling. Lên nhiều lớp khi có lý do rõ |
| **EMC — nhiễu điện từ** | Quan trọng với drone: ESC đóng cắt dòng lớn ngay cạnh mạch cảm biến |
| **Chọn linh kiện, làm BOM** | Kiểm tra tồn kho nhà phân phối, tìm linh kiện thay thế |
| **Xuất file sản xuất** | Gerber, và đọc quy tắc sản xuất của xưởng bạn định đặt |
| **Mạch bảo vệ** | Chống cắm ngược cực, chống quá áp, cầu chì |

**Quy tắc sống còn:** mọi giá trị linh kiện phải tra từ datasheet. Không suy từ tên linh kiện, không lấy từ mạch mẫu trên mạng mà không hiểu vì sao. Một con tụ sai giá trị có thể làm cả board mất ổn định theo cách rất khó tìm ra.

---

## Bài đầu tiên — 1 đến 2 buổi

Dùng nguồn thấp áp 3,3 V hoặc 5 V do CLB cấp, dựng mạch LED có điện trở hạn dòng trên breadboard. Tính dòng dự kiến, nhờ người phụ trách kiểm tra cách mắc **trước khi** cấp nguồn, rồi đo điện áp và so với tính toán.

Không dùng điện lưới, chưa cần vẽ PCB. Mục tiêu là tập quy trình: tính → lắp khi chưa cấp nguồn → kiểm tra → cấp nguồn → đo → giải thích chênh lệch.

---

## Tự chấm: bạn đã có nền chưa

> **Thiết kế một mạch nguồn nhỏ, từ đầu đến hồ sơ sản xuất.**
>
> Ví dụ hạ áp từ pin xuống mức nuôi vi điều khiển. Vẽ sơ đồ nguyên lý và layout hoàn chỉnh, chạy ERC và DRC sạch lỗi, xuất được Gerber.
>
> Nộp kèm: file dự án, ảnh sơ đồ và layout, và **bảng ghi rõ mỗi giá trị linh kiện dựa trên trang nào của datasheet nào**.
>
> Chưa cần đặt sản xuất. Cần đúng, giải thích được từng lựa chọn, và được người có kinh nghiệm review trước khi đặt board thật.

Bảng cuối được chấm kỹ nhất. Một layout đẹp mà các con số lấy từ suy đoán vẫn có thể chạy sai, mất ổn định hoặc làm hỏng linh kiện.

---

## Tài nguyên

- [Tài liệu KiCad](https://docs.kicad.org/) — EDA mã nguồn mở, miễn phí, đủ sức làm board thật. Hiện chỉ có tiếng Anh
- **Datasheet của mọi linh kiện bạn đặt lên board.** Không có ngoại lệ
- **Quy tắc sản xuất của xưởng bạn định đặt** — mỗi xưởng có giới hạn khác nhau về độ rộng đường mạch, khoảng cách, lỗ khoan. Vẽ xong mới đọc là quá muộn

**Dùng ở mảng:** cả ba — mọi mảng đều cần board. Xem [Ba mảng sản phẩm](ba-mang-san-pham.md).

**Thị trường tuyển gì:** tìm tin *Hardware Engineer*, *PCB Design*, *Electronics Engineer*; chú ý yêu cầu lặp lại về công cụ EDA, nguồn, EMC, thiết bị đo. Cách làm ở [README](../README.md#học-tới-đâu-thì-thị-trường-nhận).

**Mentor phụ trách:** `<cần điền>`
