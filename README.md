# Công cụ cửa hàng — 3 danh mục

Một trang chủ (`index.html`) dẫn tới 3 công cụ độc lập, host chung 1 repo GitHub Pages:

```
/                     → Trang chủ (menu chọn danh mục)
/ban-giao/            → Công việc hằng ngày (bàn giao), dữ liệu lưu Google Sheet
/tra-cuu-ctkm/        → Tra cứu CTKM & Tồn kho (đọc file Excel do bạn upload)
/kiem-ke/             → Kiểm kê hàng hoá, quét mã vạch (chạy offline)
```

Mỗi thư mục là 1 app riêng biệt, không phụ thuộc lẫn nhau — bạn có thể mở thẳng
`/tra-cuu-ctkm/` hoặc `/kiem-ke/` mà không cần qua trang chủ.

## Bước 1 — Đưa lên GitHub Pages

1. Tạo 1 repo GitHub mới (public).
2. Upload **toàn bộ** cấu trúc thư mục này lên repo, giữ nguyên cây thư mục
   (đừng đổ hết file vào 1 chỗ — mỗi app cần nằm đúng thư mục riêng).
3. **Settings > Pages** → Source: `Deploy from a branch` → branch `main`,
   thư mục `/ (root)` → **Save**.
4. Link app dạng: `https://<tên-github>.github.io/<tên-repo>/`

## Bước 2 — Riêng phần "Bàn giao": nối Google Sheet

Đây là app duy nhất trong 3 cái cần cấu hình dữ liệu (2 app còn lại tự chứa,
không cần server).

1. Vào [sheets.google.com](https://sheets.google.com), tạo spreadsheet mới.
2. **Extensions > Apps Script**, dán nội dung file
   [`ban-giao/apps-script/Code.gs`](ban-giao/apps-script/Code.gs) vào.
3. **Deploy > New deployment** → Web app → Execute as: `Me` → Who has access:
   `Anyone` → Deploy. Cấp quyền khi được hỏi (script của chính bạn nên an toàn).
4. Copy **Web app URL** (dạng `https://script.google.com/macros/s/xxxxx/exec`).
5. Mở `.../ban-giao/` trên trình duyệt → app tự bật màn **Cài đặt kết nối** →
   dán URL vào → Lưu. Xong, không cần sửa code.
6. Danh sách công việc định kỳ nằm ở sheet `CauHinh` (tự tạo sau lần chạy đầu)
   — sửa/thêm/xoá trực tiếp trong đó bất cứ lúc nào.

Chi tiết đầy đủ về cách dùng "Bàn giao" xem trong
[`ban-giao/README.md`](ban-giao/README.md) *(nội dung giống hướng dẫn cũ, chỉ
đổi đường dẫn thư mục)*.

## Về "Tra cứu CTKM & Tồn kho" và "Kiểm kê hàng hoá"

Hai công cụ này **giữ nguyên như file gốc bạn gửi** — chạy độc lập ngay trên
trình duyệt, không cần Google Sheet hay Apps Script. Người dùng tự upload file
Excel CTKM/Tồn kho (hoặc quét mã) mỗi lần dùng, dữ liệu lưu tạm trên máy
(`localStorage`).

**Một lưu ý nhỏ về "Kiểm kê hàng hoá":** file gốc có khai báo
`manifest.json` và icon (`icons/icon-192.png`) để hỗ trợ "Thêm vào màn hình
chính" như app thật (PWA). Hai file này **chưa có** trong repo — thiếu chúng
không ảnh hưởng gì đến việc quét/kiểm kê bình thường, chỉ là biểu tượng "Thêm
vào màn hình chính" sẽ không đẹp/không hoạt động đầy đủ. Nếu muốn mình bổ sung
2 file đó (manifest + icon), báo lại.

## Giới hạn cần biết

- "Bàn giao" ở chế độ công khai, không mật khẩu (theo đúng lựa chọn trước đó).
- "Tra cứu CTKM" và "Kiểm kê hàng hoá" hoạt động dựa trên file bạn upload mỗi
  phiên — không đồng bộ dữ liệu giữa các máy/nhân viên khác nhau. Nếu sau này
  muốn 2 công cụ này cũng dùng chung 1 nguồn dữ liệu (Google Sheet), báo lại
  để mình làm thêm.
