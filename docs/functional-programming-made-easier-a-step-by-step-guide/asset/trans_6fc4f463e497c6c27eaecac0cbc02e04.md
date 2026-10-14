

```
handleQuery
  :: ∀ a
  . Query a
  -> H.HalogenM State Action Slots Output m (Maybe a)
```

在某些查询失败的罕见情况下，你可以从 `handleQuery` 返回纯 `Nothing`。

因此，现在我们准备编写 `handleQuery`。首先，我们将从类型签名和实现开始：

```
handleQuery
  :: ∀ a
  . Query a
  -> H.HalogenM State Action Slots Output m (Maybe a)
handleQuery = case _ of ①
  ???
```

① 在此处使用通配符 case 表达式。这是惯用的写法。

接下来，我们将处理 `SetCount`：

```
handleQuery
  :: ∀ a
  . Query a
  -> H.HalogenM State Action Slots Output m (Maybe a)
handleQuery = case _ of
  SetCount c a -> H.modify_ _ { count = c } *> pure (Just a) ① ②
  ???
```

① 注意有些令人困惑的双下划线。第一个是函数名 `modify_` 的一部分，第二个是 `State` 的通配符，我们用整行来更新它。

② 我们将 `State` 中的 `count` 设置为从 `Query` 传入的值，即 `c`，然后返回 `a`，即要评估的下一个内容。

最后，我们将处理 `GetCount`：

```
handleQuery
  :: ∀ a
    . Query a
  -> H.HalogenM State Action Slots Output m (Maybe a)
handleQuery = case _ of
  SetCount c a -> H.modify_ _ { count = c } *> pure (Just a)
  GetCount reply -> H.get >>= \{ count } -> pure $ Just $ reply count ①
```

① 不要忘记 `reply` 函数会将 `a` 返回给你，以便你可以将其作为要评估的下一个内容返回。

将你的代码更新以在 `where` 下添加 `handleQuery`，就像 `handleAction` 一样。

不要忘记在读取后续内容前将 `handleQuery` 也添加到你的 `EvalSpec` 中。

以下是最终的更改：

```
-- ABOVE CODE REDACTED
, eval: H.mkEval H.defaultEval {
    initialize = Just Initialize
  , finalize = Just Finalize
  , handleAction = handleAction
  , handleQuery = handleQuery ①
}
-- BELOW CODE REDACTED
```

① 添加了这一行。

如果我们能测试就好了，但由于我们是顶层组件而不是子组件，并且应用程序不会查询此组件，我们必须创建一个作为子组件的 `Counter` 来测试 `Query`。

## 29.2.5. 作为子组件的 Counter 组件

我们将更改 `Counter` 以允许它拥有也是 `Counter` 组件的子组件。

为了避免无限添加 `Counter` 子组件，我们将传递我们希望 `Counter` 拥有的子组件数量：

```
import Type.Proxy (Proxy(..)) ①

type Slots = ( counter :: H.Slot Query Output Int )

_counter = Proxy :: Proxy "counter" ②
```

① 导入 `Proxy`。

② 通常我们会在单独一行写类型签名，但这是惯用的 Halogen 写法且简洁。

我们将在 `render` 中向虚拟 DOM 添加子组件时使用它。

在开始渲染子组件之前，请确保你的代码已跟上进度。

接下来，我们将在 `render` 中向虚拟 DOM 添加子组件：

```
import CSS.Geometry (width, paddingLeft, paddingTop, paddingBottom) ①
import Data.Array (range) ②

render :: State -> H.ComponentHTML Action Slots m
render { count } = let onClick = HE.onClick <<< const <<< Just in
  HH.div []
  ([ ③
    HH.div [
      HC.style do
        display flex
        flexDirection row
        justifyContent spaceEvenly
        width (rem 6.0)
    ]
    [
      HH.button [ onClick Decrement ] [ HH.text "-" ]
    , HH.text $ show count
    , HH.button [ onClick Increment ] [ HH.text "+" ]
    ]
  ] <> children) ③
where
children = if numChildren == 0 then [] else ④
  [ HH.div [
      HC.style do
        display flex
        paddingLeft (rem 1.0)
        paddingTop (rem 1.0)
        paddingBottom (rem 1.0)
  ] $ range 0 (numChildren - 1) <#\n -> ⑤
  -- COMPILER ERROR!!
  HH.slot _counter n (component 0) (n + 1) FromChild] ⑥
```

① 将 `paddingLeft`、`paddingTop` 和 `paddingBottom` 添加到导入列表。

② 添加此导入。

