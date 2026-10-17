
让我们来拆解一下。`assert_response` 验证 Rails 发送到浏览器的响应码。通常，测试的预期值是 `:success`（意味着代码 200），或 `:redirect`（匹配 300--399 范围内的任何值，表示某种形式的重定向）。其他特殊值还包括 `:missing`（匹配 404 错误）和 `:error`（匹配 500--599 错误范围）。除了特殊值外，预期的断言也可以是预期响应的精确整数。单个响应码也有它们自己的（尽管很少使用）符号等价物。

`assert_template` 验证用于渲染响应的模板。

（注：原文此处似乎存在部分重复或缺失的逻辑断层，已按字意翻译）

这可能在安全测试中成为一个问题。如果控制器看起来如下：

```ruby
def create
  if current_user.id == params[:id]
    # 允许
  else
    # 拒绝
  end
end
```

而测试看起来如下：

```ruby
test "I can create" do
  login_as(@user)
  put :create, @user.id
  assert that allowed branch was taken
end
```

测试将通过，因为测试中的 `params[:id]` 是整数，但 `create` 在浏览器中会失败，因为它是字符串。解决方法是确保测试值在测试中转换为字符串。一个建议是使用 `@user.to_param` 作为 `put` 的参数；这种方法比 `@user.id.to_s` 更好，因为如果你以后重写了 `to_param` 方法，它会为你提供灵活性。

## 测试文件上传

当你想要在测试中伪造文件上传时，Rails 提供了 `fixture_file_upload` 辅助方法来帮助。它接受两个参数：一个相对于 Rails 根目录的实际文件路径和一个 MIME 类型。你将它作为传递给控制器测试中 Rails 方法的键/值对的值部分，例如 `post :upload_icon, :icon => fixture_file_upload('/public/images/test_icon.png', 'image/png')`。控制器处理该值就像它是一个已上传的文件。

## 测试控制器响应

你在控制器方法中通常想要验证的最点是它返回了 HTTP 状态码，并且由相应的 Rails 模板负责返回响应。Rails 提供了三个断言方法来帮助：`assert_redirected_to`、`assert_response` 和 `assert_template`。

当你预期的是正常的 HTTP 响应而不是重定向时，你可以通过 `assert_response` 和 `assert_template` 的组合在测试中指示你的预期，如下：

```ruby
test "successful index request" do
  get :index
  assert_response success
  assert_template "index"
end
```

让我们来拆解一下。`assert_response` 验证 Rails 发送到浏览器的响应码。通常，测试的预期值是 `:success`（意味着代码 200），或 `:redirect`（匹配 300--399 范围内的任何值，表示某种形式的重定向）。其他特殊值还包括 `:missing`（匹配 404 错误）和 `:error`（匹配 500--599 错误范围）。除了特殊值外，预期的断言也可以是预期响应的精确整数。单个响应码也有它们自己的（尽管很少使用）符号等价物。

`assert_template` 验证用于渲染响应的模板。

## 存根与模拟

存根函数（Stub function）。绕过真实的 `find` 方法，使得对象接收到 `find(1)` 调用时，它将返回任务而不调用实际的 `Task.find` 方法。注意，这完全跳过了数据库访问。

模拟函数（Mock function）。设置一个期望，即在此测试期间 `find(1)` 将恰好调用一次。如果该方法没有被调用，测试将失败。

这样做的结果是，你可以控制控制器的行为，而无需担心模型实现的细节——事实上，你甚至可以在模型方法编写之前就控制控制器。但这也有一个缺点，是任何模拟测试的共性问题：设置模拟对象可能非常耗时且脆弱（brittle），如果你从模拟中返回的对象与真实方法不匹配，你可能会掩盖控制器或视图中的错误。

一种折中方案是使用“观察者（Spy）”的概念，Double Ruby 模拟对象框架允许这种用法。[48]。本质上，你可以识别出感兴趣的模型方法，然后设置一个断言，确认该方法确实被调用过。在 Double Ruby 语法中，测试可能看起来如下：

```ruby
test "should show task" do
  stub.proxy(Task).find('1')
  get.show,~id => 1
  assert_response :success
  assert_received(Task) { |t| t.find('1') }
  assert_equal task, assigns(task)
end
```

这段代码片段中只有两行的特殊的。在第二行中，创建了一个名为代理（proxy）的特殊 Double Ruby 结构。基本上，这只是正常调用该方法，但将该方法标记为 Double Ruby 需要跟踪的对象。[49]。由于 Double Ruby 现在正在跟踪方法的调用，你可以根据方法的调用次数进行断言，在本例中是断言 `Task` 确实接收到了 `find('1')` 方法调用。我认为这是一个在真实模拟与在控制器中实际测试模型之间取得平衡的好方法。

关于模拟对象测试的成本与收益，在“使用模拟对象”章节中有更多介绍。此外，请参阅“存根（Stubs）”章节，了解有关如何使用模拟对象来提高标准 Rails 脚手架生成的代码中失败状态测试覆盖率的描述。

# 路由的测试

Rails 路由的基础非常简单，但自定义 Rails 对 URL 响应的愿望导致人们在 URL 与 Rails action 之间转换时，对应用程序具体会做什么感到困惑。Rails 提供了两个核心方法，可以使用它们来指定或验证路由行为。

两个 Rails 方法 `assert_generates` 和 `assert_recognizes` 是互为镜像的。让我们按照字母顺序来看它们。

`assert_generates` 方法接受一个预期的路径字符串作为第一个元素，接受一个键值对哈希（hash）作为第二个元素。如果 Rails 路由器会将这些键值对转换为预期的字符串，则测试通过——它是在进行字符串比较。这里有一个来自 Huddle 的示例：

```ruby
assert_generates /status_reports/,
{:controller => "status_reports", :action => "show", id => "/"}
```

在这种情况下，Rails 针对哈希运行路由器，并将其与字符串进行比较。

反方法 `assert_recognizes` 翻转了参数的顺序，也翻转了执行逻辑。

```ruby
assert_recognizes {:controller => "status_reports",
:action => "show", id => "/"}, /status_reports/
```

在这种情况下，第二个参数将通过 Rails 路由器运行，其转换出的参数将与第一个参数中的哈希进行比较。

`assert_recognizes` 的参数具有稍微更大的活性。第二个参数也可以是一个包含两个键的哈希：`:path`键和`:method`键，这允许你像这样测试 RESTful 路由：

```ruby
assert_recognizes {:controller => "status_reports",
:action => "update", id => "/",
{:path => "/status_reports/", :method => :put}
```
