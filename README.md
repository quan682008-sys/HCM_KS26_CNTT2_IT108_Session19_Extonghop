# HCM_KS26_CNTT2_IT108_Session19_Extonghop
# BÀI LÀM – BẢO MẬT TÀI KHOẢN VÀ SECRETS

## Phần 1: Nhận diện nguy cơ bảo mật

### 1. Phân tích hai tình huống

**Tình huống 1: Typosquatting (Phishing)**

Trang `githuh-security.com` có tên gần giống GitHub nhưng bị sai chữ "github" thành "githuh". Đây có thể là website giả mạo nhằm dụ người dùng nhập mật khẩu để đánh cắp tài khoản.

**Tình huống 2: Mã độc từ phần mềm crack**

Việc yêu cầu tắt Windows Defender trước khi cài phần mềm crack là dấu hiệu rất đáng nghi. Khi tắt chương trình bảo vệ, máy tính dễ bị mã độc xâm nhập và đánh cắp thông tin cá nhân.

### 2. Quy tắc 5 không

- Không nhấn vào đường link đáng ngờ.
- Không nhập mật khẩu vào website được dẫn từ email lạ.
- Không tải hoặc sử dụng phần mềm crack.
- Không tự ý tắt Windows Defender hay phần mềm diệt virus.
- Không bỏ qua những cảnh báo bảo mật của hệ thống.

### 3. Bốn bước xử lý khi gặp sự cố

1. Ngắt kết nối Internet để hạn chế mã độc liên lạc ra ngoài.
2. Sử dụng một thiết bị an toàn khác để thay đổi mật khẩu quan trọng.
3. Quét mã độc, xử lý các tệp nguy hiểm hoặc cài lại hệ điều hành nếu cần.
4. Thông báo cho nhóm hoặc quản trị viên để được hỗ trợ.

## Phần 2: Quản lý mật khẩu an toàn

### 1. Nguy cơ khi dùng chung mật khẩu

Nếu email, GitHub và Vercel đều sử dụng cùng một mật khẩu, chỉ cần một dịch vụ bị lộ thông tin đăng nhập thì các tài khoản còn lại cũng có nguy cơ bị chiếm quyền.

Kẻ tấn công có thể sử dụng kỹ thuật **Credential Stuffing**, tức là lấy thông tin đăng nhập đã bị rò rỉ để thử trên những dịch vụ khác.

Vì vậy, mỗi tài khoản nên có mật khẩu riêng và bật 2FA để tăng khả năng bảo vệ.

### 2. Cơ chế Zero-Knowledge

Zero-Knowledge trong trình quản lý mật khẩu có nghĩa là dữ liệu được mã hóa trước khi gửi lên máy chủ.

Khóa mã hóa được tạo từ thông tin bí mật của người dùng, chẳng hạn Master Password. Nhà cung cấp không có quyền truy cập trực tiếp vào mật khẩu gốc hay nội dung đã giải mã.

Nhờ đó, nếu dữ liệu trên máy chủ bị đánh cắp, kẻ xấu cũng khó đọc được nội dung khi không có khóa giải mã.

### 3. Cấu hình tạo mật khẩu mạnh

| Thông số | Thiết lập |
|---|---|
| Độ dài | 20 ký tự |
| Chữ hoa A–Z | Bật |
| Chữ thường a–z | Bật |
| Chữ số 0–9 | Bật |
| Ký tự đặc biệt | Bật |

Em chọn mật khẩu dài 20 ký tự và kết hợp nhiều loại ký tự để tăng độ khó khi bị dò mật khẩu.

## Phần 3: Xác thực hai yếu tố (2FA)

### 1. So sánh SMS OTP và Authenticator

**SMS OTP có hai hạn chế:**

- Có nguy cơ bị chiếm mã khi kẻ xấu thực hiện SIM Swapping.
- Phụ thuộc vào sóng điện thoại, đồng thời tin nhắn có thể bị chặn hoặc đánh cắp.

**Authenticator App (TOTP):**

Ứng dụng tạo mã xác thực trực tiếp trên điện thoại, không cần gửi qua SMS. Mã thường thay đổi sau 30 giây và vẫn hoạt động khi không có Internet.

Vì vậy, em ưu tiên sử dụng Authenticator vì an toàn hơn trước những hình thức tấn công vào SIM và mạng di động.

### 2. Các bước bật 2FA trên GitHub

1. Đăng nhập GitHub và vào **Settings**.
2. Mở mục **Password and authentication**.
3. Chọn **Enable two-factor authentication**.
4. Chọn phương thức **Authenticator App**.
5. Dùng Google Authenticator quét mã QR.
6. Nhập mã gồm 6 chữ số để hoàn tất xác thực.

### 3. Lưu trữ mã khôi phục

**Nên làm:**

- Lưu mã trong trình quản lý mật khẩu như Bitwarden.
- In mã ra giấy và cất tại vị trí an toàn.

**Không nên làm:**

- Gửi mã qua email hoặc Zalo.
- Lưu mã bằng ảnh chụp màn hình không được bảo vệ.
- Đưa mã lên GitHub hoặc các thư mục công khai.

Mã khôi phục rất quan trọng vì có thể giúp đăng nhập khi mất điện thoại hoặc không sử dụng được ứng dụng Authenticator.

## Phần 4: Bảo vệ Secrets trong mã nguồn

### 1. Xác định thông tin nhạy cảm

Trong đoạn code ban đầu có hai thông tin không nên viết trực tiếp:

- `API_KEY`: Khóa dùng để truy cập API.
- `DB_PASSWORD`: Mật khẩu kết nối cơ sở dữ liệu.

Việc hardcode những giá trị này có thể khiến thông tin bị lộ khi chia sẻ hoặc đẩy code lên GitHub.

### 2. Code sau khi chỉnh sửa

```js
require("dotenv").config();

const API_KEY = process.env.API_KEY;
const DB_PASSWORD = process.env.DB_PASSWORD;

function connectDatabase() {
  return connect(DB_PASSWORD);
}
```

**File `.env`**

```env
API_KEY=your_api_key_here
DB_PASSWORD=your_database_password_here
```

**File `.gitignore`**

```gitignore
.env
node_modules/
```

**File `.env.example`**

```env
API_KEY=
DB_PASSWORD=
```

Ở đây, em chuyển thông tin nhạy cảm sang file `.env` và sử dụng `process.env` để đọc dữ liệu. File `.gitignore` giúp Git không tự động theo dõi file `.env` nếu file này chưa được đưa vào Git trước đó.

Còn `.env.example` chỉ dùng để hướng dẫn người khác cấu hình môi trường, không chứa mật khẩu thật.

### 3. Bốn bước kiểm tra trước khi Push GitHub

1. Kiểm tra `.gitignore` đã khai báo `.env` hay chưa.
2. Sử dụng `git status` và `git diff --cached` để kiểm tra các thay đổi chuẩn bị commit.
3. Rà soát mã nguồn xem còn API Key, Password hoặc Token nào bị viết trực tiếp không.
4. Kiểm tra lịch sử commit. Nếu từng đẩy Secret lên GitHub thì phải thu hồi hoặc thay đổi Secret đó ngay.

