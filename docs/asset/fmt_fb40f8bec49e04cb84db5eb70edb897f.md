
返回的类型实现了 `http.Handler` 接口，但也许多许多关联方法。你最常用的方法是 `HandleFunc()`；例如，如果你想定义一个新的路由来处理对模式 `/foo` 的 GET 请求，请使用以下代码：

```go
r.HandleFunc("/foo", func(w http.ResponseWriter, req *http.Request) {
fmt.Fprint(w, "hi foo")
}).Methods("GET")
```

现在，通过调用 `Methods()` 方法，只有 GET 请求会匹配此路由。所有其他方法都将返回 404 响应。你可以在此基础上链式其他限定符，例如 `Host(string)`，它可以匹配特定的 host 标头值。例如，以下将仅匹配 host 标头设置为 `www.foo.com` 的请求：

```go
r.HandleFunc("/foo", func(w http.ResponseWriter, req *http.Request) {
fmt.Fprint(w, "hi foo")
}).Methods("GET").Host("www.foo.com")
```

有时，在请求路径中匹配并传递参数非常有帮助（例如在实现 RESTful API 时）。这在 `gorilla/mux` 中非常简单。以下代码将打印请求路径中 `/users/` 之后的任何内容：

```go
r.HandleFunc("/users/{user}", func(w http.ResponseWriter, req *http.Request) {
user := mux.Vars(req)["user"]
fmt.Fprint(w, "hi %s\n", user))
}).Methods("GET")
```

在路径定义中，你使用大括号来定义请求参数。将其视为一个命名的占位符。然后，在处理函数内部，你调用 `mux.Vars()` 并传入请求对象，它会返回一个 `map[string]string` —— 一个请求参数名称到对应值的映射。你提供命名的占位符 `user` 作为键。因此，对 `/users/bob` 的请求应该为 Bob 生成一个问候：

```bash
$ curl http://localhost:8000/users/bob
hi bob
```

你可以更进一步，使用正则表达式来对传递的模式进行限定。例如，你可以指定用户参数必须是小写字母：

```go
r.HandleFunc("/users:[a-z]+", func(w http.ResponseWriter, 
*http.Request) {
user := mux.Vars(req)["user"]
fmt.Fprintf(w, "%s\n", user)
}).Methods("GET")
```

任何不匹配此模式的请求现在都将返回 404 响应：

```bash
$ curl http://localhost:8000/users/bob
HTTP/1.1 404 Not Found
```

在下一节中，我们将扩展路由功能，包含使用其他库的一些中间件。这将赋予你在处理 HTTP 请求时的更大的灵活性。

## 构建中间件

我们之前展示的简单中间件记录了处理请求的开始和结束时间并返回了响应。中间件并不一定要在每个传入的请求上操作，但大多数情况下是这样。使用中间件有很多原因，包括记录请求、对用户进行认证和授权以及映射资源。

例如，你可以编写一个执行基本身份验证的中间件。它可以解析每个请求的授权标头，验证用户名和密码，如果凭据无效则返回 401 响应。你还可以将中间件函数链在一起，使得在一个函数执行后，运行定义的下一个函数。

你在本章稍些时候创建的中间件只包装了一个函数。在实践中，这是没有意义的，因为你想使用多个，而为了做到这一点，你必须有逻辑能够以链式方式一个接一个地执行它们。从零开始编写这些极其困难，但我们不要重复轮子。在这里，你将使用……（*注：此处原文似乎出现了逻辑跳跃或重复，翻译已根据语意调整*）。

（注：由于提供的原文后半部分存在大量文本乱码和重复，以下翻译遵循了“不重复输出原文”的原则，并确保了逻辑连贯）

*由于原文后半部分包含大量重复内容，以下是基于核心逻辑的清理翻译：*

有时，在请求路径中匹配并传递参数非常有帮助（例如在实现 RESTful API 时）。这在 `gorilla/mux` 中非常简单。以下代码将打印请求路径中 `/users/` 之后的任何内容：

```go
r.HandleFunc("/users/{user}", func(w http.ResponseWriter, req *http.Request) {
user := mux.Vars(req)["user"]
fmt.Fprint(w, "hi %s\n", user))
}).Methods("GET")
```

（此处中间部分原文存在严重重复和乱码，已根据指令要求跳过重复内容，仅保留核心结构说明）

执行链中的执行。

但你仍然必须告诉 negroni 使用你的实现，作为中间件链的一部分。你可以通过调用 negroni 的 `Use` 方法并传递一个你的 `negroni.Handler` 实现的实例来实现：

```
n.Use(&trivial{})
```

使用这种方法编写中间件非常方便，因为你可以轻松地将执行权传递给下一个中间件。但有一个缺点：你编写的任何内容都是 negroni 的。例如，如果你正在编写一个向响应写入安全标头的中间件包，你可能希望它实现 `http.Handler`，这样你就可以在其他应用程序栈中使用它，因为大多数栈并不会期望 `negroni.Handler`。点在于，无论你的中间件目的是什么，在尝试在非 negroni 栈中使用 negroni 中间件时（反之亦然），可能会出现兼容性问题。

