

响应对象，等等。在我们的应用完成处理一个请求后，Rails 会取出响应对象中的信息，并用它向客户端发送响应。

请求和响应对象对于我们功能测试的运行至关重要——使用它们意味着我们不必启动真实的 Web 服务器就可以运行控制器测试。也就是说，功能测试不一定需要 Web 服务器、网络或客户端。

## 索引页：仅供管理员

好的，现在让我们编写第一个控制器测试——一个简单地“访问”索引页面的测试：

```
Download depot_r/test/functional/admin_controller_test.rb

test "index" do
  get :index
  assert_response :success
end
```

`get` 方法是由测试辅助器加载的一个便捷方法，它模拟向 `AdminController` 的 `index` 动作发起一个 Web 请求（可以看作 HTTP GET），并捕获响应。然后，`assert_response` 方法会检查响应是否成功。

好，让我们看看运行这个测试时会发生什么。我们将使用 `-n` 选项来指定要运行的特定测试方法的名称：

```
depot> ruby -I test test/functional/admin_controller_test.rb -n test_index
Loaded suite test/functional/admin_controller_test
Started
F
Finished in 0.239281 seconds.

1) Failure:
test_index(AdminControllerTest)
[test/functional/admin_controller_test.rb:20:in `test_index'
/Library/Ruby/Gems/1.8/ ... /setup_and_teardown.rb:33:in `__send__'
/Library/Ruby/Gems/1.8/ ... /setup_and_teardown.rb:33:in `run']:
Expected response to be a <:success>, but was <302>
```

这看起来很简单，那么发生了什么？响应码 302 表示请求被重定向了，所以它不算成功。但为什么会重定向？因为这就是我们设计 `ApplicationController` 的方式。它使用一个前置过滤器来拦截那些未以管理员身份登录的用户不能访问的动作调用。在这个例子中，前置过滤器确保在 `index` 动作运行之前先执行 `authorize` 方法。

```
class ApplicationController < ActionController::Base
  layout "store"
  before_filter :authorize, :except => :login
  #...

  protected
    def authorize
      unless User.find_by_id(session[:user_id])
        flash[:notice] = "Please log in"
        redirect_to :controller => 'admin', :action => 'login'
      end
    end
end
```

由于我们还没有登录，会话中不存在有效用户，因此请求会被重定向到登录动作。根据 `authorize` 的逻辑，结果页面应该包含一条 *flash* 通知，告诉我们需要登录。好的，让我们重写功能测试来捕获这一流程：

```
test "index without user" do
  get :index
  assert_redirected_to :action => "login"
  assert_equal "Please log in", flash[:notice]
end
```

这一次，当我们请求 index 动作时，预期会被重定向到登录动作，并看到视图生成的 flash 通知：

```
depot> ruby -I test test/functional/admin_controller_test.rb
Loaded suite test/functional/admin_controller_test
Started
.
Finished in 0.0604571 seconds.
1 tests, 2 assertions, 0 failures, 0 errors
```

确实，我们得到了预期结果。⁶ 现在我们知道，在用户登录之前，仅管理员的动作是不可访问的（*前置过滤器*正在起作用）。让我们在拥有有效用户的情况下尝试查看索引页面。

回顾一下，应用会将当前登录用户的 id 存储到会话中，以 `:user_id` 键作为索引。因此，要模拟一个已登录用户，我们只需在发起 index 请求前将一个用户 id 设置到会话中即可。现在唯一的问题是如何确定该使用哪个用户 id。

> ⁶. 取决于你的 Rails 版本，控制台日志可能会显示通过了三个断言。那是因为旧版 Rails 中的 `assert_redirected_to` 方法内部使用了两个底层断言。

我们不能随便塞一个随机数进去，因为应用控制器的 `authorize` 方法会根据它的值从数据库获取对应的用户行。看来我们需要向 users 表中填充一些有效数据。这正好给了我们一个了解动态夹具的机会。

## 动态夹具

我们将创建一个 `users.yml` 测试夹具，向 `users` 表添加一行数据。我们将这个用户命名为 `dave`。

```
dave:
  name: dave
  salt: NaCl
  hashed_password: ???
