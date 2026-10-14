

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

① 添加此导入。

② o 表示我们将要交给 _reverseKeys 的 JSON 对象。

③ 如果此步骤因我们传入了错误的 JSON 字符串而失败，我们不会崩溃，而是会由于底层的 ExceptT 而被处理。将其与我们之前讨论的在 Javascript 代码中使用 JSON.parse 的情况进行对比。

如果卡住了，停止阅读并看看是否能现在完成这个。

接下来，我想反转键并将这些结果交给 decodeJson：

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

① decodeJSON 返回一个 F a，所以这里不需要 pure。

现在，我们可以使用 processJSON：

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
    _ -> show (processJSON studentJson :: _ Student)
    Right _ ->
      "The number of Ajax calls is different than what's being processed."
  where
    processJSON json = runExcept do
      o <- parseJSON json
      decodeJSON $ _reverseKeys o
```

① 在这 2 处使用 `processJSON`。

让我们看看那个讨厌的编译器错误：

![](img/8c0e9b687c62642e828ccb5481e11313_1266_0.png)

我们之前见过这个错误。编译器再次过度特化了。

确保你的 test 代码与上面的代码匹配。

然后注释掉有问题的代码行。

最后，像上次那样为 `processJSON` 添加一个带有类型孔的类型签名，以查看编译器推断出的类型。

然后将该类型进行泛化。一旦编译通过，就取消注释有问题的代码行，希望一切都能编译。

试试看，并在完成或卡住时返回这里。

好吧，这里是所有这些更改直到类型孔：

```
test :: Effect Unit
test = launchAff_ do
  results <- parSequence $ (\json -> Ajax.post ResponseFormat.string "http://localhost:3000/" $ Just $ RequestBody.String json)
    <$> [
      encodeJSON testTeacher
    , encodeJSON testStudent
    ]
  log $ case map (_ . body) <$> sequence results of
    Left err -> Ajax.printError err
    Right [teacherJson, studentJson] ->
      show (processJSON teacherJson :: _ Teacher) <> "\n\n"
      -- <>  show (processJSON studentJson :: _ Student) ①
    Right _ ->
      "The number of Ajax calls is different than what's being processed."
where
  processJSON :: ?x ②
  processJSON json = runExcept do
    o <- parseJSON json
    decodeJSON $ _reverseKeys o
```

① 注释掉了有问题的行。

② 添加了带有类型孔的类型签名。

它推断出的类型如下：

```
String -> Either (NonEmptyList ForeignError) Teacher
```

但由于：

```
type MultipleErrors = NonEmptyList ForeignError
```

我们可以简化为：

```
String -> Either MultipleErrors Teacher
```

现在，我们可以将其泛化为：

```
∀ a. String -> Either MultipleErrors a
```

添加它后得到：

```
import Foreign (Foreign, MultipleErrors) ①

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
      show (processJSON teacherJson :: _ Teacher) <> "\n\n"
      -- <>  show (processJSON studentJson :: _ Student)
    Right _ ->
      "The number of Ajax calls is different than what's being processed."
  where
    processJSON :: ∀ a. String -> Either MultipleErrors a ②
    processJSON json = runExcept do
      o <- parseJSON json
      decodeJSON $ _reverseKeys o -- COMPILER ERROR!!
```

① 将 MultipleErrors 添加到导入列表中。

② 添加了我们泛化的类型签名。

现在，又出现了一个编译器错误：

![](img/8c0e9b687c62642e828ccb5481e11313_1269_0.png)

好吧，与我们上次的 processJSON 不同，这里我们调用了 decodeJSON，所以我们需要相应地约束 a：

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
      show (processJSON teacherJson :: _ Teacher) <> "\n\n"
      <> show (processJSON studentJson :: _ Student) ①
    Right _ ->
      "The number of Ajax calls is different than what's being processed."
  where
    processJSON :: ∀ a. Decode a => String -> Either MultipleErrors a ②
    processJSON json = runExcept do
      o <- parseJSON json
      decodeJSON $ _reverseKeys o
```

① 取消注释。

② 将 a 约束为具有 Decode 实例。

对你的代码进行这些更改（不要忘记取消注释）并运行它，看看是否有效。

现在我们必须在 spago.dhall 文件中重新添加 foreign：

```
[error] Some of your project files import modules from packages that are not in the direct dependencies of your project.
To fix this error add the following packages to the list of dependencies in your config:
- foreign
```

一旦修复，我们运行它来看看是否有效。而它并没有：

```
(Left (NonEmptyList (NonEmpty (ForeignError "Unexpected token o in JSON at position 1") Nil)))

(Left (NonEmptyList (NonEmpty (ForeignError "Unexpected token o in JSON at position 1") Nil)))
```

但为什么不呢？我们从哪里开始查找？

嗯，我们可以看到解码失败了。所以，让我们使用 spy 看看我们给 decodeJSON 的是什么：

```
import Debug (spy)

-- REDACTED test code above the where section
where
processJSON :: ∀ a. Decode a => String -> Either MultipleErrors a
processJSON json = runExcept do
  o <- parseJSON json
  decodeJSON $ spy "json" $ _reverseKeys o ①
```

① 在 decodeJSON 和 _reverseKeys 之间添加了 spy。谈论中间人攻击。

进行此更改并在你的 `spago.dhall` 中添加 debug（如果还没有）。

现在运行它，看看控制台打印了什么。从中，你有足够的信息来弄清楚这个问题。

一开始可能并不明显。花了我几分钟，但当我意识到时，我觉得自己很蠢，因为我写了这段代码，即使这是一个很容易犯的错误。

试试看，看看你是否能发现我的错误。

以下是输出的部分列表：

