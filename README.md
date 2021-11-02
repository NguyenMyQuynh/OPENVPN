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

# TRIỂN KHAI MÔ HÌNH CLIENT TO SITE:

![image](https://user-images.githubusercontent.com/62002485/139847572-4fca99aa-ef89-4ea1-808c-3fab1ef15170.png)

## pfSense 
Là 1 firewall mã nguồn mở thịnh hành nhất hiện nay:
https://www.pfsense.org/download/

Mặc định khi push lên nếu có 2 card mạng thì pfsense sẽ xem card sử dụng DHCP như là card WAN.

### Thực hiện cấu hình pfsense:

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

- Vào trang chủ pfsense để cài đặt:

![image](https://user-images.githubusercontent.com/62002485/139855304-072659e8-dea7-4f38-815a-9d736fc7a38e.png)

- Tạo CA:

![image](https://user-images.githubusercontent.com/62002485/139848115-41c615d4-11a3-481a-98d3-61163d48fcaa.png)

- Tạo server Certificate:

![image](https://user-images.githubusercontent.com/62002485/139848388-3553cec9-abaa-44b5-9ebb-b2a5e6d2278d.png)

- Tạo server VPN:

![image](https://user-images.githubusercontent.com/62002485/139847768-1bcced8c-6277-4e1f-998f-15d8227a4781.png)

![image](https://user-images.githubusercontent.com/62002485/139849849-cecdefd9-83d3-4cbc-8a4f-83e6bfaa3dd3.png)

![image](https://user-images.githubusercontent.com/62002485/139849917-5a1e8cf8-5e1c-43cf-9255-61a98df64a9e.png)

- Kiểm tra server đã tạo ở tag export client:

![image](https://user-images.githubusercontent.com/62002485/139848922-be3bafd5-57f7-4127-a71b-d01a1c00ff0f.png)

- Tạo user sử dụng certificate đã tạo:

![image](https://user-images.githubusercontent.com/62002485/139849109-232402f9-1a88-42db-9ae3-7cef6bf8bfec.png)





