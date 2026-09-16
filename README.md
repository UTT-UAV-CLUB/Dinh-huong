# Định hướng — UTT UAV Club

> Câu lạc bộ nghiên cứu Máy bay không người lái
> Trường Đại học Công nghệ Giao thông Vận tải — Hà Nội

CLB làm ba mảng sản phẩm: **UAV**, **IoT** và **AIoT**. Tài liệu này nói rõ mỗi mảng cần cái nền gì, và bạn phải học gì để đi vào được.

---

## Nếu bạn mới vào CLB, đọc cái này trước

**→ [Bạn đang ở đâu](docs/00-ban-dang-o-dau.md)**

Đây là file quan trọng nhất trong repo. Nó giúp biến những mục tiêu còn rất rộng như *"làm drone tự bay"*, *"làm AI nhận diện"* hay *"làm nhà thông minh"* thành một việc đầu tiên vừa sức.

Bạn không cần hiểu hết mọi thuật ngữ rồi mới được hỏi. Hãy đọc file đó, đánh dấu chỗ mình đang đứng và mang cả những chỗ chưa hiểu ra hỏi — như vậy mentor sẽ giúp bạn nhanh hơn.

### Bắt đầu trong hôm nay

1. Đọc [Bạn đang ở đâu](docs/00-ban-dang-o-dau.md) và làm phần tự kiểm tra.
2. Chọn **một nền để thử trước**, chưa phải cam kết theo lâu dài.
3. Mở file của nền đó và làm mục **Bài đầu tiên — 1 đến 2 buổi**. Bài tự chấm ở cuối là đích của cả chặng, không phải việc phải làm ngay.
4. Nếu tắc, ghi lại mục tiêu, điều đã thử và lỗi thực tế rồi hỏi trong nhóm CLB.

Chưa có board cũng không sao. Hãy hỏi CLB đang có thiết bị gì trước khi mua; nhiều phần nền chung có thể học ngay trên máy tính.

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

Chọn **một nền để bắt đầu**. Sau khi thử thật, bạn có thể đổi. Mục tiêu ban đầu là đi đủ sâu để làm được một việc hoàn chỉnh, không phải học dàn trải cả bốn nền.

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
| [Phụ lục: sơ đồ kỹ năng](docs/phu-luc-so-do-ky-nang.md) | Khi muốn nhìn toàn cảnh ngành nhúng |

---

## Ba nguyên tắc của CLB

**1. Bắt đầu từ đúng chỗ.** Không có câu hỏi nào là ngu. Một mục tiêu lớn sẽ dễ trả lời hơn khi tách thành bước gần nhất với nền hiện tại của bạn.

**2. Làm được mới tính.** Đọc hết tài liệu mà chưa ra sản phẩm thì coi như chưa bắt đầu. Mỗi nền trong repo này đều có phần tự kiểm tra bằng việc làm, không phải bằng lý thuyết.

**3. Tự thử trước, rồi hỏi sớm và hỏi rõ.** Tài liệu giúp bạn đi bước đầu; mentor giúp ở những chỗ bạn đã thử nhưng vẫn tắc. Đừng im lặng quá lâu chỉ vì sợ câu hỏi của mình còn cơ bản.

---

## Học tới đâu thì xin được việc?

Để biết kỹ năng nào đang được tuyển dụng, hãy xem mô tả công việc thực tế:

**[Nhóm Tuyển Dụng Lập Trình Nhúng (Embedded), Automotive, C, C++, IOT, QT, QML](https://web.facebook.com/groups/775890384111054)** là một nơi tham khảo. Nên đối chiếu thêm tin tuyển dụng ở các nguồn khác thay vì dựa vào một bài đăng hoặc một nhóm duy nhất.

Cách làm: lấy 5–10 mô tả công việc gần đây ở mảng bạn quan tâm, ghi lại các kỹ năng lặp lại nhiều lần, rồi đối chiếu với nền đang học. Mức lương, chức danh và yêu cầu số năm kinh nghiệm thay đổi theo công ty nên không dùng một tin đơn lẻ làm kết luận.

Đây là một cách kiểm tra hướng học bằng nhu cầu thực tế, bên cạnh góp ý của mentor và trải nghiệm khi bạn tự làm dự án.

---

## Liên hệ

- Email: utt.uav.club@gmail.com
- Facebook: UTT UAV Club
- Phòng 102, Nhà chuyên gia, Trường Đại học Công nghệ Giao thông Vận tải

*Tài liệu này là tài sản chung. Thấy sai, thấy thiếu, thấy khó hiểu — mở Pull Request sửa. Đó cũng là bài tập Git đầu tiên của bạn.*
