

```
import Handler.Account as AH ①
import Manager.Account as AM

handler :: CreateUserRequest -> Handler
handler (CreateUserRequest { authToken, user: user' }) = do
    { accountsAVar, sessionsAVar } <- ask
    verifiedSession <- lift $ verifySession sessionsAVar authToken
    response <- case verifiedSession of
        Nothing -> CreateUserResponse
            $ CreateUserResultsFailure { reason: NotAuthenticated }
        Just (Session { userName }) -> do
            admin <- lift $ AM.findAccount accountsAVar userName ②
                <#> maybe false (\(Account a) -> a.admin)
            if not admin then pure CreateUserResponse
                $ CreateUserResultsFailure { reason: NotAuthorized }
            else do
                passwordHash <- lift
                    $ passwordHashHex user'.userName user'.password
                let user = delete (Proxy :: _ "password") user'
                    account = Account $
                        insert (Proxy :: _ "passwordHash") passwordHash user
                result <- lift $ AM.createAccount accountsAVar account ②
                case result of
                    AM.CreateAccountAlreadyExists -> CreateUserResponse ②
                        $ CreateUserResultsFailure { reason: AlreadyExists }
                    AM.CreateAccountSuccess -> do ②
                        result <- lift $ AH.createAccount account ③ ④
                        ???
```

① 由于我们有 2 个 createAccounts，所以必须将这些改为 qualified 导入。

② 将这些代码行改为使用 AM 的 qualified 导入。

③ 使用 AH 的 qualified 导入。

④ 不要忘记 lift。

现在，我们可以处理错误和成功的情况：

```
handler :: CreateUserRequest -> Handler
handler (CreateUserRequest { authToken, user: user' }) = do
  { accountsAVar, sessionsAVar } <- ask
  verifiedSession <- lift $ verifySession sessionsAVar authToken
  response <- case verifiedSession of
    Nothing -> CreateUserResponse
      $ CreateUserResultsFailure { reason: NotAuthenticated }
    Just (Session { userName }) -> do
      admin <- lift $ AM.findAccount accountsAVar userName
        <#> maybe false (\(Account a) -> a.admin)
      if not admin then pure CreateUserResponse
        $ CreateUserResultsFailure { reason: NotAuthorized }
      else do
        passwordHash <- lift
          $ passwordHashHex user'.userName user'.password
        let user = delete (Proxy :: _ "password") user'
            account = Account $
              insert (Proxy :: _ "passwordHash") passwordHash user
        result <- lift $ AM.createAccount accountsAVar account
        case result of
          AM.CreateAccountAlreadyExists -> CreateUserResponse
            $ CreateUserResultsFailure { reason: AlreadyExists }
          AM.CreateAccountSuccess -> do
            result <- lift $ AH.createAccount account
            pure $ case result of ①
              AH.CreateAccountFileError err -> CreateUserResponse
                $ CreateUserResultsFailure { reason: FileIOError err }
              AH.CreateAccountSuccess -> CreateUserResultsSuccess
    ???
```

① 处理成功情况和错误情况。

最后，我们可以... 等等。等等。等等。

在继续之前，先看看我们到目前为止写的内容。你对这段代码有什么感觉？

我的想法是它太复杂了。坦白说，这是一团糟。

错误检查太多了。书中前面那些很棒的 Monadic Happy Path 编程去哪了？我想要它回来！！

我希望整个 case 表达式都在 ExceptT 中运行，这样我就不用检查错误了。

我们的自然倾向可能是继续硬着头皮往前写，告诉自己以后会修复，但我们不会。

