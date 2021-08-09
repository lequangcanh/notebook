### Vấn đề về subdomain
* Trong Rails routes, subdomain được hiểu rất đơn giản,nó là những gì đứng trước domain chính. Ví dụ:
  * `admin.project.com.vn` thì mặc định subdomain được hiểu là `admin.project`, nếu trong `config/routes.rb` chỉ khai báo `constraints subdomain: "admin"` thì sẽ lỗi ngay
  * `admin.project.com` thì subdomain được hiểu là `admin`
  * Vậy thì làm sao trỏ tới đúng subdomain ở case 1. Lúc này phải setting lại config `config.action_dispatch.tld_length = 2` (top-level domain length, mặc định nó sẽ = 1)
