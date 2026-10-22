

```
config.plugin_locators = Rails::Plugin::FileSystemLocator
```

这些是用于查找你希望为应用程序加载的所需插件的类。

```
config.plugin_paths = "vendor/plugins"
```

这是插件目录的根路径。

```
config.plugins = nil
```

这是要加载的插件列表。如果设置为 nil，则会加载所有插件。如果设置为 []，则不会加载任何插件。否则，插件将按指定的顺序加载。

```
config.routes_configuration_file = "config/routes.rb"
```

这是要使用的路由配置文件路径。

```
config.time_zone = "UTC"
```

这设置默认时区。设置后将为 Active Record 模型启用时区感知，并将 Active Record 默认时区设置为 :utc。

如果你想使用其他时区，以下 Rake 任务可能会有所帮助：time:zones:all、time:zones:us 和 time:zones:local。time:zones:local 将尝试根据系统本地时间缩小可能性范围。

```
config.view_path = "app/views"
```

这是查找视图模板的位置。

```
config.whiny_nils = true | false
```

如果设置为 true，Rails 将尝试拦截你在未初始化对象上调用方法时的情况。例如，如果你的 @orders 变量未设置且你调用 @orders.each，Ruby 通常只会说类似 undefined method `each' for nil 的内容。启用 whiny_nils 后，Rails 会拦截此情况并改为提示你可能期望一个数组。默认情况下在开发环境中是开启的。

### B.2 Active Record 配置

```
config.active_record.allow_concurrency = true | false
```

如果设置为 true，每个线程将使用单独的数据库连接。由于 Rails 在用于提供 Web 应用程序时不是线程安全的，因此此变量默认为 false。你可能会考虑（谨慎地）将其设置为 true，如果你正在编写使用 Active Record 的多线程应用程序，且在 Rails 其余部分范围之外使用。

```
config.active_record.colorize_logging = true | false
```

默认情况下，Active Record 日志消息包含嵌入的 ANSI 控制序列，当使用支持这些序列的终端应用程序查看时，会对某些行进行着色。将选项设置为 false 可移除此着色。

```
config.active_record.default_timezone = :local | :utc
```

将其设置为 :utc 可使从数据库加载和保存的日期和时间被视为 UTC。

```
config.active_record.lock_optimistically = true | false
```

如果为 false，则乐观锁定被禁用。参见第 20.4 节、乐观锁定，第 422 页。

```
config.active_record.logger = logger
```

这接受一个 logger 对象，应与 Log4R 接口兼容。内部用于记录数据库活动。它也可在应用程序希望通过 logger 属性记录活动时使用。

```
config.active_record.pluralize_table_names = true | false
```

如果设置为 false，创建对应表名时类名将不会被复数化。

```
config.active_record.primary_key_prefix_type = option
```

如果 option 为 nil，每个表的默认主键列名为 id。如果为 :table_name，则在前面加上表名。通过将 option 设置为 :table_name_with_underscore，可在表名和 id 部分之间添加下划线。

```
config.active_record.record_timestamps = true | false
```

将其设置为 false 可禁用 created_at、created_on、updated_at 和 updated_on 列的自动更新。这在第 409 页有描述。

```
config.active_record.table_name_prefix = "prefix"
```

在生成表名时添加给定的字符串。例如，如果模型名为 User 且前缀字符串为 "myapp-"，Rails 将查找表 myapp-users。如果必须在不同应用程序之间共享数据库或必须在同一数据库中进行开发和测试，这可能很有用。

```
config.active_record.table_name_suffix = "suffix"
```

在生成表名时附加给定的字符串。

```
config.active_record.timestamped_migrations = true | false
```

将其设置为 false 可使用递增整数代替时间戳作为迁移前缀。

```
config.active_record.schema_format = :sql | :ruby
```

这控制转储数据库架构时使用的格式。这在运行测试时很重要，因为 Rails 使用从开发环境转储的架构来填充测试数据库。:ruby 格式创建

```
config.action_mailer.default_content_type = "text/plain"
```

这是电子邮件的默认内容类型。

```
config.action_mailer.default_implicit_parts_order =
%w( text/html text/enriched text/plain)
```

我们曾在第 616 页看到，如果找到名为 xxx.text.plain.rhtml、xxx.text.html.rhtml 等的模板文件，Rails 会自动生成多部分消息。此参数决定这些部分添加到电子邮件中的顺序，从而决定电子邮件客户端赋予它们的优先级。

```
config.action_mailer.default_mime_version = "1.0"
```

这是电子邮件的默认 mime 版本。

```
config.action_mailer.delivery_method = :smtp | :sendmail | :test
```

这决定电子邮件的投递方式。与 smtp 设置一起使用。参见第 610 页开始的描述。

```
config.action_mailer.logger = logger
```

将其设置为覆盖邮件程序使用的默认记录器。未设置时，使用整个应用程序的记录器。

```
config.action_mailer.perform_deliveries = true | false
```

如果为 false，邮件程序将不会投递电子邮件。

```
config.action_mailer.raise_delivery_errors = true | false
```

如果为 true，电子邮件投递失败时会引发异常。请注意，Rails 只知道电子邮件向邮件传输代理的初始交接。它无法判断邮件是否真正到达收件人。此参数在测试环境中为 true，但在其他环境中默认为 false。

```
config.action_mailer.register_template_extension extension
```

这注册模板扩展，以便使用 ERb 或 Builder 以外的模板语言编写的邮件程序模板得到支持。

```
config.action_mailer.sendmail_settings = hash
```

这是一个包含以下设置的哈希：

-   :location 这是 sendmail 可执行文件的路径。默认为 /usr/sbin/sendmail。

-   :arguments 这包含命令行参数。默认为 -i -t。

```
config.action_mailer.smtp_settings = hash
```

参见第 610 页开始的描述。

## 附录 C

### 源代码

本附录包含我们为最终 Depot 应用程序创建的文件的完整列表，以及我们修改的生成文件。

所有代码均可从我们的网站下载：

- http://pragprog.com/titles/rails3/code.html

### C.1 完整的 Depot 应用程序

### 数据库配置和迁移

Download depot_f/config/database.yml

```
# SQLite version 3.x
# gem install sqlite3-ruby (not necessary on OS X Leopard)
development:
  adapter: sqlite3
  database: db/development.sqlite3
  pool: 5
  timeout: 5000

