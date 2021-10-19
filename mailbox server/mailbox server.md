**Zimbra Store (Zimbra server)**

**-** MTA sv nhận thư qua SMTP và định tuyến mỗi thư đến mailbox sv thích hợp, sử dụng LMTP. Khi mỗi tin nhắn đến, Zimbra sv lập một bản kê khai để có chỉ mục Lucene.

- Gói lưu trữ ZB cài đặt các thành phần cho mailbox server, bao gồm Jetty, đây là bộ chứa servlet *Java Servlets là các chương trình chạy trên một Web server hoặc một Application server và thực hiện như là **một tầng trung gian** giữa một Yêu cầu từ một trình duyệt web hoặc HTTP client với các Database hoặc các ứng dụng trên HTTP server*mà phần mềm Zimbra chạy trong đó. Trong ZCS, thùng chứa servlet này được gọi là mailbox.
- Mỗi tài khoản được cấu hình trên mailbox server và tài khoản này được liên kết với mailbox có chứa tất cả các thư và tập tin đính kèm cho tài khoản thư đó. Mailbox server bao gồm các thành phần sau:
- The mailbox server includes the following volumes:

- Message Store. Mail message files are in opt/zimbra/store

- Data Store. The MySQL database files are in opt/zimbra/db

- Index Store. Index files are in opt/zimbra/index

- Backup Area. Sao lưu từng bước và toàn bộ in opt/zimbra/backup

- Log files. Each component in the Zimbra Collaboration Suite has log files. Local logs are in /opt/zimbra/log

