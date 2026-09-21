# Bạn đang ở đâu

File này dành cho bạn vừa vào CLB và đang định hỏi *"anh dạy em làm drone tự bay đi"*, *"em muốn làm AI nhận diện"*, *"em muốn học STM32, bắt đầu từ đâu?"*.

Không có gì sai khi muốn những thứ đó. Chỉ là **chúng là điểm đến, không phải điểm bắt đầu** — mỗi thứ nằm trên năm sáu lớp nền chồng lên nhau.

CLB không phải khoá học có giáo viên đi cùng từ đầu đến cuối. Đây là nơi mọi người tự học, làm dự án và chia sẻ kinh nghiệm. File này giúp bạn tự đi đoạn đầu.

---

## Bạn đang muốn X — việc đầu tiên là Y

| Bạn muốn | Thực ra cần gì trước | Bắt đầu từ |
|---|---|---|
| **Drone tự bay, tự bám mục tiêu** | Đây là sản phẩm của ba nghề ghép lại: firmware giữ thăng bằng, thị giác máy để nhìn, hardware để tồn tại. Chọn **một**. | [Nền chung](#nền-chung--ai-cũng-phải-có) → [Ba mảng](ba-mang-san-pham.md) |
| **AI nhận diện vật thể** | Câu hỏi ngược lại: *nhận diện xong rồi thì sao?* Ở đây nó phải dẫn tới một hành động thật. Và phần khó là chạy nổi trên board nhúng, không phải chọn model. | [Thị giác máy](nen-thi-giac-may.md) |
| **Học STM32** | STM32 là họ vi điều khiển, chưa phải mục tiêu. Biết mình muốn đọc cảm biến hay điều khiển động cơ mới chọn được bài đầu. Cần C có con trỏ và phép toán bit. | [Nền chung](#nền-chung--ai-cũng-phải-có) → [Firmware STM32](nen-stm32.md) |
| **Nhà thông minh, hệ thống IoT** | Đây là chỗ có kết quả sớm nhất và dễ thử nhất. | [ESP32 & Kết nối](nen-esp32.md) |
| **Làm mạch, vẽ PCB** | Nghề cho sản phẩm cầm được sớm nhất, nhưng phạt nặng khi cẩu thả. | [Hardware](nen-hardware.md) |
| **Chưa biết gì cả** | Câu hỏi trung thực nhất, và dễ trả lời nhất. | [Nền chung](#nền-chung--ai-cũng-phải-có) ở dưới |

Chưa cần quyết định hôm nay bạn theo nghề nào. Cần bắt đầu hôm nay.

---

## Tự kiểm tra: điểm bắt đầu của bạn

Đánh dấu theo việc bạn **đã tự làm được**, không theo số video đã xem. Đây không phải bài thi.

**Điểm A — bắt đầu từ nền chung**
- [ ] Chưa từng viết chương trình C nào tự mình nghĩ ra
- [ ] Chưa từng dùng dòng lệnh Linux
- [ ] Chưa từng dùng Git

→ Giữ mục tiêu STM32, AI hay drone làm hướng đi, nhưng bước tiếp theo là Nền chung. Gần như ai cũng từng bắt đầu ở đây.

**Điểm B — đã có nền cơ bản**
- [ ] Viết được chương trình C có con trỏ và struct, tự nghĩ ra, không copy
- [ ] Dùng được `cd`, `ls`, `cat`, cài được phần mềm, đọc hiểu thông báo lỗi
- [ ] Tạo được branch, commit, mở được Pull Request
- [ ] SSH được vào máy khác và chạy lệnh trên đó

→ Chọn nền và mở file tương ứng.

**Điểm C — nhận được việc nhỏ trong dự án**
- [ ] Đọc được datasheet và tìm ra thông tin mình cần
- [ ] Tự sửa được lỗi build
- [ ] Phân biệt được "code sai" và "phần cứng sai", và biết cách kiểm tra

→ Hỏi người phụ trách mảng về một đầu việc đang cần người.

---

## Nền chung — ai cũng phải có

Bốn thứ này không phụ thuộc bạn chọn nền nào.

**1. Lập trình C** — ba trong bốn nền dùng trực tiếp; nền còn lại vẫn phải đọc hiểu code người khác.

Cần: kiểu dữ liệu và độ rộng bit · con trỏ · struct, mảng, hàm · **phép toán trên bit** · khái niệm stack và heap. Chưa cần: OOP, template C++, thuật toán thi đấu.
*Con trỏ khó, phải quay lại học nhiều lần. Bình thường.*

> **Tự chấm:** viết chương trình C nhận một mảng byte, tách các trường bên trong bằng dịch bit và mặt nạ bit. Đây đúng là việc bạn làm hằng ngày khi đọc thanh ghi.

**2. Terminal Linux** — board nhúng không có giao diện, công cụ build không có nút bấm.

Cần: thao tác file · đường dẫn tuyệt đối và tương đối · cài phần mềm · **đọc hiểu thông báo lỗi** · `ssh`. Máy Windows thì cài WSL, chưa cần cài song song hệ điều hành.

> **Tự chấm:** ssh vào một Raspberry Pi qua mạng, tạo file, chạy một script Python bạn vừa viết. Không cắm màn hình vào board.

**3. Git & GitHub** — không biết Git nghĩa là không đóng góp được gì, dù code giỏi đến đâu.

Cần: hiểu commit và branch · `clone`/`add`/`commit`/`push`/`pull` · mở Pull Request · sửa theo góp ý · xử lý conflict mà không xoá thư mục đi clone lại.

> **Tự chấm:** tạo repo thử nghiệm, làm việc trên branch riêng, mở Pull Request.

**4. Python cơ bản** — công cụ, script phân tích dữ liệu, và cả nền thị giác máy đều dùng.

Cần: đọc ghi file · vòng lặp, hàm · `pip` · hiểu môi trường ảo để làm gì.

---

## Hai kỹ năng không ai dạy nhưng quyết định bạn đi được bao xa

### Dùng AI làm cộng sự

AI bây giờ rất mạnh. **Hãy tận dụng để tự học và chuẩn bị câu hỏi tốt hơn.** Mentor không thể đi cùng từng bước, còn AI giải thích lại một khái niệm bao nhiêu lần cũng được.

- **Bắt nó giải thích, đừng chỉ lấy đáp án.** Hỏi "tại sao làm thế" nhiều hơn "code hộ tôi".
- **Không dán code mình không hiểu vào dự án.** Đến lúc nó hỏng bạn sẽ không sửa được.

> **Nhưng AI cũng bịa số liệu, và bịa rất tự tin.** Một con số điện áp hay tên thanh ghi nghe cực hợp lý vẫn có thể sai. Hỏi AI để **hiểu** tài liệu — đừng hỏi AI thay cho việc đọc tài liệu.

AI là cộng sự, không phải người làm hộ.

### Hỏi cho nhanh được giúp

**Cứ hỏi. Đừng ngại.** Ngồi im ba tuần vì sợ hỏi câu ngu mới là điều đáng tiếc. Phần dưới không phải điều kiện để được hỏi — chỉ là mẹo để được trả lời nhanh hơn.

Có bao nhiêu nói bấy nhiêu, thiếu cũng không sao: bạn đang cố làm gì · đã thử gì · kết quả ra sao (lỗi thì **copy nguyên văn**) · đoán nguyên nhân là gì.

*"Em bị lỗi rồi anh ơi"* thì người ta phải hỏi lại năm câu. *"Em nạp code xuống board thì nó báo dòng này, thử cắm cổng khác vẫn thế"* thì nhiều khi được trả lời ngay.

Nếu tiện, thử hỏi AI hoặc tìm nguyên văn lỗi trên mạng trước — nhiều lỗi gỡ được trong hai phút. Nhưng đang gấp hay thấy rối quá thì cứ hỏi luôn.

---

## Việc tiếp theo, ngay hôm nay

- **Điểm A:** chọn một bài nhỏ trong C, terminal hoặc Git và làm cho ra kết quả.
- **Điểm B:** mở file một nền và làm mục **Bài đầu tiên — 1 đến 2 buổi**. Bài tự chấm là đích của cả chặng, không phải việc làm ngay.
- **Điểm C:** hỏi người phụ trách mảng về một đầu việc đang cần người.

Chọn nền: [Firmware STM32](nen-stm32.md) · [ESP32 & Kết nối](nen-esp32.md) · [Hardware](nen-hardware.md) · [Thị giác máy nhúng](nen-thi-giac-may.md)

Chưa biết chọn gì thì xem [Ba mảng sản phẩm](ba-mang-san-pham.md) — chọn nền theo sản phẩm bạn thấy hấp dẫn.
