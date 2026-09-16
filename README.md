# Định hướng — UTT UAV Club

> Câu lạc bộ nghiên cứu Máy bay không người lái
> Trường Đại học Công nghệ Giao thông Vận tải — Hà Nội

CLB làm ba mảng sản phẩm: **UAV**, **IoT** và **AIoT**. Tài liệu này nói rõ mỗi mảng cần cái nền gì, và bạn phải học gì để đi vào được.

---

## Nếu bạn mới vào CLB, đọc cái này trước

**→ [Bạn đang ở đâu](docs/00-ban-dang-o-dau.md)**

Đây là file quan trọng nhất trong repo. Nó trả lời câu hỏi mà hầu hết người mới đang hỏi sai cách: *"em muốn làm drone tự bay / làm AI nhận diện / làm nhà thông minh, em bắt đầu từ đâu?"*

Đọc xong file đó rồi hẵng hỏi. Không phải vì không được hỏi, mà vì sau khi đọc bạn sẽ hỏi được câu hỏi tốt hơn nhiều.

---

## Hai thứ khác nhau: NỀN và MẢNG

Đây là chỗ gây nhầm lẫn nhiều nhất, nên nói rõ ngay.

**NỀN** là nghề của bạn — bộ kỹ năng bạn xây trong nhiều năm.
**MẢNG** là sản phẩm CLB làm ra — nơi bạn đem nghề đó ra dùng.

Chúng cắt nhau, không thay thế nhau. Cùng một nghề firmware, đem sang UAV thì viết code điều khiển bay, đem sang IoT thì viết code node cảm biến. Cùng một nghề, hai sản phẩm khác hẳn.

### Bốn nền

| Nền | Bạn làm gì | Tài liệu |
|-----|------------|----------|
| **Firmware STM32** | Code chạy trực tiếp trên vi điều khiển, không có hệ điều hành đầy đủ. Điều khiển thời gian thực. | [nen-stm32.md](docs/nen-stm32.md) |
| **ESP32 & Kết nối** | Code trên chip có sẵn Wi-Fi. Đưa dữ liệu từ thiết bị lên mạng, lên server. | [nen-esp32.md](docs/nen-esp32.md) |
| **Hardware** | Thiết kế mạch, vẽ PCB, hàn, đo. Làm ra cái board vật lý. | [nen-hardware.md](docs/nen-hardware.md) |
| **Thị giác máy nhúng** | Cho máy "nhìn". Chạy model thị giác trên board nhúng, đủ nhanh để dùng thật. | [nen-thi-giac-may.md](docs/nen-thi-giac-may.md) |

Chọn **một** nền. Không ai giỏi cả bốn, và không ai cần bạn giỏi cả bốn.

### Ba mảng

| Mảng | Sản phẩm | Dùng nền nào |
|------|----------|--------------|
| **UAV** | Máy bay không người lái | Firmware STM32 + Hardware + Thị giác máy |
| **IoT** | Thiết bị đo, gửi dữ liệu lên mạng | ESP32 & Kết nối + Hardware |
| **AIoT** | Thiết bị IoT có khả năng tự xử lý, tự nhận diện | ESP32 & Kết nối + Thị giác máy |

Chi tiết từng mảng: **[Ba mảng sản phẩm](docs/ba-mang-san-pham.md)**

---

## Còn lại trong repo

| Tài liệu | Khi nào đọc |
|----------|-------------|
| [An toàn & pháp lý](docs/an-toan-va-phap-ly.md) | **Bắt buộc**, trước khi chạm vào bất cứ thứ gì bay được hoặc có pin LiPo |
| [Cách đóng góp](CONTRIBUTING.md) | Trước khi gửi code đầu tiên |
| [Phụ lục: sơ đồ kỹ năng](docs/phu-luc-so-do-ky-nang.md) | Khi muốn nhìn toàn cảnh ngành nhúng |

---

## Ba nguyên tắc của CLB

**1. Không ai biết trước khi vào.** Không có câu hỏi nào là ngu. Nhưng có câu hỏi hỏi sai thời điểm — hỏi cách làm drone tự bay khi chưa viết nổi vòng lặp C thì không ai trả lời giúp bạn được.

**2. Làm được mới tính.** Đọc hết tài liệu mà chưa ra sản phẩm thì coi như chưa bắt đầu. Mỗi nền trong repo này đều có phần tự kiểm tra bằng việc làm, không phải bằng lý thuyết.

**3. Tự đi được rồi hãy nhờ dẫn.** CLB có rất ít người đủ sức kèm. Thời gian của họ phải dành cho những chỗ bạn thật sự tắc, không phải cho những thứ đã viết sẵn ở đây.

---

## Học tới đâu thì xin được việc?

Đừng hỏi ai. Tự xem thị trường trả lời:

**[Nhóm Tuyển Dụng Lập Trình Nhúng (Embedded), Automotive, C, C++, IOT, QT, QML](https://web.facebook.com/groups/775890384111054)** — nhóm công khai, khoảng 57,6 nghìn thành viên, nhà tuyển dụng đăng tin liên tục.

Cách dùng nhóm này cho đúng: đọc **mô tả công việc**, không đọc mức lương. Lấy vài tin tuyển dụng ở mảng bạn theo, liệt kê các kỹ năng họ yêu cầu, rồi đối chiếu với nền bạn đang học. Chỗ nào bạn chưa có — đó là việc tiếp theo của bạn.

Đây là cách tự định hướng đáng tin nhất, vì nó đến từ nơi thật sự trả tiền, không đến từ cảm nhận của bất kỳ ai trong CLB.

---

## Liên hệ

- Email: utt.uav.club@gmail.com
- Facebook: UTT UAV Club
- Phòng 102, Nhà chuyên gia, Trường Đại học Công nghệ Giao thông Vận tải

*Tài liệu này là tài sản chung. Thấy sai, thấy thiếu, thấy khó hiểu — mở Pull Request sửa. Đó cũng là bài tập Git đầu tiên của bạn.*
