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

     #### GIAO THỨC BẢO MẬT SSL:
     - Điểm cơ bản của SSL được thiết kế độc lập với tầng ứng dụng để đảm bảo tính bí mật, an toàn và chống giả mạo luồng thông tin qua Internet giữa hai ứng dụng bất kỳ, thí dụ như webserver và các trình duyệt khách (browsers).
     - Toàn bộ cơ chế hoạt động và hệ thống thuật toán mã hoá sử dụng trong SSL được phổ biến công khai, trừ khoá chia xẻ tạm thời (session key) được sinh ra tại thời điểm trao đổi giữa hai ứng dụng là tạo ngẫu nhiên và bí mật đối với người quan sát trên mạng máy tính.
     - Giao thức SSL dựa trên hai nhóm con giao thức là giao thức “bắt tay” (handshake protocol) và giao thức truyền dữ liệu (record protocol):
        - Giao thức bắt tay xác định các tham số giao dịch giữa hai đối tượng có nhu cầu trao đổi thông tin hoặc dữ liệu.
        - Giao thức truyền dữ liệu xác định khuôn dạng cho tiến hành mã hoá và truyền tin hai chiều giữa hai đối tượng đó.
     - Giao thức bắt tay là giao thức quan trọng nhất của SSL , được hai phía sử dụng để xác thực lẫn nhau và thương lượng để thống nhất các thuật toán xác thực MAC và mã hoá.Thủ tục này cũng trao đổi khoá bí mật dung cho mã hoá và MAC. Thủ tục bắt tay phải thực hiện trước khi trao đổi dữ liệu. SSL handshake gồm 4 giai đọan (phase):

  ```
  Giai đoạn 1 :


- ClientSSLthiết lậpmộtkếtnốiquagiao thức TCP và gửi tin nhắnClient_Hellođểbắtđầumột cái bắt tay.
- Các máy chủSSLphản ứngvới một thông điệpSever_Hello.

Thông báo của client_hello và server_hello bao gồm các trường sau đây:
· client_hello = (version, random, session id, cipher suite, compression method)
· server_hello = (version, random, session id, cipher suite,compression method)
Trong đó:
Ø Version : Phiên bản SSL
Ø Random : Số ngẫu nhiên dùng cho mục đích xác thực.
Ø session id : nhận dạng các phiên làm việc.
Ø cipher suite:tập các thuật toán mật mã mà hệ thống có khả năng hỗ trợ
Ø compression method : Thuật toán nén mà hệ thống có khả năng hổ trợ.

Giai đoạn 2 :


- Server gửi chứng chỉ Certificate của nó cho Client.
- ServerKeyExchange: chứa thông tin về Public key của Server mà Client cần để xác thực Server.
- Server yêu cầu Client gửi lại Certificate của Client bằng message Certificate_Request.
- Server_hello_done: kết thúc thương lượng phía server

Giai đoạn 3 :


- Client gửi chứng chỉ Certificate của nó cho Server.
- ClientKeyExchange: chứa thông tin về khóa của Client. Thông điệp này được mã hóa bằng chính Public key của Server. Chính sự mã hóa này bảo vệ thông tin về khóa của Client đồng thời xác thực luôn Server. Vì chỉ có Server mới có thể giải mã được thông điệp này.
- CertificateVerify : là một chữ ký dựa trên thông điệp bắt tay trước bằng cách sử dụng private key của certificate client. Chữ ký này được xác minh bằng cách sử dụng public key của certificate client. Điều này cho phép Server biết rằng client truy cập đến private key của certificate và như vậy certificate thuộc quyền sở hữu của client.


Giai đoạn 4 :

Hình 3.7: Giao thức bắt tay SSL _Giai đoạn 4
- Change_cipher_spec: cập nhật thông số mã
- Finish: kết thúc quá trình bắt tay thành công

Kết thức Giai đoạn 4 trong giao thức bắt tay SSL VPN là đã hoàn thành xong việc khởi tạo cho việc thiết lập đường hầm an toàn VPN. Sau đó thì trao đổi dữ liệu qua đường hầm
```
    
  <br>
    
  - `OpenVPN`: 
    - OpenVPN là một phần mềm mạng riêng ảo mã nguồn mở dành cho việc tạo các đường ống (tunnel) điểm-điểm được mã hóa giữa các máy tính.
    - OpenVPN cho phép các máy tính ngang hàng xác thực lẫn nhau bằng một khóa bí mật được chia sẻ từ trước, chứng chỉ khóa công khai (public key certificate), hoặc tên người dùng/mật khẩu. 
    - Toàn bộ phần mềm gồm có một file nhị phân cho cả các kết nối client và server và một hoặc nhiều file khóa tùy theo phương thức xác thực được sử dụng.
    - Các kết nối OpenVPN có thể đi qua được hầu hết mọi tường lửa và proxy : Khi truy cập các trang web HTTPS, thì đường hầm OpenVPN làm việc.Việc thiết lập đường hầm OpenVPN bị cấm là rất hiếm. 
    - Hỗ trợ UDP và TCP.
    - Chỉ cần một cổng trong tường lửa được mở là cho phép nhiều kết nối vào: Kể từ phần mềm OpenVPN 2.0, máy chủ đặc biệt này cho phép nhiều kết nốivào trên cùng một cổng TCP hoặc UDP, đồng thời vẫn sử dụng các cấu hình khác nhau cho mỗi một kết nối.
    - Hỗ trợ khả năng hoạt động cao, trong suốt cho IP động: Hai đầu đường hầm có thể sử dụng IP động và ít bị thay đổi. Nếu bị đổi IP, các phiên làm việc của Windows Terminal Server và Secure Shell (SSH) có thể chỉ bị ngưng trong vài giây và sẽ tiếp tục hoạt động bình thường.
    - Cài đặt đơn giản trên bất kỳ hệ thống nào: Đơn giản hơn nhiều so với IPsec.
    - Việc cài đặt mạng của clients có thể được điều khiển bởi sever. Sau khi hoàn thành cài đặt mạng của một đường hầm, sever có thể cho phép client ( cả Windows và Linux) sử dụng những sự cài đặt mạng khác nhau ngay lập tức.

