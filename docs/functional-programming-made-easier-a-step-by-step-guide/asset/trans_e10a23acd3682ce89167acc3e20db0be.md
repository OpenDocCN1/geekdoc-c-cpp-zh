

最后，这个函数返回该结果在 Aff 中。

接下来，我们将对等号的左侧进行编码：

```
withAVar :: ∀ a b. AVar a -> (a -> Aff (Tuple a b)) -> Aff b
withAVar aVar f = ??? ①
```

① 我们有 aVar 和函数 f。

接下来，我们将获取 AVar 值：

```
withAVar :: ∀ a b. AVar a -> (a -> Aff (Tuple a b)) -> Aff b
withAVar aVar f = do ①
  value <- AVar.take aVar
  ???
```

① 我们从一个 do 块开始。

现在，我们将调用我们的回调函数：

```
withAVar :: ∀ a b. AVar a -> (a -> Aff (Tuple a b)) -> Aff b
withAVar aVar f = do
  value <- AVar.take aVar
  Tuple newValue result <- f value ① ②
  ???
```

① 我们解构 Tuple 以获取 AVar 的 newValue 和计算的结果。

② 由于 f 在 Aff 中运行，我们使用 <- 语法通过 bind。 如果它没有在 Aff 中运行，我们就必须使用 let。

现在，我们将 newValue 放回 AVar 中：

```
withAVar :: ∀ a b. AVar a -> (a -> Aff (Tuple a b)) -> Aff b
withAVar aVar f = do
  value <- AVar.take aVar
  Tuple newValue result <- f value
  AVar.put newValue aVar ①
  ???
```

① 我们总是调用它。 这就是我们能够保证永远不会让 AVar 为空的方式。

最后，我们将返回计算的结果：

```
withAVar :: ∀ a b. AVar a -> (a -> Aff (Tuple a b)) -> Aff b
withAVar aVar f = do
  value <- AVar.take aVar
  Tuple newValue result <- f value
  AVar.put newValue aVar
  pure result
```

> 返回回调的计算结果。

查看这个函数，你能看出我们如何将其泛化吗？花一分钟时间看看是否能在继续之前想出一种方法。

`Aff` 可以泛化为任何具有 `MonadAff` 实例的 Monad `m`。 但是，我们必须使用 `liftAff` 将所有 `Aff` 函数提升到 `m` 中：

```
import Effect.Aff.Class (class MonadAff, liftAff)

withAVar :: ∀ a b m. MonadAff m => AVar a -> (a -> m (Tuple a b)) -> m b
withAVar aVar f = do
  value <- liftAff $ AVar.take aVar
  Tuple newValue result <- f value
  liftAff $ AVar.put newValue aVar
  pure result
```

> 添加了此导入。

> 将 `Aff` 改为 `m` 并在 `m` 上添加了 `MonadAff` 约束。

> 使用 `liftAff` 将所有 `Aff` 计算提升到 `m` 中。

现在，这个函数可以在 `Aff` 或任何其他可以在 `Aff` 中运行的 Monad 中使用，例如我们的 `Handler`，它是一个 `ReaderT` Monad 栈，底部是 `Aff`。 `ReaderT` 将 `Aff` 调用委托给其底层 Monad，这只有在栈中存在 `Aff` 时才有效。

将此添加到你的代码中，然后更改 `createAccount` 以使用它。 完成后，继续阅读。

以下是该更改：

```
createAccount :: AVar Accounts -> Account -> Aff CreateAccountResult
createAccount accountsAVar account@(Account { userName }) = do
  withAVar accountsAVar ①
    \accounts -> pure $ ②
      if Map.member userName accounts then ③
        Tuple accounts CreateAccountAlreadyExists
      else
        Tuple (Map.insert userName account accounts) CreateAccountSuccess
```

① 我们调用 withAVar 并传入 accountsAVar。

② 原始逻辑是纯计算，因此我们使用 pure 将其包装在 Aff 中。

③ 我们的 if 逻辑没有改变。

在该模块中孵化 withAVar 很不错，但它真的不属于这里。 此外，使用它在 verifySession 中会很好。

因此，我们将把它移动到名为 Utils.purs 的文件中。 在 src 文件夹下创建该文件并移动 withAVar 和适当的导入。

然后从 Manager.Account 中删除以下导入：

```
import Effect.Aff.Class (class MonadAff, liftAff)
```

并添加：

```
import Utils (withAVar)
```

完成这些任务后返回此处。

以下是 Utils.purs：

```haskell
module Utils where

import Prelude

import Data.Tuple (Tuple(..))
import Effect.Aff.AVar (AVar)
import Effect.Aff.AVar as AVar
import Effect.Aff.Class (class MonadAff, liftAff)

withAVar :: ∀ a b m. MonadAff m => AVar a -> (a -> m (Tuple a b)) -> m b
withAVar aVar f = do
  value <- liftAff $ AVar.take aVar
  Tuple newValue result <- f value
  liftAff $ AVar.put newValue aVar
  pure result
```

