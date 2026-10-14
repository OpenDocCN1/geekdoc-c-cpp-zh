

我们可以用 `oneOf` 从解码器开始：

```
oneOf [
  decodeJSON request :: LogonRequest
, decodeJSON request :: LogoffRequest
-- etc.
]
```

问题是这无法编译。PureScript 中的数组是同质的。

我们如何绕过这个问题？

一种方法是创建一个 Sum Type 来统一类型：

```
data ApiRequest
  = LogonApiRequest LogonRequest
  | LogoffApiRequest LogoffRequest
```

但这种方法的缺点是我们必须使用一个处理分发的 case 表达式：

```
case request of
  LogonApiRequest (LogonRequest _) -> LogonHandler.handle request
  LogoffApiRequest (LogoffRequest _) -> LogoffHandler.handle request
  -- etc.
```

这只是丑陋的样板代码。

另一种方法是创建一个 Typeclass，例如 ApiRequest 并让 LogonRequest、LogoffRequest 等具有该 Typeclass 的实例：

```
class ApiRequest
```

我称之为 Marker Class，即它只是标记这些类型相关。

但它同样需要 case 表达式。

我喜欢 Typeclasses 来做这件事，但上面的解决方案是从错误的方向入手。我们不应该为 Requests 创建一个 Typeclass，而应该为 Handlers 创建一个 Typeclass：

```
```purescript
class ApiHandler a where -- COMPILER WARNING!!
  handle :: String -> Either MultipleErrors Unit
```
```

第一个参数是 `Request`。

`handle` 方法如果无法解码 Request 则会以 `MultipleErrors` 错误，即解码器的错误类型，否则在成功处理 `Request` 时返回 `Unit`。

由于 `Either` 具有 `Alternative` 实例，会选择遇到的第一个 `Right`，因此我们可以在 `router` 中使用 `oneOf`。

以下编译器警告的原因是我们的 `a` 这里可以是多个类型，即许多 Kinds 或称为 `Polymorphic Kinds` 或简称为 `PolyKinds`：

![](img/8c0e9b687c62642e828ccb5481e11313_1328_0.png)

我们可以通过添加以下类型签名轻松修复它：

```
```purescript
class ApiHandler :: ∀ k. k -> Constraint
class ApiHandler a where
  handle :: String -> Either MultipleErrors Handler
```
```

添加类型签名以指定 `ApiHandler` 接受一个 `Type` 参数并返回一个 `Constraint`，这是 Typeclass 的类型。

我省略了编译器警告中显示的 `k` 的显式类型，因为它在 `∀` 的上下文中是隐含的。

但这个 Typeclass 定义仍然存在问题。你能看出吗？

Typeclass 有一个类型参数，即 `a`，它没有出现在 `handle` 方法的类型签名中：

```
```purescript
class ApiHandler :: ∀ k. k -> Constraint
class ApiHandler a where
  handle :: String -> Either MultipleErrors Unit
```
```

类型参数 `a` 没有出现在 `handle` 的类型签名中。

由于这个原因，编译器无法知道要调用哪个版本的 `handle`。你需要在编码时修复这个缺陷。

在 `Handler` 下创建一个名为 `Class` 的文件夹，然后在 `Handler/Class` 下创建一个名为 `ApiHandler.purs` 的文件并将此 Typeclass 的代码放在那里。

然后修复上述问题并使其编译。

在继续阅读之前先完成此操作。

以下是完整文件：

```
module Handler.Class.ApiHandler where

import Data.Either (Either)
import Data.Unit (Unit)
import Foreign (MultipleErrors)
import Type.Proxy (Proxy)

class ApiHandler :: V k. k -> Constraint
class ApiHandler a where
  handle :: String -> Proxy a -> Either MultipleErrors Unit
```

+   1. 注意模块的名称。看看它如何映射到文件系统中的路径。
+   2. 你也可以导入 `Prelude` 来获取 `Unit`。
+   3. 我们添加了一个 `Proxy` 参数以将类型参数 `a` 放入 `handle` 的类型签名中。

现在，返回到 `Handler.Api.Logon` 并创建一个 `Logon` 类型，然后使其成为 `ApiHandler` 的实例，该实例将 `Request` 解码为 `LogonRequest` 然后处理该 `Request`。在继续之前先完成此操作。

如果你在创建类型时卡住了，这里是它：

```
data Logon = Logon
```

