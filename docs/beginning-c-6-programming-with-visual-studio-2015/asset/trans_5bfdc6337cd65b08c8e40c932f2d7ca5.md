

```csharp
string sentence = "his gaze against the sweeping bars has "
    + "grown so weary";
List<string> words;
words = WordProcessor.GetWords(sentence);
WriteLine("Original sentence:");
foreach (string word in words)
{
    Write(word);
    Write(' ');
}
WriteLine("\n");
words = WordProcessor.GetWords(
    sentence,
    reverseWords: true,
    capitalizeWords: true);
WriteLine("Capitalized sentence with reversed words:");
foreach (string word in words)
{
    Write(word);
    Write(' ');
}
ReadKey();
}
```

4. 运行应用程序。结果如图 13-18 所示。

![](img/cf72ea860016d2d680fc085fc06f265a_416_0.png)

图 13-18

## 工作原理

在本示例中，你创建了一个执行简单字符串操作的实用工具类，并使用该类来修改字符串。该类公开的唯一公共方法包含一个必需参数和三个可选参数：

```csharp
public static List<string> GetWords(
    string sentence,
    bool capitalizeWords = false,
    bool reverseOrder = false,
    bool reverseWords = false)
{
    ...
}
```

该方法返回一个字符串值的集合，其中每个值都是原始输入中的一个单词。根据指定了三个可选参数中的哪些（如果有），可以对整个字符串集合或对单个单词值进行额外的转换。

> **注意** 这里不再更深入地探讨 `WordProcessor` 类的功能；你可以随时自行浏览代码。在此过程中，不妨思考一下如何改进这段代码。例如，单词 'twas 是否应该大写为 'Twas？你会如何实施这一更改？

调用此方法时，只使用了可用可选参数中的两个；第三个参数（reverseOrder）将使用其默认值 false：

```csharp
words = WordProcessor.GetWords(
    sentence,
    reverseWords: true,
    capitalizeWords: true);
```

另请注意，所指定的两个参数的放置顺序与它们的定义顺序不同。

最后需要指出的是，在处理带有可选参数的方法时，IntelliSense 会非常方便。在输入此“试一试”练习的代码时，你可能会注意到 `GetWords()` 方法的工具提示，如图 13-19 所示（你也可以如图所示，将鼠标指针悬停在该方法调用上看到此工具提示）。

![](img/cf72ea860016d2d680fc085fc06f265a_417_0.png)

图 13-19

这是一个非常有用的工具提示，因为它不仅显示可用参数的名称，还显示可选参数的默认值，因此你可以一眼看出是否需要覆盖某个特定默认值。

## Lambda 表达式

Lambda 表达式是 C# 3 中引入的一种构造，你可以使用它来简化 C# 编程的某些方面，尤其是与 LINQ 结合使用时。它们一开始可能很难掌握，主要是因为它们的用法非常灵活。Lambda 表达式与其他 C# 语言功能（如匿名方法）结合使用时极其有用。在暂时不考虑 LINQ（这是本书稍后才会讨论的主题）的情况下，匿名方法是研究这一主题的最佳切入点。先快速回顾一下。

### 匿名方法回顾

在本章前面，你已经了解了匿名方法——即以内联方式提供的方法，如果不用匿名方法，则需要一个委托类型变量。当你向事件添加事件处理程序时，事件序列如下：

1. 定义一个事件处理程序方法，其返回类型和参数与你想要订阅的事件所需的委托相匹配。
2. 声明一个用于该事件的委托类型的变量。
3. 将委托变量初始化为该委托类型的一个实例，该实例引用事件处理程序方法。
4. 将该委托变量添加到该事件的订阅者列表中。

实际上，事情比这要简单一些，因为你通常不会费心去用一个变量来存储委托——你在订阅事件时直接使用委托的实例即可。

之前你使用以下代码时就是这种情况：

```csharp
Timer myTimer = new Timer(100);
myTimer.Elapsed += new ElapsedEventHandler(WriteChar);
```

此代码订阅 `Timer` 对象的 `Elapsed` 事件。该事件使用 `ElapsedEventHandler` 委托类型，并通过方法标识符 `WriteChar` 实例化。结果是，当 `Timer` 引发 `Elapsed` 事件时，会调用 `WriteChar()` 方法。传递给 `WriteChar()` 的参数取决于 `ElapsedEventHandler` 委托定义的参数类型，以及 `Timer` 中引发事件的代码所传递的值。

