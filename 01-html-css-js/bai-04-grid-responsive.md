# Bài 4: Grid và responsive

**Mục tiêu:** dùng CSS Grid để chia bố cục theo hàng và cột cùng lúc, và dùng media query để trang có bố cục khác nhau trên điện thoại và máy tính. Áp dụng lên trang profile: trên máy tính, phần Giới thiệu và Liên hệ nằm cạnh nhau, các dự án tự chia cột. Trên điện thoại, mọi thứ xếp thành một cột.

---

## 1. Flexbox hay Grid?

| | Flexbox | Grid |
|---|---|---|
| Xếp theo | **Một chiều**: một hàng hoặc một cột | **Hai chiều**: hàng và cột cùng lúc |
| Ai quyết định kích thước | Nội dung của item | Khung lưới do container vẽ sẵn |
| Hợp với | Thanh menu, một hàng nút, ảnh cạnh chữ | Bố cục cả trang, lưới thẻ, bảng ảnh |

Hai cái không thay thế nhau. Một trang thường dùng Grid cho bố cục lớn, Flexbox cho từng khối nhỏ bên trong.

## 2. Vẽ lưới

```css
.luoi {
  display: grid;
  grid-template-columns: 200px 1fr 1fr;   /* 3 cột */
  gap: 16px;
}
```

```
┌────────┐ ┌──────────────┐ ┌──────────────┐
│ 200px  │ │     1fr      │ │     1fr      │
└────────┘ └──────────────┘ └──────────────┘
           └──── phần còn lại chia đôi ────┘
```

- Mỗi giá trị trong `grid-template-columns` là một cột.
- Các item tự điền vào lưới từ trái sang phải, hết hàng thì xuống hàng mới. Không cần khai báo số hàng.
- `gap` giống hệt `gap` của Flexbox.

### Đơn vị `fr`

`fr` là "một phần của chỗ còn trống". Trình duyệt trừ các cột cố định và `gap` trước, rồi chia phần còn lại theo tỉ lệ:

```css
grid-template-columns: 2fr 1fr;   /* cột trái gấp đôi cột phải */
```

Khung rộng 600px (không tính gap): cột trái 400px, cột phải 200px.

### `repeat()` và `minmax()`

```css
grid-template-columns: repeat(3, 1fr);   /* = 1fr 1fr 1fr */
grid-template-columns: minmax(200px, 1fr) 2fr;   /* cột đầu: ít nhất 200px, nhiều nhất 1fr */
```

### Lưới tự chia cột

Mẫu hay dùng nhất của Grid, **không cần media query**:

```css
.the-list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
  gap: 16px;
}
```

Đọc thành lời: *"Xếp càng nhiều cột càng tốt (`auto-fit`), miễn mỗi cột rộng ít nhất 180px. Còn dư chỗ thì các cột giãn đều ra (`1fr`)."*

Màn hình rộng: 3 cột. Hẹp lại: 2 cột. Điện thoại: 1 cột. Trình duyệt tự tính.

## 3. Đặt tên vùng: `grid-template-areas`

Vẽ bố cục bằng chữ, mỗi chuỗi là một hàng:

```css
.trang {
  display: grid;
  grid-template-columns: 2fr 1fr;
  grid-template-areas:
    "chinh  phu"
    "duoi   duoi";
}
.khoi-a { grid-area: chinh; }
.khoi-b { grid-area: phu; }
.khoi-c { grid-area: duoi; }
```

```
┌──────────────────┐ ┌────────┐
│      chinh       │ │  phu   │
└──────────────────┘ └────────┘
┌─────────────────────────────┐
│            duoi             │   ← tên lặp lại 2 lần = chiếm 2 cột
└─────────────────────────────┘
```

Quy tắc: mỗi chuỗi phải có **đúng số cột** đã khai báo. Một tên lặp lại nghĩa là khối đó trải qua nhiều ô. Tên viết bằng chữ, không có dấu nháy khi dùng trong `grid-area`.

## 4. Media query: CSS theo cỡ màn hình

```css
/* Viết cho mọi màn hình */
h1 { font-size: 1.5rem; }

/* Chỉ áp dụng khi màn hình rộng từ 768px trở lên */
@media (min-width: 768px) {
  h1 { font-size: 2rem; }
}
```

Rule trong `@media` chỉ có tác dụng khi điều kiện đúng. Vì nó nằm **sau** trong file, nó ghi đè rule phía trên (cùng độ cụ thể, rule viết sau thắng: đúng như Bài 2).

### Mobile-first

Có hai cách viết:

