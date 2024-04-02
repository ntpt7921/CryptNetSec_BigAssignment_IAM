# Cơ sở lý thuyết {#theoretical_basis}

## IAM

Identity Management (IdM) - quản lý danh tính, hay với tên khác Identity and Access Management (IAM
hoặc IdAM) - quản lý danh tính và quyền truy cập, là một khung chính sách và công nghệ để đảm bảo
rằng đúng người dùng (là một phần của hệ sinh thái được kết nối với hoặc trong doanh nghiệp) có
quyền truy cập phù hợp đến nguồn lực công nghệ. Các hệ thống IdM nằm trong phạm trù về bảo mật CNTT
và quản lý dữ liệu. IAM không chỉ xác định, xác thực và kiểm soát quyền truy cập của các cá nhân -
nó cũng kiểm soát tương tự phần cứng và ứng dụng mà nhân viên cần truy cập.

IdM (hoặc IAM) là các quy trình tổ chức và kỹ thuật để đăng ký và cấp phép quyền truy cập đầu tiên
trong giai đoạn cấu hình, sau đó là giai đoạn vận hành để xác định, xác thực và kiểm soát các cá
nhân hoặc nhóm người dùng có quyền truy cập vào các ứng dụng, hệ thống hoặc mạng dựa trên quyền truy
cập được cấp trước đó. Quản lý danh tính (IdM) là nhiệm vụ kiểm soát thông tin về người dùng trên
máy tính. Thông tin đó bao gồm thông tin xác thực danh tính của người dùng và thông tin mô tả dữ
liệu và hành động mà họ được phép truy cập và/hoặc thực hiện. Nó cũng bao gồm việc quản lý thông tin
mô tả về người dùng cũng như cách thức và ai có thể truy cập và sửa đổi thông tin đó. Ngoài người
dùng, các thực thể được quản lý thường bao gồm tài nguyên phần cứng và mạng và thậm chí cả ứng dụng.

Thực thể, danh tính và thuộc tính:

: Trong hầu hết các mô hình lý thuyết và thực tế về danh tính số, một đối tượng danh tính nhất định
bao gồm một tập hữu hạn các thuộc tính. Các thuộc tính này ghi lại thông tin về đối tượng, cho các
mục đích bên ngoài mô hình hoặc để vận hành mô hình, ví dụ như trong phân loại và truy xuất.

![Nói chung, một thực thể - entity - (thực hoặc ảo) có thể có nhiều danh tính - identity - và mỗi
danh tính có thể bao gồm nhiều thuộc tính - attribute/property, trong đó danh tính phải là duy nhất
trong một không gian tên nhất định nào đó. Sơ đồ minh họa mối quan hệ khái niệm giữa danh tính và
thực thể, cũng như giữa danh tính và thuộc tính của chúng.](img/Identity-concept.png){width=100%}

Trong bối cảnh thực tế, quản lý danh tính có thể bao gồm bốn chức năng cơ bản:

1. Chức năng quản lý danh tính: Tạo, quản lý và xóa danh tính mà không quan tâm đến quyền truy cập
   hoặc quyền lợi.

2. Chức năng truy cập (đăng nhập) của người dùng: Ví dụ: thẻ thông minh và dữ liệu liên quan của nó
   được khách hàng sử dụng để đăng nhập vào một hoặc nhiều dịch vụ.

3. Liên kết danh tính: Liên kết danh tính bao gồm một hoặc nhiều hệ thống chia sẻ quyền truy cập của
   người dùng và cho phép người dùng đăng nhập dựa trên việc xác thực đối với một trong các hệ thống
   tham gia liên kết. Sự tin cậy này giữa một số hệ thống thường được gọi là "Vòng tròn tin cậy".

   Ví dụ: Đăng nhập vào một dịch vụ nào đó sử dụng tài khoảng Google, ở đây dịch vụ sẽ gửi yêu cầu
   và chuyển hướng người dùng đến trang đăng nhập của Google; sau khi người dùng đăng nhập thành
   công, hệ thống IAM của Google sẽ gửi xác nhận (được ki số) tới dịch vụ. Người dùng không cần phải
   tạo tài khoảng riêng cho nhiều dịch vụ. OpenID Connect là một giao thức xác thực ta sẽ nói tới và
   được dùng trong bài này.

4. Chức năng giám sát: Giám sát các tắc nghẽn, trục trặc và hành vi đáng ngờ.

## OpenID Connect

OpenID Connect (OIDC) là một giao thức xác thực có khả năng tương tác dựa trên khung thông số kỹ
thuật OAuth 2.0 (IETF RFC 6749 và 6750). OIDC cung cấp xác thực, có nghĩa là xác minh rằng người
dùng đúng như họ nói. OAuth 2.0 ủy quyền những hệ thống mà người dùng được phép truy cập. OAuth 2.0
thường được sử dụng để cho phép hai ứng dụng không liên quan chia sẻ thông tin mà không ảnh hưởng
đến dữ liệu người dùng. Nó đơn giản hóa cách xác minh danh tính của người dùng dựa trên xác thực
được thực hiện bởi Máy chủ ủy quyền và để lấy thông tin hồ sơ người dùng theo cách có thể tương tác
và giống như REST.

