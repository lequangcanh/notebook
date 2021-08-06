* Service xử lý message bất đồng bộ
* Autoscale xử lý hàng tỉ message mỗi ngày
* Chi phí thấp
* Support push và pull message

### Publisher and Subscriber
* Publisher: Send message vào topic (HTTP)
* Subscriber: Nhận message, có 2 cách:
  * Pull: Subscriber tự lấy message từ topic (HTTP)
  * Push: message được send cho subscribers thông qua webhook endpoint
* Snapshot: Lưu lại trạng thái của subscription
* Khi subscriber nhận được message và gửi lại ACK thì lần sau sẽ không nhận những message cũ nữa

### CLI
* `gcloud pubsub topics create <TOPIC_NAME>`
* `gcloud pubsub subscriptions create <SUB_NAME> --topic=<TOPIC_NAME>`
* `gcloud pubsub topics publish <TOPIC_NAME> --message=....`
* `gcloud pubsub subscriptions pull <SUB_NAME> [--auto-ack]`
