

我将添加那个限定词：

```
processAjaxResult
  :: ∀ t129
    . Either Ajax.Error { body :: String | t129 } ①
    -> String
```

① 为限定 Error 属于哪个 Error 而添加了 Ajax. 前缀。

现在编译器很满意，但我们不满意。t129 代表什么。顺便说一下，你的数字可能是 94，也可能不是。没关系，因为你的数字同样没有帮助。

我们可以通过 t129 的使用方式看出它是一个 Row Type。传统做法是把这个叫做 r：

```
processAjaxResult
  :: ∀ r
    . Either Ajax.Error { body :: String | r }
    -> String
```

但等等。我们知道 Record 只是 Response a，其中 a 是一个 String：

```
processAjaxResult ①
  :: Either Ajax.Error (Ajax.Response String) ②
    -> String
```

① 由于我们不再使用 r，所以移除了 ∀。

② 由于 Affjax 是 qualified 导入，所以完全限定了 Response。

现在，这很棒，但它没有我希望的那么通用。看看 processAjaxResult 的类型签名和代码，看看在阅读我的分析之前你能否找到所有可以泛化的地方。

这是我做的分析：

```
processAjaxResult
  :: Either Ajax.Error (Ajax.Response String)
  -> String
processAjaxResult = case _ of
  Left err -> Ajax.printError err
  Right { body } ->
    case runExcept (decodeJSON body :: _ ReversedTeacher) of
      Left err -> show err
      Right reversedTeacher -> show reversedTeacher
```

① 我们只能解码 ReversedTeacher。这可以是任意 a。

② 如果我们把解码的内容泛化为某个 a，那么这个 a 最好要有 Show 实例。

③ 一旦我们可以解码任意 a，我们应该把 reversedTeacher 重命名为更通用的名字。

记住上一章的内容，类型签名中没有我们可以使用的 a。所以，在继续前进之前，先把它作为 Proxy 添加并进行上述泛化。

要做的第一个改变是添加 Proxy 参数：

```
import Type.Proxy (Proxy) ①

processAjaxResult
  :: ∀ a
  . Show a ②
  => Proxy a ③
  -> Either Ajax.Error (Ajax.Response String)
  -> String
processAjaxResult _ = case _ of ④
  Left err -> Ajax.printError err
  -- COMPILER ERROR!!
  Right { body } -> case runExcept (decodeJSON body :: _ a) of ⑤
    Left err -> show err
    Right reversedTeacher -> show reversedTeacher
```

① 为 Proxy 添加了导入。

② 约束 a 必须可显示。

③ 添加了 Proxy 参数类型。

④ 为 Proxy 添加了不关心的参数。

⑤ 解码 _ a 而不是 _ ReverseTeacher。

这是编译器错误：

```
{ grades: [ Preschool, Kindergarten,
, numberOfStudents: 23
, personal: {
  height: Centimeters 162.56
, weight: Kilograms 63.5
, age: Years 31
}
, status: NonTenured
}

processAjaxResult :: ∀ a. Show a => Pr
processAjaxResult _ = case _ of
  Left err -> Ajax.printError err
  Right { body } -> case runExcept $ (decodeJSON body :: _ a) of
    Left err -> show err

No type class instance was found for
Foreign.Generic.Class.Decode a1

while applying a function decodeJSON
of type Decode t2 => String -> ExceptT (NonEmpty
to argument body
while checking that expression decodeJSON body
has type t0 a1
in value declaration processAjaxResult
```

好吧，我记得要让它可显示，但忘了它也必须有 Decode 实例，因为我们在调用 decodeJSON，而它期望解码类型为 _ a 的值。

让我们修复它：

```
processAjaxResult
  :: ∀ a
    . Show a
    => Decode a ①
    => Proxy a
    -> Either Ajax.Error (Ajax.Response String)
    -> String
processAjaxResult _ = case _ of
  Left err -> Ajax.printError err
  Right { body } -> case runExcept (decodeJSON body :: _ a) of
    Left err -> show err
    Right reversedTeacher -> show reversedTeacher
```

① 添加了 Decode 约束。

现在编译器很满意。但我不满意。我看到还有一个可以改进的小地方。

注意变量名 reversedTeacher。这现在不准确了。它不再只是 Teacher 的反向版本。它可以是任意反向的 JSON 对象。

让我们把它重命名为 reversedRecord：

```
```haskell
processAjaxResult
  :: V a
  . Show a
  => Decode a
  => Proxy a
  -> Either Ajax.Error (Ajax.Response String)
  -> String

