1. Điểm khác nhau chính

- Vị trí: padding nằm bên trong border; margin nằm bên ngoài border.
- Màu nền (background): padding nhận màu nền của phần tử; margin luôn trong suốt và không có màu nền.
- Kích thước & vùng bấm: padding làm tăng kích thước vùng chứa và mở rộng vùng có thể bấm (clickable area), ví dụ trên nút bấm; margin không làm phần tử to ra mà chỉ đẩy các phần tử khác ra xa.

Khi nào dùng padding?

- Làm nút bấm (button) hoặc thẻ (card) trông đầy đặn, dễ đọc và dễ bấm hơn.
- Giữ chữ hoặc nội dung bên trong không bị dính sát vào viền.

Khi nào dùng margin?

- Tạo khoảng cách giữa các phần tử độc lập (các đoạn văn, ảnh, card nằm cạnh nhau).
- Căn giữa khối theo chiều ngang bằng margin: 0 auto hoặc dịch chuyển vị trí bằng margin âm

2. 
- Khi không có box-sizing: border-box 

Phép tính. 300px + 20px * 2 + 5px * 2 = 350px.

- Khi có box-sizing: border-box. Hộp rộng đúng 300px.

Phép tính chiều rộng vùng nội dung thực tế còn lại. 300px - (20px × 2) - (5px × 2) = 250px.

3. 
rem: tính theo cỡ chữ của thẻ <html>, thường là 16px. Đặt ở đâu cũng ra cùng một số: 0.5rem luôn là 8px.
em: tính theo cỡ chữ của chính phần tử đó. Một nút có font-size: 20px thì padding: 0.5em là 10px. Nút có chữ to hơn thì padding cũng to theo.

4. Với `<p class="intro">` và hai rule `.intro { color: blue; }` rồi `p { color: red; }` (rule `p` viết sau), chữ màu màu xanh vì class > p 