<br>

### CÀI ĐẶT OPENVPN:
Giải pháp mạng riêng ảo sử dụng mã nguồn mở OpenVPN cho phép các nhân viên thường đi công tác xa có thể ngồi bất kì nơi đâu có kết nối internet đều có thể truy cập vào các ứng dụng, dịch vụ của hệ thống mạng nội bộ trong công ty 1 cách an toàn và đảm bảo tính toàn vẹn của dữ liệu và thông tin người dùng. Với những tính năng ưu việt OpenVPN hỗ trợ cho người quản trị dễ dàng kiểm soát được những kết nối bất kì đâu. 
- Trên Windows, OpenVPN cài đặt giống như bất kỳ chương trình khác.
- Để tự động khởi động và dừng của OpenVPN, lúc khởi động lại sẽ cần phải chạy OpenVPN như là một dịch vụ Windows điều này cũng rất đơn giản.
- Trên Linux cái đặt cũng rất đơn giản,hầu hết các bản phân phối đều có OpenVPn như một phần trong các gói hệ thống.
- Nếu sử dụng nhân của hệ điều hành linux 2.4.x hoặc cao hơn thì OpenVPN đều được tích hợp sẵn các trình điều khiển. Nếu sử dụng thấp hơn, thì có thể tải về và cài đặt TAP / TUN trình điều khiển khá dễ dàng.
- Tùy chọn pthreads. Tùy chọn này là rất quan trọng vì nó cho phép xử lý đa luồng để tạo ra một kênh điều khiển khác nhau mà trao đổi khóa được thực hiện. Thời gian rekeying mặc định là một giờ, do đó pthreads cho phép bạn loại bỏ độ trễ giờ rekeying qua một kênh riêng biệt và chuyển đổi sang các vật liệu keying mới một cách liền mạch.
- OpenVPN không được xây dựng các tính năng để xử lý cân bằng tải, nhưng nó hoàn toàn giải quyết dc dễ dàng bằng cách sử dụng iptables.
    
