# Bài 2: CSS cơ bản

**Mục tiêu:** hiểu selector, cascade, box model, màu, font và đơn vị, rồi dùng chúng để làm đẹp trang profile ở Bài 1. Chưa cần dàn layout, vì Flexbox là Bài 3 và Grid là Bài 4.

---

## 1. Gắn CSS vào trang

Có 3 cách, nhưng chỉ nên dùng cách thứ ba:

```html
<p style="color: red">Inline: viết thẳng vào thẻ. Khó sửa, tránh dùng.</p>

<style> p { color: red; } </style>   <!-- Trong <head>. Chỉ hợp cho thử nhanh. -->

<link rel="stylesheet" href="style.css">   <!-- File riêng. Dùng cách này. -->
```

Đây chính là chỗ đúng của `rel="stylesheet"`: trên thẻ `<link>` trong `<head>`, không phải trên `<a>`.

## 2. Cú pháp và selector

```css
selector {
  thuộc-tính: giá-trị;
}
```

| Selector | Chọn | Ví dụ |
|---|---|---|
| `p` | Mọi thẻ `p` | `p { color: #333; }` |
| `.tag` | Phần tử có `class="tag"` | `.tag { font-weight: 700; }` |
| `#lien-he` | Phần tử có `id="lien-he"` | Dùng cho link `#`, hạn chế dùng để style |
| `nav a` | `a` nằm **bên trong** `nav` | `nav a { text-decoration: none; }` |
| `h1, h2` | Cả `h1` và `h2` | `h1, h2 { color: navy; }` |
| `a:hover` | `a` khi rê chuột lên | `a:hover { color: red; }` |
| `*` | Mọi phần tử | Dùng cho reset |

Một phần tử có thể có nhiều class, cách nhau bằng dấu cách: `class="tag muted"`.

## 3. Cascade: khi hai rule cùng nhắm một phần tử

1. **Độ cụ thể (specificity)** cao hơn thì thắng: `#id` > `.class` > `thẻ`.
2. Bằng nhau thì rule **viết sau** thắng.
3. Một số thuộc tính được **kế thừa** từ cha xuống con, ví dụ `color`, `font-family`, `line-height`. Đặt chúng ở `body` là cả trang dùng theo. Còn `padding`, `margin`, `border` thì không kế thừa.

Vì `#id` mạnh quá, rule viết bằng id rất khó ghi đè về sau. Thói quen tốt: **style bằng class, dùng id cho link và JavaScript.**

## 4. Box model

Mọi phần tử là một cái hộp gồm 4 lớp, từ trong ra ngoài:

```
┌──────────── margin (khoảng cách với hộp khác) ────────────┐
│  ┌──────────── border (viền) ───────────────────────────┐  │
│  │  ┌──────────── padding (đệm bên trong) ───────────┐  │  │
│  │  │              content (nội dung)                │  │  │
│  │  └────────────────────────────────────────────────┘  │  │
│  └──────────────────────────────────────────────────────┘  │
└────────────────────────────────────────────────────────────┘
```

```css
.card {
  width: 300px;
  padding: 16px;              /* 4 phía */
  padding: 8px 16px;          /* trên-dưới 8px, trái-phải 16px */
  border: 2px solid #ddd;     /* độ dày, kiểu, màu */
  border-radius: 8px;         /* bo góc */
  margin: 0 auto;             /* trên-dưới 0, trái-phải tự chia đều: căn giữa */
}
```

**Bẫy hay gặp:** mặc định `width` chỉ tính phần content. Hộp trên sẽ rộng 300 + 16×2 + 2×2 = **336px**. Dòng sau làm `width` tính luôn cả padding và border, nên hộp rộng đúng 300px:

```css
*, *::before, *::after { box-sizing: border-box; }
```

Gần như mọi dự án đều mở đầu bằng dòng này.

**block và inline:** `div`, `p`, `section`, `h1` là **block**: chiếm hết chiều ngang, xuống dòng mới. `a`, `strong`, `img` là **inline**: nằm trong dòng chữ, và padding trên-dưới không đẩy được các dòng xung quanh. Muốn link trong nav có padding đàng hoàng, đổi nó thành `display: inline-block`.

Mở DevTools (`F12`) → *Elements* → chọn phần tử → tab *Computed*: bạn sẽ thấy đúng hình hộp ở trên với số đo thật.

