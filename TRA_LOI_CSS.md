# Tìm và sửa lỗi CSS – Trang khuyến mãi thiệp Tết 2026

- Bài tập 1: `css-bai1/trang.html` – CSS đã sửa: `css-bai1/style-loi.css` (bản lỗi gốc: `style-goc.css`)
- Bài tập 2: `css-bai2/trang.html` – CSS đã sửa: `css-bai2/style-loi.css` (bản lỗi gốc: `style-goc.css`)

HTML giữ nguyên 100%, vì HTML link tới `style-loi.css` nên CSS đã sửa vẫn mang tên này.

---

## Bài tập 1 – Lỗi CSS: triệu chứng và nguyên nhân

| # | Triệu chứng nhìn thấy | Nguyên nhân | Cách sửa |
|---|---|---|---|
| 1 | Chỉ có 2 thẻ trên một hàng, thẻ thứ 3 rớt xuống hàng dưới | Không có `box-sizing: border-box` nên width thực = flex-basis `(100% - 48px)/3` + padding 32px + border 2px → tổng 3 thẻ vượt 100% | Thêm `box-sizing: border-box` vào `*` |
| 2 | Cuộn trang thì menu trôi mất, không dính | `.site-header` có `position: sticky` nhưng thiếu `top` → sticky không có ngưỡng để dính | Thêm `top: 0` |
| 3 | Khi cuộn, chữ tiêu đề hero đè lên menu | `.hero-overlay` có `z-index: 5` còn header không có `z-index` | Thêm `z-index: 100` cho `.site-header` |
| 4 | Tiêu đề hero không nằm giữa ảnh (lệch xuống, cuộn thì không đi theo ảnh) | `.hero-overlay` là `position: absolute` nhưng `.hero` không được định vị → overlay căn theo khung trang (initial containing block) thay vì theo `.hero` | Thêm `position: relative` cho `.hero` |
| 5 | Ảnh hero bị méo, kéo giãn | `width/height: 100%` với `object-fit` mặc định `fill` | Thêm `object-fit: cover` (và `display: block`) |
| 6 | Cả 3 nhãn "-20%" dồn về góc trên bên phải trang, không nằm trên thẻ | `.badge` là `position: absolute` nhưng `.card` không được định vị → nhãn định vị theo trang | Thêm `position: relative` cho `.card` |
| 7 | Chữ và giá tràn ra ngoài đáy thẻ | `.card` bị cố định `height: 300px`, nội dung cao hơn | Bỏ `height` cố định |
| 8 | Ảnh trong thẻ to tràn ra ngoài thẻ | `.card img` không giới hạn kích thước → hiển thị kích thước gốc | `width: 100%; height: 180px; object-fit: cover` |
| 9 | Nút "↑" nằm ở góc TRÊN bên phải | `.back-to-top` dùng `top: 24px` | Đổi thành `bottom: 24px`, thêm `z-index: 200` |

**Nội dung ngắn để điền cột G (Bài tập 1):**

> 1) Thẻ thứ 3 rớt hàng – thiếu `box-sizing: border-box`, padding + border cộng thêm vào flex-basis. 2) Menu không dính khi cuộn – `position: sticky` thiếu `top: 0`. 3) Chữ hero đè lên menu khi cuộn – header thiếu `z-index`. 4) Tiêu đề không ở giữa ảnh – `.hero` thiếu `position: relative`, overlay absolute căn theo trang. 5) Ảnh hero bị méo – thiếu `object-fit: cover`. 6) Nhãn "-20%" dồn lên góc trang – `.card` thiếu `position: relative`. 7) Chữ tràn khỏi thẻ – `.card` có `height: 300px` cố định. 8) Ảnh tràn khỏi thẻ – `.card img` thiếu `width: 100%`. 9) Nút "↑" nằm góc trên – dùng `top` thay vì `bottom`.

---

## Bài tập 2 – Prompt sửa lỗi với AI

