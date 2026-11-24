# Bài 1: HTML cơ bản và thẻ ngữ nghĩa

**Mục tiêu:** viết một trang HTML đúng cấu trúc, dùng thẻ đúng ý nghĩa. Đây là khung xương của trang profile, dự án nhỏ đầu tiên của trạm 1.

---

## 1. HTML là gì

HTML mô tả **nội dung là gì**, không phải trông ra sao (đó là việc của CSS). `<h1>` nghĩa là "tiêu đề quan trọng nhất", không phải "chữ to".

Khung của mọi trang:

```html
<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Tên hiện trên tab</title>
</head>
<body>
  <!-- Nội dung người dùng nhìn thấy -->
</body>
</html>
```

> Trong VS Code, file `.html` trống gõ `!` rồi `Tab` là ra khung này.

## 2. Các thẻ hay dùng

```html
<h1>Tiêu đề chính (mỗi trang một cái)</h1>
<h2>Tiêu đề mục</h2>
<p>Đoạn văn. <strong>Quan trọng</strong> và <em>nhấn mạnh</em>.</p>

<a href="https://github.com">Link ra ngoài</a>
<a href="#lien-he">Link tới phần có id="lien-he"</a>

<img src="anh.jpg" alt="Mô tả ảnh cho người không xem được ảnh">

<ul>  <li>Danh sách không thứ tự</li> </ul>
<ol>  <li>Danh sách có thứ tự</li> </ol>

<table>
  <thead><tr><th>Kỹ năng</th><th>Mức độ</th></tr></thead>
  <tbody><tr><td>HTML</td><td>Mới học</td></tr></tbody>
</table>
```

## 3. Thẻ ngữ nghĩa (semantic)

Thay vì `<div>` ở khắp nơi, dùng thẻ nói lên vai trò:

```
<header>   đầu trang: logo, tên, menu
<nav>      thanh điều hướng
<main>     nội dung chính (mỗi trang một cái)
<section>  một phần có tiêu đề riêng
<article>  một khối nội dung độc lập (bài viết, dự án)
<footer>   chân trang
```

Lợi ích: trình đọc màn hình hiểu trang, Google hiểu trang, và bạn đọc lại code cũng dễ hơn.

## 4. Chạy thử

Cài extension **Live Server** trong VS Code → chuột phải file HTML → **Open with Live Server**. Mỗi lần lưu, trình duyệt tự tải lại.

Mở **DevTools** (`F12`) → tab *Elements* để xem cây HTML.

---

## Bài tập

Làm trong `01-html-css-js/bai-01/`. File khởi đầu `index.html` đã có sẵn.

**BT1. Trang profile (chỉ HTML, chưa CSS).** Hoàn thành `index.html` với:
- `<header>` có tên bạn và một `<nav>` gồm 3 link tới các mục bên dưới (`#gioi-thieu`, `#ky-nang`, `#lien-he`).
- `<main>` gồm:
  - `section#gioi-thieu`: tiêu đề `h2`, một đoạn giới thiệu, một ảnh (ảnh bất kỳ, nhớ `alt`).
  - `section#ky-nang`: một **bảng** 3 cột: Kỹ năng, Mức độ, Đang học ở trạm nào. Ít nhất 4 dòng.
  - `section#du-an`: một `ol` liệt kê 3 dự án bạn sẽ làm trong lộ trình, mỗi cái là một `<article>` có `h3` và một câu mô tả.
  - `section#lien-he`: link GitHub của bạn.
- `<footer>` có dòng bản quyền với năm hiện tại.

**BT2. Kiểm tra.** Dán code vào https://validator.w3.org/#validate_by_input và sửa đến khi không còn lỗi.

**BT3. Câu hỏi** (trả lời trong `bai-01/tra-loi.md`):
1. Vì sao `alt` của ảnh quan trọng?
2. Khi nào dùng `<section>`, khi nào dùng `<div>`?
3. Có nên dùng `<h3>` chỉ vì muốn chữ nhỏ hơn `<h2>` không? Vì sao?

**Git:** commit sau mỗi bài tập. Ví dụ `Thêm khung trang profile`, `Thêm bảng kỹ năng`.

---

Làm xong, nói **"chấm bài 1"**.
