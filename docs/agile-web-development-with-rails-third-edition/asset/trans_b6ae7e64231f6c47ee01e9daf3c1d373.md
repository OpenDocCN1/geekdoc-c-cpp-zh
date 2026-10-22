

![](img/a160fc3a330a0b3b2a764d41d614e688_103_0.png)

## Figure 7.3: 现在有一个加入购物车按钮。

- 修改应用程序，使点击图书的图像也会调用尚未编写的 add_to_cart 动作。提示：link_to 的第一个参数会放在生成的 <a> 标签中，而 Rails 辅助方法 image_tag 会构造一个 HTML <img> 标签。将对其的调用作为 link_to 调用的第一个参数包含在内。确保在对 link_to 的调用中，在你的 html_options 中包含 :method => :post。
- number_to_currency 辅助方法的完整描述如下：

```
number_to_currency(number, options = {})
```

将数字格式化为货币字符串。options 哈希可用于自定义输出格式。数字可以使用 :precision 键包含精度级别；默认值为 2。货币类型可以使用 :unit 键设置（默认 "$"）。单位分隔符可以使用 :separator 键设置（默认 "."）。分隔符可以使用 :delimiter 键设置（默认 ","）。

```
number_to_currency(1234567890.50)          -> $1,234,567,890.50
number_to_currency(1234567890.506)         -> $1,234,567,890.51
number_to_currency(1234567890.50, :unit => "&pound;",
                    :separator => ",", :delimiter => "")
                    -> &pound;1234567890,50
```

尝试设置各种选项，并观察对你的目录列表的影响。

（你会在 http://pragprog.wikidot.com/rails-play-time. 上找到提示。）

实现此会话跟踪的底层机制各不相同。有时应用程序会在每个页面的表单数据中编码会话信息。有时编码后的会话标识符会添加到每个 URL 的末尾（所谓的 URL 重写选项）。有时应用程序使用 cookie。Rails 使用基于 cookie 的方法。

cookie 只是一块由 Web 应用程序传递给 Web 浏览器的命名数据。浏览器会记住它。此后，当浏览器向应用程序发送请求时，cookie 数据会随之发送。应用程序使用 cookie 中的信息将请求与服务器上存储的会话信息匹配起来。这是对一个混乱问题的丑陋解决方案。幸运的是，作为 Rails 程序员，你不必担心所有这些低级细节。事实上，唯一需要深入了解这些细节的原因是为了解释为什么 Rails 应用程序的用户必须在浏览器中启用 cookie。

与其让开发人员担心协议和 cookie，Rails 提供了一个简单的抽象。在控制器内部，Rails 维护一个特殊的类似哈希的集合，称为 session。你在处理请求期间存储在此哈希中的任何键/值对，都将在同一浏览器的后续请求中可用。

在 Depot 应用程序中，我们希望使用会话功能来存储每个买家购物车中的信息。但我们在这里必须稍微小心一点——这个问题比看起来要深。存在弹性和可扩展性的问题。

一种选择是将会话信息存储在服务器上的文件中。如果你运行单个 Rails 服务器，这没有问题。但想象一下，你的商店应用程序变得如此流行，以至于单台服务器机器的容量用尽，你需要运行多台机器。来自特定用户的第一个请求可能被路由到一台后端机器，但第二个请求可能转到另一台。存储在第一台服务器上的会话数据在第二台服务器上不可用；用户会在请求之间看到购物车中的商品出现和消失，从而感到非常困惑。

因此，最好确保会话信息存储在应用程序外部的某个地方，以便在需要时可以在多个应用程序进程之间共享。而且如果此外部存储是持久的，我们甚至可以重启服务器而不会丢失任何会话信息。我们在第 22.2 节 Rails Sessions，第 477 页中讨论了设置会话信息的所有内容，我们会看到有许多不同的会话存储选项。现在，让我们安排我们的应用程序将会话数据存储在数据库中的一张表中。

## 将会话放入数据库