```text
[Context]
Tôi có trang khuyến mãi thiệp Tết (trang.html + style-loi.css, gửi kèm). HTML đã đúng cấu trúc,
semantic và KHÔNG được sửa. CSS đang có một vài lỗi tinh vi về box model / position.
Yêu cầu hiển thị đúng:
- Thanh menu trên cùng dính lại khi cuộn (sticky) và luôn nằm trên ảnh.
- Ảnh hero phủ kín khung, tiêu đề nằm chính giữa ảnh.
- Ba thẻ sản phẩm xếp một hàng ngang; mỗi thẻ có nhãn "-20%" ở góc trên bên phải của chính thẻ đó;
  ảnh và chữ nằm gọn trong thẻ.
- Nút "↑" nổi cố định ở góc dưới bên phải màn hình khi cuộn.

[Role]
Bạn là lập trình viên Front-end lão luyện, hiểu sâu box model, stacking context, z-index,
position sticky/absolute/fixed và flexbox.

[Action]
1. Đối chiếu từng yêu cầu ở trên với CSS, tìm ra những thuộc tính làm trang hiển thị SAI.
   Gợi ý kiểm tra: tổ tiên của phần tử sticky có overflow khác visible không; box-sizing của
   .card so với flex-basis; thứ tự z-index giữa .badge và .card img.
2. Chỉ sửa lỗi thật, sửa ở mức tối thiểu (đổi/thêm/xoá ít thuộc tính nhất).
3. KHÔNG được sửa hoặc xoá những đoạn trông "lạ" nhưng là cố ý thiết kế, trừ khi chứng minh
   được chúng vi phạm một yêu cầu hiển thị ở trên, ví dụ:
   - margin âm của .products (khối sản phẩm đè lên mép dưới hero, bo góc trên),
   - transform: scale(1.08) của ảnh hero,
   - position + z-index của .products và .card img,
   - mục đích chống tràn ngang của .page (nếu đổi thì phải giữ được tác dụng này).
4. Không sửa HTML, không thêm JavaScript.

[Format]
(a) Bảng: STT | Triệu chứng nhìn thấy | Nguyên nhân (thuộc tính, selector) | Cách sửa.
(b) Danh sách những đoạn "trông lạ" bạn quyết định GIỮ NGUYÊN và lý do.
(c) Toàn bộ file style-loi.css đã sửa; mỗi chỗ sửa có comment /* [SỬA n] ... */ bằng tiếng Việt.

[Target]
- Trang đạt đủ 4 yêu cầu hiển thị ở màn hình rộng và khi thu hẹp cửa sổ (~700px).
- Không phát sinh thanh cuộn ngang.
- Số dòng CSS thay đổi là ít nhất có thể; HTML không đổi.
```

**Kết quả áp dụng (các lỗi thật trong bài 2):**

| # | Triệu chứng | Nguyên nhân | Cách sửa |
|---|---|---|---|
| 1 | Cuộn trang thì menu trôi mất dù đã có `position: sticky; top: 0` | `.page { overflow-x: hidden }` biến `.page` thành scroll container, sticky bám theo `.page` (không cuộn) nên không dính | Đổi thành `overflow-x: clip` (vẫn cắt tràn ngang nhưng không tạo scroll container) |
| 2 | Thẻ thứ 3 rớt xuống hàng dưới | `.card { box-sizing: content-box }` ghi đè `border-box` của `*` → padding + border cộng thêm vào flex-basis | Bỏ `box-sizing: content-box` |
| 3 | Nhãn "-20%" không thấy trên các thẻ | `.card img` có `position: relative; z-index: 2` còn `.badge` không có `z-index` → ảnh che nhãn | Thêm `z-index: 3` cho `.badge` |

Giữ nguyên (đúng, cần thiết): `margin: -48px` + `z-index: 1` của `.products`, `transform: scale(1.08)` của `.hero-bg`, `position/z-index` của `.card img`, `min-height` của `.card`.
