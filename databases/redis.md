* Mở port redis cho bên ngoài truy cập
    ```
    Replaced bind 127.0.0.1 with bind 0.0.0.0 in the /etc/redis/redis.conf file, the line does not have a leading # nor space,
    Replaced protected-mode yes with protected-mode no in this same file,
    Allowed all traffic to port 6379 using ufw allow 6379 and ufw allow 6379/tcp
    ```
