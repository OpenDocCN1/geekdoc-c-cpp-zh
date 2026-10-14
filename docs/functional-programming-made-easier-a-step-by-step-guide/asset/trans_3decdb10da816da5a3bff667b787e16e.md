

```
json: { contents:
    { teacher:
        { contents:
            { status: { tag: 'NonTenured' },
              personal:
                { contents: { weight: 63.5, height: 162.56, age: 31 },
                  tag: 'Personal' },
              numberOfStudents: 23,
              grades:
                [ { tag: 'Preschool' },
                  { tag: 'Kindergarten' },
                  { contents: 1, tag: 'Grade' } ] },
        tag: 'Teacher' },
    personal:
        { contents: { weight: 17.9, height: 107.9, age: 5 },
          tag: 'Personal' },
    grade: { contents: 1, tag: 'Grade' },
    gpa: 3.2 },
  tag: 'Student' }
```

记住这就是我们要交给 decodeJSON 的。问问自己这看起来像 decodeJSON 想要的样子吗：

```
decodeJSON :: ∀ a. Decode a => String -> F a
```

你现在能看出来了吗？

好吧，如果你意识到这并不是一个 String，那么恭喜你。_reverseKeys 是与 Javascript 对象一起工作的。如果还记得的话，这就是为什么我们要调用 parseJSON，即将 String 转换为 Foreign。

问题是我们告诉编译器 _reverseKeys 会返回一个 String：

```
foreign import _reverseKeys :: Foreign -> String
```

但它并没有。我骗了编译器，现在我要付出代价。

所以，我们需要在从 _reverseKeys 返回它之前将 Javascript 对象字符串化。注意我们不能让 reverseKeys 来做这件事，因为它是递归的。

但我们可以让 _reverseKeys 来做这件事：

```
exports._reverseKeys = o => JSON.stringify(reverseKeys(o));
```

做出这个更改并运行它，同时保留 spy 代码。看看你得到什么。

我得到这个：

```
json:
'{"contents":{"status":{"tag":"NonTenured"},"personal":{"contents":{"weight":63.5,"height":162.56,"age":31},"tag":"Personal"},"numberOfStudents":23,"grades":[{"tag":"Preschool"},{"tag":"Kindergarten"},{"contents":1,"tag":"Grade"}]},"tag":"Teacher"}'
json:
'{"contents":{"teacher":{"contents":{"status":{"tag":"NonTenured"},"personal":{"contents":{"weight":63.5,"height":162.56,"age":31},"tag":"Personal"},"numberOfStudents":23,"grades":[{"tag":"Preschool"},{"tag":"Kindergarten"},{"contents":1,"tag":"Grade"}]},"tag":"Teacher"},"personal":{"contents":{"weight":17.9,"height":107.9,"age":5},"tag":"Personal"},"grade":{"contents":1,"tag":"Grade"},"gpa":3.2},"tag":"Student"}.'
(Right (Teacher { grades: [Preschool,Kindergarten,(Grade 1)],
numberOfStudents: 23, personal: (Personal { age: (Years 31), height:
(Centimeters 162.56), weight: (Kilograms 63.5) }), status: NonTenured }))

(Right (Student { gpa: (GPA 3.2), grade: (Grade 1), personal: (Personal { age:
(Years 5), height: (Centimeters 107.9), weight: (Kilograms 17.9) }), teacher:
(Teacher { grades: [Preschool,Kindergarten,(Grade 1)], numberOfStudents: 23,
personal: (Personal { age: (Years 31), height: (Centimeters 162.56), weight:
(Kilograms 63.5) }), status: NonTenured }) })
```

注意我们的 spy 现在显示的是一个 String 并且我们的代码可以工作了！！

在继续之前删除 Debug 和 `spy` 调用。

现在，只是为了确保我们没有破坏任何东西，再次运行你的程序。

## 第 28 章. 使用 HTTPure 编写后端

我们将创建一个新项目，在其中放置后端服务器的代码，并在后续章节中放置我们的前端程序。

进入包含你一直在工作的项目的父目录。

如果你的代码保存在名为 `/dev` 的文件夹中，并且你在第 4 章中完全按照说明操作，那么你应该运行：

```
```bash
cd /dev/purescript
```
```

如果这不是你放置项目代码的位置，现在更改到适当的目录。

接下来，使用其下的 `server` 目录创建 `fullstack` 项目目录：

```
```bash
mkdir -p fullstack/server # 或你喜欢的其他名称
cd fullstack/server
```
```

> 我们在编写前端时将创建一个名为 `client` 的目录。

在继续之前 **确保你位于 `server` 目录中。**

为了初始化项目以便我们可以安装 `npm` 包并使用 `npx` 在项目内部运行编译器和构建工具，运行：

