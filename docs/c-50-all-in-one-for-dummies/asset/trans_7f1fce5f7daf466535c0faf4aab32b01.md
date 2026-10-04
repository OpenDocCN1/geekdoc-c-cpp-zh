

使用 `String.Concat()` 方法结束句子。程序会输出直接结果，以便用户查看正在发生什么。

遍历数组是查找各种可能值之一的经典方法。（我将在下一节中向你展示另一种方法，并在第二本书中展示一种更酷的方法。）

这里是 `BuildASentence` 程序的示例运行：

```
你输入的每行都将被添加到句子中，直到你输入 EXIT 或 QUIT
Enter a string
Programming with

You’ve entered: Programming with
Enter a string
C# is fun

You’ve entered: Programming with C# is fun
Enter a string
(more or less)

You’ve entered: Programming with C# is fun (more or less)
Enter a string
EXIT

Total sentence:
Programming with C# is fun (more or less)
Press Enter to terminate...
```

我将我的输入加了**粗体**，以便输出更易读。

## 你希望比较时区分或不区分大小写？

上一个示例中使用的 `Compare()` 方法认为 "EXIT" 和 "exit" 是两个不同的字符串。然而，`Compare()` 方法还有一个包含第三个参数的第二个。该参数指示比较是否应该忽略字母大小写。`true` 表示“忽略”。

`BuildASentence` 示例中冗长的终止部分的以下版本无论传递的字符串是大写、小写还是两者的组合，都将退出设置为 `true`：

```csharp
// 如果传递了 exit 或 quit，则指示为 true，
// 忽略大小写。
if (String.Compare("exit", source, true) == 0 ||
    (String.Compare("quit", source, true) == 0)
{
    quitting = true;
}
```

这个版本比之前的循环版本更简单。代码不需要担心大小写，并且可以使用单个条件表达式，因为现在只有两个选项需要考虑，而不是更长的列表：QUIT 或 EXIT 的任何拼写变体。

## 如果我想切换大小写怎么办？

你可能对字符串中的所有字符（或只是一个字符）是大写字母还是小写字母感兴趣。你可能需要在它们之间进行转换。

### 区分全大写和全小写字符串

我几乎不想提到它，但你可以使用 `switch` 命令（参见本迷你书籍的第 5 节）来查找特定的字符串。通常，你使用 `switch` 命令将计数数字与一组可能的值进行比较；然而，`switch` 也可以作用于字符串对象。`BuildASentence` 中这个版本的终止部分使用了 `switch` 结构：

```csharp
switch(line)
{
    case "EXIT":
    case "exit":
    case "QUIT":
    case "quit":
        return true;
}
return false;
```

这种方法之所以有效，是因为你只比较有限数量的字符串。`for` 循环为搜索字符串值提供了更灵活的方法。在上一节中使用不区分大小写的 `Compare()` 使程序在理解用户方面更大的灵活性。

## 将字符串转换为大写或小写

假设你有一个小写的字符串并需要将其转换为大写。你可以使用 `ToUpper()` 方法：

```csharp
string lowercase = "armadillo";
string upcase = lowercase.ToUpper();  // ARMADILLO.
```

同样，你可以使用 `ToLower()` 将大写转换为小写。

如果你只想将字符串中的第一个字符转换为大写呢？以下这段相当复杂的代码可以实现（但你可以在本章的最后一节看到更好的方法）：

```csharp
string name = "chuck";
string properName =
    char.ToUpper(name[0]).ToString() + name.Substring(1, name.Length - 1);
```

这个示例的思路是提取 `name` 中的第一个字符（即 `name[0]`），通过 `ToString()` 将其转换为单字符字符串，然后通过 `Substring()` 在移除旧的小写第一个字符后，加上 `name` 的剩余部分。

你可以使用这个看起来很可怕的 `if` 语句来判断字符串是大写还是小写：

```csharp
if (string.Compare(line.ToUpper(CultureInfo.InvariantCulture),
    line, false) == 0) ... // 如果 line 全是大写，则为真。
```

这里 `Compare()` 方法将 `line` 的大写版本与 `line` 本身进行比较。如果 `line` 已经是大写的，则没有差异。你可以研究 `CultureInfo.InvariantCulture` 工具，因为我不会在这里解释它。对于“是否全小写”，请在 `Compare()` 调用前加一个非 (`!`) 运算符。或者，你可以像下一节描述的那样使用循环。

网站上的 `StringCaseChanging` 示例说明了这些和其他技术，包括对文化的简要解释。

![](img/6df7bb88e9302e93)

### 遍历字符串

你可以使用 `foreach` 循环访问字符串中的字符。以下代码逐个处理：

```csharp
string favoriteFood = "cheesurgers";
foreach (char c in favoriteFood)
{
    Console.WriteLine(c);
}
```

## 搜索字符串

如何判断字符串是否为空 ("") 或为 `null`？（`null` 意味着尚未赋值）。使用 `IsNullOrEmpty` 方法，如下所示：

```csharp
bool notThere = string.IsNullOrEmpty(favoriteFood); // False
```

你可以通过两种方式将字符串设置为空字符串：

```csharp
string name = "";
string name = string.Empty;
```

如果你想找到某个字符，可以使用索引表示法。数组从零开始，所以如果你想要第一个字符，就请求 `[0]`。如果你想要第三个，就请求 `[2]`。

```csharp
char thirdChar = favoriteFood[2]; // "cheesurgers" 中的 'e'
```