它不需要比这更复杂。它只需要一个数据构造函数。

如果你在这个类型上卡住了，将其添加到你的代码中，然后通过编写 `ApiHandler` 实例来完成。然后继续阅读。

我们将一行一行地编写这个实例，从实例定义开始：

```
```haskell
import Handler.Class.ApiHandler (class ApiHandler)

instance apiHandlerLogon :: ApiHandler Logon where
```
```

导入 `ApiHandler` Typeclass。

现在是实现的左侧：

```
```haskell
instance apiHandlerLogon :: ApiHandler Logon where
  handle request _ = do
    ???
```
```

不要关心 `Proxy` 参数，因为它只存在于告知编译器调用哪个 `handle` 实现。

我们从 `do` 块开始，因为我们将在 `Either` Monad 中编码。我们在 `Either` 中编码，因为 `handle` 和 `decodeJSON` 都返回 `Either`。

接下来，我们将使用 `decodeJSON` 解码 `request`：

```
```haskell
import Prelude

import Control.Monad.Except (runExcept)
import Data.Api.Logon (LogonRequest)
import Foreign.Generic (decodeJSON)

instance apiHandlerLogon :: ApiHandler Logon where
  handle request _ = do
    logonReq <- runExcept (decodeJSON request :: _ LogonRequest)
    ???
```
```

添加这些导入。

不要忘记我们需要 `runExcept` `decodeJSON` 的结果。

最后，我们将调用 Logon 处理程序，我们称之为 `handler`：

```
```haskell
instance apiHandlerLogon :: ApiHandler Logon where
  handle request _ = do
    logonReq <- runExcept (decodeJSON request :: _ LogonRequest)
    pure handler -- COMPILER ERROR!
```
```

我们有一个预期的编译器错误，因为我们还没有编写 `handler`。

将你的代码更新为与此匹配。

接下来，我们将编写一个 stubbed-out 版本的 handler，即什么都不做的版本。记住，handle 在成功时返回 Right unit。这意味着 handler 将返回 Unit。

在继续之前先编写 handler 的类型签名。

这里是类型签名：

```
handler :: LogonRequest -> Unit
```

好吧，我们知道关于 Pure Functions 的一件事是，任何返回 Unit 的 Pure Function 都不能做任何事情。然而，Monadic Function 可以返回 Effect Unit，这意味着它只有副作用。

但是，我认为我们希望 handler 返回一个响应。这意味着我们必须将我们的 handler 改为返回 ResponseM。但如果我们这样做，那么我们的 Typeclass 方法 handle 也需要返回 ResponseM。

这里是它当前的定义：

```
class ApiHandler :: ∀ k. k -> Constraint
class ApiHandler a where
  handle :: String -> Proxy a -> Either MultipleErrors Unit
```

我们如何改变它来实现这一点？在阅读答案之前先看看你是否能回答。

我们希望确保我们仍然在 Either Monad 中工作，这样我们仍然可以在 router 中获得其 Alternative 实例的好处，并在请求无法解码时获得其短路效果。

因此，我们不会改变 Either，而是简单地将 Unit 改为 ResponseM 作为 Either 的第二个类型参数：

```
import HTTPure.Response (ResponseM) ①

class ApiHandler :: ∀ k. k -> Constraint
class ApiHandler a where
  handle :: String -> Proxy a -> Either MultipleErrors ResponseM ②
```

+   ① 导入 ResponseM。

+   ② 将成功类型从 Unit 改为 ResponseM。

同时，移除：

```
import Data.Unit (Unit)
```

现在，重写 handler 的类型签名并在继续之前完成 handler 的 stub 编码。

这里是新的类型签名：

```
import HTTPure.Response (ResponseM) ①
handler :: LogonRequest -> ResponseM
```

① 导入 ResponseM。

现在我们只需用 do 块 stub 它出来，因为我们最终可能在这里有很多行代码：

```
import HTTPure as HTTPure ①
handler :: LogonRequest -> ResponseM
handler _ = do
  HTTPure.notFound ②
```

① 以限定方式导入 HTTPure。

② 目前的 404 错误。

好吧，现在我们在实例中有编译器错误：

```
instance apiHandlerLogon :: ApiHandler Logon where
  handle request _ = do
    -- COMPILER ERROR!!
    logonReq <- runExcept (decodeJSON request :: _ LogonRequest)
    pure handler
```

这里是错误信息：

