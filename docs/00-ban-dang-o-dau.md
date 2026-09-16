# Bạn đang ở đâu

File này dành cho bạn vừa vào CLB và đang định hỏi một câu kiểu:

> *"Anh dạy em làm drone tự bay đi."*
> *"Em muốn làm AI nhận diện vật thể."*
> *"Em muốn học STM32, bắt đầu từ đâu?"*

Không có gì sai khi muốn những thứ đó. Vấn đề nằm ở chỗ khác: **những thứ đó không phải điểm bắt đầu, chúng là điểm đến**. Và khoảng cách từ chỗ bạn đang đứng tới đó thường xa hơn bạn nghĩ — không phải vì nó khó một cách bí ẩn, mà vì nó được xếp chồng lên khoảng năm sáu lớp nền mà bạn chưa có.

CLB chỉ có một hai người đủ sức kèm. Nếu mỗi người mới đều cần được giải thích lại từ đầu, không ai còn thời gian làm việc thật. File này viết ra để bạn tự đi được đoạn đường đầu tiên.

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

Và cái khó không nằm ở model. Model là phần dễ nhất, có sẵn đầy. Cái khó là chạy nó **trên board nhúng gắn trên thiết bị**, đủ nhanh để phản ứng kịp, với lượng điện ít ỏi. Một model chính xác 99% mà chạy quá chậm để dùng thì bằng không.

**Việc của bạn bây giờ:** học Python cho chắc, học Linux dòng lệnh, rồi làm cho một cái camera trên board nhúng chạy được và **tự đo xem nó chạy nhanh bao nhiêu khung hình mỗi giây**.
**Bắt đầu từ:** [Nền thị giác máy nhúng](nen-thi-giac-may.md).

### "Em muốn học STM32"

Câu này hỏi được, nhưng nó giống như nói "em muốn học lái xe" mà chưa biết đi bộ. STM32 là con chip — bạn học nó để làm gì mới là câu hỏi thật.

**Kiểm tra nhanh:** bạn viết được chương trình C dùng con trỏ và phép toán trên bit chưa? Nếu chưa, học STM32 lúc này bạn sẽ chỉ copy code mẫu và không hiểu vì sao nó chạy. Đến khi nó không chạy, bạn sẽ bế tắc hoàn toàn.

