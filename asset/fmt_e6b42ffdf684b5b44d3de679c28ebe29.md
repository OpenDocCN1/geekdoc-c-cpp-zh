
但这会在遇到错误的 `String` 时抛出异常。我们不想让漂亮的 PureScript 代码因为糟糕的 Javascript 代码而崩溃。

那么，让我们找到一种方法将 `String` 转换为 `Foreign`。 在 Pursuit 中搜索 `String -> Foreign`，因为 `Foreign` 是 Javascript 数据的类型，看看你能找到什么。

我不知道你怎么样，但我得到的是一个满满的空页面。好吧，那么我们需要思考这个问题。我们缺少什么？

`String` 可能是无效的 JSON。因此，我们搜索的类型签名应该考虑到这一点。让我们寻找 `String -> Maybe Foreign`。

好吧，我找到了 `readJSON_`，但它在另一个包中，而且它没有返回 `Foreign`。所以这行不通。

尝试 `String -> Either e Foreign`。

又是大空无。好吧，我不知道你怎么样，但我厌倦了猜测类型签名。让我们尝试猜测函数名。

好名字是什么？好吧，在 Javascript 中我们使用 `JSON.parse`，所以寻找 `parse`。

你找到了什么？

我找到了大量的 `parse` 函数。所以，我去了页面的底部并一直点击 `Load more results` 按钮，直到按钮消失，这意味着没有更多搜索结果。

然后我在页面中搜索 `Foreign` 并找到了：

```
parse :: String -> Either Error Foreign
```

这是在我从未见过的模块 `FFI.Foreign.JSON` 中，当我点击它时我发现：

## MODULE
`FFI.Foreign.JSON`

PACKAGE
`purescript-ffi-foreign`

REPOSITORY
`markfarrell/purescript-ffi-foreign`

latest (0.0.2)

## # parse

```
parse :: String -> Either Error Foreign
```

Source

## # stringify

```
stringify :: Foreign -> String
```

Source

好吧，看到版本号，0.0.2 并没有让我很有信心想要使用这个模块。

但当我查看页面时，我看到一个名为 `stringify` 的函数。我想知道如果我们搜索它会找到什么，因为这个名字相当独特。

去做吧，看看你是否能在我们信任的库中找到它。

好吧，我在值得信赖的库中只找到一个，那就是 `Argonaut`。但我们在这个解决方案中没有使用 `Argonaut`。

那么，让我们回到寻找 `parse`。搜索 `JSONParse` 时你会发现什么。

好吧，我什么都没得到。尝试 `parseJSON` 看看会有什么出现。

终于！！

```
parseJSON :: String -> F Foreign
```

这个函数在 `Foreign.JSON` 中，一个来自我们信任的包 `purescript-foreign-generic` 的模块。

有时候找到你要找的东西就像拔牙。你必须不断尝试你能想到的任何东西，直到你终于找到你要找的东西。

所以，我们在 PureScript 代码中调用 `_reverseKeys` 时会想要使用 `parseJSON`。

现在，我们已经克服了那个技术障碍，我们准备好编写 `foreign import` 行了。

继续使用我们在 `Ch27a.purs` 中做过的事情来帮助你编写将调用 Javascript 函数 `_reverseKeys` 的 PureScript 函数。

一直做到编译器用红色下划线你的整个文件。这可能在你完成之前就会发生。

我做到这里：

```
import Foreign (Foreign) ①

import Data.Function.Uncurried (Fn1, runFn1) ②

foreign import _reverseKeys :: Fn1 Foreign String ③
```

- ① 导入 `Foreign`。
- ② 导入调用非柯里化 Javascript 函数的辅助函数。意识到 1 个参数的函数按定义是柯里化的。
- ③ 定义 `Foreign` 函数类型签名。

就在这时，我在每一行上都得到了红色下划线。

但在我们深入错误之前，`_reverseKeys` 只接受 1 个参数。让我们删除 `Data.Function.Uncurried` 的导入，然后只使用一个普通的 Type Signature：

