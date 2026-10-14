
```
    Right _ ->

      "The number of Ajax calls is different than what's being processed."

where

  processJSON = lmap show <<< runExcept ①
```

① 使用 Point-free 记法提取了公共代码。

这是一个意外的编译器错误：

![](img/8c0e9b687c62642e828ccb5481e11313_1247_0.png)

这是一种我们不太常见的错误类型。

仔细看看 `processJSON`，弄清楚它的类型是什么。在继续之前花一分钟做这件事。

很难弄清楚，对吧？

好吧，编译器已经弄清楚了它的类型，但它不告诉我们。所以，我们要哄着它告诉我们。

把有编译器错误的那行注释掉。然后为 `processJSON` 添加一个 Type Hole 作为完整的类型签名。

然后看看你会得到什么。在继续阅读之前完成这些。

以下是这些改动：

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

  log $ case map ( _.body) <$> sequence results of

    Left err -> Ajax.printError err

    Right [teacherJson, studentJson] ->

      show (processJSON

        $ decodeJSON teacherJson :: _ Teacher) <> "\n\n"

        -- <> show (processJSON

        --   $ decodeJSON studentJson :: _ Student)

    Right _ ->

      "The number of Ajax calls is different than what's being processed."

  where

    processJSON :: ?x

    processJSON = lmap show <<< runExcept
```

1. 注释掉了有问题的代码行。
2. 为类型签名添加了 Type Hole。注意我没有使用 `_`。这是因为使用 `_` 意味着编译器会推断出它是什么，而且不会给我们编译器警告。

以下是推断出的类型签名：

```
Except (NonEmptyList ForeignError) Identity Teacher

  -> Either String Teacher
```

看到 `Teacher` 出现的两处了吗？那是因为编译器无法知道我们想要在这些位置使用 `a`。

它只知道我们如何使用它，而在这种情况下，我们是在 `Teacher` 上使用它。当编译器为 `processJSON` 的第一次使用推断类型时，它并不知道我们稍后会在代码中用一个完全不同的类型来使用它。

因为推断过程是局部化的，所以编译器**过度特化**了该类型。

所以，这里有一个案例，我们必须显式提供一个更通用的类型签名，以便我们可以使用 `processJSON` 处理除 `Teacher` 之外的其他类型。

继续取消注释有问题的代码。然后用该推断类型的通用版本替换类型孔。同时，在你的类型签名中使用 `F`。

在继续之前先完成此操作。

为了使类型签名通用化，我们将从 `F` 的类型开始，即我们从类型孔中得到的那一个，然后逐步过渡到类型签名中的内容：

```
type F = Except MultipleErrors

type Except e = ExceptT e Identity

type MultipleErrors = NonEmptyList ForeignError

--------

ExceptT (NonEmptyList ForeignError) Identity Teacher

Except (NonEmptyList ForeignError) Teacher

Except MultipleErrors Teacher

F Teacher
```

- ① `F` 的定义。
- ② `Except` 的定义。
- ③ `MultipleErrors` 的定义。
- ④ `processJSON` 的第一个参数的推断类型。
- ⑤ `Except` 的定义替换。
- ⑥ `MultipleErrors` 的定义替换。
- ⑦ `F` 的定义替换。

因此，推断的类型只是 `F Teacher`，如果我们将其泛化，它将是 `F a`：

```
import Foreign (F) ①

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

      show (processJSON

        $ decodeJSON teacherJson :: _ Teacher) <> "\n\n"

      <> show (processJSON

        $ decodeJSON studentJson :: _ Student) ②

    Right _ ->

      "The number of Ajax calls is different than what's being processed."

where

  processJSON :: ∀ a. F a -> Either String a ③

  processJSON = lmap show <<< runExcept
```

- ① 导入 `F`。
- ② 已取消注释。
- ③ 用推断类型的通用版本替换类型孔。

顺便说一下，另一种快速确定 `processJSON` 输入类型的方法是查看 `decodeJSON` 的输出类型，因为我们正在用其输出调用 `processJSON`：

```
decodeJSON :: ∀ a. Decode a => String -> F a
```

我们可以看到它返回 `F a`，这就是 `processJSON` 的输入。这本是最快弄清楚的方法。下次，也许我们先尝试这种方法。

现在，我们的新模块第一次干净地编译了。

现在，我们准备运行代码。

首先，在 VSCode 或你正在使用的任何终端程序中打开另一个终端窗口并运行：

```
node src/echo-server.js
```

然后编辑 `Main.purs` 以调用 `Ch27b` 而不是 `Ch27a`。

然后运行程序，看看你得到什么。

看起来我们需要在 `spago.dhall` 中添加 `foreign`：

```
[error] Some of your project files import modules from packages that are not in the direct dependencies of your project.

To fix this error add the following packages to the list of dependencies in your config:

