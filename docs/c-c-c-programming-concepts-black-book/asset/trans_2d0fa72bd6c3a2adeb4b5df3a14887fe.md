
在代码清单 19.39 中，我们使用 All() 方法检查了整数数组中的所有元素是否都能被 5 整除。接着，我们使用 Any() 方法检查了数组中是否有任一元素能被 3 整除。最后，我们使用 Contains() 方法检查了数组中是否存在 8。由于数组不包含 8，此操作将返回 false。程序的输出如下：

```text
The result of using All operator is True
The result of using Any operator is True
The result of checking the existence of 8 is False
```

现在让我们学习 C# 中的错误处理。

## 错误处理

当我们执行代码时，可能会由于某些数据错误导致代码失败，并且正在进行的进程的执行会在运行时停止。为了在运行时处理这种异常情况，C# 提供了一种内置支持机制，称为异常处理。异常是代码在运行时的一种非预期行为，会导致执行过程终止。因此，我们需要确保代码在运行时不会失败。与其反复检查代码中的错误，不如使用 C# 提供的 try-catch 机制来处理异常。

在 try-catch 机制中，可能在运行时产生错误的代码位于 try 块内，当错误发生时，错误会在 catch 块中处理。代码清单 19.40 展示了 try-catch 块的结构：

### 代码清单 19.40：展示 try-catch 块的结构

```csharp
using System;
class Program
{
    public static void Main()
    {
        try
        {
            //write the code block that may generate an error
        }
        catch (Exception A)
        {
            //Handle the exception
        }
    }
}
```

我们也可以为单个 try 块定义多个 catch 块。请注意，将多个 catch 块按从特定类型到泛型类型的顺序排列是一种良好实践。代码清单 19.41 展示了一个带有多个 catch 块的 try 块：

### 代码清单 19.41：展示 try-catch 块的另一种结构

```csharp
using System;
class Program
{
    public static void Main()
    {
        try
        {
            //write the code block that may generate an error
        }
        catch (ApplicationException aEx)
        {
            //Handle the application exceptions
        }
        catch (Exception ex)
        {
            //Handle the generic exceptions
        }
    }
}
```

除 try-catch 块之外，C# 还提供了 finally 块，无论 try 块如何退出，该块都会执行。因此，当控制流到达执行末尾时，finally 块会执行。此外，即使在 catch 块中处理了错误之后，finally 块也会执行。finally 块主要用于：

- 避免语句重复。
- 在异常处理后释放资源。例如，如果在处理来自数据库的数据时发生异常，那么 *finally* 块可以包含终止数据库连接的代码。
- 为对象赋值。
- 显示对用户有用的消息。

当我们希望专注于代码性能时，编写 finally 块是一种良好实践。代码清单 19.42 展示了 try-catch-finally 块的结构。

### 代码清单 19.42：展示 try-catch-finally 块的结构

```csharp
using System;

class Program
{
    public static void Main()
    {
        try
        {
            //write the code block that may generate an error
        }
        catch (Exception ex)
        {
            //Handle the exceptions
        }
        finally
        {
            //write the finally statement
        }
    }
}
```

现在，让我们编写一小段 C# 代码来理解 try-catch 块的用法。代码清单 19.43 展示了说明异常发生时程序行为的代码片段：

### 代码清单 19.43：展示 try-catch 块的实现

```csharp
using System;

class Program
{
    public static void Main()
    {
        try
        {
            Console.WriteLine("Enter the first number:");
            int num1 = Convert.ToInt32(Console.ReadLine());

            Console.WriteLine("Enter the second number:");
            int num2 = Convert.ToInt32(Console.ReadLine());
            int div = num1 / num2;
            Console.WriteLine("The result of division is {0}", div);
        }
        catch (Exception ex)
        {
            Console.WriteLine("Exception occurred!!!");
            Console.WriteLine(ex.Message);
        }
    }
}
```

前面的程序接受两个整数 num1 和 num2。程序的输出如下：

```text
Enter the first number:
5
Enter the second number:
0
Exception occurred!!!
Attempted to divide by zero.
```