```
```bash
npm init -y
```
```

这将创建一个名为 `package.json` 的文件。这将跟踪我们安装的任何 `npm` 包。

要本地安装 PureScript 编译器 `purescript` 和构建工具 `spago`，运行：

```
```bash
npm install --save-dev spago@0.20.0 purescript@0.14.1
```
```

注意 `--save-dev` 选项。这将告诉 `npm` 这些包仅用于开发。

为了验证我们是否已本地安装编译器，我们将使用 `npx`（注意 x）：

```
```bash
npx purs --version # 应打印出 0.14.1
```
```

`npx` 在我们的本地 `node_modules` 目录中查找 `purs`，即 PureScript 编译器的名称，然后

运行它并将所有其他命令行参数传递给它。参数 `--version` 告诉 `purs` 打印出其版本。

为了验证我们是否已本地安装构建工具，运行：

```
npx spago version # 应打印出 0.20.0
```

现在，使用 `git` 为项目准备版本控制，运行：

```
git init # 应打印 `Initialized empty Git repository in <dir>`
```

最后一步是使用 `spago` 为此项目初始化构建 PureScript 程序：

```
npx spago init
```

使用以下命令构建入门应用：

```
npx spago build
```

现在，如果你使用 VSCode，你应该能够输入以下命令在编辑器中打开此目录：

```
code .
```

如果这不起作用或你使用不同的编辑器，那么只需从编辑器手动打开此目录。

### 28.1. HTTPure 简要入门

HTTPure 是一个 HTTP 服务器框架，具有以下特性：

- 经过充分测试
- 文档完善
- 构建时充分利用 PureScript 语言特性以实现灵活且可扩展的路由
- 纯粹（没有 `set`、`get`、`use` 等）

### 28.1.1. 创建 HTTP 服务器

使用 HTTPure.serve 可以创建一个不安全的服务器，即 HTTP。使用 `HTTPure.serveSecure` 可以

创建安全服务器，即 HTTPS。

很多时候，服务器放置在代理或负载均衡器后面，例如 `nginx` 或 `haproxy`。使用此配置时，在企业层在此层管理 SSL 证书是有意义的，在这种情况下，就没有必要创建安全服务器。

如果你确实需要在服务器层管理证书，可以向 `HTTPure.serveSecure` 提供证书文件。

我们不会陷入为测试创建自签名证书的麻烦中。相反，我们只创建一个不安全服务器，因为我们只是在这里学习。但在开始新的服务器项目之前，了解这些问题始终很重要。

让我们创建一个非常简单的服务器。首先，我们需要将 `purescript-httpure` 包添加到 `spago.dhall`：

```
```dhall
{-
Welcome to a Spago project!
You can edit this file as you like.
-}
{ name = "my-project"
, dependencies =
  [ "console"
  , "effect"
  , "httpure"
  , "psci-support"
  ]
, packages = ./packages.dhall
, sources = [ "src/**/*.purs", "test/**/*.purs" ]
}
```
```

❶ 我重新格式化了 `dependencies` 以便我可以管理它们。

❷ 添加了 `httpure`。注意我们不使用包名中的前缀 `purescript-`。另外，注意 `httpure` 拼写只有一个 `p`。

然后运行以下命令构建我们的项目：

```
```bash
npx spago build
```
```

我们可以忽略以下警告：

[warn] None of your project files import modules from some projects that are in the direct dependencies of your project.
These dependencies are unused. To fix this warning, remove the following packages from the list of dependencies in your config:
- httpure

现在编辑你的 Main.purs 使其如下所示：

```
module Main where

import Prelude

import Effect.Class.Console (log)
import HTTPure as HTTPure
import HTTPure.Request (Request)
import HTTPure.Response (ResponseM)
import HTTPure.Server (ServerM)

router :: Request -> ResponseM
router _ = HTTPure.ok "This works" ① ②

port :: Int
port = 3000

main :: ServerM
main = HTTPure.serve port router
  $ log $ "Server up running on port: " <> show port ③
```

① 路由器接收任何请求并确定适当的响应。这里我们的简单路由器只是回复一个常量文本消息。

② HTTPure.ok 发送一个 HTTP 状态码为 200 的响应。

③ HTTPure.serve 在指定端口启动一个不安全服务器。一旦服务器启动，它将运行第三个参数，即一个 Effect Unit。这本可以是一个 do 块，但我们只有一行代码。

现在使用以下命令运行此服务器：

```
npx spago run
```

然后打开浏览器并在地址栏中输入 localhost:3000，然后按回车。它应该显示 This works。

现在，如果你仔细查看 main 的类型签名，你可能会想知道我们如何拥有一个