```
```haskell
handler :: CreateUserRequest -> Handler
handler (CreateUserRequest { authToken, user: user' }) = do
  { accountsAVar, sessionsAVar } <- ask
  verifiedSession <- lift $ verifySession sessionsAVar authToken
  response <- case verifiedSession of
    Nothing -> CreateUserResponse
      $ CreateUserResultsFailure { reason: NotAuthenticated }
    Just (Session { userName }) -> do
      admin <- lift $ AM.findAccount accountsAVar userName
        <#> maybe false (\(Account a) -> a.admin)
      if not admin then pure CreateUserResponse
        $ CreateUserResultsFailure { reason: NotAuthorized }
      else do
        passwordHash <- lift
          $ passwordHashHex user'.userName user'.password
        let user = delete (Proxy :: _ "password") user'
            account = Account $
              insert (Proxy :: _ "passwordHash") passwordHash user
        result <- lift $ AM.createAccount accountsAVar account
        case result of
          AM.CreateAccountAlreadyExists -> CreateUserResponse
            $ CreateUserResultsFailure { reason: AlreadyExists }
          AM.CreateAccountSuccess -> do
            result <- lift $ AH.createAccount account
            pure $ case result of
              AH.CreateAccountFileError err -> CreateUserResponse
                $ CreateUserResultsFailure { reason: FileIOError err }
              AH.CreateAccountSuccess -> CreateUserResultsSuccess
  ???
```
```

唯一的区别是 `CreateUserFailureReason`，例如 `NotAuthenticated`、`NotAuthorized`、`AlreadyExists` 和 `FileIOError`。

所有错误条件都只是设置不同的 `CreateUserFailureReason`。这意味着我们的 `do` 块类型签名可以是 `ExceptT CreateUserFailureReason Aff Unit`。

`a` 是 `Unit`，因为我们只想要这些函数的副作用，最后我们只需查看 `result` 的 `Either` 并决定是构建错误响应还是成功响应。

这是我们到目前为止的重写：

```
handler :: CreateUserRequest -> Handler
handler (CreateUserRequest { authToken, user: user' }) = do
  { accountsAVar, sessionsAVar } <- ask
  result <- lift $ runExceptT do
    ???
```

我们在旧代码中做的第一件事是调用 verifySession。让我们从函数调用开始孵化这行代码，并修改它直到它具有我们 do 块的正确类型，即 ExceptT CreateUserFailureReason Aff Session。

这是它的类型签名：

```
verifySession :: AVar Sessions -> UUID -> Aff (Maybe Session)
```

我们知道可以使用 note 将 verifySession 返回的 Maybe 转换为 Either。我们必须使用 map，因为 Maybe 在 Aff 上下文中：

```
verifySession sessionsAVar authToken <#> note NotAuthenticated
  :: Aff (Either CreateUserFailureReason Session)
```

现在，我们只需要一种方法将 Aff (Either CreateUserFailureReason Session) 转换为 ExceptT CreateUserFailureReason Aff Session，以便在我们的 do 块中使用它。

首先要注意的是，我们有一个 Either，而我们应该能够将其转换为 ExceptT，因为 ExceptT 包含一个 Either：

```
newtype ExceptT e m a = ExceptT (m (Either e a))
```

而且事实证明有一个函数可以做到这一点，但它在 Haskell 中，而出于某种原因它不在 PureScript 中。但我们将在这里一起编写它。我们可以从 Haskell 复制代码，但那样我们就学不到那么多。

让我们称它为 Haskell 中的名字，liftEither：

```
import Data.Either (Either) ①

liftEither :: ∀ e m a. Either e a -> ExceptT e m a
```

① 添加此导入。

这将接受一个 Either 并返回一个 ExceptT。

接下来，我们将编写 Left 情况：

```
import Data.Either (Either(..)) ①

liftEither :: ∀ e m a. Either e a -> ExceptT e m a
liftEither (Left err) = ???
```

① 包含 Either 的数据构造子。

我们需要一种方法将 e 转换为 ExceptT e m a。如果你直接在 Pursuit 中搜索 e -> ExceptT e m a，你会得到大量函数，其中没有一个看起来正确。

但如果你意识到 ExceptT 是 MonadError 的特例，这可能会有所帮助。

MonadError 有 2 个类型参数，e 然后是 m。所以在 Pursuit 中搜索 e -> m a，看看是否能找到可用的东西。然后返回这里。

你找到 throwError 了吗？这是它的定义：

```
throwError :: ∀ a m e. MonadThrow e m => e -> m a ①
```

① 在我们的例子中，throwError 中的 m 是 ExceptT e m。

我们可以使用它：

```
import Control.Monad.Error.Class (throwError) ①

liftEither :: ∀ e m a. Either e a -> ExceptT e m a
liftEither (Left err) = throwError err
???
```

① 添加此导入。

但是，现在我想像 throwError 一样泛化我们的类型签名：

```
import Control.Monad.Error.Class (class MonadError, throwError) ①

liftEither :: ∀ e m a. MonadError e m => Either e a -> m a ②
liftEither (Left err) = throwError err
???
```

① 将类型类 MonadError 添加到导入列表。

② 将 ExceptT e m 替换为 m。

