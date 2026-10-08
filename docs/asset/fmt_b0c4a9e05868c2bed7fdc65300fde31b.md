
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace MyWhileLoop
{
    class Program
    {
        static void Main(string[] args)
        {
            // Example 1
            // 一个简单的 while 循环示例
            Console.WriteLine("Loop 1:");
            int i = 0;
            while (i < 5)
            {
                Console.WriteLine("I = {0}", i);
                i++;
            }
            // Example 2
            // 使用布尔值的 while 循环
            Boolean flag = false;
            i = 0;
            Console.WriteLine("\nLoop 2:");
            // 注意：此处逻辑在原文中似乎不完整，保持结构
            /*
            while (flag)
            {
                if (i > 5)
                {
                    ...
                }
            } */
            // Example 3
            // 一个永远不会执行的循环
            Console.WriteLine("\nLoop 3:");
            while (i <= 0)
            {
            }
        }
    }
}
```

# 第3章：C# 5.0 程序中的流程控制与异常处理

```csharp
{
    Console.WriteLine("I = {0}", i);
    i++;
    Console.Write("PRESS ENTER to quit...");
    Console.ReadLine();
}
```

列表 3.5 包含了三个示例来展示 `while` 循环的使用。第一个示例是一个简单的循环示例。在第二个示例中，`while` 循环根据变量值设置的布尔值进行操作。在第三个示例中，如果 `while` 语句中的指定条件在第一次迭代之前不成立，则 `while` 循环将不会执行。

图 3.7 显示了列表 3.5 的输出。

![](img/17af790174c480761404624aeed9b30b_173_0.png)

图 3.7：`MyWhileLoop` 程序的输出

学习如何使用 `do...while` 循环。

## 使用 do...while 循环

`do...while` 循环的工作原理与 `for` 循环和 `while` 循环非常相似。`do...while` 循环不包含任何初始化语句，也不会自动递增。与 `while` 循环不同，`do...while` 循环在循环结束时检查条件，而不是在开始时。因此，无论给定条件真为假，`do...while` 循环至少都会执行一次。让我们创建一个名为 `MyWhileLoop` 的控制台程序，展示 `do...while` 循环的使用。列表 3.6 显示了 `MyWhileLoop` 程序的代码：

### 列表 3.6：MyWhileLoop 程序的代码

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace MyWhileLoop
{
    class Program
    {
        static void Main(string[] args)
        {
            // 首先是一个简单的计数器 do 循环
            int i = 0;
            do
            {
                Console.WriteLine("Loop 1:");
                Console.WriteLine("I = {0}", i);
                i++;
            } while (i < 5);

            // 接下来是相同的情况，使用布尔值而不是索引
            i = 0;
            bool done = false;
            do
            {
                Console.WriteLine("Loop 2:");
                Console.WriteLine("I = {0}", i);
                i++;
                if (i > 5)
                    done = true;
            } while (!done);

            // 最后是一个为假的条件，以不进入循环
            do
            {
                Console.WriteLine("Loop 3");
                Console.Write("PRESS ENTER to quit...");
                Console.ReadLine();
            } while (false);
        }
    }
}
```

列表 3.6 显示了三个示例来展示 `do...while` 循环的使用。在第一个示例中，`do...while` 循环显示 `i` 的值，直到语句中的条件为真。第二个示例包含一个检查布尔标志的 `do...while` 循环。在第三个示例中，语句中的指定条件为假，但循环仍然执行了。

图 3.8 显示了列表 3.6 的输出：

![](img/17af790174c480761404624aeed9b30b_174_0.png)

图 3.8：`MyWhileLoop` 程序的输出

学习如何使用 `for`。

## 使用 for 循环

`for` 循环允许你创建一个包含初始化、递增/递减和验证循环计数器的循环。`for` 循环可以用于简单的索引，也可以用于涉及数组和元素的复杂循环。C# 有多种 `for` 循环的变体，已在列表 3.7 中所示。

让我们创建一个名为 `MyForLoop` 的控制台程序来学习如何使用 `for`。列表 3.7 显示了 `MyForLoop` 程序的代码：

