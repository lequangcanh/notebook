### Cloud Monitoring
* Theo dõi các cơ sở hạ tầng
* Metrics
* Graph and Dashboard
* Alert
* Có thể monitor 1 hoặc nhiều GCP project và 1 hoặc nhiều AWS account

### Cloud Logging
* Cloud Audit Logs gốm:
  * Admin Activity logs
  * System event Logs
  * Data access logs
  * Policy Denined logs
* Log từ 1 resource nào đó sẽ đi vào Log route
* Log Route check config để quyết định cái nào lưu vào, cái nào từ chối, và lưu vào đâu
* Có 2 loại Log bucket:
  * `_required`: Chứa Admin activity, system event và Access transparency logs. Được lưu trong 400 ngày, không trả phí, không thể xóa và cũng không thể thay đổi được con số 400
  * `_default`: Những logs khác, default lưu trong 30 ngày, phải trả phí, không thể xóa nhưng có thể disable, có thể config retain day trong range 1 ngày -> 10 năm

### Cloud Trace
* 1 service tốn bao nhiêu lâu để xử lý request
* Độ trễ trung bình của request
* Đã quá giờ như thế nào
* Support cho GCE, GKE, GAE

### Cloud Debugger
* Chụp lại trạng thái của app đang chạy
* Trực tiếp trên GCP
* Snapshot của các biến
* Không cần add log, không cần deploy lại
