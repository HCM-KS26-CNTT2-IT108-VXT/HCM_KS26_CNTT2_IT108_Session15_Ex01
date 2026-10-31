# BÀI 1: HỆ THỐNG QUẢN LÝ TÀI LIỆU DỰ ÁN DOANH NGHIỆP

**Dự án:** Số hóa Bảo tàng PTIT  
**Sinh viên thực hiện:** Võ Xuân Thịnh  
**Mã sinh viên:** N26DTCN032  
**Chủ đề:** Hybrid Workflow và Version History

\---

## I. PHÂN TÍCH VẤN ĐỀ

### 1\. Thực trạng

Trong dự án Số hóa Bảo tàng PTIT, bạn A được giao nhiệm vụ thiết kế mô hình 3D các hiện vật. Tuy nhiên, bạn A chỉ lưu trữ dữ liệu trên ổ cứng máy tính cá nhân và gửi file cho các thành viên thông qua Zalo.

Cách làm này tồn tại một số rủi ro:

* **Hỏng thiết bị:** Khi ổ cứng gặp lỗi Bad Sector, dữ liệu có thể bị hỏng hoặc mất hoàn toàn.
* **Không có bản sao lưu:** File chỉ tồn tại trên một thiết bị nên khó khôi phục khi xảy ra sự cố.
* **Hết hạn dữ liệu:** File gửi qua Zalo có thể hết hạn tải xuống.
* **Khó quản lý phiên bản:** Các thành viên không biết đâu là bản thiết kế mới nhất hoặc bản ổn định nhất.

### 2\. Giải pháp đề xuất

Sử dụng mô hình Hybrid Workflow kết hợp giữa Local Storage và Cloud Storage.

* **Local Storage:** Lưu file trực tiếp trên ổ SSD của máy tính để thuận tiện cho việc thiết kế và chỉnh sửa.
* **Cloud Storage:** Sử dụng OneDrive hoặc Google Drive để tự động đồng bộ và lưu trữ bản sao trực tuyến.
* **Version History:** Lưu lại lịch sử chỉnh sửa để có thể khôi phục những phiên bản trước đó khi file bị lỗi.

Giải pháp này giúp hạn chế nguy cơ mất dữ liệu và hỗ trợ các thành viên làm việc nhóm hiệu quả hơn.

\---

## II. BÁO CÁO PHÂN TÍCH QUY TRÌNH HYBRID WORKFLOW

### 1\. Sơ đồ luồng dữ liệu từ Local SSD lên Cloud

Quy trình hoạt động được thiết kế như sau:

**Bước 1:** Designer mở file thiết kế 3D trên máy tính.

**Bước 2:** Khi nhấn Ctrl + S, phần mềm lưu dữ liệu vào Local SSD.

**Bước 3:** Phần mềm đồng bộ như OneDrive phát hiện file vừa thay đổi.

**Bước 4:** Hệ thống đưa dữ liệu vào hàng đợi đồng bộ và tải file lên Cloud Storage.

**Bước 5:** Cloud nhận dữ liệu, lưu phiên bản mới và cập nhật trạng thái đồng bộ.

**Bước 6:** Các thành viên có quyền truy cập có thể tải hoặc xem phiên bản mới nhất.

### Sơ đồ minh họa

```text
       DESIGNER
           |
           v
    Mở file thiết kế 3D
           |
           v
       Nhấn Ctrl + S
           |
           v
     LOCAL SSD
    (Lưu file mới)
           |
           v
   Phần mềm đồng bộ
      OneDrive
           |
           v
    Kiểm tra thay đổi
           |
           v
   Đưa vào hàng đợi
     đồng bộ dữ liệu
           |
           v
    CLOUD STORAGE
   (Lưu bản sao trực tuyến)
           |
           v
    VERSION HISTORY
   (Lưu lịch sử phiên bản)
           |
           v
   Các thành viên nhóm
    truy cập và sử dụng
```

