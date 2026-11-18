# Cây thông Noel ASCII 3D: popup cho website

Cây thông Noel 3D vẽ hoàn toàn bằng ký tự ASCII. Cây xoay tròn và mọc dần từ dưới lên, sau đó lần lượt hiện dây kim tuyến, quả châu, đèn nháy, hộp quà, ngôi sao và lời chúc. Tất cả hiện thành **một popup nổi** trên trang web của bạn.

| File | Dùng để |
|---|---|
| `christmas-tree.js` | Toàn bộ popup. Đây là file duy nhất bạn cần đưa lên. |
| `index.html` | Trang demo để xem thử (mở bằng trình duyệt). |
| `christmas-tree-with-code.js` | Bản sao lưu có thêm khung code chạy bên dưới cây, giống video. Muốn dùng bản này thì đổi tên nó thành `christmas-tree.js`. |

## Cách 1: website của bạn đã chạy trên GitHub Pages

1. Chép `christmas-tree.js` vào repo, cùng thư mục với file HTML của trang.
2. Mở file HTML đó, thêm dòng này ngay trước `</body>`:

   ```html
   <script src="christmas-tree.js" defer></script>
   ```

   Nếu file JS nằm trong thư mục con, sửa đường dẫn cho khớp, ví dụ `src="assets/js/christmas-tree.js"`.
   Trang dùng Jekyll (có thư mục `_layouts`) thì thêm vào `_layouts/default.html` để trang nào cũng có.
3. Đẩy lên GitHub:

   ```bash
   git add christmas-tree.js index.html
   git commit -m "Thêm popup cây thông Noel"
   git push
   ```

   Khoảng một phút sau GitHub Pages cập nhật xong, mở trang là popup hiện lên.

Không dùng git: trên github.com vào repo, chọn **Add file → Upload files**, kéo `christmas-tree.js` vào rồi **Commit changes**. Sau đó bấm biểu tượng bút chì trên file HTML để thêm thẻ `<script>` ngay trên web.

## Cách 2: website ở nơi khác, chỉ dùng GitHub để chứa file

1. Tạo một repo mới trên GitHub, ví dụ `christmas-tree`, rồi tải `christmas-tree.js` lên.
2. Vào **Settings → Pages**, chọn branch `main` rồi **Save**.
3. Trên trang web của bạn, thêm (thay `TEN-GITHUB` bằng tên tài khoản của bạn):

   ```html
   <script src="https://TEN-GITHUB.github.io/christmas-tree/christmas-tree.js" defer></script>
   ```

## Tuỳ chỉnh

Thêm thuộc tính vào chính thẻ `<script>`:

| Thuộc tính | Mặc định | Ý nghĩa |
|---|---|---|
| `data-open` | `session` | Khi nào tự mở: `session` mỗi lần vào trang một lần, `once` chỉ một lần duy nhất cho mỗi người xem, `always` mỗi lần tải trang, `never` không tự mở |
| `data-delay` | `800` | Chờ bao nhiêu mili-giây rồi mới tự mở |
| `data-message` | `MERRY CHRISTMAS 2026` | Lời chúc dưới gốc cây, gõ được tiếng Việt có dấu |
| `data-signature` | `HaiLC` | Dòng chữ nhỏ ở góc dưới bên trái |
| `data-button` | `true` | `false` để ẩn nút tròn ở góc màn hình |
| `data-position` | `right` | Nút tròn nằm góc `right` hay `left` |
| `data-fps` | `30` | Số khung hình mỗi giây, từ 12 đến 60 |

Ví dụ:

```html
<script src="christmas-tree.js" defer
  data-message="GIÁNG SINH AN LÀNH"
  data-signature="@ten.cua.ban"
  data-open="once"></script>
```

Hoặc cấu hình bằng JavaScript, đặt **trước** thẻ nạp file:

```html
<script>window.ChristmasTreeConfig = { message: 'GIÁNG SINH AN LÀNH', open: 'once' };</script>
```

## Mở popup bằng nút của riêng bạn

```html
<button onclick="ChristmasTree.open()">Xem cây thông</button>
```

Ngoài ra có `ChristmasTree.close()`, `ChristmasTree.toggle()` và `ChristmasTree.replay()`.
Khi popup đang mở: `Esc` để đóng, `Space` để tạm dừng, `R` để chạy lại.

## Dùng với React, Vue, Next.js

Đặt `christmas-tree.js` vào thư mục `public/`, rồi:

- Vite, Create React App, Vue: thêm `<script src="/christmas-tree.js" defer></script>` vào `index.html`.
- Next.js: trong layout, `import Script from 'next/script'` rồi đặt `<Script src="/christmas-tree.js" strategy="afterInteractive" />`. Các thuộc tính `data-*` đặt thẳng lên `<Script>`.

## Ghi chú

- Không dùng thư viện, không gửi dữ liệu đi đâu. Popup chỉ lưu một cờ nhỏ trong `sessionStorage` hoặc `localStorage` để nhớ là đã tự mở rồi.
- Chỉ vẽ khi popup đang mở và tự dừng khi tab bị ẩn, nên không làm nặng trang.
- Popup nằm trong Shadow DOM: CSS của trang bạn không làm vỡ popup và ngược lại.
- Ý tưởng hình ảnh lấy cảm hứng từ video ASCII art của @dwcminh.ascii trên TikTok. Code trong file này được viết mới.
