
`example.staticInt = 2;` // 通过类初始化类方法。

以下代码段以几乎相同的方式定义并访问 `InstanceMethod()` 和 `ClassMethod()`：

```csharp
Example example = new Example(); // 创建一个实例。
example.InstanceMethod(); // 调用实例方法。
ClassMethod(); // 通过类调用方法。
```

以下几行无法编译：

`example.ClassMethod();` // 无法通过实例访问类方法。

`example.InstanceMethod();` // 无法通过类访问实例方法。

类的每个实例都有自己的实例方法副本。但同一类的所有实例具有相同的类成员——包括数据成员和方法——以及它们的值

`InstanceMethod()` 将控制权传递给 `ClassMethod()`。执行最后所示的代码生成输出：

```
this is an instance
this is a class method
```

在方法完成后，控制权返回到调用处。通过阅读 C# 代码的注释，你应该能够对程序的意图有一个良好的理解。如果不能，说明你注释得不当。相反，如果你无法剥离注释并通过方法和变量名来理解意图，说明你的方法命名不够清晰，或者方法分得不够小（或者两者兼有）。

# TIP

在描述方法时我会加上括号——例如 `InstanceMethod()`，以便它们更容易识别。否则，你可能会在理解我在说什么时感到困惑。

### 一个供你的方法示例

在本节中，我将第一卷第 5 章的 `CalculateInterestTable` 拆分为几个合理的方法；演示了正确的定义定义如何有助于编写和理解程序。

# REMEMBER

我将在章的后续章节详细解释方法定义和调用的细节。这个示例仅提供了一个概述。

## 230 适用于文件的方法示例

- ◆ 一个输入部分，用户在其中输入本金、利息和时长信息
- ◆ 一个镜像输入数据的部分，以便用户核实输入的数据是否正确
- ◆ 一个创建并输出表格的部分

使用此列表开始寻找重构程序的方法。事实上，如果你进一步检查该程序的输入部分，你会发现输入这些金额时使用了完全相同的基础代码：

- ◆ 本金
- ◆ 利息
- ◆ 时长

你的观察为你提供了另一个很好的切入点。或者，你也可以先为这些注释中的部分编写方法，然后一个一个地填充它们。这就是“意图编程”。

我使用了规划方法的技术创建了以下版本的 `CalculateInterestTableWithMethods` 程序：

```csharp
// CalculateInterestTableWithMethods -- 生成一个利息表
// 类似于其他利息表程序
```

### 适用于文件的方法示例

```csharp
// 1a -- 获取本金。
principal = InputPositiveDecimal("principal");
// 1b -- 输入利率。
interest = InputPositiveDecimal("interest");
// 1c - 最后是时长
duration = InputPositiveDecimal("duration");

// InputPositiveDecimal -- 从键盘返回一个正的小数。
public static decimal InputPositiveDecimal(string prompt)
{
    // 不断尝试，直到用户输入正确。
    while (true)
    {
        // 提示用户输入。
        Console.WriteLine("Enter * " + prompt + ":");
        // 从键盘获取值。
        string input = Console.ReadLine();
        decimal value = Convert.ToDecimal(input);
        // 如果输入的值正确，则退出循环。
        if (value >= 0)
        {
            // 返回用户输入的小数值。
            return value;
        }
        // 否则，针对错误的输入生成错误。
        Console.WriteLine(prompt + " * cannot be negative");
        Console.WriteLine("Try again");
        Console.WriteLine();
    }
}

// OutputTable -- 给定本金和利息，
// 根据 duration 指定的期数生成未来价值表。（实现第3部分）。
public static void OutputTable(decimal principal, decimal interest, decimal duration)
{
    for (int year = 1; year < duration; year++)
    {
        // 计算本金加利息的值。
        decimal interestPaid;
        interestPaid = principal * (interest / 100);
        // 现在通过将利息加上之前的本金来计算新的本金。
        principal = principal + interestPaid;
        // 将本金四舍五入到最接近的分。
        principal = decimal.Round(principal, 2);
        // 输出结果。
        Console.WriteLine(year + " *=" + principal);
    }
}
```

我将 `Main()` 方法分为三个明显不同的部分，每个部分都用粗体注释进行了标记。我进一步将第一部分划分为标记为 1a、1b 和 1c 的子部分。

## 232 适用于文件的方法示例

