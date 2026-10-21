
# 17.2 查找以下用于控制台读写程序中的错误。

```
using System;
using System.Collections.Generic;
using System.Text;

namespace debugApp2_chap17
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("This is a Console Application in C#!");
            Console.Write("Please enter your Name: ");
            string name = Console.ReadLine();
            Console.WriteLine("Hi! ", name , ". This program takes input from the users.");
            Console.Write();
        }
    }
}
```

# 17.3 更正用于计算两个数之和的程序。

```
using System;
using System.Collections.Generic;
using System.Text;

namespace debugApp3_chap17
{
    class Program
    {
        int num1 = 0;
        int num2 = 0;
        int sum = 0;
        static void Main(string[] args)
        {
            Console.WriteLine("Please enter the first number : ");
            num1 = Int32.Parse(Console.ReadLine());
            Console.WriteLine("Please enter the second number : ");
            num2 = Int32.Parse(Console.ReadLine());
            sum = addValues(num1 + num2);
            Console.WriteLine("Sum of " + num1 + " + " + num2 + " = " + sum);
            Console.ReadLine();
        }
        int addValues(int m, int n)
        {
            return m + n;
        }
    }
}
```

## 编程练习

### 17.1 编写一个程序，仅使用一条 Write 语句和一条 WriteLine 语句，打印如下所示的从 1 × 1 到 9 × 9 的乘法表：

```
1 2 3 4 5 6 7 8 9
2 4 . . . . . . 18
3 6 . . . . . . 27
. . . . . . . . .
. . . . . . . . .
9 18 27 . . . . . 81
```

### 17.2 修改以上程序，使显示内容包含居中的标题 MULTIPLICATION TABLE。

### 17.3 编写一个程序，将整数 111、222 和 333 存储在一个数组中，并按照以下方式显示，不使用任何循环语句。

```
(a)111 222 333
```

```
(b)111
222
333
```

### 17.4 编写一个能够产生以下输出的程序：

```
Product of 1 and 1 is 1
Product of 3 and 3 is 9
Product of 5 and 5 is 25
Product of 7 and 7 is 49
Product of 9 and 9 is 81
```

### 17.5 编写一个程序，以 10 的列宽打印数值 1234：

- (a) 右对齐
- (b) 左对齐
- (c) 右对齐并在左侧填充零

### 17.6 编写一个程序，以指数格式打印数值 10.45678，并满足以下要求：

- (a) 精确到两位小数
- (b) 精确到四位小数
- (c) 精确到八位小数

### 17.7 编写一个程序，以定点格式打印数值 345.6789，并满足以下要求。

- (a) 精确到两位小数
- (b) 精确到五位小数
- (c) 精确到零位小数

### 17.8 编写一个程序，使用以下格式规范打印整数 3456789：

- (a) 使用格式字符 D
- (b) 使用格式字符 N
- (c) 使用格式字符 E
- (d) 使用零占位符
- (e) 使用井号字符
- (f) 使用逗号分隔符

### 17.9 编写一个程序，演示以下格式字符的使用：

- (a) 小数点分隔符 (.)
- (b) 百分号 (%)

### 17.10 编写一个程序，读取并显示以下数据表：

| 项目名称 | 项目代码 | 价格 |
|-----------|-----------|-------|
| 风扇       | 67831     | 1234.50 |
| 电机     | 935642    | 5786.70 |

项目名称和项目代码必须左对齐，价格应右对齐。

## 18.3.1 编译时错误

所有语法错误都会被 C# 编译器检测并显示，因此这些错误被称为编译时错误。每当编译器显示错误时，它不会生成 .cs 文件。因此，我们必须修复所有错误，才能成功编译并运行程序。

# 程序 18.1 编译时错误示例

```
/* This program contains an error */
using Sytem;
class Error1
{
    public static void Main()
    {
        Console.WriteLine("Hello C#!");
    }
}
```

C# 编译器在告诉我们程序中的错误位置方面做得很出色。例如，如果在程序 18.1 中拼错了 System 命名空间，屏幕上将显示以下消息：

Error1.cs(2.7) : 错误 CS0234 : 类或命名空间中不存在类型或命名空间名称“Sytem”。

我们现在可以转到相应的行，更正错误并重新编译程序。有时，单个错误可能是编译后期多个错误的根源。例如，在多处使用未声明的变量将导致一系列“未定义变量”类型的错误。我们通常应将最早出现的错误视为问题的主要来源。修复此类错误后，应重新编译程序并查找其他错误。

大多数编译时错误是由打字错误引起的。印刷错误很难发现。我们可能需要逐词甚至逐字符地检查代码。最常见的问题有：

- 缺少分号
- 类和方法中括号缺失（或不匹配）
- 标识符和关键字拼写错误
- 字符串中缺少双引号
- 使用未声明的变量
- 赋值/初始化中的类型不兼容
- 对对象的错误引用
- 使用 = 代替 == 运算符等

## 18.3.2 运行时错误

有时，程序可能成功编译并生成 .exe 文件，但可能无法正常运行。此类程序可能因逻辑错误而产生错误结果，或因堆栈溢出等错误而终止。最常见的运行时错误有：

- 将整数除以零。
- 访问数组边界之外的元素。
- 试图将值存储到不兼容类或类型的数组中。
- 传递的方法参数不在有效范围或不是有效值。
- 试图对数组使用负大小。
- 将空对象引用作为合法对象引用来访问方法或变量。
- 将无效字符串转换为数字，或将无效数字转换为字符串。
- 访问字符串边界之外的字符等。

当遇到此类错误时，C# 通常会生成错误消息并中止程序。程序 18.2 演示了运行时错误如何导致程序执行终止。

# 程序 18.2 运行时错误示例

```
using System;
class Error2
{
    public static void Main()
    {
        int a = 10;
        int b = 5;
        int c = 5;

        int x = a/(b-c);
        Console.WriteLine("x = " + x);

        int y = a/(b+c);
        Console.WriteLine("y = " + y);
    }
}
```

程序 18.2 在语法上是正确的，因此编译过程中不会出现任何问题。当 C# 运行时尝试执行除以零的操作时，会生成一个错误条件，导致程序在显示相应的消息后停止。以下语句永远不会执行：
int y = a/(b + c);

## 18.4 异常

异常是由程序中的运行时错误导致的一种状态。当 C# 编译器遇到诸如整数除以零之类的错误时，它会创建一个异常对象并抛出它（即告知我们发生了错误）。

如果异常对象未被正确捕获和处理，编译器将显示错误消息并终止程序。如果我们希望程序继续执行其余代码，则应尝试捕获错误条件抛出的异常对象，然后显示适当的消息以采取纠正措施。此任务称为异常处理。

异常处理机制的目的是提供一种检测和报告“异常情况”的手段，以便采取适当的行动。该机制建议并入一个单独的错误处理代码，该代码执行以下任务：

- 发现问题（命中异常）
- 通知错误已发生（抛出异常）
- 接收错误信息（捕获异常）
- 采取纠正措施（处理异常）
