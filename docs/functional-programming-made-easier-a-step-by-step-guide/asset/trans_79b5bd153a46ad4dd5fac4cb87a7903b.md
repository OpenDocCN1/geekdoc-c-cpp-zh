
## 第 30 章 使用 Halogen 编写前端

在上一章中，我们探索了使用 Halogen 构建 UI 时的所有主要部分。但是，要构建一个真正的*单页应用程序*（SPA），需要的不仅仅是 UI。

我们需要处理*哈希路由*，即在客户端进行路由，其中 URL 的 Hash 部分（即 `#` 之后的部分）决定要显示哪个页面，以及（可选地）显示什么内容。

顺便说一句，`#` 之后所有内容的技术术语是 *URI 片段*。

我们还需要设计我们的*应用 Monad*，即我们的应用所运行的 Monad 栈。在上一章中，我们总是使用 `runUI` 来运行 Halogen UI，它在 `Aff` 中求值我们的组件。而对于我们的应用，我们将希望使用自己的栈来运行。

在我们深入探讨这两个领域之前，让我们先在我们的 `server` 旁边添加一个同级目录。

如果你的代码保存在名为 `/dev` 的文件夹中，并且你完全按照第 4 章的说明操作，那么你应该运行：

```
cd /dev/purescript
```

如果你没有把项目代码放在这里，请现在切换到相应的目录。

现在创建 client：

```
cd fullstack
mkdir client
cd client
```

在继续之前，*请确保你位于 `client` 目录中*。

要初始化你的项目，以便我们可以在项目内安装 `npm` 包，并使用 `npx` 运行编译器和构建工具，请运行：

```
npm init -y
```

这将创建一个名为 `package.json` 的文件。它会记录我们安装的所有 `npm` 包。

要在本地安装 PureScript 编译器 `purescript` 和构建工具 `spago`，请运行：

```
npm install --save-dev spago@0.20.0 purescript@0.14.1
```

注意 `--save-dev` 选项。这会告诉 npm，这些包仅用于开发。

为了验证我们已在本地安装编译器，我们将使用 npx（注意带 x）：

```
npx purs --version # should print out 0.14.1
```

npx 会在我们本地的 node_modules 目录中查找 purs（PureScript 编译器的名称），然后运行它，并将所有其他命令行参数传递给它。参数 `--version` 会让 purs 打印出它的版本。

为了验证我们已在本地安装构建工具，请运行：

```
npx spago version # should print out 0.20.0
```

现在，使用 git 为项目准备版本控制，请运行：

```
git init # should print `Initialized empty Git repository in <dir>`
```

最后一步是初始化此项目，以便使用 spago 构建 PureScript 程序：

```
npx spago init
```

使用以下命令构建初始应用：

```
npx spago build
```

你会得到一堆类似这样的警告：

```
Warning 1 of 4:

in module Data.Ord.Generic
at .spago/prelude/v5.0.0/src/Data/Ord/Generic.purs:22:3 – 22:41 (line 22,
column 3 – line 22, column 41)

    Name b1 was introduced but not used.

in value declaration genericCompare'

See
https://github.com/purescript/documentation/blob/master/errors/UnusedName.md
for more information,
    or to contribute content related to this warning.
```

这是因为许多库还没有跟上编译器的第 14 版本。PureScript 编译器的第 14 版本现在会对未使用的变量给出警告。这一变更已经做出，但并非所有库都完全跟上了。

此外，还有一些来自第 13 版本的已弃用特性也会产生警告。它们将在第 15 版本中被彻底移除，但现阶段我们只会收到警告。当这些警告来自库时，可以忽略。库的维护者会适时修复它们。

我们只需要担心自己代码中的这些警告。但目前所有警告都来自库，因为我们还没有编写任何代码。

现在，如果你使用的是 VSCode，你应该可以键入以下命令在编辑器中打开此目录：

```
code .
```

如果这不起作用，或者你使用的是其他编辑器，那么只需从编辑器中手动打开此目录。

### 30.1. Halogen CSS 库设置

不幸的是，编译器的第 14 版本是一个过渡版本。并非所有库都已跟上。也许等你读到这段文字时，最后一句话就不再成立了。

但在撰写本文时，你必须使用一个不属于标准 package-set 的 halogen-css 版本。如果你在安装 spago 和 purescript 时显式指定了版本，那么情况将始终如此。

要使用正确版本的 halogen-css，你需要编辑 packages.dhall 文件的最后部分，使其看起来像这样：

