
```
create  app/helpers
create  app/models
:       :       :
create  log/development.log
create  log/test.log
work>
```

该命令创建了一个名为 demo 的目录。进入该目录并列出其内容（在 Unix 上使用 `ls`，在 Windows 下使用 `dir`）。你会看到一批文件和子目录：

```
work> cd demo
demo> ls -p
README           config/      lib/         script/      vendor/
Rakefile         db/          log/         test/
app/             doc/         public/      tmp/
```

所有这些目录（及其包含的文件）起初可能让人望而生畏，但我们现在可以先忽略其中大部分。在本章中，我们只会直接用到其中两个：`app` 目录，用于编写我们的应用程序；以及 `script` 目录，其中包含一些有用的实用脚本。

让我们从 `script` 子目录开始。其中包含的一个脚本名为 `server`。这个脚本会启动一个独立的 Web 服务器，可以在 WEBrick 下运行我们新创建的 Rails 应用程序。² 闲话少说，让我们启动演示应用程序：

```
demo> ruby script/server
=> Booting WEBrick...
=> Rails application started on http://0.0.0:3000
=> Ctrl-C to shutdown server; call with --help for options
[2006-01-08 21:44:10] INFO  WEBrick 1.3.1
[2006-01-08 21:44:10] INFO  ruby 1.8.2 (2004-12-30) [powerpc-darwin8.2.0]
[2006-01-08 21:44:11] INFO  WEBrick::HTTPServer#start: pid=10138 port=3000
```

正如启动跟踪信息的最后一行所示，我们刚刚在 3000 端口启动了一个 Web 服务器。³ 通过在浏览器中指向 URL http://localhost:3000，我们可以访问该应用程序。结果如图 4.1 所示。

如果你查看启动 WEBrick 的那个窗口，你会看到显示你正在访问该应用程序的跟踪信息。我们将让 WEBrick 在这个控制台窗口中继续运行。稍后，当我们编写应用程序代码并通过浏览器运行它时，

> 2. WEBrick 是一个纯 Ruby 编写的 Web 服务器，随 Ruby 1.8.1 及更高版本一起分发。由于它保证可用，Rails 将其用作开发 Web 服务器。然而，如果你的系统安装了 Mongrel Web 服务器（且 Rails 能找到它），`script/server` 命令将优先使用它而不是 WEBrick。你可以通过向以下命令提供一个选项来强制 Rails 使用 WEBrick：
> `demo>ruby script/server webrick`

> 3. 地址中的 0.0.0.0 部分表示 WEBrick 将接受所有接口上的连接。在 Dave 的 OS X 系统上，这意味着两个本地接口（127.0.0.1 和 ::1）以及他的局域网连接。

![](img/a160fc3a330a0b3b2a764d41d614e688_45_0.png)

# 图 4.1：新创建的 Rails 应用程序

此时，我们有一个新应用程序在运行，但它还没有包含我们的任何代码。让我们来纠正这种情况。

## 4.2 你好，Rails！

我们忍不住——我们就是要写一个 “Hello, World!” 程序来尝试新系统。在 Rails 中，这相当于一个向浏览器发送我们欢快问候的应用程序。

正如我们在第 2 章 “Rails 应用程序架构”（第 22 页）中所见，Rails 是一个模型-视图-控制器框架。Rails 接受来自浏览器的传入请求，解码请求以找到控制器，并在该控制器中调用动作方法。然后控制器调用一个特定的视图来向用户显示结果。好消息是，Rails 处理了连接所有这些动作的大部分内部管道代码。要编写我们简单的 “Hello, World!” 应用程序，我们需要控制器和视图的代码。我们不需要模型的代码，因为我们不处理任何数据。让我们从控制器开始。

与我们使用 `rails` 命令创建新的 Rails 应用程序的方式相同，我们也可以使用生成器脚本为项目创建新的控制器。这个命令称为 `generate`，它位于我们创建的 demo 项目的 `script` 子目录中。因此，要创建一个名为 Say 的控制器，我们要确保在 demo 目录中，然后运行该脚本，并传入我们要创建的控制器名称。⁴

