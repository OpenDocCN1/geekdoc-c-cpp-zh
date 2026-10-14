

![](img/8c0e9b687c62642e828ccb5481e11313_1214_0.png)

你能看出我哪里出错了吗？

我们期望 `sequence` 返回一个 `Either` 但我却将其结果用作 `Aff`。我本应该在这里直接使用一个 `let`：

```
```purescript
test :: Effect Unit
test = launchAff_ do
  results <- parseSequence $ (\json -> Ajax.post ResponseFormat.json
    "http://localhost:3000/"
    $ Just $ RequestBody.String json)
  <$> [
      encodeJSON testTeacher
    , encodeJSON testStudent
    ]
  let bodies = sequence results
  pure unit
```
```

我忘记从 `Response` 中提取 `body`。如果还没做，现在就先做，然后再继续阅读。

我们可以使用 `map` 来提取 `body`：

接下来，我们需要对 2 个不同的 Json 值进行不同的处理，因为一个是 Teacher 编码的，另一个是 Student 编码的。

查看 processAjaxResult 看看我们可以借用什么来将它们解码为 Teacher 和 Student，然后再转成字符串。

一旦你明白该怎么做，就在继续之前修改测试代码。

我们将使用 decodeJson 和 show：

```
test :: Effect Unit
test = launchAff_ do
  results <- parSequence $ (\json -> Ajax.post ResponseFormat.json
    "http://localhost:3000/"
    $ Just $ RequestBody.String json)
    <$> [
      encodeJSON testTeacher
    , encodeJSON testStudent
    ]
  log $ case map (_.body) <$> sequence results of -- COMPILER ERROR!!
    Left err -> Ajax.printError err
    Right [teacherJson, studentJson] ->
      show (decodeJson teacherJson :: _ Teacher) <> "\n\n" ①
      <> show (decodeJson studentJson :: _ Student)
```

① 我们在两者之间用几个换行符解码并显示。

编译器错误说：

![](img/8c0e9b687c62642e828ccb5481e11313_1216_0.png)

我漏掉了这里的最后一个 case，即当 Array 的长度不是 2 时。我们知道这种情况总会发生，但如果上面的代码发生变化而 case 表达式没有更新，我们最好给出一个友好的提示：

```
test :: Effect Unit
test = launchAff_ do
    results <- parSequence $ (\json -> Ajax.post ResponseFormat.json
        "http://localhost:3000/"
        $ Just $ RequestBody.String json)
    <$> [
        encodeJSON testTeacher
      , encodeJSON testStudent
    ]
    log $ case map (_body) <$> sequence results of
        Left err -> Ajax.printError err
        Right [teacherJson, studentJson] ->
            show (decodeJson teacherJson :: _ Teacher) <> "\n\n"
            <> show (decodeJson studentJson :: _ Student)
        Right _ ->
            "The number of Ajax calls is different than what's being processed."
```

现在就进行此更改，然后清理未使用的导入。

最后，运行它看看结果。

当然，spago 抱怨道：

```
[error] Some of your project files import modules from packages that are not in the direct dependencies of your project.
To fix this error add the following packages to the list of dependencies in your config:
- parallel
```

添加它然后再次运行。当我这样做时，我得到：

```
(Right (Teacher { grades: [Preschool,Kindergarten,(Grade 1)],
numberOfStudents: 23, personal: (Personal { age: (Years 31), height:
(Centimeters 162.56), weight: (Kilograms 63.5) }), status: NonTenured }))

(Right (Student { gpa: (GPA 3.2), grade: (Grade 1), personal: (Personal { age:
(Years 5), height: (Centimeters 107.9), weight: (Kilograms 17.9) }), teacher:
(Teacher { grades: [Preschool,Kindergarten,(Grade 1)], numberOfStudents: 23,
personal: (Personal { age: (Years 31), height: (Centimeters 162.56), weight:
(Kilograms 63.5) }), status: NonTenured }) }))
```

我们已经以我们计划的所有方式解码了我们类型的反向键版本，除了使用 Javascript。

但是，我们必须等到学会如何从 PureScript 代码调用 Javascript 之后才能做到这一点。

不要忘记使用 VSCode 终端下拉菜单切换终端窗口并用 `Ctrl-C` 杀死 Echo Server。

## Chapter 26. Foreign Function Interface (FFI)