# Warning: The database defined as "test" will be erased and
# re-generated from your development database when you run "rake".
# Do not set this db to the same as development or production.
test:
  adapter: sqlite3
  database: db/test.sqlite3
  pool: 5
  timeout: 5000

production:
  adapter: sqlite3
  database: db/production.sqlite3
  pool: 5
  timeout: 5000
```

Download depot_t/db/migrate/20080601000001_create_products.rb

```
class CreateProducts < ActiveRecord::Migration
  def self.up
    create_table :products do |t|
      t.string :title
      t.text :description
      t.string :image_url

      t.timestamps
    end
  end

  def self.down
    drop_table :products
  end
end
```

Download depot_t/db/migrate/20080601000002_add_price_to_product.rb

```
class AddPriceToProduct < ActiveRecord::Migration
  def self.up
    add_column :products, :price, :decimal,
      :precision => 8, :scale => 2, :default => 0
  end

  def self.down
    remove_column :products, :price
  end
end
```

Download depot_t/db/migrate/20080601000003_add_test_data.rb

```
class AddTestData < ActiveRecord::Migration
  def self.up
    Product.delete_all
    Product.create(:title => 'Pragmatic Project Automation',
      :description =>
        %{
          <p>
            <em>Pragmatic Project Automation</em> shows you how to improve the
            consistency and repeatability of your project's procedures using
            automation to reduce risk and errors.
          </p>
          <p>
            Simply put, we're going to put this thing called a computer to work
            for you doing the mundane (but important) project stuff. That means
            you'll have more time and energy to do the really
            exciting---and difficult---stuff, like writing quality code.
          </p>},
      :image_url => '/images/auto.jpg',
      :price => 29.95)

    Product.create(:title => 'Pragmatic Version Control',
      :description =>
        %{
          <p>
            This book is a recipe-based approach to using Subversion that will
            get you up and running quickly---and correctly. All projects need
```

