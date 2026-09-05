# Nguyễn Thị Thanh Chi — Portfolio

Trang portfolio cá nhân dạng static site (không cần bước build) cho Nguyễn Thị Thanh Chi — Brand Management / Social Media Marketer. Gồm giới thiệu, kỹ năng, các dự án tiêu biểu (CapitaLand Development, Lazada Vietnam, TikTok Shop Vietnam, freelance) và thông tin liên hệ, hỗ trợ song ngữ Anh/Việt.

## Cấu trúc thư mục

```
index.html           Toàn bộ giao diện, CSS và JS (single-page)
content.json          Nội dung song ngữ — nguồn dữ liệu chính (languages.en / languages.vi)
content-fallback.js   Bản sao content.json dạng JS, dùng khi mở trực tiếp qua file:// (không fetch được JSON)
cv.pdf                File CV công khai (tên cố định)
assets/               Ảnh và video minh hoạ
```

## Chạy thử ở local

```bash
python3 -m http.server 5173
```

Sau đó mở `http://localhost:5173`. Có thể mở trực tiếp `index.html` bằng trình duyệt (`file://`) — khi đó site sẽ tự dùng `content-fallback.js` thay vì fetch `content.json`.

Dừng server:

```bash
pkill -f "python3 -m http.server 5173"
```

## Chỉnh sửa nội dung

- Toàn bộ text hiển thị nằm trong `content.json`, dưới `languages.en` và `languages.vi`. Sửa nội dung ở đây, **giữ nguyên tên khóa**.
- Các trường có tên kết thúc bằng `Html` được phép chứa thẻ `em`, `strong`, `span`, `i` để nhấn mạnh thị giác.
- Nếu bản tiếng Việt thiếu một giá trị, site sẽ tự dùng giá trị tiếng Anh tương ứng.
- Sau khi sửa `content.json`, phải regenerate lại `content-fallback.js` để `window.PORTFOLIO_CONTENT` khớp cấu trúc với JSON đã parse.
- Nếu không chỉ định ngôn ngữ, cần cập nhật đồng thời cả `en` và `vi`.

## Cập nhật CV

CV được phục vụ từ cùng thư mục với `index.html`. Khi thay CV mới:

1. Đặt tên file chính xác là `cv.pdf` ở thư mục gốc.
2. Đảm bảo phần preview và nút download vẫn trỏ về `./cv.pdf`.

## Ghi chú triển khai

- Là site tĩnh, không có bước build — deploy bằng cách phục vụ trực tiếp các file trong repo.
- Luôn dùng đường dẫn tương đối có thể deploy được (vd: `./cv.pdf`), không dùng path local tuyệt đối (vd: `/Users/...`).
- Xem thêm quy tắc chi tiết cho việc chỉnh sửa/tự động hoá tại [AGENTS.md](AGENTS.md).
