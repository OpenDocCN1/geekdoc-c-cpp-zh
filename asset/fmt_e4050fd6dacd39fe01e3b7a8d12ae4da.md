
```cs
Console.WriteLine("The Number {0} is Found.", myNumber);
Finish:
Console.WriteLine("End of search.");
Console.write("\nENTER to quit...");
Console.ReadLine();
```

在列表 3.11 中，我们创建了一个名为 `myArray` 的二维数组，其中包含了从 1 到 400 的数字。接下来，我们创建了接收运行时输入的 `Variable`。根据循环在 `myArray` 中搜索用户输入的数字。如果从数组中找到该数字，`goto` 语句将跳转到 `Found` 标签。然而，如果没有找到输入的数字，`goto` 语句将跳转到 `Finish` 标签。

图 3.13 显示了列表 3.11 的输出：

![](img/17af790174c480761404624aeed9b30b_180_0.png)

图 3.13：MyLabeledStatement 程序的输出

# 跳出循环

在程序中使用循环时，有时你需要在不完成循环内任务的情况下跳出循环。你可以通过以下三种方法之一跳出循环：

- 使用 `break` 语句立即终止循环
- 使用次要条件，例如使用跳转到标签的 `goto` 语句来打破循环
- 通过处理所需的元素数量或更改变量状态来终止循环

让我们创建一个名为 `MyBreakLoop` 的控制台程序，展示跳出循环的三种不同方法。列表 3.12 显示了 `MyBreakLoop` 的代码：

```cs
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace MyBreakLoop
{
    class Program
    {
        static void Main(string[] args)
        {
            bool done = false;
            Console.WriteLine("Loop 1:");
            for (int i = 0; i < 5; i++)
            {
                Console.WriteLine(i);
                if (i == 3)
                {
                    break;
                }
            }

            Console.WriteLine("Loop 2:");
            int counter = 0;
            do
            {
                Console.WriteLine(counter);
                counter++;
                if (counter == 5)
                {
                    goto handle_done;
                }
            } while (false);

            Console.WriteLine("Loop 3:");
            for (int i = 0; i < 5; i++)
            {
                Console.WriteLine(i);
                if (i == 2)
                {
                    done = true;
                    break;
                }
            }

            handle_done:
            Console.WriteLine("End of search.");
        }
    }
}
```

# 使用 continue 语句

`continue` 语句用于将程序控制转移到循环的开头。它持续转移程序控制直到某个条件满足。让我们创建一个名为 `MyContinueStatement` 的控制台程序来展示 `continue` 的使用。列表 3.13 显示了 `MyContinueStatement` 程序的代码：

列表 3.13：MyContinueStatement 程序的代码

```cs
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace MyContinueStatement
{
    class Program
    {
        static void Main(string[] args)
        {
            int number = 1;
            while (true)
            {
                Console.WriteLine(number);
                number++;
                if (number <= 10)
                {
                    continue;
                }
                else
                {
                    break;
                }
                Console.WriteLine("Series is broken at number: " + number);
                Console.WriteLine("PRESS ENTER to quit...");
                Console.ReadLine();
            }
        }
    }
}
```

在列表 3.13 中，`while` 循环在条件为真时一直执行。在循环内部，如果语句检查输入的数字是否小于 10，则将程序控制转移到 `continue` 语句。`continue` 语句反过来在条件满足时将程序控制转移到循环的开头。如果条件失败，程序控制转移到 `else` 块并打破循环。

# 处理异常

异常处理是 C# 错误处理的核心。假设你正在创建一个除以两个数字的程序，你希望程序不会被异常异常终止。为了确保这一点，你必须在运行之前就处理可能导致异常终止的异常。

# 第 3 章：C# 5.0 程序中的流程控制与异常处理

程序。让我们创建一个名为 `MyException` 的控制台应用程序，展示如何处理异常。列表 3.14 显示了 `MyException` 程序的代码：

列表 3.14：MyException 程序的代码

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace MyException
{
    class Program
    {
        static void Main(string[] args)
        {
            int number = 0;
            int div = 0;
            try {
                div = 100 / number;
            } catch (DivideByZeroException)
            {
                Console.WriteLine("Exception Occured");
                Console.WriteLine("Result is " + div);
                Console.Write("\nPress ENTER to quit...");
                Console.ReadLine();
            }
        }
    }
}
```

在列表 3.14 中，你可以看到两个块——`try` 和 `catch`。在 `try` 块中，给出了两个数除法的逻辑，而 `catch` 块则处理可能发生的异常。

图 3.16 显示了列表 3.14 的输出：

![](img/17af790174c480761404624aeed9b30b_183_0.png)

图 3.16：MyException程序的输出

图 3.16 显示，当 100 除以 0 时，会发生 `DivideByZeroException`；因此，程序控制转移到 `catch` 块，并在 `catch` 内部显示结果。

# 抛出异常

你可以使用 `throw` 语句来抛出自定义异常。`throw` 语句只需要一个参数来抛出异常。当遇到 `throw` 语句时，程序将终止。让我们创建一个名为 `MyThrowException` 的控制台应用程序，展示如何处理异常。列表 3.15 显示了 `MyThrowException` 程序的代码：

列表 3.15：MyThrowException 程序的代码

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace MyThrowException
{
    class Program
```

# 立即解决方案

