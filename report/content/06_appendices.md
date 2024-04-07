\newpage
\appendix

# Giới thiệu và cài đặt Keycloak

## Giới thiệu Keycloak

![Logo của Keycloak](./img/keycloak_icon.png){width=70%}

Keycloak

: Quản lý quyền truy cập và nhận dạng nguồn mở

    Thêm xác thực vào các ứng dụng và dịch vụ bảo mật với nỗ lực tối thiểu. Không cần phải xử lý việc
    lưu trữ người dùng hoặc xác thực người dùng.

    Keycloak cung cấp liên kết người dùng (federation), xác thực mạnh mẽ, quản lý người dùng, ủy quyền
    chi tiết, v.v. 

Tính năng:

- Single-Sign On: Đăng nhập một lần vào nhiều ứng dụng
- Giao thức chuẩn: OpenID Connect, OAuth 2.0 và SAML 2.0
- Quản lý tập trung: Dành cho quản trị viên và người dùng
- LDAP và Active Directory: Kết nối với thư mục người dùng hiện có
- Đăng nhập xã hội: Dễ dàng kích hoạt đăng nhập xã hội
- Môi giới nhận dạng: OpenID Connect hoặc SAML 2.0 IdP
- Hiệu suất cao: Nhẹ, nhanh và có thể mở rộng
- Clustering: Dành cho khả năng mở rộng và tính sẵn sàng
- Giao diện: Tùy chỉnh giao diện
- Chính sách mật khẩu: Tùy chỉnh chính sách mật khẩu

Hiện tại, Keycloak được phát triển dưới sự hậu thuẫn của Redhat - các nhà phát triển được thuê làm
việc trên dự án này dưới quyền của Redhat. Nhưng chương trình vẫn giữ giấy phép mã nguồn mở
Apache License 2.0.

Với thiết đặt ban đầu dễ dàng, tính năng đầy đủ, chạy được trên nhiều nền tảng (Keycloak được viết
bằng Java). Keycloak là một lựa chọn rất lý tưởng ứng với các yêu cầu của bài tập lớn của nhóm.

## Cài đặt Keycloak

Keycloak được cung cấp với nhiều phương pháp cài đặt khác nhau. Ta có thể chọn một trong nhiều
phương pháp cài đặt để phát đầu sử dụng Keycloak như:

- Cài thẳng và chạy bằng runtime OpenJDK
- Chạy trong container với Docker
- Chạy trong container với Podman

Nhóm chọn cài đặt bằng phương pháp cài thẳng và chạy bằng runtime OpenJDK.

### Cài OpenJDK

