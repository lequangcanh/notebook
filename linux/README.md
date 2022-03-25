### Về stdin, stdout, stderr

* stdin (0) nhận dữ liệu cho shell
* stdout (1) hiển thị kết quả các lệnh
* stderr (2) hiển thị các lỗi trong quá trình thực thi các lệnh
* Trong linux 3 thằng này sẽ được symlink tới process tương ứng
  ```bash
  /dev/stdin -> /proc/self/fd/0
  /dev/stdout -> /proc/self/fd/1
  /dev/stderr -> /proc/self/fd/2
  ```
* Trong đó self nó sẽ được symlink tới 1 các process trong folder ``/proc` luôn. Hiểu nó là process hiện tại
* `2>&1` nghĩa là merge kết quả của `stderr` vào `stdout` luôn

  **[ĐANG BỎ NGỎ]**
* self nó hoạt động ntn? Thay đổi liên tục?
* Trong ubuntu thì mọi thứ work bình thường, nhưng trong các docker image bản alpine push log vào `/dev/stdout` hoặc `/proc/self/fd/1` thì nó lại không work? Nhưng push vào `/proc/1/fd/1` thì nó lại work? Process 1 này là gì?

### File /etc/resolv.conf
* symlink tới `../run/resolvconf/resolv.conf`?
* Trong `../run/resolvconf/resolv.conf` thì giá trị lại thay đổi mỗi khi đổi mạng?

### Cài song song windows và ubuntu
* Sai timezone trên win: `sudo timedatectl set-local-rtc 1`
* Mở ổ đĩa windows trên ubuntu: 

  `sudo fdisk -l`

  `sudo ntfsfix /dev/sda1`

### Cài zsh default trên ubuntu
`getent passwd | grep 'le.quang.canh' | sed -e 's/bash/zsh/g' | sudo tee -a /etc/passwd`