```
demo> ruby script/generate controller Say
exists  app/controllers/
exists  app/helpers/
create  app/views/say
exists  test/functional/
create  app/controllers/say_controller.rb
create  test/functional/say_controller_test.rb
create  app/helpers/say_helper.rb
```

该脚本会记录它检查的文件和目录，并注明何时向你的应用程序添加新的 Ruby 脚本或目录。目前，我们只对其中一个脚本以及（稍后）新的目录感兴趣。

我们将要查看的源文件是控制器。你可以在 `app/controllers/say_controller.rb` 文件中找到它。让我们来看一下：

```
Download work/demo1/app/controllers/say_controller.rb
```

```
class SayController < ApplicationController
end
```

相当简洁，是吧？SayController 是一个继承自 ApplicationController 的空类，因此它自动获得所有默认的控制器行为。让我们把它变得更有趣。我们需要添加一些代码，让我们的控制器处理传入的请求。这些代码需要做什么？目前它什么都不用做——我们只需要一个空的动作方法。那么，下一个问题是，这个方法应该叫什么？为了回答这个问题，我们需要看看 Rails 处理请求的方式。

### Rails 与请求 URL

与任何其他 Web 应用程序一样，Rails 应用程序在用户看来与一个 URL 相关联。当你在浏览器中访问该 URL 时，你是在与应用程序代码通信，它会为你生成响应。

然而，实际情况要比这复杂一些。假设你的应用程序可以通过 URL http://pragprog.com/ 访问。托管你应用程序的 Web 服务器对路径相当智能。它知道发送到该 URL 的传入请求必定是在与应用程序通信。传入 URL 中超过此处的任何内容都不会改变这一点——同一个应用程序仍会被调用。任何额外的路径信息都会传递给应用程序，应用程序可将其用于自身的内部目的。

Rails 使用路径来确定要使用的控制器名称以及要在该控制器上调用的动作名称。⁵ 图 4.2 展示了这一点。路径的第一部分是控制器名称，路径的第二部分是动作名称。这显示在下一页的图 4.3 中。

![](img/a160fc3a330a0b3b2a764d41d614e688_47_0.png)

图 4.2：URL 被映射到控制器和动作。

### 我们的第一个动作

让我们为 Say 控制器添加一个名为 hello 的动作。从前面的讨论中我们知道，添加 hello 动作意味着在 SayController 类中创建一个名为 hello 的方法。但它应该做什么呢？目前，它不需要做任何事情。请记住，控制器的工作是设置好相关事务，以便视图知道要显示什么。在我们的第一个应用程序中，没有什么需要设置的，因此空动作就可以了。使用你喜欢的编辑器修改 `app/controllers` 目录中的 `say_controller.rb` 文件，添加如下所示的 `hello` 方法，然后保存文件：

```
Download work/demo1/app/controllers/say_controller.rb
class SayController < ApplicationController
  def hello
  end
end
```

> 5. Rails 在解析传入 URL 时相当灵活。在本章中，我们描述默认机制。我们将在第 426 页的 21.2 节 “路由请求” 中展示如何覆盖此机制。

http://pragprog.com/say/hello

创建 SayController 的一个实例，并调用动作方法 hello

```
class UserController
```

```
class SayController
```

```
class ProductController
```

```
class LoginController
  def login
    # code . . .
  end
end
```

```
class SayController
  def hello
    # code for hello action
  end
end
```

图 4.3：Rails 路由到控制器和动作。

现在让我们尝试调用它。在浏览器窗口中导航到 URL http://localhost:3000/say/hello。（注意，在开发环境中，路径前面没有任何应用程序字符串——我们直接路由到控制器。）你会看到类似下面的内容：⁶

![](img/a160fc3a330a0b3b2a764d41d614e688_48_0.png)

这可能令人烦恼，但这个错误完全合理（除了奇怪的路径）。我们创建了控制器类和动作方法，但还没有告诉 Rails 要显示什么。而这正是视图发挥作用的地方。还记得我们运行脚本创建新控制器的时候吗？该命令添加了

> 6. 如果你反而看到类似 “No route matches "/say/hello"” 的消息，请尝试停止并重新启动服务器，因为你所做的一些事情导致 Rails 在控制器创建之前缓存了配置信息。
