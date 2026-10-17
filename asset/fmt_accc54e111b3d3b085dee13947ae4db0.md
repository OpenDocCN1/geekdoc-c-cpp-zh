
```csharp
try {
    throw new DivideByZeroException();
} catch (DivideByZeroException) {
    Console.WriteLine("Exception");
}
```

## checked 和 unchecked 语句

`checked` 和 `unchecked` 语句用于检查溢出。整数类型的转换和运算使用 `unchecked` 关键字。下面的代码段展示了 `checked` 和 `unchecked` 语句的示例：

```csharp
byte number1 = 127;
byte number2 = 127;
try {
    byte result = (byte)(number1 * number2);
    Console.WriteLine("unchecked result: " + result);
    result = (checked)(number1 * number2);
    Console.WriteLine("checked result: " + result);
} catch (OverflowException exc) {
    Console.WriteLine(exc);
}
```

在前面的片段中，你可以看到 `OverflowException` 用于捕捉溢出。

## 解决方案

### 使用 if 语句

`if` 语句是计算机编程中最常用的条件语句。当块中的条件为真时执行块中的语句；否则，程序控制转移到 `else` 语句并执行 `else` 块中的语句。让我们创建一个名为 `MyIfStatement` 的控制台应用程序，展示 `if` 语句的使用。列表 3.1 显示了 `MyIfStatement` 应用程序的代码：

列表 3.1：`MyIfStatement` 应用程序代码

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace MyIfStatement
{
    class Program
    {
        static void Main(string[] args)
        {
            int year;
            Console.Write("enter the year value (yyyy): ");
            year = int.Parse(Console.ReadLine());
            if (year % 4 == 0 && year % 100 != 0 || year % 400 == 0)
            {
                Console.WriteLine("the " + year + " is a leap year,");
            }
            else
            {
                Console.WriteLine("the " + year + " is not a leap year,");
            }
            Console.Write("press ENTER to quit... ");
            Console.ReadLine();
        }
    }
}
```

在列表 3.1 中，提示用户输入年份。在 `if` 语句内部，定义了一个条件来测试指定的年份是否为闰年。如果满足条件，程序控制转移到 `if` 块并显示该年份为闰年；否则，程序控制转移到 `else` 块并显示该年份不是闰年。

图 3.3 显示了列表 3.1 的输出：

![](img/17af790174c480761404624aeed9b30b_168_0.png)

图 3.3：`MyIfStatement` 应用程序的输出

让我们学习如何使用嵌套 `if` 语句。

### 使用嵌套 if 语句

当程序中有多个需要评估条件时，可以使用一组嵌套 `if` 来评估这些条件。例如，如果你想在程序中检查学生的年龄、姓名和性别，可以使用嵌套 `if` 语句。

# 第 3 章：C# 5.0 程序中的流程控制与异常处理

列表 3.2：`MyNestedIfStatement` 的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace MyNestedIfStatement
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Finding the Largest of Three Numbers\n");
            Console.Write("Enter the First Number: ");
            int number = int.Parse(Console.ReadLine());
            Console.Write("Enter the Second Number: ");
            int number2 = int.Parse(Console.ReadLine());
            Console.Write("Enter the Third Number: ");
            int number3 = int.Parse(Console.ReadLine());
            if (number > number2 && number > number3)
            {
                Console.WriteLine(number + " is the Largest Number");
            }
            else
            {
                if (number2 > number3)
                {
                    Console.WriteLine(number2 + " is the Largest Number");
                }
                else
                {
                    Console.WriteLine(number3 + " is the Largest Number");
                }
            }
            Console.Write("\nPRESS ENTER to quit...");
            Console.ReadLine();
        }
    }
}
```

在列表 3.2 中，用户被提示输入三个数字。在第一个语句中，我们检查第一个数字是否大于第二、三个数字。如果满足条件，程序控制将跳转到该块并执行内部的语句。如果第一个语句不满足此条件，程序控制将跳转到 `else` 语句并检查第二个数字是否大于第三个。如果 `else` 语句满足，程序控制将跳转到 `else` 块并执行内部语句。如果两个语句都不满足条件，程序控制将跳转到 `else` 块并执行其内部语句。

在这种情况下（图 3.4），我们分别输入 89、20 和 46 作为第一、第二和第三个数字。它显示输出 89 是最大的数字。

图 3.4 显示了列表 3.2 的输出：

