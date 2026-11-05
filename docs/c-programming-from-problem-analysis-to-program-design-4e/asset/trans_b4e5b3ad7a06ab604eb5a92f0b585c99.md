
The focus is on writing *需要做什么*。图 2-18 显示了 CarpetCalculator 示例的结构化英语设计。

![](img/36e48639a06772bcb0fa1ea2525b33a3_154_0.png)

**图 2-18** CarpetCalculator 示例的结构化英语

结构化英语是与面向对象方法一起使用的较为常见的工具之一，用于记录过程逻辑。决策树和表格有时会与结构化英语结合使用，尤其是在解决方案需要作为解决方案的一部分开发多条替代路径时。第 5 章将向您介绍这些工具。

面向对象方法关注我们世界中存在的对象（人、地点和事物）。类图有助于设计和记录对象的数据项和行为。图 2-19 显示了 CarpetCalculator 示例的类图。

![](img/36e48639a06772bcb0fa1ea2525b33a3_154_1.png)

**图 2-19** CarpetCalculator 示例的类图

图 2-19 包含方法。在本章中，您学习了数据项。类图中的中间部分包含标识符及其数据类型。方法包含在类图的底部部分。**方法**是用于在 C# 中实现对象行为的程序。在第 3 章中，您将学习如何编写方法。图 2-20 显示了一个没有方法的类图解决方案。目前应用程序的设计方式将是这样。请注意，图 2-20 包含三个额外的数据成员且没有方法。

![](img/36e48639a06772bcb0fa1ea2525b33a3_155_0.png)

**图 2-20** 没有方法的修订类图

在算法开发完成后，应检查设计的正确性。当您对算法进行桌面检查时，使用计算器并写下您得到的结果。在您实现设计后，可以将程序获得的结果与计算器的结果进行比较。

在这一点上，似乎使用计算器直接进行计算会更容易。请记住，当您编写可用于许多不同数据集的一组指令时，计算机的强大功能就会发挥作用。在下一章中，您将学习如何调用方法以允许交互式输入数据，例如地毯价格和房间尺寸。这将为您的程序增加更多功能。

## 编写解决方案

在您完成设计并验证算法的正确性后，就该将设计翻译成源代码了。如果您正在 Visual Studio 中创建应用程序，您可能需要回看图 1-26 以查看建议的更改。它们包括以下内容：

- 启动 Visual Studio 后，在菜单栏上单击 **文件**，单击 **新建项目**。在 **新建项目** 窗口中，选择 **Visual C#**；在中间窗口中，选择 **控制台应用程序**。输入适当的名称，例如 `CarpetExample`。
- 您可以删除 `using System.Collections.Generic; using System.Linq;` 和 `using System.Text;` 语句。这些命名空间对此应用程序不需要。
- 修改 `Main()` 方法的签名。您可以从括号内删除“string[] args”。
- 将 `.cs` 文件名从 `Program.cs` 更改为更能代表应用程序操作的名称，例如 `CarpetCalculator.cs`。当被问及是否“希望在此项目中重命名代码元素 Program 的所有引用”时，回答“是”。

最终的程序列表如下所示：

```csharp
/* CarpetCalculator.cs Author: Doyle
* Calculates the total cost of carpet, given
* room dimensions in feet and inches and carpet
* price in price per square yard.
*/
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
namespace CarpetExample
{
    class CarpetCalculator
    {
        static void Main()
        {
            const int SQ_FT_PER_SQ_YARD = 9;
            const int INCHES_PER_FOOT = 12;
            const string BEST_CARPET = "Berber";
            const string ECONOMY_CARPET = "Pile";

            int roomLengthFeet = 12,
                roomLengthInches = 2,
                roomWidthFeet = 14,
                roomWidthInches = 7;

            double roomLength,
                   roomWidth,
                   carpetPrice,
                   numOfSquareFeet,
                   numOfSquareYards,
                   totalCost;

            roomLength = roomLengthFeet +
                (double)roomLengthInches / INCHES_PER_FOOT;
            roomWidth = roomWidthFeet +
                (double)roomWidthInches / INCHES_PER_FOOT;
            numOfSquareFeet = roomLength * roomWidth;
            numOfSquareYards = numOfSquareFeet /
                SQ_FT_PER_SQ_YARD;
            carpetPrice = 27.95;
            totalCost = numOfSquareYards * carpetPrice;
            Console.WriteLine("The cost of " +
                BEST_CARPET +
                " is {0:C}", totalCost);
            Console.WriteLine();
            carpetPrice = 15.95;
            totalCost = numOfSquareYards * carpetPrice;
            Console.WriteLine("The cost of " +
                ECONOMY_CARPET +
                " is " + "{0:C}",
                totalCost);

            Console.ReadKey();
        }
    }
}
```

> **注意** 可读性很重要。请注意，第二行语句如何缩进以表示该语句尚未完成。

## 实现代码

在实现期间，源代码会被编译以检查是否违反了任何规则。如果您使用的是 Visual Studio，请从 **生成** 菜单中单击 **生成解决方案** 以编译项目。要运行应用程序，请使用 **调试** 菜单上提供的 **不使用调试启动** 选项。

## 测试和调试

在此最后一步，测试程序并确保您得到正确的结果。输出应与您的原型相匹配。您的间距正确吗？图 2-21 显示了从显示计算结果中生成的输出。

![](img/36e48639a06772bcb0fa1ea2525b33a3_157_0.png)

**图 2-21** CarpetCalculator 程序的输出

总之，本章集中讨论了使用数据。在软件开发的剩余部分中，您将使用本章学到的概念。在第 3 章中，您将学习如何编写描述数据行为的方法。

## 编码标准

正如您在第 1 章中所读到的，编码或编程风格是一个术语，用于描述编写源代码的可接受约定。它超出了语言的规则，并提供了指导方针或建议，应遵循这些指导方针以确保朝着共同目标工作的程序员之间的一致性。遵循这些指导方针可以减少编程项目中引入的错误或 bug 的数量。它节省时间，提高程序的可维护性，并有助于确保代码的可靠性。命名约定在本章前面讨论过，下面将重点介绍。

### 命名约定

- 使用有意义、描述性的词语作为标识符。
- 除非是众所周知的缩写，否则不要为标识符使用缩写。
- 除用作循环迭代器的变量外，不要使用单字符标识符。
- 对以下内容使用 Pascal 大小写（所有单词的首字母大写；其他字符小写）：
  - 类和类型标识符
  - 方法名称
  - 命名空间标识符
  - 属性名称
- 对以下内容使用 Camel 大小写（除第一个单词外，所有单词的首字母大写；其他字符小写）：
  - 局部变量标识符
  - 对象标识符
  - 私有数据成员
  - 参数
- 文件名应与类名匹配。
- 使用全部大写字符命名常量。
- 不要在标识符中使用下划线。
- 使用名词或名词短语命名类。

### 间距约定

- 使用制表符而不是空格进行缩进。
- 使用空白（一个空行）分隔和组织代码的逻辑组。
- 将花括号 { } 放在与括号外代码相同的级别。
