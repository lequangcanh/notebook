* Delete multi branch, keep branch contain master, develop
    ```
    git branch | grep -v "master" | grep -v "develop"  | xargs git branch -D
    ```
* Keep branch is master, develop
    ```
    git branch | grep -v "master$" | grep -v "develop$"  | xargs git branch -D
    ```

* Ignore file not use .gitignore
    ```
    .git/info/exclude
    ```

* Line of Code
    ```
    git ls-files | xargs wc -l
    ```

* Lỗi khi 1 key có thể connect 1 server sau khi key đã bị change mặc dù vãn tồn tại trong máy local:
    * Nguyên nhân: Bị cache lại do ssh-agent
    * Kiểm tra lại bằng cách chạy lệnh ssh-add -l để xem cách key nào đang có trên terminal
    * Giải pháp: Chạy lệnh `eval "$(ssh-agent -s)"`
