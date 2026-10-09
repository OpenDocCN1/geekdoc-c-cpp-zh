

![](img/25af69ec45b3c0b589a8dccd0c2a88be_80_0.png)

鼓励读者阅读每个示例源代码，例如从上到下，即使它可能意义不大。你会认出你已经知道的东西，以及你不知道的东西。这是学习过程中非常重要的一部分。

## 4.2.1. 解释

该程序询问用户的姓名，并使用该姓名来个性化问候语。

让我们尝试运行该程序：

```bash
dotnet run
```

它打印出以下“问题”：

```text
What is your name?
```

如果你用例如“joe”来“回答”它，则它会向终端打印出以下个性化问候语。

```text
Hello JOE! How are you?
```

整个“对话”可能看起来像这样：

```text
What is your name?
Jill               ①
Hello JILL! How are you?
```

① 你在终端上提供的输入。你输入例如“jill”，然后按回车键（换行）。然后，程序读取你的输入并执行下一步指令。

## 4.2.2. 语法

这个示例代码主要基于我们到目前为止已经涵盖的内容。

这里有 `var` 声明（第 2 行和第 10 行）。有一个 `if/else` 语句（第 4-8 行）。我们使用 `System` 命名空间中的 `Console.WriteLine()` 静态方法将文本打印到终端（第 1 行和第 11 行）。如前所述，`System` 命名空间的 `using` 声明是隐式的。

在第二行中，虽然我们之前没有见过 `ReadLine()`，但我们很容易猜到它是定义在 `Console` 类中的一个静态方法（基于其语法/形式）。

空行大多被编译器忽略。它们通常用于提高可读性（第 3 行和第 9 行）。

![](img/25af69ec45b3c0b589a8dccd0c2a88be_81_0.png)

我们可以添加成千上万个空行，这对编译器来说差别不大。然而，过度使用空行，或者通常的空白字符，会降低可读性。☺

这个示例代码从控制台或“stdin”读取输入，而不是从命令行参数获取。

在第 1 行，它首先打印出一个作为提示用户的“问题”。此时他知道/她知道期望输入，特别是用户的姓名。然后程序等待用户输入。

C# 程序有多种处理用户输入的方式。示例代码使用了 `System` 命名空间中 `Console` 类的另一个静态方法 `ReadLine()`。`Console.ReadLine()` 方法将用户输入作为字符串返回。我们将返回值用于初始化局部变量 `name`。因此，`name` 的类型是 `string`。（更准确地说，它是一个“可空字符串”。关于可空引用类型的讨论将推迟到本书稍后部分。）

如果用户没有输入任何内容（只是按了回车键），则返回值可能是空字符串。我们可以使用 .NET 中 `System.String` 类的静态方法 `IsNullOrEmpty()` 来确定是否输入了任何非空字符串。示例代码使用了泛化版本 `string.IsNullOrWhiteSpace`。如果给定的字符串参数（在此处为 `name`）为 `null` 或为空，或仅包含空格如 `" "`，则评估结果为 `true`。

![](img/placeholder.png) `string.IsNullOrWhiteSpace(name)` 在本质上等同于（`name is null || name.Trim() == ""`）。`Trim()` 方法移除字符串开头和结尾的所有空格（如果有）。注意调用这两个方法时语法的差异：`string.IsNullOrWhiteSpace(name)` 与 `name.Trim()`。`Trim()` 是一个“实例方法”。

如果没有提供“有效”的输入字符串，我们 simply 将姓名设置为“Friend”（`if` 块）。如果提供了非空姓名（在移除所有前导和尾随空格后），那么，仅为说明起见，我们将姓名改为全大写字母（`else` 块）。为此，我们使用来自 `name` 对象的“实例方法” `ToUpper()`。

注意语法。方法 `ToUpper()` 使用“点号表示法”在 `name` 上调用。方法 `ToUpper()` 定义在 `System.String` 类中，但它用于 `String` 类的“实例”上，即本例中的 `name`。如上所述，像这样的方法被称为“实例方法”。

![](img/placeholder.png) 我们将在整本书中讨论静态方法/属性与实例方法/属性之间的区别，以及何时使用哪一个。但是，如前所述，我们将面向对象编程（OOP）的完整讨论推迟到第二部分。

转换后的 `name` 值随后被重新赋值给同一个变量 `name`。这是一个常见的习惯用法，因为一旦完成大写转换，我们就不再需要 `name` 的旧值。

（`name` 的旧值，例如最初从输入读取的值，第 4 行）在此 `if/else` 语句之后，程序不再能够访问它，它可以被“垃圾回收”。关于这一点将在稍后详细讨论。还需要注意的一点是，如上所述，使用“块”的某些语句如 `if/else` 不以分号结尾。）

接下来，使用静态方法 `string.Format()` 创建个性化问候语：

```csharp
var greeting = string.Format("Hello {0}! How are you?", name);
```

这个语句等同于使用插值字符串的以下写法：

```csharp
var greeting = $"Hello {name}! How are you?";
```

`System.String` 的 `Format()` 方法接受一个或多个参数。第一个参数是一个字符串，是一个格式说明符，其中包括 `{0}` 和 `{1}` 等占位符。这些占位符按照从 `{0}` 开始的顺序被随后的参数替换。

在这个例子中，只有一个占位符和一个附加参数。结果将是单个字符串。如果 `name` 是 "JOHN"，那么 `greeting` 将是 "Hello JOHN! How are you?"

有些人喜欢使用 `string.Format()` 进行字符串格式化（例如，而不是使用较新的字符串插值语法）。这真的是一种口味和偏好的问题，但请注意使用字符串格式化的一个缺点。

当我们更新程序时，格式化和参数列表可能会失去同步。人们很容易想象这是如何发生的。而且，*它确实会发生*。使用 `$` 字符串插值对这类潜在错误更具鲁棒性。

然后，`greeting` 的值使用 `WriteLine()` 方法打印到控制台，如前面的 hello world 示例所示，程序终止（因为没有更多要执行的语句）。

`Console.WriteLine()` 的一个有趣之处在于，就接受参数的方式而言，它与 `string.Format()` 方法非常相似。例如，我们可以简单地如下调用 `WriteLine()`：

```csharp
Console.WriteLine("Hello {0}! How are you?", name);
```

而不是像示例代码中那样先调用 `string.Format()`：

```csharp
var greeting = string.Format("Hello {0}! How are you?", name);
Console.WriteLine(greeting);
```

这两个代码段或多或少是等价的。

## 4.3. 代码阅读 - Hello World 4 回顾

最后，让我们看下面的例子：

```csharp
hello-universe-4/Program.cs

class Program {
    static void Main() => Console.WriteLine(
        string.Format("Hello {0}! How are you?", ReadName())
    );

    static string? ReadName() {
        Console.WriteLine("What is your name?");
        var name = Console.ReadLine();

        if (string.IsNullOrEmpty(name)) {
            name = "Friend";
        } else {
            name = name.ToUpper();
        }

        return name;
    }
}
```

这个示例代码在语义上等同于 "hello-world-4"。

> 这个“Hello World”永远没有尽头吗？☺

这是最后一个了。我保证！☺ 但请记住，这并不是关于“hello world”或我们在本书中使用的任何特定示例。我们正在学习 C# 语言及其惯用的现代编程风格。注意，本书开头较慢，但随后会开始以相当快的速度前进。最好系好安全带！☺

### 4.3.1. 解释

该程序的行为与其早期对应版本 hello-world-4 完全相同。该程序像以前一样询问用户的姓名，并使用用户的