`            `+  Message store: Tất cả thư email được lưu trữ ở định dạng MIME ( ***Multipurpose Internet Mail Extensions** là một [chuẩn Internet](https://vi.wikipedia.org/w/index.php?title=Chu%E1%BA%A9n_Internet&action=edit&redlink=1 "Chuẩn Internet (trang chưa được viết)") về định dạng cho [thư điện tử](https://vi.wikipedia.org/wiki/Th%C6%B0_%C4%91i%E1%BB%87n_t%E1%BB%AD "Thư điện tử")* ) trong Message store. Một thông báo được gửi tới nhiều người nhận có tài khoản trên một mail  sv chỉ được lưu trữ một lần trong hệ thống tập tin. 

MIME :Multipurpose Internet Mail Extensions (MIME) là một tiêu chuẩn Internet giúp mở rộng khả năng giới hạn của email bằng cách cho phép chèn hình ảnh, âm thanh và văn bản trong một tin nhắn

- *Hỗ trợ nhiều tập tin đính kèm trong một tin nhắn duy nhất*
- *Hỗ trợ cho các ký tự không phải ASCII*
- *Hỗ trợ bố cục, phông chữ và màu sắc được phân loại dưới dạng văn bản phong phú.*
- *Hỗ trợ các tập tin đính kèm có thể chứa các file thực thi, âm thanh, hình ảnh và các file video, vv*
- *Hỗ trợ cho chiều dài tin nhắn không giới hạn.*

Each mailbox has a dedicated directory named after its internal Zimbra mailbox ID.

***Note:** Mailbox IDs are unique per server, not system-wide*

- **Single-Copy Message Storage** :Lưu trữ bản sao đơn cho phép các thư có nhiều người nhận được lưu trữ chỉ một lần trong hệ thống tệp tin.
- **Quản lý lưu trữ theo cấp bậc**: Quản lý Lưu trữ Hierarchical (HSM) cho phép bạn định cấu hình dung lượng lưu trữ cho các thư cũ. Để quản lý tài nguyên lưu trữ email của bạn, bạn có thể thực hiện chính sách HSM khác cho mỗi mailbox sv. Các thư và tệp đính kèm được di chuyển từ vùng chính sang vùng thứ cấp(phụ) hiện tại, dựa trên độ tuổi của thư. Các tin nhắn vẫn có thể truy cập.

`        `+Data store: Kho dữ liệu là một cơ sở dữ liệu MySQL, trong đó ID mailbox nội bộ được liên kết với các tài khoản người dùng. Các nhận dạng chính trong cơ sở dữ liệu ZCS là ID hộp thư, thay vì tên người dùng hoặc tên tài khoản. Lưu trữ dữ liệu ID mailbox đến tài khoản OpenLDAP của người dùng. Cơ sở dữ liệu này chứa tập hợp các định nghĩa thẻ, thư mục, lịch biểu lịch và danh bạ của mỗi người dùng, cũng như trạng thái của mỗi thư - đọc, chưa đọc, các thẻ liên quan đến tin nhắn và thư mục nằm trong thư.

Các tập tin cơ sở dữ liệu MySQL được lưu ở **opt / zimbra / db**

` `**The Data Store contains:**

- Mailbox-account mapping :Bộ nhận dạng chính trong cơ sở dữ liệu Zimbra là mailbox ID, chứ không phải là tên người dùng hoặc tên tài khoản. MailboxID là duy nhất trong một Single Mail SV. (mỗi tài khoản mail có một mailbox ID riêng trên Data store) Data store mô tả mail ID Zimbra cho tài khoản OpenLDAP của người dùng.
- Mỗi tập hợp các định nghĩa thẻ, thư mục và danh bạ, lịch hẹn lịch, sổ ghi chép tác vụ và các quy tắc lọc của người dùng.
- Thông tin về mỗi thư, bao gồm cả việc nó được đọc hay chưa đọc và những thẻ nào được liên kết.

**Backup**

Zimbra bao gồm một trình quản lý sao lưu có cấu hình, nằm trên mỗi Zimbra SV, thực hiện cả chức năng sao lưu và phục hồi. Bạn không phải dừng lại Zimbra SVđể chạy quá trình sao lưu. Trình quản lý sao lưu có thể được sử dụng để khôi phục một người dùng, thay vì phải khôi phục lại toàn bộ hệ thống trong trường hợp hộp thư của một người dùng bị hỏng

**Redo Log**

- Mỗi Mailbox Zimbra SV tạo ra các redo log, nơicó chứa các giao dịch hiện tại ,được xử lý bởi message store server kể từ lần sao lưu cuối cùng.
- Khi phục hồi máy chủ, sau khi các tập tin sao lưu được phục hồi đầy đủ, bất kỳ redo log nào trong kho lưu trữ và làm lại làm lại đăng nhập sử dụng được replayed để đưa hệ thống đến điểm trước khi thất bại.
- Khi kích thước redo log đạt tới 100MB, redo log hiện tại được cuộn đưa tới thư mục lưu trữ(archive directory). Tại thời điểm đó, máy chủ bắt đầu đăng nhập làm lại mới. Tất cả các giao dịch không cam kết từ redo log lần trước được bảo toàn. Trong trường hợp tai nạn, khi máy chủ khởi động lại, đăng nhập làm lại hiện tại được đọc để áp dụng lại bất kỳ giao dịch không cam kết nào.???
- Khi một bản sao lưu gia tăng được chạy, các bản ghi redo được chuyển từ kho lưu trữ sang thư mục sao lưu.

**Log**

- Triển khai Zimbra bao gồm các thành phần khác của bên thứ ba với một hoặc nhiều Mailbox SV Zimbra. Mỗi thành phần có thể tạo ra bản ghi output của chính nó.
- Thông báo zimbra log được lược chọn, tạo ra SNMP traps, thứ bạn có thể chụp bằng bất kỳ phần mềm giám sát SNMP nào.

*Công cụ theo dõi SNMP*

Zimbra sử dụng swatch để xem sản lượng syslog để tạo ra các bẫy SNMP

Bạn có thể thực hiện phần mềm theo dõi máy chủ để theo dõi các bản ghi hệ thống, CPU và cách sử dụng đĩa, và các thông tin thời gian chạy khác.

*Cấu hình SNMP*

- Zimbra bao gồm gói cài đặt với giám sát SNMP. Gói này nên được chạy trên mọi máy chủ (Zimbra, OpenLDAP và Postfix) là một phần của cấu hình Zimbra.

Cấu hình SNMP duy nhất là máy chủ đích mà cần gửi bẫy.

*Lỗi khi tạo bẫy SNMP*

- Thông báo lỗi ZCS tạo ra các bẫy SNMP khi một dịch vụ bị dừng hoặc được bắt đầu. Bạn có thể nắm bắt những thông báo này bằng phần mềm giám sát SNMP của bên thứ ba và trực tiếp các tin nhắn đã chọn vào máy phát trang hoặc hệ thống cảnh báo khác

.đọc thêm về file log mailbox tại <https://wiki.zimbra.com/wiki/Using_log4j_to_Configure_mailboxd_Logging>

`       `+ Index store: Chỉ số và công nghệ tìm kiếm được cung cấp thông qua Lucene (<https://lucene.apache.org/core/3_5_0/fileformats.html>)

*Lucene là thư viện tìm kiếm dựa trên java đơn giản nhưng mạnh mẽ. Nó có thể được sử dụng trong bất kỳ ứng dụng nào để thêm khả năng tìm kiếm vào nó. Lucene là dự án nguồn mở. Đó là thư viện có khả năng mở rộng và hiệu suất cao được sử dụng để chỉ mục và tìm kiếm hầu như bất kỳ loại văn bản nào. Thư viện Lucene cung cấp các hoạt động cốt lõi được yêu cầu bởi bất kỳ ứng dụng tìm kiếm nào. Lập chỉ mục và tìm kiếm*

Mỗi email và tập tin đính kèm được tự động  ghi vào mục lục(*lập lịch trình một chủ đề để lưu trữ thông tin*) khi tin nhắn đến. Một file mục lục được liên kết vớii 1 tài khoản. Quá trình tokenizing và lập chỉ mục không thể cấu hình bởi người dùng hoặc administrator.Các file index đc lưu trong **opt/zimbra/index.**

- **Quá trình:**
- ZB MTA định tuyến mail đến đến ZCS mailbox sv, cái mà chứa tài khoản người dùng.
- Mailbox sv phân tích thông điệp bao gồm tiêu đề, phần thân và tất cả các tập tin đính kèm có thể đọc được (*như các tệp PDF hoặc các tài liệu Microsoft Word*) nhằm tokenize các từ. 
- Máy chủ hộp thư chuyển thông tin tokenized đến Lucene để tạo các file mục lục
- Tokenization là phương pháp lập chỉ mục cho mỗi từ. Một số mẫu phổ biến nhất, chẳng hạn như số điện thoại, địa chỉ email và tên miền được mã hoá như thể hiện trong hình Tokenization Thông báo

