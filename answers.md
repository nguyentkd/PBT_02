# PBT_02 - Answers

## A1 - Input Types

1. `type="email"` -> Ô nhập text có kiểm tra định dạng email cơ bản, tự báo lỗi nếu không có ký tự `@` và domain hợp lệ. Use case: ô email đăng ký / đăng nhập.
2. `type="password"` -> Ô nhập text bị che ký tự bằng dấu chấm/asterisk, có thể kết hợp `minlength` và `pattern`. Use case: mật khẩu tài khoản.
3. `type="number"` -> Ô số có nút tăng/giảm trên nhiều trình duyệt, tự chặn giá trị không phải số. Use case: số lượng sản phẩm.
4. `type="tel"` -> Ô text tối ưu cho số điện thoại, trên mobile thường mở bàn phím số. Không tự validate chuẩn số điện thoại, thường kết hợp `pattern`. Use case: số điện thoại giao hàng.
5. `type="date"` -> Bộ chọn ngày. Tự validate định dạng ngày, hỗ trợ `min`/`max`. Use case: ngày sinh hoặc ngày giao hàng mong muốn.
6. `type="range"` -> Thanh trượt chọn giá trị trong một khoảng. Tự validate theo `min`, `max`, `step`. Use case: chọn số ngày giao hàng hoặc mức ngân sách.
7. `type="checkbox"` -> Ô chọn bật/tắt. Có thể dùng `required` nếu bắt buộc tick. Use case: đồng ý điều khoản.
8. `type="radio"` -> Nhóm lựa chọn một trong nhiều phương án, chỉ chọn một giá trị trong cùng `name`. Use case: giới tính hoặc phương thức thanh toán.
9. `type="url"` -> Ô text kiểm tra định dạng URL. Use case: nhập link website, fanpage, hoặc trang sản phẩm.
10. `type="file"` -> Ô chọn file từ máy người dùng, có thể giới hạn loại file bằng `accept`. Use case: tải ảnh avatar hoặc chứng từ.

## A2 - Validation Attributes

1. Trường hợp 1: Bấm Submit sẽ không được gửi vì `required` và giá trị đang rỗng. Trình duyệt báo lỗi bắt buộc nhập.
2. Trường hợp 2: Không submit được vì `type="email"` yêu cầu định dạng email hợp lệ, còn `abc` không có cấu trúc email.
3. Trường hợp 3: Không submit được vì `number` phải nằm trong khoảng từ 1 đến 10, nhưng giá trị 15 vượt `max`.
4. Trường hợp 4: Không submit được vì `pattern="[0-9]{10}"` yêu cầu đúng 10 chữ số, còn `abc123` chứa chữ cái và không khớp toàn bộ mẫu.
5. Trường hợp 5: Không submit được vì `minlength="8"` yêu cầu tối thiểu 8 ký tự, còn `123` chỉ có 3 ký tự.

## A3 - Accessibility

1. `<label for="email">` quan trọng vì nó gắn nhãn rõ ràng cho input. Screen reader đọc đúng tên trường, và người dùng cũng có thể click vào label để focus vào ô nhập.
2. Dùng `<fieldset>` + `<legend>` khi có một nhóm input liên quan về mặt ngữ nghĩa, đặc biệt là radio buttons hoặc checkbox groups. Ví dụ: nhóm phương thức thanh toán, nhóm giới tính, nhóm địa chỉ giao hàng.
3. `aria-label` dùng khi control không có text visible đủ nghĩa, ví dụ nút icon chỉ có biểu tượng kính lúp. Không nên dùng `aria-label` khi đã có `<label>` vì dễ tạo hai nguồn mô tả khác nhau, làm code khó bảo trì và có thể khiến screen reader đọc không nhất quán.

## A4 - Media

1. `loading="lazy"` trì hoãn tải ảnh cho đến khi ảnh gần vào vùng nhìn thấy. Nó giảm băng thông, tăng tốc tải trang ban đầu, đặc biệt hữu ích với trang có nhiều ảnh. Không nên dùng cho ảnh quan trọng ở phần đầu trang hoặc ảnh hero vì chúng cần hiển thị ngay.
2. Nên cung cấp nhiều `<source>` trong `<video>` để tăng khả năng tương thích giữa trình duyệt và thiết bị. Ba format phổ biến là `mp4`, `webm`, và `ogg`.
3. `alt` dùng để mô tả nội dung ảnh cho người dùng không nhìn thấy ảnh, cho screen reader, và để thay thế khi ảnh không tải được.
   - Ảnh sản phẩm iPhone 16: `alt="iPhone 16 màu Titan tự nhiên, góc nhìn chính diện"`
   - Ảnh trang trí: `alt=""` nếu chỉ mang tính decor và không cung cấp thông tin
   - Ảnh biểu đồ doanh thu Q1/2026: `alt="Biểu đồ cột thể hiện doanh thu quý 1 năm 2026 tăng đều qua ba tháng"`

