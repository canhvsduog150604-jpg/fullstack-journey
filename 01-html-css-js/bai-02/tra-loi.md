1. Điểm khác nhau chính

• Vị trí: padding nằm bên trong border; margin nằm bên ngoài border.
• Màu nền (background): padding nhận màu nền của phần tử; margin luôn trong suốt và không có màu nền.
• Kích thước & vùng bấm: padding làm tăng kích thước vùng chứa và mở rộng vùng có thể bấm (clickable area), ví dụ trên nút bấm; margin không làm phần tử to ra mà chỉ đẩy các phần tử khác ra xa.
• Giá trị đặc biệt: margin chấp nhận giá trị âm (kéo phần tử lại gần hoặc chồng lên nhau) và auto (thường dùng margin: 0 auto để căn giữa khối). padding không nhận giá trị âm hay auto.
• Gộp lề (margin collapse): Hai margin dọc liền kề có thể gộp lại thành một khoảng cách lớn nhất; padding không bị gộp lề.

Khi nào dùng padding?

• Làm nút bấm (button) hoặc thẻ (card) trông đầy đặn, dễ đọc và dễ bấm hơn.
• Giữ chữ hoặc nội dung bên trong không bị dính sát vào viền hoặc nền màu của hộp.

Khi nào dùng margin?

• Tạo khoảng cách giữa các phần tử độc lập (các đoạn văn, ảnh, card nằm cạnh nhau).
• Căn giữa khối theo chiều ngang bằng margin: 0 auto hoặc dịch chuyển vị trí bằng margin âm

2. 
- Khi không có box-sizing: border-box (mặc định là content-box)

• Cách hoạt động. Thuộc tính width: 300px chỉ áp dụng cho vùng nội dung bên trong; padding và border ở hai bên trái, phải sẽ được cộng thêm vào kích thước tổng.
• Phép tính. 300px (width) + 20px (padding trái) + 20px (padding phải) + 5px (border trái) + 5px (border phải) = 350px.

- Khi có box-sizing: border-box

• Cách hoạt động. Thuộc tính width: 300px bao gồm cả nội dung, padding và border; phần nội dung bên trong sẽ tự động thu hẹp lại để tổng chiều rộng không vượt quá 300px.
• Phép tính tổng chiều rộng. 300px (giữ nguyên theo giá trị width đã khai báo).
• Phép tính chiều rộng vùng nội dung thực tế còn lại. 300px - (20px × 2) - (5px × 2) = 250px.

3. 
rem:
• font-size của thẻ <html> (mặc định thường là 16px).
• Đồng nhất trên toàn trang; 1.5rem luôn bằng 24px (nếu html là 16px) dù lồng bao nhiêu cấp thẻ.
• Nên dùng khi: Đặt cỡ chữ (font-size), khoảng cách bố cục tổng thể (margin, gap) để giữ tỉ lệ nhất quán toàn trang và hỗ trợ người dùng phóng to chữ trên trình duyệt.

em:
• font-size của phần tử cha gần nhất (khi dùng cho font-size), hoặc của chính phần tử đó (khi dùng cho padding, margin, width).
• Dễ bị cộng dồn (compounding) khi lồng nhiều thẻ cha con cùng dùng em.
• Nên dùng khi: Đặt padding, margin bên trong một component (như button, badge) để khoảng cách tự co giãn tỉ lệ thuận theo cỡ chữ của chính component đó.

4. Với `<p class="intro">` và hai rule `.intro { color: blue; }` rồi `p { color: red; }` (rule `p` viết sau), chữ màu màu xanh vì class > p 