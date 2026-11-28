# Bài 5: HTML form

**Mục tiêu:** viết form đúng chuẩn: mỗi ô nhập có nhãn, chọn đúng loại ô cho từng kiểu dữ liệu, để trình duyệt tự kiểm tra dữ liệu trước khi gửi, và style form cho dễ dùng. Áp dụng lên trang profile: phần Liên hệ có thêm form gửi lời nhắn.

Form hôm nay chưa gửi được đi đâu, vì chưa có server. Đến trạm FastAPI, chính form này sẽ gửi dữ liệu lên backend của bạn.

---

## 1. Form, input và name

```html
<form>
  <label for="ho-ten">Họ tên</label>
  <input type="text" id="ho-ten" name="ho-ten">

  <button type="submit">Gửi</button>
</form>
```

Bấm **Gửi**, trình duyệt gom dữ liệu thành các cặp `name=giá trị` rồi gửi đi. Form không có `action` thì gửi về chính trang đó, và dữ liệu hiện lên thanh địa chỉ:

```
index.html?ho-ten=Himmel
```

- **`name`** là "tên khóa" khi gửi đi. Ô nào **không có `name` thì không được gửi**, dù bạn có gõ vào.
- **`id`** chỉ dùng trong trang: để `label` trỏ tới, để CSS và JavaScript tìm.
- Thường đặt `id` và `name` giống nhau cho dễ nhớ, nhưng là hai việc khác nhau.

## 2. Label

```html
<label for="email">Email</label>
<input type="email" id="email" name="email">
```

`for` của `label` phải **trùng với `id`** của ô nhập. Khi đó:

1. Bấm vào chữ "Email" là con trỏ nhảy vào ô. Với checkbox, radio: bấm vào chữ là tick được, không phải nhắm vào ô vuông nhỏ.
2. Trình đọc màn hình đọc "Email, ô nhập" cho người khiếm thị. Không có label, họ chỉ nghe "ô nhập", không biết phải gõ gì.

`placeholder` (chữ mờ trong ô) **không thay được label**: gõ chữ vào là nó biến mất, và nhiều trình đọc màn hình không đọc nó.

## 3. Các loại ô nhập

| Thẻ | Dùng cho | Điện thoại hiện bàn phím |
|---|---|---|
| `<input type="text">` | Chữ ngắn: tên, tiêu đề | Chữ |
| `<input type="email">` | Email. Trình duyệt tự kiểm tra có `@` | Có sẵn phím `@` |
| `<input type="tel">` | Số điện thoại | Bàn phím số |
| `<input type="number">` | Số để tính toán: tuổi, số lượng | Bàn phím số |
| `<input type="date">` | Ngày | Bảng chọn ngày |
| `<input type="password">` | Mật khẩu. Hiện dấu chấm | Chữ |
| `<textarea>` | Chữ dài nhiều dòng | Chữ |
| `<select>` + `<option>` | Chọn 1 trong danh sách dài | Danh sách cuộn |
| `<input type="radio">` | Chọn 1 trong vài lựa chọn, thấy hết cùng lúc | |
| `<input type="checkbox">` | Bật/tắt, hoặc chọn nhiều | |

Số điện thoại dùng `tel`, không dùng `number`: số điện thoại không phải để cộng trừ, và `number` làm mất số 0 ở đầu.

### Select

```html
<label for="chu-de">Chủ đề</label>
<select id="chu-de" name="chu-de" required>
  <option value="">-- Chọn chủ đề --</option>
  <option value="hop-tac">Hợp tác dự án</option>
  <option value="khac">Khác</option>
</select>
```

`value` là thứ được gửi đi, chữ giữa thẻ là thứ người dùng thấy. Lựa chọn đầu có `value=""` (rỗng), nên khi có `required`, người dùng **bắt buộc** phải chọn cái khác.

### Radio và fieldset

