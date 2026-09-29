# Blakletterpress – Bài tập HTML

Website tĩnh (HTML/CSS) dựa trên template Blakletterpress. Lời giải chi tiết các câu hỏi xem trong [BAI_TAP.md](BAI_TAP.md).

## Các trang

- `index.html` – trang chủ
- `register.html` – form đăng ký nhận thông tin
- `media.html` – trang đa phương tiện (video, audio, bản đồ)
- `index_new.html` – trang chủ refactor sang HTML5 semantic
- `about.html`, `news.html`, `blog.html`, `news_wrong.html`, `blog_wrong.html`

## Chạy local

```bash
python -m http.server 5500
```

Mở http://localhost:5500

## Deploy lên Vercel

1. Push repo này lên GitHub.
2. Vào https://vercel.com/new → **Import** repo vừa push.
3. Framework Preset: **Other**, để trống Build Command và Output Directory → **Deploy**.
