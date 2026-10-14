

`params` 是 URL 中的查询参数。

最后，`hash` 以前置的 `#` 打印，这让我们知道它是 URI 片段，或通常所称的 Hash。

所以，我怀疑 `RouteParser` 接受一个 `String` 并产生一个 `RouteState`。做一点调查工作，我在 `Routing.Duplex.Parser` 中找到了 `runRouteParser`：

```
runRouteParser :: ∀ a. RouteState → RouteParser a → RouteResult a
```

我们可以看到它返回 `RouteResult`，即：

```
data RouteResult a
  = Fail RouteError
  | Success RouteState a
```

这在成功情况下包含一个 `RouteState`。

所以看起来 `RouteParser` 会解析 URL 路径的段、查询参数和 URI 片段（Hash）。

但是，URI 片段的好处是，它们本身也可以有路径段，因为 `/` 字符在片段中是允许的。它也可以具有等同于查询字符串或查询参数的内容，因为 `=`、`&` 和 `?` 也允许在片段中使用。

所以，如果我们仅将 `Routing.Duplex` 用于解析 URI 片段，那么我们将能够解析 `segments` 和 `params`。我们无法从 URI 片段中解析 `hash`，因为 `#` 不允许在 URI 片段中。

## 30.2.1. 定义路由

在定义我们的路由之前，让我们通过运行以下命令安装 `purescript-routing-duplex` 和 `purescript-routing`：

```
npx spago install routing-duplex routing
npx spago build
```

你会得到以下警告：

```
[warn] None of your project files import modules from some projects that are in the direct dependencies of your project.
These dependencies are unused. To fix this warning, remove the following packages from the list of dependencies in your config:
- routing
- routing-duplex
```

这是因为我们还没有在代码的任何地方使用该库。还没呢。

现在，让我们定义一个与后端服务器 API 对应的路由类型。但让我们先简单地只包含登录和注销：

```
data Route
  = Logon
  | Logoff
```

接下来，我们需要让我们的路由类型具有通用实例，以便 `Routing.Duplex` 可以使用它：

```
import Data.Generic.Rep (class Generic) ①

data Route
  = Logon
  | Logoff
derive instance genericRoute :: Generic Route _ ②
```

- ① 添加此导入。
- ② 派生 Generic。

现在，我们将构建我们的 Codec，即 编码器-解码器。以下是完整内容：

```
import Routing.Duplex (RouteDuplex', root, path) ①
import Routing.Duplex.Generic (sum, noArgs)

routeCodec :: RouteDuplex' Route
routeCodec = root $ sum ② ③
  { "Logon": path "logon" noArgs ④ ⑤ ⑥
  , "Logoff": path "logoff" noArgs
  }
```

- ① 添加这些导入。
- ② root 表示 URL 路径的根，即 /。
- ③ sum 用于表示和类型。我们在这里使用它，因为我们的路由类型是一个和类型。
- ④ 每个字段名字符串必须与数据构造子的名称完全匹配，因此使用双引号来在记录字段名中使用大写字符。
- ⑤ path 定义特定值的路径，例如 logon。
- ⑥ noArgs 是当特定路由没有参数时。

传递给 sum 的记录定义了路由，其字段名必须与 `RouteDuplex' a` 的 `a` 中的数据构造子 EXACTLY 匹配。在我们的例子中，字段名与 Route 的数据构造子匹配。

还有一个 product 函数可用于乘积类型。

到目前为止，我们已定义了以下有效路径段：

```
/logon
/logoff
```

这些是静态段。我们一会儿会看到变量段。

接下来，使用以下命令安装 purescript-uuid 包：

```
npx spago install uuid
npx spago build
```

再次，我们可以忽略以下警告：

```
[warn] None of your project files import modules from some projects that are in the direct dependencies of your project.
These dependencies are unused. To fix this warning, remove the following packages from the list of dependencies in your config:
- routing
- uuid
```

接下来，在 src/Data 下创建一个名为 UserId.purs 的文件。添加以下代码：

```
module Data.UserId where

import Data.UUID (UUID)

newtype UserId = UserId UUID
```

这是一个 UserId，我们将在 URL 中使用它来查看用户信息。