```
let upstream =
    https://github.com/purescript/package-sets/releases/download/psc-0.14.1-20210506/packages.dhall

sha256:d199e142515f9cc15838d8e6d724a98cd0ca776ceb426b7b36e841311643e3ef ①

let additions = ②
  { halogen-css =
    { dependencies =
        [ "css"
        , "halogen"
        ]
    , repo =
        "https://github.com/purescript-halogen/purescript-halogen-css"
    , version =
        "v8.0.0"
    }
  }

in  upstream // additions ③
```

① 这一行已经存在。

② 你需要添加这段内容，以使用 halogen-css 库的 v8.0.0 版本。

③ 你需要修改这一行以匹配。

### 30.2. 哈希路由

我们将使用 2 个库来进行路由，分别是 purescript-routing 和 purescript-routing-duplex。

我们将使用 purescript-routing 来处理 URL Hash 的变化，并使用 purescript-routing-duplex 进行路由的解析和打印。

在 src 下创建一个名为 Data 的文件夹，然后在该文件夹下创建一个名为 Route.purs 的文件。我们将把路由编解码器放在这里。

接下来添加以下内容：

```
```haskell
module Data.Route where

import Prelude hiding ((/))
```
```

> 我们正在隐藏除法运算符，因为 `Routing.Duplex.Generic.Syntax` 有一个类似的用于定义 URL 路径的运算符，我们想要使用它。

接下来，前往 `Pursuit` 并查找 `RouteDuplex`，阅读其描述，注意它唯一的 Data Constructor，然后回到这里。

让我们仔细看看 `RouteDuplex` 的定义，尤其是它的 Data Constructor：

```
```haskell
data RouteDuplex i o = RouteDuplex (i -> RoutePrinter) (RouteParser o)
```
```

它的第一个参数是一个函数，接受一个 `i` 并产生一个 `RoutePrinter`，无论它是什么。第二个参数是 `o` 的解析器。

在文档中，它说我们会想要使用 `RouteDuplex'`，因为在这种定义下输入和输出是相同的类型：

```
```haskell
type RouteDuplex' a = RouteDuplex a a
```
```

> 输入和输出是相同的类型。

这个类型名称中的 `Duplex` 部分表示这样一个事实：我们可以将 URL 从 `String` 解析为某个输出类型（第二个 `a`），然后以该输出类型（第一个 `a`）作为输入，创建一个可以产生 `String` 的 `RoutePrinter`。

这个库将使我们能够为路由定义一个类型，并为我们的 `Route` 类型定义一个 Duplex 解析器/打印器。

让我们回到 `RouteDuplex` 的 Data Constructor：

```
```haskell
RouteDuplex (i -> RoutePrinter) (RouteParser o)
```
```

在这一点上，我们对解析器已经相当熟悉了。但确切地说，`RoutePrinter` 是什么。回到 `Pursuit`，点击 `RoutePrinter` 进行调查。然后继续阅读。

当我这样做时，我发现 `RoutePrinter` 包含一个从 `RouteState` 到 `RouteState` 的函数。现在在 `Pursuit` 中点击 `RouteState`，看看你有什么发现。然后继续阅读。

这是我在直接查看源代码时发现的内容：

```
type RouteState =
  { segments :: Array String
  , params :: RouteParams
  , hash :: String
  }
```

RouteState 似乎包含已解析 URL 的各部分。你能弄清楚这些不同部分分别是什么吗？

我无法做到。为了弄清楚这一点，请回到 Pursuit 上的 RoutePrinter，看看能否找到一个能帮助我们更好理解的函数。找一个接受或返回 RouteState 的函数。

一旦你找到你认为可行的方法，你将不得不查看该函数的代码，因为这些函数都没有文档。在继续阅读之前，看看你是否能弄清楚 segments、params 和 hash 分别代表什么。

当我这样做时，我找到了 printPath：

```
printPath :: RouteState -> String
printPath { segments, params, hash: hash' } =
  printSegments segments <> printParams params <> printHash hash'
where
  printSegments = case _ of
    [""] -> "/"
    xs -> joinWith "/" $ map unsafeEncodeURIComponent xs

  printParams [] = ""
  printParams ps = "?" <> joinWith "&" (uncurry printParam <$> ps)

  printParam key "" = unsafeEncodeURIComponent key
  printParam key val = unsafeEncodeURIComponent key <> "="
    <> unsafeEncodeURIComponent val

  printHash "" = ""
  printHash h = "#" <> h
```

① 打印 segments。

② 打印 params。

③ 打印 hash。

由此我们可以看到，segments 之间用 / 分隔打印。这些 segments 必须构成一个 URL 路径，例如 /logon。

接下来，我们可以看到 params 前面带有 ?，并且之间用 & 分隔。我们可以得出结论：
