### Backup DB
* Snapshot
* Transaction Log: Lưu log liên tục
* Standby: Master-Slave

### High Availability and High Durability
* Để tăng độ khả dụng (HA): có nhiều standby, phân phối DB trên nhiều region, zone
* Tăng độ bền (HD): Có nhiều bản copy data (standby, snapshot, transsaction logs, replicas) trên nhiều zone và region
* RPO (Recovery Point Objecttive): Khoảng thời gian mất dữ liệu tối đa chấp nhận được
* RTO (Recovery Time Objective): Khoảng thời gian down time tối đa cho phép
* Các kịch bản khi DB có vấn đề
  |RPO|RTO|Solution|
  |---|---|--------|
  |Rất nhỏ (1m)|Rất nhỏ (5m)|Hot standby. Có 1 standby sẵn sàng để backup|
  |Rất nhỏ (1m)|Vừa (15m)|Warm standby. Có 1 standby với kiến trúc nhỏ nhất, scale nó lên khi gặp sự cố|
  |Rất nhỏ (1m)|Vài giờ|Có thể sử dụng snapshot và transaction logs|
  |Cho phép dữ liệu có thể mất||Build server mới khi có vấn đề|
  
### Relational databases
* OLTP (Online Transaction Processing): 
  * Application mà 1 lượng lớn users thực hiện một lượng lớn các transaction nhỏ.
  * Lưu data theo row
  * RDS phổ biến: MySQL, SQL Server, ....
  * GCP Service: Cloud SQL, Cloud Spanner
* OLAP (Online Analytics Processing):
  * Application cho phép users phân tích petabytes data
  * Lưu data theo column
  * GCP Service: Big Query

### NoSQL 
* Cloud Firestore (recommend cho ít TB), Cloud BigTable (recommend > 10TB)
* Datastore là 1 highly scalable NoSQL database cho webapp và mobile app.
* Firestore là thế hệ tiếp theo của Datastore
* Firestore được xây dựng trên NFS (Network Filesystem)
* Có 3 options cho hệ thống lưu trữ dữ liệu của Cloud Firestore:
  * Datastore (cũ)
  * Firestore in Datastore (sử dụng Firestore tương thích ngược với Datastore)
  * Firestore Native mode (recommened)

### Memory Store: 
* Redis, Memcached

### Usecase
* Cloud SQL: Support MySQL, PostgreSQL, SQL Server
* Cloud Spanner được sử dụng khi:
  * Cần lưu trữ nhiều hơn
  * Global DB
  * Higher Availability
* Big Query/Data Warsehourse: Truy vấn trên dataset rất lớn, vì vậy nó rất đắt cần estimate trước khi chạy. Trả tiền theo data đã scan chứ không phải theo result
* Data Flow: Tạo các job để backup data. Rất quan trọng với Big Table vì dữ liệu rất lớn
