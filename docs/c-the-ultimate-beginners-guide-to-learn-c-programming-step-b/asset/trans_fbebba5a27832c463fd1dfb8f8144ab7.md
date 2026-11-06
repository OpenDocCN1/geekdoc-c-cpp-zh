
```csharp
}
```

输出如下所示：

```text
Value of x is 2
Exact value of x is: 2
```

一个 *else if* 条件求值为真，因此其块内的语句被执行了。所有条件之外的代码块也执行了。你可以通过将 x 的值修改为各种值来试验这段代码，看看会发生什么。

### 嵌套 if 语句

C# 允许我们嵌套条件语句。我们可以嵌套 *if* 和 *else if* 语句，这意味着我们在另一个 *if* 或 *else if* 语句内部使用 *if* 语句。下面的语法演示了如何在 C# 中嵌套 *if* 语句：

```csharp
if( boolean_expression a) {

    /* 如果布尔表达式 a 为真，则执行 */

    if(boolean_expression b) {

        /* 如果布尔表达式 b 为真，则执行 */

    }

}
```

*else if* 语句可以使用上面给出的语法进行嵌套。

考虑下面给出的示例：

```csharp
using System;

namespace DecisionMaking {

    class NestedIf {

        static void Main(string[] args) {

            /* 定义局部变量 */

            int x = 1;
            int y = 2;


            /* 检查布尔条件 */

            if (x == 1) {
                /* 如果条件为真，则检查下面的 if 条件 */
                if (y == 2) {
                    /* 如果条件为真，则打印以下内容 */
                    Console.WriteLine("Value of x is 1 and y is 2");
                }
            }
            Console.WriteLine("Exact value of x is : {0}", x);
            Console.WriteLine("Exact value of y is : {0}", y);
            Console.ReadLine();
        }
    }
}
```

代码返回：

```text
Value of x is 1 and y is 2
Exact value of x is : 1
Exact value of y is : 2
```

两个 *if* 条件都求值为真，因此嵌套 *if* 中的语句被执行了。如果其中一个或两个条件求值为假，那么这条语句就不会被执行。下面是一个示例：

```csharp
using System;

namespace DecisionMaking {
    class NestedIf {
        static void Main(string[] args) {
            /* 定义局部变量 */
            int x = 1;
            int y = 2;
            /* 检查布尔条件 */
            if (x == 1) {
                /* 如果条件为真，则检查下面的 if 条件 */
                if (y == 3) {
                    /* 如果条件为真，则打印以下内容 */
                    Console.WriteLine("Value of x is 1 and y is 2");
                }
            }
            Console.WriteLine("Exact value of x is : {0}", x);
            Console.WriteLine("Exact value of y is : {0}", y);
            Console.ReadLine();
        }
    }
}
```

在上面的代码中，嵌套的 *if* 条件检查变量 y 的值是否为 3，而这是假的。这个块中的语句将不会被执行。*C#* 编译器会跳过这一部分，继续执行条件之外的代码。它返回以下内容：

```text
Exact value of x is : 1
Exact value of y is : 2
```

### switch 语句[15]

这条语句与使用多个 *if* 语句是一样的。它由一个可能性列表、针对每种可能性的操作以及一个默认部分组成，默认部分用于在没有任何一个选项求值为真时执行。下面是此语句的语法：

```csharp
switch(expression)

{
    case <value_1>:

        // 代码

        break;

    case <value_2>:

        // 代码

        break;

    case <value_N>:
        // 代码
        break;

    default:
        // 代码
        break;
}
```

下面是一个示例：

```csharp
using System;

public class SwitchStatement
{
    public static void Main()
    {
        int a = 3;
        switch (a)
        {
            case 1:
                Console.WriteLine("The value of x is 1");
                break;

            case 2:
                Console.WriteLine("The value of x is 2");
                break;

            case 3:
                Console.WriteLine("The value of x is 3");
                break;

            default:
                Console.WriteLine("Unknown value of x");
                break;
        }
    }
}
```

代码返回以下内容：

```text
The value of x is 3
```

