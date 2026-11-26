# Bài 3: Flexbox

**Mục tiêu:** dùng Flexbox để xếp các phần tử theo hàng hoặc cột, căn giữa, chia khoảng cách, và tự xuống hàng khi màn hình hẹp. Áp dụng ngay lên trang profile: đưa menu lên cùng hàng với tên, đặt ảnh cạnh đoạn giới thiệu, xếp 3 dự án thành 3 thẻ nằm ngang.

---

## 1. Container và item

Flexbox luôn có hai vai:

- **Flex container:** phần tử cha, được đặt `display: flex`.
- **Flex item:** các **con trực tiếp** của nó. Cháu chắt không bị ảnh hưởng.

```html
<nav>                                 <!-- container -->
  <a href="#gioi-thieu">Giới thiệu</a>  <!-- item -->
  <a href="#ky-nang">Kỹ năng</a>        <!-- item -->
  <a href="#lien-he">Liên hệ</a>        <!-- item -->
</nav>
```

```css
nav { display: flex; }
```

Chỉ một dòng này, 3 link đã nằm thành một hàng.

**Quy tắc quan trọng nhất:** thuộc tính để xếp item (`justify-content`, `align-items`, `gap`, `flex-wrap`) viết cho **cha**. Thuộc tính để một item co giãn (`flex`) viết cho **con**.

## 2. Hai trục

```
flex-direction: row (mặc định)

  trục chính (main axis) →
  ┌──────┐ ┌──────┐ ┌──────┐
  │  1   │ │  2   │ │  3   │   ↓ trục phụ (cross axis)
  └──────┘ └──────┘ └──────┘
```

| `flex-direction` | Item xếp theo | Trục chính | Trục phụ |
|---|---|---|---|
| `row` (mặc định) | Hàng ngang | Ngang → | Dọc ↓ |
| `column` | Cột dọc | Dọc ↓ | Ngang → |

Mọi thuộc tính căn chỉnh đều nói theo **trục**, không nói theo "ngang" hay "dọc". Đổi `flex-direction` là các trục đổi chỗ cho nhau.

## 3. Căn trên trục chính: `justify-content`

```
flex-start       [1][2][3]·········
center           ·····[1][2][3]·····
flex-end         ·········[1][2][3]
space-between    [1]·····[2]·····[3]   ← hai đầu sát mép
space-around     ·[1]···[2]···[3]·
space-evenly     ··[1]··[2]··[3]··     ← mọi khoảng bằng nhau
```

## 4. Căn trên trục phụ: `align-items`

Khi các item cao khác nhau trong một hàng:

```
stretch (mặc định)   flex-start        center            flex-end
┌──┐┌──┐┌──┐         ┌──┐┌──┐┌──┐      ┌──┐              
│1 ││2 ││3 │         │1 ││2 ││3 │      │1 │┌──┐┌──┐      ┌──┐┌──┐┌──┐
│  ││  ││  │         └──┘│  │└──┘      │  ││2 ││3 │      │1 ││2 ││3 │
└──┘└──┘└──┘             └──┘          └──┘└──┘└──┘      └──┘└──┘└──┘
cao bằng nhau        dính mép trên     nằm giữa          dính mép dưới
```

`stretch` là mặc định, nên các item trong một hàng flex tự cao bằng nhau. Với ảnh, điều này thường làm ảnh bị kéo méo: đặt `align-items: flex-start` để tránh.

**Căn giữa cả hai chiều**, mẫu hay dùng nhất:

```css
.hop {
  display: flex;
  justify-content: center;   /* giữa theo trục chính */
  align-items: center;       /* giữa theo trục phụ */
}
```

## 5. Khoảng cách và xuống hàng

```css
.the-list {
  display: flex;
  gap: 16px;          /* khoảng cách giữa các item, không thừa ở hai đầu */
  flex-wrap: wrap;    /* hết chỗ thì xuống hàng, thay vì ép item co lại */
}
```

- **`gap` tốt hơn `margin`** cho khoảng cách giữa các item: không phải xử lý item đầu, item cuối, và không bị thừa khoảng ở mép.
- Mặc định là `flex-wrap: nowrap`: mọi item bị ép nằm trên một hàng, dù có bị bóp nhỏ đến đâu.

## 6. Item co giãn: `flex`

Viết cho **item**, không phải cho container:

| Viết | Nghĩa |
|---|---|
| `flex: 1` | Chia đều phần chỗ trống còn lại với các item cùng có `flex: 1` |
| `flex: 2` | Lấy gấp đôi phần của item có `flex: 1` |
| `flex: none` | Giữ nguyên kích thước, không co không giãn |
| `flex: 1 1 200px` | Bắt đầu từ 200px, được giãn (số 1 đầu), được co (số 1 thứ hai) |

Mẫu "thẻ tự xuống hàng" hay dùng:

```css
.cards { display: flex; flex-wrap: wrap; gap: 16px; }
.cards > * { flex: 1 1 200px; }
```

Màn hình rộng: các thẻ chia đều một hàng. Màn hình hẹp, không đủ 200px cho mỗi thẻ: thẻ tự xuống hàng.

Selector `.cards > *` nghĩa là "mọi con trực tiếp của `.cards`". Dấu `>` chỉ chọn con, không chọn cháu.

## 7. Ba mẫu sẽ dùng mãi

```css
/* Logo bên trái, menu bên phải */
header { display: flex; justify-content: space-between; align-items: center; }

/* Chữ chiếm phần còn lại, ảnh giữ cỡ */
.media { display: flex; gap: 16px; align-items: flex-start; }
.media p   { flex: 1; }
.media img { flex: none; }

/* Hàng thẻ tự xuống hàng */
.cards { display: flex; flex-wrap: wrap; gap: 16px; }
.cards > * { flex: 1 1 200px; }
```

**Xem bằng DevTools:** trong tab *Elements*, phần tử nào có `display: flex` sẽ có nhãn nhỏ **flex** bên cạnh. Bấm vào nhãn đó, trình duyệt vẽ khung từng item và khoảng `gap` lên trang.

---

## Bài tập

Làm trong `01-html-css-js/bai-03/`. Mình đã chép trang profile từ Bài 2 sang: `index.html`, `NvM.jpg`, và `style.css` (giữ nguyên CSS Bài 2 của bạn, cuối file có chỗ trống cho từng bài tập).

Mở bằng **Live Server**. Mỗi bài tập làm xong thì bấm `Ctrl + Shift + M` trong DevTools để xem cả bản điện thoại.

Mỗi yêu cầu ghi theo dạng: **selector** → **thuộc tính** → *kết quả nhìn thấy*. Giá trị px tự chọn.

### BT1. Header: tên bên trái, menu bên phải

| Selector | Thuộc tính | Kết quả nhìn thấy |
|---|---|---|
| `header` | `display: flex` | Tên và menu nằm cùng một hàng |
| `header` | `justify-content: space-between` | Tên dính mép trái, menu dính mép phải |
| `header` | `align-items: center` | Menu nằm giữa theo chiều cao của tên, không bị lệch lên trên |
| `header` | `flex-wrap: wrap` | Thu cửa sổ thật hẹp: menu xuống dưới tên thay vì bị bóp méo |

**Tự kiểm tra:** đường kẻ dưới header (từ Bài 2) vẫn chạy hết chiều ngang.

### BT2. Nav: dùng gap thay cho padding đầu

| Selector | Thuộc tính | Kết quả nhìn thấy |
|---|---|---|
| `nav` | `display: flex` | 3 link vẫn nằm một hàng |
| `nav` | `gap` | Các link cách nhau đều |
| `nav a:first-child` | **Xóa cả rule này** | Không còn cần, vì menu giờ nằm bên phải chứ không thẳng hàng với tên |

**Tự kiểm tra:** rê chuột lên link, nền hover vẫn bao quanh chữ đều 4 phía.

### BT3. Giới thiệu: chữ bên trái, ảnh bên phải

**Sửa `index.html` trước.** Trong `section#gioi-thieu`, bọc thẻ `<p>` và thẻ `<img>` bằng một `<div class="intro">`. Thẻ `<h2>` để ngoài, vẫn nằm trên cùng:

```html
<section id="gioi-thieu">
  <h2>Giới thiệu</h2>
  <div class="intro">
    <p>...</p>
    <img ...>
  </div>
</section>
```

**Rồi viết CSS:**