- foreign
```

现在当我修复它并重新运行代码时，我得到：

```
(Left "(NonEmptyList (NonEmpty (ErrorAtProperty \"tag\" (TypeMismatch \"String\" \"Undefined\")) Nil))")

(Left "(NonEmptyList (NonEmpty (ErrorAtProperty \"tag\" (TypeMismatch \"String\" \"Undefined\")) Nil))")
```

首先，它不起作用。

其次，你注意到到处都是 `\"` 吗？这通常意味着我们多加了一个 `show`。如果显示一个 `String`，它会在该 `String` 周围加上双引号。

让我们从 `processJSON` 中移除 `lmap show`，看看是否能清除嵌入的引号：

```
import Foreign (F, MultipleErrors) ① ②

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

      show (processJSON

        $ decodeJSON teacherJson :: _ Teacher) <> "\n\n"

      <> show (processJSON

        $ decodeJSON studentJson :: _ Student)

    Right _ ->

      "The number of Ajax calls is different than what's being processed."

where

  processJSON :: ∀ a. F a -> Either MultipleErrors a ③

  processJSON = runExcept ④
```

- ① 移除了 `Data.Bifunctor` 的导入，因为我们不再使用 `lmap`。
- ② 将 `MultipleErrors` 添加到导入列表中。
- ③ 由于我们不再对其进行 `show` 映射，因此必须更改返回类型。
- ④ 移除了 `lmap show`。

从技术上讲，我们不再需要 `processJSON`。因此，让我们将其移除。是的，经过所有这些工作后，我们要将其移除：

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

移除了 `import Foreign`。

如果我每写、调试并最终扔掉一行代码就能得到一美元，我就富有了。

对你的代码进行这些更改并运行，看看现在显示什么。

我得到的是：

```
[warn] None of your project files import modules from some projects that are in the direct dependencies of your project.

These dependencies are unused. To fix this warning, remove the following packages from the list of dependencies in your config:

- foreign
```

好吧，看起来 `foreign` 再次不再是我们程序的直接依赖项。所以将其移除。抱歉。

现在，重新运行，这就是我得到的结果：

```
(Left (NonEmptyList (NonEmpty (ErrorAtProperty "tag" (TypeMismatch "String" "Undefined")) Nil)))

(Left (NonEmptyList (NonEmpty (ErrorAtProperty "tag" (TypeMismatch "String" "Undefined")) Nil)))
```

好吧，这更好。当它不起作用时，它打印出更好的消息。

但为什么它不起作用？

如果花时间检查它，消息应该能告诉我们。它似乎期望一个名为 `tag` 的属性，类型为 `String`，但它是 `Undefined`。

所以这告诉我们该键不存在。

但为什么呢？

如果你在想我们还没有反转键，你是对的。

我们需要这样做。花一分钟想想你如何在 Javascript 中完成此操作。你会采取什么方法？

我知道我会怎么做。我会抄袭回显服务器的代码。它正在接收一个 JSON 对象并递归地反转它遇到的所有对象的键，这正是我们需要的。

所以，创建一个名为 `Ch27b.js` 的新文件。复制回显服务器中执行 JSON 反转键的代码。然后返回这里。

以下是应复制到 `Ch27b.js` 的代码：

```javascript
const reverseArray = a => {

  var na = [];

  for (var i = 0; i < a.length; ++i) {

    const value = a[i];

    const nValue = value.constructor.name == 'Object'

      ? reverseKeys(value) : value;

    na.push(nValue);

  }

  return na;

}

const reverseKeys = o => {

  const no = {};

  for (const [key, value] of Object.entries(o)) {

    const nValue = value.constructor.name == 'Object'

      ? reverseKeys(value)

      : (value.constructor.name == 'Array'

        ? reverseArray(value) : value);

    no[key.split("").reverse().join("")] = nValue;

  }

  return no;

};
```

如果这对回显服务器有效，对我们也应该有效。我们唯一需要做的就是使其可以从 PureScript 调用。

首先在 `Ch27b.js` 中导出 `reverseKeys`。如果需要帮助，可以查看 `Ch27a.js` 看看我们之前是如何做的。

进行此更改，然后返回这里。

以下是添加的代码：

```javascript
exports._reverseKeys = reverseKeys;
```

现在，我们准备像以前一样向我们的代码添加 `foreign import`。继续尝试并在卡住或完成时返回这里。

好吧，也许我们有点操之过急了。我们从未考虑过 `reverseKeys` 的类型。看看那个函数，看看你是否能判断它的类型是什么。

它是一个 Javascript 对象。所以，我们需要传递一个 Javascript 对象。但我们在 PureScript 中如何做到这一点？

我们正在将一个 `String` 传递给 `decodeJSON`。所以，我们可以只更改我们的 Javascript 来执行：

```javascript
exports._reverseKeys s = reverseKeys(JSON.parse(s)); // NOT IDEAL!!
```
