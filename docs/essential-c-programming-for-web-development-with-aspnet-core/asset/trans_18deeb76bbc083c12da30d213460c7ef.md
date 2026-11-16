

在此示例中，int 是数据类型，表示变量 age 可以存储整数值（不带小数的完整数字）。

## 为变量赋值

声明变量后，可以使用赋值运算符（=）为其赋值：

```csharp
age = 30;
```

现在，变量 age 存储的值为 30。你也可以在一行中声明并初始化变量：

```csharp
int age = 30;
```

## 变量命名约定

在 C# 中，变量名称必须遵循某些约定：

- 必须以字母或下划线（_）开头。
- 可以包含字母、数字和下划线。
- 区分大小写，这意味着 age 和 Age 被视为不同的变量。
- 建议使用能反映变量用途的描述性名称，使你的代码更易读且更易于维护。

## 数据类型：对数据进行分类

数据类型在编程中起着至关重要的作用，它定义了变量可以存储的值的类型。C# 提供了一组丰富的内置数据类型，每种都针对特定用途设计。让我们探讨一些最常见的类型：

### 1. 数值数据类型

- int（整数）：表示不带小数的整数（例如，-2、0、100）。
- double（双精度浮点数）：表示带小数的数字（例如，3.14、-1.5）。
- float（单精度浮点数）：与 double 类似，但精度较低。
- decimal（十进制浮点数）：为财务计算提供高精度。

### 2. 文本数据类型

- char（字符）：表示单个 Unicode 字符（例如，'A'、'!'、'?'）。
- string（字符串）：表示字符序列（例如，"Hello, world!"）。

### 3. 布尔数据类型

- bool（布尔）：表示逻辑值，可以是 true 或 false。

### 4. 其他数据类型

- DateTime：表示特定的日期和时间。
- object：C# 中所有其他类型的基类。

## 选择合适的数据类型

为变量选择合适的数据类型对于高效使用内存和防止潜在错误至关重要。请考虑你将要处理的数据的性质，并选择最合适的类型。例如，如果你存储一个人的年龄，int 将是一个合理的选择。但是，如果你需要以小数精度存储他们的身高，double 或 float 将更合适。

## 运算符：对数据执行操作

运算符是对变量和值执行操作的符号或关键字。C# 提供了大量运算符，根据其功能分类：

### 1. 算术运算符

- +（加法）
- -（减法）
- *（乘法）
- /（除法）
- %（取模 - 返回除法的余数）

### 2. 赋值运算符

- =（简单赋值）
- +=（相加并赋值）
- -=（相减并赋值）
- *=（相乘并赋值）
- /=（相除并赋值）
- %=（取模并赋值）

### 3. 比较运算符

- ==（等于）
- !=（不等于）
- >（大于）
- <（小于）
- >=（大于或等于）
- <=（小于或等于）

### 4. 逻辑运算符

- &&（逻辑 AND）
- ||（逻辑 OR）
- !（逻辑 NOT）

### 5. 其他运算符

- ++（自增）
- --（自减）
- ?:(条件运算符 - if-else 的简写)

## 运算符优先级

当表达式涉及多个运算符时，C# 遵循特定的优先级顺序来对它们求值。理解此顺序至关重要，以确保你的代码按预期行为。你可以使用括号来覆盖默认优先级并控制求值顺序。

在本章中，我们探讨了 C# 编程的基本构建块：变量、数据类型和运算符。我们学习了如何声明变量、为其赋值，以及为不同场景选择合适的数据类型。我们还深入了解了运算符的世界，发现了如何对数据执行各种操作。掌握这些知识后，你现在已准备好开始使用 ASP.NET Core 3 构建 Web 应用程序的激动人心的旅程。

## 控制流（if、else、switch、循环）

在编程领域，控制流语句使我们能够指导代码的执行，做出决策、重复操作，并以娴熟的方式处理各种场景。C# 提供了一组强大的控制流构造，包括 if、else、switch 和循环，使我们能够创建动态且可适应的程序。在本节中，我们将深入探讨这些构造，揭示其复杂性并演示其实际应用。

## if、else 和 else if：做出决策

if 语句是 C# 中决策的基石。它允许我们仅在满足某个条件时执行一段代码。以下是基本语法：

```csharp
if (condition)
{
    // Code to execute if the condition is true
}
```

让我们通过一个示例来说明：

```csharp
int age = 25;
if (age >= 18)
{
    Console.WriteLine("You are eligible to vote.");
}
```

在此片段中，仅当 `age` 变量的值大于或等于 18 时，`if` 块中的代码才会执行。

我们可以通过加入 `else` 语句来增强决策能力，它在原始条件为假时提供替代的代码路径：

```csharp
if (age >= 18)
{
    Console.WriteLine("You are eligible to vote.");
}
else
{
    Console.WriteLine("You are not yet eligible to vote.");
}
```

现在，如果 `age` 小于 18，`else` 块中的代码将被执行。

对于涉及多个条件的场景，我们可以使用 `else if` 语句：

```csharp
if (age >= 65)
{
    Console.WriteLine("You are eligible for senior citizen benefits.");
}
else if (age >= 18)
{
    Console.WriteLine("You are eligible to vote.");
}
else
{
    Console.WriteLine("You are not yet eligible to vote.");
}
```

在此扩展示例中，我们检查多个年龄范围，并根据条件提供相应的消息。

## switch：处理多个情况

`switch` 语句提供了一种基于表达式值处理多个情况的简洁方法。当你有一系列离散值需要比较时，它特别有用。让我们看看它的实际应用：

```csharp
int dayOfWeek = 3; // Assuming 1 represents Monday, 2 represents Tuesday, and so on
switch (dayOfWeek)
{
    case 1:
        Console.WriteLine("It's Monday.");
        break;
    case 2:
        Console.WriteLine("It's Tuesday.");
        break;
    case 3:
        Console.WriteLine("It's Wednesday.");
        break;
    // ... other cases
    default:
        Console.WriteLine("Invalid day of the week.");
        break;
}
```

在此示例中，switch 语句计算 dayOfWeek 的值并执行相应的 case 块。`break` 语句至关重要，可防止贯穿，确保仅执行预期的代码块。`default` case 充当任何不匹配指定 case 的值的捕获项。

## 循环：重复执行操作

循环对于在编程中执行重复任务不可或缺。C# 提供了几种类型的循环，每种都适用于不同的场景：

### 1. for 循环

for 循环在预先知道迭代次数时非常理想。它由三部分组成：初始化、条件和迭代。

```csharp
for (int i = 0; i < 5; i++)
{
    Console.WriteLine("Iteration: " + i);
}
```

此循环将执行五次，在每个周期中打印迭代编号。

### 2. while 循环

while 循环会在指定条件保持为真时继续执行。

```csharp
int count = 0;
while (count < 10)
{
    Console.WriteLine("Count: " + count);
    count++;
}
```

此循环将递增 count 变量并打印其值，直到其达到 10。

