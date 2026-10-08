
```csharp
class InputPointsWithWhile
{
    static void Main()
    {
        int sum = 0;
        int startValue;
        int endValue;
        string keyValue;
        Console.Write("Enter the beginning value. ");
        string inValue = Console.ReadLine();
        startValue = Convert.ToInt32(inValue);
        Console.Write("Enter the last value. ");
        inValue = Console.ReadLine();
        endValue = Convert.ToInt32(inValue);
        Console.Write("Sum of values {0} through {1} ",
            startValue, endValue);
        while (startValue < endValue + 1)
        {
            sum = sum + startValue;
            startValue++;
        }
        Console.WriteLine("is {0}", sum);
    }
}
```

示例 6-2 有一些需要考虑的问题。条件表达式现在是：

```csharp
while (startValue < endValue + 1)
```

# 使用 While 语句

使用 `while (startValue <= endValue)` 也可以达到相同的结果。注意，用户输入的最后一个数字应该加到总和中。如果条件是 `while(startValue < endValue)`，循环将不会执行最后一个值。这是一个常见的差一错误（off-by-one error）。这与计数控制循环有关。重要的是要测试边界情况，以确保它们被考虑在内。你应该始终检查循环控制变量的初始值和最终值，以确保获得预期的结果。如果没有在边界使用复合运算符，结果将是不正确的。

为什么在循环执行前打印 `startValue` 和 `endValue` 的范围值？以下语句出现在循环之前：

```csharp
Console.Write("Sum of values {0} through {1} ", startValue, endValue);
```

变量 `startValue` 在循环内部改变。因此，在完成所有计算后打印结果是更好的。

在示例 6-2 中，当用户输入比 `endValue` 大的值时会发生什么？如果你回答循环体一次都不会执行，那么你是正确的。因为条件表达式求值为假，循环体被跳过。

### 哨兵控制循环

虽然你提前不知道循环应该执行多少次，但这是计数控制循环的要求。另一种选择是哨兵控制循环。哨兵控制循环通常在不知道确确切数量时用于输入。如果你的程序输入多个分数，你可能会显示一条消息，让用户输入一个负值表示他们已结束。你不会有负分；因此，这是一个合适的哨兵值。

哨兵控制循环也被称为无限循环，因为在循环执行之前不知道重复次数。要设计无限循环，请选择一个哨兵值用于表达式。哨兵值是一个极端值、一个虚拟值。它是一个不应该被处理的值——例如在处理正分时的负值。

哨兵值被用作无限循环条件表达式中的操作数。哨兵控制循环带来的优势是不需要知道循环将执行多少次。当所有数据完成后，哨兵值应该指示循环正常终止。示例 6-3 展示了如何使用哨兵控制循环来输入任意数量的数据值。

### 示例 6-3

```csharp
/ InputValuesLoop.cs Author: Doyle
* 演示了输入数值的循环。
*/
using System;
namespace InputValuesLoop
{
    class InputValuesLoop
    {
        static void Main()
        {
            string inValue = ""; // 初始化为 null
            Console.Write("此程序将允许你输入");
            Console.Write("值一个值。要停止，请输入");
            Console.WriteLine(" -99");
        }
    }
}
```

```csharp
while (inValue!="-99"){
    Console.WriteLine("Enter value (-99 to exit)");
    inValue = Console.ReadLine();
}
```

在使用计数控制循环时，必须在示例 6-3 中设置条件表达式。这必须在循环执行之前完成。这一次，用于存储输入值的变量 `inValue` 被初始化为空字符串(`""`)；双引号之间没有放置任何值。变量 `inValue` 可以初始化为除 -99 以外的任何值。但是，它必须被初始化。

C# 不允许你使用未赋值的值。如果你没有初始化 `inValue`，当你尝试在条件表达式中使用 `inValue` 时，将收到错误消息“Use of unassigned local variable inValue”（使用了未赋值的局部变量 inValue）。

