* GAE là 1 service được xây dựng trên kiến trúc serverless
* App Engine là Regional, không thể change Region
* Mặc định GAE đã connect tới Stack Driver
* Bạn chỉ cần code application và deploy lên GAE
* Các công việc ở tầng infra đã có Google lo
* GAE cung cấp 2 option là Standard và Flexible:
  * Standard: App của bạn sẽ được chạy trên các NNLT được định nghĩa trước
    * Version 1 chỉ support Java, Python, PHP, Go
    * Version 2 thì support thêm Ruby và NodeJS
  * Flexible: App của bạn sẽ được chạy với Docker container
* 1 project chỉ deploy được 1 application lên GAE
  * Có thể chia 1 application thành nhiều service hoặc component
  * Có thể run application với các version khác nhau. Mỗi version có thể run trên nhiều instance. Nhiều version có thể run cùng lúc
* So sánh tính năng của Standard và Flexible
|Feature|Standard|Flexible|
|-------|--------|--------|
|Pricing|Instance hourse|vCPU,Memory, Persistent Disk|
|Scaling|Manual, Basic, Automatic|Manual, Automatic|
|Scaling to 0|Yes|No. Min is 1|
|Startup time|seconds|minutes|
|Rapid scaling|Yes|No|
|Max request timeout|1-10 minutes|60 minutes|
|Local Disk|Can write to /tmp|Yes|
|SSH|No|Yes|

* Scaling instances:
  * Automatic: Sử dụng khi workload được chạy liên tục. Config min và max instance, target
  * Basic: Sử dụng trong các case instance được tạo khi nhận request, shutdown khi không có request. Config max instance và Idle timeout
  * Manual: Config số lượng instance được chạy bằng tay

### Deploy
* GAE mặc định sẽ đọc config deploy từ file `app.yml` trong application
* Mỗi lần deploy sẽ tạo 1 version mới và mặc định nếu không có thêm option gì tất cả traffic đều trỏ về version mới nhất
* Có thể đặt tên cho version để dễ quản lý `gcloud app deploy --version=v1`
* Có thể chia traffic cho các version `gcloud app services set-traffic --splits=v1=0.5,v2=0.5` thì khi request tới nó có thể sẽ được trỏ vào ngẫu nhiên v1 hoặc v2
* Các endpoint mặc định mà GAE sinh ra cho application
  * default service: `PROJECT_ID.REGION_ID.r.appspot.com`
  * service chỉ định: `SERVICE-dot-PROJECT_ID.REGION_ID.r.appspot.com`
  * Version chỉ định: `VERSION-dot-SERVICE-dot-PROJECT_ID.REGION_ID.r.appspot.com`
* GAE split traffic thông qua:
  * IP (mặc định)
  * Cookie (GOOGAPPUID)
  * Random
* Deploy Flexible bằng image `gcloud app deploy --image-url gcr.io/image_name:tag`
