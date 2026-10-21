

- 将 `catch (Exception e)` 放在其他 catch 块之前。
- 将捕获超类对象的 catch 放在捕获其子类对象的 catch 之前。
- 将通用 catch 处理程序 `catch` 放在其他 catch 块之前。
- 创建用户定义的异常类时，忘记实现 `System.Exception` 类的全部三个构造函数。
- 在可能导致溢出的操作上忘记使用 `checked` 运算符。
- 在 catch 处理程序中拼写异常类名称错误。

## 复习题

18.1 判断下列说法是否正确。
（a）语法错误会被编译器捕获并提示。
（b）运行时错误总会终止程序的执行。
（c）异常是由语法错误引起的。
（d）异常处理程序用于纠正运行时错误。
（e）catch 块可以放在程序中的任何位置。
（f）try 块通常包围包含运行时错误的代码块。
（g）catch 块不一定必须包含任何语句。
（h）使用多个 catch 语句时，C# 允许它们以任意顺序排列。
（i）无参数 catch 语句必须放在所有 catch 处理程序的末尾。
（j）try 块后面必须始终跟一个 catch 块。
（k）finally 块可用于处理 try 块生成的任何异常。
（l）`checked` 运算符用于检查语法错误。

18.2 什么是调试？解释其在软件开发生命周期中的重要性。

18.3 什么是编译时错误？举一些例子。它们是如何被检测到的？

18.4 什么是运行时错误？举一些例子。它们是如何被检测到的？

18.5 什么是异常？举一些例子。

18.6 如何编写代码来区别处理各种异常？

18.7 为什么有必要用专门的代码来处理异常？

18.8 描述处理异常所涉及的任务。

18.9 我们如何定义以下内容？
（a）try 块
（b）catch 块
（c）finally 块

18.10 列出 C# 程序中至少四种常见的异常。

18.11 当一个 try 块后面既没有 catch 块，也没有 finally 块时，会发生什么？

18.12 区分无参数 catch 语句和 `catch(Exception e)` 语句。

18.13 如何实现一个可能引发类型未知异常的方法？

18.14 什么是 finally 语句？它有什么用途？

18.15 使用 finally 块的目的是什么？举一些例子。

18.16 当异常发生在一个嵌套的 try 块的内部 try 块中时，会发生什么？

18.17 在什么情况下你认为有必要定义自己的异常类？

18.18 我们什么时候使用无参数 catch 处理程序？

18.19 解释异常处理机制如何用于调试程序。

18.20 为什么在 C# 中必须对 catch 块进行正确排序？

18.21 说明在以下情况下会发生什么：
- （a）异常在 try 块之外被抛出
- （b）没有 catch 处理程序与抛出的异常类型匹配
- （c）多个处理程序与抛出的异常类型匹配
- （d）catch 处理程序抛出一个异常
- （e）catch 是多个 catch 处理程序中的第一个

18.22 找出以下代码段中的错误（如果有）：
- （a）try
{
    byte m = 1000 * 5000;
    goto catch;
}

- （b）try
{
    byte m = checked (1000 * 2000);
}
catch (FormatException e)
{
    ....
}

- （c）try {...}
catch (Exception e) {...}
catch (ArithmeticException e) {...}
finally {}

- （d）try {...}
finally {...}
catch {...}

- （e）try {...}
catch (DividebyzeroException e)
{...}
finally {...}

# 调试练习

18.1 给定的程序能否编译？如果不能，为什么？

```
using System;
using System.Collections.Generic;
using System.Text;
namespace debigApp1_chap18
{
class Program
{
static void Main(string[] args)
{
```

```
Console.WriteLine("This display is from the Main function.");
Program pp = new Program();
pp.show();
Console.WriteLine("Exit from the Main function.");

public void show()
{
    Console.WriteLine("Showing message from the Show function.");
}
public void check()
{
    Console.WriteLine("Entering Check function.");
    try
    {
        Console.WriteLine("Entering try block of check function.");
        Console.WriteLine("Exiting from try block.");
    }
    catch
    {
        Console.WriteLine("Exception caught and handled!");
    }
    catch (NullReferenceException ex)
    {
        Console.WriteLine(ex.Message);
    }
    Console.WriteLine("Exiting from Check function.");
}
```

18.2 修正给定程序中的语法错误，以演示 finally 关键字。

```
using System;
using System.Collections.Generic;
using System.Text;

namespace debigApp1_chap18
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("This display is from the Main function.");
            Program pp = new Program();
            pp.show();
            Console.WriteLine("Exit from the Main function.");
        }
        public void show()
        {
            Console.WriteLine("Showing message from the Show function.");
        }
    }
```

```
private void CHECK()
{
    try
    {
        Console.WriteLine("Entering try block of check function.");
    }
    catch
    {
        Console.WriteLine("This is finally block.");
    }
    catch
    {
        Console.WriteLine("Exception caught and handled!");
    }
}
```

# 18.3 找出以下程序中的错误。

```
using System;
using System.Collections.Generic;
using System.Text;
namespace debugApp3.chap18
{
    class Program
    {
        static void Main(string[] args)
        {
            string name = "";
            string address = "";
            int age = 0;
            Console.WriteLine("This is another example of try catch block.");
            Console.Write("Please enter your name : ");
            name = Console.ReadLine();
            Console.Write("Please enter your address : ");
            address = Console.ReadLine();
            Console.Write("Please enter your age : ");
            {
                age = Console.ReadLine();
                Console.WriteLine("Hello {0}. You live in {1} and you are {2} years old.", name, address, age);
            }
            catch (FormatException e)
            {
                Console.WriteLine("Age is a number." + e.Message);
            }
        }
    }
}
```

```
catch
{
    Console.WriteLine("error");
}
}
finally
{
    Console.WriteLine("Press any key to exit.");
}

}
```

# 编程练习

- 18.1 开发一个包含可能异常的程序。使用 try 块抛出异常，并使用 catch 块正确处理它。
- 18.2 编写一个程序，演示多个 catch 处理程序的应用。
- 18.3 编写一个程序，抛出一个“数组索引越界”类型的异常，然后适当地处理它。
- 18.4 编写一个程序，有效处理 `ArgumentException` 类型的异常。
- 18.5 开发一个可能抛出多个异常的程序，这些异常使用 catch 和 finally 块处理。
- 18.6 定义一个对整数数组进行排序的方法。为“索引越界”情况加入异常处理机制。
编写一个使用此方法对给定整数集进行排序的 Main 程序。
- 18.7 修改练习 18.6 的程序，将异常处理机制并入调用该方法的 Main 程序中。
- 18.8 编写一个程序，调用一个包含异常的深度嵌套方法。加入必要的异常处理机制。
- 18.9 定义一个名为 `NoMatchException` 的异常，当字符串不等于 `"India"` 时抛出该异常。编写一个使用此异常的程序。
- 18.10 编写一个程序，从键盘读取姓名并显示在屏幕上。当姓名长度超过 15 个字符时，程序应抛出异常。设计你自己的异常机制。

