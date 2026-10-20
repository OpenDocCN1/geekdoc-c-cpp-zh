
```csharp
String lastname = "Doe";
```

```csharp
String name = $"My full name is: {firstname} {lastname}";
```

```csharp
Console.WriteLine(name);
```

你可以通过引用其索引号来访问字符串中的字符 **Access Strings**

在方括号 [] 内。

此示例：打印 mystring 中的第一个字符：

## Example:

```csharp
String mystring = "Hello";
```

```csharp
Console.WriteLine(mystring[0]); // Outputs "H"
```

## Adding Numbers and Strings

WARNING!

C# 使用 + 运算符进行加法和连接。

记住：数字相加。字符串连接。

如果你添加两个数字，结果将是一个数字：

## Example:

```csharp
int x = 10;
```

int y = 20;

int z = x + y; // z will be 30 (an integer/number)

![](img/e7ca4af023a4148a909dd82c11f81893_67_0.png)

## C# Booleans

在编程中，你经常需要一种数据类型只能有两个值，例如：

- YES / NO
- ON / OFF
- TRUE / FALSE

对于此，C# 有一个 bool 数据类型，可以取 true 或 false 的值。

### Boolean Values

布尔类型使用 bool 关键字声明，只能取 true 或 false 的值：

## Example:

```
bool iscsharpfun = true;
```

```
bool isfishatasty = false;
```

```
Console.WriteLine(iscsharpfun); // Outputs True
```

```
Console.WriteLine(isfishatasty); // Outputs False
```

## Boolean Expression

布尔表达式是返回布尔值：True 或 False 的 C# 表达式。

你可以使用比较运算符，例如大于（>）运算符来判断一个表达式（或变量）是否为真：

## Example:

```
int x = 10;
```

```
int y = 9;
```

```
Console.WriteLine(x > y); // returns True, because 10 is higher than 9
```

```
using System;

namespace MyApplication
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine(10 != 15); // returns False, because 10 is not equal to
        }
    }
}
```

![](img/e7ca4af023a4148a909dd82c11f81893_69_0.png)

## 2.13 C# Conditions and If Statements

C# 支持数学中的常见逻辑条件：

- 小于：a < b
- 小于或等于：a <= b
- 大于：a > b
- 大于或等于：a >= b
- 等于 a == b
- 不等于：a != b

你可以使用这些条件为不同的决策执行不同的操作。

C# 有以下条件语句：

- 使用 if 指定在指定条件为真时执行的代码块
- 使用 else 指定在同一条件为假时执行的代码块

```csharp
using System;

namespace MyApplication
{
    class Program
    {
        static void Main(string[] args)
        {
            if (20 > 18)
            {
                Console.WriteLine("20 is greater than 18");
            }
        }
    }
}
```

![](img/e7ca4af023a4148a909dd82c11f81893_71_0.png)

```csharp
using System;

namespace MyApplication
{
    class Program
    {
        static void Main(string[] args)
        {
            int x = 20;
            int y = 18;
            if (x > y)
            {
                Console.WriteLine("x is greater than y");
            }
        }
    }
}
```

![](img/e7ca4af023a4148a909dd82c11f81893_71_1.png)

### 2.13.2 The else Statement

使用 else 语句指定在条件为 False 时执行的代码块。

Syntax

```text
if (condition)
{
    // block of code to be executed if the condition is True
}
```

Else

