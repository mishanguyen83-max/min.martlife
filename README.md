# Min MartLife — Website demo

Website giới thiệu đồ gia dụng điện tử và thiết bị SmartHome của shop **Min MartLife**
(Facebook: [Min Smart Life](https://www.facebook.com/profile.php?id=61596530125836)).

> **DEMO — Chưa phải website bán hàng thật.**
> Trang chưa có giỏ hàng. Mọi sản phẩm, thông số, đánh giá, số lượng đã bán
> và giá trên trang đều là **nội dung demo** để xem trước giao diện.
> Giá thật, tình trạng hàng, bảo hành và phí giao được shop xác nhận qua
> Facebook khi khách nhắn tin. Không có số điện thoại, địa chỉ hay Zalo thật
> nào được đăng trên trang — vì shop chưa cung cấp các thông tin đó.

## Cấu trúc

| File | Mô tả |
|---|---|
| `index.html` | Toàn bộ website: 1 file tĩnh duy nhất (Tailwind qua CDN + Google Fonts + vanilla JS, không cần build) |
| `_headers` | Header cache & bảo mật cho Cloudflare Pages |
| `README.md` | File này |
| `design-system/` | Design system (ui-ux-pro-max) — **không sửa** |

## Deploy lên Cloudflare Pages

Repo GitHub: `mishanguyen83-max/min.martlife`

1. Vào [Cloudflare Dashboard → Workers & Pages → Create → Pages → Connect to Git](https://dash.cloudflare.com/).
2. Chọn repo `mishanguyen83-max/min.martlife`, branch `main` (hoặc branch bạn dùng).
3. **Build settings:**
   - Framework preset: **None**
   - Build command: *(để trống)*
   - Build output directory: `/` (thư mục gốc)
   - Root directory: *(để trống)*
4. Bấm **Save and Deploy**. Mỗi lần push lên GitHub, Cloudflare tự deploy lại.
5. (Tùy chọn) Thêm custom domain trong Pages → Custom domains.

Vì site là file tĩnh thuần, không cần Node, không cần build step — deploy xong
là chạy ngay.

## Chạy thử ở máy local

```bash
cd min.martlife
python3 -m http.server 8000
# mở http://localhost:8000
```

## Cách sửa sản phẩm

Mở `index.html`, tìm mảng `PRODUCTS` (gần cuối file, trong thẻ `<script>`).
Mỗi sản phẩm là một object:

```js
{
  id: 1,
  name: "Camera trong nhà WiFi 2K",
  cat: "smarthome",        // "smarthome" hoặc "giadung"
  catLabel: "SmartHome",
  benefit: "Mô tả ngắn 1 dòng về lợi ích.",
  specs: ["Thông số 1", "Thông số 2", "Thông số 3"],
  price: 890000,           // giá demo (VND, số nguyên)
  old: 1190000,            // giá gạch ngang (demo)
  badge: "Bán chạy",       // "Bán chạy" | "Mới" | "Giảm giá demo"
  rating: 4.8,             // đánh giá demo
  sold: 120,               // số đã bán demo
  isNew: false,
  compat: "Google Home, Alexa, Apple HomeKit (demo)",
  icon: "camera"           // camera | lock | switch | bulb | plug | speaker
                           // robot | fryer | purifier | fan | kettle | cooktop
}
```

- **Thêm sản phẩm:** copy một object, tăng `id`, thêm vào mảng — lưới, bộ lọc,
  tìm kiếm, sắp xếp và modal tự cập nhật.
- **Đổi giá:** sửa `price` / `old`. Nhớ giữ nhãn “Giá demo” — đừng gỡ nhãn
  này cho tới khi giá là giá thật đã được shop xác nhận.
- **Đổi link Facebook:** sửa hằng số `FB` ở đầu script và các link trong HTML
  (tìm `facebook.com/profile.php?id=61596530125836`).
- **Combo:** sửa trực tiếp 3 thẻ combo trong section `#combo`.

## Design system

Theo `design-system/min-martlife/MASTER.md` (ui-ux-pro-max skill):

- Font: Plus Jakarta Sans; Primary `#1E293B`; CTA `#22C55E`; nền `#0F172A`; card `#1B2336`
- Glassmorphism (backdrop blur, viền trắng mờ 1px), transition 150–300ms
- Không dùng emoji làm icon — chỉ dùng SVG inline
- Focus visible, target chạm tối thiểu 44px, tôn trọng `prefers-reduced-motion`
- Responsive: 375 / 768 / 1024 / 1440px, tương phản tối thiểu 4.5:1

## Tính năng hiện có

- Header sticky + menu mobile, tìm kiếm, CTA “Nhắn Facebook”
- Hero dark glass + minh họa SVG nhà thông minh (không ảnh ngoài)
- Lọc theo danh mục, tìm kiếm, sắp xếp (mới nhất / giá / bán chạy demo)
- 12 sản phẩm demo (6 SmartHome + 6 gia dụng), modal chi tiết (Esc để đóng)
- 3 combo SmartHome demo, hướng dẫn đặt hàng 3 bước, FAQ
- Scroll reveal (tắt khi `prefers-reduced-motion`), nút về đầu trang

## Chưa có (để sau)

- Giỏ hàng / thanh toán (đặt hàng qua Facebook)
- Giá thật, kho hàng thật, form liên hệ, số điện thoại / địa chỉ / Zalo
