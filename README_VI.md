# CyberQuest — một repository duy nhất

## Cấu trúc
- `index.html`, `style.css`, `script.js`: trang điều khiển (controller) tại gốc repo.
- `participant/index.html`: trang người tham gia.
- `shared/config.js`: cấu hình tham chiếu chung.
- `assets/QR_CQ2026-01.png`: QR PNG đóng gói sẵn.

## Quan trọng trước khi triển khai
QR đi kèm được tạo cho tên repository **`cyberquest`** và URL:
`https://peody.github.io/cyberquest/participant/?qr=1&sessionCode=CQ2026-01`

Để dùng QR có sẵn mà không phải tạo lại, hãy tạo repository GitHub tên `cyberquest` trong tài khoản `peody`. Nếu dùng tên repo khác hoặc tài khoản khác, cần tạo lại QR theo URL GitHub Pages mới và cập nhật ảnh trong `assets/QR_CQ2026-01.png`.

## Đưa lên GitHub Pages
1. Tải ZIP và giải nén.
2. Tạo repo `cyberquest` trên GitHub.
3. Upload toàn bộ **nội dung bên trong thư mục ZIP** lên thư mục gốc repo (không upload một thư mục bọc bên ngoài).
4. Vào **Settings → Pages**.
5. Ở **Build and deployment**, chọn **Deploy from a branch**.
6. Chọn branch `main`, folder `/(root)`, bấm **Save**.
7. Chờ GitHub hoàn tất deployment; mở `https://peody.github.io/cyberquest/`.
8. Mở `/participant/?qr=1&sessionCode=CQ2026-01` trên thiết bị thứ hai và bấm xác nhận tham gia.
9. Từ controller, gửi lệnh bắt đầu và kết thúc.

## Đồng bộ MQTT
Cả hai trang dùng broker `wss://broker.emqx.io:8084/mqtt` và topic `cyberquest/demo/CQ2026-01`. Trang người tham gia chỉ subscribe sau khi người dùng bấm xác nhận. `DEMO_ALERT` hiển thị cảnh báo mô phỏng; `DEMO_END` kết thúc mô phỏng.

## Kiểm thử / chẩn đoán
- QR phải mở URL trên có `sessionCode=CQ2026-01`.
- Trên trang tham gia phải thấy mã phiên `CQ2026-01`.
- Nếu lệnh không tới: mở DevTools → Console/Network ở cả hai thiết bị, kiểm tra thư viện `mqtt` từ unpkg có tải được và kết nối WebSocket tới broker có thành công không.
- Broker công cộng không cung cấp quyền riêng tư cho topic; không truyền dữ liệu cá nhân. Mã phiên cố định không phải cơ chế xác thực.
- Chỉ sử dụng cho diễn tập đã thông báo; trang tham gia có cơ chế thoát rõ ràng.

## Giới hạn kiểm thử
Mã nguồn và QR đã được đóng gói, nhưng kết nối MQTT trực tiếp cần được xác minh sau khi triển khai trên GitHub Pages và mạng thực tế.
