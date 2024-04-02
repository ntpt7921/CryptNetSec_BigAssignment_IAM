# Phân tích thiết kế {#design}

Các yêu cầu được đề ra ở mục \ref{intro} như sau:

- Các chức năng quản lý người dùng: tạo, cập nhật, xóa, tìm kiếm thông tin định danh của người dùng
với các dịch vụ thư mục như OpenLDAP.
- Các chức năng xác thực với các phương pháp: username và password, smart card và PIN(Personal
Identification Number).
- Các chức năng nhật ký để quản lý các sự kiện xác thực, thay đổi các đối tượng thư mục.
- Các chức năng quản trị thông qua Web cho việc quản lý người dùng và nhật ký.

Nhóm tìm được trên mạng một bài viết tổng hợp và so sánh các ứng dụng SSO mã nguồn mở, dược đóng góp
và viết bởi cộng đồng \cite{sso-comparison}. Nhóm quyết định sử dụng Keycloak để thực hiện bài tập
lớn này, dựa vào các đặc tính quan trọng sau:

- Có admin UI để quản lý người dùng, nhật ký và các thiết đặt khác.
- Dễ dàng cài và thiết đặt.

Mặc dù vậy, do Keycloak không hỗ trợ nên tính năng đăng nhập bằng smart card và PIN sẽ không được
hiện thực. Bài làm của nhóm sẽ thỏa mãn hết các yêu cầu được đề ra trừ hai yêu cầu đăng nhập trên.

```{=latex}
% Please add the following required packages to your document preamble:
% \usepackage{graphicx}
% \usepackage{lscape}
\begin{landscape}
\begin{table}[]
\caption{So sánh một số ứng dụng SSO mã nguồn mở}
\label{tab:my-table}
\resizebox{\columnwidth}{!}{%
\begin{tabular}{l|c|c|c|c|c|c|c|c|c|c|c|}
\cline{2-12}
\multicolumn{1}{c|}{} & \textbf{Keycloak} & \textbf{WSO2 Identity Server} & \textbf{Gluu} & \textbf{CAS} & \textbf{OpenAM} & \textbf{Shibboleth IdP} & \textbf{ZITADEL} & \textbf{Authentik} & \textbf{Authelia} & \textbf{lemonldap-ng} & \textbf{logto} \\ \hline
\multicolumn{1}{|l|}{\textbf{\begin{tabular}[c]{@{}l@{}}OpenID Connect/\\ OAuth support\end{tabular}}} & yes & yes & yes & yes & yes & yes & yes & yes & yes & yes & yes \\ \hline
\multicolumn{1}{|l|}{\textbf{\begin{tabular}[c]{@{}l@{}}Multi-factor\\ authentication\end{tabular}}} & yes & yes & yes & yes & yes & yes & yes & yes & yes & yes & yes \\ \hline
\multicolumn{1}{|l|}{\textbf{Admin UI}} & yes & yes & yes & yes & yes & no & yes & Yes &  & yes & yes \\ \hline
\multicolumn{1}{|l|}{\textbf{\begin{tabular}[c]{@{}l@{}}Identity\\ brokering\end{tabular}}} & yes & yes & yes &  &  &  & yes &  &  & yes & yes \\ \hline
\multicolumn{1}{|l|}{\textbf{Open source}} & yes & ? nominally & yes & yes & yes & yes & yes (Apache 2.0) & yes & yes & yes (GPL) & yes (MPL-2.0 license) \\ \hline
\multicolumn{1}{|l|}{\textbf{\begin{tabular}[c]{@{}l@{}}Commercial\\ support\end{tabular}}} & yes & yes & yes & third-party & yes & third-party & yes & yes &  & yes & yes \\ \hline
\multicolumn{1}{|l|}{\textbf{\begin{tabular}[c]{@{}l@{}}Add federation\\ metadata\end{tabular}}} & no & yes &  &  &  & yes & no &  &  & yes & yes \\ \hline
\multicolumn{1}{|l|}{\textbf{\begin{tabular}[c]{@{}l@{}}Add metadata\\ from URL\end{tabular}}} & import only & yes &  &  &  & yes & yes &  &  & yes & yes \\ \hline
\multicolumn{1}{|l|}{\textbf{\begin{tabular}[c]{@{}l@{}}Installation \& \\ configuration\end{tabular}}} & easy &  & difficult &  & difficult & easy/medium &  &  &  & easy/medium & easy \\ \hline
\end{tabular}%
}
\end{table}
\end{landscape}
```

