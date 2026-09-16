# Bạn đang ở đâu

File này dành cho bạn vừa vào CLB và đang định hỏi một câu kiểu:

> *"Anh dạy em làm drone tự bay đi."*
> *"Em muốn làm AI nhận diện vật thể."*
> *"Em muốn học STM32, bắt đầu từ đâu?"*

Không có gì sai khi muốn những thứ đó. Vấn đề nằm ở chỗ khác: **những thứ đó không phải điểm bắt đầu, chúng là điểm đến**. Và khoảng cách từ chỗ bạn đang đứng tới đó thường xa hơn bạn nghĩ — không phải vì nó khó một cách bí ẩn, mà vì nó được xếp chồng lên khoảng năm sáu lớp nền mà bạn chưa có.

CLB không phải một khóa học có giáo viên đi cùng từ đầu đến cuối; đây là nơi mọi người tự học, làm dự án và chia sẻ kinh nghiệm. Mentor có thời gian giới hạn, nên file này giúp bạn tự đi đoạn đầu và chuẩn bị đủ thông tin để được hỗ trợ đúng chỗ.

Bạn không cần đọc thuộc hay hiểu hết ngay. Hãy tìm phần gần nhất với mục tiêu của mình, làm phần tự kiểm tra, rồi chọn một việc nhỏ để thử.

---

## Bạn đang đòi cái này — thực ra bạn cần cái kia trước

Tìm thứ gần nhất với điều bạn muốn.

### "Em muốn làm drone tự bay, tự bám theo người"

Thứ bạn vừa mô tả là sản phẩm của **ba nhóm người khác nhau** làm trong nhiều tháng, ghép lại.

Để nó bay được: có người viết firmware giữ thăng bằng. Để nó nhìn được: có người chạy model thị giác trên board nhúng. Để nó tồn tại: có người vẽ mạch, hàn, đo. Và để ba thứ nói chuyện được với nhau: có người hiểu giao thức truyền tin giữa chúng.

