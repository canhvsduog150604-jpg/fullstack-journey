# Trả lời câu hỏi Bài 0

1. `git add` đưa thay đổi vào staging, lúc này thay đổi **chưa được lưu** vào lịch sử. `git commit` mới lưu những gì đang nằm trong staging thành một commit.

2. Không. `git commit` chỉ lưu những gì đã ở trong staging. File đã sửa mà chưa `git add` thì vẫn ở trạng thái *modified* và không có trong commit. (Mình kiểm chứng bằng `git status`: file chưa add hiện ở mục "Untracked files" hoặc "Changes not staged", và Git báo "nothing added to commit".)

3. Vì dễ push nhầm lên GitHub, người khác sẽ thấy được mật khẩu hoặc file `.env`. Xóa file ở commit sau cũng không cứu được vì nó vẫn nằm trong lịch sử Git, và có bot quét GitHub tìm key bị lộ chỉ trong vài phút. Cách phòng: ghi `.env` vào `.gitignore` ngay từ đầu.