变量的值被初始化为 3。执行代码后，会匹配到 3 对应的 *case* 代码，因此其块中的语句将被执行。如果所有 *case* 条件都不为真，则将执行 *default* 部分。下面演示了这种情况：

```csharp
using System;

public class SwitchStatement
{
    public static void Main()
    {
        int a = 5;

        switch (a)
        {
            case 1:
                Console.WriteLine("The value of x is 1");
                break;
            case 2:
                Console.WriteLine("The value of x is 2");
                break;
            case 3:
                Console.WriteLine("The value of x is 3");
                break;
            default:
                Console.WriteLine("Unknown value of x");
                break;
        }
    }
}
```

代码返回如下输出：

```text
Unknown value of x
```

switch 语句中的 case 标签必须是唯一的。switch 语句可用于任何类型的表达式，包括字符串、整数、bool、char、枚举等。下面是如何将其用于字符串：

```csharp
using System;

public class SwitchStatement
{
    public static void Main()
    {
        string firstName = "Nicholas";
        switch (firstName)
        {
            case "Samuel":
                Console.WriteLine("Your first name is Samuel");
                break;
            case "Nicholas":
                Console.WriteLine("Your first name is Nicholas");
                break;
            case "Bismack":
                Console.WriteLine("Your first name is Bismack");
                break;
        }
    }
}
```

代码返回以下输出：

```text
Your first name is Nicholas
```

### switch 中的 Goto[16]

在某些情况下，使用 *switch* 语句时，我们可能需要跳到某个 case。这可以使用 *jump* 或 *goto* 语句来完成。考虑下面给出的示例：

```csharp
using System;

public class SwitchStatement
{
    public static void Main()
    {
        string firstName = "Nicholas";
        switch (firstName)
        {
            case "text":
                Console.WriteLine("is your first name");
                break;
            case "Samuel":
                Console.WriteLine("Samuel");
                break;
            case "Nicholas":
                Console.WriteLine("Nicholas");
                goto case "text";
                break;
            case "Bismack":
                Console.WriteLine("Bismack");
                break;
        }
    }
}
```

代码返回以下输出：

```text
Nicholas
is your first name
```

### 嵌套 Switch

可以在另一个 switch 语句内创建 switch 语句，这就构成了嵌套 switch。下面是一个示例：

```csharp
using System;

public class NestedSwitch
{
    public static void Main()
    {
        int x = 10;

        switch (x)
        {
            case 10:
                Console.WriteLine(10);

                switch (x - 1)
                {
                    case 9:
                        Console.WriteLine(9);

                        switch (x - 2)
                        {
                            case 8:
                                Console.WriteLine(8);
                                break;
                        }
                        break;
                }
                break;
            case 20:
                Console.WriteLine(20);
                break;
            case 125:
                Console.WriteLine(25);
                break;
            default:
                Console.WriteLine(30);
                break;
        }
    }
}
```

输出如下：

## 第 8 章：循环

作为一名程序员，你会使用循环语句来重复运行某些代码块。循环在 C# 编程中起着重要作用。因此，如果你想在短时间内掌握这门语言，也应该认真学习这部分内容。

### 循环基础

在创建程序时，你经常需要多次执行代码序列。多次输入相同的代码块会非常乏味。因此，你需要一种快速简单的方法来重复代码。幸运的是，C# 语言支持循环语句。

循环是一种重复运行代码片段的工具。你可以使用它按特定次数运行代码，或者只要给定条件满足就持续运行。C# 提供了不同类型的循环语句。让我们逐一详细分析每种类型：

### while 循环[47]

这是 C# 中最简单的循环语句。其语法为：

```csharp
while (the_assigned_condition)
{
    the_loop’s_body;
}
```

在此语法中，“the_assigned_condition”是一个产生布尔值的表达式。该条件决定了“body”将运行多少次。另一方面，“body”是你想要执行的语句（或语句组）。

下面给出的图将说明 while 循环是如何工作的：

![](img/9196118a802f2581793dbd40a99c7360_61_0.png)

在处理 “while” 循环时，C# 程序会检查布尔值

