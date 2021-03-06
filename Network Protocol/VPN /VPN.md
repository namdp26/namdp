### 1. VPN là gì?
VPN (Virtual Private Network) là một công nghệ mạng giúp tạo kết nối mạng an toàn trên Public Network hoặc Private Network do một nhà cung cấp dịch vụ sở hữu. Các tập đoàn lớn, các cơ sở giáo dục và cơ quan chính phủ sử dụng công nghệ VPN để cho phép người dùng từ xa kết nối an toàn đến mạng riêng của cơ quan mình.
Ứng dụng của VPN: 
- Truy cập vào Business Network từ xa
- Truy cập vào Home Network từ xa
- Truy cập các trang web bị chặn theo vùng, quốc gia.
- Duyệt web ẩn danh
- Tải tập tin
### 2. Các giao thức phổ biến trong VPN
Các giao thức VPN gồm 1 tập hợp các giao thức. Những chức năng mà mọi VPN cần giải quyết là:
- **Tunnelling:**
Chức năng cơ bản của VPN là phân phối các gói (packet) từ điểm này đến điểm khác mà không để lộ chúng cho bất kỳ ai trên đường truyền. Để làm điều này, VPN đóng gói tất cả dữ liệu theo định dạng mà cả máy khách và máy chủ đều hiểu được. Bên gửi dữ liệu đặt nó vào định dạng tunnelling và bên nhận trích xuất để có được thông tin.
- **Encryption:** 
Tunnelling không cung cấp tính năng bảo vệ. Bất cứ ai cũng có thể trích xuất dữ liệu. Dữ liệu cũng cần phải được mã hóa trên đường truyền. Bên nhận sẽ biết cách giải mã dữ liệu từ một người gửi nhất định.
- **Authentication:** 
Để bảo mật, VPN phải xác thực danh tính của bất kỳ client nào cố gắng “giao tiếp” với nó. Client cần xác nhận rằng nó đã đến đúng máy chủ dự định.
- **Session Managerment:** 
Một khi người dùng được xác thực, VPN cần duy trì phiên để client có thể tiếp tục “giao tiếp” với nó trong một khoảng thời gian.
#### 2.1 Những giao thức yếu 
- **Point-To-Point Tunneling Protocol (PPTP)**
Giao thức cũ nhất vẫn đang được sử dụng là PPTP (Point-to-Point Tunneling Protocol). PPTP lần đầu tiên được sử dụng vào năm 1995. PPTP không chỉ định giao thức mã hóa nhưng có thể sử dụng một số giao thức như MPPE-128. Việc thiếu sự tiêu chuẩn hóa về giao thức là một rủi ro, vì nó chỉ có thể sử dụng tiêu chuẩn mã hóa mạnh nhất mà cả 2 phía cùng hỗ trợ. Nếu một phía chỉ hỗ trợ tiêu chuẩn yếu hơn thì kết nối phải sử dụng mã hóa yếu hơn người dùng mong đợi.
Tuy nhiên, vấn đề thực sự với PPTP là quá trình xác thực. PPTP sử dụng giao thức MS-CHAP, có thể dễ dàng bị crack trong giai đoạn hiện nay. Kẻ tấn công có thể đăng nhập và mạo danh người dùng được ủy quyền.
- **IP security (IPSec)**
Được dùng để bảo mật các giao tiếp, các luồng dữ liệu trong môi trường Internet (môi trường bên ngoài VPN). Đây là điểm mấu chốt, lượng traffic qua IPSec được dùng chủ yếu bởi các Transport mode, hoặc các tunnel (hay gọi là hầm - khái niệm này hay dùng trong Proxy, SOCKS) để MÃ HÓA dữ liệu trong VPN.
- **L2TP**
Giao thức L2TP thường hoạt động với thuật toán mã hóa IPSec. Nó mạnh hơn so với PPTP nhưng vẫn khiến người dùng lo ngại. Lỗ hổng chính trong L2TP/IPSec là phương thức trao đổi khóa công khai (public key). Trao đổi khóa công khai Diffie-Hellman là cách để hai bên thỏa thuận về khóa mã hóa tiếp theo và không ai được biết về khóa này. Có một phương pháp có thể “bẻ khóa” quá trình này, đòi hỏi sức mạnh điện toán khá lớn, nhưng sau đó nó cho phép truy cập vào tất cả các giao tiếp trên một VPN nhất định
- **Secure Sockets Layer (SSL) và Transport Layer Security (TLS)**
Có 1 phần tương tự như IPSec, 2 giao thức trên cũng dùng mật khẩu để đảm bảo an toàn giữa các kết nối trong môi trường Internet.
Bên cạnh đó, 2 giao thức này còn sử dụng chế độ Handshake - có liên quan đến quá trình xác thực tài khoản giữa client và server. Để 1 kết nối được coi là thành công, quá trình xác thực này sẽ dùng đến các Certificate - chính là các khóa xác thực tài khoản được lưu trữ trên cả server và client.
#### 2.2. Những giao thức bảo mật tốt hơn
- **IKEv2 (Internet Key Exchange)**
IKEv2 (Internet Key Exchange) được xếp hạng bảo mật cao trong số các giao thức hiện tại. IKEv2 sử dụng IPSec tunnelling và có nhiều lựa chọn giao thức mã hóa. IKEv2 được sử dụng với mã hóa AES-256 nên rất khó bị bẻ khóa. IKEv2 sử dụng tính năng xác thực dựa trên chứng chỉ mạnh mẽ và có thể sử dụng thuật toán HMAC để xác minh tính toàn vẹn của dữ liệu được truyền. IKEv2 hỗ trợ giao tiếp nhanh và đặc biệt mạnh mẽ trong việc duy trì phiên, ngay cả khi kết nối Internet bị gián đoạn. Windows, MacOS, iOS và Android đều hỗ trợ IKEv2. Một số triển khai mã nguồn mở cũng có sẵn.
- **SSTP (Secure Socket Tunneling Protocol)**
SSTP (Secure Socket Tunneling Protocol) là một sản phẩm của Microsoft, được hỗ trợ chủ yếu trên Windows. Khi được sử dụng với mã hóa AES và SSL, SSTP cung cấp tính năng bảo mật tốt, xét về mặt lý thuyết. Hiện tại chưa tìm thấy lỗ hổng nào của SSTP nhưng rất có thể một điểm yếu nào đó vẫn tồn tại.
- **OpenVPN**
OpenVPN là một bộ giao thức mở, cung cấp tính năng bảo mật mạnh mẽ và đã trở nên rất phổ biến. OpenVPN được phát hành lần đầu tiên vào năm 2001 theo giấy phép GPL. OpenVPN có mã nguồn mở, nên việc kiểm tra lỗ hổng được bảo đảm. Chức năng mã hóa của OpenVPN thường sử dụng thư viện OpenSSL. OpenSSL hỗ trợ nhiều thuật toán mã hóa, bao gồm AES.
- **SoftEther (Software Ethernet)**
SoftEther (Software Ethernet) là một cái tên mới, lần đầu tiên ra mắt vào năm 2014. Giống như OpenVPN, SoftEther cũng có mã nguồn mở. SoftEther hỗ trợ các giao thức mã hóa mạnh nhất, bao gồm AES-256 và RSA 4096-bit. SoftEther cung cấp tốc độ giao tiếp lớn hơn so với hầu hết các giao thức, bao gồm OpenVPN, ở một tốc độ dữ liệu nhất định. Nó không hỗ trợ hệ điều hành riêng nhưng có thể được cài đặt trên nhiều hệ điều hành, bao gồm Windows, Mac, Android, iOS, Linux và Unix.
Là một giao thức mới, SoftEther không được hỗ trợ nhiều như một số giao thức khác. SoftEther không tồn tại đủ lâu như OpenVPN, vì vậy người dùng chưa có nhiều thời gian để kiểm tra những điểm yếu có thể xuất hiện trên giao thức này. Tuy nhiên, SoftEther là một ứng cử viên nặng ký cho bất kỳ ai cần cho một giải pháp VPN.

### 3. Các mô hình triển khai VPN phổ biến
- **VPN Client to Site**
VPN loại này giúp Client có thể kết nối đến 1 Private Network từ xa thông qua 1 VPN Server. Người dùng cần có phần mềm VPN Client tương ứng với VPN Server để có thể xác thực và tạo kết nối.
VPN client to site thường được sử dụng cho các mục đích: Truy cập vào vùng mạng LAN (Internal) trong Datacenter, tạo ra kết nối an toàn.
 
- **VPN Site to Site**
Là một dạng VPN kết nối 2 hay nhiều mạng riêng với nhau thông qua đường truyền an toàn và bảo mật. Giúp các chi nhánh khác nhau trong doanh nghiệp truy cập đến ứng dụng hoặc tài nguyên nội bộ an toàn và bảo mật cao hơn.

Các ứng dụng VPN opensource phổ biến hiện nay là : OpenVPN, SoftetherVPN.