**Bắt đầu từ:** phần C ở [Nền chung](#nền-chung--ai-cũng-phải-có), rồi sang [Nền firmware STM32](nen-stm32.md).

### "Em muốn làm nhà thông minh / hệ thống IoT"

Đây là mảng dễ có kết quả sớm nhất, và cũng là chỗ tốt nhất để bắt đầu nếu bạn chưa biết mình hợp với gì.

**Bắt đầu từ:** [Nền ESP32 & Kết nối](nen-esp32.md). Mục tiêu đầu tiên rất cụ thể: đọc một cảm biến, đẩy số đo đó lên mạng, xem được từ điện thoại.

### "Em muốn làm mạch, vẽ PCB"

Được. Đây là nghề cho ra sản phẩm cầm được sớm nhất, nhưng cũng là nghề phạt nặng nhất khi cẩu thả — board sai thì mất tiền đặt lại và mất vài tuần chờ.

**Bắt đầu từ:** [Nền Hardware](nen-hardware.md).

### "Em chưa biết gì cả, em nên làm gì?"

Đây là câu hỏi trung thực nhất trong tất cả, và dễ trả lời nhất.

Làm hết [Nền chung](#nền-chung--ai-cũng-phải-có) ở dưới. Mất khoảng hai đến ba tuần. Trong lúc làm, bạn sẽ tự nhận ra mình thích phần nào — thích code thì đi firmware, thích cầm mỏ hàn thì đi hardware, thích nghịch dữ liệu và ảnh thì đi thị giác máy.

Không cần quyết định ngay hôm nay. Cần bắt đầu ngay hôm nay.

---

## Tự kiểm tra: bạn đang ở mức nào

Làm thử, đừng chỉ đọc. Mất khoảng một buổi.

**Mức 0 — chưa có nền**
- [ ] Tôi chưa từng viết chương trình C nào tự mình nghĩ ra
- [ ] Tôi chưa từng dùng dòng lệnh Linux
- [ ] Tôi chưa từng dùng Git

→ Bạn ở đây thì **mọi câu hỏi về STM32, AI, drone đều chưa có nghĩa**. Bắt đầu từ Nền chung. Đây không phải lời chê — gần như ai cũng bắt đầu từ mức này.

**Mức 1 — có nền cơ bản**
- [ ] Tôi viết được chương trình C có dùng con trỏ và struct, tự nghĩ ra, không copy
- [ ] Tôi dùng được `cd`, `ls`, `cat`, cài được phần mềm, đọc hiểu được thông báo lỗi
- [ ] Tôi tạo được branch, commit và mở được Pull Request
- [ ] Tôi ssh được vào một máy khác và chạy lệnh trên đó

→ Bạn chọn được nền rồi. Mở file nền tương ứng và làm theo.

**Mức 2 — đi được một mình**
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

### 2. Dòng lệnh Linux

**Tại sao:** board nhúng không có giao diện. Công cụ build không có nút bấm. Bạn sẽ sống trên dòng lệnh.

Cần làm được: di chuyển và thao tác file · hiểu đường dẫn tuyệt đối và tương đối · cài phần mềm · **đọc thông báo lỗi và hiểu nó đang nói về cái gì** · `ssh` vào máy khác.

Máy chạy Windows thì cài WSL. Chưa cần cài song song hệ điều hành.

**Tự chấm:** ssh vào một board Raspberry Pi qua mạng, tạo file trên đó, chạy một script Python bạn vừa viết. Không cắm màn hình trực tiếp vào board.

### 3. Git & GitHub

**Tại sao:** đây là cách CLB làm việc chung. Không biết Git nghĩa là bạn không đóng góp được gì, dù code giỏi đến đâu.

Cần làm được: hiểu commit và branch, và vì sao không ai commit thẳng vào `main` · `clone`/`add`/`commit`/`push`/`pull` · tạo branch và mở Pull Request · sửa theo góp ý của người review · xử lý conflict mà không xoá cả thư mục đi clone lại.

Luật cụ thể của CLB nằm ở [CONTRIBUTING.md](../CONTRIBUTING.md).

**Tự chấm:** mở một Pull Request vào chính repo này — sửa lỗi chính tả, làm rõ một câu khó hiểu, hoặc thêm thứ bạn thấy thiếu. PR được merge là bạn qua.

### 4. Python cơ bản

**Tại sao:** công cụ, script phân tích dữ liệu, và toàn bộ nền thị giác máy dùng Python.

Cần làm được: đọc ghi file · vòng lặp và hàm · cài thư viện bằng `pip` · hiểu môi trường ảo là gì và tại sao cần.

---

## Hai kỹ năng không ai dạy nhưng quyết định bạn đi được bao xa

### Không bịa số liệu

Đây là nguyên tắc số một của CLB.

Khi bạn nói *"con chip này chạy ở 3.3V"* hay *"cảm biến này lấy mẫu 1000 lần mỗi giây"* — con số đó phải đến từ **datasheet**. Không phải từ trí nhớ. Không phải suy ra từ tên linh kiện. Không phải từ một video trên mạng.

Lý do rất thực tế: **một con số bịa trông y hệt một con số đúng.** Người review không có cách nào phát hiện, và nó sẽ đi thẳng vào thiết kế. Đến khi board cháy hoặc drone rơi thì mới biết, và lúc đó tìm lại nguyên nhân rất tốn kém.

Không tra được thì viết thẳng **"chưa kiểm chứng"**. Không ai đánh giá thấp bạn vì câu đó. Người ta đánh giá thấp bạn vì một con số sai làm hỏng phần cứng.

Quy tắc phụ, cũng quan trọng: **không suy thông số từ tên gọi**. Tên linh kiện, tên chân, tên hàm chỉ gợi ý chỗ cần tra — chúng không phải bằng chứng.

### Hỏi đúng cách

Nói đủ bốn thứ:

1. Bạn đang cố làm gì
2. Bạn đã thử những gì
3. Kết quả thực tế ra sao — kèm thông báo lỗi **nguyên văn**, copy nguyên xi, không diễn đạt lại
4. Bạn nghĩ nguyên nhân có thể là gì

*"Em bị lỗi rồi anh ơi"* sẽ không nhận được câu trả lời nào hữu ích, vì không ai biết bắt đầu từ đâu.

Trước khi hỏi người, thử ba việc: đọc kỹ thông báo lỗi từ đầu đến cuối, tìm nguyên văn thông báo đó trên mạng, và kiểm tra xem tài liệu trong repo này đã trả lời chưa.

---

## Xong rồi thì đi đâu

Chọn một nền:

- [Firmware STM32](nen-stm32.md) — code chạy trực tiếp trên vi điều khiển
- [ESP32 & Kết nối](nen-esp32.md) — đưa thiết bị lên mạng
- [Hardware](nen-hardware.md) — thiết kế mạch và PCB
- [Thị giác máy nhúng](nen-thi-giac-may.md) — cho máy nhìn được

Chưa biết chọn gì thì đọc [Ba mảng sản phẩm](ba-mang-san-pham.md) để xem CLB đang làm ra cái gì, rồi chọn nền theo sản phẩm bạn thấy hấp dẫn.

Và nếu bạn muốn biết **học tới đâu thì thị trường nhận**: vào [nhóm tuyển dụng lập trình nhúng](https://web.facebook.com/groups/775890384111054), đọc mô tả công việc trong các tin tuyển dụng, đối chiếu với nền bạn đang học. Đó là thước đo thật, không phải ý kiến của ai cả.