**Giải thích:** Khi Designer nhấn Ctrl + S, dữ liệu được lưu trên máy tính trước. Sau đó, phần mềm đồng bộ sẽ phát hiện thay đổi và tự động tải dữ liệu lên Cloud khi có kết nối Internet.

Lưu ý: Việc nhấn Ctrl + S không đồng nghĩa với việc file đã được tải lên Cloud ngay lập tức. Người dùng cần chờ phần mềm đồng bộ báo trạng thái hoàn tất.

### 2\. Cách xử lý khi xảy ra xung đột phiên bản (File Version Conflict)

Xung đột phiên bản xảy ra khi hai thành viên cùng chỉnh sửa một file trong khoảng thời gian gần nhau hoặc khi một thiết bị ngoại tuyến tiếp tục chỉnh sửa file trong lúc thiết bị khác đã cập nhật bản mới lên Cloud.

**Ví dụ:**

* Bạn A chỉnh sửa file `HienVat\\\_3D.blend` trên máy tính cá nhân.
* Bạn B cũng mở và chỉnh sửa file đó trên một thiết bị khác.
* Bạn A lưu phiên bản thứ nhất.
* Bạn B lưu phiên bản thứ hai.
* Hệ thống phát hiện có sự khác biệt giữa hai bản chỉnh sửa.

**Phương án xử lý:**

1. Hệ thống phát hiện sự khác biệt giữa các phiên bản.
2. Phần mềm đồng bộ có thể tạo một bản sao xung đột hoặc yêu cầu người dùng xử lý tùy theo ứng dụng.
3. Người quản lý kiểm tra nội dung của cả hai file.
4. Chọn phiên bản đầy đủ và ổn định nhất.
5. Đổi tên bản được chọn thành phiên bản chính thức.
6. Lưu trữ bản còn lại để tránh mất dữ liệu quan trọng.

**Nguyên tắc:** Không tự ý ghi đè hoặc xóa bản xung đột khi chưa kiểm tra nội dung.

\---

## III. PHƯƠNG ÁN DỰ PHÒNG KHI MẤT INTERNET HOẶC SẬP NGUỒN

Đây là tình huống quan trọng cần giải quyết để đảm bảo dữ liệu không bị gián đoạn trong quá trình đồng bộ.

### 1\. Khi máy tính mất kết nối Internet

* File vẫn được lưu trực tiếp trên Local SSD khi người dùng nhấn Ctrl + S.
* Phần mềm OneDrive tiếp tục giữ những thay đổi chưa được đồng bộ trong hàng đợi.
* Khi Internet hoạt động trở lại, phần mềm tự động tiếp tục tải dữ liệu lên Cloud.
* Người dùng kiểm tra trạng thái đồng bộ để xác nhận dữ liệu đã được tải lên thành công.

### 2\. Khi máy tính bị sập nguồn đột ngột

* Nếu file đã được lưu hoàn chỉnh trên Local SSD, dữ liệu đó vẫn có thể được sử dụng sau khi máy tính khởi động lại.
* Những dữ liệu chưa được tải lên Cloud sẽ được phần mềm đồng bộ tiếp tục xử lý khi máy tính hoạt động trở lại.
* Nếu máy tính sập nguồn đúng lúc đang ghi file, file có thể bị lỗi hoặc chưa được lưu đầy đủ.
* Designer cần kiểm tra file, sử dụng chức năng Auto Recovery của phần mềm thiết kế nếu có và khôi phục từ Version History nếu cần.

### 3\. Biện pháp hạn chế rủi ro

* Sử dụng phần mềm đồng bộ chính thức như OneDrive hoặc Google Drive.
* Không tắt máy khi phần mềm vẫn đang tải dữ liệu lên Cloud.
* Chờ biểu tượng đồng bộ hoàn tất trước khi kết thúc công việc.
* Sử dụng bộ lưu điện UPS nếu thường xuyên làm việc với file thiết kế dung lượng lớn.
* Không để nhiều người cùng chỉnh sửa trực tiếp một file nếu phần mềm không hỗ trợ cộng tác đồng thời.

