
如果表达式的计算结果为 true，则执行一组给定的语句。但是，如果表达式的计算结果为 false，则执行另一组给定的语句。

在 C# 中，有两个选择语句，如下所示：

- if 语句
- switch 语句

下面我们来逐一讨论这些语句的用法。

## 使用 if 语句

假设有这样的一种情况：您希望根据条件（比如一个数字是偶数还是奇数）来执行一组给定的语句。在这种情况下，可以使用 if 语句以编程方式决定应执行哪一组给定的语句。if 语句允许您根据计算结果为 true 或 false 的布尔表达式的值，从两组给定的语句中选择一组语句执行。执行 if 语句时，会对表达式求值。如果表达式的计算结果为 true，则执行一组给定的语句；如果表达式的计算结果为 false，则执行另一组语句。

if 语句的语法如下：

```csharp
if(expression)
{
    //statements1
}
else
{
    //statements2
}
```

在上述语法中，

- **if：** 指用于表示 if 语句的 if 关键字。
- **expression：** 指作为 if 语句条件的布尔表达式。
- **{}：** 指一对花括号，当您希望在 if 语句中执行一组语句时需要使用花括号。一组语句是指被视为单个语句的多条语句的集合。
- **statement1：** 指当表达式计算结果为 true 时要执行的语句组。该语句组可以是单个语句，也可以是一个语句块。
- **else：** 指用于表示 if 语句的 else 子句的 else 关键字。if 语句的 else 子句是可选的。if 语句中只能有一个 else 子句。
- **statement2：** 指当表达式计算结果为 false 时要执行的语句组。该语句组也是可选的，可以是单个语句，也可以是一个语句块。

![](img/9862a98a1a2d3bb14334137965a1ec60_303_0.png)

> 方括号（[]）不是语法的一部分；它们仅表示其中的内容是可选的。这种语法表示法贯穿本章。

上述语法是一个简单的 if 语句的语法，它只包含一个 if 子句和一个 else 子句。但是，C# 允许您在一个 if 语句中嵌套另一个 if 语句。您可以在 if 语句的 if 子句或 else 子句中嵌套多个 if 语句。请注意，在这种情况下，else 子句对应于最后一个（即最近的）if 语句。这是因为编译器会将 else 子句与最后一个未匹配的 if 语句（即没有 else 子句的 if 语句）关联起来。

嵌套 if 语句的语法如下：

```csharp
if(expression1)
{
    if(expression2)
    {
        //statements1
    }
    else
    {
        //statements2
    }
}
else
{
    if(expression3)
    {
        //statements3
    }
    else
    {
        //statements4
    }
}
```

在上述语法中，

- **if**：指用于表示 if 语句的 if 关键字
- **else**：指用于表示 if 语句的 else 子句的 else 关键字
- **expression1、expression2、expression3**：指 if 语句的布尔表达式
- **statements1、statements2、statements3、statements4**：指语句组

现在，让我们创建两个 Console 应用程序，逐一了解简单 if 语句和嵌套 if 语句的用法。

执行以下步骤以了解简单 if 语句的用法：

- 1. *启动* Visual Studio 2010。
- 2. 从菜单栏中*选择*“文件→新建→项目”。此时将打开“新建项目”对话框。
- 3. 在“新建项目”对话框左侧窗格的“已安装模板”部分中，*选择*“Visual C#→Windows”。
- 4. 从中间窗格中*选择*“控制台应用程序”以创建一个 Console 应用程序。
- 5. 在“名称”文本框中输入应用程序的名称 **IfStatement**（也可在 CD 上获得），并在“位置”框中为应用程序选择适当的位置。
- 6. 单击“确定”按钮关闭“新建项目”对话框并创建 IfStatement 应用程序。
- 7. *添加*清单 1.4 中所示的突出显示的代码片段到 **Program.cs** 文件中：