### 列表 3.7：MyForLoop 程序的代码

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace MyForLoop
{
    class Program
    {
        static void Main(string[] args)
        {
            // 演示一个从 1 数到 5 的简单循环
            for (int i = 0; i < 5; ++i)
                Console.WriteLine("i = {0}", i);

            // 演示在字符串中查找字母
            // 然后一直打印直到遇到空格。
            // 这展示了如何在第二个循环中跳过初始化
            int nPos = 0;
            string s = "this is a test of the emergency system";
            for (nPos = 0; nPos < s.Length; ++nPos)
                if (s[nPos] == 'b')
                    break;
            for (nPos = 0; nPos < s.Length; ++nPos)
                if (s[nPos] == ' ')
                    break;
            Console.WriteLine("\n");

            // 最后，演示如何将 for 循环用于
            // 整数以外的情况以及如何更改计数器
            int state = 0;
            for (double d = 0.0; d < 5.0; d)
            {
                Console.WriteLine("d = {0}", d);
                switch (state)
                {
                    case 0:
                        d += 0.1;
                        break;
                    case 1:
                        d += 0.2;
                        break;
                    case 2:
                        d += 0.5;
                        break;
                }
                state++;
                if (state > 2)
                    state = 0;
            }
            Console.Write("\nPress ENTER to quit...");
            Console.ReadLine();
        }
    }
}
```

在列表 3.7 中，我们使用了四次 `for` 循环。在第一情况下，循环在条件 `i<5` 为真时显示变量 `i` 的值。第二个循环初始化 `nPos` 值为 0，而第三个循环在没有初始化的情况下显示 `nPos` 的值。在最后一个 `for` 循环中，我们使用 `switch` 语句显示了 `d` 的值。

图 3.9 显示了列表 3.7 的输出：

![](img/17af790174c480761404624aeed9b30b_176_0.png)

图 3.9：`MyForLoop` 程序的输出

学习如何使用 `foreach` 循环。

## 使用 foreach 循环

`foreach` 循环允许轻松访问数组的所有元素。为了理解 `foreach` 循环的使用，让我们创建一个程序，在其中你需要首先创建一个数组。创建数组后，你可以使用 `foreach` 循环访问该数组的每个元素。让我们创建一个名为 `MyForLoop` 的控制台程序。列表 3.8 显示了 `MyForLoop` 的代码：

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace MyForLoop
{
    class Program
    {
        static void Main(string[] args)
        {
            string[] bookTitles = new string[] { "Finland", "Iceland", "France", "United States" };

            Console.WriteLine("The available titles are: ");
            foreach (string i in bookTitles)
            {
                Console.WriteLine(i);
            }
            Console.Write("\nPress ENTER to quit...");
            Console.ReadLine();
        }
    }
}
```

```cs
{
  Console.Write("\npress ENTER to quit...");
  Console.ReadLine();
}
```

在列表 3.9 中，我们定义了两个名为 `firstMatrix` 和 `secondMatrix` 的多维数组。我们使用了两个循环（外层和内层）来读取 `firstMatrix` 数组的元素，并使用了两个循环来读取 `secondMatrix` 数组的元素。外层 `for` 循环读取行元素，内层循环读取列元素。

图 3.11 显示了列表 3.9 的输出。

![](img/17af790174c480761404624aeed9b30b_178_0.png)

图 3.11：`MyNestedLoop` 程序的输出

在图 3.11 中，你可以看到输入两个矩阵后，它们的和作为输出显示。

# 创建无限循环

无限循环是一种无法立即终止的循环。当你希望某个语句或一组语句执行无限次时，可以使用无限循环。在无限循环中，你可能需要指定一个终止条件。让我们创建一个名为 `MyInfiniteLoop` 的控制台应用程序。列表 3.10 显示了 `MyInfiniteLoop` 程序的代码。

### 列表 3.10：MyInfiniteLoop 程序的代码：

```cs
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace MyInfiniteLoop
{
    class Program
    {
        static void Main(string[] args)
        {
            int counter;
            for (counter = 0 ; counter++)
            {
                Console.WriteLine("I Stuck in a Loop");
            }
        }
    }
}
```

在列表 3.10 中，我们没有在 `for` 循环中指定任何条件；因此，它将无限执行。

# 第 3 章：C# 5.0 程序中的流程控制与异常处理

图 3.12 显示了列表 3.10 的输出。

![](img/17af790174c480761404624aeed9b30b_179_0.png)

图 3.12：`MyInfiniteLoop` 程序的输出

图 3.12 显示了 `I Stuck in a loop` 的无限次输出。

# 使用 goto 语句

`goto` 语句允许程序控制从一个点转移到另一个点。程序控制的转移基于带标签的语句。让我们创建一个名为 `MyLabeledStatement` 的控制台程序来展示 `goto` 语句的使用。列表 3.11 显示了 `MyLabeledStatement` 程序的代码：

### 列表 3.11：MyLabeledStatement 程序的代码

```cs
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace MyLabeledStatement
{
    class Program
{
        static void Main(string[] args)
        {
            int x = 100, y = 4;
            int count = 0;
            string[,] myArray = new string[x,y];
            // 初始化数组
            for (int i = 0; i < x; i++)
                for (int j = 0; j < y; j++)
                    myArray[i, j] = (++count).ToString();

            // 读取输入；
            Console.Write("Enter the Number to Search for:");
            string myNumber = Console.ReadLine();

            // 搜索；
            for (int i = 0; i < x; i++)
                for (int j = 0; j < y; j++)
                    if (myArray[i, j].Equals(myNumber))
                        goto Found;

            Console.WriteLine("The Number {0} was not Found.", myNumber);

        Found:
        }
}
```

# 立即解决方案

`goto` `Finish;`

`Found:`
