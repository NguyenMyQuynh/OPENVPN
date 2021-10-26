# OPEN VPN

## VPN
- Nhu cầu ngày càng tăng về việc `truyền tải dữ liệu an toàn` trong các tổ chức dẫn đến sự bùng nổ thị trường các giải pháp mạng riêng ảo VPN (Virtual Private Network).
- Về căn bản, mỗi VPN là một mạng riêng rẽ sử dụng một mạng chung (thường là internet) để kết nối cùng với các site (các mạng riêng lẻ) hay nhiều người sử dụng từ xa.
- Để có thể gửi và nhận dữ liệu thông qua mạng công cộng mà vẫn bảo đảm tính an tòan và bảo mật VPN cung cấp các cơ chế mã hóa dữ liệu trên đường truyền tạo ra một đường ống bảo mật giữa nơi nhận và nơi gửi (Tunnel)
- Để có thể tạo ra một đường ống bảo mật đó, dữ liệu phải được mã hóa hay che giấu đi chỉ cung cấp phần đầu gói dữ liệu (header) là thông tin về đường đi 

<br>

### CÁC THÀNH PHẦN CẦN THIẾT ĐỂ TẠO KẾT NỐI VPN
  - `User Authentication`: cung cấp cơ chế chứng thực người dùng, chỉ cho phép người dùng hợp lệ kết nối và truy cập hệ thống VPN.
  - `Address Management`: cung cấp địa chỉ IP hợp lệ cho người dùng sau khi gia nhập hệ thống VPN để có thể truy cập tài nguyên trên mạng nội bộ
  - `Data Encryption`: cung cấp giải pháp mã hoá dữ liệu trong quá trình truyền nhằm bảo đảm tính riêng tư và toàn vẹn dữ liệu
  - `Key Management`: cung cấp giải pháp quản lý các khoá dùng cho quá trình mã hoá và giải mã dữ liệu

<br>

### CÁC LOẠI VPN:
  - `Client to Side`: Loại kết nối này dựa trên kiến trúc Client/Server và nó hoạt động như sau:
 ``` 
(1). VPN client muốn truy cập vào mạng của cơ quan trước hết phải kết nối vào internet
(2). VPN client khởi tạo một kết nối VPN đến VPN server của cơ quan. Kết nối này được tạo ra nhờ một phần mềm VPN đã được cài đặt trên máy client.
(3). VPN server sẽ kiểm tra và xác nhận kết nối. Nếu hợp lệ, kết nối sẽ được thiết lập.
(4). Một khi kết nối đã được thiết lập, VPN client có thể truyền thông với hệ thống mạng nội bộ của cơ quan thông qua môi trường internet như là một host nội bộ
```
  - `Site to Site`: Việc sử dụng mật mã dành cho nhiều người để kết nối nhiều điểm cố định với nhau thông qua một mạng công cộng như Internet.
    - Intranet VPN : Áp dụng trong trường hợp công ty có một hoăc vài địa điểm từ xa ,mỗi địa điểm đều có mạng cục bộ LAN .Khi đó, họ có thể tạo ra một VPN intranet (VPN nội bộ) thông qua môi trường internet để nối mạng cục bộ vào một mạng riêng duy nhât .
    - Extranet VPN : Khi một công ty có mối quan hệ mật thiết với một công ty khác (ví dụ như đối tác cung cấp, khách hàng...), họ có thể xây dựng một VPN extranet (VPN mở rộng) kết nối LAN với LAN để nhiều tổ chức khác nhau có thể làm việc trên một môi trường chung để chia sẻ tài nguyên.
  
 <br>
 
 ### CÁC GIAO THỨC PHỔ BIẾN DÙNG CHO VPN:
 - Giao thức được thực hiện trên OSI lớp 3: `IPsec`
 
 IPSec là sự tập hợp của các chuẩn mở được thiết lập để đảm bảo sự cẩn mật dữ liệu, đảm bảo tính toàn vẹn dữ liệu và chứng thực dữ liệu giữa các thiết bị mạng. Đối với IPv4, việc áp dụng IPSec là một tuỳ chọn, nhưng đối với IPv6, giao thức bảo mật này được triển khai bắt buộc.
 
 Transport mode cung cấp cơ chế bảo vệ cho dữ liệu của các lớp cao hơn (TCP, UDP hoặc ICMP). Trong Transport mode, phần IPSec header được chèn vào giữa phần IP header và phần header của giao thức tầng trên. Chế độ transport này có thuận lợi là chỉ thêm vào vài bytes cho mỗi packets và nó cũng cho phép các thiết bị trên mạng thấy được địa chỉ đích cuối cùng của gói.
 
 Tunnel mode bảo vệ toàn bộ gói dữ liệu. Toàn bộ gói dữ liệu IP được đóng gói trong một gói dữ liệu IP khác và một IPSec header được chèn vào giữa phần đầu nguyên bản và phần đầu mới của IP. Chế độ này cho phép những thiết bị mạng, chẳng hạn như router, hoạt động như một IPSec proxy thực hiện chức năng mã hóa thay cho host. Router nguồn sẽ mã hóa các packets và chuyển chúng dọc theo tunnel. Router đích sẽ giải mã gói IP ban đầu và chuyển nó về hệ thống cuối. Vì vậy header mới sẽ có địa chỉ nguồn chính là gateway.
 
 Với tunnel hoạt động giữa hai security gateway, địa chỉ nguồn và đích có thể được mã hóa. Tunnel mode được dùng khi một trong hai đầu của kết nối IPSec là security gateway và địa chỉ đích thật sự phía sau các gateway không có hỗ trợ IPSec
 
 - Các giao thức được thực hiện trên OSI lớp 4: Có thể thiết lập các đường hầm VPN bằng cách sử dụng chỉ ở các lớp ứng dụng. Secure Sockets Layer (SSL) vàTransport Layer Security(TLS)
