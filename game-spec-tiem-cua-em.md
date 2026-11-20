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
| Bối cảnh | Một tiệm ăn sáng nhỏ ở góc phố Việt Nam: mái hiên, bàn nhựa, đèn vàng, có cây hoa giấy |
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
  favoriteDish: "xoi_ga",       // [ĐIỀN: id món cô ấy thích nhất, xem mục 7] — món này cho x2 tiền
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
4. Nguyên liệu phải thêm **đúng thứ tự công thức**. Sai thứ tự hoặc sai nguyên liệu → món thành "món hỏng" (hiện khói xám nhẹ), chỉ có thể bỏ vào thùng rác.
5. Nguyên liệu **cần nấu** (ví dụ trứng chiên, chả) phải đặt lên **bếp** trước: chạm trạm → món lên bếp → chờ thanh nấu đầy (xem thời gian ở mục 7) → chạm vào để lấy. Nếu để quá 5 giây sau khi chín → **cháy** (màu đen, có khói) → chỉ bỏ đi được.
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

## 7. THỰC ĐƠN, NGUYÊN LIỆU, CÔNG THỨC

> Chủ đề mặc định: **tiệm ăn sáng Việt Nam** (xôi + bánh mì + nước). Người dùng có thể đổi trong `config.js`.
> `[ĐIỀN: nếu muốn món khác, ví dụ trà sữa/bánh tráng trộn, ghi ở đây]`

### 7.1 Nguyên liệu (trạm)

| id | Tên hiển thị | Emoji tạm (nếu chưa có hình) | Cần nấu? | Thời gian nấu | Mở ở màn |
|---|---|---|---|---|---|
| `xoi` | Xôi trắng | 🍚 | Không | – | 1 |
| `hanh_phi` | Hành phi | 🧅 | Không | – | 1 |
| `ga_xe` | Gà xé | 🍗 | Không | – | 1 |
| `ruoc` | Ruốc | 🟫 | Không | – | 3 |
| `trung` | Trứng | 🥚 | **Có** | 3 giây | 4 |
| `cha` | Chả | 🥓 | **Có** | 4 giây | 7 |
| `xoi_gac` | Xôi gấc | 🔴 | Không | – | 9 |
| `banh_mi` | Ổ bánh mì | 🥖 | Không | – | 5 |
| `pate` | Pa-tê | 🟤 | Không | – | 5 |
| `dua_leo` | Dưa leo | 🥒 | Không | – | 5 |
| `tra_da` | Trà đá | 🧊 | Không | – | 2 |
| `sua_dau` | Sữa đậu nành | 🥛 | Không | – | 8 |
| `ca_phe` | Cà phê sữa | ☕ | **Có** (pha) | 5 giây | 11 |

- Trạm "cần nấu" chiếm 1 ô bếp. Số ô bếp mặc định: **2** (nâng cấp lên 3, 4).
- Ô bếp có thanh tiến độ tròn quanh nguyên liệu: đang nấu = cam `#FF9F43`, chín = xanh `#5BD67A` + lấp lánh, sắp cháy (còn 2 giây) = đỏ nhấp nháy.

### 7.2 Công thức món (thứ tự bắt buộc từ trái sang phải)

| id | Tên món | Công thức | Giá gốc | Mở ở màn |
|---|---|---|---|---|
| `xoi_trang` | Xôi trắng hành phi | xoi → hanh_phi | 10 | 1 |
| `xoi_ga` | Xôi gà | xoi → ga_xe → hanh_phi | 18 | 1 |
| `tra_da_ly` | Ly trà đá | tra_da | 3 | 2 |
| `xoi_ruoc` | Xôi ruốc | xoi → ruoc → hanh_phi | 15 | 3 |
| `xoi_trung` | Xôi trứng | xoi → trung(chín) → hanh_phi | 20 | 4 |
| `banh_mi_pate` | Bánh mì pa-tê | banh_mi → pate → dua_leo | 15 | 5 |
| `banh_mi_trung` | Bánh mì trứng | banh_mi → trung(chín) → dua_leo | 18 | 6 |
| `xoi_cha` | Xôi chả | xoi → cha(chín) → hanh_phi | 22 | 7 |
| `sua_dau_ly` | Ly sữa đậu | sua_dau | 8 | 8 |
| `xoi_gac_ga` | Xôi gấc gà | xoi_gac → ga_xe → hanh_phi | 25 | 9 |
| `banh_mi_full` | Bánh mì đặc biệt | banh_mi → pate → cha(chín) → trung(chín) → dua_leo | 35 | 10 |
| `ca_phe_ly` | Cà phê sữa đá | ca_phe(chín) → tra_da | 15 | 11 |
| `xoi_thap_cam` | Xôi thập cẩm | xoi → ga_xe → ruoc → cha(chín) → trung(chín) → hanh_phi | 45 | 12 |
| `combo_tinh_yeu` | **Combo Tình Yêu** 💕 | xoi_gac → ga_xe → trung(chín) → hanh_phi, kèm 1 ly sua_dau (2 khay) | 60 | 14 |

