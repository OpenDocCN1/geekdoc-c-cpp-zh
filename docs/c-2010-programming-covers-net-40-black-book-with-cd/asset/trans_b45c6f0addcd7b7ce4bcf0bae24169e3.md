

## 使用带参数的方法

参数提供了一种将值传递给方法的方式。在 C# 中，你可以通过四种不同的方式将参数传递给方法：按值传递、使用 ref 关键字、使用 out 关键字以及使用 params 关键字。未声明任何修饰符的参数是值参数。现在，创建一个名为 MyMethodParameters 的新控制台应用程序（也在 CD 上提供）。用清单 4.8 所示的代码替换该应用程序的 Program.cs 文件的默认代码：

### 清单 4.8：显示 MyMethodParameters 应用程序的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace MyMethodParameters
{
    class Program
    {
        static void Main(string[] args)
        {
            Amount Amt = new Amount();
            Amt.Balance(12000, 2000);
            Amt.GetData();
            Console.Write("\nPress ENTER to quit..");
            Console.ReadLine();
        }
    }
    public class Amount
    {
        double BalanceAmount;
        public void Balance(double TotalAmount, double Deductions)
        {
            BalanceAmount = TotalAmount - Deductions;
            Console.WriteLine("Your Current Amount is Rs: " + BalanceAmount);
        }
        public void Debit()
        {
            int DebitAmount = 0;
            Console.Write("Enter Amount:");
            DebitAmount = int.Parse(Console.ReadLine());
            BalanceAmount = BalanceAmount - DebitAmount;
            Console.WriteLine("Your Balance Amount is Rs.:" + BalanceAmount);
        }
        public void Credit()
        {
            int CreditAmount = 0;
            Console.Write("Enter Amount:");
            CreditAmount = int.Parse(Console.ReadLine());
            BalanceAmount = BalanceAmount + CreditAmount;
            Console.WriteLine("Your Balance Amount is Rs.:" + BalanceAmount);
        }
        public void GetData()
        {
            char Data;
            Console.WriteLine("----------------------------------------");
            Console.Write("Press (d) for Debit and (c) for Credit:");
            Data = char.Parse(Console.ReadLine());
            if (Data == 'd')
            {
                Debit();
            }
            if (Data == 'c')
            {
                Credit();
            }
        }
    }
}
```

在清单 4.8 中，Amount 类的 Balance 方法有两个参数，TotalAmount 和 Deductions。这些参数的类型为 double，分别被赋值为 12000 和 2000。

图 4.10 显示了 MyMethodParameters 应用程序的输出：

![](img/e073a4882197be4ab61103cbe0bcb394_204_0.png)

图 4.10：显示 MyMethodParameters 应用程序的输出

## 使用带参数的方法

在 C# 中，params 关键字允许你指定一个接受可变数量参数的方法参数。params 关键字必须占据方法形式参数列表的最后一个位置。现在，创建一个名为 MyVariableArguments 的新控制台应用程序（也在 CD 上提供）并用清单 4.9 所示的代码替换该应用程序的 Program.cs 文件的默认代码：

### 清单 4.9：显示 MyVariableArguments 应用程序的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace MyVariableArguments
{
    class Program
    {
        public static int GetSum(params int[] numbers)
        {
            int sum = 0;
            foreach (int num in numbers)
                sum += num;
            return sum;
        }
        public static void Main(string[] args)
        {
            Console.WriteLine("The Sum is:");
            Console.WriteLine(GetSum(1, 2, 3, 4, 5, 6, 7, 8, 9));
            Console.WriteLine(GetSum(2, 4, 6, 8));
            Console.WriteLine("\nPress ENTER to quit..");
            Console.ReadLine();
        }
    }
}
```

清单 4.9 包含一个方法 GetSum，它接受可变数量的参数并打印它们的和。图 4.11 显示了 MyVariableArguments 应用程序的输出：

![](img/e073a4882197be4ab61103cbe0bcb394_205_0.png)

图 4.11：显示 MyVariableArguments 应用程序的输出

## 向方法传递引用参数