![image](https://user-images.githubusercontent.com/62002485/138945631-2336f0be-ff8e-4f24-a132-82616b285879.png)

![image](https://user-images.githubusercontent.com/62002485/138950207-c432dc2e-0a14-4c41-afeb-3a4c935dce61.png)

<br>

<hr>

### 1.	Định nghĩa VPN:

VPN(virtual private network) là công nghệ xây dựng hệ thống mạng riêng ảo nhằm đáp ứng nhu cầu chia sẻ thông tin, truy cập từ xa và tiết kiệm chi phí. 

VPN cho phép các máy tính truyền thông với nhau thông qua một môi trường chia sẻ như mạng Internet nhưng vẫn đảm bảo được tính riêng tư và bảo mật dữ liệu. Để cung cấp kết nối giữa các máy tính, các gói thông tin được bao bọc bằng một header có chứa những thông tin định tuyến, cho phép dữ liệu có thể gửi từ máy truyền qua môi trường mạng chia sẻ và đến được máy nhận, như truyền trên các đường ống riêng được gọi là tunnel. Để bảo đảm tính riêng tư và bảo mật trên môi trường chia sẻ này, các gói tin được mã hoá và chỉ có thể giải mã với những khóa thích hợp, ngăn ngừa trường hợp "trộm" gói tin trên đường.

### 2.	Các dạng kết nối mạng riêng ảo VPN.

- Remote Access: Đáp ứng nhu cầu truy cập dữ liệu và ứng dụng cho người dùng ở xa, bên ngoài công ty thông qua Internet.

  Ví dụ: khi người dùng muốn truy cập vào cơ sở dữ liệu hay các file server, gửi nhận email từ các mail server nội bộ của      công ty.

- Site To Site: Áp dụng cho các tổ chức có nhiều văn phòng chi nhánh, giữa các văn phòng cần trao đổi dữ liệu với nhau. 

  Ví dụ một công ty đa quốc gia có nhu cầu chia sẻ thông tin giữa các chi nhánh đặt tại Nhật Bản và Việt Nam, có thể xây dựng   một hệ thống VPN Site-to-Site kết nối hai site Việt Nam và Nhật Bản tạo một đường truyền riêng trên mạng Internet phục vụ    quá trình truyền thông an toàn, hiệu quả.


### 3.	Các giao thức sử dụng trong VPN.

#### 3.1	PPTP(Point-to-Point Tunneling Protocol)

PPTP là một phương thức của mạng riêng ảo, được phát triển bởi Microsoft kết hợp với một số công ty khác, nó sử dụng một kênh điều khiển qua giao thức TCP và đường hầm GRE để đóng gói các gói dữ liệu PPP (Point-to-Point), tạo hệ thống riêng ảo dựa trên kết nối quay số (dial-up)

**Hạn chế:**

  Khó khăn lớn nhất gắn kèm với PPTP là cơ chế  yếu kém về bảo  mật  do nó 
  dùng  mã  hóa  đồng  bộ  trong  khóa  được  xuất  phát  từ  việc  nó  sử  dụng  mã  hóa  đối xứng là cách tạo ra khóa từ     mật khẩu của người dùng. Điều này càng nguy hiểm hơn vì  mật  khẩu  thường  gửi  dưới  dạng  phơi  bày  hoàn  toàn  trong    quá  trình  xác  nhận. Giao thức tạo đường hầm kế tiếp (L2F) được phát triển nhằm cải thiện bảo mật với mục đích này. Hiện được coi là lỗi thời và không bảo mật. Đã bị bẻ khóa bởi NSA.


#### 3.2	L2TP (Layer 2 Tunneling Prototype)

L2TP (Layer 2 Tunnel Protocol) không có mã hóa các dữ liệu đi qua nó mà phải nhờ vào IPsec để mã hóa dữ liệu. Giao thức này sử dụng cổng UDP port 500 nên dữ bị tưởng lửa chặn lại nên phải trải qua thêm một công đoạn chuyển tiếp port. L2TP/IPsec đóng gói dữ liệu 2 lần nên không cho hiệu năng cao.


#### 3.3	SSTP( Secure Socket Tunneling Protocol)

SSTP (Secure Socket Tunneling Protocol) là một dạng của kết nối VPN trong Windows Vista và Windows Server 2008. SSTP sử dụng các kết nối HTTP đã được mã hóa SSL để thiết lập một kết nối VPN đến VPN gateway. SSTP là một giao thức rất an toàn vì các thông tin quan trọng của người dùng không được gửi cho tới khi có một “đường hầm” SSL an toàn được thiết lập với VPN gateway. 

#### 3.4	IPSec 

IP Security (IPSec) là một giao thức được chuẩn hoá bởi IETF từ năm 1998 nhằm mục đích nâng cấp các cơ chế mã hoá và xác thực thông tin cho chuỗi thông tin truyền đi trên mạng bằng giao thức IP. Hay nói cách khác, IPSec là sự tập hợp của các chuẩn mở được thiết lập để đảm bảo sự cẩn mật dữ liệu, đảm bảo tính toàn vẹn dữ liệu và chứng thực dữ liệu giữa các thiết bị mạng.

IPSec cung cấp một cơ cấu bảo mật ở tầng 3 (Network layer) của mô hình OSI.

IPSec được thiết kế như phần mở rộng của giao thức IP, được thực hiện thống nhất trong cả hai phiên bản IPv4 và IPv6. Đối với IPv4, việc áp dụng IPSec là một tuỳ chọn, nhưng đối với IPv6, giao thức bảo mật này được triển khai bắt buộc.

Khi hai máy tính thiết lập kết nối VPN, chúng phải đồng thuận về một tập hợp các giao thức bảo mật và thuật toán mã hóa, đồng thời trao đổi key mật mã để mở khóa và xem dữ liệu đã mã hóa.

Đây là lúc IPSec phát huy vai trò. IPSec làm việc với các VPN tunnel để thiết lập kết nối hai chiều riêng tư giữa các thiết bị. IPSec không phải là một giao thức đơn lẻ; thay vào đó, đó là một bộ giao thức và tiêu chuẩn hoàn chỉnh, hoạt động cùng nhau để giúp đảm bảo tính bảo mật, toàn vẹn và xác thực của các gói dữ liệu Internet đi qua VPN tunnel.

Đây là cách IPSec tạo một VPN tunnel bảo mật:

- IPSec xác thực dữ liệu để đảm bảo tính toàn vẹn của gói dữ liệu trong quá trình truyền tải.
- IPSec mã hóa lưu lượng truy cập Internet qua các VPN tunnel để không thể xem dữ liệu.
- IPSec bảo vệ dữ liệu khỏi các cuộc tấn công Replay Attack, có thể dẫn đến việc đăng nhập trái phép.
- IPSec cho phép trao đổi key mật mã bảo mật giữa các máy tính.
- IPSec cung cấp hai chế độ bảo mật: Tunnel và Transport.

IPSec gửi dữ liệu bằng cách sử dụng chế độ Tunnel hoặc Transport. Các chế độ này có liên quan chặt chẽ đến loại giao thức được sử dụng, AH hoặc ESP.

- Chế độ Tunnel: Trong chế độ Tunnel, toàn bộ gói tin được bảo vệ. IPSec gói gói dữ liệu trong một packet mới, mã hóa nó và thêm một IP header mới. Nó thường được sử dụng trong thiết lập VPN site-to-site. Chế độ Tunnel trong IPsec được sử dụng giữa hai router chuyên dụng, với mỗi router hoạt động như một đầu của "đường hầm" ảo thông qua mạng công cộng. Trong chế độ Tunnel, IP header ban đầu chứa đích cuối cùng của gói được mã hóa, cùng với payload gói. Để cho những router trung gian biết nơi chuyển tiếp các gói tin, IPsec thêm một IP header mới. Tại mỗi đầu của đường hầm, những router giải mã những IP header để chuyển các gói đến đích của chúng.

- Chế độ Transport: Trong chế độ Transport, IP header gốc vẫn còn và không được mã hóa. Chỉ có payload và ESP trailer được mã hóa mà thôi. Chế độ Transport thường được sử dụng trong thiết lập VPN client-to-site. Trong chế độ Transport, payload của mỗi gói được mã hóa, nhưng IP header ban đầu thì không. Do đó, các router trung gian có thể xem đích cuối cùng của mỗi gói - trừ khi sử dụng một giao thức tunnel riêng biệt (chẳng hạn như GRE).


<br>

## pfSense 
Là 1 firewall mã nguồn mở thịnh hành nhất hiện nay:
https://www.pfsense.org/download/
 
### 1.	Giới thiệu về tường lửa.

Tường lửa, firewall, là rào chắn mà một số cá nhân, tổ chức, doanh nghiệp thiết lập để ngăn chặn người dùng mạng Internet truy cập các thông tin không mong muốn hoặc/và ngăn chặn người dùng từ bên ngoài truy nhập các thông tin bảo mật nằm trong mạng nội bộ. Nói cách khác, tường lửa là một thiết bị giúp kiểm soát các truy cập giữa mạng công cộng và mạng nội bộ, để bảo đảm an toàn cho sự vận hành của mạng nội bộ.

### 2.	Giới thiệu về Pfsense.

PfSense là tường lửa mềm, tức là bạn chỉ cần một máy tính bất kì, hoặc tốt hơn là một máy chủ, rồi cài đặt pfSense là đã có ngay một tường lửa mạnh mẽ cho hệ thống mạng trong doanh nghiệp. 

Trong phân khúc tường lửa cho doanh nghiệp vừa và nhỏ, với khoảng dưới 1000 người sử dụng, pfSense được đánh giá là tường lửa nguồn mở tốt nhất hiện nay với khả năng đáp ứng lên tới hàng triệu kết nối đồng thời. 

### 3.	Tính năng của Pfsense.

#### 3.1	Alias.

Alias là một cách để ta có thể Group nhiều Port hoặc nhiều Network lại với nhau. Lợi ích của Aliases giúp ta có thể làm cho bảng Rule trở nên gọn hơn nhờ việc tạo ít Rule hơn.

#### 3.2	NAT.

NAT trên Pfsense để cho các user đi được Internet đã được tạo ra một cách tự động. Công việc NAT này là để cho ta NAT một server ra ngoài internet hay còn gọi là NAT outside.

##### 3.3	Rules.

Tạo Rules để cho phép ta quản lý traffic đi qua cổng LAN hoặc WAN của PFSENSE. Ta có thể Block, Pass hoặc Reject một traffic khi nó đi qua interface được áp dụng Rules.

#### 3.4	Traffic shaper.

Traffic shaper giúp bạn theo dõi và quản lí bang thông mạng dễ dàng và hiệu quả hơn.

Traffic shaping là phương pháp tối ưu hóa kết nối internet. Nó tăng tối đa tốc độ trong khi đảm bảo tối thiểu thời gian trễ.

Khi sử dụng những gói dữ liệu ACK dduwoj sắp xếp thứ tự ưu tiên trong đường truyền tải lên, điều này cho phép tiến trình tải về được tiếp tục với tốc độ tối đa.

#### 3.5	Firewall Schedules.

Các firewall rule có thể được sắp xếp để nó chỉ có thể hoạt động vào các hời điểm nhất định trong ngày hoặc vào những ngày nhất định cụ thể hoặc các ngày trong tuần.


#### 3.6 Virtual IPs.

Một virtual IPs có thể sử dụng bất kỳ địa chỉ IP của pfsense, đó không phải là một địa chỉ IP chính. Trong các tính huống khác nhau, mỗi trog số đó có các tính năng riêng của nó. 

### 4.	Một số dịch vụ của Pfsense.
#### 4.1	VPN.

-	OpenVPN
-	PPTP
-	L2TP
-	IPSEC

#### 4.2	DHCP server 

DHCP server chỉnh cấu hình cho mạng TCP/IP bằng cách tự động gán các địa chỉ IP cho khách hàng khi họ vào mạng.

#### 4.3	Load Balancer.

Chức năng cân bằng tải của Pfsense có những đặc điểm:

**Ưu điểm:**

-	Miễn phí
-	Có khả năng bổ sung thêm tính năng bằng gói dịch vụ cộng thêm
-	Dễ cài đặt, cấu hình

**Hạn chế:**

-	Phải trang bị thêm modem nếu không có sẵn
-	Không được hỗ trò từ nhà sản xuất như các thiết bị cân bằng tải khác
-	Vẫn chưa có tính năng lọc URL như các thiết bị thương mại.
-	Đòi hỏi người sử dụng phải có kiến thức cơ bản về mạng để cấu hình.
 
 <br>

# TRIỂN KHAI MÔ HÌNH CLIENT TO SITE:

![image](https://user-images.githubusercontent.com/62002485/139943868-82567ee1-5baf-4704-9160-61bd4764635e.png)

![image](https://user-images.githubusercontent.com/62002485/139863542-67d098cb-b089-4647-837f-00c6ed6f3204.png)

<i>Hiểu nôm na :D Sau khi thêm user vào openvpn server Client To Site thì file cấu hình có ip cấp cho client trong mạng tunnel, khi kết nối nhập đúng user pass thì kết nối đc đến vpn server và sau đó vpn server móc từ pfsense card WAN, tiến hành tạo đường hầm kết nối cho client vào mạng cục bộ phía trong pfsense.</i>

![image](https://user-images.githubusercontent.com/62002485/139921266-8adeb229-9336-441b-b67e-b423dc9c59fc.png)

- Network Adapter
  - pfsense: ![image](https://user-images.githubusercontent.com/62002485/139945436-fd78bbfc-95b2-404c-b35f-828862921468.png)

  - Win Server: ![image](https://user-images.githubusercontent.com/62002485/139945540-764d490a-72d2-401d-9435-ace75a64a05c.png)

  - Win 10: ![image](https://user-images.githubusercontent.com/62002485/139945590-18717bee-c35c-447f-99b0-633d895bc0ed.png)


Mặc định khi push lên nếu có 2 card mạng thì pfsense sẽ xem card sử dụng DHCP như là card WAN.

### Thực hiện cấu hình pfsense:

IP Card WAN sẽ cùng lớp mạng máy thật bên ngoài.

![image](https://user-images.githubusercontent.com/62002485/139860171-66e0f22f-672e-4a1e-a316-076b18c29f89.png)

- Cấu hình chỉ định card mạng WAN LAN cho pfsense:

![image](https://user-images.githubusercontent.com/62002485/139852709-8c540b90-bf01-4988-a292-c68594664ef8.png)

![image](https://user-images.githubusercontent.com/62002485/139852677-413fddbc-9975-4e93-8731-5242f664ab3a.png)

- Setup IP address cho các interface pfsense:

![image](https://user-images.githubusercontent.com/62002485/139853351-7fff8340-724b-4b6d-b003-7d7811887c98.png)

![image](https://user-images.githubusercontent.com/62002485/139853297-574f67c4-b1f0-4249-aa08-905c52ab1ed3.png)

![image](https://user-images.githubusercontent.com/62002485/139854105-c6a269d5-1943-4b66-8779-41db2c20d55d.png)

![image](https://user-images.githubusercontent.com/62002485/139854424-faf63510-22fa-473e-bf2f-e0825cac44f4.png)

![image](https://user-images.githubusercontent.com/62002485/139856166-865048ad-0a16-469b-9959-a35a9b511b52.png)

- Cập nhật IP cho Windows Server 2019 (Mạng cục bộ):

![image](https://user-images.githubusercontent.com/62002485/139854930-cfb2c21e-1ed3-4042-a8f2-b58031404bcc.png)

### Vào trang chủ pfsense để cài đặt:

<i> **Note: Update new IP </i> 

<br>

![image](https://user-images.githubusercontent.com/62002485/139862227-ad13e385-d93e-4f76-a728-ea29c7af7ada.png)


![image](https://user-images.githubusercontent.com/62002485/139855304-072659e8-dea7-4f38-815a-9d736fc7a38e.png)

- Tạo CA:

![image](https://user-images.githubusercontent.com/62002485/139848115-41c615d4-11a3-481a-98d3-61163d48fcaa.png)

- Tạo server Certificate:

![image](https://user-images.githubusercontent.com/62002485/139848388-3553cec9-abaa-44b5-9ebb-b2a5e6d2278d.png)

- Tạo server VPN:

![image](https://user-images.githubusercontent.com/62002485/139847768-1bcced8c-6277-4e1f-998f-15d8227a4781.png)

![image](https://user-images.githubusercontent.com/62002485/139908730-65f310fc-4736-4923-8dd7-5570019858f4.png)

![image](https://user-images.githubusercontent.com/62002485/139849849-cecdefd9-83d3-4cbc-8a4f-83e6bfaa3dd3.png)

VD: push “route 172.16.0.0 255.255.255.0” (lệnh này sẽ đẩy route mạng 172.16.0.0 đến Client, hay còn gọi là Lan Routing trong Windows Server, giúp cho VPN Client thấy được mạng bên trong của công ty)

![image](https://user-images.githubusercontent.com/62002485/139849917-5a1e8cf8-5e1c-43cf-9255-61a98df64a9e.png)

- Kiểm tra server đã tạo ở tag export client:

![image](https://user-images.githubusercontent.com/62002485/139848922-be3bafd5-57f7-4127-a71b-d01a1c00ff0f.png)

- Tạo user sử dụng certificate đã tạo:

![image](https://user-images.githubusercontent.com/62002485/139849109-232402f9-1a88-42db-9ae3-7cef6bf8bfec.png)

![image](https://user-images.githubusercontent.com/62002485/139910486-b7ffde4d-6d7f-41ed-9862-40a7d75991f4.png)

![image](https://user-images.githubusercontent.com/62002485/139910557-6ea50cce-4585-49e7-b609-09e366533353.png)

- Vào tag Client Export, với option server Client To Site vừa tạo có sự xuất hiện của user vpn01, tiến hành tải file cấu hình về máy client:

![image](https://user-images.githubusercontent.com/62002485/139915732-eb319a32-2ec5-4286-93d5-e170f5daf0c8.png)

<i>**Ngoài cách cài VM Tool để kéo thả file, vì đã biết ip mặt ngoài WAN pfsense nên có thể thêm làm như sau: thêm Rules WAN, giữ tất cả giá trị theo mặc định, và chọn protocol là `Any`. Tải xong cần disable Rules.</i>

- Chạy file cấu hình vừa tải được để `cài OpenVPN và import cấu hình đã cài đặt trên pfsense xuống`. (Win10 cần run as admin)
- Thông thường tạo VPN theo port, hệ thống pfsense tự động tạo phần NAT để móc vào.
- Vào Firewall -> NAT để check:
![image](https://user-images.githubusercontent.com/62002485/139917494-1c8564de-0150-4260-ab5f-42fdd748e0cc.png)

- Tiến hành connect:

![image](https://user-images.githubusercontent.com/62002485/139917844-ebedbb43-cc1b-4815-bb1a-a65722ae0c60.png)


![image](https://user-images.githubusercontent.com/62002485/143025020-a753a5dd-583a-4f28-ac6b-6ba83c92f2e3.png)


- Cần xem thêm card WAN đã tạo đường vpn ở đâu port nào thì ta sẽ tạo rules ngay đó trên card WAN.
Phải mở Rules để port 600069 trên card WAN của pfsense mới đc mở và chúng ta có thể móc về.

![image](https://user-images.githubusercontent.com/62002485/139922125-2a404b19-8d20-431a-8533-2acbaed81b99.png)


- Cần add thêm network port của VPN(interface VPN) và thêm rules với destination là alias mặt ngoài pfsense (hoặc any :v) cho interface đó:

![image](https://user-images.githubusercontent.com/62002485/139924628-6940c2d4-f4f2-403d-9220-b6b3eb32bc5d.png)

![image](https://user-images.githubusercontent.com/62002485/139924672-0af4be20-f38f-4c57-b560-e62b605d90d0.png)

- Add thêm Rules LAN any 

- Tắt firewall trên máy client và máy local công ty.

[Video](https://www.youtube.com/watch?v=UxjqHRUEIz8)

<br>

# TRIỂN KHAI MÔ HÌNH OpenVPN site- to- site trên Pfsense

### Mô hình triển khai:

<img src ="http://i.imgur.com/0rQ5vzB.png">

### Yêu cầu:
-	2 máy cài đặt pfsense.
-	2 máy client kết nối với hai máy Pfsense.

### Cài đặt:

#### Site A (pfsense0)

Cấu hình trên site A với vai trò như một server

<img src="http://i.imgur.com/JsSPA0z.png">

**Chú ý:** Server mode chọn **Peer to Peer (Shared Key)**

<img src="http://i.imgur.com/EcZSdG8.png">
<img src="http://i.imgur.com/Nsw4561.png">

Sau đó các bạn chon **save**

<img src="http://i.imgur.com/MMzkjZq.png ">

Sau đó chọn edit -> copy Shared Key sang site B với vai trò như một client.
<img src ="http://i.imgur.com/SZwEeNg.png ">

Tạo rule trong WAN

<img src ="http://i.imgur.com/G0gDUuE.png ">
<img src ="http://i.imgur.com/mt7KmE7.png">

Tạo rule trong OpenVPN

<img src ="http://i.imgur.com/7raFwJf.png ">
<img src ="http://i.imgur.com/EcK4Wu8.png ">

#### Site B (Pfsense1)

<img src ="http://i.imgur.com/ZiZxFrm.png">

**Chú ý:** Shared Key bỏ tích và copy Shared Key từ site A sang.

<img src ="http://i.imgur.com/fTGCwuq.png">
<img src ="http://i.imgur.com/qujiDea.png ">


Kết quả như hình dưới là bạn đã cấu hình thành công:

Site A

<img src ="http://i.imgur.com/QvRg2Kl.png">

Site B

<img src="http://i.imgur.com/QOTLmcc.png">

<br>

<hr>

![image](https://user-images.githubusercontent.com/62002485/143103303-f7194360-a219-4864-a59c-a5f07fbd1075.png)
 
- Tạo server vpn:

![image](https://user-images.githubusercontent.com/62002485/143103462-bad5b21c-ad93-4bf6-9ed2-d597ecb129c0.png)

![image](https://user-images.githubusercontent.com/62002485/143103600-66110465-c89c-4df1-a804-794952d0c5c2.png)

![image](https://user-images.githubusercontent.com/62002485/143103704-1ace8c69-6786-4678-8b78-35a080b42763.png)

- Add rules WAN, openvpn:

![image](https://user-images.githubusercontent.com/62002485/143103949-b68b8cde-99f1-4ec4-a5b6-355484bb0313.png)

![image](https://user-images.githubusercontent.com/62002485/143104027-f32f9b90-4f5e-4fb0-8e8d-c58e905c6ede.png)

![image](https://user-images.githubusercontent.com/62002485/143104085-02c56c20-c647-4540-bf53-b5c6e0ea8518.png)

![image](https://user-images.githubusercontent.com/62002485/143104163-dfea75f3-6217-419a-af12-2dde7cf14e97.png)

![image](https://user-images.githubusercontent.com/62002485/143104252-30bf8692-3ee1-4fd2-80f8-afd44d6bc6c3.png)

![image](https://user-images.githubusercontent.com/62002485/143104425-21a77931-5fcc-4b78-ac03-16fd21eb9534.png)

![image](https://user-images.githubusercontent.com/62002485/143104508-12d3fe33-f199-45c0-b1bc-d18df4ce0cf1.png)

![image](https://user-images.githubusercontent.com/62002485/143104595-253f20a5-17b5-4e1f-bad0-557d573edf59.png)

- Tạo client:

![image](https://user-images.githubusercontent.com/62002485/143104852-e4fd4b6b-d518-4f24-99b4-319065c53a37.png)

![image](https://user-images.githubusercontent.com/62002485/143104922-5f8673d9-0bfb-4d46-8133-65ea31be472d.png)

![image](https://user-images.githubusercontent.com/62002485/143104993-a9d817a7-dd4a-4eb5-b6af-e18ebcc442a0.png)

![image](https://user-images.githubusercontent.com/62002485/143105113-ef4055e0-1537-4f24-96cf-a881f8960afd.png)

![image](https://user-images.githubusercontent.com/62002485/143105295-a0594912-e777-4b24-aed6-29fcf46699fb.png)

- Add rules:

![image](https://user-images.githubusercontent.com/62002485/143105576-33516647-3969-41c2-8d3b-2654432d0a76.png)

![image](https://user-images.githubusercontent.com/62002485/143105685-90585472-dad7-4947-897c-a6ddfa561a3c.png)

![image](https://user-images.githubusercontent.com/62002485/143105771-93a03133-4101-40bf-b238-f161edf875d7.png)

[Video](https://www.youtube.com/watch?v=-8xt7LUtYH4)













 






