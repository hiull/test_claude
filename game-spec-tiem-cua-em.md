# TÀI LIỆU YÊU CẦU GAME: "TIỆM CỦA EM"

> **Gửi AI đang đọc tài liệu này (Gemini / Claude / bất kỳ trợ lý nào):**
> Đây là bản đặc tả đầy đủ cho một game nấu ăn – quản lý thời gian (time-management cooking game) làm tặng bạn gái.
> Hãy đọc **toàn bộ** tài liệu trước khi viết bất kỳ dòng code nào. Mọi con số, màu sắc, chữ hiển thị, hành vi đều đã được quy định ở đây.
> Nếu có điểm nào mâu thuẫn hoặc thiếu, **hỏi lại người dùng trước**, không tự đoán.
> Các chỗ ghi `[ĐIỀN: ...]` là thông tin cá nhân người dùng sẽ tự điền; nếu còn để trống thì dùng **giá trị mặc định** ghi kèm.

---

## MỤC LỤC

0. Nguyên tắc bắt buộc
1. Tổng quan game
2. Thông tin cá nhân hoá (người dùng điền)
3. Nền tảng & công nghệ
4. Cấu trúc thư mục & file
5. Màn hình & luồng điều hướng
6. Gameplay cốt lõi (vòng lặp chính)
7. Thực đơn, nguyên liệu, công thức
8. Khách hàng
9. Tính điểm, tiền, sao
10. Danh sách màn chơi (15 màn)
11. Cửa hàng nâng cấp
12. Hệ thống quà & kỷ niệm (phần "tặng bạn gái")
13. Giao diện (UI) chi tiết từng màn hình
14. Phong cách hình ảnh, màu sắc, font
15. Hoạt ảnh (animation) & hiệu ứng
16. Âm thanh & nhạc
17. Lưu game
18. Điều khiển & cảm ứng
19. Văn bản hiển thị (toàn bộ chữ trong game)
20. Hiệu năng & tương thích
21. Trường hợp đặc biệt (edge cases)
22. Tiêu chí nghiệm thu (checklist hoàn thành)
23. Lộ trình làm theo giai đoạn
24. Những điều KHÔNG được làm
25. Game tham khảo & tính năng học hỏi (**đọc kỹ: có thay đổi một số mục trên**)

---

## 0. NGUYÊN TẮC BẮT BUỘC

1. **Game là sản phẩm gốc.** Chỉ cùng *thể loại* với các game bán đồ ăn trên CH Play. **Không** dùng tên, nhân vật, hình ảnh, âm thanh, màn chơi hay logo của bất kỳ game có sẵn nào (ví dụ: không dùng tên "Tiệm Xôi Bà Sáu", không vẽ lại nhân vật của game đó).
2. **Toàn bộ chữ trong game bằng tiếng Việt có dấu**, đúng chính tả.
3. **Chạy trên trình duyệt điện thoại**, màn hình dọc, không cần cài đặt, không cần internet sau khi tải xong lần đầu.
4. **Không quảng cáo, không mua hàng thật, không thu thập dữ liệu**, không gửi gì lên server.
5. **Chỉ dùng tài nguyên miễn phí có giấy phép rõ ràng** (CC0 ưu tiên) hoặc tự vẽ bằng code (Canvas/SVG/emoji). Ghi nguồn trong `CREDITS.md`.
6. Code phải **dễ sửa**: mọi con số cân bằng game (giá, thời gian, số khách...) nằm trong **một file cấu hình** `config.js`, không viết cứng rải rác.
7. Thông tin cá nhân (tên, lời nhắn, ảnh) nằm trong **một file riêng** `personal.js` để người dùng tự sửa mà không cần hiểu code.

---

## 1. TỔNG QUAN GAME

| Mục | Nội dung |
|---|---|
| Tên game | **"Tiệm của [ĐIỀN: tên bạn gái]"** – mặc định: *"Tiệm của Em"* |
| Thể loại | Nấu ăn – quản lý thời gian, chơi theo màn |
| Người chơi | 1 người (bạn gái) |
| Thời lượng 1 màn | 60–120 giây |
| Tổng số màn | 15 màn chính + 1 màn bí mật |
| Tổng thời gian chơi hết | khoảng 30–45 phút |
| Độ khó | Dễ → vừa. Mục tiêu là **vui và cảm động**, không phải khó |
| Món chủ đề | **Bánh tráng**: trộn, nướng, cuốn, kèm trà tắc và nước mía (mục 7) |
| Bối cảnh | Một xe và tiệm bánh tráng vỉa hè trước cổng trường lúc chiều tà: mái hiên sọc, ghế nhựa đỏ, bếp than hồng, dây đèn vàng, cây hoa giấy |
| Nhân vật chính | Chủ tiệm = bạn gái (đứng sau quầy, không bắt buộc hiện hình; nếu hiện thì là nhân vật chibi tóc dài, tạp dề hồng) |
| Thông điệp | Mỗi màn qua được mở một kỷ niệm của hai người; màn cuối là lời nhắn đặc biệt |

**Một câu mô tả:** Khách đến quầy gọi món bằng bong bóng hình ảnh, người chơi chạm vào nguyên liệu theo đúng thứ tự để làm món, đưa cho khách trước khi khách hết kiên nhẫn, kiếm tiền đạt mục tiêu để qua màn, dùng tiền nâng cấp tiệm, và mở khoá ảnh/lời nhắn kỷ niệm.

---

## 2. THÔNG TIN CÁ NHÂN HOÁ (NGƯỜI DÙNG ĐIỀN)

Tất cả nằm trong file `personal.js`. Mẫu:

```js
// personal.js — CHỈ SỬA FILE NÀY ĐỂ CÁ NHÂN HOÁ
window.PERSONAL = {
  herName: "Em",                // [ĐIỀN: tên/biệt danh bạn gái] — hiện trên biển tiệm, lời chào
  myName: "Anh",                // [ĐIỀN: tên/biệt danh của bạn] — khách đặc biệt "Anh" ghé tiệm
  shopName: "Tiệm của Em",      // tên biển hiệu; nếu để trống sẽ tự thành "Tiệm của " + herName
  anniversary: "2024-02-14",    // [ĐIỀN: ngày quen nhau, YYYY-MM-DD] — dùng để đếm số ngày bên nhau
  favoriteDish: "bt_tron_kho_bo", // [ĐIỀN: id món bánh tráng cô ấy thích nhất, xem mục 7.3] — món này cho x2 tiền
  welcomeMessage: "Chào mừng bà chủ nhỏ của anh đến với tiệm! 💕",
  finalMessage: "Cảm ơn em vì đã ở bên anh. Tiệm này mãi là của em. Yêu em! ❤️",
  // 15 kỷ niệm, mỗi màn qua mở 1 cái. photo = đường dẫn ảnh trong thư mục assets/memories/
  memories: [
    { title: "Lần đầu gặp nhau", date: "2024-01-01", photo: "assets/memories/01.jpg", text: "[ĐIỀN: vài dòng kỷ niệm]" },
    // ... tổng cộng 15 mục. Nếu thiếu ảnh -> hiện khung trái tim vẽ bằng code + chữ.
  ],
  friends: [ // [ĐIỀN: tối đa 6 tên bạn bè chung] — dùng làm tên khách quen
    "Linh", "Tuấn", "Mai", "Hùng", "Trang", "Nam"
  ],
};
```

**Quy tắc:**
- Nếu ảnh không tồn tại hoặc tải lỗi → hiển thị ảnh thay thế: nền hồng nhạt `#FFE4EC`, trái tim đỏ `#FF5C8A` ở giữa, tiêu đề kỷ niệm bên dưới. **Không bao giờ hiện icon ảnh vỡ.**
- Ảnh nên nén ≤ 300 KB/ảnh, tỉ lệ 4:5 (ví dụ 800×1000). Game tự cắt vừa khung (object-fit: cover).
- Số ngày bên nhau = hôm nay − `anniversary`, hiển thị ở màn hình chính: "Đã bên nhau **N** ngày 💞".

---

## 3. NỀN TẢNG & CÔNG NGHỆ

| Mục | Yêu cầu |
|---|---|
| Ngôn ngữ | HTML5 + CSS + JavaScript thuần (ES2020). **Không cần build tool.** |
| Engine | **Phaser 3.80.1** tải từ CDN `https://cdn.jsdelivr.net/npm/phaser@3.80.1/dist/phaser.min.js` — *hoặc* Canvas 2D thuần nếu AI thấy đơn giản hơn. Chọn 1 và giữ nguyên suốt dự án. |
| Kích thước gốc | **720 × 1280** (dọc, 9:16). Tự co giãn vừa màn hình (Scale mode FIT, căn giữa), viền thừa tô màu nền `#FFF6EC`. |
| Hướng màn hình | Dọc. Nếu xoay ngang trên điện thoại → hiện lớp phủ "Xoay dọc điện thoại để chơi nhé 📱". |
| Trình duyệt hỗ trợ | Chrome Android 100+, Safari iOS 15+, Chrome/Edge máy tính. |
| Chạy offline | Có `manifest.json` + `service-worker.js` để "Thêm vào màn hình chính" như app (PWA). Tuỳ chọn ở giai đoạn cuối. |
| Lưu trữ | `localStorage` (xem mục 17). |
| Triển khai | Đưa lên **GitHub Pages** hoặc **Netlify** miễn phí → gửi link cho bạn gái. |
| Xuất APK (tuỳ chọn) | Dùng **Capacitor** bọc lại thành file APK. Làm sau cùng, không bắt buộc. |

---

## 4. CẤU TRÚC THƯ MỤC & FILE

