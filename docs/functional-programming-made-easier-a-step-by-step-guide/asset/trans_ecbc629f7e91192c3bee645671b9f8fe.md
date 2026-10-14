
理解这些生命周期问题，对于创建一个高性能且运行正常的应用来说非常重要。

要修复这个编译错误，Users 组件需要从其父组件 Router 组件接收 Input。请记住，这由 EvalSpec 中的 receive 函数处理。

首先，在 Component.Users 中创建一个名为 SelectedUserName 的 Action，它接收一个 Maybe String，然后在 handleAction 中先为处理它编写桩代码。其次，在 EvalSpec 中实现 receive。然后回到这里继续阅读。

下面是第一部分：

```
type Input = Maybe String ①

data Action
  = Initialize
  | UserSelected User
  | SelectedUserName (Maybe String) ②

-- ABOVE CODE REDACTED
  handleAction :: Action -> H.HalogenM State Action Slots Output m Unit
  handleAction = case _ of
-- CODE REDACTED
  UserSelected (User { userName }) -> navigate $ Route.Users $ Just userName
  SelectedUserName _ -> pure unit ③
```

① 从 Unit 改为 Maybe String。

② 新增 Action 来处理来自父组件的 Input。

③ 为处理我们新 Action 的代码搭了桩（先留空）。

下面是第二部分：

```
component
  :: ∀ m
    . MonadAff m
  => MonadAsk Env m
  => Navigate m Route
  => H.Component Query Input Output m
component = H.mkComponent
  { initialState: \_ -> ①
      { authorized: false
      , selectedUser: Nothing
      , users: []
      }
  , render
  , eval: H.mkEval H.defaultEval
      { handleAction = handleAction
      , receive = Just <<< SelectedUserName ②
      , initialize = Just Initialize
      }
  }
```

① 由于我们还没有用户，目前我们丢弃了最初收到的 Input。我们需要修复这个问题。

② 来自父组件的 Input 会产生 Action `SelectedUserName`。

注意，`initialState` 并没有使用它从父组件（即 Router 组件）获得的 `userName`。

我们在这里无法查找用户，因为目前还没有任何用户——我们还没有调用后端来获取用户。

我们需要将这个值存储到 State 中，这样当我们确实从服务器 API 获取到用户后，就可以选出当前用户（如果有的话）。

在继续阅读之前，请修改代码，简单地把初始用户名存储到我们的新字段 `initUserName` 中。

下面是这个改动：

```
type State =
  { authorized :: Boolean
  , selectedUser :: Maybe User
  , users :: Array User
  , initUserName :: Maybe String ①
  }

-- ABOVE CODE REDACTED
component = H.mkComponent
  { initialState: \initUserName -> ②
    { authorized: false
    , selectedUser: Nothing
    , users: []
    , initUserName ③
    }
  }
-- BELOW CODE REDACTED
```

① 新增了初始用户名字段，该字段可能为 `Nothing`，具体取决于初始 URL 哈希路径。

② 我们不再丢弃 Input 参数。

③ 我们用从 Router 组件（即我们的父组件）获得的 `initUserName` 来初始化新字段。

我们现在需要修改 `handleAction` 中的 `Initialize` 分支，让它在成功地从 `QueryUsersRequest` API 调用取回用户之后，更新 `selectedUser`。

让我们先来写代码：

```
-- ABOVE CODE REDACTED
    Right (QueryUsersResponse
      (QueryUsersResultsSuccess { users })) ->
      H.modify_
        { authorized = true
        , users = users
        , selectedUser = initUserName <#> \userName -> ??? ①
        }
-- BELOW CODE REDACTED
```

① 我们需要找到具有指定 `userName` 的用户。

显然，我把 `users` 设计成 Array 是个错误：

```
type State =
  { authorized :: Boolean
  , selectedUser :: Maybe User
  , users :: Array User
  , initUserName :: Maybe String
  }
```

如果它是一个以 `userName` 为键的 Map，那就好太多了。

把这行未完成的代码注释掉，并修复我的错误：将 State 中的 `users` 改为 Map，然后修复所有因此改动而受影响的地方，用 Map 取代 Array。

然后回到这里继续阅读。

首先，我们要修改 State：

