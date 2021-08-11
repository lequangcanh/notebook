### Feature
* Cung cấp và quản lý máy ảo
* Load Balancing và Auto scaling cho nhiều VM instances
* Attach storage cho VM instances
* Quản lý kết nối các network

### Machine Family
* Là loại phần cứng để run các workload
* Có 3 Family được chia theo mục đích sử dụng:
  * General (E2, N2, N2D, N1): Tỉ lệ giá cả và hiệu năng hợp lý. Dùng cho các web app server, DB vừa và nhỏ, ....
  * Memory Optimized (M2, M1): Bộ nhớ cực kỳ cao. Dùng cho DB cần lưu trong RAM nhiều, xử lý dữ liệu trên RAM
  * Compute Optimized (C2): CPU cao. Dùng cho gaming app
* Mỗi Machine Family sẽ có nhiều Machine Type. Các machine sẽ được đặt tên theo công thức:

  `MachineFamily-WorkloadType-NumOfCPU`

  Ví dụ: `e2-standard-2` là Machine dòng E2 dùng cho mục đích standard và có 2 CPU.

  Các thông số về RAM, disk, network cũng sẽ tăng theo cấp số của CPU.
* Trong instance type, RAM sẽ gấp đôi theo số CPU, nhưng số lượng ít nhiều sẽ theo thứ tự highcpu < standard < highmem
* Maximum vCPU của 1 custom VM là 96, max RAM là 624GB

### VM IP Address
* Mỗi VM có ít nhất 1 internal IP, external IP là optional
* Khi stop VM, external IP sẽ bị thu hồi, internal IP thì vẫn được giữ lại đến khi VM bị xóa
* IP Address sẽ có 2 loại:
  * Ephemaral: Có thể thay đổi (thường sẽ được cấp bởi Google)
  * Static: Không thay đổi (cái này phải tốn tiền mua dù có dùng hay không)
* Đồng nghĩa với việc khi VM được set static IP, thì có stop cũng không bị thu hồi

### Giảm thiểu cost khi sử dụng VM
* Chỉ áp dụng cho GCE và GKE, không áp dụng được cho GAE, Data Flow
* Có các option
  * Sử dụng discount
  * Committed: Commit con số sử dụng trong 1 khoảng thời gian nào đó
  * Preemptible: Dùng tạm thời, có thể bị GCP thu hồi bất cứ lúc nào mà không cần báo trước. Tối đa 24h
* Có thể sử dụng Preemptible instance để thực thi các batch processing. Nếu jobs đang thực thi mà instance bị stop, có thể làm chậm việc thực thi job chứ không hoàn toàn stop hẳn. Preemptible instance sẽ hoàn thành những jobs đang chạy mà không đòi hỏi thêm bất kỳ chi phí nào

### Một số config quan trọng
* **Live migration**:
  * Giữ cho VM luôn chạy khi có cập nhật phần mềm hoặc phần cứng
  * Không support cho GPUs và Preemptive instances
  * Về cơ chế thì nó sẽ chạy trên 1 host khác cùng zone để thực hiện cập nhật
* **Availability Policy**:
  * On host maintenance: Điều gì xảy ra khi có update kiến trúc
    * Migrate: Migrate instance trên 1 hardware khác
    * Terminate: Tắt luôn VM instance
  * Automatic restart: Restart VM nếu nó bị tắt bởi 1 lý do nào đó không phải của user init, ví dụ như lỗi phần cứng, ...
* Có thể chọn Custom Machine Type khi những option được định nghĩa trước không phù hợp. **Chỉ áp dụng cho General Family**
* GPU chỉ support một số machine type
* Có thể change machine type khi VM instance đã được stop

### Instance Template và Instance Group
* Instance Template khai báo các thuộc tính của instance và lưu lại như 1 Template
* Có thể run instance từ template
* Instance Group có tác dụng trong auto scale, có thể tự quản lý bằng cách add các instance vào group. Nhưng tốt nhất là nên để Google quản lý bằng instance template

### Startup
* Sau khi request tạo 1 instance mới (Service account phải được tạo trước khi attach vào instance), instance sẽ được bắt đầu ở trạng thái Provisioning. Sau khi space được tìm thấy và gán vào host machine, instance sẽ được chuyển sang trạng thái Starting, trong khi host machine chuẩn bị run instance và sắp xếp lại một số thứ như network adapter, ... Ngay khi VM được khoier động lên và hệ điều hành chạy các start up scripts, instance sẽ chuyển sang trạng thái Running

### Sole tenancy
* Sole tenancy đảm bảo răng chỉ những VMs trong cùng project sẽ run trên 1 máy chủ vật lý

### Login to server
* RDP (Remote Desktop Protocol) được sử dụng để loggin vào 1 Windows server
* SSH được sử dụng để loggin vào Linux server