| Cách | Viết mặc định cho | Media query dùng | |
|---|---|---|---|
| **Mobile-first** | Điện thoại | `min-width`: thêm dần cho màn to | ✅ Dùng cách này |
| Desktop-first | Máy tính | `max-width`: gỡ dần cho màn nhỏ | Dễ rối hơn |

Mobile-first dễ hơn vì bố cục điện thoại thường là một cột đơn giản. Màn hình to thì **thêm** cột, thêm khoảng cách. Ít phải viết rule để "gỡ" cái đã viết.

**Đặt tất cả media query ở cuối file**, sau các rule thường. Đặt ở đầu thì rule thường viết sau sẽ đè mất.

Bài này dùng một mốc duy nhất: **768px** (khoảng cỡ máy tính bảng dựng đứng).

### Thử trên DevTools

`F12` → `Ctrl + Shift + M` → ở thanh trên cùng, gõ chiều rộng: `375` cho điện thoại, `1024` cho máy tính. Kéo dần từ 375 lên 1024 để thấy bố cục đổi đúng lúc qua mốc 768.

---

## Bài tập

Làm trong `01-html-css-js/bai-04/`. Mình đã chép trang profile từ Bài 3 sang: `index.html`, `NvM.jpg`, `style.css` (giữ nguyên CSS Bài 2 và Bài 3 của bạn, cuối file có chỗ trống cho từng bài tập).

Mỗi yêu cầu ghi theo dạng: **selector** → **thuộc tính** → *kết quả nhìn thấy*. Giá trị px tự chọn, trừ chỗ đề ghi sẵn.

Mỗi bài tập kiểm tra ở **hai cỡ**: 375px (điện thoại) và 1024px (máy tính).

### BT1. Bố cục trang bằng Grid

**Mục tiêu:** điện thoại 1 cột như hiện giờ. Máy tính:

```
┌──────────────────────────┐ ┌────────────┐
│       Giới thiệu         │ │  Liên hệ   │
└──────────────────────────┘ └────────────┘
┌───────────────────────────────────────────┐
│                 Kỹ năng                   │
└───────────────────────────────────────────┘
┌───────────────────────────────────────────┐
│                  Dự án                    │
└───────────────────────────────────────────┘
```

**Sửa `index.html` trước.** Thêm class cho 4 thẻ `section` (giữ nguyên `id`, vì link trong menu cần nó):

| Thẻ | Thêm |
|---|---|
| `<section id="gioi-thieu">` | `class="khu-gioi-thieu"` |
| `<section id="ky-nang">` | `class="khu-ky-nang"` |
| `<section id="du-an">` | `class="khu-du-an"` |
| `<section id="lien-he">` | `class="khu-lien-he"` |

**Rồi viết CSS (phần cho mọi màn hình):**

| Selector | Thuộc tính | Kết quả nhìn thấy |
|---|---|---|
| `body` (rule có sẵn) | Đổi `max-width` từ `720px` thành `960px` | Trang rộng hơn trên máy tính, đủ chỗ cho 2 cột |
| `main` | `display: grid`, `gap: 16px` | Chưa đổi gì nhiều: vẫn 1 cột, các section cách nhau |
| `main` | `grid-template-areas` gồm 4 chuỗi, mỗi chuỗi 1 tên: `"gioi-thieu" "ky-nang" "du-an" "lien-he"` (viết mỗi chuỗi một dòng) | Chưa thấy khác: vẫn 1 cột. Đây là bố cục cho điện thoại |
| `section` (rule có sẵn) | **Xóa** `margin-bottom` | Khoảng cách giữa các section giờ do `gap` lo. Giữ cả hai thì khoảng cách bị cộng dồn |
| `.khu-gioi-thieu` | `grid-area: gioi-thieu` | Section nằm đúng vùng tên của nó |
| `.khu-ky-nang` | `grid-area: ky-nang` | Như trên |
| `.khu-du-an` | `grid-area: du-an` | Như trên |
| `.khu-lien-he` | `grid-area: lien-he` | Như trên |

**Phải khai báo `grid-template-areas` trước khi dùng `grid-area`.** Nếu một item dùng tên vùng không có trong `grid-template-areas`, trình duyệt tự tạo một ô ngầm ngoài lưới, và mọi item cùng dồn vào ô đó, chồng lên nhau.

Phần `grid-template-columns` và `grid-template-areas` 2 cột cho máy tính viết ở BT3, trong media query. Nó sẽ ghi đè bố cục 1 cột ở trên.

**Tự kiểm tra ở 375px:** 4 section xếp một cột, khoảng cách giữa chúng đều nhau và bằng `gap`.

### BT2. Dự án: đổi từ Flexbox sang Grid

