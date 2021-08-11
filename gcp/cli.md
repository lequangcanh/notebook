* Có các lệnh:
  * `gcloud`: đây là command cơ bản cho hầu hết các trường hợp
  * `gsutil`: command sử dụng khi làm việc với GCS
  * `bq`: command dùng làm việc với Big query
  * `cbt`: Cloud Big table
  * `kubectl`: Tương tác với K8s
* Cấu trúc command gcloud
  * `gcloud <group> <subgroup> <action> .....`
  * Trong đó:
    * `group` sẽ là các service của GCP như: compute, container, dataflow, function, iam, ...
    * `subgroup` sẽ là group con của các service ví dụ như instance, machine-type, ...
    * `action` là hành động muốn thực thi ví dụ như delete, create, list, start, stop, ...
* Set region và zone mặc định khi tạo VM. Có 3 cách:
  * `gcloud compute project-info add-metadata --metadata=google-compute-default-region=...,google-compute-default-zone=...`
  * `gcloud config set compute/region ...`
  * `gcloud create compute ... --zone=... --region=...`
  * Khi cả 3 option trên đều được setting thì sẽ ưu tiên theo thứ tự từ command dưới lên
* Filter bằng cách thêm option `--filter="key:(value1 value 2)"`
* Sort bằng option `--sort-by (NAME/~NAME)`

* Tạo các config khác nhau: `gcloud config configurations create <NAME>`
* Active 1 config để thao tác với các service: `gcloud configurations active <NAME>`
