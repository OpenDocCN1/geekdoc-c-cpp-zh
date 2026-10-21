

```csharp
Console.WriteLine("London");
Console.WriteLine("Bombay");
Console.WriteLine("Paris");
Console.WriteLine("Type your choice");
String name = Console.ReadLine();

switch (name)
{
    case "Bombay":
        Console.WriteLine("Bombay:Guide 5");
        break;
    case "London":
        Console.WriteLine("London:Guide 10");
        break;
    case "Paris":
        Console.WriteLine("Paris:Guide 15");
        break;
    default:
        Console.WriteLine("Invalid choice");
        break;
}
}
```

程序 6.6 的输出：

```
Select your choice
London
Bombay
Paris
Type your choice
London
London : Guide 10
```

### 6.7.1 Switch 语句中的贯穿

如果在 case 块中没有 break 语句，控制能够无问题地转移到下一个 case 块，这种情况被称为‘贯穿’。贯穿在 C、C++ 和 Java 中是允许的。但在 C# 中，如果 case 块包含可执行代码，则不允许自动贯穿。但是如果 case 块为空，如前所述，则允许。例如，

```csharp
switch (m)
{
    case 1:
        x = y;
    case 2:
        x = y + m;
    default:
        x = y - m;
}
```

在 C# 中是错误的。如果我们希望连续执行两个 case 块，就必须使用 goto 语句强制该过程。例如：

```csharp
switch (m)
{
    case 1:
        x = y;
        goto case 2;
    case 2:
        x = y + m;
        goto default;
    default:
        x = y - m;
        break;
}
```

goto 机制使我们能够在 case 之间向前和向后跳转，因此可以任意排列标签。示例：

```csharp
switch (m)
{
    default:
        x = y - m;
        break;
    case 2:
        x = y + m;
        goto default;
    case 1:
        x = y;
        goto case 2;
}
```

是完全有效的。

程序 6.7 使用 switch case 允许用户选择可乐罐的大小。根据用户选择，程序会打印用户必须为所选特定类型的罐支付的金额。

### 程序 6.7 | 另一个 SWITCH 示例

```csharp
using System;
class SwitchExample
{
    public static void Main()
    {
        Console.WriteLine("Select your Cola Can:");
        Console.WriteLine("S=SMALL M=MEDIUM L=LARGE");
        Console.Write("Please enter your option: ");
        String s = Console.ReadLine();
        int cost = 0;
        switch (s)
        {
            case "S":
                cost += 10;
                break;
            case "M":
                cost += 15;
                goto case "S";
            case "L":
                cost += 30;
                goto case "S";
            default:
                Console.WriteLine("Invalid option. Please select either S, M, or L.");
                break;
        }
        if (cost != 0)
            Console.WriteLine("Please pay {0} Rupees.", cost);
    }
}
```

![](img/bae4ee2c7c29c052feb3b9a9c5659998_112_0.png)

## 6.8 ?: 运算符

C# 有一个不寻常的运算符，用于进行双向决策；它是由 ? 和 : 组合而成，接受三个操作数。该运算符通常被称为条件运算符。条件运算符的一般使用形式如下：

```
conditional expression ? expression1 : expression2
```

首先评估条件表达式。如果结果为真，则评估 expression1 并作为条件表达式的值返回。否则，评估 expression2 并返回其值。例如，段落

```csharp
if (x < 0)
    flag = 0;
else
    flag = 1;
```

可以写成

```csharp
flag = (x < 0) ? 0 : 1;
```

考虑以下函数的求值：

```
y = 1.5x + 3      for x <= 2
y = 2x + 5        for x > 2
```

这可以使用条件运算符如下求值：

```csharp
y = (x > 2) ? (2*x + 5) : (1.5*x + 3);
```

条件运算符可以嵌套以求值更复杂的赋值决策。例如，考虑一名销售家用产品的售货员的周薪。如果 x 是每周售出的产品数量，她的周薪由下式给出