- **Món đồ uống** làm trên khay riêng như món khác.
- **Một khách có thể gọi 2 món** (từ màn 8): bong bóng hiện 2 hình; phải giao đủ cả 2 (giao từng món một, món đã giao hiện dấu ✓).
- Món `favoriteDish` trong `personal.js`: **giá x2** và có viền hồng lấp lánh trong bong bóng.

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
| Mèo con | Mèo cam | 20 giây | 0, nhưng **+1 tim** | Chỉ gọi xoi_trang; rất hiếm (5%) | 7 |

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
| 1 | 60 | 60k | 6–8 | 1.3 | xôi trắng, xôi gà | **Có hướng dẫn từng bước** |
| 2 | 70 | 90k | 5–7 | 1.25 | trà đá | Gợi ý: "Đồ uống cũng làm trên khay nha" |
| 3 | 75 | 120k | 5–7 | 1.2 | xôi ruốc | Khách "Anh" xuất hiện lần đầu |
| 4 | 80 | 150k | 4.5–6.5 | 1.2 | trứng (bếp) | **Hướng dẫn bếp** |
| 5 | 80 | 180k | 4.5–6 | 1.15 | bánh mì pa-tê | |
| 6 | 90 | 220k | 4–6 | 1.15 | bánh mì trứng | Mở chiêu đặc biệt 💖 |
| 7 | 90 | 260k | 4–5.5 | 1.1 | chả (bếp) | |
| 8 | 90 | 300k | 4–5.5 | 1.1 | sữa đậu | Khách gọi 2 món |
| 9 | 100 | 350k | 3.5–5 | 1.05 | xôi gấc | |
| 10 | 100 | 400k | 3.5–5 | 1.05 | bánh mì đặc biệt | Màn "Ngày mưa" (hiệu ứng mưa, nhạc nhẹ) |
| 11 | 100 | 450k | 3.5–5 | 1.0 | cà phê | |
| 12 | 110 | 520k | 3–4.5 | 1.0 | xôi thập cẩm | |
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
| `bep` | Thêm bếp | 2 → 3 → 4 | 200k, 450k | Thêm ô bếp |
| `bep_nhanh` | Bếp to lửa | 0 → 3 | 150k, 300k, 500k | Giảm thời gian nấu 10% / 20% / 30% |
| `ghe` | Thêm chỗ khách | 3 → 4 | 400k | 4 vị trí khách (khách nhiều hơn, tiền nhiều hơn) |
| `quat` | Quạt máy | 0 → 2 | 200k, 400k | Kiên nhẫn khách +10% / +20% |
| `nhac` | Loa nhạc | 0 → 1 | 250k | Tip +20% |
| `chong_chay` | Chảo chống dính | 0 → 1 | 300k | Thời gian trước khi cháy tăng từ 5 lên 10 giây |
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
- Nền `#FFF6EC`. Giữa: biểu tượng chén xôi bốc khói (vẽ bằng code) nhún lên xuống.
- Thanh tải 400×24, bo góc 12, nền `#FFE0C2`, phần đầy `#FF8FAB`. Dưới: "Đang nhóm bếp... 42%".

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
  2. "Chạm vào **Xôi trắng** trước."
  3. "Rồi chạm **Gà xé**."
  4. "Cuối cùng là **Hành phi**. Thứ tự quan trọng lắm đó!"
  5. "Giờ chạm vào khay rồi chạm vào khách để giao món."
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
- Thiếu hình món Việt (xôi, bánh mì...) → **vẽ bằng code** (Canvas/SVG) theo phong cách sticker ở 14.1, hoặc dùng emoji phóng to đặt trên đĩa tròn trắng.
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
| Đặt lên bếp | Rơi xuống + khói nhỏ bốc lên liên tục khi đang nấu | – |
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
| `sfx_sizzle.mp3` | Đang chiên | Lặp khi có món trên bếp |
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
"Anh đói, nhưng nhớ em hơn 💕", "Món nào em làm cũng ngon nhất!", "Cho anh một phần xôi và một phần trái tim em nhé", "Bà chủ đáng yêu quá!", "Anh ghé chỉ để nhìn em thôi 😳"

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

## PHỤ LỤC A — CÂU HỎI NGƯỜI DÙNG CẦN TRẢ LỜI TRƯỚC KHI BẮT ĐẦU

1. Tên / biệt danh bạn gái? Tên / biệt danh của bạn?
2. Ngày quen nhau (để đếm số ngày)?
3. Món chủ đề giữ **xôi + bánh mì** hay đổi sang món khác (trà sữa, bánh tráng trộn, phở...)?
4. Món cô ấy thích nhất?
5. 6 tên bạn bè chung?
6. 15 kỷ niệm: tiêu đề + ngày + vài dòng + ảnh (có thể gửi sau, game vẫn chạy với ảnh thay thế).
7. Lời nhắn cuối game (EndingScene) và lời nhắn ẩn khi đạt 3 sao mọi màn?
8. Câu nói riêng của hai người cho khách "Anh"?
9. Chơi qua **link web** hay cần **file APK**?
10. Có ngày cụ thể cần tặng không (sinh nhật, kỷ niệm) để ưu tiên tiến độ?

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
