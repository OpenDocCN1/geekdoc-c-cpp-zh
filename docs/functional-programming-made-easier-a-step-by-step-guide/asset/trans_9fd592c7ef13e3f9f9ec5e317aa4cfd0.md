

```haskell
import Data.Either (Either, note) ❶

userId :: RouteDuplex' String -> RouteDuplex' UserId
userId = as printer parser where ❷
  printer :: UserId -> String
  printer (UserId uuid) = UUID.toString uuid
  parser :: String -> Either String UserId
  parser = UUID.parseUUID
    >>> map UserId
    >>> note "Invalid UserId"
```

❶ 添加了此导入。

这使用了 `parseUUID` 将 `String` 解析为 `UUID`。这可能会失败并返回一个 `Maybe UUID`，这就是为什么我们使用数据构造函数 `UserId` 对 `Maybe UUID` 进行映射的原因。

我们必须对该结果的 `Maybe UserId` 应用 `note`，以将其转换为 `as` 期望其解析器返回的 `Either`。

我们可以删除类型签名（如果你喜欢也可以保留它们）：

```haskell
import Data.Either (note) ❶

userId :: RouteDuplex' String -> RouteDuplex' UserId
userId = as printer parser where
  printer (UserId uuid) = UUID.toString uuid
  parser = UUID.parseUUID
    >>> map UserId
    >>> note "Invalid UserId"
```

❶ 由于我们删除了类型签名，因此不再需要 `Either`，所以从导入列表中移除了它。

接下来，我们将使用 `userId` 来定义 Users 路由：

```haskell
import Routing.Duplex (RouteDuplex', root, path, as, optional, segment) ❶
import Routing.Duplex.Generic.Syntax ((/:)) ❷

routeCodec :: RouteDuplex' Route
routeCodec = root $ sum
  { "Logon": path "logon" noArgs
  , "Logoff": path "logoff" noArgs
  , "Users": users / (optional $ userId segment) ❸ ❹
  }
```

+   ① 将 `optional` 和 `segment` 添加到导入列表中。
+   ② 添加了此导入。
+   ③ 使用 `/` 来分隔路径段。
+   ④ 使用 `optional` 组合子，因为第二个路径段是可选的。

现在，你已经看到了如何为自己的类型编写自定义 Codec，我有一些坏消息。我们没有用户的 `UserId`。我们只有一个唯一的 `userName`。这意味着我们不能使用我们刚刚编写的代码。

如果这是一个真实的应用程序，那么你很可能会这样做。但由于这只是一个学习应用程序，没有唯一的 `UserId` 是可以的。

因此，我们必须对我们的路由类型进行以下更改：

```
data Route
  = Logon
  | Logoff
  | Users (Maybe String) ①
-- | Users (Maybe UserId)
```

① 将 `UserId` 更改为 `String`。

然后按如下方式更改我们的 Codec：

```
routeCodec :: RouteDuplex' Route
routeCodec = root $ sum
  { "Logon": path "logon" noArgs
  , "Logoff": path "logoff" noArgs
  , "Users": "users" / optional segment ①
  -- , "Users": "users" / (optional $ userId segment)
  }
```

① `segment` 解析并打印一个 `String`。

这个路由 Codec 对我们来说已经足够完整，可以继续构建应用程序的其余部分了。

## 30.3. Application Monad

当我们在上一章中编写 Halogen 应用程序时，我们在 `Aff` 中运行它。但通常，我们希望在 Monad 栈中运行组件。

这个应用程序也不例外。我们需要一个应用程序 Monad 来在其中运行组件计算。

如果我们要在自定义应用程序 Monad 中运行，我们称之为 AppM，有几件事我们必须做。

首先，我们需要决定我们的 Monad 栈，如果有的话，会是什么样子。根据经验，我可以肯定地说，我们至少需要一个 ReaderT。原因是我们需要一些全局状态来跟踪已登录的用户。

因此，让我们先通过在 src 下创建一个名为 AppM.purs 的文件并添加以下内容来记录我们的决定：

```
module AppM where

import Control.Monad.Reader.Trans (ReaderT)
import Effect.Aff (Aff)
import Env (Env) -- COMPILER ERROR!!

newtype AppM a = AppM (ReaderT Env Aff a) ①
```

① 我们的应用程序栈是一个 ReaderT，其底部是 Aff，即最终在 Aff 中运行。Env 是我们 reader 的只读类型。

由于我们还没有创建它，所以导入 Env 时会出现编译器错误。我们现在就来做。

创建一个名为 Env.purs 的文件并将其放在 src 下。将以下代码添加到其中：

```
module Env where

import Effect.Ref (Ref)
import Data.LoggedOnUser (LoggedOnUser) -- COMPILER ERROR!!
import Data.Maybe (Maybe)

type Env =
  { userRef :: Ref (Maybe LoggedOnUser) ①
  }
```