processAjaxResult _ = case _ of
  Left err -> Ajax.printError err
  Right { body } -> case runExcept (decodeJSON body :: _ a) of
    Left err -> show err
    Right reversedRecord -> show reversedRecord
```
```

① 将 `reverseTeacher` 重命名为 `reversedRecord`。

此时，停下来确保你的代码与此匹配，然后继续。

接下来，修改测试代码以在阅读任何进一步内容之前调用 `processAjaxResult`。

以下是利用 `processAjaxResult` 对 `test` 的更改：

```
```purescript
import Type.Proxy (Proxy(..)) ①

test :: Effect Unit
test = launchAff_ do
  result <- Ajax.post ResponseFormat.string
    "http://localhost:3000/"
    $ Just $ RequestBody.String $ encodeJSON teacher
  log $ processAjaxResult (Proxy :: _ ReversedTeacher) result ②
```
```

① 添加 `(..)` 以导入 `Proxy` 数据构造子。

② 给它一个类型为 `Proxy ReversedTeacher` 的 `Proxy`，但使用 `_` 代替 `Proxy`，因为编译器可以自行推断出那部分，我希望保持尽可能可读。

就为了好玩，运行测试并确保你得到：

```
```text
lanosrep: { ega: (Years 31), thgieh: (Centimeters 162.56), thgieh: (Kilograms 63.5) }, sedarg: [Preschool,Kindergarten,(Grade 1)], stnedutsForebmun: 23, sutats: NonTenured }
```
```

## 25.2.3. 使用 Argonaut 解码响应

复制所有代码并粘贴到名为 Ch25b 的新文件中。我们将在此文件中工作，所以确保关闭 Ch25a。

同时更改你的 Main 以调用 Ch25b 的 test 函数。

修改 Ch25b 的模块名为 Ch25b。

我们需要在 spago.dhall 中添加 Argonaut 库。去 Pursuit 查看需要在 spago.dhall 文件中添加什么。然后添加它并构建。然后继续阅读。

spago.dhall 文件中需要更新以下内容：

```
{-
Welcome to a Spago project!
You can edit this file as you like.
-}
{ name = "my-project"
, dependencies =
  [ "aff"
  , "aff-bus"
  , "affjax"
  , "argonaut" ①
  , "arrays"
  , "avar"
  , "bifunctors"
  , "console"
  , "contravariant"
  , "control"
  , "datetime"
  , "effect"
  , "either"
  , "exceptions"
  , "foreign-generic"
  , "foldable-traversable"
  , "integers"
  , "lists"
  , "maybe"
  , "newtype"
  , "nonempty"
  , "prelude"
  , "profuntor"
  , "psci-support"
  , "random"
  , "strings"
  , "tailrec"
  , "transformers"
  , "tuples"
  , "unfoldable"
  , "unicode"
  , "debug"
  ]
, packages = ./packages.dhall
, sources = [ "src/**/*.purs", "test/**/*.purs" ]
}
```

① 再次将其放在此处以保持字母顺序。

然后只需确保我们这样做是正确的，我们应该运行：

```
npx spago build
```

现在，我们准备开始显式编写解码器来处理 Echo Server 反转我们键的倾向。我们将首先删除所有 Reversed 版本的记录。

请确保你在删除 ReversedPersonal、ReversedStudent 和 ReversedTeacher 之前正在编辑 Ch25b。

当你这样做时，test 的最后一行将不再编译，所以将其注释掉并暂时用 pure unit 替换它以便编译：

```
test :: Effect Unit
test = launchAff_ do
  -- COMPILER WARNING!!
  result <- Ajax.post ResponseFormat.string
    "http://localhost:3000/"
    $ Just $ RequestBody.String $ encodeJSON teacher
  -- log $ processAjaxResult (Proxy :: _ ReversedTeacher) result
  pure unit
```

事实上，现在就注释掉 Ajax.post 行，因为我们也要破坏它：

```
test :: Effect Unit
test = launchAff_ do
  -- result <- Ajax.post ResponseFormat.string
  --   "http://localhost:3000/"
  --   $ Just $ RequestBody.String $ encodeJSON teacher
  -- log $ processAjaxResult (Proxy :: _ ReversedTeacher) result
  pure unit
```

此时，编译器警告我们导入语句中有冗余导入。我们稍后会修复这些，因为我们会不断破坏它们。

由于我们不再需要 decodeOptions，我们可以删除它。当你这样做时，请特别注意代码现在损坏的所有地方。这些都是我们需要从使用 Foreign 解码 JSON 改为使用 Argonaut 的地方。

你应该得到编译错误的地方有 2 处：