```
import Data.Map (Map) ①

type State =
  { authorized :: Boolean
  , selectedUser :: Maybe User
  , users :: Map String User ②
  , initUserName :: Maybe String
  }
```

① 添加了这个导入。

② 从 Array 改为 Map。

接下来，我们修复 `render`，让它使用 users 这个 Map 的值来工作：

```
import Data.Array (fromFoldable) ①
import Data.Map as Map

    render :: State -> H.ComponentHTML Action Slots m
    render { authorized, users, selectedUser } = ②
    -- CODE REACTED
        (Map.values users # fromFoldable ③
            <# \(user@(User { userName })) ->
                HH.li [
                    HP.class_ $ ClassName "list-group-item"
                , HC.style do
                    backgroundColor paperColor
                    cursor pointer
                , HE.onClick $ const $ UserSelected user
                ]
                [ HH.text userName ])
    -- BELOW CODE REACTED
```

① 添加了这些导入。

② 也解构 `selectedUser`。

③ 只使用 Map 中的值。我们必须用 `fromFoldable` 把从 `Map.values` 得到的 List 转换为 Array。

接下来，我们修复 `initialize`：

```
-- ABOVE CODE REACTED
component = H.mkComponent
    { initialState: \initUserName ->
        { authorized: false
        , selectedUser: Nothing
        , users: Map.empty ①
        , initUserName
        }
    , render
    , eval: H.mkEval H.defaultEval
        { handleAction = handleAction
        , receive = Just <<< SelectedUserName
        , initialize = Just Initialize
        }
    }
```

① 从空 Array 改为空 Map。

最后，我们把从 `QueryUsersRequest` 返回的 users Array 转换为 Map：

```
import Data.Foldable (foldl) ①
import Data.Newtype (unwrap)

-- ABOVE CODE REDACTED
    Right (QueryUsersResponse
        (QueryUsersResultsSuccess { users })) ->
    let mkMap f =
        foldl (\m r -> Map.insert (f r) r m) Map.empty in ②
    H.modify_ _
        { authorized = true
        -- COMPILER ERROR!!
        , users = mkMap (_ .userName <<< unwrap) users ③
        -- , selectedUser = initUserName <#> \userName ->
        }
-- BELOW CODE REDACTED
```

① 添加了这些导入。

② `mkMap` 接收一个 Record 的 Array，并使用 `f` 从每个 Record 生成一个 Key。然后它会将该 Key 和该 Record 作为值添加到 Map 中。

③ 使用 `unwrap` 从 `User` 中取出包含的 Record。

因为在上面的代码中使用了 `unwrap`，我们会得到一个编译错误。这是因为 `User` 没有 `Newtype` 实例。

因此，我们必须去定义 `User` 的服务器代码那里，确保它有一个 `Newtype` 实例：

```
import Prelude ①
import Data.Newtype (class Newtype)

newtype User = User (Record (UserRow ()))
derive instance genericUser :: Generic User _
derive instance newtypeUser :: Newtype User _ ②
```

① 添加了这些导入。

② 派生 `Newtype`。

现在回到客户端代码，运行：

```
make build
```

这将基于我们刚在服务器端改动的代码进行构建。

但这会产生一个错误：

```
[error] Some of your project files import modules from packages that are not in the direct dependencies of your project.
To fix this error add the following packages to the list of dependencies in your config:
- arrays
- foldable-traversable
- newtype
- ordered-collections
```

把这些包添加到 spago 中，然后重新构建：

```
make build
```

然后回到 Component.Users 并保存文件，编译错误应该就会消失。

既然我把 `users` 设计成 Array 的这个糟糕决定已修复，我们可以回到之前注释掉的那行代码：

```
-- ABOVE CODE REDACTED
    Right (QueryUsersResponse
        (QueryUsersResultsSuccess { users })) ->
    let mkMap f = foldl (\m r -> Map.insert (f r) r m) Map.empty in
    H.modify_ _
        { authorized = true
        , users = mkMap (_.userName <<< unwrap) users
        -- , selectedUser = initUserName <#> \userName -> ①
        }
-- BELOW CODE REDACTED
```

① 这一行还没有完成。

取消对该未完成代码行的注释，并完成它的编码，以便在 users 的 Map 中查找 `initUserName`。完成后，回到这里继续。

这个改动如下：