```
tiem-cua-em/
├── index.html              # điểm vào, nạp các script theo thứ tự
├── style.css               # nền, font, lớp phủ xoay màn hình
├── personal.js             # thông tin cá nhân (mục 2)
├── config.js               # MỌI con số cân bằng game (mục 7–11)
├── src/
│   ├── main.js             # khởi tạo game, đăng ký scene
│   ├── save.js             # đọc/ghi localStorage
│   ├── audio.js            # quản lý âm thanh, bật/tắt
│   ├── scenes/
│   │   ├── BootScene.js    # nạp tài nguyên, thanh loading
│   │   ├── MenuScene.js    # màn hình chính
│   │   ├── MapScene.js     # chọn màn
│   │   ├── GameScene.js    # màn chơi
│   │   ├── ResultScene.js  # kết quả sau màn
│   │   ├── ShopScene.js    # nâng cấp
│   │   ├── AlbumScene.js   # album kỷ niệm
│   │   └── EndingScene.js  # kết thúc đặc biệt
│   └── objects/
│       ├── Customer.js
│       ├── Station.js      # trạm nguyên liệu
│       ├── Plate.js        # đĩa/khay đang làm món
│       └── UI.js           # nút, thanh tiến độ, popup dùng chung
├── assets/
│   ├── img/                # hình nguyên liệu, khách, nền
│   ├── sfx/                # hiệu ứng âm thanh
│   ├── music/              # nhạc nền
│   ├── fonts/
│   └── memories/           # ảnh kỷ niệm 01.jpg ... 15.jpg
├── manifest.json
├── service-worker.js
├── CREDITS.md              # nguồn tài nguyên & giấy phép
└── README.md               # cách chạy, cách sửa personal.js, cách đưa lên mạng
```

---

## 5. MÀN HÌNH & LUỒNG ĐIỀU HƯỚNG

```
[Boot/Loading] → [Màn hình chính]
                     ├─ "Mở tiệm" → [Bản đồ màn chơi] → [Màn chơi] → [Kết quả]
                     │                                                 ├─ "Màn tiếp" → [Màn chơi kế]
                     │                                                 ├─ "Chơi lại" → [Màn chơi đó]
                     │                                                 └─ "Về bản đồ" → [Bản đồ]
                     ├─ "Nâng cấp" → [Cửa hàng]
                     ├─ "Kỷ niệm" → [Album]
                     └─ ⚙️ → [Cài đặt: nhạc, âm thanh, rung, xoá dữ liệu]
Qua màn 15 → [Kết thúc đặc biệt] → mở khoá Màn bí mật
```

- Lần đầu mở game: hiện **popup chào mừng** với `welcomeMessage`, rồi tự vào **Màn 1 có hướng dẫn**.
- Nút "Quay lại" (← góc trên trái) có ở mọi màn hình trừ màn hình chính.
- Nút Back vật lý của Android: trong màn chơi → mở menu Tạm dừng; ở màn khác → về màn trước.

---

## 6. GAMEPLAY CỐT LÕI

### 6.1 Bố cục màn chơi (toạ độ trên khung 720×1280)

| Vùng | Toạ độ Y | Nội dung |
|---|---|---|
| Thanh trên (HUD) | 0–110 | Thời gian còn lại (trái), tiền / mục tiêu (giữa), nút ⏸ (phải) |
| Khu khách | 110–560 | Nền mặt tiền tiệm; **3 vị trí khách** ở x = 140, 360, 580 (mở rộng 4 vị trí khi nâng cấp: x = 110, 270, 450, 610) |
| Quầy | 560–700 | Mặt quầy gỗ; **2 khay làm món** ở x = 240 và 480 (nâng cấp lên 3: x = 160, 360, 560) |
| Khu nguyên liệu | 700–1180 | Lưới trạm nguyên liệu 4 cột × 3 hàng, mỗi ô 150×140, cách nhau 20 |
| Thanh dưới | 1180–1280 | Thùng rác 🗑 (trái), nút combo/chiêu đặc biệt (phải, mở từ màn 6) |

### 6.2 Vòng lặp chính

1. **Khách xuất hiện** ở vị trí trống, đi vào từ bên phải (0,6 giây), dừng lại, hiện **bong bóng gọi món** phía trên đầu.
2. Bong bóng hiện **hình món ăn** + các nguyên liệu nhỏ bên dưới (để người chơi biết công thức). Có **thanh kiên nhẫn** ngang dưới bong bóng.
3. Người chơi **chạm vào trạm nguyên liệu** → nguyên liệu bay vào **khay đang được chọn** (khay chọn có viền vàng `#FFC94D` dày 6px). Chạm vào khay khác để đổi khay chọn.
4. **Đế** (bánh tráng / ly) phải có trước, **bước kết thúc** (lắc / gấp / cuốn / rót) làm sau cùng; topping ở giữa thứ tự tuỳ ý (chi tiết mục 7.1). Thêm topping khi chưa có đế → không nhận, đồ đựng rung nhẹ.
5. Món **nướng** làm trên **vỉ than** theo thanh canh lửa (mục 7.1). Để kim chạy vào vùng đỏ → **cháy** (màu đen, có khói) → chỉ bỏ đi được.
6. Khi khay đã đủ món → chạm vào khay rồi chạm vào khách (hoặc **kéo thả** khay lên khách). Hỗ trợ cả 2 cách.
7. Giao **đúng món** → khách vui (biểu cảm 😍), trả tiền + tiền tip, đồng xu bay lên HUD, khách đi ra bên trái.
8. Giao **sai món** → khách lắc đầu (😕), món bị trả lại khay, mất 10% kiên nhẫn.
9. Hết kiên nhẫn → khách giận (😠), bỏ đi, **không trả tiền**, mất 1 "tim tiệm" (xem 6.4).
10. Hết giờ → kết thúc màn, sang màn Kết quả.

### 6.3 Thanh kiên nhẫn

- Màu theo phần trăm còn lại: **> 60% xanh lá `#5BD67A`**, **30–60% vàng `#FFC94D`**, **< 30% đỏ `#FF6B6B`** và nhấp nháy 2 lần/giây.
- Dưới 30%: khách đổi biểu cảm sang 😤 và bong bóng rung nhẹ (±3px).
- Thời gian kiên nhẫn gốc theo loại khách (mục 8), nhân với hệ số màn chơi (mục 10).

### 6.4 Tim tiệm

- Mỗi màn có **3 tim** ❤️❤️❤️ (hiện dưới HUD).
- Mỗi khách bỏ đi giận → mất 1 tim.
- Mất hết 3 tim → **thua màn ngay** (dù còn thời gian).
- Đây là game tặng nên dễ: từ lần thua thứ 2 liên tiếp ở cùng một màn, màn đó được **+20% kiên nhẫn khách** và hiện chữ "Anh giúp em một chút nha 😉".

### 6.5 Combo

- Giao đúng liên tiếp không để khách nào bỏ đi → tăng combo. Combo hiện chữ lớn ở giữa: "Combo x2!", "x3"...
- Tiền thưởng combo: +5% mỗi bậc, tối đa x10 (+50%).
- Combo reset khi: khách bỏ đi, hoặc giao sai món.

### 6.6 Chiêu đặc biệt (mở từ màn 6)

- Nút "💖 Năng lượng yêu thương" ở góc dưới phải, nạp dần khi giao đúng món (mỗi món +10%).
- Đầy 100% → chạm để kích hoạt: **đóng băng thanh kiên nhẫn mọi khách trong 8 giây**, nền có hiệu ứng trái tim bay.

---

## 7. THỰC ĐƠN, NGUYÊN LIỆU, CÔNG THỨC — CHỦ ĐỀ BÁNH TRÁNG 🫓

> **Chủ đề chính thức: tiệm bánh tráng vỉa hè**, vì bạn gái người dùng mê bánh tráng.
> Tiệm có **3 khu làm món + 1 quầy nước**, mỗi khu có cách làm (thao tác) riêng để game không nhàm chán.
> Mọi giá, thời gian, ngày mở khoá đều nằm trong `config.js`.

### 7.1 Bốn khu làm món

| Khu | Đồ đựng | Cách làm | Mở từ màn |
|---|---|---|---|
| 🥣 **Quầy trộn** | Bịch nilon hoặc tô | 1) Chạm **bánh tráng sợi** trước (luôn là bước đầu). 2) Thêm topping, **thứ tự tuỳ ý**. 3) Chạm **sốt/tắc**. 4) Bấm nút **"Lắc!"** rồi lắc: **vuốt qua lại 6 lần** trên bịch (hoặc chạm nhanh 6 lần), thanh "Độ đều" đầy thì xong. Chưa lắc mà giao → khách chê "Chưa trộn đều nè!" (tính sai món). | 1 |
| 🔥 **Bếp nướng than** | Vỉ nướng (2 vỉ, nâng cấp lên 3) | 1) Chạm **bánh tráng tròn** để đặt lên vỉ. 2) Chạm **trứng cút** (đập trứng), rồi **nhấn giữ 1 giây** để tán đều trứng (vòng tròn đầy). 3) Thêm topping, thứ tự tuỳ ý. 4) Thanh **canh lửa**: kim chạy từ trái sang phải trong 6 giây; vùng **xanh** = giòn vừa (+10% tiền), vàng = tạm được, **đỏ** = cháy (bỏ đi). Chạm vỉ để **gấp đôi bánh** và lấy ra đĩa. 5) Chạm **sốt** cuối cùng (mayonnaise / tương ớt). | 4 |
| 🌯 **Quầy cuốn** | Thớt tre | 1) Chạm **bánh tráng phơi sương** để trải ra thớt. 2) Thêm nhân, thứ tự tuỳ ý. 3) **Vuốt từ dưới lên** để cuốn (hoạt ảnh cuộn tròn). 4) Thêm **chén nước chấm** (chạm). | 7 |
| 🧋 **Quầy nước** | Ly nhựa | 1) Chạm **ly**. 2) **Nhấn giữ 2 giây** để rót (vòng tròn đầy). 3) Chạm **đá**. 4) Tuỳ món: thêm tắc hoặc topping. Quầy nước nằm bên phải, **vuốt ngang** hoặc bấm mũi tên ▶ để chuyển sang. | 2 |

**Quy tắc thứ tự (thay cho mục 6.2 bước 4):** chỉ **bước đầu** (đế bánh tráng / ly) và **bước cuối** (lắc / gấp / cuốn / rót) là bắt buộc đúng chỗ. Topping ở giữa **bỏ theo thứ tự nào cũng được**, nhưng phải **đủ và không thừa**. Thừa topping → khách nói "Chị đâu có gọi cái này!" (sai món). Thiếu → "Còn thiếu {topping} nè em!".

**Độ cay (sa tế / ớt):** từ màn 3, đơn có biểu tượng 🌶️ x0 đến x3. Chạm hũ **sa tế** mỗi lần +1 cấp, số cấp hiện trên đồ đựng. Sai độ cay tính là sai món.

### 7.2 Nguyên liệu

