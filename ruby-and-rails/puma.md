### Workers, Threads

* Số xử lý đồng thời tối đa của Rails app sẽ bằng `workers * threads`
* Nó sẽ có liên quan đến số database pool config trong `database.yml`. Số pool này là số cổng mà Rails app có thể kết nối tới database
* Mặc định thì nên config số pool này bằng với max threads, tức là có bao nhiêu threads thì sẽ có tương ứng bấy nhiêu pool để xử lý
* Khi config số pool quá nhỏ hơn so với số threads có thể dẫn đến các request sẽ phải đợi để connect vào database dẫn tới lỗi 500
* Ngược lại khi config số pool quá lớn và số threads cũng quá lớn có thể dẫn tới database bị quá tải vì phải xử lý rất nhiều query cùng 1 lúc
* Vì vậy dựa vào số max connection mà DB có thể đáp ứng được để config số pool, số threads trên mỗi con instance có thể access vào DB