与 Java 相比，C++ 的一个重要方面是它能够从给定的函数或方法返回多个值。在 Java 中，函数只返回特定类型的一个值。传递给 Java 类的方法的参数对于简单类型来说是单向的。例如，你不能传递一个整数并让方法修改它。另一方面，C++ 允许你使用两种不同的方法将变量通过引用传递给方法或函数。你可以传递变量的地址并在方法或函数中将其视为指针，或者你可以接受对变量的引用并在方法或函数中修改它。

以下代码片段显示了如何传递引用参数：

```
int PassByPointer( int* x ) {
    *x = 3; }
int main(void) {
    int x = 10;
    PassByPointer(&x);
    // x is now 3 }
```

或者，你也可以按如下代码片段所示传递引用参数：

```
int PassByReference( int& x ) {
    x = 3; }
int main(void) {
    int x = 10;
    PassByReference(x);
    // x is now 3 }
```

这两种方法的弊端是它们可能会突然挂起程序。在第一种方法中，你需要传递一个 NULL 指针。取消引用指针可能会导致程序崩溃。此外，在这两种方法中，数据都在调用方法内部被修改。这可能导致难以追踪的模糊错误。

C# 通过提供 ref 关键字解决了这两个问题。要向方法传递引用类型参数，你需要使用 ref 关键字声明该方法。此外，你必须在方法中传递一个变量并指定你是以引用方式发送它。这样，方法的开发者和使用该方法的程序员都得到了保护。你不能传递 NULL 引用。尝试向引用参数传递 NULL 会导致编译时错误。现在，创建一个名为 MyReferenceArgument 的新控制台应用程序（也在 CD 上提供）并用清单 4.10 所示的代码替换该应用程序的 Program.cs 文件的默认代码：

### 清单 4.10：显示 MyReferenceArgument 应用程序的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace MyReferenceArgument
{
    class Program
    {
        static void Main(string[] args)
        {
            int x = 10;
            Console.WriteLine("Before calling non-ref function, x = {0}", x);
            NonRefFunction(x);
            Console.WriteLine("\nAfter calling non-ref function, x = {0}", x);
            RefFunction(ref x);
            Console.WriteLine("\nAfter calling ref function, x = {0}", x);
            Console.Write("\nPress ENTER to quit.");
            Console.ReadLine();
        }

        static void NonRefFunction(int x)
        {
            Console.WriteLine("Top of NonRefFunction. X = {0}", x);
            x = x + 10;
            Console.WriteLine("Bottom of NonRefFunction. X = {0}", x);
        }

        static void RefFunction(ref int x)
        {
            Console.WriteLine("Top of RefFunction. X = {0}", x);
            x = x + 10;
            Console.WriteLine("Bottom of RefFunction. X = {0}", x);
        }
    }
}
```

在清单 4.10 中，有两行代码被高亮显示。第一行高亮代码是 NonRefFunction 方法的声明，该方法接受一个值参数，如以下代码片段所示：

```
static void NonRefFunction(int x)
{
    Console.WriteLine("Top of NonRefFunction. X = {0}", x);
    x = x + 10;
    Console.WriteLine("Bottom of NonRefFunction. X = {0}", x);
}
```

第二行高亮代码是 RefFunction 方法的声明，该方法接受一个引用参数，如以下代码片段所示：

```
static void RefFunction(ref int x)
{
    Console.WriteLine("Top of RefFunction. X = {0}", x);
    x = x + 10;
    Console.WriteLine("Bottom of RefFunction. X = {0}", x);
}
```

图 4.12 显示了 MyReferenceArgument 应用程序的输出：

```
Before calling non-ref function, x = 10
Top of NonRefFunction. X = 10
Bottom of NonRefFunction. X = 10
After calling non-ref function, x = 10
Top of RefFunction. X = 10
Bottom of RefFunction. X = 20
After calling ref function, x = 20
Press ENTER to quit...
```

## 向方法传递对象作为参数

如前所述，这个关键字指的是类的当前实例。你也可以使用它将对象作为参数传递给另一个类所属的方法。要了解如何将对象作为参数传递给方法，首先创建一个名为 MyObjectArgument 的新控制台应用程序（也在 CD 上提供）并用清单 4.11 所示的代码替换该应用程序的 Program.cs 文件的默认代码：

### 清单 4.11：显示 MyObjectArgument 应用程序的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace MyObjectArgument
{
    class Program
    {
        static void Main(string[] args)
        {
            // your code here
        }
    }
}
```