| id | Tên hiển thị | Emoji tạm | Khu | Mở ở màn | Giá nhập 5 phần (nếu dùng kho, mục 25.4) |
|---|---|---|---|---|---|
| `bt_soi` | Bánh tráng sợi | 🍜 | Trộn | 1 | 5k |
| `kho_bo` | Khô bò | 🥩 | Trộn, Cuốn | 1 | 15k |
| `trung_cut` | Trứng cút | 🥚 | Trộn, Nướng | 1 | 8k |
| `xoai` | Xoài xanh bào | 🥭 | Trộn | 1 | 6k |
| `rau_ram` | Rau răm | 🌿 | Trộn, Cuốn | 1 | 3k |
| `dau_phong` | Đậu phộng rang | 🥜 | Trộn, Nướng | 1 | 4k |
| `tac` | Tắc (quất) vắt | 🍋 | Trộn, Nước | 1 | 3k |
| `sa_te` | Sa tế | 🌶️ | Trộn, Nướng | 3 | 5k |
| `kho_muc` | Khô mực xé | 🦑 | Trộn | 3 | 18k |
| `hanh_phi` | Hành phi | 🧅 | Trộn, Nướng, Cuốn | 2 | 4k |
| `muoi_tom` | Muối tôm | 🧂 | Trộn, Cuốn | 5 | 4k |
| `bo_beo` | Bơ béo (sốt bơ) | 🧈 | Trộn, Cuốn | 5 | 8k |
| `bt_tron` | Bánh tráng tròn (nướng) | ⚪ | Nướng | 4 | 5k |
| `hanh_la` | Hành lá | 🌱 | Nướng | 4 | 3k |
| `xuc_xich` | Xúc xích | 🌭 | Nướng | 6 | 12k |
| `pho_mai` | Phô mai | 🧀 | Nướng | 9 | 15k |
| `cha_bong` | Chà bông | 🟫 | Nướng, Cuốn | 6 | 10k |
| `mayo` | Mayonnaise | 🥫 | Nướng | 4 | 6k |
| `tuong_ot` | Tương ớt | 🔴 | Nướng | 4 | 5k |
| `bt_phoi_suong` | Bánh tráng phơi sương | 📃 | Cuốn | 7 | 6k |
| `thit_luoc` | Thịt luộc | 🥓 | Cuốn | 7 | 15k |
| `rau_song` | Rau sống | 🥬 | Cuốn | 7 | 4k |
| `nuoc_cham` | Nước chấm me | 🫙 | Cuốn | 7 | 5k |
| `tom_kho` | Tép (tôm khô) | 🦐 | Trộn | 10 | 12k |
| `ly` | Ly nhựa | 🥤 | Nước | 2 | 2k |
| `tra` | Bình trà | 🫖 | Nước | 2 | 3k |
| `da` | Đá | 🧊 | Nước | 2 | 1k |
| `nuoc_mia` | Nước mía | 🎋 | Nước | 8 | 8k |
| `tran_chau` | Trân châu | ⚫ | Nước | 11 | 6k |

### 7.3 Công thức món

> Cột "Topping" là danh sách cần đủ, **thứ tự tuỳ ý**. "Đế" và "Kết thúc" bắt buộc đúng chỗ.

| id | Tên món | Khu | Đế | Topping | Kết thúc | Giá | Mở ở màn |
|---|---|---|---|---|---|---|---|
| `bt_tron_co_ban` | Bánh tráng trộn cơ bản | Trộn | bt_soi | xoai, rau_ram, dau_phong | tac → Lắc | 15k | 1 |
| `bt_tron_kho_bo` | Bánh tráng trộn khô bò | Trộn | bt_soi | kho_bo, trung_cut, xoai, rau_ram, dau_phong | tac → Lắc | 25k | 1 |
| `tra_da` | Trà đá | Nước | ly | – | rót tra → da | 3k | 2 |
| `tra_tac` | Trà tắc | Nước | ly | tac | rót tra → da | 10k | 2 |
| `bt_tron_hanh_phi` | Bánh tráng trộn hành phi | Trộn | bt_soi | trung_cut, hanh_phi, rau_ram, dau_phong | tac → Lắc | 20k | 2 |
| `bt_tron_kho_muc` | Bánh tráng trộn khô mực | Trộn | bt_soi | kho_muc, trung_cut, xoai, rau_ram, sa_te (theo cấp cay) | tac → Lắc | 30k | 3 |
| `bt_nuong_trung` | Bánh tráng nướng trứng | Nướng | bt_tron | trung_cut (đập + tán), hanh_la, dau_phong | canh lửa → gấp → mayo | 18k | 4 |
| `bt_bo` | Bánh tráng bơ | Trộn | bt_soi | bo_beo, muoi_tom, hanh_phi, rau_ram | Lắc | 22k | 5 |
| `bt_nuong_xuc_xich` | Bánh tráng nướng xúc xích | Nướng | bt_tron | trung_cut, xuc_xich, hanh_la, cha_bong | canh lửa → gấp → tuong_ot | 25k | 6 |
| `bt_cuon_bo` | Bánh tráng cuốn bơ | Cuốn | bt_phoi_suong | bo_beo, muoi_tom, cha_bong, kho_bo | Vuốt cuốn → nuoc_cham | 25k | 7 |
| `bt_cuon_thit` | Bánh tráng phơi sương cuốn thịt | Cuốn | bt_phoi_suong | thit_luoc, rau_song, rau_ram | Vuốt cuốn → nuoc_cham | 30k | 7 |
| `nuoc_mia_ly` | Nước mía | Nước | ly | tac | rót nuoc_mia → da | 12k | 8 |
| `bt_nuong_pho_mai` | Bánh tráng nướng phô mai | Nướng | bt_tron | trung_cut, pho_mai, xuc_xich, hanh_la | canh lửa → gấp → mayo | 32k | 9 |
| `bt_tron_dac_biet` | Bánh tráng trộn đặc biệt | Trộn | bt_soi | kho_bo, kho_muc, tom_kho, trung_cut, xoai, rau_ram, dau_phong, hanh_phi | tac → Lắc | 40k | 10 |
| `tra_sua_tran_chau` | Trà sữa trân châu | Nước | ly | tran_chau | rót tra → da | 20k | 11 |
| `combo_tinh_yeu` | **Combo Tình Yêu** 💕 | 2 khu | – | 1 phần **món cô ấy thích nhất** (`favoriteDish`) + 1 ly trà tắc, giao cùng lúc | – | 60k | 14 |

- **Một khách có thể gọi 2 món** (từ màn 8), thường là 1 món bánh tráng + 1 ly nước.
- Món `favoriteDish` (mặc định: `bt_tron_kho_bo`) có **giá x2** và viền hồng lấp lánh trong bong bóng gọi món.
- Đóng gói: món trộn giao trong **bịch buộc dây thun** (hoạt ảnh buộc 0,3 giây sau khi lắc xong), món nướng trên **giấy gói**, món cuốn trên **hộp xốp**.

### 7.4 Bố cục màn chơi theo khu (thay chi tiết cho mục 6.1)

- Khu nguyên liệu (y 700–1180) hiện **các trạm của khu đang đứng**. Thanh tab nhỏ phía trên khu nguyên liệu: `🥣 Trộn | 🔥 Nướng | 🌯 Cuốn | 🧋 Nước`. Khu chưa mở hiện ổ khoá 🔒.
- Đổi khu: chạm tab hoặc vuốt ngang. **Khay/đồ đựng đang làm dở được giữ nguyên** khi đổi khu.
- Tab có **chấm đỏ** khi có khách đang chờ món của khu đó.
- Bếp nướng luôn chạy kể cả khi đang đứng khu khác. Bánh sắp cháy (kim vào vùng đỏ) → tab 🔥 nhấp nháy đỏ và kêu "xèo xèo" to hơn.

---

## 8. KHÁCH HÀNG

### 8.1 Loại khách

| Loại | Hình dạng | Kiên nhẫn gốc | Tip | Đặc điểm | Xuất hiện từ màn |
|---|---|---|---|---|---|
| Học sinh | Áo trắng, cặp sách | 25 giây | +0–2 | Hay gọi món rẻ | 1 |
| Nhân viên văn phòng | Áo sơ mi, cà vạt | 18 giây | +3–5 | Vội, kiên nhẫn ngắn | 3 |
| Cô bán rau | Nón lá, gánh | 30 giây | +1–3 | Rất kiên nhẫn | 2 |
| Anh shipper | Mũ bảo hiểm, áo khoác | 15 giây | +5–8 | Rất vội, tip cao | 6 |
| Bà cụ | Tóc bạc, gậy | 35 giây | +2 | Đi vào chậm (1,2 giây) | 5 |
| Bạn bè (tên từ `friends`) | Như khách thường + **bảng tên** trên đầu | 30 giây | +5 | Hiện lời chào "Ghé tiệm [herName] nè!" | 4 |
| **"Anh"** (`myName`) | Áo hồng, cầm bó hoa 💐 | **Không bao giờ hết** | +20 | Xuất hiện **1 lần mỗi màn** từ màn 3, vào ngẫu nhiên giữa màn; khi được phục vụ thả 10 trái tim bay lên và câu nói ngẫu nhiên (mục 19.5) | 3 |
| Mèo con | Mèo cam | 20 giây | 0, nhưng **+1 tim** | Chỉ "gọi" 1 trứng cút (chạm trạm trứng cút rồi chạm mèo); rất hiếm (5%) | 7 |

- Nếu chưa có hình vẽ: vẽ khách bằng hình tròn (đầu) + hình chữ nhật bo góc (thân), màu áo khác nhau, mặt bằng emoji. Vẫn phải phân biệt rõ từng loại.

### 8.2 Sinh khách

- Khoảng cách giữa 2 khách: ngẫu nhiên trong khoảng `[spawnMin, spawnMax]` giây của màn (mục 10).
- Chỉ sinh khách khi còn vị trí trống. Nếu đầy, khách tiếp theo chờ.
- Món khách gọi: chọn ngẫu nhiên trong danh sách món đã mở ở màn đó, **có trọng số**: món mới mở ở màn hiện tại có trọng số x2 để người chơi luyện.
- 10 giây cuối màn: không sinh khách mới.

---

## 9. TÍNH ĐIỂM, TIỀN, SAO

- **Tiền nhận mỗi món** = giá gốc × hệ số tốc độ + tip + thưởng combo.
- **Hệ số tốc độ**: giao khi kiên nhẫn còn > 60% → x1.2 (hiện chữ "Nhanh quá! ⚡"); 30–60% → x1.0; < 30% → x0.8.
- Đơn vị tiền hiển thị: **"k"** (nghìn đồng), ví dụ "18k". Biểu tượng: đồng xu vàng 🪙.
- **Sao** theo tiền kiếm được trong màn so với mục tiêu:
  - ⭐ = đạt mục tiêu (bắt buộc để qua màn)
  - ⭐⭐ = đạt 130% mục tiêu
  - ⭐⭐⭐ = đạt 160% mục tiêu **và** không khách nào bỏ đi
