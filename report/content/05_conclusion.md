# Kết luận {#conclusion}

Do là một ứng dụng ổn định, với lịch sử phát triển lâu dài, được hỗ trợ và phát triển bởi Redhat
dưới điều khoản mã nguồn mở, nên Keycloak không có điểm yêu nào mà nhóm có thể tìm ra với hiểu biết
hiện tại. Các tính năng hiện có của Keycloak cũng phần nhiều đáp ứng được hết các yêu cầu cần thiết
của một hệ thống IAM hiện đại.

Trong thực hiện bài tập lớn này, nhóm đã thực hiện được phần lớn các yêu cầu được đặc ra bởi đề bài.
Trong đó, có hai yêu cầu quan trọng vẫn chưa thực hiện được:

- Hỗ trợ đăng nhập bằng PIN: Nhóm không rõ lắm PIN có khác gì với mật khẩu hay không. Nhưng vì
Keycloak không hỗ trợ một người dùng có nhiều mật khẩu, nên nhóm không thể hiện thực tính năng này.
Nếu có thể thay thế được, Keycloak có hỗ trợ sử dung OTP bằng các ứng dung như Google Authenticator,
Authy hay FreeOTP.

- Hỗ trợ đăng nhập bằng smart card: Nhóm xác định cấu trúc thông tin của thẻ tương tự password
(chuỗi dữ liệu thô). Từ đó mặc định rằng việc đăng nhập bằng smart card cũng giống như là đăng nhập
bằng password. Tương tự như PIN, Keycloak không hỗ trợ nhiều mật khẩu cho một người dùng, bởi vậy
không thể hiện thực được tính năng này.

Từ kết quả đã có của nhóm, một số hướng có thể phát triển thêm bao gồm:

- Tích hợp dịch vụ thư mục vào Keycloak (ví dụ OpenLDAP)
- Thiết đặt và vận hành giao thức SAML cho việc đăng nhập
- Thiết đặt Social login (đắng nhập từ các tài khoảng mạng xã hội)
- Tìm hiểu về tính năng triển khai Keycloak trên cluster, nhằm tăng availability và reliability
