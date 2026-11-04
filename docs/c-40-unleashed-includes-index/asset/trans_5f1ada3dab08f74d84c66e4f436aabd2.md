
```csharp
static string ToDutchBinaryString(int x)
{
    switch (x)
    {
        case 0:
            return "nul";
        case 1:
            return "een";
        default:
            throw new InvalidOperationException("Not a binary digit.");
    }
}
```

switch 指令是表驱动的，基本上为整数值 0、1、2 等指定目标标签。如果 case 标签中出现间隙（例如上面只有 0 和 2），switch 会将缺失的值（也就是 1）的控制权转移到 default 标签。所有不属于“覆盖范围”的值也会直接穿过 switch 指令，控制权同样被转移到 default 标签。

在图 7.9 中，switch 检查参数值 x，如果值等于 0，则将控制权转移到标签 IL_0012；如果等于 1，则转移到 IL_0018。否则，控制流直接穿过，在 default 分支所在的位置 IL_001e 处进行无条件跳转。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_401_0.png)

**图 7.9** switch 标签指定跳转目标。

由于 switch 指令针对其连续的目标标签集合知道值 0、1、2 等，编译器会做一些基本的数学运算来使代码适应这种行为。例如，如果你的 switch 包含值 10 和 11 的 case，编译器会在执行 switch 之前减去 10，然后再次基于 0。这里展示了一个示例，同样在值的范围中留下了一个间隙：

```csharp
switch (x)
{
    case 11:
        return "elf";
    case 13:
        return "dertien";
    default:
        throw new InvalidOperationException("Unexpected value.");
}
```

代码不会对 x 进行 switch，而是对 x - 11 进行 switch。注意这样做是安全的，因为这里使用的减法运算符在编译器看来没有副作用，因为只支持内置的整数类型。11 这个 case 将对应第一个 switch 标签，不存在的 12 的 case 将被修补为跳转到 default，而 13 的 case 将落在其适当的位置。其余的继续向下穿过。图 7.10 说明了这一点，还展示了指令及其操作数的字节。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_402_0.png)

**图 7.10** 更复杂的 switch 逻辑。

如果 switch 中使用的值的范围过于零散，无法归一化为一个大致连续的区间，编译器将转而生成代码，就像编写了常规的多路 if 语句一样。

注意，switch 指令的从零开始特性使其非常适合枚举值，因为（在标准情况下）枚举值包含一个从零开始的值集合。例如，我们的 Color 枚举从 Red 到 Blue 的值为 0 到 2，因为我们没有否决编译器选择的默认值（稍后会详细讨论）。

对于基于字符串的 switch，代码会被视为多路 if 语句，使用 System.String 类型上定义的 `==` 运算符将字符串与提供的值进行比较。这会执行区分大小写的逐字符相等性检查。如果 case 数量增长得太多（目前的阈值是六个或更多，但这一阈值随时可能改变），而且由于顺序对开发人员来说无关紧要，编译器会生成更高效的代码，在内部使用 `Dictionary<string, int>`。这种集合类型使用一种称为哈希的技术来加快查找操作，正如我们在第 16 章“集合类型”中讨论集合时将会看到的那样。

例如：

```csharp
static string DutchDecimalDigitToEnglish(string s)
{
    switch (s)
    {
        case "nul": return "zero";
        case "een": return "one";
        case "twee": return "two";
        // Enough additional cases here.
        default:
            throw new InvalidOperationException("Not a decimal digit.");
    }
}
```

这段代码大致被编译为如下等价形式：

```csharp
static Dictionary<string, int> s_switchHelper; // really a random name

static string DutchDecimalDigitToEnglish(string s)
{
    if (s_switchHelper == null)
        s_switchHelper = new Dictionary<string, int>
            { { "nul", 0 }, { "een", 1 }, { "twee", 2 }, /* more cases */ };

    int __num;
    if (s_switchHelper.TryGetValue(s, out __num))
        switch (__num)
        {
            case 0: return "zero";
            case 1: return "one";
            case 2: return "two";
            default: goto __default;
        }

    __default:
        throw new InvalidOperationException("Not a decimal digit.");
}
```

实际代码为了适应多线程执行会稍显复杂，但其核心思想是将基于字符串的 switch 转换为运行时原生支持的基于 int 的 switch。这种映射基于一个在首次使用时实例化的字典。

但为什么要这么大费周章呢？实际上，我想通过这个特殊的例子传递一个隐含信息：表驱动执行是一种非常有用的技术。显然，你的 case 标签中的嵌入语句可能会复杂得多，做的事情也远不止建立某种映射。但下次你编写 switch 来编码某种映射时，可以考虑使用表来代替。我们的例子可以完全重写如下：

```csharp
static Dictionary<string, string> s_dutchToEnglish;

static string DutchDecimalDigitToEnglish(string s)
{
    if (s_dutchToEnglish == null)
    {
        s_dutchToEnglish = new Dictionary<string, string>
            { { "nul", "zero" }, { "een", "one" }, /* more mappings */ };
    }

    string english;
    if (!s_dutchToEnglish.TryGetValue(s, out english))
        throw new InvalidOperationException("Not a decimal digit.");

    return english;
}
```

### 其他语言速览：SELECT CASE 和 MATCH

虽然本书讲的是 C#，但在 .NET 的世界中，你迟早可能会面对用其他语言编写的代码。所以我想指出其他语言中与 switch 大致对应的特性。

Visual Basic 有 Select Case，它可以用于我们在 C# 中使用 switch 所做的事情，但还能做更多，比如范围检查（Case 1 to 10）和不等式检查（Case > 1）。

F# 有一种匹配（matching）结构，其功能远超 C# 的 switch 和 Visual Basic 的 Select Case。它支持对元组、列表、可区分联合（discriminated unions）和类型进行完整的模式匹配。这里展示了一个定义函数来计算形状表面积的示例：

这里我们使用一个局部变量从 1 数到 10，并在每次循环迭代时向屏幕打印一定数量的星号。这里使用块语法使循环体包含两条语句，不过我建议即使循环体只有一条语句也使用花括号。熟悉后置递增运算符的读者——现在应该每个人都熟悉了——会注意到这段代码可以缩写如下：

```csharp
int i = 1;
while (i <= 10)
    Console.WriteLine(new string('*', i++));
```

确实，它更短了，但可读性并不更好。请避免在生产代码中这样写。接下来，如果有人过来给循环体添加一条 if 语句，导致 i 的递增变得有条件，那么循环很可能会进入一种状态：i 不再递增，条件永远无法为 false——变成一个失控循环！

有时编写无限循环是有意义的（例如，创建一个作为服务驱动程序的消息处理器）。它的任务是接收消息并将它们分派给某个执行实际处理的工作者。如果你有时看到这样的代码，不要感到惊讶：

```csharp
while (true)
{
    // Do something.
}
```

你接下来的逻辑问题应该是这个循环如何终止。这本身是一个话题，并且高度依赖于上下文。有时会使用异常来实现这一目的，有时会设置一个布尔标志（但可能不会立即产生效果，因为循环可能在等待消息进入时被阻塞），但还有其他技术存在。既然说到这里，这正是讨论如何修改循环迭代行为的最佳位置。

### break

break 语句可用于跳出循环。它将控制权转移到紧跟在循环之后的语句。例如：

```csharp
var rand = new Random();
while (true)
{
    var num = rand.Next();
    if (num % 2 == 0)
        break;
    Console.WriteLine(num);
}
```