```
foreign import _reverseKeys :: Foreign -> String
```

不要忘记删除 `Data.Funtion.Uncurried`。

现在，对于那个错误。这是编译器错误：

![](img/8c0e9b687c62642e828ccb5481e11313_1258_0.png)

现在，当你得到这些错误时，这意味着编译器找不到你的 `Foreign` 函数或它在解析你的 Javascript 代码时遇到问题。

通常，这是因为你使用了更现代的 Javascript 元素。错误信息有一些解析信息，也许我们可以利用它来帮助我们：

接下来，我们将调用 `Object.entries` 来获取条目：

```
// for (const [key, value] of Object.entries(o)) {

const entries = Object.entries(o);

// ???
```

接下来，我们将编写一个传统的、老式的 `for` 循环：

```
// for (const [key, value] of Object.entries(o)) {

const entries = Object.entries(o);

for (var i = 0; i < entries.length; ++i) {

    // ???
    // the rest of the old for-loop

}
```

最后，我们需要从当前条目的第一个位置获取 `key`，从第二个位置获取 `value`：

```
// for (const [key, value] of Object.entries(o)) {

const entries = Object.entries(o);

for (var i = 0; i < entries.length; ++i) {

    const key = entries[i][0]; ① ③
    const value = entries[i][1]; ② ③
    // the rest of the old for-loop

}
```

- ① 从这对的第一个位置获取 `key`。
- ② 从这对的第二个位置获取 `value`。
- ③ 不要忘记 `const`。第一次编码时，我把它们漏掉了，这使得它们对这个模块是全局的。由于这个函数是递归的，递归调用会踩到这些全局变量。我讨厌 Javascript。

当我回到我的 PureScript 代码并保存它时，编译器错误消失了。这告诉我们我们的 Javascript 代码可以被 PureScript 编译器解析。

现在，让我们回到测试：

```
test :: Effect Unit

test = launchAff_ do

  results <- parSequence $ (\json -> Ajax.post ResponseFormat.string "http://localhost:3000/" $ Just $ RequestBody.String json)

    <$> [

      encodeJSON testTeacher

    , encodeJSON testStudent

    ]

  log $ case map (_.body) <$> sequence results of

    Left err -> Ajax.printError err

    Right [teacherJson, studentJson] ->

      show (runExcept $ decodeJSON teacherJson :: _ Teacher) <> "\n\n"

      <> show (runExcept $ decodeJSON studentJson :: _ Student)

    Right _ ->

      "The number of Ajax calls is different than what's being processed."
```

我们需要调用 `parseJSON` 将我们的 `String` 转换为 `Foreign`，以便调用 `_reverse`。并且我们将在 2 行上放置相同的代码。

并且查看 `parseJSON`，我们可以看到它的类型签名是：

```
parseJSON :: String -> F Foreign
```

这在 `F` Monad 中运行。但同样，`decodeJSON` 也是如此。所以现在，我们需要将它们绑定。

我有点希望我没有决定抛弃 `processJSON`。哦，算了。我们写过一次。我们可以再写一次。

这是我正在考虑的起点：

```
test :: Effect Unit

test = launchAff_ do

  results <- parSequence $ (\json -> Ajax.post ResponseFormat.string

    "http://localhost:3000/"

    $ Just $ RequestBody.String json)

    <$> [

      encodeJSON testTeacher

    , encodeJSON testStudent

    ]

  log $ case map (_.body) <$> sequence results of

    Left err -> Ajax.printError err

    Right [teacherJson, studentJson] ->

      show (runExcept $ decodeJSON teacherJson :: _ Teacher) <> "\n\n"

      <> show (runExcept $ decodeJSON studentJson :: _ Student)

    Right _ ->

      "The number of Ajax calls is different than what's being processed."

  where

    processJSON json = ???
```

我只添加了 `where` 部分。我们希望最终在 `processJSON` 中有 `runExcept`、`decodeJSON`、`parseJSON` 和 `_reverseKeys`。我们希望将所有这些复杂性包含在 `processJSON` 内部。

