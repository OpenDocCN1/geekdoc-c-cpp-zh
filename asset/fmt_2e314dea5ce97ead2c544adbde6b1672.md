
很明显这段代码并不好。我们忽略了 `CreateUserResultsSuccess` 和 `CreateUserResultsFailure` 被包装在 `CreateUserResponse` 中这一事实。

请修复我在 `Component.Modal.CreateUser` 中犯的错误，然后继续阅读。

修复如下：

```
import Data.Api.CreateUser (CreateUserRequest(..), CreateUserResults(..)
                             , CreateUserFailureReason(..)
                             , CreateUserResponse(..)) ❶

-- ABOVE CODE REDACTED
        case createResponse of
            Left err -> H.modify_ _ { errorMessage = Just err }
            Right (CreateUserResponse CreateUserResultsSuccess) -> do ❷
                H.raise $ PassThroughOutput
                    $ User
                        { userName
                        , admin
                        , firstName
                        , lastName
                        , temporaryPassword: true
                        }
            Right (CreateUserResponse ❷
                    (CreateUserResultsFailure { reason })) -> case reason of
                NotAuthorized ->
                    errorMsg "You're not authorized to create a new user."
                NotAuthenticated ->
                    H.modify_ $ errorMsg "Your session just timed out."
                        <<< _ { postModalAction = Just RouteToLogon }
                AlreadyExists ->
                    errorMsg "A user with that User Name already exists."
                FileIOError err -> errorMsg
                    $ "A fatal error on the Accounts File occurred:"
                    <> err

-- BELOW CODE REDACTED
```

- ❶ 将 `CreateUserResponse` 添加到导入列表。

- ❷ 在两处都包装在 `CreateUserResponse` 中。

现在重新构建并重新测试：调用用户 `test4`，看看会发生什么。

当我这样做时，现在可以正确解码并将新用户添加到列表中。但是，当然，我们仍然需要通知父组件，因为 Modal 永远不会消失。

我们还必须修复竞态条件。我们需要做的是创建一种方式，让内部组件告知 Modal 何时可以安全地将按钮点击事件通知给父组件。这将给内部组件时间，在 Modal 被销毁之前完成它需要做的任何事情。在我们的场景中，我们希望先创建用户，然后相应地处理响应。

我们已经有了从内部组件到其父组件（即 Modal）的通道。这个机制称为 InnerOutput：

```
data InnerOutput iOutput
  = PassThroughOutput iOutput
  | EnableAffirmative
  | DisableAffirmative
  | EnableNegative
  | DisableNegative
  | CloseAffirmative
  | CloseNegative
```

你可能会认为 CloseAffirmative 或 CloseNegative 可以解决我们的竞态条件，但一旦你看到它们的实现，你就不会这么想了：

```
handleAction
    :: Action iInput iOutput
    -> H.HalogenM (State iInput) (Action iInput iOutput)
                     (Slots iQuery iOutput) (Output iOutput) m Unit
handleAction = case _ of
  Input input -> H.modify_ _ { iInput = input }
  Output innerOutput -> case innerOutput of
    PassThroughOutput output -> H.raise $ InnerOutput output
    EnableAffirmative -> H.modify_ _ { affirmativeDisabled = false }
    DisableAffirmative -> H.modify_ _ { affirmativeDisabled = true }
    EnableNegative -> H.modify_ _ { negativeDisabled = false }
    DisableNegative -> H.modify_ _ { negativeDisabled = true }
    CloseAffirmative -> handleAction AffirmativeClickedInternal ❶
    CloseNegative -> handleAction NegativeClickedInternal ❶
-- BELOW CODE REDACTED
```

> ❶ 它们会递归调用，表现得就像用户点击了按钮一样。

使用这种机制会导致无限循环，因为它们只是调用了同一个按钮点击处理器。这就是整个过程的起因。

我们需要一种不同的消息来通知父组件。对于我们的 `Message` 内部组件，我们会立即输出这个值；但对于 `CreateUser` 内部组件，我们要等到成功创建用户后再输出。