实际上，C# 编译器可以通过方法组语法用更少的代码实现相同的结果：

```csharp
myTimer.Elapsed += WriteChar;
```

C# 编译器知道 `Elapsed` 事件所需的委托类型，因此它可以填补空白。但是，你应谨慎使用这种语法，因为它会使代码更难阅读，也更难确切了解正在发生的事情。当你使用匿名方法时，前面展示的事件序列就缩减为一步：

1. 使用一个内联匿名方法，其返回类型和参数与事件所需委托的返回类型和参数相匹配，即可订阅该事件。

内联匿名方法通过使用 `delegate` 关键字来定义：

```csharp
myTimer.Elapsed +=
    delegate(object source, ElapsedEventArgs e)
    {
        WriteLine("Event handler called after {0} milliseconds.",
            (source as Timer).Interval);
    };
```

这段代码与单独使用事件处理程序的效果一样好。主要区别在于，这里使用的匿名方法实际上对代码的其余部分是不可见的。例如，你不能在应用程序的其他位置重用此事件处理程序。此外，这里使用的语法——找不到更好的描述——有点笨拙。`delegate` 关键字会立刻让人困惑，因为它实际上被重载了——你既可以将它用于匿名方法，也可以用它定义委托类型。

### 用于匿名方法的 Lambda 表达式

这就引出了 Lambda 表达式。Lambda 表达式是简化匿名方法语法的一种方式。事实上，它们的作用不止于此，但本节将暂时从简处理。使用 Lambda 表达式，你可以将上一节末尾的代码重写如下：

```csharp
myTimer.Elapsed += (source, e) => WriteLine("Event handler called after " +
    $"{(source as Timer).Interval} milliseconds.");
```

乍一看，这……嗯，有点令人费解（除非你熟悉所谓的函数式编程语言，如 Lisp 或 Haskell）。然而，如果你仔细看，就能看到，或者至少推断出它是如何工作的，以及它与它所替代的匿名方法之间的关系。Lambda 表达式由三个部分组成：

- 括号内的（未指定类型的）参数列表
- `=>` 运算符
- 一个 C# 语句

参数的类型是根据上下文推断出来的，使用的逻辑与本章前面的“匿名类型”一节中展示的逻辑相同。`=>` 运算符只是将参数列表与表达式主体分隔开来。表达式主体在调用 Lambda 表达式时执行。

![](img/cf72ea860016d2d680fc085fc06f265a_421_0.png)

图 13-20

## 工作原理

此示例使用 Lambda 表达式生成函数，这些函数可用于返回对两个输入参数执行特定处理的结果。然后，这些函数对 25 对值进行操作，并将结果输出到控制台。

你首先要定义一个名为 `TwoIntegerOperationDelegate` 的委托类型，用来表示一个接受两个 `int` 参数并返回 `int` 结果的方法：

```csharp
delegate int TwoIntegerOperationDelegate(int paramA, int paramB);
```

稍后定义 Lambda 表达式时会用到这个委托类型。这些 Lambda 表达式会编译为返回类型和参数类型与该委托类型匹配的方法，你很快就会看到。

接下来，你添加一个名为 `PerformOperations()` 的方法，它接受一个 `TwoIntegerOperationDelegate` 类型的参数：

```csharp
static void PerformOperations(TwoIntegerOperationDelegate del)
{
```

此方法背后的思路是，你可以向它传递一个委托实例（或匿名方法或 Lambda 表达式，因为这些构造会编译为委托实例），然后该方法将使用各种值调用该委托实例所表示的方法：

```csharp
for (int paramAVal = 1; paramAVal <= 5; paramAVal++)
{
  for (int paramBVal = 1; paramBVal <= 5; paramBVal++)
  {
    int delegateCallResult = del(paramAVal, paramBVal);
```

然后将参数和结果输出到控制台：

```csharp
Write($"({paramAVal}, " +
    $"{paramBVal}) = {delegateCallResult}");
if (paramBVal != 5)
{
  Write(", ");
```