## A5 - So sánh `<figure>` vs `<img>`

Cách 1 dùng khi ảnh chỉ là một nội dung độc lập, không cần chú thích. Ví dụ: ảnh avatar người dùng, banner sản phẩm không kèm mô tả giá.

Cách 2 dùng khi ảnh cần chú thích hoặc là một khối nội dung có ngữ nghĩa riêng. Ví dụ: ảnh sản phẩm kèm giá, ảnh biểu đồ kèm nhận xét, ảnh infographic kèm caption.

## C1 - Debug Form

Lỗi 1: Dòng 1 - Trường "Tên" không có `<label for="...">`, vi phạm accessibility.
Sửa: `<label for="fullname">Tên:</label> <input type="text" id="fullname" name="fullname" required>`

Lỗi 2: Dòng 3 - Email không có `id` và `name`, nên không gắn label được và khi submit khó xử lý dữ liệu.
Sửa: `<label for="email">Email:</label> <input type="email" id="email" name="email" placeholder="Email của bạn" required>`

Lỗi 3: Dòng 5-6 - Hai ô mật khẩu không có label, người dùng screen reader không biết nhập gì.
Sửa: `<label for="password">Mật khẩu:</label> <input type="password" id="password" name="password" placeholder="Mật khẩu" required minlength="8">` và `<label for="confirm_password">Nhập lại mật khẩu:</label> <input type="password" id="confirm_password" name="confirm_password" placeholder="Nhập lại mật khẩu" required>`

Lỗi 4: Dòng 8 - Số điện thoại dùng `type="text"` và hard-code `value`, không phù hợp cho nhập liệu và không có `label`.
Sửa: `<label for="phone">Phone:</label> <input type="tel" id="phone" name="phone" placeholder="0901234567" pattern="[0-9]{10}" required>`

Lỗi 5: Dòng 10-13 - `<select>` không có `label` và các `<option>` thiếu `value` rõ ràng.
Sửa: `<label for="city">Tỉnh/Thành:</label> <select id="city" name="city" required><option value="">-- Chọn tỉnh/thành --</option><option value="hn">Hà Nội</option><option value="hcm">TP.HCM</option></select>`

Lỗi 6: Dòng 15-17 - Checkbox đồng ý điều khoản chỉ là text trong `<label>`, không có `<input type="checkbox">` nên không submit được.
Sửa: `<label for="agree"><input type="checkbox" id="agree" name="agree" required> Tôi đồng ý điều khoản</label>`

Lỗi 7: Dòng 19 - Nút submit dùng `<input type="submit">` vẫn chạy được, nhưng best practice là dùng `<button type="submit">` để linh hoạt hơn và dễ style hơn.
Sửa: `<button type="submit">Gửi</button>`

Lỗi 8: Toàn form thiếu `<form action="..." method="POST">` rõ ràng và thiếu cấu trúc `fieldset` cho nhóm field liên quan. Với form đăng ký, nên khai báo action/method và tổ chức nhóm trường hợp lý hơn.
Sửa: `<form action="#" method="POST"> ... </form>`

## C2 - Chiến lược Validation

1. Regex:
   - CMND/CCCD: `^[0-9]{12}$`
   - Số tài khoản: `^[0-9]{10,15}$`

2. HTML5 validation chưa đủ an toàn cho ứng dụng ngân hàng. Nó chỉ là validation phía client, có thể bị bỏ qua bằng DevTools, request thủ công, script, hoặc API client. Backend vẫn phải kiểm tra lại toàn bộ dữ liệu.

3. Ba loại validation HTML5 không làm được và cần JavaScript:
   - Kiểm tra confirm password có khớp password hay không.
   - Kiểm tra logic phụ thuộc giữa nhiều trường, ví dụ ngày kết thúc phải sau ngày bắt đầu.
   - Kiểm tra dữ liệu từ nguồn ngoài, ví dụ gọi API để xác minh mã giảm giá còn hiệu lực.

4. Hai rủi ro bảo mật nếu chỉ validate frontend:
   - Kẻ xấu có thể gửi request giả mạo với dữ liệu sai hoặc độc hại trực tiếp vào backend.
   - Dữ liệu bẩn có thể đi vào database, gây lỗi nghiệp vụ, lỗi tính toán, hoặc mở đường cho injection nếu backend xử lý thiếu an toàn.
