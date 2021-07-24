* Resource nên được đặt trong 1 project phù hợp
* Resource nên được tag bằng label
* `gcloud` mặc định set region và zone theo khu vực gần nhất

### Các loại service
* **IaaS (Infrastructure as a Service)**: Chỉ sử dụng cơ sở hạ tầng từ nhà cung cấp, chúng ta sẽ phải cài tất cả mọi thứ từ OS, Application Runtime, Application, ....
* **PaaS (Platform as a Service)**: Chỉ cần quan tâm tới application code. Mọi thứ còn lại cloud service sẽ lo
* **CaaS (Container as a Service)**: Tương tự như PaaS nhưng thứ chúng ta quan tâm là container
* **FaaS (Function as a Service)**: Chúng ta sẽ quan tâm đến function thay vì cả application

### Serverless
* Một kiến trúc serverless nghĩa là chúng ta chỉ cần quan tâm tới phần coding, phần application, làm sao để ứng dụng của chúng ta có thể work được
* Chúng ta sẽ không quan tâm và không can thiệp vào tầng kiến trúc như config server, cài đặt OS, auto scaling, load balancing, ....
* Với kiến trúc serverless chúng ta sẽ trả tiền theo request, chứ không trả tiền cho server