Các radio **cùng `name`** thành một nhóm: chọn cái này thì cái kia tự bỏ chọn.

```html
<fieldset>
  <legend>Liên hệ lại qua</legend>

  <input type="radio" id="lai-email" name="lien-he-lai" value="email" checked>
  <label for="lai-email">Email</label>

  <input type="radio" id="lai-dien-thoai" name="lien-he-lai" value="dien-thoai">
  <label for="lai-dien-thoai">Điện thoại</label>
</fieldset>
```

- `fieldset` gom một nhóm ô liên quan, `legend` là tiêu đề của nhóm. Trình đọc màn hình đọc "Liên hệ lại qua, Email" để người nghe hiểu "Email" thuộc câu hỏi nào.
- `checked` chọn sẵn một lựa chọn.
- Mỗi radio vẫn cần `id` riêng và `label` riêng.

## 4. Nút

```html
<button type="submit">Gửi</button>   <!-- gửi form -->
<button type="reset">Xóa hết</button> <!-- trả form về như lúc đầu -->
<button type="button">Xem thử</button> <!-- không làm gì, chờ JavaScript -->
```

Nút trong form mà **không ghi `type`** thì mặc định là `submit`. Luôn ghi `type` cho rõ.

## 5. Trình duyệt tự kiểm tra dữ liệu

Thêm thuộc tính vào ô nhập, trình duyệt sẽ chặn không cho gửi và hiện thông báo khi sai:

| Thuộc tính | Nghĩa | Ví dụ |
|---|---|---|
| `required` | Không được để trống | `<input required>` |
| `minlength`, `maxlength` | Số ký tự ít nhất, nhiều nhất | `<textarea minlength="10" maxlength="500">` |
| `min`, `max` | Giá trị nhỏ nhất, lớn nhất (số, ngày) | `<input type="number" min="1" max="100">` |
| `type="email"` | Phải có dạng `ten@mien` | |
| `pattern` | Phải khớp mẫu (regex) | `<input type="tel" pattern="0[0-9]{9}">`: 10 số, bắt đầu bằng 0 |

**Kiểm tra ở trình duyệt là để người dùng sửa sai nhanh, không phải để bảo mật.** Ai cũng có thể mở DevTools, xóa chữ `required`, rồi gửi dữ liệu rỗng. Vì vậy server luôn phải kiểm tra lại. Bạn sẽ làm việc đó ở trạm FastAPI.

## 6. Style cho form

```css
/* Ô nhập không tự kế thừa font của trang: phải ép */
input, select, textarea, button {
  font: inherit;
}

/* Khi người dùng bấm Tab tới, hiện viền rõ ràng */
input:focus-visible {
  outline: 2px solid var(--mau-nhan);
  outline-offset: 2px;
}

/* Ô sai, nhưng chỉ sau khi người dùng đã đụng vào */
input:user-invalid {
  border-color: red;
}
```

- **`font: inherit`**: thiếu dòng này, ô nhập dùng font và cỡ chữ riêng, nhỏ hơn và khác hẳn phần còn lại của trang.
- **Không bao giờ xóa `outline`** mà không thay bằng cái khác. Người dùng bàn phím nhìn viền đó để biết mình đang ở ô nào.
- **`:user-invalid`** khác `:invalid`: `:invalid` tô đỏ ngay khi vừa mở trang (vì ô `required` đang trống), trông như người dùng đã làm sai. `:user-invalid` chỉ tô đỏ sau khi người dùng đã gõ vào rồi rời đi, hoặc đã bấm Gửi.

**Dùng phím Tab** để đi qua các ô, `Shift + Tab` để lùi lại, `Space` để tick, phím mũi tên để đổi radio. Form tốt là form dùng được hoàn toàn bằng bàn phím.

---

## Bài tập

Làm trong `01-html-css-js/bai-05/`. Mình đã chép trang profile từ Bài 4 sang: `index.html`, `NvM.jpg`, `style.css` (giữ nguyên CSS Bài 2, 3, 4 của bạn).

