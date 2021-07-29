* Block Storage:
  * Tương tự nhử ổ cứng máy tính
  * 1 Block storage có thể kết nối với 1 VM
  * Tuy nhiên, 1 Block storage read only có thể attach vào nhiều VM
  * 1 VM thì lại có thể kết nối với nhiều Block Storage
* File Storage:
  * Được share với nhiều VM
  * Nơi để lưu trữ file, edit, share file nhanh chóng
* Local SSDs:
  * Là storage vật lý attach vào VM
  * Chỉ tồn tại khi VM đang running
  * Độ trễ thấp
  * Bộ nhớ tạm
* Persistent Disks:
  * Độc lập với VM
  * Regional & Zonal
  * Có 3 loại: Standard (HDD, giá rẻ) < Balanced (SSD, cân bằng giữa giá và performance) < SSD (performance cao)
* Snapshot: Backup storage

### Machine Image
* Được tạo từ 1 VM, chứa mọi thứ có thể tạo 1 VM