- Tiền kiếm được cộng vào **ví tổng** (dùng mua nâng cấp), kể cả khi thua màn (được 50%).
- Chơi lại màn đã qua: vẫn nhận tiền bình thường, sao chỉ lưu kết quả cao nhất.

---

## 10. DANH SÁCH MÀN CHƠI

| Màn | Thời gian | Mục tiêu | spawnMin–Max (giây) | Hệ số kiên nhẫn | Mở mới | Ghi chú |
|---|---|---|---|---|---|---|
| 1 | 60 | 60k | 6–8 | 1.3 | BT trộn cơ bản, BT trộn khô bò | **Có hướng dẫn từng bước (quầy trộn)** |
| 2 | 70 | 90k | 5–7 | 1.25 | quầy nước (trà đá, trà tắc), BT trộn hành phi | Hướng dẫn ngắn: vuốt sang quầy nước, nhấn giữ để rót |
| 3 | 75 | 120k | 5–7 | 1.2 | BT trộn khô mực, độ cay sa tế | Khách "Anh" xuất hiện lần đầu |
| 4 | 80 | 150k | 4.5–6.5 | 1.2 | **bếp nướng**, BT nướng trứng | **Hướng dẫn bếp nướng** (đập trứng, giữ tán, canh lửa, gấp) |
| 5 | 80 | 180k | 4.5–6 | 1.15 | bánh tráng bơ | |
| 6 | 90 | 220k | 4–6 | 1.15 | BT nướng xúc xích | Mở chiêu đặc biệt 💖 |
| 7 | 90 | 260k | 4–5.5 | 1.1 | **quầy cuốn**, BT cuốn bơ, BT phơi sương cuốn thịt | Hướng dẫn vuốt để cuốn |
| 8 | 90 | 300k | 4–5.5 | 1.1 | nước mía | Khách gọi 2 món |
| 9 | 100 | 350k | 3.5–5 | 1.05 | BT nướng phô mai | |
| 10 | 100 | 400k | 3.5–5 | 1.05 | BT trộn đặc biệt | Màn "Ngày mưa": khách gọi đồ nướng nhiều gấp đôi |
| 11 | 100 | 450k | 3.5–5 | 1.0 | trà sữa trân châu | |
| 12 | 110 | 520k | 3–4.5 | 1.0 | – | Màn "Tan trường": nhóm học sinh đến liên tục |
| 13 | 110 | 580k | 3–4.5 | 1.0 | – | Màn "Sáng Chủ Nhật" (đông khách) |
| 14 | 120 | 650k | 3–4.5 | 1.0 | Combo Tình Yêu | |
| 15 | 120 | 720k | 3–4 | 1.0 | – | Màn cuối: nền hoàng hôn, kết thúc mở EndingScene |
| ★ Bí mật | 90 | không có | 3–4 | 1.0 | – | Chỉ có khách "Anh" và bạn bè; không thua được; chơi để vui |

- **Bản đồ màn**: 15 nút tròn trên đường quanh co (như con đường trong phố), màn chưa mở hiện ổ khoá 🔒, màn đã qua hiện số sao.
- Màn N+1 mở khi màn N đạt ít nhất 1 sao.

---

## 11. CỬA HÀNG NÂNG CẤP

| id | Tên | Cấp | Giá mỗi cấp | Tác dụng |
|---|---|---|---|---|
| `khay` | Thêm khay | 2 → 3 | 300k | 3 khay làm món |
| `bep` | Thêm vỉ nướng | 2 → 3 → 4 | 200k, 450k | Nướng nhiều bánh cùng lúc |
| `bep_nhanh` | Than hồng loại 1 | 0 → 3 | 150k, 300k, 500k | Kim canh lửa chạy nhanh hơn 10/20/30% và vùng xanh rộng hơn |
| `ghe` | Thêm chỗ khách | 3 → 4 | 400k | 4 vị trí khách (khách nhiều hơn, tiền nhiều hơn) |
| `quat` | Quạt máy | 0 → 2 | 200k, 400k | Kiên nhẫn khách +10% / +20% |
| `nhac` | Loa nhạc | 0 → 1 | 250k | Tip +20% |
| `chong_chay` | Quạt than tay | 0 → 1 | 300k | Vùng vàng sau vùng xanh dài gấp đôi, khó cháy hơn |
| `lac_nhanh` | Bịch dây kéo | 0 → 1 | 200k | Lắc chỉ cần 4 lần thay vì 6 |
| Trang trí (chỉ để đẹp) | Đèn lồng, chậu hoa giấy, biển tên neon, mèo thần tài, rèm hồng | 1 | 100k–300k | Hiện trong khung cảnh tiệm |

- Mỗi thẻ nâng cấp: hình, tên, mô tả 1 dòng, cấp hiện tại (chấm tròn ●●○), giá, nút "Mua". Không đủ tiền → nút xám, chữ "Thiếu Xk".
- Mua thành công: âm thanh "ting", thẻ nhún lên (scale 1 → 1.1 → 1, 0,25 giây), pháo giấy nhỏ.

---

## 12. HỆ THỐNG QUÀ & KỶ NIỆM

1. **Qua mỗi màn lần đầu** → mở khoá 1 kỷ niệm (theo thứ tự trong `memories`).
   - Hiệu ứng: phong bì hồng ✉️ rơi xuống giữa màn hình → chạm để mở → ảnh trượt ra → tiêu đề, ngày, đoạn văn hiện dần từng chữ (30 ms/chữ, chạm để hiện hết ngay).
2. **Album**: lưới 3 cột × 5 hàng. Kỷ niệm đã mở hiện ảnh thu nhỏ; chưa mở hiện phong bì khoá + "Qua màn N để mở". Chạm vào để xem lớn, vuốt trái/phải để chuyển.
3. **Đạt 3 sao màn bất kỳ** → nhận 1 "trái tim vàng" 💛. Đủ 15 trái tim vàng (3 sao mọi màn) → mở **lời nhắn ẩn thứ 2** `[ĐIỀN: thêm trường bonusMessage trong personal.js]`.
4. **EndingScene** (sau màn 15):
   - Màn hình tối dần → tiệm sáng đèn vàng → khách "Anh" bước vào cầm bó hoa.
   - Chữ `finalMessage` hiện từng chữ ở giữa, font viết tay, cỡ 44.
   - Sau đó: trình chiếu tất cả ảnh kỷ niệm (mỗi ảnh 3 giây, chuyển mờ dần), nhạc nền ending.
   - Cuối cùng: "Đã bên nhau N ngày. Và còn nhiều nữa 💞" + nút "Về tiệm".
5. **Ngày đặc biệt**: nếu ngày hiện tại trùng ngày tháng của `anniversary` → màn hình chính có pháo hoa và câu "Chúc mừng kỷ niệm của tụi mình! 🎉".

---

## 13. GIAO DIỆN CHI TIẾT TỪNG MÀN HÌNH

### 13.1 Boot / Loading
- Nền `#FFF6EC`. Giữa: biểu tượng bịch bánh tráng trộn (vẽ bằng code) lắc qua lại.
- Thanh tải 400×24, bo góc 12, nền `#FFE0C2`, phần đầy `#FF8FAB`. Dưới: "Đang nhóm than... 42%".

### 13.2 Màn hình chính
- Nền: mặt tiền tiệm (mái hiên sọc hồng–trắng, biển hiệu ghi `shopName`).
- Tiêu đề lớn trên biển, font viết tay, màu `#C2185B`, viền trắng 4px.
- Dòng "Đã bên nhau N ngày 💞" dưới biển, cỡ 28.
- 3 nút lớn xếp dọc giữa màn (mỗi nút 460×110, bo góc 28, đổ bóng): **"Mở tiệm"** (hồng `#FF5C8A`), **"Nâng cấp"** (cam `#FF9F43`), **"Kỷ niệm"** (tím nhạt `#B388FF`). Chữ trắng, đậm, cỡ 40.
- Góc trên phải: ⚙️. Góc trên trái: ví tiền 🪙 1.250k.
- Nhạc nền menu.

### 13.3 Bản đồ
- Cuộn dọc, màn 1 ở dưới cùng, màn 15 ở trên cùng. Tự cuộn đến màn mới nhất khi mở.
- Mỗi nút màn: tròn đường kính 110, số màn ở giữa, sao bên dưới.
- Chạm vào màn → popup: "Màn 5", mục tiêu "180k", món mới (hình), nút "Bắt đầu".

### 13.4 Màn chơi
- Xem bố cục mục 6.1.
- HUD: ⏱ "1:20" (dưới 10 giây chữ đỏ và phóng to nhẹ mỗi giây), tiền "85k / 150k" kèm thanh tiến độ nhỏ, ⏸.
- **Đếm ngược bắt đầu**: "3, 2, 1, Mở tiệm thôi!" (mỗi số 0,7 giây, phóng to rồi mờ dần).
- **Menu tạm dừng**: lớp phủ đen 50%, bảng giữa: "Tạm dừng", nút "Chơi tiếp", "Chơi lại", "Về bản đồ", công tắc nhạc/âm thanh.
- **Hướng dẫn (màn 1, 4)**: lớp phủ tối, khoét sáng vùng cần chạm, bàn tay 👆 nhấp nháy chỉ vào, khung chữ phía trên. Các bước màn 1:
  1. "Có khách rồi! Nhìn bong bóng để biết khách muốn gì nha."
  2. "Chạm **Bánh tráng sợi** trước để bỏ vào bịch."
  3. "Giờ thêm **Xoài**, **Rau răm**, **Đậu phộng**. Cái nào trước cũng được!"
  4. "Vắt **Tắc** vào rồi bấm **Lắc!** — vuốt qua lại thật đều tay nha!"
  5. "Xong rồi! Chạm vào bịch rồi chạm vào khách để giao."
  6. "Giỏi quá! Khách hết kiên nhẫn sẽ bỏ đi, nhanh tay nha 💪"
  - Trong hướng dẫn thời gian không chạy và khách không mất kiên nhẫn.

