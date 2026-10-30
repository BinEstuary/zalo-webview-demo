# QR Scanner · Zalo WebView demo

Trang demo xử lý trường hợp người dùng quét QR bằng Zalo và trang mở trong Zalo WebView, nơi camera thường không ổn định.

## Hành vi

- **Phát hiện Zalo** qua User-Agent (`/Zalo/i`).
- **Trong Zalo**: hiện overlay hướng dẫn mở bằng trình duyệt mặc định, thử tự chuyển sang Chrome (Android: `intent://` sang Chrome; iOS: thử Safari `x-safari-https://` trước, nếu vẫn ở trong Zalo sau 1.5s thì thử Chrome `googlechromes://`), tắt nút bật camera trực tiếp và chỉ cho chọn ảnh QR.
- **Ngoài Zalo**: bật camera và quét bằng `BarcodeDetector`, hoặc chọn ảnh QR từ thư viện.
- Thêm `?no_redirect=1` vào URL để tắt tự chuyển hướng khi test.

## Giới hạn cần biết

- `BarcodeDetector` chưa có trên mọi trình duyệt (ví dụ Firefox, Safari). Khi không có, trang chỉ dùng được chức năng chọn ảnh. Bản production nên dùng thư viện JS như `html5-qrcode` hoặc `zxing-js`.
- Chuyển hướng sang Chrome/Safari là best-effort, có thể không hoạt động trên một số máy hoặc bị Zalo chặn sau này. Overlay hướng dẫn là đường dự phòng chính.
- Chưa kiểm thử thực tế trong Zalo trên thiết bị thật. Cần test trên Android và iOS.

## Chạy thử local

Mở trực tiếp `index.html` trong trình duyệt, hoặc:

```bash
cd zalo-webview-demo
python3 -m http.server 8000
```

Sau đó truy cập `http://localhost:8000`. Camera chỉ hoạt động trên `localhost` hoặc HTTPS.

## Deploy lên GitHub Pages

1. Tạo repo mới trên GitHub, ví dụ `zalo-webview-demo`.
2. Đưa các file trong thư mục này lên nhánh `main` ở root của repo (`index.html`, `README.md`).
3. Vào **Settings → Pages**, chọn **Deploy from a branch**, branch `main`, folder `/ (root)`.
4. Trang sẽ có tại `https://<username>.github.io/zalo-webview-demo/`.

Lưu ý: camera chỉ chạy trên HTTPS, GitHub Pages đã có sẵn HTTPS.