现在更改 `verifySession` 以使用 `withAVar` 然后返回此处。

以下是该更改：

```haskell
import Utils (withAVar) ❶

verifySession :: AVar Sessions -> UUID -> Aff (Maybe Session)
verifySession sessionsAVar authToken = do
  expireSessions sessionsAVar
  withAVar sessionsAVar ❶
    \sessions -> do ❷
      now <- getTime <$> liftEffect now
      pure $ case Map.lookup authToken sessions of ❸
        Nothing -> Tuple sessions Nothing
        Just (Session session) ->
          let newSession = Session $ session { lastTime = now }
              newSessions = Map.insert authToken newSession sessions in
          Tuple newSessions (Just newSession)
```

- ❶ 我们现在使用 `withAVar` 和 `sessionsAVar`。 它将在调用我们的回调函数之前和之后执行 `AVar.take` 和 `AVar.put`。

- ❷ 这是我们的回调。 它在 `Aff` 中运行，因此有 `do` 块。

- ❸ 我们的 `case` 表达式是纯计算，因此我们使用 `pure` 将其包装在 `Aff` 中。

现在通过使用 `withAVar`，我们的代码更安全，我们不必记住在逻辑的每条可能路径上调用 `AVar.put`。

接下来，我们需要在磁盘上创建一个 `Account`。 但是，我们已经在 `Handler.Account` 中有 `createAccount`：

```
createAccount :: Account -> Aff (Either String Unit)
createAccount account = lmap show
  <$> (try $ appendTextFile ASCII accountsFile $ accountToCSV account)
```

查看这个函数，看看它是否适用于 `CreateUserRequest` 的要求。 然后继续阅读。

看起来是可行的，但我看到一个问题，我们在 `Manager.Account` 中的 `createAccount` 中已经修复了。 比较两者，看看你是否能看出这个有什么问题。 然后继续阅读。

我可以看到我们在 Account Manager 中避免的同样的布尔盲视，其返回类型为 `Either String Unit`。 从技术上讲，这不是布尔盲视，但 `Either String Unit` 中的 `String` 是一个隐含的文件 I/O 错误。

这是一种隐式优于显式的情况，而显式不仅是可能的，而且实现起来很容易，效果也好得多。

为了消除返回类型的隐式特性，我们将为 `Handler.Account` 创建一个类似于 `Manager.Account` 中的 `CreateAccountResult` 的类型，并修改 `createAccount` 以使用它。 为数据构造函数使用名称 `CreateAccountSuccess` 和 `CreateAccountFileError`。

完成后，修改 `Handler.Account` 中的 `createAccount` 以使用我们新的类型。

完成后返回此处。

以下是该更改：

```
data CreateAccountResult
  = CreateAccountSuccess
  | CreateAccountFileError String

createAccount :: Account -> Aff CreateAccountResult
createAccount account = lmap show
  <$> (try $ appendTextFile ASCII accountsFile $ accountToCSV account)
  <#> case _ of
    Left err -> CreateAccountFileError err
    Right _ -> CreateAccountSuccess
```

- 1. 为调用 `createAccount` 的结果创建了一个类型，比 `Either String Unit` 更具信息性。
- 2. 将 `Either String Unit` 更改为 `CreateAccountResult`。 这可能破坏了调用此函数的任何人。
- 3. 使用翻转的 `map` 通过 `<#>`。

使用 **case** 和通配符处理来自 `try` 的 `Either`。

这是一个小的改进，但仍然值得。 也许不是今天，但一个月后，我们会感激这一点。

现在，追踪 `createAccount` 被调用的位置并使其检查新的返回类型。 修复后返回此处并继续阅读。

结果是还没有人调用它。 这很好，因为我们的更改会破坏我们的调用代码。

我们现在准备开始处理 `Handler.Api.CreateUser`。

在 `src/Handler/Api` 下创建一个名为 `CreateUser.purs` 的文件，并确保将模块命名为 `Handler.Api.CreateUser`。

接下来，查看我们对 `Handler.Api.Logoff` 所做的事情，看看我们可以借鉴什么。 然后返回此处。

我首先注意到我们需要的数据类型：

```
data Logoff = Logoff
```

记住它用于帮助 `router` 区分调用哪个处理程序。 因此，为 `CreateUser` 添加这个，然后继续阅读。

以下是该类型：

```
module Handler.Api.CreateUser where

data CreateUser = CreateUser
```

我们可以从 `Logoff` 复制的下一件事是 `ApiHandler` 实例代码。 因此继续编写它。 然后返回此处继续。

这是样板代码，但我们将其减少到只有 1 行代码：

```
instance apiHandlerCreateUser :: ApiHandler CreateUser where
  handle _ = handleApi handler
```

现在编译器不满意，因为我们还没有导入任何东西。 从 `Logoff` 偷取导入以使错误消失。 在出现关于 `handler` 的错误时停止，因为我们还没有编写它。 在继续前进之前执行此操作。

以下是我的导入：