| Selector | Thuộc tính | Kết quả nhìn thấy |
|---|---|---|
| `.intro` | `display: flex` | Đoạn văn và ảnh nằm cạnh nhau |
| `.intro` | `gap` | Chữ và ảnh có khoảng cách |
| `.intro` | `align-items: flex-start` | Ảnh không bị kéo dãn theo chiều cao đoạn văn |
| `.intro p` | `flex: 1 1 250px` | Đoạn văn chiếm hết phần còn lại bên trái |
| `.intro img` | `width: 200px` (hoặc tự chọn) và `flex: none` | Ảnh giữ đúng cỡ, không bị co lại |
| `.intro` | `flex-wrap: wrap` | Màn hình hẹp: ảnh xuống dưới đoạn văn |

Vì sao `.intro p` dùng `flex: 1 1 250px` mà không chỉ `flex: 1`: số `250px` nói "đoạn văn cần ít nhất khoảng 250px". Khi hàng không còn đủ 250px cho chữ cộng thêm chỗ cho ảnh, ảnh mới xuống hàng. Chỉ viết `flex: 1` thì đoạn văn chịu co lại mãi, thành một cột chữ rất hẹp bên cạnh ảnh.

**Tự kiểm tra:** ở bản máy tính, ảnh nằm bên phải chữ. Ở bản điện thoại (`Ctrl + Shift + M`), ảnh nằm dưới chữ.

### BT4. Dự án: 3 thẻ nằm ngang

**Sửa `index.html` trước.** Thêm `class="du-an-list"` vào thẻ `<ol>` trong `section#du-an`.

| Selector | Thuộc tính | Kết quả nhìn thấy |
|---|---|---|
| `.du-an-list` | `display: flex`, `flex-wrap: wrap`, `gap` | 3 dự án nằm thành hàng, có khoảng cách |
| `.du-an-list` | `list-style: none`, `padding: 0` | Mất số thứ tự 1, 2, 3 và khoảng thụt lề bên trái |
| `.du-an-list > li` | `flex: 1 1 180px` | 3 thẻ rộng bằng nhau. Màn hình hẹp: thẻ xuống hàng |
| `.du-an-list article` | `border`, `border-radius`, `padding` | Mỗi dự án thành một thẻ có khung |
| `.du-an-list article` | `height: 100%` | 3 khung cao bằng nhau dù chữ dài ngắn khác nhau |
| `.du-an-list h3` | `font-size`, `margin-top: 0` | Tiêu đề thẻ nhỏ lại vừa khung, không bị khoảng trống trên đầu |

Lưu ý: `display: flex` đặt cho `ol`, nên item là các `li`, không phải các `article`. Đó là lý do `flex` viết cho `li`.

**Tự kiểm tra:** ở bản máy tính có 3 thẻ trên một hàng, cao bằng nhau. Ở bản điện thoại, mỗi thẻ một hàng, rộng hết khung.

### BT5. Luyện tập: Flexbox Froggy

Chơi [Flexbox Froggy](https://flexboxfroggy.com/) (đổi ngôn ngữ ở góc trên phải), **từ level 1 đến level 24**.

Chụp màn hình level 24 khi đã qua, lưu thành `bai-03/froggy.png`.

### BT6. Câu hỏi

Trả lời trong `bai-03/tra-loi.md`, mỗi câu một dòng có đánh số. Ngắn thôi, 1 đến 2 câu mỗi ý:

1. `justify-content` và `align-items` khác nhau thế nào?
2. Khi đặt `flex-direction: column`, `justify-content: center` căn theo chiều ngang hay chiều dọc? Vì sao?
3. Ở BT4, vì sao viết `flex: 1 1 180px` cho `li` mà không viết cho `article`?
4. Vì sao nên dùng `gap` thay cho `margin` giữa các flex item?

### Git

Commit sau mỗi bài tập, theo bảng:

| Sau | Tên commit |
|---|---|
| Lấy file bài 3 | `Thêm bài 3: Flexbox` |
| BT1 | `Xếp header bằng flex` |
| BT2 | `Dùng gap cho nav` |
| BT3 | `Đặt ảnh cạnh phần giới thiệu` |
| BT4 | `Xếp dự án thành hàng thẻ` |
| BT5 | `Thêm ảnh Flexbox Froggy` |
| BT6 | `Trả lời câu hỏi bài 3` |

Cách commit riêng từng bài tập khi đã sửa nhiều file: `git add` đúng file của bài tập đó, `git status` để xem lại, rồi mới `git commit`.

Đọc thêm: [MDN: Flexbox](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/CSS_layout/Flexbox), [CSS-Tricks: A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/).

---

Làm xong, nói **"chấm bài 3"**.