对于来自 `Modal` 的 `NegativeClicked` 查询，我们会立即让 `Modal` 知道，现在可以安全地将按钮点击事件通知给父组件。

这听起来比实际更复杂。我们先在 `Component.Modal` 中添加新的 `InnerOutputs`：

```
data InnerOutput iOutput
  = PassThroughOutput iOutput
  | EnableAffirmative
  | DisableAffirmative
  | EnableNegative
  | DisableNegative
  | CloseAffirmative
  | CloseNegative
  | ParentAffirmative
  | ParentNegative
```

> ① 新的输出。

现在，修改 `handleAction` 来处理这些新的输出。

完成这一步后回到这里。

改动如下：

```
handleAction
  :: Action iInput iOutput
  -> H.HalogenM (State iInput) (Action iInput iOutput)
    (Slots iQuery iOutput) (Output iOutput) m Unit
handleAction = case _ of
  Input input -> H.modify_ _ { iInput = input }
  Output innerOutput -> case innerOutput of
    PassThroughOutput output -> H.raise $ InnerOutput output
    EnableAffirmative -> H.modify_ _ { affirmativeDisabled = false }
    DisableAffirmative -> H.modify_ _ { affirmativeDisabled = true }
    EnableNegative -> H.modify_ _ { negativeDisabled = false }
    DisableNegative -> H.modify_ _ { negativeDisabled = true }
    CloseAffirmative -> handleAction AffirmativeClickedInternal
    CloseNegative -> handleAction NegativeClickedInternal
    ParentAffirmative -> H.raise Affirmative ①
    ParentNegative -> H.raise Negative ①
  AffirmativeClickedInternal -> ②
    void $ H.tell _inner unit AffirmativeClicked ③
  NegativeClickedInternal -> ②
    void $ H.tell _inner unit NegativeClicked ③
```

- ① 只有在内部组件告知我们可以安全操作时，才通知父组件。这些代码是从 AffirmativeClickInternal 和 NegativeClickedInternal 中剪切粘贴过来的。

- ② 删除了多余的 do。

- ③ 删除了通知父组件的代码。在我们之前测试时，其中一处本应被注释掉。

现在，修改 Component.Modal.Message，让 Modal 知道：按钮点击一发生，就可以安全地通知父组件。

完成后或遇到困难时回到这里。

如果遇到困难，可以看看 Component.Modal.CreateUser 是如何得知按钮点击的。你需要在 Component.Modal.Message 中实现类似的机制。

准备好继续后回到这里。

改动如下：

```
import Component.Modal (InnerOutput(..), InnerQuery(..))
import Data.Maybe (Maybe(..))

handleQuery
  :: ∀ a
  . InnerQuery Query a
  -> H.HalogenM State Action Slots (InnerOutput Output) m (Maybe a)
handleQuery = case _ of
  AffirmativeClicked a -> do
    H.raise ParentAffirmative
    pure $ Just a
  NegativeClicked a -> do
    H.raise ParentNegative
    pure $ Just a
  _ -> pure Nothing
```

在两个类型上都添加了 `(..)`，以获得它们的数据构造器。

添加了这个导入。

让 `Modal` 知道，它可以通知父组件按钮点击事件。

记住要返回 `Just a`，这样我们的查询才能被正确响应。

`Negative` 按钮也是同样的逻辑。

对于所有其他查询，我们什么都不做。

我们不能忘记将 `handleQuery` 添加到 `EvalSpec` 中：

```
component
  :: ∀ m
  . MonadAff m
  => H.Component (InnerQuery Query) Input (InnerOutput Output) m
component = H.mkComponent
  { initialState: \message -> { message }
  , render
  , eval: H.mkEval H.defaultEval
      { handleQuery = handleQuery
      }
  }
```

支持 `Queries`。