**Việc của bạn bây giờ:** chọn **một** trong ba nghề đó. Không phải cả ba.
**Bắt đầu từ:** mục [Nền chung](#nền-chung--ai-cũng-phải-có) ở dưới, rồi đọc [Ba mảng sản phẩm](ba-mang-san-pham.md) để biết mình sẽ ghép vào đâu.

### "Em muốn làm AI nhận diện vật thể"

Câu hỏi ngược lại dành cho bạn: **nhận diện xong rồi thì sao?**

Nếu câu trả lời là "hiện lên màn hình cho đẹp" thì đó không phải việc của CLB này. Ở đây, nhận diện xong phải dẫn tới một hành động: drone bay lệch sang trái, cái van đóng lại, cái còi kêu lên.

Model chỉ là một phần của hệ thống. Thách thức lớn ở CLB là chạy nó **trên board nhúng gắn trên thiết bị**, đủ nhanh để phản ứng kịp và đủ ổn định với nguồn điện, nhiệt độ, camera thực tế. Độ chính xác cao vẫn chưa đủ nếu hệ thống không đạt tốc độ hoặc độ trễ mà bài toán yêu cầu.

**Việc của bạn bây giờ:** học Python cho chắc, học Linux dòng lệnh, rồi làm cho một cái camera trên board nhúng chạy được và **tự đo xem nó chạy nhanh bao nhiêu khung hình mỗi giây**.
**Bắt đầu từ:** [Nền thị giác máy nhúng](nen-thi-giac-may.md).

### "Em muốn học STM32"

Câu này hoàn toàn hợp lý, nhưng STM32 là một họ vi điều khiển chứ chưa phải mục tiêu cuối. Biết mình muốn đọc cảm biến, điều khiển động cơ hay làm flight controller sẽ giúp chọn bài đầu tiên phù hợp.

**Kiểm tra nhanh:** bạn viết được chương trình C dùng con trỏ và phép toán trên bit chưa? Nếu chưa, hãy củng cố C trước hoặc học song song bằng bài rất nhỏ. Nếu chỉ chép code mẫu, bạn sẽ khó tự tìm lỗi khi phần cứng không phản hồi.

**Bắt đầu từ:** phần C ở [Nền chung](#nền-chung--ai-cũng-phải-có), rồi sang [Nền firmware STM32](nen-stm32.md).

### "Em muốn làm nhà thông minh / hệ thống IoT"

Đây là mảng dễ có kết quả sớm nhất, và cũng là chỗ tốt nhất để bắt đầu nếu bạn chưa biết mình hợp với gì.

**Bắt đầu từ:** [Nền ESP32 & Kết nối](nen-esp32.md). Mục tiêu đầu tiên rất cụ thể: đọc một cảm biến, đẩy số đo đó lên mạng, xem được từ điện thoại.

### "Em muốn làm mạch, vẽ PCB"

Được. Đây là nghề cho ra sản phẩm cầm được sớm nhất, nhưng cũng là nghề phạt nặng nhất khi cẩu thả — board sai thì mất tiền đặt lại và mất vài tuần chờ.

**Bắt đầu từ:** [Nền Hardware](nen-hardware.md).

### "Em chưa biết gì cả, em nên làm gì?"

Đây là câu hỏi trung thực nhất trong tất cả, và dễ trả lời nhất.

Làm [Nền chung](#nền-chung--ai-cũng-phải-có) ở dưới đến mức hoàn thành được các bài tự chấm. Thời gian có thể từ vài tuần đến lâu hơn tùy nền tảng và quỹ thời gian. Trong lúc làm, bạn sẽ dần nhận ra mình thích code, phần cứng hay dữ liệu và hình ảnh.

Không cần quyết định ngay hôm nay. Cần bắt đầu ngay hôm nay.

---

## Tự kiểm tra: điểm bắt đầu của bạn

Hãy đánh dấu theo việc bạn **đã tự làm được**, không theo số video đã xem. Đây không phải bài thi và cũng không dùng để xếp hạng thành viên.

**Điểm A — bắt đầu từ nền chung**
- [ ] Tôi chưa từng viết chương trình C nào tự mình nghĩ ra
- [ ] Tôi chưa từng dùng dòng lệnh Linux
- [ ] Tôi chưa từng dùng Git

→ Giữ mục tiêu STM32, AI hay drone làm hướng đi, nhưng bước tiếp theo nên là Nền chung. Gần như ai cũng từng bắt đầu ở đây.

**Điểm B — đã có nền cơ bản**
- [ ] Tôi viết được chương trình C có dùng con trỏ và struct, tự nghĩ ra, không copy
- [ ] Tôi dùng được `cd`, `ls`, `cat`, cài được phần mềm, đọc hiểu được thông báo lỗi
- [ ] Tôi tạo được branch, commit và mở được Pull Request
- [ ] Tôi ssh được vào một máy khác và chạy lệnh trên đó

→ Bạn chọn được nền rồi. Mở file nền tương ứng và làm theo.

**Điểm C — đã có thể nhận việc nhỏ trong dự án**
- [ ] Tôi đọc được datasheet và tìm ra thông tin mình cần trong đó
- [ ] Tôi tự sửa được lỗi build mà không cần hỏi ai
- [ ] Tôi phân biệt được "code sai" và "phần cứng sai", và biết cách kiểm tra xem là cái nào

→ Bạn bắt đầu nhận được việc thật trong dự án của CLB.

---

## Nền chung — ai cũng phải có

Bốn thứ này không phụ thuộc bạn chọn nền nào. Thiếu chúng thì mọi thứ phía sau đều tắc.

### 1. Lập trình C

**Tại sao:** ba trong bốn nền dùng C trực tiếp. Nền còn lại vẫn phải đọc hiểu code của người khác.

Cần nắm: biến và độ rộng bit của từng kiểu · con trỏ · struct và mảng · hàm · **phép toán trên bit** (AND, OR, XOR, dịch trái, dịch phải) · khái niệm stack và heap.

Con trỏ khó, và bạn sẽ phải quay lại học nhiều lần. Điều đó bình thường, không phải dấu hiệu bạn không hợp.

Chưa cần: lập trình hướng đối tượng, template C++, thuật toán thi đấu.

**Tự chấm:** viết chương trình C nhận một mảng byte, tách ra các trường dữ liệu bên trong bằng phép dịch bit và mặt nạ bit, in kết quả ra. Đây chính xác là việc bạn sẽ làm hằng ngày khi đọc thanh ghi phần cứng.

### 2. Terminal Linux

**Tại sao:** board nhúng không có giao diện. Công cụ build không có nút bấm. Bạn sẽ sống trên dòng lệnh.

Cần làm được: di chuyển và thao tác file · hiểu đường dẫn tuyệt đối và tương đối · cài phần mềm · **đọc thông báo lỗi và hiểu nó đang nói về cái gì** · `ssh` vào máy khác.

Máy chạy Windows thì cài WSL. Chưa cần cài song song hệ điều hành.

**Tự chấm:** ssh vào một board Raspberry Pi qua mạng, tạo file trên đó, chạy một script Python bạn vừa viết. Không cắm màn hình trực tiếp vào board.

### 3. Git & GitHub

**Tại sao:** đây là cách CLB làm việc chung. Không biết Git nghĩa là bạn không đóng góp được gì, dù code giỏi đến đâu.

Cần làm được: hiểu commit và branch, và vì sao không ai commit thẳng vào `main` · `clone`/`add`/`commit`/`push`/`pull` · tạo branch và mở Pull Request · sửa theo góp ý của người review · xử lý conflict mà không xoá cả thư mục đi clone lại.

**Tự chấm:** tạo một repo thử nghiệm, làm việc trên branch riêng và mở Pull Request. Khi đã biết quy trình của CLB, bạn có thể sửa lỗi chính tả hoặc làm rõ tài liệu trong repo này.

### 4. Python cơ bản

**Tại sao:** công cụ, script phân tích dữ liệu, và toàn bộ nền thị giác máy dùng Python.

Cần làm được: đọc ghi file · vòng lặp và hàm · cài thư viện bằng `pip` · hiểu môi trường ảo là gì và tại sao cần.

---

## Hai kỹ năng không ai dạy nhưng quyết định bạn đi được bao xa

### Dùng AI làm cộng sự

AI bây giờ rất mạnh. **Hãy tận dụng để tự học và chuẩn bị câu hỏi tốt hơn.** Mentor không thể luôn đi cùng từng bước, còn AI có thể giải thích lại một khái niệm nhiều lần và giúp bạn tìm hướng thử tiếp theo.

Dùng sao cho ra kỹ năng thật:

- **Bắt nó giải thích, đừng chỉ lấy đáp án.** Hỏi "tại sao làm thế" nhiều hơn "code hộ tôi".
- **Không dán code mình không hiểu vào dự án.** Đến lúc nó hỏng bạn sẽ không sửa được, và người review sẽ hỏi.

> **Nhưng AI cũng bịa số liệu, và bịa rất tự tin.** Một con số điện áp hay tên thanh ghi nghe cực kỳ hợp lý vẫn có thể sai. Hỏi AI để **hiểu** tài liệu đang nói gì — đừng hỏi AI thay cho việc đọc tài liệu.

AI là cộng sự, không phải người làm hộ.

### Hỏi cho nhanh được giúp

**Cứ hỏi. Đừng ngại.** Ngồi im ba tuần vì sợ hỏi câu ngu mới là điều đáng tiếc — ai trong CLB cũng từng tắc ở đúng những chỗ bạn đang tắc.

Phần dưới không phải điều kiện để được hỏi. Nó chỉ là mẹo giúp bạn nhận được câu trả lời nhanh hơn và đúng hơn.

Nói được càng nhiều thứ sau càng tốt — có bao nhiêu nói bấy nhiêu, thiếu cũng không sao:

- Bạn đang cố làm gì
- Bạn đã thử gì rồi
- Nó ra kết quả thế nào — nếu có thông báo lỗi thì **copy nguyên văn**, đừng kể lại bằng lời
- Bạn đoán nguyên nhân là gì

Khác biệt rất lớn: *"em bị lỗi rồi anh ơi"* thì người ta phải hỏi lại năm câu mới biết bắt đầu từ đâu, còn *"em nạp code xuống board thì nó báo dòng này, em thử cắm lại cổng khác vẫn thế"* thì nhiều khi được trả lời ngay trong một câu.

Và nếu tiện, thử hỏi AI trước hoặc tìm nguyên văn thông báo lỗi trên mạng — nhiều lỗi gỡ được trong hai phút. Nhưng nếu bạn đang gấp hoặc thấy rối quá thì cứ hỏi luôn, không phải xin phép ai cả.

---

## Xong rồi thì đi đâu

Chọn một nền:

- [Firmware STM32](nen-stm32.md) — code chạy trực tiếp trên vi điều khiển
- [ESP32 & Kết nối](nen-esp32.md) — đưa thiết bị lên mạng
- [Hardware](nen-hardware.md) — thiết kế mạch và PCB
- [Thị giác máy nhúng](nen-thi-giac-may.md) — cho máy nhìn được

Chưa biết chọn gì thì đọc [Ba mảng sản phẩm](ba-mang-san-pham.md) để xem CLB đang làm ra cái gì, rồi chọn nền theo sản phẩm bạn thấy hấp dẫn.

### Việc tiếp theo ngay hôm nay

- Nếu ở **Điểm A**: chọn một bài nhỏ trong C, terminal hoặc Git và làm cho ra kết quả.
- Nếu ở **Điểm B**: mở file của một nền và làm mục **Bài đầu tiên — 1 đến 2 buổi**; xem bài tự chấm như mục tiêu dài hơn.
- Nếu ở **Điểm C**: hỏi người phụ trách mảng về một issue hoặc đầu việc nhỏ đang cần người.

Nếu muốn biết **học tới đâu thì thị trường nhận**, hãy lấy 5–10 mô tả công việc gần đây từ nhiều nguồn, tìm các kỹ năng xuất hiện lặp lại rồi đối chiếu với nền đang học. [Nhóm tuyển dụng lập trình nhúng](https://web.facebook.com/groups/775890384111054) là một nguồn tham khảo, không phải thước đo duy nhất.
