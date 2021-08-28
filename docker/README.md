### Cài docker
* Cài docker bằng lệnh curl: `curl -fsSL https://get.docker.com/ | sh`
* Cài đặt docker-compose: `https://docs.docker.com/compose/install/`
* Thêm current user vào docker group để khỏi dùng sudo `sudo usermod -aG docker $USER`

### Network
1. Network của của docker. Nếu như bị trùng thì tạo ra 1 file là "/etc/docker/daemon.json" với nội dung là
    ```json
    {
        "bip": "172.20.0.1/24"
    }
    ```
    sau đấy restart lại docker để nó nhận
2. Network trong cái docker-compose. Khi tạo network bằng lệnh `docker network create git` thì phải chú ý 1 cái là cái này nó lấy cái IP ngẫu nhiên, có khả năng trùng IP trong mạng LAN. Nên tự định nghĩa dãi IP `docker network create --ip-range 172.21.2.0/16 <NETWORK_NAME>`. Hoặc config trong file docker-compose.yml:
    ```yaml
    networks:
        my_network:
            ipam:
                driver: default
                config:
                    - subnet: 172.21.0.0/24
    ```
