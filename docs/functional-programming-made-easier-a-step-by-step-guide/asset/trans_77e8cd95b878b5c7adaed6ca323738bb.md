

```
```haskell
instance apiHandlerLogon :: ApiHandler Logon where
  handle request _ = do
    logonReq <- runExcept (decodeJSON request :: _ LogonRequest)
    pure $ handler logonReq
```
```

> ① 在 handleApi 中，我们要让这个类型声明变成多态的。

希望你还记得我们过去是怎么做的。在继续阅读之前，先看看你能做到哪一步。

那么，我们先从类型签名开始：

```
```haskell
import Data.Either (Either)
import Foreign (MultipleErrors)
import Type.Proxy (Proxy)

handleApi
  :: ∀ a
  .  Proxy a
  -> String
  -> Either MultipleErrors Handler
```
```

接下来，我们编写左侧部分：

```
```haskell
handleApi
  :: ∀ a
  .  Proxy a
  -> String
  -> Either MultipleErrors Handler
handleApi _ request = ???
```
```

如果你在类型签名上卡住了，而这一步帮你解了围，那就先停下来，看看自己能否继续编码。

等你准备好继续时，再回到这里。

现在，我们可以从 Logon 的 handle 实现中复制粘贴代码，只需稍作修改：

```
handleApi
  :: ∀ a
    . Proxy a
  -> String
  -> Either MultipleErrors Handler
handleApi _ request = do
  req <- runExcept (decodeJSON request :: _ a) ① ②
  pure $ handler req -- COMPILER ERROR!! ②
```

① 我们使用 `a`，因为它是要解码的请求类型。
② 将 `logonReq` 重命名为更通用的 `req`。

现在，编译器报错：

![](img/8c0e9b687c62642e828ccb5481e11313_1449_0.png)

问题在于，我们把这个函数和某个 handler 函数放在了同一个文件中。因此编译器会检查 `req` 的类型（即 `a`），并将其与 handler 第一个参数的类型（即 `LogonRequest`）进行对比。

这会带来麻烦。我们把代码移动到一个名为 `Common.purs` 的文件中，位于 `src/Handler/Api` 目录下。

接下来，我们将复制目前已经写好的代码，再加上一些额外内容：

```
module Handler.Api.Common where

import Prelude

import Control.Monad.Except (runExcept)
import Data.Either (Either)
import Foreign (MultipleErrors)
import Foreign.Generic (decodeJSON)
import Handler.Class.ApiHandler (Handler)

handleApi
  :: ∀ a
  . Proxy a
  -> String
  -> Either MultipleErrors Handler
handleApi _ request = do
  req <- runExcept (decodeJSON request :: _ a)
  pure $ handler req -- COMPILER ERROR!!
```

暂停阅读，确保你的代码已经跟到这里，然后再回来继续读。

我们仍然有一个编译器错误，但在这个文件里错误不同：

![](img/8c0e9b687c62642e828ccb5481e11313_1450_0.png)

这告诉我们 `handler` 未定义。这个 `handler` 函数需要被传入。停在这里，修改类型签名以包含 `handler`，然后再继续读。

修改如下：

```
handleApi
  :: ∀ a
  . Proxy a
  -> (a -> Handler) ①
  -> String
  -> Either MultipleErrors Handler
handleApi _ handler request = do ①
  req <- runExcept (decodeJSON request :: _ a) -- COMPILER ERROR!!
  pure $ handler req
```

① 添加 `handler` 作为第二个参数。

要注意，`handler` 的类型签名是 `a -> Handler`。它接受请求的类型（例如 `LogonRequest`），也就是我们从 `Proxy` 参数得到的同一个 `a`。可以看到，我们正是用同一个 `a` 来帮助编译器选择合适的 `decodeJSON` 实现。

如果这样还不明白，看看 `Handler.Api.Logon` 中 `handler` 的类型签名：

```
handler :: LogonRequest -> Handler ①
```

① 在这种情况下，`a` 就是 `LogonRequest`。

现在类型签名中已经有了 `a`，我们不再需要 `Proxy` 了。在继续阅读之前，把它从类型签名中移除。

修改如下：

```
handleApi
  :: ∀ a
    . (a -> Handler) ①
  -> String
  -> Either MultipleErrors Handler
handleApi handler request = do ①
  req <- runExcept (decodeJSON request :: _ a) -- COMPILER ERROR!!
  pure $ handler req
```

① 移除了 `Proxy` 参数。

现在，我们把注意力转向这个编译器错误：

![](img/8c0e9b687c62642e828ccb5481e11313_1451_0.png)