**Xóa** các thuộc tính Flexbox của Bài 3 cho phần dự án:

| Selector | Xóa |
|---|---|
| `.du-an-list` | `display: flex`, `flex-wrap: wrap` |
| `.du-an-list > li` | Cả rule (`flex: 1 1 180px`) |

Giữ nguyên `gap`, `list-style`, `padding` của `.du-an-list` và toàn bộ rule `.du-an-list article`, `.du-an-list h3`.

**Rồi thêm:**

| Selector | Thuộc tính | Kết quả nhìn thấy |
|---|---|---|
| `.du-an-list` | `display: grid` | Các thẻ vẫn chồng một cột |
| `.du-an-list` | `grid-template-columns: repeat(auto-fit, minmax(180px, 1fr))` | Máy tính: 3 thẻ nằm một hàng, rộng bằng nhau. Điện thoại: 1 cột |

**Tự kiểm tra:** kéo dần từ 375 lên 1024. Số cột đổi 1 → 2 → 3 mà **không có media query nào**. Ba khung vẫn cao bằng nhau.

### BT3. Media query

Viết **ở cuối file**, trong **một** khối `@media (min-width: 768px) { ... }`. Bên ngoài khối là phần cho điện thoại.

**Phần cho điện thoại (ngoài `@media`):**

| Selector | Thuộc tính | Kết quả nhìn thấy ở 375px |
|---|---|---|
| `h1` | `font-size: 1.5rem` | Tên nhỏ lại, không chiếm 2 dòng |
| `header` (rule có sẵn) | Thêm `flex-direction: column`, đổi `align-items` thành `flex-start` | Menu nằm hẳn dưới tên, thẳng mép trái |

**Phần cho máy tính (trong `@media (min-width: 768px)`):**

| Selector | Thuộc tính | Kết quả nhìn thấy ở 1024px |
|---|---|---|
| `h1` | `font-size: 2rem` | Tên to lại |
| `header` | `flex-direction: row`, `align-items: center` | Tên trái, menu phải như Bài 3 |
| `main` | `grid-template-columns: 2fr 1fr` | Lưới có 2 cột, cột trái gấp đôi |
| `main` | `grid-template-areas` theo hình ở BT1 | Giới thiệu và Liên hệ nằm cạnh nhau. Kỹ năng và Dự án trải hết 2 cột |

Gợi ý cho `grid-template-areas`: cần 3 chuỗi (3 hàng), mỗi chuỗi 2 tên (2 cột). Hàng 2 và 3 lặp tên vì mỗi khối chiếm cả 2 cột.

**Tự kiểm tra:**
- 375px: header xếp dọc, 4 section một cột.
- 1024px: bố cục đúng hình ở BT1.
- Kéo qua mốc 768px: bố cục đổi đúng lúc đó.
- Bấm 3 link trong menu: vẫn nhảy đúng tới section (vì `id` vẫn còn).

### BT4. Luyện tập: Grid Garden

Chơi [Grid Garden](https://cssgridgarden.com/) (đổi ngôn ngữ ở góc trên phải), **từ level 1 đến level 28**.

Chụp màn hình khi qua level 28, lưu thành `bai-04/grid-garden.png`.

### BT5. Câu hỏi

Trả lời trong `bai-04/tra-loi.md`, mỗi câu một dòng có đánh số, 1 đến 2 câu mỗi ý:

1. Khi nào dùng Grid, khi nào dùng Flexbox? Cho một ví dụ mỗi loại trên trang profile của bạn.
2. Khung rộng 900px (không tính gap), `grid-template-columns: 2fr 1fr`. Mỗi cột rộng bao nhiêu?
3. Mobile-first là gì? Vì sao media query viết bằng `min-width` mà không phải `max-width`?
4. Ở BT1, vì sao phải xóa `margin-bottom` của `section` khi đã có `gap`?

### Git

| Sau | Tên commit |
|---|---|
| Lấy file bài 4 | `Thêm bài 4: Grid và responsive` |
| BT1 | `Chia bố cục trang bằng grid` |
| BT2 | `Đổi danh sách dự án sang grid` |
| BT3 | `Thêm media query cho điện thoại và máy tính` |
| BT4 | `Thêm ảnh Grid Garden` |
| BT5 | `Trả lời câu hỏi bài 4` |

Đọc thêm: [MDN: Grids](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/CSS_layout/Grids), [MDN: Media query fundamentals](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/CSS_layout/Media_queries), [CSS-Tricks: A Complete Guide to Grid](https://css-tricks.com/snippets/css/complete-guide-grid/).

---

Làm xong, nói **"chấm bài 4"**.
