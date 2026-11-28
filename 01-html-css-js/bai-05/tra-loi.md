index.html?ho-ten=aa&email=asd%40gmail.com&so-dien-thoai=80703418&chu-de=&loi-nhan=chào2312321&lien-he-lai=email&ban-sao=co

1. 
Có 7 cặp name=giá trị - Ô liên hệ lại = điện thoại không xuất hiện vì tôi đang chọn ô email rồi
- Checkbox không tick thì không được gửi. Lần thử này bạn tick nên ban-sao=co mới xuất hiện. Thử lại mà không tick, cặp đó sẽ biến mất.

2. 
for của label phải trùng id của ô nhập vì nếu khác đi, khi click vào chữ nó sẽ không tự động chọn vào ô

Lợi ích:
- Người dùng có thể thoải mái bấm hơn
- Trình đọc màn hình sẽ đọc đúng tên nhãn khi người dùng di chuyển tới ô nhập, giúp trang web thân thiện hơn với người khiếm thị

3. 
Khác nhau giữa :invalid và :user-invalid
- invalid` tô đỏ ngay khi vừa mở trang (vì ô `required` đang trống), trông như người dùng đã làm sai. `:user-invalid` chỉ tô đỏ sau khi người dùng đã gõ vào rồi rời đi, hoặc đã bấm Gửi.

4. 
Đã có required và minlength ở trình duyệt mà server vẫn phải kiểm tra lại vì: 
- Có thể mở DevTools xóa thuộc tính
- Server kiểm tra lại để tránh dữ liệu rỗng, sai định dạng, gây lỗi database hoặc lách luật nghiệp vụ.
- Validate ở trình duyệt để thông báo nhanh cho người dùng, còn server kiểm tra lại để đảm bảo an toàn, dữ liệu sạch