### BT1. Viết form

Trong `section#lien-he`, **giữ nguyên** `h2` và link GitHub. Thêm bên dưới link:

```html
<form class="form-lien-he">
  ...các trường...
</form>
```

**Mỗi trường** (trừ nhóm radio và checkbox) bọc trong một `div` có `class="truong"`, bên trong là `label` rồi đến ô nhập:

```html
<div class="truong">
  <label for="ho-ten">Họ tên</label>
  <input type="text" id="ho-ten" name="ho-ten" required minlength="2">
</div>
```

**Các trường cần có, theo đúng thứ tự:**

| # | Nhãn hiện ra | Thẻ và `type` | `id` và `name` | Ràng buộc |
|---|---|---|---|---|
| 1 | Họ tên | `input type="text"` | `ho-ten` | `required`, `minlength="2"` |
| 2 | Email | `input type="email"` | `email` | `required` |
| 3 | Số điện thoại | `input type="tel"` | `so-dien-thoai` | Không bắt buộc. `pattern="0[0-9]{9}"` |
| 4 | Chủ đề | `select`, 4 `option`: `-- Chọn chủ đề --` (`value=""`), `Hợp tác dự án`, `Hỏi về bài học`, `Khác` | `chu-de` | `required` |
| 5 | Lời nhắn | `textarea rows="5"` | `loi-nhan` | `required`, `minlength="10"`, `maxlength="500"` |

**Rồi thêm, không bọc trong `div.truong`:**

| # | Thêm gì | Chi tiết |
|---|---|---|
| 6 | Nhóm radio | `fieldset` + `legend` "Liên hệ lại qua". 2 radio cùng `name="lien-he-lai"`: Email (`id="lai-email"`, `value="email"`, `checked`) và Điện thoại (`id="lai-dien-thoai"`, `value="dien-thoai"`). Mỗi radio một `label` đặt **sau** nó |
| 7 | Checkbox | `id` và `name` là `ban-sao`, `value="co"`, `label` đặt **sau** nó: "Gửi cho tôi một bản sao". Không bắt buộc. Bọc cả hai trong `<div class="chon">` |
| 8 | Nút gửi | `button type="submit"`, chữ "Gửi lời nhắn" |

**Tự kiểm tra:**
- Bấm vào **chữ** của từng nhãn: con trỏ nhảy vào đúng ô. Với radio và checkbox: bấm vào chữ là chọn được.
- Dùng `Tab` đi từ ô đầu tới nút Gửi mà không cần chuột, thứ tự đúng 1 → 8.

### BT2. Thử kiểm tra dữ liệu

Làm từng dòng, ghi lại trình duyệt có chặn không:

| # | Làm gì rồi bấm Gửi | Trình duyệt phải |
|---|---|---|
| 1 | Để trống hết | Chặn, báo ở ô Họ tên |
| 2 | Họ tên: `A` | Chặn, báo quá ngắn |
| 3 | Email: `abc` | Chặn, báo thiếu `@` |
| 4 | Không chọn chủ đề | Chặn, báo ở ô Chủ đề |
| 5 | Lời nhắn: `chào` | Chặn, báo quá ngắn |
| 6 | Số điện thoại: `123` | Chặn, báo không đúng định dạng |
| 7 | Điền đúng hết, để trống số điện thoại | **Cho gửi**: trang tải lại |

Sau dòng 7, nhìn thanh địa chỉ: phần sau dấu `?` là dữ liệu form. **Chép nguyên đoạn đó** vào `bai-05/tra-loi.md`, ở đầu file.

Chữ tiếng Việt có dấu sẽ hiện thành dạng `%E1%BB%...`: đó là cách trình duyệt mã hóa ký tự đặc biệt trong địa chỉ web. Dấu cách thành `+`.