OpenID Connect cho phép các nhà phát triển ứng dụng và trang web khởi chạy các luồng đăng nhập và
nhận các xác nhận có thể kiểm chứng về người dùng trên các ứng dụng khách dựa trên Web, thiết bị di
động và JavaScript. Và bộ thông số kỹ thuật có thể mở rộng để hỗ trợ nhiều tính năng tùy chọn như mã
hóa dữ liệu nhận dạng, khám phá Nhà cung cấp OpenID và đăng xuất phiên.

Đối với các nhà phát triển, nó cung cấp câu trả lời an toàn và có thể xác minh cho câu hỏi “Danh
tính của người hiện đang sử dụng trình duyệt hoặc ứng dụng di động được kết nối là gì?” Trên hết, nó
loại bỏ trách nhiệm thiết lập, lưu trữ và quản lý mật khẩu thường liên quan đến vi phạm dữ liệu dựa
trên thông tin xác thực.

Có sáu thành phần chính trong OIDC:

- Authentication (xác thực) là quá trình xác minh rằng người dùng đúng như họ nói.
- Người dùng là những người hoặc dịch vụ tìm cách truy cập ứng dụng mà không cần tạo tài khoản mới
hoặc cung cấp tên người dùng và mật khẩu.
- Client là phần mềm, chẳng hạn như trang web hoặc ứng dụng, yêu cầu token được sử dụng để xác thực
người dùng hoặc truy cập tài nguyên.
- Relying party (bên tin cậy) là các ứng dụng sử dụng nhà cung cấp OpenID để xác thực người dùng.
- OpenID provider là các ứng dụng mà người dùng đã có tài khoản. Vai trò của họ trong OIDC là xác
thực người dùng và chuyển thông tin đó cho bên tin cậy.
- Identity token chứa dữ liệu nhận dạng bao gồm kết quả của quá trình xác thực, nhận dạng cho người
dùng và thông tin về cách thức và thời điểm người dùng được xác thực.

Quy trình xác thực OIDC điển hình bao gồm các bước sau:

1. Người dùng truy cập ứng dụng mà họ muốn truy cập (bên phụ thuộc).
2. Người dùng gõ tên người dùng và mật khẩu của họ.
3. Bên dựa sẽ gửi yêu cầu đến nhà cung cấp OpenID.
4. Nhà cung cấp OpenID xác thực credential của người dùng và và cấp ủy quyền.
5. Nhà cung cấp OpenID gửi mã identity token (và thường có thêm access token) cho bên phụ thuộc.
6. Bên dựa sẽ gửi access token đến thiết bị của người dùng.
7. Người dùng được cấp quyền truy cập dựa trên thông tin được trong access token.

![Sơ đồ OIDC authorization (basic) flow. Bước 1, người dùng cố gắng bắt đầu một phiên client và được
chuyển hướng đến OpenID provider, đi kèm với client ID độc nhất của client đó; bước 2, OpenID
provider xác thực và ủy quyền cho người dùng trong một một phiên làm việc cụ thể; bước 3,
one-time-code sẽ được chuyển trở lại client bằng URI redirect định trước; bước 4, client chuyển
one-time-code, client ID và client secret đến OpenID provider, OpenID provider xác thực mã và trả về
access token có thời hạn sử dụng. Ở Bước 5, client sử dụng access token để biết thêm thông tin chi
tiết về người dùng (nếu cần) và thiết lập phiên cho người
dùng.](./img/oidc-basic-flow.png){width=100%}

Các luồng OIDC xác định cách yêu cầu và phân phối token cho bên phụ thuộc. Một vài ví dụ:

- OIDC authorization flow: OpenID provider gửi unique code cho bên phụ thuộc. Sau đó, relying party
sẽ gửi unique code lại cho OpenID provider để đổi lấy token. Phương pháp này được sử dụng để OpenID
provider có thể xác minh relying party trước khi gửi token. Trình duyệt không thể nhìn thấy token
trong phương pháp này, điều này giúp giữ an toàn.

- OIDC authorization flow với PKCE: Luồng này giống với luồng ủy quyền OIDC, ngoại trừ việc nó sử
dụng trao đổi mã bằng public key (public key for code exchange - PKCE) để gửi thông tin liên lạc
dưới dạng hàm băm. Điều này làm giảm khả năng token bị lộ.

- Client credentials: Luồng này cung cấp quyền truy cập vào API bằng cách sử dụng danh tính của
chính client. Nó thường được sử dụng để liên lạc từ máy chủ đến máy chủ và các tập lệnh tự động
không yêu cầu sự tương tác của người dùng.

- Device code: Luồng này cho phép người dùng đăng nhập và truy cập các API trên các thiết bị kết nối
Internet không có trình duyệt hoặc có trải nghiệm bàn phím kém, chẳng hạn như TV thông minh.


