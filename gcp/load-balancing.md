* Phân phối các traffic giữa các instances trong 1 region hoặc nhiều regions
* Tính năng
  * Health check
  * Auto scaling
  * Global LB with single anycast IP
* 1 LB sẽ có 3 phần
  * BE config: Nơi nhận request (endpoint)
  * Host and rule: Định nghĩa các path để traffic đến các BE khác nhau
  * FE config: IP, port, protocol mà client request
* Các giao thức được sử dụng
  * Client - LB: HTTPS/TLS
  * LM - VM: HTTP/TCP
* Có các loại LB ứng với các giao thức:
  * Internal TCP/UDP Load Balancing
  * Internal HTTP(S) Load Balancing