{

// block of code to be executed if the condition is False }

```
using System;
namespace MyApplication
{
    class Program
    {
        static void Main(string[] args)
        {
            int time = 20;
            if (time < 18)
            {
                Console.WriteLine("Good day.");
            }
            else
            {
                Console.WriteLine("Good evening.");
            }
        }
    }
}
```

![](img/e7ca4af023a4148a909dd82c11f81893_72_0.png)

## Example: explained

在上面的 Example: 中，time（20）大于 18，因此条件为 False。因为这样，我们进入 else 条件并打印到屏幕上 "Good evening"。如果时间小于 18，程序将打印 "Good day"。

### 2.13.3 The else if Statement

使用 else if 语句在第一个条件为 False 时指定新的条件。

Syntax

If (condition1)

```
{
    // block of code to be executed if condition1 is True
}
Else if (condition2)
{
    // block of code to be executed if the condition1 is false and condition2 is True
}
Else
{
    // block of code to be executed if the condition1 is false and condition2 is False
}
```

```
using System;
namespace MyApplication
{
    class Program
    {
        static void Main(string[] args)
        {
            int time = 22;
            if (time < 10)
            {
                Console.WriteLine("Good morning.");
            }
            else if (time < 20)
            {
                Console.WriteLine("Good day.");
            }
            else
            {
                Console.WriteLine("Good evening.");
            }
        }
    }
}
```

![](img/e7ca4af023a4148a909dd82c11f81893_73_0.png)

## Example: explained

在上面的 Example: 中，time（22）大于 10，因此第一个条件为 False。else if 语句中的下一个条件也为 False，因此我们进入 else 条件，因为 condition1 和 condition2 均为 False - 并打印到屏幕上 "Good evening"。

然而，如果时间是 14，我们的程序将打印 "Good day。"

## C# Switch Statements

使用 switch 语句选择要执行的多个代码块之一。

## Syntax

```
switch(expression)
{
    case x:
        // code block
        break;
    case y:
        // code block
        break;
```

Default:

```
// code block

break;
}
```

下面的 Example: 使用星期几数字计算星期几名称：

```
using System;

namespace MyApplication
{

class Program
{

static void Main(string[] args)
{

int day = 4;

switch (day)
{

case 1:

Console.WriteLine("Monday");

break;
```

```
case 2:
    Console.WriteLine("Tuesday");
    break;
case 3:
    Console.WriteLine("Wednesday");
    break;
case 4:
    Console.WriteLine("Thursday");
    break;
case 5:
    Console.WriteLine("Friday");
    break;
case 6:
    Console.WriteLine("Saturday");
    break;
case 7:
    Console.WriteLine("Sunday");
    break;
```

```
}
}
}
}
```

![](img/e7ca4af023a4148a909dd82c11f81893_77_0.png)

## 2.14 Loops

循环可以在指定条件达到时执行代码块。循环很有用，因为它们节省时间，减少错误，并使代码更具可读性。

### 2.14.1 C# While Loop

while 循环只要指定条件为 True 就会循环执行代码块：

Syntax

```text
while (condition)
{
    // code block to be executed
}
```

在下面的 Example: 中，只要变量（i）小于 5，循环中的代码就会一遍又一遍地运行：

```csharp
using System;
namespace MyApplication
{
    class Program
    {
        static void Main(string[] args)
        {
            int i = 0;
            while (i < 5)
            {
                Console.WriteLine(i);
                i++;
            }
        }
    }
}
```

![](img/e7ca4af023a4148a909dd82c11f81893_78_0.png)

### 2.14.2 The Do/While Loop

do/while 循环是 while 循环的一个变体。此循环将在检查条件是否为真之前执行一次代码块，然后只要条件为真就重复循环。

Syntax

Do

```text
{
```

语句 1 在执行代码块之前执行一次。

语句 2 定义执行代码块的条件。

语句 3 在执行代码块之后每次执行。

下面的 Example: 将打印数字 0 到 4：

```
using System;
namespace MyApplication
{
class Program
{
static void Main(string[] args)
{
for (int i = 0; i < 5; i++)
{
Console.WriteLine(i);
}
}
}
}
```

![](img/e7ca4af023a4148a909dd82c11f81893_80_0.png)

### 2.14.4 The foreach Loop

还有一个 foreach 循环，专门用于遍历数组中的元素：

Syntax

```
foreach (type variablename in arrayname) {

// code block to be executed}
```
