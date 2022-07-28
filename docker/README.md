### Cài docker
* Cài docker bằng lệnh curl: `curl -fsSL https://get.docker.com/ | sh`
* Cài đặt docker-compose: `https://docs.docker.com/compose/install/`
* Thêm current user vào docker group để khỏi dùng sudo `sudo usermod -aG docker $USER`

### Network
1. Network của của docker. Nếu như bị trùng thì thêm config vào "/etc/docker/daemon.json" (nếu chưa có file này thì tạo) với nội dung là
    ```json
    {
        "bip": "172.20.0.1/24"
    }
    ```
    sau đấy restart lại docker để nó nhận
2. Network trong cái docker-compose. Khi tạo network bằng lệnh `docker network create <NETWORK_NAME>` thì phải chú ý 1 cái là cái này nó lấy cái IP ngẫu nhiên, có khả năng trùng IP trong mạng LAN. Nên tự định nghĩa dãi IP `docker network create --ip-range 172.21.2.0/16 <NETWORK_NAME>`. Hoặc config trong file docker-compose.yml:
    ```yaml
    networks:
        my_network:
            ipam:
                driver: default
                config:
                    - subnet: 172.21.0.0/24
    ```

### Container
* Cho phép 1 container luôn bật khi khởi động máy `docker update --restart unless-stopped <CONTAINER_ID>`

### Logs
* Mặc định logs từ container sẽ lưu vào json file tại folder `/var/lib/docker/containers/{container_id}`. Gõ `docker logs <CONTAINER_ID> -f` thì nó sẽ in ra log ở trong file json này
* Nếu file logs lớn, gõ `docker logs -f` đợi nó load all sẽ khá lâu, có thể thêm option -n để nó load n dòng tính từ cuối file `docker logs <CONTAINER_ID> -f -n 20`
* Mặc định thì file logs của container sẽ lưu không giới hạn, chỉ bị xóa khi xóa container, muốn giới hạn lại file logs thì có thể thêm config vào `/etc/docker/daemon.json`
    ```yaml
    {
      "log-driver": "json-file",
      "log-opts": {
        "max-size": "10m",
        "max-file": "3"
      }
    }
    ```
    Hoặc cho container riêng lẽ `docker run -it --log-driver json-file --log-opt max-size=10m --log-opt max-file=3 alpine ash`
    Hoặc thêm option trong Compose:
    ```yaml
    logging:
      driver: "json-file"
      options:
        max-size: "50m"
    ```
* Log file quá lớn, muốn xóa hết log trong file json của container đang chạy, `cd /var/lib/docker/containers/<CONTAINER_ID>` rồi clear content của file log bằng lệnh `echo > <CONTAINER_ID>-json.log`, tuyệt đối ko xóa file này