### 清单 1.4：展示用于演示 if 语句用法的代码

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace IfStatement
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.Write("Enter a number: ");
            int Num = Convert.ToInt32(Console.ReadLine());
            if (Num % 2 == 0)
                Console.WriteLine(Num + " is an even number!");
            else
                Console.WriteLine(Num + " is an odd number?");
            Console.ReadLine();
        }
    }
}
```

在清单 1.4 中突出显示的代码行中，我们首先提示用户输入一个数字。然后，我们将输入的数字存储在 **int** 类型变量 **Num** 中。接下来，我们使用 **if** 语句检查 **Num** 变量除以 2 的余数是否为 0。然后，我们显示一条消息，指示输入的数字是偶数。仅当 if 语句中测试的条件为 true 时，才会显示此消息。最后，我们显示与 else 子句对应的另一条消息，指示输入的数字是奇数。仅当 if 语句中测试的条件为 false 时，才会显示此消息。

- 8. 按键盘上的 F5 键运行应用程序。应用程序的输出出现，提示您输入一个数字，如图 C#-1.14 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_305_0.png)

图 C#-1.14

- 9. 在控制台中*输入* 10，然后按 **ENTER** 键。出现一条消息，指示输入的数字是偶数，如图 C#-1.15 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_305_1.png)

图 C#-1.15

- 10. *关闭*显示输出的控制台。

- 11. 再次按键盘上的 F5 键运行应用程序。应用程序的输出出现，提示您输入一个数字（图 C#-1.16）。

- 12. 在控制台中*输入* 15，然后按 **ENTER** 键。出现一条消息，指示输入的数字是奇数，如图 C#-1.16 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_305_2.png)

图 C#-1.16

现在，执行以下步骤以了解嵌套 if 语句的用法：

- 1. *启动* Visual Studio 2010。
- 2. 从菜单栏中*选择* **文件→新建→项目**。此时将打开“新建项目”对话框。
- 3. 在“新建项目”对话框左侧窗格的 **已安装模板** 部分中，*选择* **Visual C#→Windows**。
- 4. 从中间窗格中*选择* **控制台应用程序** 以创建一个 Console 应用程序。
- 5. 在 **名称** 文本框中输入应用程序的名称 **NestedIfStatements**（也可在 CD 上获得），并在 **位置** 框中为应用程序选择适当的位置。
- 6. 单击 **确定** 按钮关闭 **新建项目** 对话框并创建 **NestedIfStatements** 应用程序。
- 7. *添加* 清单 1.5 中所示的突出显示的代码片段到 **Program.cs** 文件中：

### 清单 1.5：展示用于演示嵌套 if 语句用法的代码

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace NestedIfStatements {
    class Program {
        static void Main(string[] args) {
            Console.Write("Enter a vowel:");
            char myChar = Convert.ToChar(Console.ReadLine());
            char x = Char.ToUpper(myChar);
            if (x == 'A')     //First if statement
                Console.WriteLine("The entered vowel is: A");
            else if (x == 'E') //Second if statement
                Console.WriteLine("The entered vowel is: E");
            else if (x == 'I') //Third if statement
                Console.WriteLine("The entered vowel is: I");
            else if (x == 'O') //Fourth if statement
                Console.WriteLine("The entered vowel is: O");
            else if (x == 'U') //Fifth if statement
                Console.WriteLine("The entered vowel is: U");
            else
                Console.WriteLine("The entered character is not a vowel!");
            Console.ReadLine();
        }
    }
}
```

在清单 1.5 中突出显示的代码行中，我们首先提示用户输入一个元音。然后，我们将输入的字符存储在 char 类型变量 myChar 中。接下来，我们将输入的字符转换为其大写形式，并将大写形式存储在另一个 char 类型变量 x 中。之后，我们使用一系列嵌套 if 语句来检查用户输入的是英文字母表中的哪个元音，并在控制台上显示一条消息，指明输入的元音。在最后一个 if 语句的 else 子句中，我们显示一条消息，指示输入的字符不是元音。仅当 if 语句中的所有条件都不为 true 时，才会显示此消息。

- 8. 按键盘上的 F5 键运行应用程序。应用程序的输出出现，提示您输入一个元音，如图 C#-1.17 所示。

![](img/9862a98a1a2d3bb14334137965a1ec60_306_0.png)

- 9. 在控制台中输入（a 或 A），然后按 ENTER 键。控制台上出现一条消息，指示输入的元音是 A，如图 C#-1.18 所示。

![](img/9862a98a1a2d3bb14334137965a1ec60_306_1.png)

- 10. 关闭显示输出的控制台。