## 5. Màu

```css
color: #1f6feb;              /* hex */
color: rgb(31 111 235);      /* rgb */
background: rgb(0 0 0 / 5%); /* có độ trong suốt */
```

Đặt màu thành **biến** để đổi một chỗ là cả trang đổi theo:

```css
:root {
  --mau-nen: #ffffff;
  --mau-chu: #222222;
  --mau-nhan: #1f6feb;
}
a { color: var(--mau-nhan); }
```

## 6. Chữ

```css
body {
  font-family: system-ui, -apple-system, "Segoe UI", Roboto, sans-serif;
  font-size: 1rem;        /* 16px mặc định của trình duyệt */
  line-height: 1.6;       /* không đơn vị: 1.6 lần cỡ chữ */
}
h1 { font-size: 2rem; font-weight: 800; }
.muted { color: #666; font-size: 0.875rem; }
```

`font-family` là một danh sách: máy không có font đầu thì dùng font kế tiếp.

## 7. Đơn vị

| Đơn vị | Tính theo | Dùng cho |
|---|---|---|
| `px` | Điểm ảnh cố định | Viền, bóng, chi tiết nhỏ |
| `rem` | Cỡ chữ của `<html>` (thường 16px) | Cỡ chữ, padding, margin |
| `em` | Cỡ chữ của chính phần tử đó | Padding của nút, để nút to theo chữ |
| `%` | Kích thước của phần tử cha | Chiều rộng |
| `vw`, `vh` | 1% chiều rộng, chiều cao màn hình | Khối chiếm cả màn hình |

Ưu tiên `rem` cho chữ: người dùng tăng cỡ chữ trong trình duyệt thì trang to theo, còn `px` thì không.

---

## Bài tập

Làm trong `01-html-css-js/bai-02/`. Mình đã chép trang profile của bạn từ Bài 1 sang `index.html` và gắn sẵn `style.css`. Thư mục `bai-01` giữ nguyên để so sánh trước và sau.

Mở `index.html` bằng **Live Server**, mỗi lần lưu `style.css` là trình duyệt tự cập nhật.

Mỗi yêu cầu ghi theo dạng: **selector** → **thuộc tính** → *kết quả nhìn thấy*. Giá trị cụ thể (bao nhiêu px, màu gì) bạn tự chọn, trừ chỗ nào đề ghi sẵn.

### BT1. Nền tảng

| Selector | Thuộc tính | Kết quả nhìn thấy |
|---|---|---|
| `*` | `box-sizing: border-box` | Chưa thấy gì khác, nhưng từ giờ `width` tính cả padding và border |
| `body` | `font-family`, `line-height` | Chữ đổi sang font hệ thống, các dòng giãn ra dễ đọc hơn |
| `body` | `max-width: 720px` | Trên màn hình rộng, nội dung không còn kéo dài hết chiều ngang |
| `body` | `margin: 0 auto` | Khối nội dung nằm giữa màn hình |
| `body` | `padding` | Chữ không dính sát mép trái, phải khi thu nhỏ cửa sổ |

### BT2. Màu

**Bước 1.** Viết rule `:root` và khai báo đúng 3 biến (màu tự chọn):

| Biến | Dùng cho |
|---|---|
| `--mau-nen` | Màu nền trang |
| `--mau-chu` | Màu chữ thường |
| `--mau-nhan` | Màu nổi bật: link, viền, nhãn |

**Bước 2.** Dùng các biến đó, viết bằng `var(--ten-bien)`:

| Selector | Thuộc tính | Kết quả nhìn thấy |
|---|---|---|
| `body` | `background-color` dùng `--mau-nen` | Nền cả trang đổi màu |
| `body` | `color` dùng `--mau-chu` | Chữ cả trang đổi màu (nhờ kế thừa) |
| `a` | `color` dùng `--mau-nhan` | Mọi link đổi màu |
| `header` | `border-bottom` dùng `--mau-nhan` | Có một đường kẻ ngang ngay dưới tên và menu |

**Tự kiểm tra:** đổi giá trị `--mau-nhan` trong `:root`, lưu lại. Link và đường kẻ dưới header phải đổi màu cùng lúc. Ngoài `:root` ra, trong file không được có mã màu nào khác (như `#fff` hay `red`).

### BT3. Box model

**Section thành thẻ:**