通常，你不需要包含粗体注释。如果你这样做了，由于所有的数字和字母，列表将变得相当复杂。在实践中，如果方法设计得很周全，并且名称清晰地表达了每个方法的意图，那么这些类型的注释是不必要的。

第1部分调用 `InputData()` 方法按顺序输入程序创建表格所需的三个变量：本金、利息和时长。第2部分显示这三个变量以便核实，正如程序之前的版本所做的那样。第3部分通过 `OutputInterestTable()` 方法输出表格。

底部向上，`OutputInterestTable()` 方法包含一个带有利息计算的输出循环。这个循环与内联的、非方法的 `CalculateInterestTable` 中使用的循环相同。然而，这个版本的优势在于，当你编写这段代码时，你不需要担心输入或验证数据的任何细节。在编写这些内容时，你可以这样想：“给定数字——本金、利息和时长——输出一个利息表”，到此即可。完成后，你可以返回调用 `OutputInterestTable()` 的那行。

`OutputInterestTable()` 为尝试 Visual Studio 的重构（Refactor）菜单提供了目标。采取以下步骤尝试一下：

1. 以第一本书中的 `CalculateInterestTable` 示例为起点，选择从 `year` 变量声明到 `while` 循环结束的代码：

```csharp
int year = 0;
while(year <= duration)
{
    // 你抓取循环
    // 以及整个 while 循环。
    ...
}
```

2. 选择重构（Refactor）：提取方法（Extract Method）。

3. 在 Extract 对话框中输入 `OutputTable`。检查预览签名。注意建议的新方法签名以 `private static` 开始，并包含 principal、interest 和 duration。（我目前引入了 `private`，它是 `public` 的替代方案，如果你喜欢，可以在重构后将方法改为 `public`。）

```csharp
private static decimal OutputTable(decimal principal, decimal interest, int duration)
```

4. 点击 OK 然后点击 Apply 以完成提取方法重构。第1步中选择的代码被移动到一个新方法，位于 `Main()` 下方并命名为 `OutputTable()`。在原来的位置，你看到了这个方法调用：

```csharp
principal = OutputTable(principal, interest, duration);
```

预览显示了两个窗格，你可以精确预览哪些信息将发生变化。顶部窗格显示你正在修复的当前代码。下方窗格显示代码后的样子。对于重构，每个窗格都有许多行。你可以单独选择或取消选择它们以确定要重构的特定元素。

如果你感到“买后懊悔”，点击 Undo 或 Ctrl+Z。假设之前的重构做了一些你喜欢的事情，例如没有将本金作为参数。（因为这种情况是有可能的，你必须始终检查重构以确保它是你想要的。）事实上，这种情况在第一次编写这一部分时确实发生过。（我正在写的这一章关于软件的。）提取方法重构并没有让本金变成参数，而是变成了一个变量。要将本金移动到参数列表中，你可以使用“变量提升为参数”（Promote Variable to Parameter）重构。但在此之前，你需要初始化变量（如果变量未初始化，提升重构将不起作用）：

```csharp
decimal principal = 0;
```

执行“变量提升为参数”重构，右键点击本地 `principal` 名称并点击“Promote Variable to Parameter”将变量定义移动到参数列表：

```csharp
private static decimal OutputInterestTable(decimal interest, int duration, decimal principal)
```

然而，本金在列表末尾，而你希望它在开头。你可以使用“重新排序参数”（Reorder Parameters）重构来解决这个问题。要执行重新排序参数，右键点击新的 principal 参数并点击 Reorder Parameters 链接。在对话框中，点击 principal 行以选择它。然后双击两次 ↑ 将 principal 移动到列表顶端。点击 OK。

## 234 适用于文件的方法示例

### 为什么你应该花心方法

当 FORTRAN 引入函数概念时——C# 在 50 年代的方法，其目的是通过将相似的部分合并到公共元素中避免代码重复。假设你要编写一个在多个处计算比例的程序。你的程序可以使用需要的 `CalculateRatio()` 方法，仅仅是为了避免重复。对于 `calculateRatio()` 这样的方法来说，这种节省并不重要，但像 `WriteLine()` 这样的方法可能会被调用数百次。

这个作业可以实现这种复杂操作而无需担心它是如何执行的。应用程序程序员可以使用 `CalculateSin()` 而无需担心内部如何执行，这大大减少了她必须监控的问题。在减少了“变量”数量后，任务通过实现两个小任务完成了。