Theo hướng dẫn ở trang web [OpenJDK](https://openjdk.org/install/)[^install-openjdk].

[^install-openjdk]: [https://openjdk.org/install/](https://openjdk.org/install/).

Phiên bản hiện tại của Keycloak là 24.0.2, với yêu cầu phiên bản OpenJDK 17. Ta có hai phương pháp
có thể dùng để cài đặt dependency này:

#### Dùng package manager trên Linux (Debian)

Nhóm chủ yêu cài đặt bằng phương pháp này.

```bash
sudo apt install openjdk-17-jre
```

Sau khi cài đặt thành công, ta sẽ có thể làm việc được ta có thể tiếp tục tới bước tiếp theo.

#### Dùng prebuilt binary chính thức trên OpenJDK

Vào trang web [OpenJDK JDK 22 General-Availability Release](https://jdk.java.net/22/)[^jdk22].

Hiện tại phiên bản chính thức mới nhất của OpenJDK được cung cấp bởi trang web là OpenJDK 22. Mặc dù
yêu của của Keycloak là OpenJDK 17, ta có thể tin tưởng rằng các phiên bản với hơn của JDK sẽ tương
thích ngược với các phiên bản (không quá) cũ.

![Chọn phiên bản phù hợp cho hệ thống cần cài đặt, ở đây nhóm chọn `Linux/x64`](./img/openjdk_download.png){width=100%}

Các file sau khi giải nén ra sẽ cần được đưa vào biến môi trường `PATH` và `JAVAHOME`. Bước này có
khác nhau giữa các hệ điều hành, nhưng các bước thực hiện vẫn tương đối đơn giản. Chi tiết cho bước
này có thể được tìm thấy ở [trang web hướng dẫn cài đặt của
freeCodeCamp](https://www.freecodecamp.org/news/install-openjdk-free-java-multi-os-guide/)[^fcc-install].

[^fcc-install]: [https://www.freecodecamp.org/news/install-openjdk-free-java-multi-os-guide/](https://www.freecodecamp.org/news/install-openjdk-free-java-multi-os-guide/)

[^jdk22]: [https://jdk.java.net/22/](https://jdk.java.net/22/)

### Tải Keycloak 

Vào trang web [Download của Keycloak](https://www.keycloak.org/downloads)[^kc-download]. Do ta chọn phương thức
cài đặt thẳng và chạy bằng runtime, nên ta sẽ chọn `Server` \rightarrow `Keycloak`.

[^kc-download]: [https://www.keycloak.org/downloads](https://www.keycloak.org/downloads)

![Mục ta chọn để download được tô đỏ. Link resource cài đặt cho các phương pháp cài đặt khác cũng có
thể được thấy trong hình](./img/keycloak-download.png){width=100%}

Giải nén file tải về, ta có thư mục chứa file chương trình cho Keycloak.

### Khởi động Keycloak

Trên môi trường dòng lệnh, ta chuyển vào thư muc của Keycloak đã giải nén ở bước trước. Chú ý rằng
sẽ có một file script dùng để khởi động Keycloak ở `bin/kc.sh`. Ta sẽ chạy file này để khởi động
server Keycloak.

```bash
bin/kc.sh start-dev
```

![Kết quả khởi động Keycloak trên dòng lệnh](./img/startup-result.png)

Sử dụng tùy chọn `start-dev`, bạn đang khởi động Keycloak ở chế độ phát triển. Ở chế độ này, bạn có
thể dùng thử Keycloak lần đầu tiên để thiết lập và chạy nhanh. Chế độ này cung cấp các cài đặt mặc
định thuận tiện cho nhà phát triển.

Mặc định, Keycloak sẽ nghe ở cổng 8080 trên localhost. Để truy cập vào server vừa được khởi tạo, mở
`http://localhost:8080` bằng trình duyệt của bạn. Mặc định, Keycloak không có thiết đặt sẵn admin.
Trong lần mở đầu tiên, server sẽ yêu cầu bạn thiết đặt các thông tin đăng nhập cho tài khoảng admin.
Thông tin đăng nhập này sẽ được lưu dưới dạng riêng của Keycloak, lưu trữ qua nhiều lần khởi động.

# Thiết đặt Keycloak

Ở mục này, ta sẽ miêu tả một số thao tác thiết đặt cần thiết để sử dụng các tính năng được yêu cầu
bởi bài tập lớn.

## Thiết đặt các realm

### Tạo realm

Một realm trong Keycloak cũng giống với một căn nhà được cho thuê. Mỗi realm cho phép quản trị viên
tạo các nhóm ứng dụng và người dùng riêng biệt. Ban đầu, Keycloak bao gồm một realm duy nhất, được
gọi là `master`. Chỉ sử dụng realm này để quản lý Keycloak chứ không phải để quản lý bất kỳ ứng
dụng nào.

![Vị trí trên giao diện dùng để chuyển realm và tạo realm mới](./img/create-realm.png){width=80%}

Các bước dùng để tạo một realm:

1. Mở Keycloak Admin Console (ở [http://localhost:8080/admin](http://localhost:8080/admin)).
2. Bấm vào nút `Create Realm`
3. Nhập tên tùy chọn cho realm của bạn.
4. Xác nhận

### Tạo user

Ban đầu, realm không có người dùng (user). Thực hiện các bước sau để tạo một người dùng.

![Chọn realm và nhấp vào tab `Users` để bắt đầu tạo người dùng mới](./img/create-user.png){width=100%}

1. Trong Keycloak Admin Console (ở [http://localhost:8080/admin](http://localhost:8080/admin)),
   chọn realm mà bạn muốn tạo người dùng. Bấm vào `Users` trong menu ở bên trái.
2. Chọn nút `Add user`.
3. Đưa các thông tin cần thiết

    - `Username`: Đặt tùy ý (ví dụ `test-user`)
    - `First name`: Đặt tùy ý (ví dụ `test`)
    - `Last name`: Đặt tùy ý (ví dụ `user`)

4. Xác nhận, nếu thành công bạn sẽ được đưa đến trang thiết đặt của tài khoản `test-user` vừa mới
   tạo. Ta sẽ tiếp tục thiết đặt mật khẩu cho tài khoản.

Người dùng này sẽ cần phải có một mật khẩu được thiết đặt để đăng nhập vào dịch vụ được. Ta thực
hiện các bước sau để thiết đặt một credential mới cho `test-user`.

![Đặt mật khẩu cho người dùng `test-user`](./img/set-password.png){width=80%}

1. Bắt đầu từ trang thiết đặt của `test-user`. Chọn tab `Credentials`. Ta chọn `Set password`.
2. Đặt mật khẩu cho người dùng. Nếu thiết đặt `Temporary` được chọn, người dùng sẽ phải thiết đặt
   một password mới trong lần đăng nhập tiếp theo.
3. Xác nhận

### Tạo client (login gateway)

Để kích hoạt khả năng tạo đăng nhập cho người dùng, ta cần thiết đặt một gateway (hiểu là nơi mà
server sẽ tiếp nhận các yêu cầu từ người dùng). Các dịch vụ muốn sử dụng khả năng đăng nhập cung cấp
bởi Keycloak sẽ gửi yêu cầu tới các gateway. Duới góc nhin của Keycloak, mỗi một ứng dụng (client)
sẽ sử dụng một gateway duy nhất. Bởi vậy khi ta thiết đặt một gateway, từ được dùng trong Keycloak
là thiết đặt client.

Ta thực hiện các bước sau để thiết đặt một client:

![Thiết đặt client mới](./img/create-client.png){width=80%}

1. Bắt đầu từ Keycloak Admin Console (ở [http://localhost:8080/admin](http://localhost:8080/admin)),
   chọn realm để thiết đặt client. Bấm vào `Clients` trong menu ở bên trái.
2. Nhấp chọn `Create client` và điền thông tin cần thiết 
    - `Client type`: `OpenID Connect'`
    - `Client ID`: tùy ý (ví dụ `test-client`)

3. Xác nhận, ta được chuyển tới trang `Capability config`.

    ![Trang `Capability config` được chuyển tới](./img/client-config-capability.png){width=80%}

4. Chọn `Standard flow`, kích hoạt Authorization Code Flow cho client này. Các client khác sẽ không
   được dùng tới nên ta sẽ chỉ chọn tùy chọn này.

5. Xác nhận, ta sẽ được chuyển tới trang `Login settings`.

    ![Trang `Login settings` được chuyển tới](./img/login-settings.png){width=80%}

    Ở đây ta sẽ có một số trường quan trọng, liên quan tới việc server sẽ gửi trình duyệt của người
    dùng tới địa chỉ nào khi người dùng thực hiện các hành động trong quá trình đăng nhập/đăng xuất.

    - `Valid redirect URIs`: Đặt thành `https://www.keycloak.org/app/*` (ta sẽ sử dụng app do
    Keycloak cung cấp để thử hoạt động của gateway này).

    - `Web origins`: Địa chỉ web origin của client sử dụng gateway này (đặt thành
    `https://www.keycloak.org`, tương ứng với thiết đặt trên)

6. Xác nhận lần cuối

### Kích hoạt ghi nhật ký cho user và admin

Mặc định, các hành động của user và admin không được ghi nhật ký lại. Để thể hiện được tính năng ghi
nhật ký, ta cần phải kích hoạt các tính năng này.

Ta thực hiện các bước sau để kích hoạt tính năng cho admin và user:

1. Truy cập vào realm muốn thiết đặt, đi tới cửa số `Realm settings` (truy cập từ menu bên trái). Đi
   tới tab `Events`.

   ![Truy cập vào cửa số `Realm settings`, đi tới tab `Events`](./img/events.png){width=80%}

2. Có hai tab nhỏ hơn `User events settings` và `Admin events settings`. Kích hoạt tùy chọn `Save
   events` và xác nhận bằng cách nhấn nút `Save`.

   ![Kích hoạt logging](./img/log-enable.png){width=80%}
