### Thao tác với cluster sử dụng gcloud
* Tạo cluster `gcloud container clusters create ...`
* Connect tới cluster `gcloud container clusters get-credentials <NAME> --zone ... --region ...`
* Mỗi cluster sẽ được tạo với ít nhất 1 node pool. Node pool là template của group các nodes được tạo trong cluster
* Resize cluster `gcloud container clusters resize <NAME> --node-pool ... --num-nodes=3`
* Autoscaling `gcloud container clusters update <NAME> --enable-autoscaling --min-nodes=1 --max-nodes=10`

### Thao tác với deployment
* Tạo deployment `kubectl create deployment <NAME> --image=...`
* Expose 1 deployment `kubectl expose deployment <NAME> --type=LoadBalancer --port=8080`
* Scale deployment `kubectl scale deployment <NAME> --replicas=3`
* Autoscaling `kubectl autoscale deployment <NAME> --max=10 --cpu-percent=80`

### ConfigMap và Secrets
* Lưu trữ các hằng số như biến môi trường của application
* `kubectl create configmap <NAME> --from-literal=KEY=VALUE`

### Nodes
* Cluster là tập hợp các nodes gồm master node và worker nodes
* Master node là nơi điều khiển K8s, gồm 4 component:
  * API Server: Đảm bảo giao tiếp trong 1 K8s
  * Scheduler: Quyết định vị trí của các pods trong các nodes
  * Control Manager: Quản lý deployment và replicas
  * etcd: Phân phối data lưu trữ
* Worker node:
  * Là nơi mà các pod running
  * kubelet: Quản lý giao tiếp với master node

### Pod
* Pod là đơn vị nhỏ nhất của K8s
* Mỗi pod có thể chứa 1 hoặc nhiều container (mà thông thường là 1)
* Mỗi pod được assign 1 IP Address động
* Tất cả container trong pod sẽ dùng chung: Network, Storage, IP Address, Ports, Volumns

### Service
* Nhiệm vụ expose các pods ra bên ngoài
* Có 3 loại service:
  * ClusterIP: microservice available trong cluster
  * LoadBalancer: Expose service ra ngoài internet sử dụng Cloud Load Balancer
  * NodePort: Không tạo LB cho từng service, mà tạo 1 Ingress dùng 1 LB rồi traffic đến từng service thông qua Nodepord
