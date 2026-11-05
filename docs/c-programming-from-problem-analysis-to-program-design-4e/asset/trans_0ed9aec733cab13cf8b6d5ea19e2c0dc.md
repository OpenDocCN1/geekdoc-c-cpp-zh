

![](img/36e48639a06772bcb0fa1ea2525b33a3_88_0.png)

**图 1-22** ProgrammingMessage 示例的原型

在设计过程中，制定算法非常重要。这个问题可以使用流程图来开发算法。该算法应包括一步一步的解决方案；在本例中，解决方案很直接，仅仅涉及输出一串字符。图 1-23 包含一个流程图，定义了 ProgrammingMessage 示例所需的步骤。

![](img/36e48639a06772bcb0fa1ea2525b33a3_88_1.png)

**图 1-23** ProgrammingMessage 示例的算法

另一种选择是使用结构化英语或伪代码来定义算法。这个问题的伪代码会非常简短，只需一行代码即可在输出屏幕上显示消息 Programming can be FUN!。

采用面向对象的方法进行设计时，解决方案通常需要创建类图。对于这个问题，不需要定义任何数据成员。System 命名空间中的 Console 类已经提供了可用于在标准输出设备上显示输出的方法。因此，不需要定义新的方法或行为。所以，如果要构建类图，它只会包含类标题。图的中间或底部部分不会有任何内容。由于该图没有为此简单问题提供额外的文档或设计帮助，因此不绘制该图。

算法制定完成后，应检查设计的正确性。一种方法是模拟计算机，一步一步地执行代码，就像你自己是计算机一样，对算法进行桌面检查。当你逐步执行流程图时，它应该产生原型上出现的输出。在开始编写代码之前，仔细设计并检查算法的正确性非常重要。如果这样做，你将花费更少的时间，也会少很多烦恼。

## 编写解决方案代码

完成设计并验证算法的正确性后，就可以将设计转换为源代码了。你可以使用简单的编辑器（如记事本）在计算机上输入源代码语句，也可以使用 Visual Studio 创建文件。在此步骤中，你必须注意语言的语法规则。

如果使用 Visual Studio 创建应用程序，IDE 会自动为你生成大量代码。其中一些代码可以被删除或忽略。例如，你注意到前面的示例中删除了四个 using 语句（using System.Collections.Generic; using System.Linq; using System.Text; 和 using System.Threading.Tasks;）吗？你可以再次删除或忽略这些子句。对于你将开发的大多数应用程序，using System; 是唯一需要保留在程序语句中的 using 子句。

Visual Studio 还会修改 Main() 方法的方法头，它与本章前面看到的不同。Main() 的签名可以是空参数列表，也可以在括号中包含 string[] args。对于你正在开发的应用程序类型，不需要发送额外参数，因此你此时可以忽略或完全删除 Main() 括号内的参数。

你可能希望更改源代码文件的名称，并让 Visual Studio 更改对该名称的所有引用。当你输入 ProgrammingMessage 作为项目名称时，IDE 会自动将命名空间命名为 ProgrammingMessage。该类也可以命名为 ProgrammingMessage，这不会导致命名空间与类名相同之类的名称冲突问题。图 1-24 说明了你可能希望对 Visual Studio 生成的代码进行的更改。

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace ProgrammingMessage
{
class Program
{
static void Main(string[] args)
{
}
}
}
```

- 可以删除这些 using 语句
- 更改名称
- 可以替换为 static void Main()

**图 1-24** 推荐的删除项

你只需在 Main() 方法体中输入以下几行。

```csharp
Console.WriteLine("Programming can be");
Console.WriteLine("FUN!");
Console.ReadKey();
```

最终程序代码如下所示：

```csharp
/* Programmer: [supply your name]
Date: [supply the current date]
Purpose: This class can be used to send messages
to the output screen.
*/
using System;
namespace ProgrammingMessage
{
class ProgrammingMessage
{
static void Main()
{
Console.WriteLine("Programming can be");
Console.WriteLine("FUN!");
Console.ReadKey();
}
}
}
```

在程序开头，请标明代码的作者，并至少指定项目的用途。注意，Main() 方法中的语句是按顺序执行的。ReadKey() 方法在两个 WriteLine() 方法之后执行。ReadKey() 在程序中用于保持输出屏幕显示，直到用户按下某个键。按下键盘上的某个字符后，控制权将传递到标志着应用程序结束的下一行。

## 实现代码

在实现过程中，源代码会被编译以检查是否违反规则。若要从 Visual Studio IDE 中进行编译，请使用**生成**菜单选项。如果有错误，必须先更正才能继续。在 Visual Studio IDE 中，选择**调试**菜单栏上的**开始执行(不调试)**以查看结果。

## 测试与调试

仅仅因为没有编译器语法错误并且获得了输出，并不意味着结果是正确的。在最后一步中，测试程序并确保获得正确的结果。输出应与你的原型匹配。你的间距正确吗？

按照本章概述的步骤，你正式成为了一名 C# 程序员。你创建的程序很简单。然而，你在本章中学到的概念对你的进步至关重要。在第 2 章中，你将开始处理数据。

## 编码标准

在设计类时遵循编码标准非常重要。这样做将带来更好的解决方案，并减少修改程序语句所需的时间。在最初使用流程图和伪代码设计算法时，也应遵循标准。以下是针对伪代码的一些建议编码标准或指南。

### 伪代码

- 对于算术运算，使用 compute 或 calculate 等动词来暗示需要某种算术。
- 使用 set、reset 或 increment 等词来暗示应执行的操作类型。
- 使用 print 或 display 来指示应在屏幕上显示的内容。
- 将项目分组并添加缩进，以表明它们属于同一组。
- 对于应多次执行的语句，使用 while 或 do while 等关键字来暗示循环。
- 使用 if 或 if/else 来测试内存位置的内容。

制定并始终遵循的标准将提高你的编码效率，并使你的代码更易于维护。

## 资源

互联网上有大量专门介绍 C# 的网站。你可以从以下一个或多个站点开始探索：

- 当前 C# 语言规范 – http://www.microsoft.com/en-us/download/details.aspx?id=7029
- Visual C# Express 下载 – http://www.microsoft.com/visualstudio/en-us/products/2010-editions/visual-csharp-express
- 计算历史项目 – http://www.thocp.net/
- 英特尔处理器信息 – http://www.intel.com
- 帕斯卡计算器 – http://www.thocp.net/hardware/pascaline.htm
- Microsoft .NET 网站 – http://www.microsoft.com/net
- MSDN Visual C# 主页 – http://msdn2.microsoft.com/en-us/vcsharp/default.aspx
- 美国计算机和互联网使用情况普查数据 – http://www.census.gov/cps/
- 维基百科免费百科全书 – http://wikipedia.org
- Mono 跨平台开源 .NET 框架 – http://www.mono-project.com
- Microsoft 开发者网络 – http://msdn.microsoft.com/en-us/

## 快速复习

- 1. 计算机的力量在于软件，软件是赋予硬件功能的一组指令或程序。
- 2. 许多人认为当今的计算机技术属于现代计算的第五代。每个时代都以一项重要进步为特征。
- 3. 如今，对智能设备移动应用程序的需求正在增加。
- 4. 软件可分为两类：系统软件和应用软件。应用软件被定义为为执行特定任务而开发的程序。

