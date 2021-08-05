* Role là tập hợp các permission, không liên quan đến member
* Dùng policy để assign role cho member
* Role có 3 loại:
  * Primitive: Owner/Editor/Viewer
  * Predefined: Những role gắn liền với các resource mà Google định nghĩa sẵn
  * Custom: Role do chúng ta tự định nghĩa
* Role được assign cho member thông qua policy document, được biểu diễn bằng các policcy object
  * Policy object là list các bindings
  * Mỗi binding là bind 1 role cho list members
  * Member có thể là user, service account, group, domain
  ```json
  {
    "bindings": [
      {
        "role": "roles/storage.objectAdmin",
        "members": [
          "user:example@gmail.com",
          "serviceaccount:example@project-id.service-account",
          "group:...",
          "domain:..."
        ]
      },
      {
        "role": ".....",
        "members": ["......"]
      }
    ]
  }
  ```

### CLI
* Show list binding: `gcloud projects get-iam-policy <PROJECT_ID>`
* Add IAM policy binding: `gcloud projects add-iam-policy-binding <PROJECT_ID> --member=<MEMBER> --role=<ROLE>`
* Delete IAM policy binding `gcloud projects remove-iam-policy-binding <PROJECT_ID> --member=<MEMBER> --role=<ROLE>`
* Set IAM policy binding `gcloud projects set-iam-policy-binding <PROJECT_ID> --member=<MEMBER> --role=<ROLE>`
* Delete project `gcloud projects delete <PROJECT_ID>`

### Service account
* Được định nghĩa bởi 1 email address
* Không có pass, chỉ có cặp RSA key, không thể đăng nhập qua browser
* Các loại service account:
  * Default: Được tạo ra khi một số service cần dùng
  * User Managed: Do user tự tạo (Recommend)
  * Google Managed: Được tạo bởi Google

### ACL (Access Control List)
* Định nghĩa ai được access vào bucket hoặc object nào, cũng như họ được làm gì
* Khác với IAM là apply cho all object trong 1 bucket
* ACL được định nghĩa cho từng object khác nhau
* User chỉ có thể access khi được allow bởi IAM và ACL
* Có 2 loại của access control:
  * Uniform: Sử dụng IAM
  * Find-grained: Sử dụng IAM và ACL
* Signed URL: Cho phép access object trong 1 khoảng thời gian nhất định