Rails 使将会话数据存储在数据库中变得很容易。我们需要运行几个 Rake 任务来创建具有正确布局的数据库表。

首先，我们将创建一个包含会话表定义的迁移。有预定义的 Rake 任务可以创建我们需要的迁移：

```
depot> rake db:sessions:create
exists  db/migrate
create  db/migrate/20080601000004_create_sessions.rb
```

然后，我们将应用迁移以将表添加到我们的模式中：

```
depot> rake db:migrate
```

如果现在查看你的数据库，你会发现一个名为 sessions 的新表。

接下来，我们必须告诉 Rails 对我们的应用程序会话使用数据库存储（默认是存储在 cookie 中）。这是一个配置选项，因此不出所料，你会在 config 目录中的一个文件中找到它的指定。打开文件 environment.rb，你会看到一堆配置选项，都被注释掉了。向下扫描，找到看起来像这样的选项：¹

```
# Use the database for sessions instead of the cookie-based default,
# which shouldn't be used to store highly confidential information
# (create the session table with 'rake db:sessions:create')
# config.action_controller.session_store = :active_record_store
```

请注意，最后一条语句被注释掉了。删除该行开头的 # 字符以激活数据库会话存储：

```
# Use the database for sessions instead of the cookie-based default,
# which shouldn't be used to store highly confidential information
# (create the session table with 'rake db:sessions:create')
config.action_controller.session_store = :active_record_store
```

## 会话与浏览器

正如我们所讨论的，Rails 会话的默认实现是使用 cookie 在用户浏览器上存储会话 id。当来自该浏览器的请求进来时，Rails 提取会话 id 并使用它从（在我们的例子中）数据库中检索会话数据。但这里有一个重要的细微差别：cookie 是由服务器主机名和 cookie 名称共同存储在浏览器上的。如果你在一台服务器上运行两个不同的应用程序，你可能希望它们使用不同的 cookie 名称来存储其会话键。如果不这样做，它们会相互干扰。

幸运的是，Rails 处理了这个问题。当你使用 rails 命令创建一个新应用程序时，它会为存储会话 id 的 cookie 建立一个名称。此名称包含你的应用程序的名称。

1. 在 Rails 2.3 中，你需要在 config/initializers/session_store.rb 中查找 ActionController::Base.session_store 的设置。

事实证明，在 Ruby 中有一种更地道的方式来做同样的事情：

```
private

  def find_cart
    session[:cart] ||= Cart.new
  end
```

此方法相当棘手。它使用 Ruby 的条件赋值运算符，||= 。如果 session 哈希具有对应于键 :cart 的值，则立即返回该值。否则，将创建一个新的 Cart 对象并分配给 session。此新 Cart 然后被返回。

请注意，我们将 find_cart 方法设为 private。这可以防止 Rails 将其作为控制器上的操作公开。当我们进一步处理购物车时，请小心向此控制器添加方法——如果你在 private 声明之后添加它们，它们在类外部将不可见。新的操作必须放在 private 行之前。

## 8.2 迭代 C1：创建购物车

我们查看会话是因为我们需要一个地方来保存我们的购物车。我们已经解决了会话问题，所以让我们继续实现购物车。现在，让我们保持简单。它保存数据并包含一些业务逻辑，因此我们知道它在逻辑上是一个模型。但是，我们需要购物车数据库表吗？不一定。购物车与买家的会话绑定，只要该会话数据在所有服务器上可用（当我们最终在多服务器环境中部署时），这可能就足够了。所以现在，我们假设购物车是一个常规类，看看会发生什么。我们将使用编辑器在 app/models 目录中创建文件 cart.rb。³ 实现很简单。购物车基本上是项目数组的包装器。当添加产品（使用 add_product 方法）时，它会被附加到项目列表中：

```
class Cart
  attr_reader :items

  def initialize
    @items = []
  end

  def add_product(product)
    @items << product
  end
end
```

3. 请注意，我们不使用 Rails 模型生成器来创建此文件。生成器仅用于创建基于数据库的模型。