### 13.5 Kết quả
- Thắng: "Tuyệt vời! 🎉", sao hiện lần lượt (mỗi sao 0,4 giây, kèm âm "ting" cao dần), thống kê: tiền kiếm được, số khách phục vụ, combo cao nhất, khách bỏ đi. Sau đó phong bì kỷ niệm (nếu lần đầu qua).
- Thua: "Tiếc quá! 😢" + câu động viên ngẫu nhiên (mục 19.6), vẫn hiện tiền nhận (50%).
- Nút: "Màn tiếp" (chỉ khi thắng), "Chơi lại", "Về bản đồ".

### 13.6 Cửa hàng – xem mục 11. Danh sách cuộn dọc, ví tiền cố định ở trên.

### 13.7 Album – xem mục 12.

### 13.8 Cài đặt
- Công tắc: Nhạc nền, Âm thanh, Rung (chỉ hiện nếu thiết bị hỗ trợ `navigator.vibrate`).
- Nút "Xoá dữ liệu" màu đỏ → hỏi lại 2 lần: "Em chắc chưa? Mọi tiến trình sẽ mất đó!" → "Xoá thật" / "Thôi".
- Dòng nhỏ cuối: "Làm bằng cả trái tim bởi [myName] ❤️".

---

## 14. PHONG CÁCH HÌNH ẢNH, MÀU SẮC, FONT

### 14.1 Phong cách
- **Dễ thương, chibi, nét tròn, màu pastel ấm**, viền nâu đậm `#5D4037` dày 3–4px cho nhân vật và đồ vật (kiểu sticker).
- Không dùng màu đen thuần cho viền, không dùng bóng đổ gắt.
- Bóng đổ mềm: `rgba(93,64,55,0.25)`, lệch Y 6px, mờ 12px.

### 14.2 Bảng màu (đặt trong `config.js`)

| Tên | Mã | Dùng cho |
|---|---|---|
| Nền kem | `#FFF6EC` | Nền chung |
| Hồng chính | `#FF5C8A` | Nút chính, điểm nhấn |
| Hồng nhạt | `#FFE4EC` | Nền thẻ, popup |
| Hồng đậm | `#C2185B` | Tiêu đề |
| Cam | `#FF9F43` | Nút phụ, bếp |
| Vàng | `#FFC94D` | Viền chọn, đồng xu, sao |
| Xanh lá | `#5BD67A` | Thành công, kiên nhẫn cao |
| Đỏ | `#FF6B6B` | Cảnh báo |
| Tím nhạt | `#B388FF` | Nút kỷ niệm |
| Nâu viền | `#5D4037` | Viền, chữ thân |
| Gỗ quầy | `#C68B59` / `#A0673D` | Quầy (2 tông) |
| Trắng | `#FFFFFF` | Chữ trên nút |

### 14.3 Font (Google Fonts, có hỗ trợ tiếng Việt)
- Tiêu đề / số lớn: **"Baloo 2"** đậm (700–800).
- Chữ thường: **"Nunito"** (600).
- Lời nhắn, ending: **"Dancing Script"** hoặc **"Pacifico"** (kiểm tra hiển thị dấu tiếng Việt; nếu lỗi dấu thì dùng "Baloo 2").
- Phải tải font **trước** khi vẽ chữ (dùng `document.fonts.load`), tránh chữ bị nhảy font.
- Cỡ chữ tối thiểu trong game: **24px** (trên khung 720).

### 14.4 Nguồn hình
- Ưu tiên: **Kenney.nl** (CC0) – bộ "Food Kit", "UI Pack", "Toon Characters".
- Thiếu hình món Việt (bánh tráng, khô bò, xoài bào...) → **vẽ bằng code** (Canvas/SVG) theo phong cách sticker ở 14.1, hoặc dùng emoji phóng to đặt trên đĩa tròn trắng.
- Giai đoạn 1 được phép dùng emoji toàn bộ; giai đoạn sau thay hình.

---

## 15. HOẠT ẢNH & HIỆU ỨNG

| Sự kiện | Hiệu ứng | Thời lượng |
|---|---|---|
| Chạm nút | Thu nhỏ còn 0.92 rồi bật về 1 | 0,12 giây |
| Khách đi vào | Trượt từ phải + nhún lên xuống như đang đi (±4px, 4 lần) | 0,6 giây |
| Khách đi ra | Trượt sang trái, mờ dần | 0,5 giây |
| Bong bóng gọi món | Phóng to từ 0 lên 1 kiểu nảy (ease back-out) | 0,3 giây |
| Nguyên liệu vào khay | Bay theo đường cong từ trạm đến khay, hạ xuống, khay nhún | 0,25 giây |
| Đặt lên vỉ than | Bánh tráng rơi xuống vỉ, phồng nhẹ, khói nhỏ và tàn than đỏ bay lên | – |
| Lắc bịch | Bịch nghiêng theo hướng vuốt ±15°, topping xáo trộn, thanh "Độ đều" tăng | mỗi lần 0,15 giây |
| Cuốn bánh | Bánh cuộn tròn từ dưới lên theo ngón tay | 0,4 giây |
| Gấp bánh nướng | Bánh gập đôi thành nửa vầng trăng | 0,3 giây |
| Món chín | 3 tia lấp lánh ✨ | 0,4 giây |
| Món cháy | Chuyển màu đen, khói xám dày | 0,5 giây |
| Giao đúng | Khách nhảy lên 20px, 3 trái tim nhỏ bay lên, đồng xu bay về HUD (cong), số tiền "+22k" màu vàng bay lên mờ dần | 0,8 giây |
| Giao sai | Khách lắc ngang ±8px 3 lần, chữ "Không phải món này!" | 0,4 giây |
| Khách giận bỏ đi | Mặt đỏ, đám mây giận 💢, đi ra nhanh | 0,4 giây |
| Mất tim | Tim trên HUD vỡ đôi, rơi xuống | 0,5 giây |
| Combo | Chữ "Combo x3!" phóng to giữa màn, màu cầu vồng | 0,6 giây |
| Bỏ thùng rác | Món xoay và thu nhỏ vào thùng, thùng lắc | 0,3 giây |
| Thắng màn | Pháo giấy (confetti) 80 mảnh màu hồng/vàng/xanh | 2 giây |
| Khách "Anh" được phục vụ | 10 trái tim to bay lên toàn màn hình | 1,5 giây |

- Mọi hoạt ảnh dùng easing mềm (sine/back/quad), **không dừng đột ngột**.
- Khung hình mục tiêu: **60 FPS**; tối thiểu chấp nhận 30 FPS trên máy yếu.

---

## 16. ÂM THANH & NHẠC

| Tên file | Khi nào | Ghi chú |
|---|---|---|
| `music_menu.mp3` | Màn hình chính, bản đồ, cửa hàng | Vui nhẹ, lặp lại |
| `music_game.mp3` | Màn chơi | Nhịp nhanh hơn; 15 giây cuối tăng tốc 1.1x |
| `music_rain.mp3` | Màn 10 | Nhẹ nhàng + tiếng mưa |
| `music_ending.mp3` | EndingScene | Piano/acoustic cảm động |
| `sfx_tap.mp3` | Chạm nút | Ngắn |
| `sfx_add.mp3` | Thêm nguyên liệu | "Pụp" |
| `sfx_sizzle.mp3` | Bánh trên vỉ than | Lặp khi có bánh trên vỉ, to dần khi sắp cháy |
| `sfx_shake.mp3` | Lắc bịch bánh tráng | Tiếng sột soạt nilon, mỗi lần vuốt 1 tiếng |
| `sfx_crack.mp3` | Đập trứng cút | "Cạch" nhỏ |
| `sfx_roll.mp3` | Cuốn bánh | Tiếng sột nhẹ |
| `sfx_pour.mp3` | Rót nước | Lặp trong lúc nhấn giữ |
| `sfx_ready.mp3` | Món chín | "Ting" |
| `sfx_burn.mp3` | Món cháy | "Xèo" + "phụt" |
| `sfx_coin.mp3` | Nhận tiền | Leng keng |
| `sfx_wrong.mp3` | Sai | "Bùm" nhẹ, không chói |
| `sfx_angry.mp3` | Khách giận | "Hừm" |
| `sfx_star.mp3` | Hiện sao | Cao dần theo từng sao |
| `sfx_win.mp3` / `sfx_lose.mp3` | Kết quả | |
| `sfx_letter.mp3` | Mở phong bì kỷ niệm | Tiếng giấy + chuông |
| `sfx_heart.mp3` | Khách "Anh" | Ngọt ngào |

- Nguồn: **Kenney.nl Audio** (CC0), **Pixabay Music** (giấy phép Pixabay), **freesound.org** (chỉ chọn CC0).
- Trình duyệt chặn tự phát âm thanh → **chỉ bật nhạc sau lần chạm đầu tiên** của người dùng.
- Âm lượng mặc định: nhạc 50%, hiệu ứng 80%. Tắt/mở lưu vào save.
- Khi tab bị ẩn (chuyển app) → tự tạm dừng game và nhạc.
- Rung (nếu bật): 30 ms khi giao đúng, 80 ms khi khách giận.

---

## 17. LƯU GAME

- Khoá `localStorage`: `tiemcuaem_save_v1`. Lưu dạng JSON:

```json
{
  "version": 1,
  "wallet": 1250,
  "levels": { "1": { "stars": 3, "best": 95 }, "2": { "stars": 2, "best": 120 } },
  "unlockedLevel": 3,
  "upgrades": { "khay": 2, "bep": 3, "bep_nhanh": 1, "ghe": 3, "quat": 0, "nhac": 0, "chong_chay": 0 },
  "decor": ["den_long"],
  "memoriesUnlocked": [0, 1],
  "goldHearts": 1,
  "settings": { "music": true, "sfx": true, "vibrate": true },
  "tutorialDone": { "basic": true, "stove": false },
  "endingSeen": false,
  "firstOpen": "2026-11-20"
}
```

- Lưu ngay sau: kết thúc màn, mua nâng cấp, đổi cài đặt, mở kỷ niệm.
- Đọc save lỗi / sai định dạng → bắt lỗi (try/catch), **không crash**, tạo save mới.
- `localStorage` không dùng được (chế độ ẩn danh) → game vẫn chơi được, hiện thông báo nhỏ "Chế độ ẩn danh: tiến trình sẽ không được lưu".

---

## 18. ĐIỀU KHIỂN & CẢM ỨNG

