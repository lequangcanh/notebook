### Vấn đề về push log

* Mặc định sidekiq sẽ push log info start và done của các job ra STDOUT.
* Để write log của ActiveRecord và các log khác của Rails trong sidekiq, config thêm ở sidekiq server.
* Ngoài ra sidekiq sẽ push log level info, để config level log thì định nghĩa trong sidekiq server luôn:
  ```ruby
  # config/initializers/sidekiq.rb
  Sidekiq.configure_server do |config|
    config.logger.level = Rails.application.config.log_level
    Rails.logger = Sidekiq.logger
    ActiveRecord::Base.logger = Sidekiq.logger
    ActiveJob::Base.logger = Sidekiq.logger

    config.redis = {url: ENV["REDIS_SERVER_URL"]}
  end
  ```

### Config sidekiq 6 khi deploy bằng Capistrano

* https://github.com/lequangcanh/cap_learning#v%E1%BB%81-sidekiq