继续尝试，记住 `decodeJSON` 和 `parseJSON` 在 `F` Monad 中运行。当你完成或遇到砖墙时，继续阅读。

我知道 `runExcept` 会接受一个 `F a`，因为它展开为 `Except`。所以，我将从这里开始：

```
test :: Effect Unit

test = launchAff_ do

    results <- parSequence $ (\json -> Ajax.post ResponseFormat.string

        "http://localhost:3000/"

        $ Just $ RequestBody.String json)

        <$> [

            encodeJSON testTeacher

        , encodeJSON testStudent

        ]

    log $ case map (_.body) <$> sequence results of

        Left err -> Ajax.printError err

        Right [teacherJson, studentJson] ->

            show (runExcept $ decodeJSON teacherJson :: _ Teacher) <> "\n\n"

            <> show (runExcept $ decodeJSON studentJson :: _ Student)

        Right _ ->

            "The number of Ajax calls is different than what's being processed."

    where

        processJSON json = runExcept do ①

            ???
```

① `runExcept` 接收 `do` 块的结果，这意味着 `do` 必须是 `Except` 或 `F`。

现在，我需要在反转键之前先解析 JSON：

```
import Foreign.JSON (parseJSON) ①

test :: Effect Unit
test = launchAff_ do
  results <- parSequence $ (\json -> Ajax.post ResponseFormat.string "http://localhost:3000/" $ Just $ RequestBody.String json)
    <$> [
      encodeJSON testTeacher
    , encodeJSON testStudent
    ]
  log $ case map (_.body) <$> sequence results of
    Left err -> Ajax.printError err
    Right [teacherJson, studentJson] ->
      show (runExcept $ decodeJSON teacherJson :: _ Teacher) <> "\n\n"
      <> show (runExcept $ decodeJSON studentJson :: _ Student)
    Right _ ->
      "The number of Ajax calls is different than what's being processed."
where
  processJSON json = runExcept do
    o <- parseJSON json ② ③
    ???
```

① 添加此导入。

② `o` 表示我们将要交给 `_reverseKeys` 的 JSON 对象。

③ 如果此步骤因我们传入了错误的 JSON 字符串而失败，我们不会崩溃，而是会由于底层的 `ExceptT` 而被处理。将其与我们之前讨论的在 Javascript 代码中使用 `JSON.parse` 的情况进行对比。

如果卡住了，停止阅读并看看是否能现在完成这个。

接下来，我想反转键并将这些结果交给 `decodeJson`：

```
test :: Effect Unit
test = launchAff_ do
    results <- parSequence $ (\json -> Ajax.post ResponseFormat.string
        "http://localhost:3000/"
        $ Just $ RequestBody.String json)
        <$> [
            encodeJSON testTeacher
        , encodeJSON testStudent
        ]
    log $ case map (_.body) <$> sequence results of
        Left err -> Ajax.printError err
        Right [teacherJson, studentJson] ->
            show (runExcept $ decodeJSON teacherJson :: _ Teacher) <> "\n\n"
            <> show (runExcept $ decodeJSON studentJson :: _ Student)
        Right _ ->
            "The number of Ajax calls is different than what's being processed."
    where
        processJSON json = runExcept do
            o <- parseJSON json
            decodeJSON $ _reverseKeys o ①
```

① `decodeJSON` 返回一个 `F a`，所以这里不需要 `pure`。

现在，我们可以使用 `processJSON`：

```haskell

test :: Effect Unit

test = launchAff_ do

  results <- parSequence $ (\json -> Ajax.post ResponseFormat.string

      "http://localhost:3000/"

      $ Just $ RequestBody.String json)

    <$> [

      encodeJSON testTeacher

    , encodeJSON testStudent

    ]

  log $ case map (_.body) <$> sequence results of

    Left err -> Ajax.printError err

    Right [teacherJson, studentJson] ->

      show (processJSON teacherJson :: _ Teacher) <> "\n\n"
```
