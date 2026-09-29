# Bài tập HTML – Blakletterpress

| Trang | Mô tả |
|---|---|
| `index.html` | Trang chủ gốc (giữ nguyên) |
| `about.html`, `news.html`, `blog.html` | Các trang gốc |
| `news_wrong.html`, `blog_wrong.html` | File có lỗi (giữ nguyên để đối chiếu) |
| `register.html` | **Câu 3** – Form đăng ký nhận thông tin |
| `media.html` | **Câu 4** – Trang đa phương tiện + thẻ HTML5 semantic |
| `index_new.html` | **Câu 5** – `index.html` refactor sang HTML5 semantic |

---

## Câu 1. Các lỗi trong `news_wrong.html`

So sánh với `news.html` (bản đúng) và kiểm tra theo chuẩn HTML5:

| # | Dòng | Code lỗi | Vấn đề | Sửa |
|---|---|---|---|---|
| 1 | 1 | `<!DOCTYPE HTML5>` | Khai báo DOCTYPE sai, trình duyệt chuyển sang *quirks mode* | `<!DOCTYPE html>` |
| 2 | 5 | `<meta charset="UTF-88">` | Bảng mã không tồn tại → tiếng Việt/ký tự đặc biệt có thể lỗi font | `<meta charset="UTF-8">` |
| 3 | 6 | `<title>News - ...` | Thiếu `</title>` → toàn bộ phần sau (kể cả `<link>` CSS) bị coi là nội dung tiêu đề, **trang mất CSS** | Thêm `</title>` |
| 4 | 9 | `<boby>` | Sai chính tả thẻ `body` | `<body>` |
| 5 | 19 | `<img src="images/logo.png">` | Thiếu thuộc tính bắt buộc `alt` | `alt="LOGO"` |
| 6 | 24 | `<input type="submit" ... class="btn"` | Thiếu dấu `>` → `</form>` phía sau bị "nuốt" thành thuộc tính, form không được đóng | `class="btn">` |
| 7 | 27 | `</section>` | Thẻ đóng không khớp với thẻ mở `<div id="header">` | `</div>` |
| 8 | 33 | `class="time'>` | Nháy mở `"` và đóng `'` không khớp → giá trị thuộc tính kéo dài, nuốt cả ngày tháng và thẻ phía sau | `class="time">` |
| 9 | 34 | `<h7>NEWS TITLE ONE</h7>` | HTML chỉ có `h1`–`h6`, không có `h7` | `<h3>...</h3>` |
| 10 | 43–45 | `<p> ...` | Thiếu thẻ đóng `</p>` | Thêm `</p>` trước `<a class="more">` |
| 11 | 53 | `<a ... class="more">Read more >>` | Thiếu `</a>` → link lan sang các phần tử sau | Thêm `</a>` |
| 12 | 71 | `</ol>` | Đóng sai thẻ, thẻ mở là `<ul id="list">` | `</ul>` |

> Ngoài ra `Read more >>` nên viết `Read more &gt;&gt;` để hợp lệ tuyệt đối (lỗi nhỏ, có cả ở bản gốc).

---

## Câu 2. Prompt phát hiện và sửa lỗi `blog_wrong.html`

```text
Bạn là một chuyên gia front-end, am hiểu chuẩn HTML5 của W3C/WHATWG.

Tôi gửi kèm file blog_wrong.html (một trang trong website template Blakletterpress).
Hãy thực hiện:

1. Rà soát TOÀN BỘ file và liệt kê tất cả lỗi, gồm:
   - Lỗi cú pháp: thẻ không đóng, đóng sai thẻ (ul/ol), thuộc tính thiếu dấu nháy/dấu >.
   - Lỗi vi phạm chuẩn HTML5: charset không hợp lệ, thẻ <title> trùng lặp,
     thuộc tính bị lặp trên cùng một thẻ, width/height có đơn vị "px",
     id bị trùng trong cùng trang, phần tử con không hợp lệ (ví dụ <div> nằm trực tiếp trong <ul>),
     ký tự & chưa escape trong URL.
   - Lỗi accessibility/SEO: <img> thiếu alt, link có href rỗng.
   - Lỗi ngữ nghĩa: dùng thẻ trình bày (<i>, <b>) thay cho thẻ ngữ nghĩa (<em>, <strong>),
     link điều hướng trỏ sai (ví dụ nút "First" trỏ tới page=2).
2. Trình bày kết quả dạng bảng: STT | Số dòng | Đoạn code lỗi | Mô tả lỗi | Cách sửa.
3. Xuất lại file blog.html hoàn chỉnh đã sửa hết lỗi.
   Yêu cầu: KHÔNG thay đổi bố cục, class, id (trừ id bị trùng), nội dung chữ và đường dẫn ảnh;
   giữ nguyên cách thụt lề bằng tab như file gốc.
4. Cuối cùng, xác nhận file sau khi sửa không còn lỗi khi kiểm tra bằng https://validator.w3.org/.
```

**Kết quả mong đợi khi chạy prompt** (các lỗi có trong `blog_wrong.html`):