① Ref 包含一个 Maybe，因为有时候用户未登录。

由于我们还没有创建它，所以导入 Data.LoggedOnUser 时会出现错误。我们很快就会创建它，但在那之前，让我们看看 Env 的细节。

我们使用了一种之前没见过的东西，Ref，简写为 Reference，它是一个全局可变变量。这与 AVar 有几点不同。

首先，与 AVar 不同，它永远不会为空，因此永远不会阻塞 Fiber。

其次，它运行在 Effect 而不是 Aff 中，这意味着我们必须使用

liftEffect 提升对其 API 的调用，因为我们的 Halogen 组件将在 MonadAff 中运行，即最终在 Aff 中运行的某个 Monad。

第三，它不是线程安全的，或者更准确地说，它不是 fiber 安全的。这意味着 2 个 Fiber 都可以同时修改 Ref。与 AVar 不同，没有 take 和 put。这对我们来说不是什么大问题，因为我们的登录页面会向其中写入一个 Just 值，而我们的注销页面会向其中写入一个 Nothing。

所有其他页面只会读取它。因此，我们不需要 AVar 通常提供的那种保护

现在，我们应该定义 LoggedOnUser。在 src/Data 下创建一个名为 LoggedOnUser.purs 的文件，内容如下：

```
module Data.LoggedOnUser where

import Data.UUID (UUID)

type LoggedOnUser =
  { authToken :: UUID
  }
```

这捕获了已登录用户的 authToken。我们需要它来向服务器发出 API 调用。

现在我们应该能够使用以下命令编译所有文件：

```
npx spago build
```

我们得到：

```
[warn] None of your project files import modules from some projects that are in the direct dependencies of your project.
These dependencies are unused. To fix this warning, remove the following packages from the list of dependencies in your config:
- routing
[error] Some of your project files import modules from packages that are not in the direct dependencies of your project.
To fix this error add the following packages to the list of dependencies in your config:
- aff
- either
- maybe
- refs
- transformers
```

我们现在暂时忽略警告，但我们应该将这些新的直接依赖项添加到 spago.dhall 以解决错误：

```
{-
Welcome to a Spago project!
You can edit this file as you like.
-}
{ name = "my-project"
, dependencies =
  [ "aff" ①
  , "console"
  , "effect"
  , "either" ①
  , "maybe" ①
  , "prelude"
  , "psci-support"
  , "refs" ①
  , "routing-duplex"
  , "routing"
  , "transformers" ①
  , "uuid"
  ]
, packages = ./packages.dhall
, sources = [ "src/**/*.purs", "test/**/*.purs" ]
}
```

① 这些是在这些位置添加的，以保持列表按字母顺序排列。

现在我们可以再次尝试构建：

```
npx spago build
```

现在我们可以用警告构建，我们应该把注意力转回我们的应用程序 Monad。在继续之前，使用 derive newtype 为 AppM 派生 Monad。不要忘记你需要在 Monad 之前派生几个类型类。

然后返回这里。

以下是这些更改：

```
import Prelude ①

newtype AppM a = AppM (ReaderT Env Aff a)
derive newtype instance functorAppM :: Functor AppM
derive newtype instance applyAppM :: Apply AppM
derive newtype instance applicativeAppM :: Applicative AppM
derive newtype instance bindAppM :: Bind AppM
derive newtype instance monadAppM :: Monad AppM
```

① 导入 Prelude 以获取 Functor、Apply 等。

现在使用 derive newtype 获取 MonadEffect 和 MonadAff。这些实例将让我们使用 liftEffect 调用 Effect 中的函数，并使用 liftAff 调用 Aff 中的函数。

在阅读进一步内容之前编写此代码。

以下是这些更改：

```
import Effect.Aff.Class (class MonadAff) ①
import Effect.Class (class MonadEffect)

newtype AppM a = AppM (ReaderT Env Aff a)
derive newtype instance functorAppM :: Functor AppM
derive newtype instance applyAppM :: Apply AppM
derive newtype instance applicativeAppM :: Applicative AppM
derive newtype instance bindAppM :: Bind AppM
derive newtype instance monadAppM :: Monad AppM
derive newtype instance monadEffectAppM :: MonadEffect AppM ②
derive newtype instance monadAffAppM :: MonadAff AppM ②
```

① 添加了这些导入。

② 添加了这些行。

接下来，我们需要一种运行 AppM 栈的方法。因此编写一个名为 runAppM 的函数来运行我们的栈。记住 AppM 只是 ReaderT Monad 栈周围的新类型包装器。完成后返回这里。

首先，我们将从类型签名开始：

```
runAppM :: Env -> AppM ~> Aff ①
```

① 注意自然变换类型运算符 ~> 的使用。这让我们免于指定 a。

接下来，我们将编写实现的左侧：

