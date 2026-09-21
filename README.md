# Định hướng — UTT UAV Club

> Câu lạc bộ nghiên cứu Máy bay không người lái
> Trường Đại học Công nghệ Giao thông Vận tải — Hà Nội

CLB làm ba mảng sản phẩm: **UAV**, **IoT** và **AIoT**. Tài liệu này nói mỗi mảng cần nền gì và bạn phải học gì để vào được.

---

## Mới vào thì đọc cái này

**→ [Bạn đang ở đâu](docs/00-ban-dang-o-dau.md)**

File quan trọng nhất trong repo. Nó biến những mục tiêu còn rất rộng — *"làm drone tự bay"*, *"làm AI nhận diện"*, *"làm nhà thông minh"* — thành một việc đầu tiên vừa sức.

**Bắt đầu hôm nay:**

1. Đọc file trên, làm phần tự kiểm tra.
2. Chọn **một nền để thử**, chưa phải cam kết lâu dài.
3. Mở file nền đó, làm mục **Bài đầu tiên — 1 đến 2 buổi**.
4. Tắc thì hỏi — ghi rõ mục tiêu, đã thử gì, lỗi thực tế ra sao.

Chưa có board cũng không sao: hỏi CLB đang có thiết bị gì trước khi mua, và nhiều phần nền chung học được ngay trên máy tính.

---

## NỀN và MẢNG là hai thứ khác nhau

**NỀN** là nghề của bạn. **MẢNG** là sản phẩm CLB làm ra.

Chúng cắt nhau chứ không thay thế nhau: cùng nghề firmware, đem sang UAV thì viết code điều khiển bay, đem sang IoT thì viết code node cảm biến.

### Bốn nền — chọn một

| Nền | Bạn làm gì | Tài liệu |
|-----|------------|----------|
| **Firmware STM32** | Code chạy thẳng trên vi điều khiển. Điều khiển thời gian thực. | [nen-stm32.md](docs/nen-stm32.md) |
| **ESP32 & Kết nối** | Code trên chip có sẵn Wi-Fi. Đưa dữ liệu lên mạng. | [nen-esp32.md](docs/nen-esp32.md) |
| **Hardware** | Thiết kế mạch, vẽ PCB, hàn, đo. | [nen-hardware.md](docs/nen-hardware.md) |
| **Thị giác máy nhúng** | Chạy model thị giác trên board nhúng, đủ nhanh để dùng thật. | [nen-thi-giac-may.md](docs/nen-thi-giac-may.md) |

Thử thật rồi vẫn đổi được. Mục tiêu ban đầu là đi đủ sâu để làm xong **một việc hoàn chỉnh**, không phải học dàn trải cả bốn.

### Ba mảng

| Mảng | Sản phẩm | Dùng nền nào |
|------|----------|--------------|
| **UAV** | Máy bay không người lái | Firmware STM32 + Hardware + Thị giác máy |
| **IoT** | Thiết bị đo, gửi dữ liệu lên mạng | ESP32 & Kết nối + Hardware |
| **AIoT** | Thiết bị IoT tự xử lý, tự nhận diện | ESP32 & Kết nối + Thị giác máy |

Chi tiết: **[Ba mảng sản phẩm](docs/ba-mang-san-pham.md)**

---

## Còn lại trong repo

| Tài liệu | Khi nào đọc |
|----------|-------------|
| [An toàn & pháp lý](docs/an-toan-va-phap-ly.md) | **Bắt buộc**, trước khi chạm vào thứ gì bay được hoặc có pin LiPo |
| [Phụ lục: sơ đồ kỹ năng](docs/phu-luc-so-do-ky-nang.md) | Khi muốn nhìn toàn cảnh ngành nhúng |

---

## Ba nguyên tắc

**1. Bắt đầu từ đúng chỗ.** Không có câu hỏi nào là ngu. Mục tiêu lớn dễ trả lời hơn khi tách thành bước gần nhất với nền hiện tại của bạn.

**2. Làm được mới tính.** Đọc hết tài liệu mà chưa ra sản phẩm thì coi như chưa bắt đầu. Mỗi nền đều có phần tự chấm bằng việc làm.

**3. Tự thử trước, rồi hỏi sớm và hỏi rõ.** Đừng im lặng ba tuần chỉ vì sợ câu hỏi của mình còn cơ bản.

---

## Học tới đâu thì thị trường nhận

Lấy 5–10 mô tả công việc gần đây ở mảng bạn quan tâm, ghi lại kỹ năng lặp lại nhiều lần, đối chiếu với nền đang học. Chỗ nào chưa có là việc tiếp theo của bạn.

[Nhóm Tuyển Dụng Lập Trình Nhúng (Embedded), Automotive, C, C++, IOT, QT, QML](https://web.facebook.com/groups/775890384111054) là một nguồn tham khảo — nên đối chiếu thêm nguồn khác, đừng lấy một tin đơn lẻ làm kết luận. Đọc phần **yêu cầu công việc**, đừng đọc mức lương.

---

## Liên hệ

- Email: utt.uav.club@gmail.com
- Facebook: UTT UAV Club
- Phòng 102, Nhà chuyên gia, Trường Đại học Công nghệ Giao thông Vận tải

*Thấy sai, thấy thiếu, thấy khó hiểu — mở Pull Request sửa. Đó cũng là bài tập Git đầu tiên của bạn.*
