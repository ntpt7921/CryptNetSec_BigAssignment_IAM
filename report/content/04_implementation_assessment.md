# Hiện thực và đánh giá {#implementation_assessment}

## Hiện thực

Do sử dung Keycloak đã được viết sẵn, nhóm không có hiện thực nội dung.

## Đánh giá

Về bảo mật, một dự án nổi tiếng và được nhiều người sử dụng, được cập nhật thường xuyên như Keycloak
sẽ có khả năng rất thấp tồn tại lỗ hổng bảo mật nghiêm trọng. Gần như chắc chắn rằng bất ứng dụng gì
mà nhóm có thể viết được trong thời gian làm bài tập lớn này sẽ có khả năng bảo mật thấp hơn so với
Keycloak. Bởi vậy, tính bảo mật của Keycloak sẽ không được nhóm đánh giá, chủ yếu vì nhóm không có
đủ khả năng để thực hiện đánh giá này.

Nội dung ở chương này nhóm sẽ dành để viết lại các bước để thử các chức năng yêu cầu của bài tập
[^note].

[^note]: Xem phụ lục để biết thêm quá trình cài đặt và thiết đặt của Keycloak, các hành động trong
    chương này ngầm định rằng các bước nên trong phụ lục đã được thực hiện.

### Chức năng quản trị thông qua web

Mọi thiết đặt và tùy chỉnh làm việc của Keycloak đều có thể được xem và thay đổi dưới quyền
administrator, truy cập qua Keycloak Admin Console (`http://localhost:8080/admin`). Dưới quá trình
triển khai thực tế, `locahost` sẽ được thay bằng địa chỉ của máy chủ mà Keycloak được triển khai.
Cổng mà Keycloak nghe cũng có thể được thay đổi được, `8080` là giá trị mặc định cho giao diện
HTTP trên máy local.

Keycloak cũng hỗ trợ truy cập qua HTTPS, và yêu cầu người dùng phải cung cấp certfiticate để
Keycloak hoạt động như một web server bảo mật. Nhóm đã có thử tính năng này trên máy local bằng cách
tạo một CA ảo và đăng kí certificate bằng CA ảo này[^cert]. Nếu các thiết đặt trên thành công, cổng
mặc định cho HTTPS của Keycloak là `8443`.

![Keycloak Admin Console, nhập mật khẩu cho tài khoản admin đã cài đặt trước đó](./img/admin-console.png){width=80%}

Ngoài ra, một số người dùng đặt biệt có thể được tạo ra với quyền hạn (privileges) điều chỉnh được,
admin có thể điều chỉnh các người dùng này với quyền hạn gần tương đương với admin, nhằm phân bố
trách nhiệm quản lý. Nhưng trong bài này ta sẽ thực hiện các thao tác chỉ với tài khoảng `admin` và
người dùng `test-user`, do không có yêu cầu đòi hỏi thêm.

