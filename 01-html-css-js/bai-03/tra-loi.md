1. 
- justify-content căn theo trục chính, align-items căn theo trục phụ.

2. 
- justify-content: center sẽ căn theo chiều dọc vì trục main giờ đã thành trục dọc

3. 
- flex chỉ có tác dụng với con trực tiếp của flex container. Container là ol, nên con trực tiếp là li. Nếu viết flex cho article, dòng đó không có tác dụng gì, vì cha của article là li, mà li không phải flex container.

4. gap chỉ tạo khoảng cách giữa các phần tử liền kề, nên không thừa khoảng ở hai đầu. Dùng margin thì phải xử lý riêng item đầu hoặc item cuối, giống rule first-child