有一个庞大的 Javascript 生态系统，其中包含各种用途的库。我们已经看到了对 Node 内置模块的包装，例如 `Node.FS.Async`。你可能会想知道这些库如何与 PureScript 接口。

有一个称为 *Foreign Function Interface*，或简称 *FFI* 的机制，允许 PureScript 直接与 Javascript 接口。

由于 PureScript 并非无所不能，有时我们被迫编写 Javascript 或接口到尚未被包装的库。

在这些情况下，我们需要了解 FFI 如何工作。

让我们看一个简单的例子来调用 Node 的 path 模块中的 `join`：

```
```purescript
module NodePath where

type FilePath = String

foreign import joinPath :: FilePath -> FilePath -> FilePath
```
```

❶ foreign import 指定该函数是用 Javascript 编写的。

假设这段代码在名为 `NodePath.purs` 的文件中。那意味着我们的 Javascript 代码必须在名为 `NodePath.js` 的文件中，并且必须与 `NodePath.purs` 在同一目录中，否则代码无法编译。

我们将如何编写 Javascript 代码：

```
```javascript
const path = require('path');

exports.joinPath = function(start) {
  return function(end) {
    return path.join(start, end);
  };
};
```
```

注意 Javascript 函数是手动柯里化的。顶层函数接收一个参数并返回一个函数，该函数接收一个参数并返回 Node 的 `join` 的结果。

该描述与 PureScript 定义相匹配：

```
```purescript
foreign import joinPath :: FilePath -> (FilePath -> FilePath)
```
```

① 添加了冗余的括号以帮助查看柯里化。

我们也可以使用更现代的语法编写 Javascript，使柯里化更容易看到和编码：

```
const path = require('path');

exports.joinPath = start => end => {
  return path.join(start, end);
};
```

现在当我们运行以下测试代码时：

```
test :: Effect Unit
test = do
  log $ joinPath "abc" "xyz.txt"
```

我们在控制台上得到以下输出：

```
abc/xyz.txt
```

我们也可以以更传统的意义编写 Javascript，即非柯里化：

```
const path = require('path');

exports.joinPathImpl = (start, end) => {
  return path.join(start, end);
};
```

但现在，我们需要使用特殊的辅助函数来调用它：

```
import Data.Function.Uncurried (Fn2, runFn2) ① ②

foreign import joinPathImpl :: Fn2 FilePath FilePath FilePath ③ ④

joinPath :: FilePath -> FilePath -> FilePath ⑤
joinPath p1 p2 = runFn2 joinPathImpl p1 p2 ⑥ ⑦
```

① 导入 Fn2 类型用于接收 2 个参数的外来函数。
② 导入 runFn2 函数用于调用 2 个参数且为非柯里化的外来函数。

+   ③ 从普通的函数类型签名改为 Fn2 类型。
+   ④ 重命名为带有 Impl 后缀。这是 FFI 的一种惯用命名约定。
+   ⑤ 这是从其他 PureScript 函数调用的函数。
+   ⑥ 使用 runFn2 调用非柯里化的 Javascript 函数。
+   ⑦ 不要将它们写成点自由形式。当使用 runFn0 到 runFn10 时，如果函数参数完全饱和，即未部分应用，编译器会内联这些调用。

运行此代码仍然产生相同的输出：

```
abc/xyz.txt
```

两种方法都很好，但当你调用一个 Javascript 库，其中没有任何函数是柯里化时，使用 Data.Function.Uncurried 是最简单的解决方案。

### 26.1. FFIs That Return PureScript Types

你永远不应该直接从 Foreign 代码调用 PureScript 函数。例如，这里是如何创建 Maybe 的：

```
Data_Maybe.Just.create(x)
Data_Maybe.Nothing.value
```

这两种方式都有两个脆弱的原因。首先，编译器会进行死代码移除以减少生成的 Javascript 代码大小。如果你的代码出于某种原因没有使用 Just，那么 Data_Maybe.Just.create 可能在死代码移除期间被消除。

另一个原因是代码生成器可能会随着编译器新版本的发布而以不同的方式生成 PureScript 代码。虽然 Data_Maybe.Just.create 今天可能有效，但不能保证将来有效。

解决办法是将 Javascript 代码可能需要调用的任何 PureScript 函数作为参数传递给该函数，例如：

```
exports.doSomethingImpl = (just, nothing, p1) {
  if (result = doSomething(p1))
    return just(result);
  else
    return nothing;
};
```