- Hỗ trợ **chạm** (điện thoại) và **chuột** (máy tính) như nhau.
- Vùng chạm tối thiểu **88×88px** (trên khung 720), kể cả khi hình nhỏ hơn.
- Chạm nhanh liên tục (spam) vào trạm: mỗi lần chạm thêm 1 nguyên liệu, khoảng cách tối thiểu giữa 2 lần nhận là 80 ms.
- Kéo thả khay: khi kéo, khay theo ngón tay, phóng to 1.1; thả trúng khách → giao; thả ra ngoài → khay bay về chỗ cũ.
- Chặn thao tác mặc định của trình duyệt: không zoom bằng 2 ngón, không chọn chữ, không menu giữ lâu, không kéo trang (`touch-action: none`, `user-select: none`).
- Bàn phím (máy tính, tuỳ chọn): Esc = tạm dừng, phím 1/2/3 = chọn khay.

---

## 19. VĂN BẢN HIỂN THỊ

### 19.1 Nút & nhãn
"Mở tiệm", "Nâng cấp", "Kỷ niệm", "Cài đặt", "Bắt đầu", "Chơi tiếp", "Chơi lại", "Màn tiếp", "Về bản đồ", "Về tiệm", "Mua", "Đã tối đa", "Thiếu {x}k", "Mục tiêu", "Màn {n}", "Nhạc nền", "Âm thanh", "Rung", "Xoá dữ liệu".

### 19.2 Lời khen khi giao đúng (ngẫu nhiên)
"Ngon quá!", "Tuyệt cú mèo!", "Bà chủ giỏi ghê!", "Mai ghé nữa nha!", "Đúng món luôn!", "10 điểm!"

### 19.3 Khi giao nhanh
"Nhanh quá! ⚡", "Siêu tốc!", "Chớp nhoáng!"

### 19.4 Khách giận
"Lâu quá à...", "Thôi đi chỗ khác!", "Đói xỉu rồi 😩"

### 19.5 Khách "Anh" nói (ngẫu nhiên) — `[ĐIỀN: thêm câu riêng của hai người]`
"Anh đói, nhưng nhớ em hơn 💕", "Món nào em làm cũng ngon nhất!", "Cho anh một bịch bánh tráng và một phần trái tim em nhé", "Bánh tráng em trộn ngon hơn cả trường bên kia!", "Anh thích nhất là món em thích nhất 😋", "Bà chủ đáng yêu quá!", "Anh ghé chỉ để nhìn em thôi 😳"

### 19.6 Động viên khi thua
"Không sao, mình làm lại nha! 💪", "Em làm tốt lắm rồi, thử lần nữa nào!", "Anh tin em làm được mà ❤️"

### 19.7 Bạn bè chào
"Ghé tiệm {herName} nè!", "Nghe nói tiệm này ngon nhất phố!", "Cho mình như cũ nha!"

---

## 20. HIỆU NĂNG & TƯƠNG THÍCH

- Tổng dung lượng tải lần đầu (không tính ảnh kỷ niệm): **≤ 8 MB**.
- Thời gian tải trên 4G: **≤ 5 giây**.
- Hình gom thành **sprite sheet / atlas** khi có thể; hình ≤ 1024×1024 mỗi tấm.
- Nhạc: MP3 128 kbps, mỗi bản ≤ 1,5 MB.
- Không rò rỉ bộ nhớ khi chơi lại nhiều lần (huỷ tween, timer, sự kiện khi rời scene).
- Thử trên: 1 điện thoại Android tầm trung, 1 iPhone (Safari), Chrome máy tính.

---

## 21. TRƯỜNG HỢP ĐẶC BIỆT

| Tình huống | Xử lý |
|---|---|
| Chạm trạm khi không chọn khay nào | Tự chọn khay trống đầu tiên; không còn khay trống → khay rung + "Hết khay rồi!" |
| Khay đã đủ món mà vẫn chạm thêm nguyên liệu | Không thêm, khay rung nhẹ |
| Món cần nấu nhưng bếp đầy | Trạm rung + "Bếp đầy rồi!" |
| Chạm vào nguyên liệu chưa chín trên bếp | Không lấy được, thanh nấu nhấp nháy |
| Giao món khi khách đang đi vào (chưa đứng yên) | Không nhận, chờ khách đứng yên |
| Hết giờ khi đang kéo khay | Huỷ kéo, khay về chỗ |
| Khách đặc biệt "Anh" chưa xuất hiện mà màn sắp hết | Ép xuất hiện ở giây thứ 30 trước khi hết |
| Chuyển app / khoá màn hình giữa màn | Tự tạm dừng; quay lại thấy menu Tạm dừng |
| Xoay ngang | Lớp phủ yêu cầu xoay dọc + tạm dừng |
| Màn hình rất dài (20:9) hoặc máy tính bảng | Giữ khung 720×1280 căn giữa, phần thừa tô màu nền + hoa văn nhẹ |
| `personal.js` thiếu trường | Dùng giá trị mặc định, ghi cảnh báo trong console, không crash |
| Số kỷ niệm < 15 | Màn không có kỷ niệm tương ứng → mở thẻ "Kỷ niệm sắp tới... 💌" |
| Font chưa tải xong | Chờ tối đa 3 giây rồi dùng font dự phòng `sans-serif` |

---

## 22. TIÊU CHÍ NGHIỆM THU

Game được coi là **xong** khi tất cả đều đúng:

- [ ] Mở link trên điện thoại, chơi được ngay, không lỗi trong console.
- [ ] Toàn bộ chữ tiếng Việt có dấu, không lỗi font.
- [ ] Màn 1 có hướng dẫn đầy đủ 6 bước; màn 4 có hướng dẫn bếp.
- [ ] Đủ 15 màn + màn bí mật, đúng thông số bảng mục 10.
- [ ] Đủ 14 món, đúng công thức và thứ tự mục 7.
- [ ] Đủ 8 loại khách, phân biệt được bằng mắt.
- [ ] Thanh kiên nhẫn đổi màu đúng ngưỡng; tim tiệm hoạt động; thua khi mất 3 tim.
- [ ] Bếp: nấu → chín → cháy đúng thời gian.
- [ ] Combo, chiêu đặc biệt, sao, ví tiền tính đúng công thức mục 9.
- [ ] Cửa hàng mua được, tác dụng nâng cấp có hiệu lực ngay ở màn sau.
- [ ] Kỷ niệm mở đúng thứ tự, album xem được, ảnh lỗi có ảnh thay thế.
- [ ] EndingScene chạy đủ: khách "Anh", lời nhắn, trình chiếu ảnh, số ngày bên nhau.
- [ ] Đóng trình duyệt rồi mở lại → tiến trình còn nguyên.
- [ ] Nhạc/âm thanh bật tắt được và được ghi nhớ.
- [ ] Chạy mượt (không giật rõ) trên điện thoại Android tầm trung.
- [ ] Sửa tên trong `personal.js` → tên mới hiện khắp game.
- [ ] Sửa giá/thời gian trong `config.js` → có hiệu lực, không cần sửa chỗ khác.
- [ ] Có `README.md` hướng dẫn: chạy thử trên máy, thay ảnh, sửa lời nhắn, đưa lên GitHub Pages.
- [ ] Có `CREDITS.md` ghi nguồn mọi tài nguyên.

---

## 23. LỘ TRÌNH LÀM THEO GIAI ĐOẠN

> AI hãy làm **từng giai đoạn một**, gửi code + hướng dẫn chạy thử, **chờ người dùng xác nhận** rồi mới sang giai đoạn sau.

| Giai đoạn | Nội dung | Kết quả kiểm tra được |
|---|---|---|
| **1. Lõi chơi được** | GameScene với emoji: 3 khách, 2 khay, 4 nguyên liệu, 2 món, thanh kiên nhẫn, tiền, hết giờ | Chơi được màn 1 không hướng dẫn |
| **2. Hệ thống đầy đủ** | Tất cả món, bếp, tim, combo, 15 màn, bản đồ, kết quả, sao, lưu game | Chơi từ màn 1 đến 15 |
| **3. Cá nhân hoá** | `personal.js`, khách "Anh", bạn bè, kỷ niệm, album, ending, số ngày bên nhau | Thấy tên và ảnh riêng |
| **4. Cửa hàng & cân bằng** | Nâng cấp, trang trí, chiêu đặc biệt, chỉnh độ khó | Chơi hết thấy vừa sức |
| **5. Đẹp & hay** | Thay emoji bằng hình, hoạt ảnh mục 15, âm thanh mục 16, hướng dẫn | Trông như game thật |
| **6. Hoàn thiện** | Edge cases mục 21, PWA offline, README, CREDITS, đưa lên mạng | Có link gửi bạn gái |
| 7. (Tuỳ chọn) | Đóng gói APK bằng Capacitor | File `.apk` cài được |

---

## 24. NHỮNG ĐIỀU KHÔNG ĐƯỢC LÀM

- ❌ Không sao chép tên, nhân vật, hình, nhạc, màn chơi của game có sẵn trên CH Play / App Store.
- ❌ Không dùng hình/nhạc không rõ giấy phép (ví dụ lấy từ Google Hình ảnh).
- ❌ Không quảng cáo, không mua hàng trong game, không đăng nhập, không gửi dữ liệu đi đâu.
- ❌ Không làm game quá khó khiến người chơi bực (mục tiêu là vui và cảm động).
- ❌ Không viết cứng con số cân bằng hay thông tin cá nhân trong code logic.
- ❌ Không dùng thư viện/framework nặng không cần thiết (React, Vue...) cho game này.
- ❌ Không dùng chữ tiếng Anh trong giao diện (trừ tên file / code).

---

## 25. GAME THAM KHẢO & TÍNH NĂNG HỌC HỎI

> Mục này tổng hợp từ 5 game web cùng thể loại mà người dùng gửi. **Chỉ học cơ chế và ý tưởng**, không chép chữ, hình, âm thanh, tên nhân vật hay code của họ (xem mục 0 và 24).
> Mức ưu tiên: **[BẮT BUỘC]** = phải có, **[NÊN CÓ]** = làm nếu kịp, **[TUỲ CHỌN]** = để sau cùng.

### 25.1 Tình trạng các game tham khảo (kiểm tra ngày 20/11/2026)