大型程序（如文字处理器）是由许多层次的方法构建的。例如，`DisplayDocument()` 方法无疑会调用 `DisplayParagraph()` 方法来显示段落。`Paragraph()` 需要调用 `CalculateWordWrap()` 方法来决定组成段落的行。`CalculateWordWrap()` 必须调用 `LookupWordBreak()` 方法来决定在行尾处断开单词，使句子自然换行。这些方法中的每一个都可以用一句话描述。（注意方法命名很好）。很快，第二个优势变得显而易见：编写一个简单的方法和编写许多方法一样容易——如果方法很小，则会加倍容易。

# 你的文件示例方法 235

太棒了！`InputInterestData()` 同样适用于相同的分治逻辑。然而，那种类型的重构更为复杂，所以我手动完成了它，没有显示具体步骤。虽然对重构完整艺术的的描述超出了本书的范畴，但你可以在 csharp102.info 找到介绍。尝试一下“重构（Refactor）”菜单，并经常使用它来构建结构更好的代码。但务必始终检查结果。

由于 C# 4.0 支持命名参数，你可以在调用方法时，通过在值之前指定预期参数的名称，以你想要的任何顺序调用参数。我将在第 8 节中详细介绍这个主题，但在 C# 4.0 中，重新排列参数顺序不再是一个问题。

对于 `InterestData()`，你可以完全专注于输入三个小数值。然而，在这种情况下，你会发现输入每个值都涉及对三个不同变量执行相同的操作。`InputPositiveDecimal()` 方法将这些封装成一组通用代码，你可以将其应用于本金、利令和期限。注意，原始程序中输入的三个 `while` 循环被合并为 `InputPositiveDecimal()` 内部的一个 `while` 循环。这减少了代码重复。

避免代码重复。重构将其称为最糟糕的“代码气味”。

你的 `InputPositiveDecimal()` 方法显示它接收到的值并等待用户输入。如果该值不是负数，方法将该值返回给调用者。如果值为负数，方法将输出错误消息并循环重试。

从用户的角度来看，修改后的程序与内联版本完全相同，这正是重点所在：

```
Enter principal:100
Enter interest:-10
interest cannot be negative
Try again
```

```
Enter interest:10
Enter duration:10
```

```
Principal = 100
Interest = 10%
Duration = 10 years
```

```
1-110.00
2-121.00
3-133.10
4-146.41
5-161.05
6-177.16
7-194.88
8-214.37
9-235.81
10-259.39
Press Enter to terminate..
```

| 第二卷 |
| 第 3 章 |
| 方法 | 我们拥有 |

我将一个冗长的——有些困难的程序重构成了更小、更易于理解的部分，同时减少了一些重复。正如我那儿的人常说的，“你用木棍是打不赢它的。”

### 为方法传递参数

像下面示例这样的方法其实用性和 Bill Sempf 的发刷没什么两样，因为没有数据传入或传出该方法：

```csharp
public static void Output() {
    Console.WriteLine("this is a method");
}
```

将此示例与执行操作的现实方法进行比较。例如，数学正弦运算需要某种类型的输入——之后，你必须计算某个东西的大小。同样，为了拼接两个字符串，`Concatenate` 方法至少需要两个字符串作为输入。（正如 Beau 可能会说的，“嘿，Wally，这听起来很有逻辑。”）你需要找到一种方法让数据进入和传出方法。

### 向方法传递参数

你输入到方法的值是方法参数（arguments）或形式（parameters）。如果方法要执行某些操作，通常需要某些参数。（这种情况下，方法让我想起了我儿子：在他做任何事情之前，我们需要争论一下。）你通过在方法名后的括号中列出参数向方法传递参数。考虑对之前的 `Example` 类进行此小改进：

```csharp
public class Example {
    public static void Output(string someString) {
        Console.WriteLine("Output was passed the argument: " + someString);
    }
}
```

我可以从同一个类中这样调用这个方法：

```csharp
Output("Hello");
```

然后我将看到这个看起来不那么有趣的输出：

```
Output("Hello")
```

程序向方法 `Output()` 传递了字符串 "Hello" 的引用。方法接收该引用并将其命名为 `someString`。`Output()` 可以在方法内部使用 `someString`，就像使用任何其他字符串变量一样。

我可以以微小的方式修改示例：

```csharp
string myString = "Hello";
Output(myString);
```
