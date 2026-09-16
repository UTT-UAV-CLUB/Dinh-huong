# Cách đóng góp — Luật Git của CLB

Mọi thành viên đều phải theo quy trình này, kể cả khi chỉ sửa một dòng.

---

## Quy ước nhánh

- `main` — code đã ổn định. **Không ai commit thẳng vào đây.**
- `dev` — nhánh phát triển chính. Mọi nhánh tính năng tách ra từ đây.
- `feat/<tên>-<nội dung>` — nhánh làm việc của bạn.

Ví dụ: `feat/hung-driver-mpu6050`, `feat/lan-pcb-power-v2`

---

## Quy trình làm việc

```bash
# 1. Lấy code mới nhất
git checkout dev
git pull origin dev

# 2. Tạo nhánh riêng cho việc bạn định làm
git checkout -b feat/ten-cua-ban-noi-dung

# 3. Làm việc, commit từng bước nhỏ và có nghĩa
git add duong-dan-file-cu-the
git commit -m "Mo ta ngan gon viec ban vua lam"

# 4. Đẩy lên
git push -u origin feat/ten-cua-ban-noi-dung

# 5. Mở Pull Request vào nhánh dev trên GitHub
```

Pull Request phải được **người phụ trách mảng đó review và duyệt** trước khi merge.

Lưu ý ở bước 3: dùng `git add` với đường dẫn cụ thể. Tránh `git add .` cho đến khi bạn thật sự chắc mình đang thêm những file nào — đó là cách phổ biến nhất để vô tình commit mật khẩu và file rác.

---

## Viết commit message

**Nên:**

```
Them driver doc cam bien MPU6050 qua I2C
Sua loi tran bo dem khi goi tin MAVLink dai hon 64 byte
Cap nhat so do nguyen ly mach nguon: doi tu LDO sang buck
```

**Không nên:**

```
update
fix bug
abc
commit lan 3
```

Sáu tháng nữa sẽ có người đọc lại commit của bạn để tìm xem lỗi xuất hiện từ đâu. Người đó nhiều khả năng chính là bạn.

---

## Những thứ KHÔNG đưa vào Git

- File nhị phân lớn: file `.bin`, `.hex` đã build, mô hình 3D nặng
- Log bay thô — để ở kho lưu trữ chung của lab
- File tạm của phần mềm EDA, thư mục build, thư mục cache
- **Mật khẩu, khoá API, thông tin cá nhân** — repo này công khai, ai cũng đọc được

Dùng `.gitignore` để chặn từ đầu. Nếu đã lỡ commit mật khẩu thì **báo ngay**, đừng chỉ xoá ở commit sau — nó vẫn nằm nguyên trong lịch sử và ai cũng lấy lại được.

---

## Quy ước đặt tên repo

Để sau này 30 repo vẫn tìm được:

| Tiền tố | Dùng cho | Ví dụ |
|---------|----------|-------|
| `fw-` | Firmware, code nhúng | `fw-flight-controller-v1` |
| `hw-` | Thiết kế mạch, PCB | `hw-power-board-rev2` |
| `av-` | Autonomy, thị giác máy | `av-precision-landing` |
| `gcs-` | Trạm mặt đất, công cụ | `gcs-log-analyzer` |
| `docs-` | Tài liệu | `docs-dinh-huong` |

Tên repo viết thường, ngăn cách bằng dấu gạch ngang, không dấu tiếng Việt, không dấu chấm.

---

## Review Pull Request

Khi bạn review PR của người khác:

- Góp ý về **code**, không về người viết.
- Hỏi khi không hiểu, thay vì đoán rồi phê bình.
- Thấy một con số trong code hoặc trong bình luận — hỏi nguồn. *"Con số 3.3V này lấy từ đâu?"* là câu hỏi review tốt nhất và hay bị bỏ qua nhất.

Khi PR của bạn bị góp ý: đó không phải chê bai. Không ai viết đúng ngay lần đầu, kể cả người đang review bạn.