```
salary = { 4x + 100 for x < 40
          300 for x = 40
          4.5x + 150 for x > 40 }
```

该复杂方程可以写成

```csharp
salary = (x != 40) ? ((x < 40) ? (4*x + 100) : (4.5*x + 150)) : 300; // nesting
```

也可以使用 if...else 语句如下求值：

```csharp
if (x <= 40)
    if (x < 40)
        salary = 4*x + 100;
    else
        salary = 300;
else
    salary = 4.5*x + 150;
```

使用条件运算符时，代码变得更简洁，也许更高效。然而，可读性较差。当需要超过一次嵌套条件运算符时，最好使用 if 语句。

## 案例研究

### 问题陈述

SafeMoney Bank 为个人提供为期 1 至 15 年的简单和复利贷款。直到最近，SafeMoney Bank 的员工一直手动计算银行向个人提供的贷款的简单和复利利息。SafeMoney Bank 的经理发现，在过去两个月里，银行员工在计算简单和复利利息时出现了很多错误。此外，贷款审批也出现了很多延迟。因此，银行正在失去宝贵的客户。SafeMoney Bank 的经理如何解决这个问题？

### 解决方案

必须自动化计算简单和复利利息的任务，以减少计算中的错误。SafeMoney Bank 的经理要求 Binoy，即 SafeMoney Bank IT 部门的高级程序员，创建一个应用程序来自动化计算简单和复利利息的任务，以便银行员工能够高效地执行。经过需求分析后，Binoy 决定必须在应用程序中使用诸如 If Else 之类的决策语句，并辅以 C# 来计算简单和复利利息。Binoy 创建了以下 C# 应用程序。

```csharp
using System;

class InterestCalculator
{
    public static void Main()
    {
        Console.WriteLine("==Interest Calculator==");
        Console.WriteLine("Calculate Simple (S) / Compound (C) Interest: ");
        string choice = Console.ReadLine();

        Console.WriteLine("Enter Principal Amount: ");
        double p = double.Parse(Console.ReadLine());
        Console.WriteLine("Enter Rate of Interest: ");
        double r = double.Parse(Console.ReadLine());
        Console.WriteLine("Enter Duration: ");
        int t = Int32.Parse(Console.ReadLine());

        if (choice == "S")
        {
            double simpleInterest = (double)((p * r * t) / 100);
            Console.WriteLine("The Simple Interest is: {0,0:Rs ###.##}", simpleInterest);
        }
        else
        {
            double compoundInterest = (double)p * (Math.Pow(((r / 100) + 1), t));
            Console.WriteLine("The Compound Interest is: {0,0:Rs ###.##}", compoundInterest);
        }
    }
}
```

### 备注

C# 中的 If Else 语句可用于评估条件，并且在评估结果的基础上，必须决定程序的控制流。如果与 If 语句一起给出的条件评估为真，则必须执行特定的一组程序语句。但是如果条件评估为假，则必须执行另一组程序语句。

## 常见编程错误

- 使用 `=` 代替 `==` 符号。
- 嵌套 `if` 语句中的悬空 else。
- 在多分支构造的某些路径中忘记初始化变量。
- `&&` 和 `||` 条件运算符的不当和混淆使用。
- 未正确应用运算符优先级。
- 使用多个关系运算符如 `(a <= x <= b)`。
- 在 `if` 语句中比较浮点表达式如 `if (x == y)`。
- 在 switch 语句中忘记为 case 标签使用冒号。
- 在 switch 语句中未使用 `goto` 进行贯穿 case。
- 将运算符 `<=`、`>=` 和 `!=` 用作 `<=`、`>=` 和 `=!`。
- 在运算符 `==`、`<=`、`>=` 和 `!=` 的符号之间提供空格。
- 当 `if` 语句块包含多个语句时未使用大括号。
- 在 `if` 语句的测试表达式中使用整数值，如 `if (x).....`。
- 在 `if` 语句中条件后的右括号后立即放置分号。
- `if...else` 语句的嵌套不当。