| Game | Link | Tình trạng | Ghi chú chính |
|---|---|---|---|
| Tiệm Mì Cay | aenhatrang.com | Đang chạy | Phong phú nhất: cấp cay 0–7, luộc mì canh kim vào vùng xanh, nhân viên, thú cưng, khách quen có cốt truyện, đánh giá và trả lời đánh giá, sự kiện ngẫu nhiên, bảng xếp hạng online |
| Một Ổ Nha! (bánh mì) | hhuync.github.io/mot-o-nha | Đang chạy, mã nguồn công khai trên GitHub | JS thuần + DOM/CSS + ảnh PNG; yêu cầu riêng của khách ("không rau", "thêm ớt"); nhấn giữ để bóp sốt và rót trà; quầy nước riêng; đánh giá sao; nhiệm vụ hằng ngày; sự kiện theo mùa và giao diện (skin) |
| Tiệm Xôi Bà Tám | tiemxoibatam.io.vn | Web chỉ còn trang thông báo, game đã chuyển thành app trên App Store và Google Play | Trang web có tính năng **sao lưu tiến trình** bằng file hoặc mã để chuyển sang app |
| Spa | spa.tabbisfriends.asia | Không truy cập được (deployment bị tạm dừng) | – |
| Tiệm Trà Nhỏ (trà sữa) | trongnhi…workers.dev | Đã đóng cửa, chỉ còn ảnh thông báo | – |

### 25.2 Nhận xét chung về các game này

1. Đều là **web chạy trên điện thoại, màn hình dọc, PWA** (thêm vào màn hình chính, chơi như app).
2. Đều **chia theo "ngày bán hàng"**: chuẩn bị (nhập hàng) → mở cửa → khách đến → kết ca → tổng kết thu chi. Không chia theo màn có đồng hồ đếm ngược.
3. **Khách có cá tính**: xưng hô đúng vai vế (bà, chú, chị, em...), có lời thoại, có đánh giá sao sau khi ăn.
4. **Tiến triển dài hạn**: cấp độ tiệm và danh hiệu, mở khoá món, nâng cấp, trang trí, nhiệm vụ hằng ngày, quà điểm danh.
5. **Chữ tiếng Việt tự nhiên, có chất đời thường**, đây là phần tạo cảm xúc nhiều nhất.
6. Thao tác **không chỉ là chạm**: có nhấn giữ, canh thời điểm, vuốt chuyển quầy.

### 25.3 Thay đổi so với các mục trên

| Mục cũ | Thay đổi |
|---|---|
| 3. Công nghệ | Cho phép **JS thuần + DOM/CSS** (giống game bánh mì) thay cho Phaser. Cách này dễ làm giao diện chữ tiếng Việt đẹp, dễ sửa. AI chọn một trong hai và ghi lý do. |
| 6, 10. Màn chơi | Giữ 15 màn, nhưng gọi là **"Ngày 1" đến "Ngày 15"** và thêm bước **chuẩn bị đầu ngày** (25.4). Thay đồng hồ đếm ngược bằng **số khách trong ngày** (ví dụ ngày 1 có 8 khách, ngày 15 có 18 khách). Hết khách thì kết ca. **[NÊN CÓ]** Nếu thấy phức tạp, giữ đồng hồ như cũ. |
| 9. Sao | Thêm **đánh giá của từng khách** (25.7). Sao của ngày bằng trung bình sao của khách. |

### 25.4 Chuẩn bị đầu ngày và kho nguyên liệu [NÊN CÓ]

- Mỗi nguyên liệu có **tồn kho** (ví dụ 10 phần). Mỗi món làm xong trừ kho.
- Màn **"Chuẩn bị ngày N"** trước khi mở cửa:
  - Dự báo: thời tiết (☀️ Nắng đẹp, 🌧️ Mưa, 🥵 Nắng nóng, 🌬️ Gió mùa) và số khách dự kiến "8–10 khách".
  - Nhập thêm hàng: mỗi nguyên liệu một nút "+5 phần · 9k".
  - Mở khoá nguyên liệu mới bằng tiền.
  - Nút lớn "Mở cửa ngày N".
- Hết hàng giữa ca → trạm nguyên liệu hiện "Hết" màu xám. Khách gọi món có nguyên liệu đó sẽ đổi món hoặc buồn bỏ đi.
- Để không khó với người chơi tặng quà: **luôn có nút "Nhập nhanh"** giữa ca, giá gấp đôi.

### 25.5 Thao tác đa dạng [BẮT BUỘC: ít nhất 2 loại ngoài chạm]

| Thao tác | Dùng cho | Chi tiết |
|---|---|---|
| **Chạm** | Thêm nguyên liệu thường | Như mục 6 |
| **Nhấn giữ đến khi vòng tròn đầy** | Tán trứng trên bánh nướng, rót trà hoặc nước mía | Giữ 0,8 giây (rót đồ uống 2 giây). Vòng tròn tiến độ quanh ngón tay. Thả sớm thì không tính. Phát âm thanh rót hoặc bóp trong lúc giữ. |
| **Canh thời điểm (kim vào vùng xanh)** | Nướng bánh tráng trên vỉ than | Thanh ngang có kim chạy từ trái sang phải. Vùng **xanh** = chín vừa (thưởng +10% tiền), vùng **vàng** trước và sau = tạm được, vùng **đỏ** cuối = cháy. Chạm để lấy ra. Nâng cấp "Bếp to lửa" làm vùng xanh rộng hơn. Thay cho cơ chế "chín sau X giây" ở mục 7. |
| **Vuốt ngang** | Chuyển giữa quầy đồ ăn và quầy nước | Có nút mũi tên ở hai bên cho ai không quen vuốt. Có chấm chỉ quầy đang đứng. |

### 25.6 Yêu cầu riêng của khách [BẮT BUỘC]

- Bong bóng gọi món có thêm **dòng ghi chú** màu cam, ví dụ:
  - "không rau răm", "thêm trứng cút", "nhiều khô bò", "không xoài", "ít đá", "nướng giòn" (phải trúng vùng xanh)
  - **Độ cay 0–3** cho món có tương ớt: 🌶️ hiện bằng số quả ớt. Chọn độ cay bằng cách chạm chai tương nhiều lần (mỗi lần +1 cấp, hiện số trên khay).
- Từ ngày 3: 30% đơn có 1 yêu cầu riêng. Từ ngày 8: 50% đơn, tối đa 2 yêu cầu.
- Làm đúng yêu cầu: +5k tip và câu khen "Nhớ ý chị ghê!". Sai yêu cầu: tính là sai món.
- **Sổ công thức** 📖: nút ở góc màn chơi, mở ra danh sách món đã mở khoá kèm hình nguyên liệu đúng thứ tự. Mở sổ **không** dừng thời gian (trừ ngày 1–2).

### 25.7 Đánh giá của khách [BẮT BUỘC]

- Sau khi ăn, khách để lại **1–5 sao**, dựa trên kiên nhẫn còn lại lúc nhận món:
  - ≥ 60% → 5 sao, ≥ 35% → 4 sao, ≥ 15% → 3 sao, còn lại → 2 sao. Sai món → 1 sao.
  - Nâng cấp "Quạt máy" hạ mỗi ngưỡng 5%.
- Hiện sao nhỏ bay lên trên đầu khách khi rời đi.
- **Sổ đánh giá** (từ màn hình chính): danh sách đánh giá kèm 1 câu nhận xét lấy từ mẫu có biến, ví dụ "{món} ngon số một khu này, {xưng hô} sẽ quay lại!". AI tự viết ít nhất 40 câu gốc theo 3 nhóm: khen, góp ý nhẹ, chê vì chờ lâu.
- **[TUỲ CHỌN]** Trả lời đánh giá: chọn 1 trong 3 câu trả lời ("Cảm ơn ạ", "Xin lỗi, lần sau quán làm nhanh hơn", câu đùa). Trả lời tử tế cho đánh giá ≤ 3 sao thì khách sửa thành +1 sao.
- Điểm trung bình tiệm (ví dụ ⭐ 4,7) hiện ở thanh trên.

### 25.8 Xưng hô đúng vai vế [BẮT BUỘC]

Mỗi loại khách có bộ xưng hô riêng, dùng trong lời gọi món và đánh giá:

| Khách | Khách tự xưng | Gọi chủ tiệm | Mẫu câu gọi món |
|---|---|---|---|
| Học sinh | em | chị | "Chị ơi cho em {món} nha!" |
| Nhân viên văn phòng | anh / chị | em | "Em ơi cho anh {món}, anh tranh thủ!" |
| Cô bán rau | cô | con | "Con ơi cho cô {món} nghen!" |
| Anh shipper | anh | em | "Như mọi khi nha em, anh vội!" |
| Bà cụ | bà | cháu | "Cháu ơi, cho bà {món} nghen cháu!" |
| Bạn bè | tớ / mình | tên bạn gái | "{herName} ơi, cho mình {món}!" |
| "Anh" | anh | em / biệt danh | Câu riêng ở mục 19.5 |

### 25.9 Khách quen có cốt truyện [NÊN CÓ, rất hợp làm quà]

- Một số khách có tên riêng và **chuỗi chuyện 4–5 chương**. Mỗi lần ghé (cách nhau 1–3 ngày) mở 1 chương: một đoạn kể ngắn và **2 lựa chọn** cách đối xử. Lựa chọn nào cũng tốt, chỉ khác phần thưởng (tip, thêm khách ngày mai, quà trang trí).
- Hết chuỗi → khách thành **"Khách ruột"**: tip gấp đôi, có huy hiệu ❤️ trên đầu.
- **Chuyện của "Anh"** là chuỗi đặc biệt: mỗi chương là **một kỷ niệm thật** của hai người (lấy từ `memories` trong `personal.js`). Lựa chọn của người chơi quyết định câu trả lời "Anh" nói tiếp. Chương cuối nối vào EndingScene.
- AI viết 3 khách quen gốc với chuyện của riêng họ (ví dụ một bác xe ôm, một chị văn phòng, một bé học sinh). Không dùng lại tên hay cốt truyện của game tham khảo.

### 25.10 Sự kiện và thời tiết trong ngày [NÊN CÓ]

| Sự kiện | Tác dụng |
|---|---|
| 🌧️ Trời mưa | Khách ít hơn 15%, hay gọi đồ nóng, nền có mưa |
| 🥵 Nắng nóng | Khách gọi nước nhiều gấp đôi |
| 🎒 Học sinh tan trường | Giữa ca một nhóm 3 học sinh đến cùng lúc |
| 💰 Ngày lãnh lương | Tip gấp đôi |
| 🏮 Lễ hội phố | Khách đông hơn 30% |
| ⭐ Người review ghé | Một khách đặc biệt, đánh giá tính gấp 3 |

