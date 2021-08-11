### VPC
* VPC là Global resource
* Chứa những subnet cùng hoặc khác region
* Khi create 1 subnet:
  * Enable Private Google Access: cho phép VM kết nối với Google API sử dụng private IP
  * Enable Flow logs: theo dõi các vấn đề gặp phải
* Resource trong 1 network sử dụng 1 dãi IP liên tục được biểu diễn dưới dạng CIDR Block
* Firewall rule:
  * Ingress: Target đi từ bên ngoài vào GCP target
  * Egress: Traffic đến destination từ GCP target
  * Trong đó: Target là tất cả instance hoặc được mark bởi tag, service account. Source có thể được mark bằng CIDR, tag, service account
  * Firewall rule gồm các component: Direction of traffic, action on match, protocol

### Shared VPC
* Được tạo trong 1 organization hoặc shared folder
* Cho phép VPC được share giữa các project cùng organization
* Shared VPC chưa 1 host project và nhiều service project. Trong đó
  * Host project: Chứa shared VPC
  * Service project: Attach to host project

### VPC Peering
* Có thể peer các network cùng project, khác project, khác organization
* Các giao tiếp giống như trong 1 project
* Network Admin không thể change
