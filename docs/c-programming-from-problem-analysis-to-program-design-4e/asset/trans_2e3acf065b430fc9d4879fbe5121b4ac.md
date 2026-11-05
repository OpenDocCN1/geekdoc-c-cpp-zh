

![](img/36e48639a06772bcb0fa1ea2525b33a3_302_0.png)

图 5-1 单向 if 语句

### 示例 5.9

一家公司在年底向所有产品销售额超过 500,000.00 美元的员工发放 1000.00 美元奖金。下面的代码段是一个程序，允许用户输入其销售额。它判断是否应发放奖金，并显示一条消息指示是否授予奖金。

```csharp
/* BonusCalculator.cs  Author: Doyle
 * Allows the user to input their
 * gross sales for the year. This value
 * is checked to determine whether
 * a bonus is in order.
 *********************************/

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace BonusCalculatorApp
{
    class BonusCalculatorApp
    {
        static void Main( )
        {
            string inValue;
            decimal salesForYear;
            decimal bonusAmount = 0M;

            Console.WriteLine("Do you get a bonus this year?");
            Console.WriteLine( );
            Console.WriteLine("To determine if you are due "
                                + "one,");
            Console.Write("enter your gross sales figure: ");
            inValue = Console.ReadLine();
            salesForYear = Convert.ToDecimal(inValue);
            if (salesForYear > 500000.00M)
            {
                Console.WriteLine( );
                Console.WriteLine("YES...you get a bonus!");
                bonusAmount = 1000.00M;
            }
            Console.WriteLine("Bonus for the year: {0:C}",
                                bonusAmount);
            Console.ReadLine( );
        }
    }
}
```

由于此应用程序涉及金额，因此使用新数据类型 decimal 来保存输入的值和奖金金额。请注意，在声明变量时，特殊后缀 M 被放在初始化值的末尾。该声明重复如下：

```csharp
decimal bonusAmount = 0M;
```

同样有必要在作为待求值表达式一部分的 decimal 数字字面量末尾加上 M：

```csharp
if (salesForYear > 500000.00M)
```

当赋值语句将 decimal 值 1000.00M 存入 bonusAmount 内存位置时，同样需要包含 M：

```csharp
bonusAmount = 1000.00M;
```

> **注意**
> 
> 特殊符号 m 和 M 代表金额。与 `decimal` 变量一起使用的数字字面量需要 `M`；否则会发出语法错误消息。

在查看示例 5-9 时，请注意对 Convert 类中某个方法的调用。第 3 章介绍了 Parse( ) 方法，用于将存储在字符串变量中的值转换为数值类型。也可以使用 Convert 类进行此转换。Convert 位于 System 命名空间中，并具有将一种基类型转换为另一种基类型的方法。示例 5-9 使用 Convert.ToDecimal( ) 方法将输入的字符串值转换为 decimal 值。要转换为整数，请使用 Convert.ToInt32( )；要转换为 double，请使用 Convert.ToDouble( )。如果使用 Visual Studio，请务必使用 IntelliSense 功能。您可以探索 Convert 类中可用的许多方法及其重载。

对于示例 5-9，用户输入 600000 时产生的输出如图 5-2 所示。

![](img/36e48639a06772bcb0fa1ea2525b33a3_304_0.png)

图 5-2 salesForYear 等于 600000.00 的 BonusApp

问题定义表明，销售额必须超过 500,000.00 美元才会发放奖金。输入 500000.00 时产生的输出如图 5-3 所示。

![](img/36e48639a06772bcb0fa1ea2525b33a3_304_1.png)

图 5-3 salesForYear 等于 500000.00 的 BonusApp

初学者程序员常常错误地在待求值的括号表达式末尾放置分号。如果这样做，程序仍会运行，并且不会发出语法错误消息。但是，您会创建一个空语句体来代替真语句。这种逻辑基本上表示：“当表达式求值为 true 时，什么也不做。”如果使用 Visual Studio 并将分号放在错误位置（如图 5-4 所示），您会看到一个绿色波浪线指示器，提醒您存在潜在问题。大多数其他语言的 IDE 不会警告您可能存在此问题。

