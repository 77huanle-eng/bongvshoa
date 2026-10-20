# Immersive 3D Flower Garden · 20/10

Website tặng hoa 20/10 dựng bằng **Vite + JavaScript ES Modules + Three.js**. Hoa được dựng từ custom `BufferGeometry` cong, có lớp cánh, đài hoa, thân và lá có gân. Thảm hoa xa, thân hoa, lá, cụm lá nền và cánh hoa rơi sử dụng `InstancedMesh`; cảnh có ánh nắng vàng giờ bình minh, sương, bụi sáng màu champagne và bloom hậu kỳ tiết chế. Bản **Rose Shape Fix / Golden-Hour Reference** lấy cảm hứng từ video tham khảo: camera thấp giữa các bông hồng, ánh nắng ngược phía trái, các lớp núi xa phủ sương, hoa có thân/lá, thêm lớp cánh cho hoa nền và giảm các điểm sáng kiểu đêm.

> Đây là project procedural tự tạo hình học, không sử dụng emoji làm mô hình hoa. Đây cũng không phải asset scan/photogrammetry thực vật; phong cách hoa là cách điệu nghệ thuật.

## 1. Yêu cầu

- Node.js **20.19+ hoặc 22.12+** (đề xuất Node.js 22 LTS trở lên).
- npm đi kèm Node.js.
- Trình duyệt hiện đại có WebGL 2, ví dụ Chrome/Edge/Firefox/Safari bản tương đối mới.

## 2. Cài và chạy trên máy tính Windows

1. Cài Node.js từ <https://nodejs.org/>. Mở cửa sổ Terminal/CMD mới.
2. Giải nén thư mục `flower-garden-3d`.
3. Mở CMD trong thư mục dự án, nơi có `package.json`.
4. Chạy:

```bash
npm install
npm run dev
```

5. Mở URL hiện ra trong terminal (thường là `http://localhost:5173/`). Không mở trực tiếp `index.html` bằng cách double-click vì Vite cần cung cấp ES modules qua HTTP.

### Xem trên điện thoại cùng Wi-Fi

- Cho máy tính và điện thoại dùng cùng mạng Wi-Fi.
- Để Vite tiếp tục chạy với lệnh `npm run dev`.
- Tìm địa chỉ IPv4 Wi-Fi của máy tính bằng `ipconfig` trên Windows.
- Trên điện thoại mở `http://IP-MAY-TINH:5173/`.
- Cho phép Node.js/Vite qua Windows Firewall trong mạng Private nếu Windows hỏi. Chỉ mở cổng khi cần thử nghiệm trong mạng tin cậy; không dùng dev server làm máy chủ production.

Ví dụ minh họa: `http://192.168.1.25:5173/` — thay IP này bằng IP thật trên máy bạn.

## 3. Kiểm tra source, build production và xem thử

Chạy kiểm tra cú pháp JS, các import nội bộ và ID giao diện:

```bash
npm run check
```

Lệnh này không cần tải dependency; nó là kiểm tra tĩnh, không thay thế build/bài test trên trình duyệt.


```bash
npm run build
npm run preview
```

Vite tạo website tĩnh trong thư mục `dist/`. Lệnh `preview` dùng để kiểm tra bản build cục bộ; không phải máy chủ production.

## 4. Chỉnh tên người nhận và lời chúc

Chỉnh `src/config.js`:

```js
export const GIFT_CONFIG = {
  recipient: 'em',
  sender: 'anh',
  occasion: '20 tháng 10',
  titleLine1: 'Thế giới có muôn vàn loài hoa,',
  titleLine2: 'nhưng anh chỉ muốn ngắm em.',
  subtitle: 'Lời chúc của bạn...',
  letterGreeting: 'Gửi cô gái anh thương,',
  letterParagraphs: ['Đoạn 1...', 'Đoạn 2...', 'Đoạn 3...'],
  signoff: 'Thương em thật nhiều',
};
```

Các đoạn thiệp được dựng bằng `textContent`, do đó ký tự do bạn nhập sẽ được hiển thị như văn bản. `recipient` được dùng ở tiêu đề trang và dòng chào trên thiệp; nếu thay `em` bằng tên riêng, thiệp sẽ chuyển sang lời chào theo tên đó. `letterGreeting` là cách xưng hô ở dòng thứ hai của thiệp. Trường `sender` là cấu hình sẵn để bạn có thể mở rộng chữ ký về sau.

## 5. Nhạc nền

Nút nốt nhạc bật/tắt một lớp ambience nhẹ tạo trực tiếp bằng Web Audio API. Project không tải nhạc có bản quyền từ bên ngoài và không yêu cầu file audio. Trên iOS, âm thanh chỉ bắt đầu sau lần chạm nút do chính sách autoplay của Safari.

Nếu muốn thay bằng bài nhạc riêng, hãy đặt file bạn có quyền sử dụng vào `public/audio/`, rồi thay phần Web Audio trong `src/main.js` bằng `HTMLAudioElement` và giữ điều khiển bật/tắt.

## 6. Triển khai Netlify

1. Tạo repository trên GitHub và đưa toàn bộ mã nguồn lên.
2. Đăng nhập Netlify, chọn **Add new site → Import an existing project**.
3. Chọn repository.
4. Build command: `npm run build`.
5. Publish directory: `dist`.
6. Deploy. File `vite.config.js` đặt `base: './'` để các asset build có đường dẫn tương đối.

## 7. Triển khai GitHub Pages

Workflow mẫu có sẵn tại `.github/workflows/deploy.yml`.

