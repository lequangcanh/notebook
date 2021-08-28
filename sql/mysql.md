### Index
* Clustered index: https://viblo.asia/p/hieu-ve-clustered-index-bJzKmw9Bl9N
* Hash index: https://viblo.asia/p/hash-index-trong-sql-63vKjwOVZ2R

### Collation
* Định nghĩa rule để so sánh các characters trong 1 charset. Trong đó khi suffix là `_ci (case insensitive)` nghĩa là các ký tự sẽ không phân biệt hoa thường, còn nếu suffix là `_cs (case sensitive)` nghĩa là sẽ phân biệt hoa thường

### Set mysql_native_password
```
sudo mysql -u root
select Host, User, plugin from mysql.user;
use mysql;
update mysql.user set plugin = 'mysql_native_password' where User='root';
flush privileges;
exit;
```

### Cho phép user bên ngoài truy cập vào MySQL
1. Mở port trong file config
    ```
    sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf (Ubuntu >= 16.04)
    sudo nano /etc/mysql/my.cnf (Ubuntu < 16.04)
    Comment line: bind-address 127.0.0.1
    ```
2. Add user cho phép truy cập (ko truy cập root dc)
    ```
    CREATE USER 'guest'@'localhost' IDENTIFIED BY '123456';
    GRANT ALL PRIVILEGES ON *.* TO 'guest'@'localhost' WITH GRANT OPTION;
    CREATE USER 'guest'@'%' IDENTIFIED BY '123456';
    GRANT ALL PRIVILEGES ON *.* TO 'guest'@'%' WITH GRANT OPTION;
    ```
3. Restart lại mysql
    ```
    sudo service mysql restart
    ```
