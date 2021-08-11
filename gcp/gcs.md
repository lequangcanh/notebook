* GCS là Global
* Có 4 loại class:
  * Standard: Cho việc sử dụng và truy cập data thường xuyên
  * Nearline: Dùng backup, data access ít hơn 1 lần / tháng
  * Coldline: Dùng để khôi phục khi có sự cố, data access ít hơn 1 lần / quý
  * Archive: Data ít truy cập, access ít hơn 1 lần/năm
* File được lưu dưới dạng object
* Mỗi object được định nghĩa bởi 1 unique key trong bucket
* Max size của 1 object là 5TB
* Không giới hạn số lượng object trong bucket
* Có thể set rule cho object để xóa hoặc đưa xuống class ít truy cập hơn (Object Life Cycle)

### Sử dụng gsutil khi làm việc với GCS
* Tạo bucket: `gsutil mb gs://BUCKET_NAME`
* Copy/move `gsutil cp/mv gs://SOURCE gs://DES`
* Đổi class type `gsutil rewrite STORAGE_CLASS gs://BUCKET_NAME`
* Tạo signurl `gsutil signurl -d 10 minute YOUR_KEY gs://bucket/object`

### Đồng bộ dữ data giữa 2 bucket
* `gsutil rsync [OPTION]... src_url dst_url`
