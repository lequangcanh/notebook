### Key Management Service
* Có 3 trạng thái của data
  * Data at rest: Được lưu trữ hoặc backup trong ổ cứng
  * Data in motion: Data đang transfer trong network (network có thể là internet hoặc local)
  * Data in use: Lưu trữ trong RAM để sử dụng, không lưu trữ lâu dài
* Có 2 loại mã hóa và giải mã:
  * Symmetric Encryption: Sử dụng 1 key để mã hóa và giải mã
  * Asysmetric Encryption: Sử dụng public key để mã hóa, private key để giải mã
* KMS là service để tạo và quản lý các key dùng để mã hóa, tương tác với hầu hết GCP services
* Có 3 loại:
  * Google-managed key: Các key này do Google tạo và quản lý, chúng ta không cần config gì cả
  * Customer-managed key: Key được tạo và quản lý trong KMS bởi người dùng
  * Customer-supplied key: Key được tạo từ bên ngoài và lưu vào KMS