**Kết luận:** Khi mất Internet, dữ liệu đã lưu trên máy vẫn được giữ lại và chờ đồng bộ. Tuy nhiên, nếu file chưa kịp lưu hoàn chỉnh trước khi sập nguồn thì hệ thống không thể đảm bảo khôi phục toàn bộ dữ liệu. Vì vậy, cần kết hợp lưu tự động, đồng bộ Cloud và Version History để giảm thiểu rủi ro.

\---

## IV. QUY TRÌNH THỰC THI: 3 BƯỚC THIẾT LẬP PHẦN MỀM ĐỒNG BỘ

Đề xuất sử dụng Microsoft OneDrive trên máy tính Windows.

### Bước 1: Cài đặt và đăng nhập OneDrive

* Mở ứng dụng OneDrive trên máy tính.
* Đăng nhập bằng tài khoản Microsoft.
* Chọn thư mục OneDrive để lưu trữ tài liệu dự án.
* Kiểm tra kết nối Internet và đảm bảo ứng dụng đang hoạt động.

**Mục đích:** Tạo môi trường lưu trữ Cloud để quản lý tài liệu của dự án.

### Bước 2: Thiết lập thư mục làm việc và đồng bộ tự động

* Tạo thư mục `DuAn\\\_SoHoa\\\_BaoTang\\\_PTIT`.
* Tạo các thư mục con:

  * `01\\\_TaiLieu`
  * `02\\\_ThietKe\\\_3D`
  * `03\\\_HinhAnh\\\_HienVat`
  * `04\\\_BaoCao`
* Lưu toàn bộ file thiết kế vào thư mục OneDrive.
* Bật tính năng đồng bộ tự động.
* Kiểm tra trạng thái đồng bộ sau khi lưu file bằng Ctrl + S.

**Mục đích:** Đảm bảo các file làm việc được đưa vào vùng đồng bộ để tự động tải lên Cloud.

### Bước 3: Kiểm tra Version History và thử nghiệm khôi phục

* Mở OneDrive trên trình duyệt.
* Chọn file thiết kế cần kiểm tra.
* Nhấn chuột phải và chọn Version History.
* Xem danh sách các phiên bản đã lưu.
* Chọn phiên bản cần khôi phục khi phát hiện file bị lỗi.
* Kiểm tra lại file sau khi khôi phục.

**Mục đích:** Giúp nhóm có thể quay lại phiên bản ổn định trước đó khi xảy ra sai sót trong quá trình chỉnh sửa.

\---

## V. KẾT QUẢ DỰ KIẾN

Sau khi triển khai hệ thống Hybrid Workflow kết hợp Version History, dự án Số hóa Bảo tàng PTIT đạt được những kết quả sau:

|Tiêu chí|Kết quả|
|-|-|
|Lưu trữ Local|Có thể làm việc trực tiếp trên máy tính|
|Sao lưu Cloud|Tự động đồng bộ khi có Internet|
|Mất kết nối mạng|Giữ thay đổi trong hàng đợi đồng bộ|
|Quản lý phiên bản|Theo dõi lịch sử chỉnh sửa|
|Khôi phục dữ liệu|Có thể quay lại phiên bản trước|
|Làm việc nhóm|Dễ dàng chia sẻ tài liệu|

**Lợi ích:**

* Hạn chế nguy cơ mất dữ liệu khi ổ cứng gặp sự cố.
* Tiết kiệm thời gian gửi và nhận file qua Zalo.
* Giúp các thành viên dễ dàng truy cập tài liệu dự án.
* Có thể khôi phục dữ liệu khi chỉnh sửa nhầm hoặc file bị lỗi.
* Tăng tính chuyên nghiệp trong quá trình quản lý tài liệu doanh nghiệp.



#   H C M _ K S 2 6 _ C N T T 2 _ I T 1 0 8 _ S e s s i o n 1 5 _ E x 0 1  
 