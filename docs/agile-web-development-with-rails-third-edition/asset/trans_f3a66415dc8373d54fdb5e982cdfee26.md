

`flash.now` 会创建一条瞬时的 flash 条目，而 `flash.keep` 则相反，它会让当前存在于 flash 中的条目再保留一个请求周期：

```
class SillyController
  def one
    flash[:notice] = "Hello"
    flash[:error] = "Boom!"
    redirect_to :action => "two"
  end

  def two
    flash.keep(:notice)
    flash[:warning] = "Mew!"
    redirect_to :action => "three"
  end

  def three
    # At this point,
    # flash[:notice]     => "Hello"
    # flash[:warning] => "Mew!"
    # and flash[:error] is unset
    render
  end
end
```

如果你没有向 `flash.keep` 传递任何参数，那么所有 flash 内容都会被保留。

Flash 不仅可以存储文本消息——你还可以用它来在动作之间传递各种信息。当然，对于需要长期保存的信息，你通常会使用 session（可能还要结合数据库）来存储数据；但如果只是想将参数从一个请求传递到下一个请求，flash 是非常合适的。

由于 flash 数据存储在 session 中，因此所有常规规则同样适用。特别是，每个对象都必须可序列化。我们强烈建议只在 flash 中传递简单的对象。

## 22.4 过滤器与验证

过滤器允许你在控制器中编写代码来包装动作所执行的处理过程——你可以编写一段代码，然后让它在控制器（或控制器的子类）中的任意多个动作执行之前或之后被调用。这确实是一个非常强大的功能。利用过滤器，我们可以实现身份验证机制、日志记录、响应压缩，甚至响应定制。

Rails 支持三种类型的过滤器：前置（before）、后置（after）和环绕（around）。过滤器会在动作执行之前和/或之后被调用。根据定义方式的不同，它们可以以控制器内方法的形式运行，也可以作为参数传入：

```
# ...

class SomeController < ApplicationController

  before_filter do |controller|
    logger.info("Processing #{controller.action_name}")
  end

  after_filter AuditFilter

  # ...
end
```

默认情况下，过滤器应用于控制器中的所有动作（以及该控制器的任何子类）。你可以通过 `:only` 选项（指定一个或多个需要过滤的动作）和 `:except` 选项（列出需要排除在过滤之外的动作）来修改这一行为。

```
class BlogController < ApplicationController

  before_filter :authorize, :only => [ :delete, :edit_comment ]

  after_filter :log_access, :except => :rss

  # ...
```

### 后置过滤器与响应修改

后置过滤器可用于修改出站响应，在需要时更改响应头和内容。有些应用程序使用这种技术在控制器模板生成的内容中执行全局替换（例如，将响应体中的字符串 `<customer/>` 替换为客户的姓名）。另一个用途是在用户浏览器支持的情况下压缩响应。

下面的代码就是一个示例，展示了这种技术的可能用法。¹⁰ 控制器将 `compress` 方法声明为后置过滤器。该方法会检查请求头，以确定浏览器是否接受压缩响应。如果接受，它就会使用 Zlib 库将响应体压缩成字符串。¹¹ 如果压缩后的字符串比原始响应体更短，它就用压缩版本替换原始内容，并更新响应的编码类型。

10. 这段代码并不是压缩的完整实现。特别是，它不会压缩通过 `send_file` 下载到客户端的流式数据。
11. 请注意，Zlib Ruby 扩展在你的平台上可能不可用——它依赖于底层 `libzlib.a` 库的存在。

例如，下面是一个简单的环绕过滤器，用于记录某个动作执行所花费的时间：

```
Download e1/filter/app/controllers/blog_controller.rb
class BlogController < ApplicationController
  around_filter :time_an_action

  def index
    # ...
    render :text => "hello"
  end

  def bye
    # ...
    render :text => "goodbye"
  end

  private

  def time_an_action
    started = Time.now
    yield
    elapsed = Time.now - started
    logger.info("#{action_name} took #{elapsed} seconds")
  end
end
```

我们将一个方法名 `time_an_action` 传递给 `around_filter` 声明。每当该控制器中的某个动作即将被调用时，这个过滤器方法就会被调用。它记录开始时间，然后第 19 行的 `yield` 语句会调用原始动作。当该动作返回后，它计算并记录在动作中花费的时间。

除了向 `around_filter` 传递方法名之外，你还可以传递一个块或一个过滤器类。

如果你使用块作为过滤器，它会被传入两个参数：控制器对象和一个动作代理。通过对第二个参数调用 `call` 来调用原始动作。例如，下面是上述过滤器的块版本：

```
Download e1/filter/app/controllers/blog_controller.rb
around_filter do |controller, action|
  started = Time.now
  action.call
  elapsed = Time.now - started
  controller.logger.info("#{controller.action_name} took #{elapsed} seconds")
end
```

第三种形式允许你传递一个对象作为过滤器。这个对象应当实现一个名为 `filter` 的方法。该方法会被传入控制器对象。它通过 `yield` 来调用动作。例如，下面将我们的计时过滤器实现为一个类：

```
Download e1/filter/app/controllers/blog_controller.rb
class BlogController < ApplicationController
  class TimingFilter
    def filter(controller)
      started = Time.now
      yield
      elapsed = Time.now - started
      controller.logger.info("#{controller.action_name} took #{elapsed} seconds")
    end
  end
  around_filter TimingFilter.new
end
```

还有一种替代形式的环绕过滤器，你需要传递一个实现了 `before` 和 `after` 方法的对象。这种形式已略有弃用。

与 before 和 after 过滤器一样，环绕过滤器也接受 `:only` 和 `:except` 参数。

环绕过滤器（默认情况下）以不同的方式添加到过滤器链中：第一个添加的环绕过滤器会最先执行。随后添加的环绕过滤器会被嵌套在已有的环绕过滤器内部。因此，给定以下代码：

```
around_filter :one, :two

def one
  logger.info("start one")
  yield
  logger.info("end one")
end

def two
  logger.info("start two")
  yield
  logger.info("end two")
end
```

日志消息的顺序将如下所示：

```
start one
start two
... 
end two
end one
```

这个声明将对 `post_comment` 动作应用验证。如果 session 中不包含 `:user_id` 键，则会向 flash 中添加一条提示信息，并将请求重定向到 `index` 动作。

`verify` 的参数可以分为三类。

### 适用性

这些选项用于选择哪些动作需要进行验证：

- `:only => :name 或 [ :name, ... ]`
  仅验证列出的一个或多个动作。

- `:except => :name 或 [ :name, ... ]`
  验证除列出的动作之外的所有动作。

### 测试条件

这些选项描述了对请求要执行的测试条件。如果指定了多个条件，则所有条件都必须为真，验证才能通过。

- `:flash => :key 或 [ :key, ... ]`
  flash 必须包含给定的一个或多个键。

- `:method => :symbol 或 [ :symbol, ... ]`
  请求方法（`:get`、`:post`、`:head` 或 `:delete`）必须匹配给定的符号之一。

- `:params => :key 或 [ :key, ... ]`
  请求参数必须包含给定的一个或多个键。

- `:session => :key 或 [ :key, ... ]`
  session 必须包含给定的一个或多个键。

- `:xhr => true 或 false`
  请求必须（或必须不）来自 Ajax 调用。

### 动作

这些选项描述了验证失败时应执行的操作。如果未指定任何操作，则验证失败时会向浏览器返回一个空响应。

- `:add_flash => hash`
  将给定的键/值对哈希合并到 flash 中。这可以用于向用户生成错误响应。

- `:add_headers => hash`
  将给定的键/值对哈希合并到响应头中。