现在，在 `Component.Modal.CreateUser` 中成功创建用户之后，让 `Modal` 知道：它现在可以安全地让父组件知晓 `Affirmation` 按钮的点击事件了。

- ② 在 `CreateUser` 调用成功后，我们让 `Modal` 知道，它可以告知父组件按钮点击事件。请注意，我们是在将新创建的 `User` 发送给 `Modal` 的父组件之后才这样做的。这样可以确保消息先传递过去，以防万一。我们可不想再出现另一个竞态条件。

- ③ 立即让 `Modal` 知道，它可以告知父组件 `Negative` 按钮的点击事件。

现在，我们的新机制已经完成，可以开始测试了。重新构建应用并重新测试，看看现在会发生什么。将新用户命名为 `test5`。

当我这样做时，成功了！！！注意我们的用户列表是如何更新的。

另外，注意它是如何排序的。我们没有特意让它排序，但不知何故它被排序了。这很可能是原因：

```halogen
[ HH.div [
    HC.style do
      display flex
      flexDirection column
      minWidth (rem 20.0)
      paddingRight (rem 2.0)
  ]
  [ HH.ul [
      HC.style do
        maxHeight (pct 80.0)
        overflowY overflowAuto
    ]
    (Map.values users # fromFoldable ①
      <#> \(user@(User { userName })) ->
  ]
-- BELOW CODE REDACTED
```

- ① 看起来 `Map.values` 会按键顺序获取值。

我在运行以下测试时还发现了另一个问题：

![](img/8c0e9b687c62642e828ccb5481e11313_1901_0.png)

请运行同样的测试。如果您已经有该 userName 的用户，那么就使用 user2。但请确保 first 和 last name 与我在此处输入的完全一致。

创建用户后，进入您的 `server` 项目并重启服务器。会发生什么？

我得到的是：

```
Cannot load accounts: (ParseError "Character 't' did not satisfy predicate"
(Position { line: 3, column: 146 })
```

这是第 3 行的问题，对我来说如下所示：

```
user,3b7b539fcfa135efbc1c71d2a4edc996042424638884d8b6d9053cfa71914a7628d8fe3dd
00e131537c9d82799bd58d5da86aff0ae905a26c3054a3decd70405,true,false,test,test
                                                                                         ^
                                                                                         |
This is column 146 -----------------------------------------------+
```

您认为这是为什么？

如果您记得正确的话，我们的 Parser 不允许 First Name 以小写字母开头。它也不允许除第一个字符外的其他大写字母。

我们在 API 上做了 ZERO 验证。

有很多解决方案：

+   1. 在 UI 中验证。

+   2. 允许小写字符，即更改 parser。

3. 在服务器上对用户进行编码和解码的往返检查，以确保可以读回。事实上，检查我们解码的用户是否与我们开始时相同会更好。

我们真的应该做 #1。

#2 只是放弃。

#3 也应该做，但如果客户端是我们的唯一客户端，做 #1 就能修复这个问题。但这仍然是一个危险的借口。这也真的应该做。

然而，我们不会做这些。我们已经做了很多，我相信如果你能走到这一步，你可以轻松实现 #1 和 #3。

请记住，您可能需要编辑或删除您的 accounts.csv，如果您忘记在 First 和 Last Name 字段中输入大写字符。

既然我们刚刚做了那件事，请编辑 accounts.csv 并删除有问题的行。然后启动您的服务器。

一旦您的服务器再次运行，使用另一种类型的坏名字进行测试，通过创建 last name 为 McCloud 的用户：

![](img/8c0e9b687c62642e828ccb5481e11313_1902_0.png)

创建 mccloud 后，再创建一个用户，并确保该用户足够独特以便您能记住：

![](img/8c0e9b687c62642e828ccb5481e11313_1903_0.png)

现在，重启您的服务器。现在，重新登录到应用程序并导航到 Users 页面。

注意您的唯一用户不见了？

这是因为我们 parser 中的一个问题。为了理解原因，让我们重新审视我们的 parser。