- Mỗi ngày có tối đa 1 sự kiện, báo trước ở màn Chuẩn bị.
- **Sự cố nhỏ** [TUỲ CHỌN], tối đa 1 lần mỗi ngày: nước đổ trước quầy (chạm 3 lần để lau, trong lúc đó bếp chậm lại), mèo hoang ghé (chạm cho ăn thì +1 tim).

### 25.11 Thú cưng của tiệm [NÊN CÓ]

- 1 con thú nằm trước quầy (mặc định là mèo; mua thêm cún và hamster ở mục Trang trí).
- Chạm vào thú → hoạt ảnh nhỏ và 1 câu ngẫu nhiên ("Mèo dụi đầu vào tay em", "Mèo ngáp một cái thật dài"). Mỗi con có ít nhất 5 câu.
- **[ĐIỀN: tên thú cưng thật của hai người nếu có]**: dùng tên đó làm tên mèo.

### 25.12 Tiến triển dài hạn [NÊN CÓ]

- **Cấp tiệm và danh hiệu**: mỗi món bán được +XP. Các mốc danh hiệu do AI đặt, ví dụ "Gánh hàng nhỏ" → "Tiệm đầu ngõ" → "Tiệm quen khu phố" → "Tiệm nổi tiếng" → "Tiệm của {herName}, nhất quả đất".
- **Nhiệm vụ hằng ngày**: 3 nhiệm vụ mỗi ngày (thật, theo giờ Việt Nam), ví dụ "Bán 10 bịch bánh tráng trộn", "Phục vụ 5 khách 5 sao liên tiếp". Mỗi nhiệm vụ thưởng 20–40k.
- **Quà điểm danh 7 ngày**: mỗi ngày mở game nhận quà, ngày 7 nhận quà lớn và **1 lời nhắn ngắn từ "Anh"** `[ĐIỀN: 7 câu nhắn]`.
- **Sổ thu chi** cuối ngày: doanh thu, tiền nhập hàng, tip, lãi. Chỉ để xem, không có phí điện nước phạt người chơi.
- **Chơi lại ngày**: lưu một điểm khôi phục đầu mỗi ngày. Trong menu tạm dừng có nút "Làm lại ngày này".

### 25.13 Giao diện theo mùa (skin) [TUỲ CHỌN]

- Bộ giao diện đổi nền, quầy và bảng thực đơn: Mặc định, **Trung Thu** (đèn lồng), **Tết** (hoa mai, câu đối), **Valentine** (trái tim hồng), **Noel**.
- Tự gợi ý skin phù hợp khi đến đúng dịp; mua bằng tiền trong game.

### 25.14 Kỹ thuật học được [BẮT BUỘC]

1. **Âm thanh trên iPhone**: dùng **Web Audio API** (AudioContext + AudioBuffer giải mã sẵn) cho tiếng hiệu ứng để không bị trễ. Khi quay lại app từ nền: gọi `resume()`, nếu context đã `closed` thì tạo lại. Tiếng bấm liên tục dùng một nhóm (pool) 3–4 nguồn âm.
2. **Màn tải**: tải trước toàn bộ hình và âm thanh, có thanh %, mỗi tài nguyên chờ tối đa 8 giây, toàn bộ tối đa 20 giây. Quá thời gian thì vẫn vào game, tài nguyên lỗi thì dùng emoji thay thế.
3. **Chặn thao tác trình duyệt**: `-webkit-tap-highlight-color: transparent`, `-webkit-touch-callout: none` (không hiện menu lưu ảnh khi giữ), `-webkit-user-drag: none` cho ảnh, `overscroll-behavior: none`, `touch-action: manipulation`.
4. **Vùng tai thỏ**: `viewport-fit=cover` và `padding: env(safe-area-inset-top)` / `env(safe-area-inset-bottom)`.
5. **Khung game trên máy tính**: cột giữa rộng tối đa 460px, hai bên tô nền và đổ bóng.
6. **Khoá lưu có phiên bản** (ví dụ `tiemcuaem_save_v1`). Đổi cấu trúc save thì tăng số và viết hàm chuyển đổi save cũ.
7. **Sao lưu và khôi phục**: trong Cài đặt có "Sao chép mã sao lưu" (save JSON → nén → base64, bắt đầu bằng `TIEM1-`) và "Dán mã để khôi phục". Có cảnh báo: "Đừng gửi mã qua Messenger hoặc Zalo vì tin nhắn dài có thể bị cắt."
8. **Service worker** phải đổi tên bộ nhớ đệm mỗi lần cập nhật (ví dụ `tiem-v3`). Có màn "Có gì mới" hiện một lần sau mỗi bản cập nhật.
9. **Mở trong Messenger, Zalo, Facebook**: trình duyệt bên trong các app này hay chặn lưu và âm thanh. Phát hiện bằng userAgent rồi hiện gợi ý "Mở bằng Safari hoặc Chrome để chơi mượt hơn".
10. **Không dùng bảng xếp hạng online, đăng nhập hay Google Analytics**: game tặng riêng, không cần server.

### 25.15 Hướng dẫn chơi dạng thẻ [BẮT BUỘC]

- Ngoài hướng dẫn tương tác ở màn 1 (mục 13.4), có **bộ 6–8 thẻ hướng dẫn** xem lại được từ Cài đặt → "Cách chơi". Mỗi thẻ có ảnh minh hoạ, tiêu đề, 2 dòng giải thích, nút "← Trước" và "Tiếp →", số thẻ "3 / 7".
- Lần đầu chơi phải xem hết mới vào được. Từ lần sau có nút ✕ để bỏ qua.

---

## PHỤ LỤC A — CÂU HỎI NGƯỜI DÙNG CẦN TRẢ LỜI TRƯỚC KHI BẮT ĐẦU

1. Tên / biệt danh bạn gái? Tên / biệt danh của bạn?
2. Ngày quen nhau (để đếm số ngày)?
3. ✅ Đã chốt: **bánh tráng**. Cô ấy thích loại bánh tráng nào nhất (trộn, nướng, cuốn bơ...)? Có quán bánh tráng nào hai người hay ăn không (đặt tên tiệm theo đó)?
4. Món cô ấy thích nhất?
5. 6 tên bạn bè chung?
6. 15 kỷ niệm: tiêu đề + ngày + vài dòng + ảnh (có thể gửi sau, game vẫn chạy với ảnh thay thế).
7. Lời nhắn cuối game (EndingScene) và lời nhắn ẩn khi đạt 3 sao mọi màn?
8. Câu nói riêng của hai người cho khách "Anh"?
9. Chơi qua **link web** hay cần **file APK**?
10. Có ngày cụ thể cần tặng không (sinh nhật, kỷ niệm) để ưu tiên tiến độ?
11. Chia theo **màn có đồng hồ** (mục 10) hay theo **ngày bán hàng có nhập hàng** như các game tham khảo (mục 25.3–25.4)?
12. Hai người có thú cưng thật không? Tên là gì (mục 25.11)?
13. 7 câu nhắn ngắn cho quà điểm danh 7 ngày (mục 25.12)?

## PHỤ LỤC C — QUY TRÌNH: GEMINI CHỐT NỘI DUNG → CLAUDE LÀM GAME

**Bước 1 (Gemini):** Gemini **không viết code**. Gemini chỉ phỏng vấn người dùng, điền mọi chỗ `[ĐIỀN: ...]`, giải quyết các chỗ còn để chọn (ví dụ câu 11 Phụ lục A), rồi xuất ra **bản đặc tả cuối cùng**.

**Bước 2 (Claude):** Người dùng đưa bản cuối cho Claude (khuyên dùng Claude Code để Claude tự tạo file, chạy thử, đưa lên GitHub Pages). Claude làm theo Phụ lục B và mục 23.

**Yêu cầu cho bản cuối mà Gemini xuất ra:**
1. Một file Markdown duy nhất, tên `game-spec-FINAL.md`, giữ **nguyên cấu trúc mục 0–25** của tài liệu này.
2. **Không còn** chỗ `[ĐIỀN: ...]` nào. Chỗ nào người dùng chưa muốn trả lời thì ghi rõ `MẶC ĐỊNH: <giá trị>`.
3. Ghi **đầy đủ** nội dung `personal.js` (tên, ngày, 15 kỷ niệm, lời nhắn, bạn bè, câu nói của "Anh", 7 câu điểm danh) trong một khối code ở mục 2.
4. Mỗi chỗ đã chọn giữa 2 phương án, ghi `ĐÃ CHỐT: ...` và **xoá phương án không dùng** để Claude không phải đoán.
5. Không tự thêm tính năng mới ngoài tài liệu. Muốn thêm thì liệt kê ở cuối, trong mục "Ý tưởng để sau".
6. Không bịa con số mới. Nếu đổi số nào thì ghi `ĐÃ ĐỔI: cũ → mới, lý do`.
7. Cuối file có mục **"Danh sách ảnh cần chuẩn bị"**: tên file `assets/memories/01.jpg` … `15.jpg`, mỗi ảnh ứng với kỷ niệm nào.

**Câu lệnh dán cho Gemini:**

```
Đính kèm là tài liệu đặc tả game tặng bạn gái. Bạn KHÔNG viết code.
Nhiệm vụ của bạn:
1. Đọc hết tài liệu, nhất là Phụ lục A và Phụ lục C.
2. Hỏi tôi từng nhóm câu (mỗi lần tối đa 5 câu) để điền mọi chỗ [ĐIỀN: ...] và chốt các lựa chọn còn mở.
   Gợi ý sẵn 2–3 phương án cho mỗi câu để tôi chọn nhanh.
3. Khi đủ thông tin, xuất ra game-spec-FINAL.md đúng theo "Yêu cầu cho bản cuối" ở Phụ lục C.
```

---

## PHỤ LỤC B — CÂU LỆNH MẪU ĐỂ DÁN CHO AI

```
Đây là tài liệu đặc tả game "Tiệm của Em" (file đính kèm). Hãy đọc hết toàn bộ.
Sau đó:
1. Liệt kê ngắn gọn những gì bạn hiểu, và hỏi tôi các câu trong Phụ lục A mà tôi chưa điền.
2. Khi tôi trả lời xong, làm GIAI ĐOẠN 1 (mục 23): đưa toàn bộ code theo đúng cấu trúc thư mục mục 4,
   kèm hướng dẫn chạy thử trên máy tính từng bước cho người không biết lập trình.
3. Dừng lại chờ tôi xác nhận trước khi làm giai đoạn tiếp theo.
Tuân thủ tuyệt đối mục 0 và mục 24.
```
