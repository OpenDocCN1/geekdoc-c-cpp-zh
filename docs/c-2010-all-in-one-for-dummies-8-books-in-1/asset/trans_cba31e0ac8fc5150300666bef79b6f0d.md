

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

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_255_0.png)

## 适用于文件的方法示例

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

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_257_0.png)

第1部分调用 `InputData()` 方法按顺序输入程序创建表格所需的三个变量：本金、利息和时长。第2部分显示这三个变量以便核实，正如程序之前的版本所做的那样。第3部分通过 `OutputInterestTable()` 方法输出表格。

底部向上，`OutputInterestTable()` 方法包含一个带有利息计算的输出循环。这个循环与内联的、非方法的 `CalculateInterestTable` 中使用的循环相同。然而，这个版本的优势在于，当你编写这段代码时，你不需要担心输入或验证数据的任何细节。在编写这些内容时，你可以这样想：“给定数字——本金、利息和时长——输出一个利息表”，到此即可。完成后，你可以返回调用 `OutputInterestTable()` 的那行。

![](img/36596fb11aa4233d5cab0d6ddd1d828_1)

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

![](img/36596fb11aa4233d5cab0d6ddd1d828_0)

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

