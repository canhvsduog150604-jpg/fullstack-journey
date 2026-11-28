1. 
| | Flexbox | Grid |
|---|---|---|
| Xếp theo | **Một chiều**: một hàng hoặc một cột | **Hai chiều**: hàng và cột cùng lúc |
| Ai quyết định kích thước | Nội dung của item | Khung lưới do container vẽ sẵn |
| Hợp với | Thanh menu, một hàng nút, ảnh cạnh chữ | Bố cục cả trang, lưới thẻ, bảng ảnh |

Ví dụ trên trang profile của tôi:
- Phần tên + thanh nav: flexbox
- Phần section: Grid

2. 
Hai cột: cột 1 rộng 600px, cột 2 rộng 300px

3. 
Mobile-first là cách thiết kế và viết code giao diện bắt đầu từ màn hình nhỏ (điện thoại) trước, sau đó mới mở rộng dần lên màn hình lớn hơn (tablet, laptop, desktop)

CSS bên ngoài là cho điện thoại. min-width nghĩa là "từ cỡ này trở lên thì thêm những rule này". Nếu dùng max-width, ta phải viết cho máy tính trước, rồi viết thêm rule để gỡ bỏ những gì không hợp với màn nhỏ.

4. 
Tránh cộng dồn khoảng cách