| # | Dòng | Code lỗi | Sửa |
|---|---|---|---|
| 1 | 5 | `<meta charset="utf8">` – giá trị không chuẩn | `<meta charset="UTF-8">` |
| 2 | 7 | Hai thẻ `<title>` trong `<head>` | Xóa `<title>Blakletterpress</title>` |
| 3 | 14 | `class="sitename" class="brand"` – thuộc tính trùng | Giữ một `class="sitename"` |
| 4 | 14 | `width="142px"` – width chỉ nhận số nguyên | `width="142"` |
| 5 | 16 | `<img src="images/header-text.png" ...>` thiếu `alt` | `alt="Text"` |
| 6 | 37 | `<i>free</i>` – thẻ trình bày, không có ngữ nghĩa | `free` (hoặc `<em>free</em>`) |
| 7 | 73 | `<div class="ad">` nằm trực tiếp trong `<ul>` | Xóa (hoặc bọc trong `<li>`) |
| 8 | 76 | `blog.html?page=2&sort=new` – `&` chưa escape; nút *First* trỏ sai trang | `href="blog.html"` |
| 9 | 76 | `<a href="blog.html">1` thiếu `</a>` | `<a href="blog.html">1</a>` |
| 10 | 83 | `<ul id="list">` – trùng id với danh sách bài viết (dòng 32), CSS `#list` áp nhầm vào menu | `<ul>` |
| 11 | 123 | `</ol>` đóng cho `<ul>` | `</ul>` |
| 12 | 124 | `<a href="" class="btn2">` – href rỗng | `href="news.html"` |

---

## Câu 3 & 4

- `register.html`: dùng nguyên khung `#page > #header / #contents (#main + #sidebar) / #footer` của `index.html`, chỉ thay nội dung `#main` bằng form gồm 3 `<fieldset>` (Thông tin tài khoản, Thông tin cá nhân, Tuỳ chọn nhận tin). Có validate bằng HTML5: `required`, `type="email"`, `minlength="8"`, `pattern="0[0-9]{9}"`, `type="date"`, `type="number"`.
- `media.html`: cùng khung, `#main` chứa một `<article>` với `<header>`, `<time>`, `<figure>/<figcaption>`, `<section>`, `<video>`, `<audio>`, `<iframe>` (Google Maps), `<footer>`.
- Style bổ sung được thêm vào cuối `css/style.css` (không sửa style cũ).

---

## Câu 5. Prompt refactor `index.html` → `index_new.html`

```text
Bạn là một front-end developer có kinh nghiệm về HTML5 semantic và SEO on-page.

Tôi gửi kèm 2 file: index.html và css/style.css (template Blakletterpress).
Hãy refactor index.html sang các thẻ semantic HTML5 và lưu thành index_new.html.

Yêu cầu bắt buộc:
1. Giữ NGUYÊN bố cục hiển thị và NGUYÊN nội dung chữ, hình ảnh, liên kết so với index.html.
   Khi mở 2 trang cạnh nhau phải trông giống hệt nhau.
2. Giữ nguyên tất cả id và class hiện có để CSS cũ vẫn áp dụng được.
3. Thay các <div> bằng thẻ semantic phù hợp:
   - #header        -> <header>
   - #main          -> <main>
   - #gallery       -> <section> (ảnh lớn đặt trong <figure>)
   - div.body       -> <article>
   - #sidebar       -> <aside>
   - #navigation    -> <nav> (thêm aria-label, aria-current="page" cho mục đang chọn)
   - div.section    -> <section>
   - mỗi bài trong "Placeholder" -> <article>; đổi <h5> thành <h3> để đúng thứ bậc heading
   - #footer        -> <footer>
4. Cải thiện SEO/accessibility cơ bản:
   - <html lang="en">, thêm <meta name="viewport"> và <meta name="description">.
   - Viết lại alt của ảnh có ý nghĩa (không dùng "Img", "Text", "LOGO").
   - Ô tìm kiếm dùng placeholder thay cho value + onfocus/onblur, thêm name và aria-label, form có role="search".
   - Link mở tab mới thêm rel="noopener"; link icon không có chữ thêm aria-label.
   - Chỉ có một <h1> trên trang.
5. Nếu đổi thẻ làm selector CSS cũ không còn khớp (ví dụ "#main div.body", "#sidebar div.section",
   "#gallery > div", "#posts h5"), hãy chỉ ra và đề xuất sửa CSS tối thiểu để giao diện không đổi.
6. Trả về: (a) toàn bộ code index_new.html, (b) phần CSS cần sửa/bổ sung,
   (c) bảng đối chiếu "thẻ cũ -> thẻ mới -> lý do".
```

**Kết quả áp dụng** (`index_new.html`): đã thực hiện đúng các mục trên. Phần CSS phải chỉnh để giữ nguyên giao diện:

- `#main div.body` → `#main .body`, `#sidebar div.section` → `#sidebar .section`
- Thêm `#gallery > figure`, `#posts h3`, `#searchbar input.txtfield::placeholder`

Đã kiểm tra bằng cách đo vị trí/kích thước các khối chính của `index.html` và `index_new.html` trên trình duyệt: trùng khớp hoàn toàn.