<br>

### BẢO MẬT TRONG VPN:
- Tường lửa (firewall): là rào chắn vững chắc giữa mạng riêng và Internet. Bạn có thể thiết lập các tường lửa để hạn chế số lượng cổng mở, loại gói tin và giao thức được chuyển qua. 
- Mật mã riêng (Symmetric-Key Encryption): Mỗi máy tính đều có một mã bí mật để mã hóa gói tin trước khi gửi tới máy tính khác trong mạng. 
- Mật mã chung (Public-Key Encryption): kết hợp mã riêng và một mã công khai. Mã riêng này chỉ có máy của bạn nhận biết, còn mã công khai thì do máy của bạn cấp cho bất kỳ máy nào muốn liên hệ (một cách an toàn) với nó .Để giải mã một thông điệp, máy tính phải dùng mã chung được máy tính nguồn cung cấp, đồng thời cũng cần đến mã riêng của nó nữa.
- Giao thức bảo mật: giao thức IPSec cung cấp những tính năng an toàn cao như các thuật toán mã hóa mạnh, quá trình thẩm định quyền đăng nhập toàn diện.
Ngoài ra ta còn có thể sử dụng máy chủ AAA. AAA là viết tắt của ba chữ Authentication (xác thực), Authorization (cấp quyền) và Accounting (tính cước). Các máy chủ này được dùng để đảm bảo truy cập an toàn hơn. Khi yêu cầu thiết lập một kết nối được gửi tới từ máy khách, nó sẽ phải qua máy chủ AAA để kiểm tra Các thông tin về những hoạt động của người sử dụng là hết sức cần thiết để theo dõi vì mục đích an toàn

<br>

### CÁC GIẢI PHÁP VPN THÔNG DỤNG:
  - `IPSec VPN`: 
  
    - IPSec là một giao thức mạng chuyên về bảo mật, hoạt động ở lớp mạng, thường được kết hợp với VPN, truyền tải dữ liệu an toàn và bảo mật giữa hai thực thể.
    - Trong IPSec tất cả các nghi thức lớp trên lớp mạng (từ lớp 4) như TCP, UDP, SNMP, HTTP, POP, SMTP,…đều được mã hóa một khi kênh IPSec được thiết lập. 
    - Client và server đều phải cấu hình IPSec thích hợp( chính sách an ninh (security policy), giải thuật mã hóa (encryption algorithm), kiểu xác thực (authentication method))
    
  - `SSL VPN`
    - SSL VPN tạo kết nối giữa người dùng từ xa với máy chủ trong mạng chứa tài nguyên mạng công ty thông qua giao thức HTTPS ở lớp ứng dụng thay vì tạo “đường hầm” ở lớp mạng như giải pháp IPSec.
    -  Người dùng ở xa chỉ cần sử dụng một trình duyệt web để tạo kết nối vào máy chủ trong mạng, người quản trị không cần phải cài đặt phần mềm và cấu hình bảo mật cho các máy client như đối với IPSec.
    
  - `OpenVPN`
    - OpenVPN là một phần mềm mạng riêng ảo mã nguồn mở dành cho việc tạo các đường ống (tunnel) điểm-điểm được mã hóa giữa các máy tính.
    - OpenVPN cho phép các máy tính ngang hàng xác thực lẫn nhau bằng một khóa bí mật được chia sẻ từ trước, chứng chỉ khóa công khai (public key certificate), hoặc tên người dùng/mật khẩu. 
    - Toàn bộ phần mềm gồm có một file nhị phân cho cả các kết nối client và server và một hoặc nhiều file khóa tùy theo phương thức xác thực được sử dụng.
    