| Selector | Thuộc tính | Kết quả nhìn thấy |
|---|---|---|
| `section` | `border` | Mỗi mục có khung viền bao quanh |
| `section` | `padding` | Chữ cách khung viền một khoảng, không dính vào viền |
| `section` | `border-radius` | Góc khung bo tròn |
| `section` | `margin-bottom` | Các khung cách nhau, không dính vào nhau |

**Ảnh:**

| Selector | Thuộc tính | Kết quả nhìn thấy |
|---|---|---|
| `img` | `max-width: 100%; height: auto` | Thu nhỏ cửa sổ, ảnh co theo, không lòi ra ngoài khung |

Ngoài ra, tải ảnh về, để trong `bai-02/` (ví dụ `bai-02/anh.jpg`), rồi sửa `src` trong `index.html` thành `src="anh.jpg"`.

**Bảng kỹ năng:**

| Selector | Thuộc tính | Kết quả nhìn thấy |
|---|---|---|
| `table` | `border-collapse: collapse` | Viền các ô gộp thành một đường, không còn viền đôi |
| `table` | `width: 100%` | Bảng rộng bằng khung section |
| `th, td` | `border`, `padding` | Mỗi ô có viền, chữ cách viền ô |
| `th` | `background-color` (dùng biến hoặc thêm biến mới trong `:root`) | Dòng tiêu đề của bảng có nền khác các dòng dưới |

### BT4. Thanh điều hướng

| Selector | Thuộc tính | Kết quả nhìn thấy |
|---|---|---|
| `nav a` | `text-decoration: none` | 3 link trong menu không còn gạch chân |
| `nav a` | `display: inline-block`, `padding` | Mỗi link thành một "nút" có khoảng đệm |
| `nav a:hover` | `background-color` hoặc `color` | Rê chuột lên link thì link đổi màu, bỏ chuột ra thì trở lại như cũ |

Dùng `nav a` chứ không dùng `a`, để link GitHub ở phần Liên hệ không bị ảnh hưởng.

### BT5. Class

**Sửa `index.html` trước:**
- Thẻ `<p>` trong footer: thêm `class="muted"`.
- 4 ô ở cột "Đang học ở trạm": bọc chữ bên trong bằng `<span class="tag">`, ví dụ `<td><span class="tag">Trạm 1</span></td>`.

**Rồi viết CSS:**

| Selector | Thuộc tính | Kết quả nhìn thấy |
|---|---|---|
| `.muted` | `font-size` nhỏ hơn `1rem`, `opacity` hoặc `color` nhạt hơn | Dòng bản quyền nhỏ và mờ hơn chữ thường |
| `.tag` | `background-color` (dùng `--mau-nhan`), `color` | Chữ "Trạm 1" có nền màu |
| `.tag` | `padding`, `border-radius` | Thành một nhãn nhỏ bo góc |

Không viết selector nào bắt đầu bằng `#` trong `style.css`.

### BT6. Câu hỏi

Trả lời trong `bai-02/tra-loi.md`, **bằng lời của bạn**, mỗi câu một dòng có đánh số:
1. `padding` và `margin` khác nhau thế nào? Khi nào dùng cái nào?
2. Một hộp có `width: 300px; padding: 20px; border: 5px solid`. Hộp rộng bao nhiêu px khi không có `box-sizing: border-box`, và khi có? Ghi cả phép tính.
3. `rem` và `em` khác nhau ở đâu?
4. Với `<p class="intro">` và hai rule `.intro { color: blue; }` rồi `p { color: red; }` (rule `p` viết sau), chữ màu gì? Vì sao?

### Kiểm tra bằng DevTools

Bấm `F12` → tab *Elements* → chọn một thẻ `section` → bên phải chọn tab *Computed*. Hình hộp ở đó phải hiện đúng số padding và border bạn đã viết.

### Git

Commit sau mỗi bài tập. Gợi ý tên commit:

| Sau | Tên commit |
|---|---|
| BT1 | `Thêm nền tảng CSS cho profile` |
| BT2 | `Thêm biến màu` |
| BT3 | `Style section, ảnh và bảng` |
| BT4 | `Style thanh điều hướng` |
| BT5 | `Thêm class muted và tag` |
| BT6 | `Trả lời câu hỏi bài 2` |

Đọc thêm: [MDN: CSS styling basics](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Styling_basics).

---

Làm xong, nói **"chấm bài 2"**.