[^cert]: Xem `mkcert`
    ([https://github.com/FiloSottile/mkcert](https://github.com/FiloSottile/mkcert)). Nhóm bỏ qua
    hướng dẫn chi tiết sử dụng cho công cụ này vì nó không đóng góp đáng kể tới thỏa mãn nhu cầu đề 
    bài.

### Chức năng quản lý người dùng

Trong Keycloak, mỗi realm sẽ tự quản lý danh sách người dùng của riêng mình. Để thực hiện các thao
tác chỉnh sửa (tạo, xóa, thay đổi người dùng, tìm kiếm người dùng) có thể được thực hiện từ của sổ
giao diện `Users` của realm tương ứng.

![Tab quản lý người dùng cho realm master, có thể được truy cập từ menu bên phải](./img/user-man-tab.png){width=80%}

Ta có thể thực hiện thêm người dùng (các bước thực hiện có được miêu tả trong phụ lục).

Ta có thể thực hiện xóa người dùng (từ danh sách các người dùng đã chọn, hay trong giao diện thiết
đặt của từng người dùng).

Ta có thể tìm kiếm người dùng, hoặc là tìm theo thiết đặt tìm kiếm mặc định, hoặc là tìm theo việc
lọc các giá trị của thuộc tính mà người dùng sở hữu.

![Tìm kiếm bằng cách lọc giá trị thuộc tính của người dùng](./img/user-attr-search.png){width=80%}

Ngoài ra, các thuộc tính của từng người dùng cũng có thể được thiết đặt, có thể nói tới như email,
tên, tuổi, danh tính (credentials - mật khẩu hoặc/và mã OTP), nhóm, quyền,...

Từng người dùng cũng có quyền được thay đổi một số thuộc tính của mình, cộng với việc thay đổi mật
khẩu và thiết đặt OTP (nếu thiết đặt bởi admin cho phép). Người dùng sẽ truy cập vào Keycloak
Account Console (ở `http://localhost:8080/realms/<realm_name>/account` - trong trường hợp của ta là
[http://localhost:8080/realms/test-realm/account](http://localhost:8080/realms/test-realm/account)).

### Chức năng xác thực

Quá trình xác thực cũng gần tương tự như quá trình làm truy cập vào Keycloak Admin Console. Một ứng
dụng của người dùng, tuân theo một chuẩn nào đó (ta sẽ ngầm định là OpenID Connect) sẽ thực hiển gửi
thông cần thiết tới địa chỉ gateway tương ứng của server Keycloak, đồng thời redirect trình duyệt
của người dùng tới giao diện đăng nhập và Keycloak quản lý. Quá trình đăng nhập sẽ được giao phó có
server Keycloak thực hiện. Kết quả của việc đăng nhập sẽ được giao tiếp giữa ứng dụng (client) và
Keycloak. Chi tiết quá trình và thông tin giao đổi được nói kĩ hơn ở \ref{theoretical_basis}.

Sau đây ta sẽ sử dụng một ứng dụng được cung cấp sẵn bởi Keycloak, truy cập ở
[https://www.keycloak.org/app/](https://www.keycloak.org/app/). Ứng dụng này sẽ đóng vai trò client,
thực hiện việc kết nối tới server Keycloak để thử tính năng xác thực.

![Điền thông tin cần thiết vào các trường, theo tứ tự từ trên xuống dưới, ta sẽ điền vào: URL của server Keycloak, tên của realm (`test-realm` trong trường hợp này), ID của client được thiết đặc trong realm (`test-client` trong trường hợp này). Sau đó nhấn Save.](./img/keycloak-test-app-01.png){width=80%}

Sau đó nhấn vào Sign-in, trình duyệt sẽ được chuyển tới trang đăng nhập của Keycloak. Ta sẽ nhập mật
khẩu của người dùng cần đăng nhập (ở đây là người dùng `test-user`). Nếu đăng nhập thành công, trình
duyệt sẽ chuyển hướng trỏ lại ứng dụng ban đầu.

![Sau khi đăng nhập thành công, Keycloak sẽ gửi các thông tin cần thiết (hoặc được yêu cầu) tới client, trong trường hợp này có kèm theo giá trị của các thuộc tính tên của người dùng. `test` và `user` là hai giá trị ứng với các thuộc tính tên được gửi trả, client giờ đây đã biết và hiển thị được hai giá trị này](./img/keycloak-test-app-02.png){width=80%}

![Session người dùng `test-user` sẽ được hiển thị sau khi đăng nhập thành công](./img/sessions.png){width=80%}

Từ giao diện client đã đăng nhập thành công, ta bấm vào Sign out để đăng xuất khỏi session.

### Chức năng nhật ký

Qua quá trình đăng nhập và đăng xuất ở mục trước, giờ ta có thể xem nhật ký các hành động của người
dùng.

![Nhật ký của quá trình đăng nhập, do có nhập sai mật khẩu một lần nến có hiện cảnh báo](./img/logging-history.png){width=80%}

