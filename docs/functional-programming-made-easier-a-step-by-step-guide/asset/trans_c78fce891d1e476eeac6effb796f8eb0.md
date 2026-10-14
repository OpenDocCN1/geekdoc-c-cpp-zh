
```
handleAction
  :: Action iInput iOutput
  -> H.HalogenM (State iInput) (Action iInput iOutput)
    (Slots iQuery iOutput) (Output iOutput) m Unit
handleAction = case _ of
  Input input -> H.modify_ _ { iInput = input }
  Output innerOutput -> case innerOutput of ①
    PassThrough output -> H.raise $ InnerOutput output ②
    EnableAffirmative -> pure unit ③
    DisableAffirmative -> pure unit
    EnableNegative -> pure unit
    DisableNegative -> pure unit
    CloseAffirmative -> pure unit
    CloseNegative -> pure unit
    AffirmativeClicked -> H.raise Affirmative
    NegativeClicked -> H.raise Negative
```

① 处理 innerOutput 的各种情况。
② 这是我们之前的默认行为。
③ 所有新行为目前都只是空实现。

现在，我们准备好处理各种情况了。让我们从按钮的启用和禁用开始。

我们需要保存按钮的状态，这意味着 `State` 需要改变。

修改 `State`，将 `affirmativeDisabled` 和 `negativeDisabled` 添加到 `State`，然后修改 `initialize` 将它们设置为 `false`。最后，修改 `render` 使其遵循这些值。

准备好继续后，回到这里。

首先，这是对 `State` 的修改：

```
type State iInput =
  { iInput :: iInput
  , affirmativeDisabled :: Boolean ①
  , negativeDisabled :: Boolean ①
  }
```

① 添加了这两行。

接下来，是对 `initialize` 的修改：

```
-- ABOVE CODE REDACTED
component config innerComponent = H.mkComponent
  { initialState: \iInput ->
      { iInput
      , affirmativeDisabled: false
      , negativeDisabled: false
      }
  , render
  , eval: H.mkEval $ H.defaultEval
      { handleAction = handleAction
      , handleQuery = handleQuery
      , receive = Just <<< Input
      }
  }
-- BELOW CODE REDACTED
```

> 将两者都初始化为 `false`。

现在退一步思考，似乎我们的 `Modal.Config` 应该允许我们初始化按钮的状态。我们刚才所做的修改总是将它们设置为不禁用，即 `false`。

等我们完成时，我们会支持这一点。

最后，是对 `render` 的代码修改：

```
import Halogen.HTML.Properties as HP ①

render
  :: State iInput
  -> H.ComponentHTML (Action iInput iOutput) (Slots iQuery iOutput) m
render { iInput, affirmativeDisabled, negativeDisabled } = ②
-- BELOW CODE REDACTED

-- ABOVE CODE REDACTED
      [ if not displayAffirmative then HH.text "" else
          HH.button [
              buttonStyle
            , HP.disabled affirmativeDisabled ③
            , HE.onClick $ const AffirmativeClicked
            ] [ HH.text affirmativeLabel]
        , if not displayNegative then HH.text "" else
          HH.button [
              buttonStyle
            , HP.disabled negativeDisabled ③
            , HE.onClick $ const NegativeClicked
            ] [ HH.text negativeLabel]
        ]
      ]
    ]
  ]
where
-- BELOW CODE REDACTED
```

① 添加了这个导入。
② 解构以获取 `affirmativeDisabled` 和 `negativeDisabled`。
③ 在每个按钮中添加了 `disabled` 属性。

现在，我们应该允许 `Modal.Config` 指定按钮的初始状态。

修改 `Component.Modal` 中的 `Config`，添加 `affirmativeDisabled` 和 `negativeDisabled` 字段。同时，修改 `defaultConfig` 使按钮处于启用状态，即保持当前行为。

准备好后回到这里。

以下是对 `Config` 和 `defaultConfig` 的修改：

```
type Config =
  { affirmativeLabel :: String
  , negativeLabel :: String
  , displayButtons :: ButtonDisplay
  , affirmativeDisabled :: Boolean ①
  , negativeDisabled :: Boolean ①
  }

defaultConfig :: Config
defaultConfig =
  { affirmativeLabel: "OK"
  , negativeLabel: "CANCEL"
  , displayButtons: DisplayBothButtons
  , affirmativeDisabled: false ②
  , negativeDisabled: false ②
  }
```

① 允许配置按钮初始是否禁用。
② 默认为 false。

接下来，在继续阅读之前，修改 `initialState` 以使用这些新的 `Config` 字段。

以下是对 `initialState` 的修改：

```
-- ABOVE CODE REDACTED
component config innerComponent = H.mkComponent
  { initialState: \iInput ->
    { iInput
    , affirmativeDisabled: config.affirmativeDisabled ①
    , negativeDisabled: config.negativeDisabled ①
    }
  , render
  , eval: H.mkEval $ H.defaultEval
    { handleAction = handleAction
    , handleQuery = handleQuery
    , receive = Just <<< Input
    }
  }
-- BELOW CODE REDACTED
```