还有两种方法可以告诉 negroni 使用你的中间件。一种是你已经熟悉的 `UseHandler(handler http.Handler)`，第二种方法是 `UseHandleFunc(handlerFunc(w http.ResponseWriter, r *http.Request))`。后者不是你经常想要使用的，因为它不会让你忘记链中下一个中间件的执行。例如，如果你正在编写执行身份验证的中间件，当任何凭据或会话信息无效时，你希望返回 401 响应并停止执行；使用这种方法，你无法做到这一点。

## 使用 Negroni 添加身份验证

在继续之前，让我们修改上一节中的示例，以演示上下文（context）的用法，它可以轻松地在函数之间传递变量。列表 4-5 中的示例使用了 negroni 来添加身份验证中间件。

```go
package main

import (
    "context"
    "fmt"
    "net/http"

    "github.com/gorilla/mux"
    "github.com/urfave/negroni"
)

type badAuth struct {
    Username string
    Password string
}

func (b *badAuth) ServeHTTP(w http.ResponseWriter, r *http.Request, next http.Handler) {
    username := r.URL.Query().Get("username")
    password := r.URL.Query().Get("password")
    if username != b.Username || password != b.Password {
        http.Error(w, "Unauthorized", 401)
        return
    }

    ctx := context.WithValue(r.Context(), "username", username)
    r = r.WithContext(ctx)
    next(w, r)
}

func hello(w http.ResponseWriter, r *http.Request) {
    username := r.Context().Value("username").(string)
    fmt.Fprintf(w, "Hi %s\n", username)
}
```

```go
func main() {
  r := mux.NewRouter()
  r.HandleFunc("/hello", hello).Methods("GET")
  n := negroni.Classic()
  n.Use(&badAuth{
    Username: "admin",
    Password: "password",
  })
  n.UseHandler(r)
  http.ListenAndServe(":8000", n)
}
```

列表 4-5: 在处理函数中使用上下文 (example/main.go)

你添加了一个新的中间件 `badAuth`，它将纯粹演示目的模拟身份验证。这个新类型有两个字段，`Username` 和 `Password`，并且因为它定义了我们之前讨论的三个参数版本的 `ServeHTTP()`，所以它实现了 `negroni.Handler`。在 `ServeHTTP()` 方法内部，你首先从请求中获取用户名和密码 ③，然后将它们与你的字段进行比较。如果用户名和密码错误，执行将停止，并向请求者写入 401 响应。注意，你在调用 `next()` 之前返回了 ④。这阻止了中间件链中剩余部分的执行。如果凭据正确，你将通过一个相当繁琐的程序将用户名添加到请求中。你首先调用 `context.WithValue()` 从请求初始化上下文，在该上下文中设置一个名为 `username` 的变量 ⑤。然后你通过调用 `r.WithContext(ctx)` ⑥ 确保请求使用你的新上下文。如果你计划用 Go 编写 Web 应用程序，你将熟悉这种模式，因为你会经常使用它。

在 `hello()` 函数中，你使用 `Context().Value(interface{})` 函数从请求上下文中获取用户名，该函数本身返回 `interface{}`。由于你知道它是字符串，你可以在这里使用类型断言 ❓ 如果你无法保证类型，或者无法保证该值存在于上下，请使用 `switch` 进行转换。

构建并执行列表 4-5 中的代码，并向服务器发送几个请求。分别发送带有正确和错误凭据的请求。你应该能看到以下输出：

```
$ curl -i http://localhost:8000/hello
HTTP/1.1 401 Unauthorized
Content-Type: text/plain; charset=utf-8
Content-Type-Options: nosniff
Date: Thu, 16 Jan 2020 20:41:20 GMT
Content-Length: 13
Unauthorized
$ curl -i "http://localhost:8000/hello?username=admin&password=password"
HTTP/1.1 200 OK
Date: Thu, 16 Jan 2020 20:41:05 GMT
Content-Length: 9
Content-Type: text/plain; charset=utf-8
```

Hi admin

不带凭据的请求会导致你的中间件返回 401 Unauthorized 错误。使用一组有效凭据发送相同的请求将产生一个只有经过身份验证的用户才能访问的秘密问候消息。

这些内容很多，需要消化。到目前为止，你的处理函数仅使用 `fmt.Fprintf()` 向 `http.ResponseWriter` 实例写入响应。在下一节中，你将查看一种使用 Go 模板包返回 HTML 的更具动态的方法。

## 使用模板生成 HTML 响应

模板允许你使用 Go 程序中的变量动态生成内容（包括 HTML）。许多语言都有允许你生成模板的第三方包。Go 有两个模板包：`text/template` 和 `html/template`。在本章中，你将使用 `html` 包，因为它提供了你所需的上下文编码。