1. Push project lên repository GitHub với nhánh `main`.
2. Mở **Settings → Pages**, đặt **Source = GitHub Actions**.
3. Mở tab **Actions** và kiểm tra workflow `Deploy Flower Garden`.
4. Khi workflow thành công, website có đường dẫn dạng `https://TEN-TAI-KHOAN.github.io/TEN-REPOSITORY/`.

Nếu workflow mặc định của tổ chức chặn quyền Pages, mở `Settings → Actions → General` để xác nhận workflow được phép dùng `GITHUB_TOKEN` có quyền ghi Pages. Không cần đưa khóa API hay bí mật nào vào project này.

## 8. Cấu trúc mã nguồn

```text
flower-garden-3d/
├── index.html
├── package.json
├── vite.config.js
├── public/audio/.gitkeep
├── .github/workflows/deploy.yml
└── src/
    ├── main.js
    ├── config.js
    ├── scene/        # scene, camera, lights, mountains and horizon
    ├── flowers/      # parametric petals, rose clusters, instanced meadow
    ├── animation/    # scheduler, wind, falling petals
    ├── effects/      # golden-hour sun, atmosphere and bloom
    ├── ui/           # intro and letter modal
    └── styles/       # responsive typography and interaction UI
```

## 9. Tương tác

- **Mở món quà:** bắt đầu chu kỳ nở hoa nhiều đợt, chuyển động camera và hiệu ứng ánh sáng. Từng vòng cánh đi từ tư thế nụ khép sang mở theo độ trễ riêng.
- **Cho hoa nở lại:** bắt đầu lại chu kỳ trong trang hiện tại, không reload.
- **Đọc lời thiệp:** mở thiệp reveal/flip; đóng bằng nút X, chạm vùng nền hoặc phím `Escape`; hỗ trợ Tab focus.
- **Nhạc nền:** bật/tắt ambience tạo bằng Web Audio.
- **Chuột / chạm kéo:** dịch chuyển góc nhìn trong giới hạn để tạo parallax.

## 10. Hiệu năng và giới hạn đã biết

- Capped device pixel ratio (tối đa 1.45 trên mobile và 2.0 desktop; có chế độ `?quality=4k` riêng và tự hạ thêm nếu desktop phát hiện FPS thấp kéo dài).
- Cắt animation khi tab bị ẩn và giới hạn delta time sau khi quay lại.
- Thảm hoa nền và mưa cánh dùng `InstancedMesh`; tránh tạo geometry/material mới trong vòng lặp frame.
- `prefers-reduced-motion` giảm tốc độ chuyển động và thời gian reveal; thiết bị không hỗ trợ WebGL vẫn có thể mở lời chúc và thiệp.
- Bloom dùng `UnrealBloomPass`, giảm cường độ trên mobile; nếu post-processing lỗi, renderer tự chuyển sang render trực tiếp.
- Có xử lý `webglcontextlost` / `webglcontextrestored`.
- Nếu nhiều trình duyệt di động cũ hoặc GPU yếu, nên thử nghiệm thêm trên thiết bị thật; chất lượng hình ảnh và FPS còn phụ thuộc driver/GPU, nhiệt độ, độ phân giải và các tab khác.
- Google Fonts là tài nguyên tùy chọn tải từ mạng; khi offline trình duyệt tự dùng font dự phòng.
- Chưa có kiểm thử thực địa trên mọi dòng iPhone/Android và không thể cam kết FPS cụ thể cho tất cả phần cứng.

## 11. Kiểm thử

Dùng danh sách sau trước khi gửi link cho người nhận:

- [ ] `npm install` kết thúc không có lỗi.
- [ ] `npm run build` tạo thư mục `dist/` thành công (chưa xác minh trong môi trường tạo source do registry npm timeout).
- [ ] Mở `npm run dev`, kiểm tra Console và Network.
- [ ] Nhấn “Mở món quà”, chờ các tầng hoa nở và kiểm tra nút “Cho hoa nở lại”.
- [ ] Mở/đóng thiệp bằng nút X, vùng nền và `Escape`.
- [ ] Bật/tắt nhạc sau một thao tác chạm của người dùng.
- [ ] Thử kéo góc nhìn bằng chuột, touch trên điện thoại, xoay màn hình và reload.
- [ ] Chạy thử khi `prefers-reduced-motion` được bật.
- [ ] Build production và kiểm tra URL triển khai, nhất là đường dẫn con của GitHub Pages.

## Cập nhật hình dáng hoa hồng

Bản Rose Shape Fix nghiêng bông hồng về phía camera để tránh hình dạng đĩa phẳng, giảm kích thước cánh ngoài, làm rõ tâm hoa và thu nhỏ các bông nền. Xem `VISUAL-UPDATE.md` để biết thay đổi và `TEST-REPORT.md` để biết giới hạn kiểm thử.

## Chạy chất lượng render 4K

Sau khi `npm run dev`, thêm `?quality=4k` vào địa chỉ Vite, ví dụ:

```text
http://localhost:5173/?quality=4k
```

Trên máy tính, chế độ này tăng độ phân giải drawing buffer của canvas lên mức tối đa 3840×2160 (hoặc giới hạn tương đương theo tỷ lệ màn hình), tăng chi tiết của animation và hoa trong canvas. Đây là chế độ render WebGL độ phân giải cao, không tự xuất file video. Nếu GPU giảm FPS trong thời gian dài, dự án tự giảm chất lượng render để ưu tiên chuyển động mượt. Điện thoại không bật chế độ 4K để tránh nóng máy và hao pin.
"# bongvshoa" 