① 从 false 改为使用 Config 中的值。

现在，我们准备好支持其余 `InnerOutput` 的情况了。这是我们上次在 `handleAction` 中停下的地方：

```
-- ABOVE CODE REDACTED
    Output innerOutput -> case innerOutput of
        PassThrough output -> H.raise $ InnerOutput output
        EnableAffirmative -> pure unit
        DisableAffirmative -> pure unit
        EnableNegative -> pure unit
        DisableNegative -> pure unit
        CloseAffirmative -> pure unit
        CloseNegative -> pure unit
-- BELOW CODE REDACTED
```

只需实现启用和禁用按钮的代码，然后返回这里继续。

以下是这些修改：

```
-- ABOVE CODE REDACTED
    Output innerOutput -> case innerOutput of
        PassThrough output -> H.raise $ InnerOutput output
        EnableAffirmative -> H.modify_ _ { affirmativeDisabled = false } ①
        DisableAffirmative -> H.modify_ _ { affirmativeDisabled = true } ①
        EnableNegative -> H.modify_ _ { negativeDisabled = false } ①
        DisableNegative -> H.modify_ _ { negativeDisabled = true } ①
        CloseAffirmative -> pure unit
        CloseNegative -> pure unit
-- BELOW CODE REDACTED
```

① 相应地修改 State 以覆盖全部 4 种情况。

现在实现使用 Affirmative 和 Negative 关闭的代码。然后返回这里继续。

以下是这些修改：

```
handleAction
  :: Action iInput iOutput
  -> H.HalogenM (State iInput) (Action iInput iOutput)
    (Slots iQuery iOutput) (Output iOutput) m Unit
handleAction = case _ of
  Input input -> H.modify_ _ { iInput = input }
  Output innerOutput -> case innerOutput of
    PassThrough output -> H.raise $ InnerOutput output
    EnableAffirmative -> H.modify_ _ { affirmativeDisabled = false }
    DisableAffirmative -> H.modify_ _ { affirmativeDisabled = true }
    EnableNegative -> H.modify_ _ { negativeDisabled = false }
    DisableNegative -> H.modify_ _ { negativeDisabled = true }
    CloseAffirmative -> handleAction AffirmativeClicked ①
    CloseNegative -> handleAction NegativeClicked ①
    AffirmativeClicked -> H.raise Affirmative
    NegativeClicked -> H.raise Negative
```

① 使用相应的 Action 进行递归。

注意我是如何通过递归而不是重复代码来实现的。这是为了帮助 `handleAction` 适应未来的变化。

想象一下将来在 `AffirmativeClicked` 或 `NegativeClicked` 中要做更多事情的情况。我们肯定不希望在多处重复这些代码。

更糟的是，开发者很可能会只修改其中一个，而忘了另一个。

通过递归，我们自动获得了与用户点击按钮时相同的所有行为。这就是我们在语义上所说的 `CloseAffirmative` 和 `CloseNegative` —— 唯一的区别是程序“点击”了指定的按钮。

一个典型的例子是：内部组件支持用 Enter 和 Esc 来触发 Affirmative 和 Negative。当用户按下 Esc 键时，内部组件中的逻辑会输出 `CloseNegative`。这应该与用户点击 Negative 按钮具有相同的行为。

现在，最后一件事是修改 Message 组件，即 `Component.Modal.Message`，以支持 `InnerOutput`：

```
import Component.Modal (InnerOutput) ①

component
  :: ∀ m
  . MonadAff m
  => H.Component Query Input (InnerOutput Output) m ②
```

① 添加了这个导入。
② 我们将 Message 组件的实际输出类型包裹在 `InnerOutput` 中，以满足 Modal 的期望，Modal 会在将其发送给父组件之前解包它。

`InnerOutput` 是 Modal 与内部组件之间的私有类型。

现在，一切应该都能编译了。用以下命令测试一下：

```
make build
```

希望我们的 Modal 组件足够可配置，能够支持一个表单类型的内部组件，因为那是我们接下来需要处理的部分。

## 30.15. 创建 Users Modal 组件

我们将为 Modal 创建另一个内部组件。这将比我们的 Message 组件复杂得多。

首先，在 `src/Component/Modal` 中创建一个名为 `CreateUser.purs` 的文件，内容如下：

```
module Component.Modal.CreateUser where

import Prelude

import Halogen as H
import Halogen.HTML as HH
import Halogen.HTML.CSS as HC
```

注意，我们的内部组件都放在 `src/Component/Modal` 中。这是因为这些组件不能独立存在，并且需要非常特定的接口要求才能与 Modal 配合使用。因此，将它们分开是一个好习惯。

现在，在我们编写更多代码之前，应该思考一下这个 Modal 的设计：

- 字段
  - 用户名
  - 密码
  - 管理员（复选框）
  - 名
  - 姓
- 按钮