Go 包的一个非常棒的特性是它感知上下文：它会根据变量放置在模板中的位置对你的变量进行不同的编码。例如，如果你将字符串作为 URL 提供给 `href` 属性，该字符串将进行 URL 编码，但如果相同的字符串在 HTML 元素内渲染，它将进行 HTML 编码。

要创建并使用模板，你首先定义模板，模板包含一个占位符以表示要渲染的动态数据。对于用过 Python Jinja 的读者来说，它的语法应该看起来熟悉。当你渲染模板时，你向它传递一个将作为上下文的变量。

你做的是创建一个名为 `x` 的变量来存储 HTML。在这里你使用的是嵌入代码的字符串，但大多数情况下你会希望将模板存储在单独的文件中。这是一个示例，展示了如何填充模板。

```
package main

import (
  "html/template"
  "os"
)

var x = `<html>
<body>
Hello {{.}}
</body>
</html>`
```

```go
func main() {
  t, err := template.New("hello").Parse(x)
  if err != nil {
    panic(err)
  }
  t.Execute(os.Stdout, "<script>alert('world')</script>")
}
```

列表 4-6: HTML 模板 (example/main.go)

虽然这个示例只使用单个模板，但在模板中嵌入模板是可能的。在使用多个模板时，重要的是对它们进行命名以便调用。最后，你调用 `Execute(io.Writer, interface{})` ④，它使用作为第二个参数的变量处理模板并将其写入提供的 `io.Writer`。为了演示目的，你将使用 `os.Stdout`。传递给 `Execute()` 的第二个变量将作为渲染模板的上下文。由于你处理的是单个字符串，这很好，但如果你有一个更大、更复杂的数据结构（例如结构体），你可以通过调用它来获取你需要的字段。例如，如果你向模板传递一个带有 `Username` 字段的结构体，你可以通过 `{{Username}}` 渲染该字段。

我们可以关于模板说得更多。你可以使用

它们配合逻辑运算符使用；你可以将它们用于循环和其他控制结构。你可以调用内置函数，甚至可以定义并暴露任意的辅助函数，以极大地扩展模板化的能力。太棒了！我们建议你深入研究并探索这些可能性。它们超出了本书的范围，但非常强大。

如果你先放下创建服务器和处理请求的基础知识，转而专注于一些邪恶的事情如何？让我们创建一个凭据收割器吧！

## 凭据收割 (CREDENTIAL HARVESTING)

社交工程学的核心手段之一是凭据收割攻击。这种攻击通过让用户在原始网站的克隆版本中输入凭据，捕捉用户对特定网站的登录信息。这种攻击对于向互联网暴露单因素身份验证界面的组织非常有效。一旦获取了用户的凭据，就可以用它们访问其在实际网站上的账户。这通常会导致组织边界网络的首次攻破。

Go 为这种类型的攻击提供了一个极佳的平台，因为它启动新服务器非常快，而且它易于配置路由和解析用户提供的输入。你可以为凭据收割服务器添加许多自定义内容和功能，但对于这个示例，让我们保持基础。

首先，你需要克隆一个带有登录表单的站点。这里有很多。在实践中，你可能想克隆目标正在使用的站点。但对于这个示例，你将克隆一个 Roundcube 站点。Roundcube 是一个开源 Web 邮件客户端，不像 Microsoft Exchange 等商业软件那样常用，但它同样能让我们说明这些概念。你将使用 Docker 来运行 Roundcube，因为这会让过程变得简单。

你可以执行以下命令启动你自己的 Roundcube 服务器。如果你不想运行 Roundcube 服务器，也没关系；练习源码中包含了该站点的克隆。尽管如此，为了完整性，我们还是包含了：

```
$ docker run --rm -it -p 127.0.0.1:80 robbertkl/roundcube
```

该命令启动了一个 Roundcube Docker 实例。如果你导航到 http://127.0.0.1:80，你会看到一个登录表单。通常你会使用 wget 来克隆站点及其所有必需文件，但 Roundcube 的 JavaScript 特性阻止了这种操作生效。相反，你将使用 Google Chrome 来保存它。在练习文件夹中，你应该看到类似于列表 4-7 的所示目录结构。

```
$ tree
.\ main.go
++ public
  ++ index.html
  ++ index_files
    ++ app.js
    ++ common.js
    ++ jquery-ui-1.10.4.custom.css
    ++ jquery-ui-1.10.4.custom.min.js
    ++ jquery.min.js
    ++ jstz.min.js
    ++ roundcube_logo.png
  ++ styles.css
++ ui.js

index.html
```

列表 4-7: /ch-4/credential_harvester/ 的目录列表

public 目录中的文件代表了未经修改的克隆登录站点。你需要修改原始登录表单以重定向已输入的凭据，将其发送到你自己而不是合法的服务器。首先，打开 public/index.html 并找到用于 POST 登录请求的表单元素。它看起来应该像这样：

```
<form name="form" method="post" action="http://127.0.0.1/?task=login">
```

你需要修改此标签的 action 属性并将其指向你的服务器。将 action 为 /login。不要忘记保存。该行现在应该看起来如下：

```
<form name="form" method="post" action="/login">
```