在示例 6-3 中，只要用户不输入 -99，条件表达式就会继续评估为真。注意输入语句是如何放置在循环体的最后语句的。这种位置至关重要。如果计算是循环体的一部分，则必须在循环外部进行“预读”（prime the read）。这意味着你会在进入循环体之前先输入一个值。这样做允许循环中的第一个语句成为处理该值的语句。然后，作为循环的最后一个语句，包含了另一个 `ReadLine()` 方法。如果你不将 `ReadLine()` 放在结尾作为最后一个语句，你最终会处理哨兵值（sentinel value）。一旦用户输入 -99 或哨兵值，你就希望停止处理数据。将 `ReadLine()` 放置在体内的最后一行可以使得条件表达式在输入 -99 后立即评估为假。示例 6-4 通过累加输入的值阐明了这一重要点。

### 示例 6-4

```csharp
/* PrimeRead.cs
Author: Doyle
* 哨兵循环用于数值求和
*/
using System;
namespace PrimeRead
{
    class PrimeRead
{
        static void Main()
        {
            string inValue = ""; //Initialized to null
            int sum = 0;
            int intValue;
            Console.Write("This program will let you enter");
            Console.Write(" value after value. To Stop, enter");
        Console.WriteLine("-99");
            Console.WriteLine("Enter value (-99 to exit)");
            inValue = Console.ReadLine(); // Priming read loop
            while (inValue != "-99")
            {
                intValue = Convert.ToInt32(inValue);
                sum += intValue;
                Console.WriteLine("Enter value(-99 to exit)");
                inValue = Console.ReadLine();
            }
            Console.WriteLine("Total values entered {0}", sum);
        }
    }
}
```

假设输入为：
10
12
40
5
1
99

使用上述输入，该代码的输出为：
Total values entered 68

当你实现哨兵控制循环时，务必告诉用户要输入什么值来结束循环。应该将此信息包含在循环体内部。这在输入大量值时尤为真实。你不希望用户必须去猜或记住如何终止程序。

> 注意：为了告诉用户要输入什么值来终止，你需要在调用 `ReadLine()` 之前使用 `Write()` 或 `WriteLine()` 方法显示消息。否则，他们如何知道输入什么值来停止呢？

在第 11 章中，你将学习如何处理批量并存储在存储介质（如你的文件硬盘）上的数据。哨兵控制循环适用于处理存储在文件中循环。哨兵值被放置在文件的最后一个条目。在这里，必须显示一条指示如何停止的消息。循环条件表达式与用于交互式输入数据使用的完全相同。条件表达式与选定的哨兵值匹配。

### 应用程序中使用循环

如今的许多 C# 应用程序创建具有图形用户界面（GUI）的 Windows 应用程序。到目前为止，你显示的输出都是控制台窗口，而不是 Windows 表单或网页。这些编程概念适用于任何类型的应用程序；但正如你将在后续章节中学到的，Windows 使用的是事件驱动模型。事件驱动模型通过处理事件管理用户与 GUI 之间的交互。将输出发送到控制台让你专注于界面设计之前学习编程基础。

C# 有一个名为 `MessageBox` 的定义类，可以通过它的 `Show()` 方法成员向用户显示信息。`MessageBox.Show()` 生成的输出更你熟悉的窗口。在本书的后续章节中，所有应用程序都是围绕窗口构建的。以下示例产生了一个显示 1 到 10 及其平方的表格。结果显示在对话框中，而不是控制台中。

当你不想看到控制台命令行窗口时，你需要指示输出类型为 Windows 应用程序。通过在解决方案资源管理器中选择项目，然后从项目菜单中选择该项目的属性来实现这一点。从下拉列表中选择 Windows Application 作为输出类型。你也可以右键点击解决方案资源管理器中的项目名称。属性显示为选项之一。当你选中项目时，Alt+Enter 快捷键也会显示此对话框。

### 示例 6-5

```csharp
/* SquaredValues.cs
Author: Doyle
* 显示 1 到 10 的值及其平方
*/
using System;
using System.Forms;
namespace SquaredValues
{
    class SquaredValues
    {
        static void Main()
        {
            int counter = 0;
            string result = "";
            while (counter < 10)
            {
                counter++;
                result += Math.Pow(counter, 2) + "\n";
            }
            MessageBox.Show(result, "Squared Values");
        }
    }
}
```

图 6-3 显示了该程序的输出。该图包含文本、标题栏说明、特殊按钮和图标。消息框通常用于显示短消息，但也可以通过允许用户从按钮中进行选择的形式接受输入。使用你的选择语句，你可以编写一个表达式来确定点击了哪个按钮。

# 使用 While 语句