![](img/36e48639a06772bcb0fa1ea2525b33a3_305_0.png)

图 5-4 IntelliSense 弹出消息

在 Visual Studio 中，当您将指针移到红色警告上时，IntelliSense 会弹出消息：“可能错误地使用了空语句。”

单向 if 语句不为表达式求值为 false 的情况提供另一组步骤。双向 if 语句则提供该选项。

## 双向 if 语句

可以向 if 语句添加可选的 else 子句，以提供当表达式求值为 false 时要执行的语句。对于双向 if 语句，要么执行真语句，要么执行假语句，但不会两者都执行。执行完其中一组语句后，控制权总是转移到 if 块后面的语句。双向 if 语句的一般格式为：

```
if (conditional_expression)    //No semicolon is placed on this line
    statement;                 //Executed when expression is true
else
    statement;                 //Executed when expression is false
```

请注意，不需要在 else 中重复表达式。许多初学者程序员会这样写：

```
if (aValue == 100)
    Console.WriteLine("The value is 100");
else (aValue != 100)  // INCORRECT! No need to repeat the expression.
    Console.WriteLine("The value is not 100");
```

包含 else 的正确方式是将其单独放在一行，不带任何表达式。在 else 后面的行中，包含当表达式求值为 false 时要执行的语句。下面是编写选择语句的正确方式：

```
if (aValue == 100)
    Console.WriteLine("The value is 100");
else
    Console.WriteLine("The value is not 100");
```

与单向 if 语句一样，您可以通过将语句括在花括号中来包含多条语句。

> **注意**
> 
> 可读性很重要。请注意单向和双向 if 语句所使用的缩进。语句与条件表达式对齐。可以在 Visual Studio 中设置智能缩进，以便自动对齐。

图 5-5 说明了双向 if 语句的执行流程。

![](img/36e48639a06772bcb0fa1ea2525b33a3_306_0.png)

图 5-5 双向 if 语句

当表达式求值为 true 时，执行真语句。如图所示，无论执行真语句还是假语句，执行都会在同一位置继续。请考虑示例 5-10。

### 示例 5.10

```
if (hoursWorked > 40)
{
    payAmount = (hoursWorked - 40) * payRate * 1.5 + payRate * 40;
    Console.WriteLine("You worked {0} hours overtime.", hoursWorked - 40);
}
else
    payAmount = hoursWorked * payRate;
Console.WriteLine("I am displayed, whether the expression " + "evaluates true or false");
```

如示例 5-10 所示，真部分可以有一个语句块，而假部分可以只有一条语句。此示例中假语句不需要花括号；不过，添加花括号可以提高可读性。

## TryParse() 方法

在前几章中，您使用 Parse() 方法将作为参数传入的字符串值转换为其等效的数值。您还了解到，可以使用 Convert 类的成员来完成转换。但是，如果要转换的字符串值对这两种选项中的任何一种无效，程序就会崩溃。会引发异常。在测试程序时，您可能已经遇到过引发异常的情况。例如，当需要输入数字时输入了字母字符，然后尝试将输入的值解析为数字，程序会停止执行。如果输入的值太大并尝试解析它，程序会崩溃。第 11 章将更详细地介绍调试和处理异常。

既然已经介绍了 if 语句，您可以在进行转换之前测试该值，以避免引发异常。另一种选择是使用 TryParse() 方法。第 3 章提到了 TryParse() 方法。它类似于 Parse() 方法，不同之处在于转换失败时 TryParse() 不会引发异常。TryParse() 方法将值的字符串表示形式转换为其等效的其他类型的值。它还返回一个 Boolean 返回值，指示转换是否成功。TryParse() 方法的标题如示例 5-11 所示。