这告诉我们，需要对 `a` 加以约束，使其可以被解码：

```
import Foreign.Generic.Class (class Decode) ①

handleApi
  :: ∀ a
    . Decode a ②
  => (a -> Handler)
  -> String
  -> Either MultipleErrors Handler
handleApi handler request = do
  req <- runExcept (decodeJSON request :: _ a)
  pure $ handler req
```

① 导入 `Decode` 类型类。
② 添加约束。

现在它就能编译通过了。

现在，我们可以将 `handleApi` 导入 `Handler.Api.Logon`：

```
import Handler.Api.Common (handleApi)
```

把这行加进你的代码，确保放在正确的模块中。

接下来，使用这个函数重新实现 `ApiHandler` 实例，然后再回到这里。

重写如下：

```
import Foreign.Generic (encodeJSON) ①

instance apiHandlerLogon :: ApiHandler Logon where
  handle request _ = handleApi handler request ②
```

① 从导入列表中移除了 `decodeJSON`。
② `handler` 的类型签名决定了 `handleApi` 将使用哪种类型来解码 JSON。

另外，你可以删除：

```
import Control.Monad.Except (runExcept)
```

遗憾的是，我们无法将其写成 Point-free 风格。我们可以用 `flip`，但那会很难看。不过，因为这只是一个小改动，我们可以调整类型类方法参数的顺序。

但如果我们那样做，会影响 `router`。所以，先做出这些修改，然后把 `handle` 重写为 Point-free 风格。然后继续阅读。

这是对 `Handler.Class.ApiHandler` 的修改：

```
class ApiHandler :: ∀ k. k -> Constraint
class ApiHandler a where
  handle :: Proxy a -> String -> Either MultipleErrors Handler
```

① 把参数顺序与原来相比调换了。

这是 `Main` 中 `router` 的修改：

```
router :: HandlerEnv -> Request -> ResponseM
router env { body, method }
  | method == HTTPure.Post =
    case hush <=<
      (head $ oneOf $ (handle (Proxy :: _ Logon) body) :| []) of
      Nothing -> HTTPure.badRequest body
      Just reader -> runReaderT reader env
  | otherwise = HTTPure.methodNotAllowed
```

① 调换了 `handle` 调用中的参数顺序。

最后，这是对 `Handler.Api.Logon` 的修改：

```
instance apiHandlerLogon :: ApiHandler Logon where
  handle _ = handleApi handler
```

① 现在这是 Point-free 风格，`request` 成了未命名的参数。

现在，让我们看看可以从 Logon 借鉴什么来编写 Logoff：

```
data Logon = Logon

instance apiHandlerLogon :: ApiHandler Logon where
  handle _ = handleApi handler
```

这段代码非常少，可以直接复制粘贴到我们新的 Logoff 模块中。

在 `src/Handler/Api` 下创建 `Logoff.purs`，然后把上面 `Handler.Api.Logon` 的代码复制到我们的新文件中，新文件的模块名为 `Handler.Api.Logoff`。粘贴后，别忘了把所有出现的 `Logon` 重命名为 `Logoff`。

```
```haskell
import Manager.Session (createSession)
```
```

接下来，我们需要查看 `createSession` 的类型签名，看看它需要什么：

```
```haskell
createSession :: AVar Sessions -> String -> Aff UUID
```
```

很明显，我们需要像 `Accounts` 那样为 `Sessions` 准备一个 `AVar`，我们可以从 `handler` 的这行代码看到这一点：

```
```haskell
{ accountsAVar } <- ask
```
```

如果我没记错的话，`ask` 会获取一个 `HandlerEnv`。在 VSCode 中对项目中的所有文件进行全局搜索，在 Windows 上使用 `Cmd-Shift-F` 或 `Ctrl-Shift-F`，然后输入 `HandlerEnv` 来查找它的定义位置，然后再回到这里。

这是我在 `Handler.Class.ApiHandler` 中找到的：

```
```haskell
type HandlerEnv =
  { accountsAVar :: AVar Accounts
  }
```
```

看起来我们从未添加过 `sessionsAVar`。现在就把它加上，然后继续读。

修改如下：

```
```haskell
import Manager.Session (Sessions)

type HandlerEnv =
  { accountsAVar :: AVar Accounts
  , sessionsAVar :: AVar Sessions
  }
```
```

+   1. 导入 `Sessions`。
+   2. 添加 `sessionsAVar`。

现在，我们必须像创建 `accountsAVar` 那样创建这个 `AVar`。再次在项目中搜索 `accountsAVar`，看看我们是在哪里创建的，然后继续阅读。

我在 `Main` 中找到了它：