我们将第一个整数设为 5，第二个整数设为 0。用 5 除以 0 时，编译器会抛出异常，因为 5 不能被 0 除。因此，当 try 块中发生异常时，程序的控制权会转移到 catch 块。

现在，让我们总结本章讨论的要点。

## 小结

在本章中，我们几乎涉及了 LINQ 的各个方面。首先，我们学习了 LINQ 及其在 .NET 架构中的需求。然后，我们讨论了匿名方法和 lambda 表达式。接着，我们学习了综合查询、lambda 查询以及延迟执行和立即执行。我们还学习了 LINQ to Object、LINQ to XML 和 LINQ to ADO.NET。此外，本章讨论了 LINQ 中的表达式树。接下来，讨论了筛选运算符、投影运算符、联接运算符、分组运算符、集合运算符、转换运算符、分区运算符、相等运算符、元素运算符、聚合运算符和量词运算符。最后，我们学习了使用 try-catch-finally 块进行异常处理。

## 快速复习

### 多项选择题

- Q1. LINQ 是以下哪项的缩写
    - i. 线性集成查询
    - ii. 线性积分查询
    - iii. 语言集成查询
    - iv. 语言积分查询
- **Q2.** 说出 LINQ to SQL 中使用的文件扩展名。
    - 1. `.aspx`
    - 2. `.dbmx`
    - 3. `.ascx`
    - 4. `.dbml`
- **Q3.** LINQ to XML 中使用的命名空间是：
    - 1. `System.LINQ`
    - 2. `System.XML.XLinq`
    - 3. `System.XML`
    - 4. `System.LINQ.XLinq`
- **Q4.** 从以下表达式中选择 Lambda 表达式。
    - 1. `i * i`
    - 2. `i == i * i`
    - 3. `i => i * i`
    - 4. `i / j`
- **Q5.** 延迟执行可以通过使用以下哪种方式实现：
    - 1. while 循环
    - 2. for 循环
    - 3. foreach 循环
    - 4. do-while 循环
- **Q6.** 表达式树被赋给以下哪种类型的变量：
    - 1. `Delegate<T>`
    - 2. `Expression<Delegate<T>>`
    - 3. `Expression<T>`
    - 4. 以上都不是
- **Q7.** 负责提供标准运算符的命名空间是：
    - 1. `System.Query`
    - 2. `System.Query.Sequence`
    - 3. `System`
    - 4. 以上都不是
- **Q8.** 以下哪些是合适的量词？
    - 1. All、Any
    - 2. All、any、Equal
    - 3. All
    - 4. All、Any、Equal
- Q9. 元素运算符用于：
    - i. 从集合中获取元素的位置
    - ii. 从集合中获取元素
    - iii. 获取指定位置处元素的值
    - iv. 以上都是
- Q10. Single() 方法：
    - i. 用于从集合中获取单个值
    - ii. 用于在集合包含单个元素时获取该值
    - iii. 如果集合为 null，将抛出异常
    - iv. 以上都是

### 主观题

- **Q1.** 什么是 lambda 表达式？请用合适的示例进行解释。
- **Q2.** 定义匿名方法和匿名变量。
- **Q3.** 编写一个 LINQ 程序，从数字集合中显示能被 5 整除的任意数字。[使用数组 [15, 16, 17, 18, 19, 20, 31, 35]]
- **Q4.** 修改上一个程序，以显示能被 5 整除的数字的计数。
- **Q5.** 使用分区运算符和前面的数组显示 20 到 40 之间的数字。
- **Q6.** 定义一个类 Product，它具有以下属性：
    - i. Product_ID
    - ii. Product_Name
    - iii. Product_Expiry
    - iv. Product_Price

    创建 Product 类型对象的列表，运行以下查询，并在控制台上显示结果：
    - 查询 1：显示到期日期为 '01-01-2015' 的产品列表
    - 查询 2：按价格显示产品分组
    - 查询 3：按价格值升序显示产品
- **Q7.** 编写代码以获取以下 lambda 表达式的表达式树：i => i * 5 >= 500

