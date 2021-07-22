## Sử dụng whenever

### Identity:
* https://github.com/lequangcanh/cap_learning#v%E1%BB%81-whenever

### Tạo cron jobs

* Chạy lệnh `whenever --update-crontab` sẽ viết các job vào crontab của OS
* Mặc định whenever sẽ generate các job bằng các command `/bin/bash` và nó sẽ không run được trên các OS đang cài sh. Định nghĩa lại bằng option `job_template`
* Generate cronjob trong container sẽ có vấn đề là cron không đọc được các ENV khai báo lúc run, vì bản chất các ENV này nó tồn tại trong session chứ không tồn tại trong OS trong container. Vì vậy phải thực hiện load các ENV này vào crontab. Nếu deploy thẳng lên instance thì không cần
* Xuất log ra file hoặc stdout bằng option `output`
  ```ruby
  ENV.each {|k, v| env(k, v)}
  set :output, "/dev/stdout"
  set :job_template, "/bin/sh -l -c ':job'"

  every 1.minute do
    runner "..."
  end
  ```
