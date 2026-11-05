# Bài 4 : Rủi ro đánh cắp mật khẩu từ trình duyệt


## Phần 1 :So sánh Google Chrome và Bitwarden

1. Khả năng chống Infostealer (File Login Data):

- Google Chrome (Rất kém): Mật khẩu lưu trong file SQLite Login Data, khóa giải mã được bảo vệ bằng Windows DPAPI. Các mã độc như RedLine, Lumma chỉ cần chạy dưới quyền user thông thường là tự động gọi DPAPI để giải mã toàn bộ mật khẩu trong vài giây.

- Bitwarden (Rất cao): Dữ liệu được mã hóa đầu cuối (AES-256). Kẻ tấn công có trích xuất được file dữ liệu của Bitwarden trên ổ cứng thì toàn bộ vẫn là chuỗi mã hóa vô nghĩa, không thể giải mã nếu không có Master Password.

2. Kiến trúc Zero-Knowledge:

- Google Chrome: Không phải Zero-Knowledge mặc định; phụ thuộc vào tài khoản Google và chỉ có tùy chọn mã hóa cục bộ khi người dùng tự cấu hình thêm.

- Bitwarden: Chuẩn Zero-Knowledge tuyệt đối. Toàn bộ quá trình mã hóa/giải mã diễn ra trên thiết bị (Client-side). Máy chủ Bitwarden không bao giờ nắm giữ Master Password hay khóa giải mã.

3. Đồng bộ chéo nền tảng:

- Google Chrome: Giới hạn chủ yếu trong trình duyệt Chrome và hệ sinh thái tài khoản Google; không hỗ trợ tốt ứng dụng desktop độc lập hay các trình duyệt khác.

- Bitwarden: Hoạt động độc lập trên mọi nền tảng (Windows, macOS, Linux, iOS, Android), mọi trình duyệt (Edge, Firefox, Safari, Chrome) và hỗ trợ chia sẻ kho mật khẩu an toàn theo nhóm phòng ban.

## phần 2 : Vì sao Bitwarden thắng thế về bảo mật dù tốn thao tác nhập Master Password
    Thao tác nhập Master Password tạo ra một độ trễ nhỏ, nhưng loại bỏ hoàn toàn cơ chế tấn công tự động của Infostealer:
    
    Không lưu khóa cố định trên đĩa: Chrome ủy quyền giải mã cho hệ điều hành, cho phép mã độc chiếm quyền tự động. Bitwarden chỉ giải mã khi có Master Password do con người nhập trực tiếp.
    
    Tự động xóa khóa khỏi bộ nhớ (Vault Timeout): Bitwarden tự động khóa sau khoảng thời gian không sử dụng. Khi khóa, khóa giải mã lập tức bị xóa khỏi RAM, đưa dữ liệu về trạng thái mã tĩnh an toàn tuyệt đối trước các đợt quét bộ nhớ.
    
    Cách ly dữ liệu: Tách biệt hoàn toàn kho mật khẩu khỏi tiến trình trình duyệt web—nơi thường xuyên đối mặt với các lỗ hổng thực thi mã từ xa (RCE).