现在，让我们为用户页面添加一个路由。为此，我们首先需要更新我们的路由类型：

```
import Data.Maybe (Maybe) ①
import Data.UserId (UserId(..))

data Route
  = Logon
  | Logoff
  | Users (Maybe UserId) ②
derive instance genericRoute :: Generic Route _
```

- ① 添加这些导入。
- ② 我们将 UserId 添加为 Maybe，以便在它缺失时可以看到所有用户。

注意我们在此更改后 sum 上的编译器错误：

![](img/8c0e9b687c62642e828ccb5481e11313_1660_0.png)

这是因为我们的定义由 `Routing.Duplex` 库对泛型的使用使其类型安全。编译器会在我们缺少字段时捕获。

这里它抱怨包含 Users 的行与仅包含 Logon 和 Logoff 的行不匹配。

编译器 however 不会在我们向传递给 sum 的记录中添加额外字段时抱怨。

我们需要在记录中添加一个路由定义。但在这样做之前，我们应该看看如何使用 segment 定义路径段：

```
-- Allows you to capture a variable segment. For example, the path
-- /user/5 has one static segment and one variable segment. This always
-- reads and writes a string, but when used with other combinators, it
-- can transform that string into a type of your choice. For example:
-- `path "user" (int segment)` parses to `User Int`.
segment :: RouteDuplex' String
```

注意 segment 如何定义变量段。这可以在 /user/5 的文档示例中看到。user 是一个静态路径段，而 5 是一个变量路径段。

我们可以使用以下修饰符来更改 segment 给我们的 String 类型为其他类型：

```
int :: RouteDuplex' String -> RouteDuplex' Int
boolean :: RouteDuplex' String -> RouteDuplex' Boolean
string :: RouteDuplex' String -> RouteDuplex' String ①
```

- ① 只是恒等。

虽然这些组合子转换为标准类型，但我们需要将路径段转换为 UserId。这可以用另一个更强大的组合子完成：

```
as
  :: ∀ s a b
  . (a -> s) ①
  -> (String -> Either String b) ②
  -> RouteDuplex s String
  -> RouteDuplex a b
```

- ① 这是自定义打印机。
- ② 这是自定义解析器。

as 在这里以更通用的形式编写，其中输入和输出类型可能不同。但对我们来说它们不是，所以在这种情况下它看起来像这样：

```
as
  :: ∀ a
  . (a -> String)
  -> (String -> Either String a)
  -> RouteDuplex' String
  -> RouteDuplex' a
```

我们需要编写一个函数将 `RouteDuplex' String` 转换为 `RouteDuplex' UserId`。在继续阅读之前，先写出一个名为 userId 的函数类型签名，它执行此操作。

以下是 userId 的那部分：

```
userId :: RouteDuplex' String -> RouteDuplex' UserId
```

接下来，完成代码，利用 as 提供自定义打印机和解析器。然后返回这里。

我们将用尚未确定的打印机和解析器调用 as：

```
import Routing.Duplex (RouteDuplex', root, path, as) ①

userId :: RouteDuplex' String -> RouteDuplex' UserId
userId = as printer parser where ②
  printer :: UserId -> String ③
  printer = ???
  parser :: String -> Either String UserId ③
  parser = ???
```

- ① 将 as 添加到导入列表。
- ② 以无点形式编写，其中 `RouteDuplex' String` 未命名。
- ③ 这些类型签名在这里帮助我们编写这些函数。我们最后会删除它们。

如果你没有完成，但认为现在可以了，就在这里停止阅读并试试。

下一部分是自定义打印机的代码：

```
import Data.UUID as UUID ①

userId :: RouteDuplex' String -> RouteDuplex' UserId
userId = as printer parser where
  printer :: UserId -> String
  printer (UserId uuid) = UUID.toString uuid ②
  parser :: String -> Either String UserId
  parser = ???
```

- ① 添加此导入。
- ② 解构 UserId 以获取底层 UUID 然后将其转换为字符串。注意，我们这里没有使用 show，因为它包含 UUID 前缀，例如 (UUID dc64cf80-f663-436a-a290-3cac4acf279f)。

最后，我们将编写自定义解析器：