在后面的章节中，你将学习如何为包含大量输入的内容创建表单。你的表单将包含文本框、标签、列表框、组合框、单选按钮以及许多其他类型的控件。例如，MessageBox 将输入限制为对话框类型的控件。

`MessageBox` 类的 `Show( )` 方法是重载的。在最简单的情况下，会在对话框窗口上显示一个字符串。示例 6-5 中对 `MessageBox.Show( )` 方法的调用包含两个参数如下：
`MessageBox.Show(result, "1 - 10 and squares");`

第一个参数 `result` 是显示在窗口中的字符串。该变量从循环体内部获取值。每通过一次循环体，文本都会在 `result` 的末尾进行拼接。每次循环都会将一个制表符作为第一个字符拼接（添加 `'\t'` 和 `'\n'` 以留间距）。每次循环都会将一个换行符（回车键）作为最后一个字符拼接。在所有值都放入 `result` 之后，调用 `Show( )` 方法时，其内容将显示在窗口中。由于标题和制表符、换行的存在，内容将以表格的形式出现。

第二个参数 `"1 - 10 and their squares"` 作为标题栏窗口的标题放置，如图 6-3 所示。如之前所述，`Show( )` 是重载的；你可以包含一个按钮作为第三个参数。表 6-1 列出了可以作为 `Show( )` 方法参数的按钮有效选项。

表 6-1 对话框按钮参数

| MessageBox 按钮 | 内容描述 |
|---|---|
| MessageBoxButtons.AbortRetryIgnore | 终止、重试和忽略按钮 |
| MessageBoxButtons.OK | OK 按钮 [默认] |
| MessageBoxButtons.OKCancel | OK 和取消按钮 |
| MessageBoxButtons.RetryCancel | 重试和取消按钮 |
| MessageBoxButtons.YesNo | 是和否按钮 |
| MessageBoxButtons.YesNoCancel | 是、否和取消按钮 |

![](img/45e6f245af31396d967c3186f196d331_340_0.png)

在 Visual Studio 中使用 IntelliSense，你可以看到表 6-1 中所示的属性值，以及 MessageBox 中可以包含的不同图标选项。

你可以如下添加一个按钮作为第三个参数：
`MessageBox.Show(result, "1 - 10 and their " + "squares", MessageBoxButtons.YesNoCancel);`

MessageBox 对话框上包含了“是”、“否”和“取消”的按钮。

当你查看图 6-3 时，请注意输出的最后一行值 10。然而，条件表达式表明只要计数器小于 10，循环就会执行。当计数器变为 10 时，循环终止。那么为什么 10 及其平方会被打印出来呢？另外，请注意变量 `counter` 初始化为 0，但图 6-3 中显示的第一行对应的值是 1。示例 6-6 中再次包含了该循环，以便你仔细检查。

### 示例 6-6

```
while (counter < 10)
{
  counter++;
  result += " \t" + counter + " \t" + Math.Pow(counter, 2) + "\n";
}
```

注意计数器在何时递增以及何时发生拼接。由于计数器在第一条语句中递增为 1，因此 0 从未被拼接。当 `counter` 等于 9 时（9 < 10），条件表达式求值为真。因为在循环内部拼接之前，计数器已经递增到了 10，所以打印了 10 的值。你应该仔细注意循环计数器变量的更新位置，以及你编写的用于允许正常终止的条件表达式。

`MessageBox` 是一个对话框。如你所知，对话是两个或多个个人之间的交流，因此用于用户交互。当包含 `MessageBox.Show( )` 方法的代码行执行时，处理将停止，直到用户点击 MessageBox 上的 OK 按钮做出响应。该方法调用放置在示例 6-5 的循环外部。如果放置在循环内部，则每执行一次 `MessageBox.Show( )` 调用都需要用户点击一次。如果将该方法包含在循环体内部，用户将需要点击 10 次 OK。这就是为什么循环体内部产生的值被拼接到字符串变量上。程序只包含了一次 `MessageBox.Show( )` 方法调用，且位于循环体外部。

``MessageBox.Show( )` 的重载方法可以发送表 6-1 中的一种按钮类型以及第四个参数图标，如示例 6-7 所示。

### 示例 6-7

```
MessageBox.Show(result, "1 - 10 and their " + "squares", MessageBoxButtons.YesNoCancel, MessageBoxIcon.Information);
```