```

一切都很顺利，直到 `hashed_password` 这一行。我们应该用什么作为值？在真实表中，这个值是使用 User 类中的 `encrypted_password` 方法计算出来的。该方法接收一个明文密码和一个盐值，并创建一个 SHA1 哈希值。

一种办法是启动 `script/console` 并手动调用该方法。然后我们可以复制该方法返回的值，粘贴到夹具文件中。这样可行，但有点晦涩，而且如果我们更改密码生成机制，测试可能会失败。如果能在数据加载到数据库时，使用应用程序的代码生成哈希密码，岂不是很好？那么，请看下面的内容：

```
<% SALT = "NaCl" unless defined?(SALT) %>
```

```
dave:
  name: dave
  salt: <%= SALT %>
  hashed_password: <%= User.encrypted_password('secret', SALT) %>
```

`hashed_password` 这一行的语法应该看起来很眼熟：`<%=...%>` 指令与我们在模板中替换值所用的指令相同。事实证明，Rails 在测试夹具中也支持这些替换。这就是为什么我们称它们为动态夹具。

现在我们可以再次测试 `index` 动作了。我们必须记得在 admin 控制器测试类中添加 `fixtures` 指令：

```
fixtures :users
```

然后我们编写测试方法：

```
test "index with user" do
  get :index, {}, { :user_id => users(:dave).id }
  assert_response :success
  assert_template "index"
end
```

这里的关键概念是 `get` 方法的调用。注意，我们在动作名称后面添加了几个新参数。参数 2 是一个空哈希——表示要传递给动作的参数。参数 3 是一个用于填充会话数据的哈希。这里我们使用了自己的用户夹具，将会话条目 `:user_id` 设置为测试用户的 id。然后我们的测试断言响应成功（而非重定向），并且动作渲染了 `index` 模板。（我们稍后会更深入地讨论所有这些断言。）

## 登录

现在测试数据库中已经有了一个用户，让我们看看能否以该用户身份登录。如果使用浏览器，我们会导航到登录表单，输入用户名和密码，然后将这些字段提交给 admin 控制器的 `login` 动作。我们预期会被重定向到 index 列表页，并且会话中妥善地存放着测试用户的 id。下面是在功能测试中实现这一过程的代码：

```
Download depot_r/test/functional/admin_controller_test.rb

test "login" do
  dave = users(:dave)
  post :login, :name => dave.name, :password => 'secret'
  assert_redirected_to :action => "index"
  assert_equal dave.id, session[:user_id]
end
```

这里我们使用了 `post` 方法来模拟提交表单数据，并将 `name` 和 `password` 表单字段的值作为参数传递。

如果我们尝试使用无效密码登录，会发生什么？

```
Download depot_r/test/functional/admin_controller_test.rb

test "bad password" do
  dave = users(:dave)
  post :login, :name => dave.name, :password => 'wrong'
  assert_template "login"
end
```

不出所料，测试用户没有被重定向到 index 列表页，而是再次看到了登录表单。

## 功能测试的便捷功能

以上是对如何为控制器编写功能测试的一次简短浏览。在此期间，我们使用了 Rails 自带的许多辅助方法和断言，它们能让你的测试工作更轻松。在我们继续深入之前，现在来仔细看看 Rails 专为测试控制器提供的一些便捷功能。

### assert_dom_not_equal(expected_html, actual_html, message)

比较两个包含 HTML 的字符串，如果它们由同一个文档对象模型表示/不由同一个文档对象模型表示，则断言成功。由于该断言会比较两个字符串的完整（规范化）版本，因此面对应用变更时它很脆弱。请考虑改用 `assert_select`。

```
expected = "<html><body><h1>User Unknown</h1></body></html>"
assert_dom_equal(expected, @response.body)
```

### assert_response(type, message)

断言响应是一个数字 HTTP 状态码，或是以下符号之一。其中一些符号涵盖一段响应码范围（例如，`:redirect` 表示状态码 300–399）。

- :accepted – 202
- :bad_gateway – 502
- :bad_request – 400
- :conflict – 409
- :continue – 100
- :created – 201
- :error – 500–599
- :expectation_failed – 417
- :failed_dependency – 424
- :forbidden – 403
- :found – 302
- :gateway_timeout – 504
- :gone – 410
- :http_version_not_supported – 505
- :im_used – 226
- :insufficient_storage – 507
- :internal_server_error – 500
- :length_required – 411
- :locked – 423
- :method_not_allowed – 405
- :missing – 404
- :moved_permanently – 301
- :multi_status – 207
- :multiple_choices – 300
- :no_content – 204
- :non_authoritative_information – 203
- :not_acceptable – 406

