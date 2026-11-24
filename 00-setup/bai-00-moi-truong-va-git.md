# Bài 0: Môi trường làm việc và Git

**Mục tiêu:** dùng terminal thoải mái, đưa repo `fullstack-journey` lên GitHub. Mọi bài tập từ nay đều commit vào repo này.

**Máy bạn đã có:** Git 2.56, Node 24, Python 3.14, VS Code. Git đã có `user.name` và `user.email`.
**Còn thiếu:** nhánh mặc định `main`, SSH key để kết nối GitHub.

---

## 1. Terminal trong 10 phút

Trong VS Code mở terminal bằng `` Ctrl + ` ``. Chọn **Git Bash** làm terminal mặc định (bấm mũi tên cạnh dấu `+` → *Select Default Profile* → *Git Bash*), để lệnh giống hệt trên Mac/Linux và server sau này.

| Lệnh | Ý nghĩa |
|---|---|
| `pwd` | Đang đứng ở thư mục nào |
| `ls` / `ls -la` | Liệt kê file (kể cả file ẩn) |
| `cd ten-thu-muc` | Đi vào thư mục |
| `cd ..` | Lùi ra một cấp |
| `cd ~` | Về thư mục home (`C:\Users\ADMIN`) |
| `mkdir ten` | Tạo thư mục |
| `touch file.txt` | Tạo file rỗng |
| `cat file.txt` | In nội dung file |
| `rm file.txt` | Xóa file (không vào thùng rác!) |

**Đường dẫn tuyệt đối** bắt đầu từ gốc: `/c/Users/ADMIN/fullstack-journey`.
**Đường dẫn tương đối** tính từ chỗ đang đứng: `00-setup/bai-00-moi-truong-va-git.md`.

> Mẹo: gõ vài chữ đầu rồi bấm `Tab` để tự hoàn thành tên. Bấm `↑` để gọi lại lệnh cũ.

## 2. Git là gì, trong một hình

```
thư mục làm việc  --git add-->  staging  --git commit-->  lịch sử (local)  --git push-->  GitHub
```

- **commit** = một bức ảnh chụp toàn bộ dự án tại một thời điểm, kèm lời nhắn.
- **staging** = khu chọn những thay đổi sẽ vào bức ảnh tiếp theo.
- **push** = gửi các commit lên GitHub.

Lệnh dùng hằng ngày:

```bash
git status            # có gì thay đổi?
git add ten-file      # đưa vào staging (git add . = tất cả)
git commit -m "Thêm bài 0"
git log --oneline     # xem lịch sử
git push
```

**Lời nhắn commit tốt** nói *thay đổi gì*, ở thì hiện tại: `Thêm form đăng nhập`, `Sửa lỗi xóa todo`. Tránh: `update`, `fix`, `asdf`.

## 3. Kết nối GitHub bằng SSH

```bash
git config --global init.defaultBranch main
ssh-keygen -t ed25519 -C "laptop-cua-toi"     # Enter 3 lần là được
cat ~/.ssh/id_ed25519.pub                      # copy dòng này
```

Vào GitHub → bấm **ảnh đại diện** góc trên phải → **Settings** (của tài khoản, không phải tab Settings của repo) → thanh trái, nhóm *Access* → **SSH and GPG keys → New SSH key** → dán cả dòng `ssh-ed25519 ...` vào. Link thẳng: https://github.com/settings/keys. Kiểm tra (lần đầu gõ `yes`):

```bash
ssh -T git@github.com
# Hi <tên-bạn>! You've successfully authenticated...
```

> Không bao giờ chia sẻ file `id_ed25519` (không có đuôi `.pub`). Đó là khóa bí mật.

---

## Bài tập

**BT1. Terminal.** Chỉ dùng terminal (không dùng chuột), trong `fullstack-journey/00-setup/`:
1. Tạo thư mục `thuc-hanh`, đi vào đó.
2. Tạo file `gioi-thieu.txt`, ghi vào 3 dòng: tên bạn, vì sao bạn học lập trình, một app bạn muốn làm được. (Gợi ý: `echo "dòng 1" >> gioi-thieu.txt`)
3. In nội dung file ra màn hình.
4. Ghi lại **tất cả lệnh bạn đã gõ** vào file `00-setup/lenh-da-dung.txt`.

**BT2. Repo đầu tiên.**
1. Tạo repo **trống** tên `fullstack-journey` trên GitHub (không tick README).
2. Trong thư mục `fullstack-journey`:
   ```bash
   git init
   git add .
   git commit -m "Khởi tạo lộ trình học"
   git remote add origin git@github.com:<tên-bạn>/fullstack-journey.git
   git push -u origin main
   ```
3. Mở GitHub, thấy file của bạn trên đó.

**BT3. Ba commit.** Sửa `gioi-thieu.txt` ba lần (mỗi lần thêm một dòng), mỗi lần một commit với lời nhắn rõ ràng. Push lên. Chạy `git log --oneline` và chép kết quả vào cuối `lenh-da-dung.txt`.

**Câu hỏi tự kiểm tra** (trả lời trong `00-setup/tra-loi.md`):
1. `git add` và `git commit` khác nhau thế nào?
2. Nếu bạn sửa file nhưng chưa `git add`, thì `git commit` có lưu thay đổi đó không?
3. Vì sao không nên commit file mật khẩu hay `.env`?

---

Làm xong, nói **"chấm bài 0"**. Mình sẽ xem `lenh-da-dung.txt`, `tra-loi.md`, lịch sử commit và cho Bài 1.