```csharp
{
    static void Main(string[] args)
    {
        int number;
        Console.Write("Enter a Number:");
        number = int.Parse(Console.ReadLine());
        try
        {
            if (number > 10)
                throw new Exception("Maximum Limit is 10");
        }
        catch (Exception e)
        {
            Console.WriteLine("Exception has been Occured");
        }
        finally{
            Console.WriteLine("This is the Last Statement");
            Console.WriteLine("\npress ENTER to quit...");
            Console.ReadLine();
        }
    }
}
```

在 3.15 中，你可以看到在 `try` 块中，`if` 语句检查变量的值是否大于 10。如果条件失败，就会抛出一个新异常“Maximum Limit is 10”。

图 3.17 显示了 3.15 的输出：

![](img/17af790174c480761404624aeed9b30b_184_0.png)

图 3.17：MyThrowException程序的输出

在 3.15 中，你可以看到抛出了自定义异常。每当输入数字超过 10 时，就会引发异常，然后在 `catch` 块中被捕获。

# 使用 checked 和 unchecked 语句

正如深度解析部分所讨论的，`checked` 和 `unchecked` 语句用于检查内存溢出异常。让我们创建一个名为 `CheckOverflow` 的控制台应用程序展示 `checked` 和 `unchecked` 语句的使用。列表 3.16 显示了 `CheckOverflow` 程序的代码：

列表 3.16：CheckOverflow 程序的代码

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace CheckOverflow
{
    class Program
    {
        static void Main(string[] args)
        {
            byte number1,number2;
            byte result;
            number1 = 127;
            number2 = 127;

            try {
                result = unchecked((byte)(number1 * number2));
                Console.WriteLine("unchecked result: " + result);
                
                result = checked((byte)(number1 * number2));
                Console.WriteLine("checked result: " + result);
            } catch (OverflowException exception) {
                Console.WriteLine(exception);
            } finally {
                Console.Write("\nPress ENTER to quit...");
                Console.ReadLine();
            }
        }
    }
}
```

在列表 3.16 中，你可以看到有两个字节型变量 `number1` 和 `number2`，并给它们都赋值为 127。在 `try` 块中，两个变量的乘积存储在另一个字节型变量 `result` 中。由于 `number1` 和 `number2` 中存储值的相积超过了 `result` 变量可以存储的值限制，因此发生了异常。在这种情况下，`checked` 语句捕获了溢出异常并显示异常，但 `unchecked` 语句没有引起任何异常并显示了结果。

图 3.18 显示了列表 3.16 的输出。

![](img/17af790174c480761404624aeed9b30b_185_0.png)

图 3.18：CheckOverflow程序的输出

# 总结

在本章中，你学习了流程控制语句，例如选择语句、迭代语句和跳转语句。你还学习了程序执行期间可能引发各种异常以及处理它们的方法。此外，你学习了 `checked` 和 `unchecked` 语句。这些语句都通过“立即解决方案”部分进行了解释。

在下一章中，你将学习命名空间（`namespaces`）、类（`classes`）和结构体（`structs`）。

# 命名空间、类和结构体

如果你需要以下内容的解决方案，请参：

| | |

| --- | --- |

| 创建命名空间 | 162 |

| 向命名空间添加引用 | 163 |

| 通过 using 指令访问预命名空间 | 165 |

| 创建类 | 166 |

| 声明部分类 | 167 |

| 创建对象 | 167 |

| 使用 this 关键字 | 169 |

| 创建对象数组 | 170 |

| 使用带参数的方法 | 172 |

| 使用带参数的方法 | 173 |

| 向方法传递引用 | 174 |

| 将对象作为参数传递给方法 | 175 |

| 从方法返回值 | 177 |

| 创建部分方法 | 177 |

| 在类中使用参数构造函数 | 179 |

| 创建拷贝构造函数 | 179 |

| 调用类的析构函数 | 181 |

| 创建静态类 | 181 |

| 在类中使用静态方法 | 182 |

| 使用属性赋值并获取值 | 183 |

![](img/17af790174c480761404624aeed9b30b_186_0.png)

| 如果你需要以下内容的解决方案，请参： |

| --- | --- |

| 使用对象初始化器 | 184 |

| 使用只读属性获取值 | 185 |

| 创建静态属性 | 186 |

| 创建匿名类型 | 187 |

| 使用索引器 | 188 |

| 使用字符串索引器 | 189 |

| 使用嵌套类 | 190 |

| 使用结构体 | 191 |

## 深度解析

C# 是一种平台无关语言，这意味着它可以与任何编程语言兼容。C# 语言提供了丰富的功能和强大的结构，允许你用极少的代码快速方便地创建应用程序。编程的最基本方面涉及使用：

- 命名空间：允许在通用名称下对类、对象和函数进行分组
- 类：代表包含数据成员（如常量和字段）、函数成员（如方法、属性和事件）以及嵌套类型的数据结构
- 对象：代表允许访问类成员（如字段、方法和属性）的构建块
- 结构体：代表可以包含数据成员的数据结构

在本章中，你探索了 C# 的一些新特性，并尝试比较它与 C++、Java 等语言的差异。章节探讨了命名空间的概念以及如何在 C# 程序中使用它们。接下来，你将探索类和对象的概念。最后，章节讨论了如何使用不同的访问修符使用它们。

让我们从讨论命名空间开始本章。

# 探索命名空间

命名空间的概念对 C# 来说并不新，因为它在 C++ 和 Java 中已经得到了扩展。命名空间是一个包装在一个或多个结构元素外的封装器，使其唯一化并与其他元素区分来。以下代码片段显示了命名空间的示例：

```csharp
public class Corp {
    enum Corp {
}
```