③ 必须添加括号才能将子组件附加到顶层 `div`。

④ 我们根据 `numChildren` 计算子组件。如果没有子组件，则为空数组。

⑤ 使用 `range` 创建一个要映射的数组。`numChildren` 设为 3 时，`range 0 (numChildren - 1)` 会产生 `[0, 1, 2]`。

⑥ 使用 `HH.slot` 创建一个槽。

在继续之前，请确保你已相应地更新代码。

我们现在先忽略编译器错误，集中讨论 `HH.slot` 调用的细节：

```
HH.slot _counter n (component 0) (n + 1) FromChild
```

第一个参数是引用 `Slots` 类型中标签的 `Proxy`。

第二个参数唯一标识此子组件与其他同类型子组件的区别，即在 `Slots` 类型中具有相同标签的子组件，在我们的例子中是 `_counter`。

第三个参数是组件。我们使用零个子组件创建它。

第四个参数是组件的输入。这将在第一次传递给 `initialState`，随后接收并将计数器设置为比其唯一 id 大一的初始值，即 1、2、3 等。

第五个参数是槽函数，它接收子组件的 `Output` 并将其转换为在 `handleAction` 中处理的 `Action`。

接下来，我们应该将 `FromChild` 添加到 `Action`：

```
data Action
  = Initialize
  | Finalize
  | Increment
  | Decrement
  | FromChild Int ①
```

① 添加了数据构造函数。

这修复了我们之前的编译器错误，并且由于我们尚未完成，所以又出现了另一个错误。

因此，让我们通过在 `handleAction` 中处理这个新的 `Action` 来完成：

```
handleAction
  :: Action
  -> H.HalogenM State Action Slots Output m Unit
handleAction = case _ of
  Initialize -> log "Initialize"
  Finalize -> log "Finalize"
  Increment -> H.modify_ \s -> s { count = s.count + 1 }
  Decrement -> H.modify_ \s -> s { count = s.count - 1 }
  FromChild c -> log $ "Received from Child: " <> show c ①
```

① 添加此 case 仅记录我们从子组件接收到的内容。

确保你的代码完全是最新的，然后重新运行服务器。

你是否收到编译器错误？

那是因为顶层的 `Counter` 尚未获得新的参数。按如下方式更改 `main`：

```
main :: Effect Unit
main = do
  HA.runHalogenAff do
    body <- HA.awaitBody
    runUI (Counter.component 3) 0 body
```

❶ 为 `numChildren` 传递 3。

再试一次。

你是否得到：

```
[warn] None of your project files import modules from some projects that are
in the direct dependencies of your project.
These dependencies are unused. To fix this warning, remove the following
packages from the list of dependencies in your config:
- const ❶
[error] Some of your project files import modules from packages that are not
in the direct dependencies of your project.
To fix this error add the following packages to the list of dependencies in
your config:
- arrays ❷
```

❶ 不再需要。

❷ 我们需要这个。

更新你的 `spago.dhall` 以添加 `arrays` 并移除 `const`。

现在运行服务器并刷新浏览器。你应该得到：

![](img/8c0e9b687c62642e828ccb5481e11313_1608_0.png)

目前，我们没有办法调用 `H.raise` 来向父组件发送 `Output`。因此，让我们在 `Counter` 下添加一个按钮，其 `Action` 将调用 `H.raise`：

```
```haskell
import CSS.Common (center)

render :: State -> H.ComponentHTML Action Slots m
render { count } = let onClick = HE.onClick <<< const <<< Just in
  HH.div []
  ([
      HH.div
        [ HC.style do
            display flex
            flexDirection row
            justifyContent spaceEvenly
            width (rem 6.0)
        ]
        [
            HH.button [ onClick Decrement ] [ HH.text "−" ]
          , HH.text $ show count
          , HH.button [ onClick Increment ] [ HH.text "+" ]
        ]
    , HH.div ①
        [ HC.style do
            display flex
            justifyContent center
            width (rem 6.0)
            paddingTop (rem 0.5)
        ]
        -- COMPILER ERROR!!
        [ HH.button [ onClick RaiseParent ] [ HH.text "Raise" ] ] ②
    ] <> children)
  where
    -- BELOW CODE REDACTED
```
```

① 添加了此 `div`。

② 我们将在点击此按钮时发送 `RaiseParent` 的 `Action`。

在阅读后续内容前，先用此 `div` 更新你的 `render` 函数。

现在，添加处理 `RaiseParent` 的代码以调用 `H.raise` 并传入我们当前的 `count` 值。这应该会消除编译器错误。然后返回此处。

以下是这些更改：