![](img/17af790174c480761404624aeed9b30b_169_0.png)

让我们学习使用 `switch` 语句。

### 使用 switch 语句

如前所述，C# 中的基本选择功能是 `if` 语句；然而，有时可能由于多个 `if` 语句的嵌套，导致程序变得复杂且难以理解。在这种情况下，你可以在程序中使用 `switch` 语句来降低复杂性并使其易于理解。

# 立即解决方案

让我们创建一个名为 `MySwitchStatement` 的控制台应用程序来展示 `switch` 语句的使用。列表 3.3 显示了 `MySwitchStatement` 程序的代码：

列表 3.3：`MySwitchStatement` 的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace MySwitchStatement
{
    class Program
    {
        static void Main(string[] args)
        {
            string Name;
            int Marks;
            Console.Write("Enter Name: ");
            Name = Console.ReadLine();
            Console.Write("Enter Marks: ");
            Console.WriteLine("Select the Range of Marks: ");
            Console.WriteLine("1. 0-20");
            Console.WriteLine("2. 21-40");
            Console.WriteLine("3. 41-60");
            Console.WriteLine("4. 61-80");
            Console.WriteLine("5. 80-100");
            Console.Write("Enter Your Choice (1,2,3,4,5): ");
            Marks = int.Parse(Console.ReadLine());
            switch (Marks)
            {
                case 1:
                    Console.write(Name + " your marks are Low.\n");
                    break;
                case 2:
                    Console.write(Name + " your marks are Low.\n");
                    break;
                case 3:
                    Console.write(Name + " your marks are Average.\n");
                    break;
                case 4:
                    Console.write(Name + " your marks are Good.\n");
                    break;
                case 5:
                    Console.write(Name + " your marks are very good.\n");
                    break;
                default:
                    break;
            }
            Console.write("\nPress ENTER to quit... ");
            Console.ReadLine();
        }
    }
}
```

在列表 3.3 中，用户被提示输入名称并选择分数范围。选择分数范围后，用户被提示根据分数范围输入选择（`case`）。当用户输入选择时，将根据该选择显示消息。

图 3.5 显示了列表 3.3 的输出：

![](img/17af790174c480761404624aeed9b30b_171_0.png)

### 使用穿透式（Fall-through）switch 语句

穿透 `switch` 语句是 `switch` 语句的一种，其中多个 `case` 通过一个语句块和 `break` 语句组合在一起。让我们创建一个名为 `DaysMonth` 的控制台应用程序来展示如何使用穿透 `switch` 语句。列表 3.4 显示了 `DaysMonth` 程序的代码：

列表 3.4：`DaysMonth` 的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace DaysMonth
{
    class ClassProgram
    {
        static void Main(string[] args)
        {
            string month;
            Console.Write("Enter the Name of a Month: ");
            month = Console.ReadLine().ToUpper();
            switch (month)
            {
                case "JANUARY":
                case "MARCH":
                case "MAY":
                case "JULY":
                case "AUGUST":
                case "OCTOBER":
                case "DECEMBER":
                    Console.WriteLine(month + " has 31 days");
                    break;
                case "APRIL":
                case "JUNE":
                case "SEPTEMBER":
                case "NOVEMBER":
                    Console.WriteLine(month + " has 30 days");
                    break;
                case "FEBRUARY":
                    Console.WriteLine(month + " has 28 or 29 days");
                    break;
                default:
                    Console.WriteLine("You have entered an month name");
                    break;
            }
        }
    }
}
```

# 立即解决方案

```
            Console.write("\nPress ENTER to quit...");
            Console.ReadLine();
```

在 3.4 中，我们将天数相同的月份组合在一起，例如一月和三月。将所有相同输出的情况放在一个处的原因是我们可以对它们应用单一的 `break` 语句。当用户输入无效月份时，会执行 `default` 语句。

图 3.6 显示了 3.4 的输出：

![](img/17af790174c480761404624aeed9b30b_172_0.png)

图 3.6：`DayMonth` 程序的输出

当循环进入错误的月份时，我们会得到消息：“You have entered an month name”。

# 使用 while 循环

C# 中的 `while` 循环用于重复过程直到满足条件。让我们创建一个名为 `MyWhileLoop` 的控制台应用程序，展示如何使用 `while` 循环。列表 3.5 显示了 `MyWhileLoop` 的代码。

列表 3.5：`MyWhileLoop` 程序的代码