### BT3. Style cho form

Thêm 2 biến vào `:root` có sẵn: `--mau-loi` (màu đỏ cho ô sai) và `--mau-vien` (màu viền ô nhập, xám vừa).

| Selector | Thuộc tính | Kết quả nhìn thấy |
|---|---|---|
| `.form-lien-he` | `display: grid`, `gap: 12px`, `margin-top` | Các trường cách đều nhau, form tách khỏi link GitHub |
| `.truong` | `display: grid`, `gap: 4px` | Nhãn nằm trên ô nhập, sát ô |
| `.truong input, .truong select, .truong textarea` | `font: inherit`, `width: 100%` | Ô nhập dùng font của trang, rộng hết khung |
| như trên | `padding`, `border: 1px solid var(--mau-vien)`, `border-radius` | Ô nhập có khoảng đệm, viền mảnh, bo góc |
| `.truong textarea` | `resize: vertical` | Chỉ kéo được chiều cao, không kéo vỡ khung theo chiều ngang |
| `.form-lien-he :focus-visible` | `outline: 2px solid var(--mau-nhan)`, `outline-offset: 2px` | Bấm Tab: ô đang chọn có viền màu nhấn |
| `.form-lien-he :user-invalid` | `border-color: var(--mau-loi)` | Gõ sai rồi rời ô: viền ô đỏ. **Mới mở trang thì chưa đỏ** |
| `fieldset` | `border: 1px solid var(--mau-vien)`, `border-radius` | Nhóm radio có khung cùng kiểu với ô nhập |
| `.chon` | `display: flex`, `align-items: center`, `gap: 8px` | Checkbox và chữ thẳng hàng |
| `.form-lien-he button` | `font: inherit`, `background-color: var(--mau-galaxy)`, `color: var(--mau-nen)`, `border: none`, `padding`, `border-radius`, `cursor: pointer` | Nút xanh đậm, chữ trắng, rê chuột hiện bàn tay |
| `.form-lien-he button:hover` | `background-color` khác (dùng biến có sẵn hoặc thêm biến mới) | Rê chuột lên nút thì nút đổi màu |

Vì sao `width: 100%` chỉ viết cho ô trong `.truong`: nếu viết cho mọi `input`, radio và checkbox cũng bị kéo rộng hết khung, chữ bị đẩy xuống dòng dưới.

**Tự kiểm tra:**
- Mới mở trang: không ô nào đỏ.
- Gõ `abc` vào Email rồi bấm `Tab`: ô Email đỏ.
- Ở 1024px, form nằm gọn trong cột Liên hệ bên phải. Ở 375px, form rộng hết màn hình.

### BT4. Câu hỏi

Trả lời trong `bai-05/tra-loi.md`, bên dưới đoạn địa chỉ đã chép ở BT2. Mỗi câu một dòng có đánh số, 1 đến 2 câu:

1. Nhìn đoạn địa chỉ đã chép: có bao nhiêu cặp `name=giá trị`? Ô nào **không** xuất hiện, vì sao?
2. Vì sao `for` của `label` phải trùng `id` của ô nhập? Nêu 2 lợi ích.
3. `:invalid` và `:user-invalid` khác nhau thế nào? Vì sao bài này dùng `:user-invalid`?
4. Đã có `required` và `minlength` ở trình duyệt rồi, vì sao server vẫn phải kiểm tra lại?

### Git

| Sau | Tên commit |
|---|---|
| Lấy file bài 5 | `Thêm bài 5: HTML form` |
| BT1 | `Thêm form liên hệ` |
| BT2 | `Ghi kết quả thử form` |
| BT3 | `Style form liên hệ` |
| BT4 | `Trả lời câu hỏi bài 5` |

Đọc thêm: [MDN: Web forms](https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Forms), [MDN: Client-side form validation](https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Forms/Form_validation).

---

Làm xong, nói **"chấm bài 5"**.
