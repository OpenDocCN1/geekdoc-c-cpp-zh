
```
num2 = int.Parse(Console.ReadLine());
    result = num1 / num2;
    Console.WriteLine("The result of {0}/{1} is {2}",
        num1, num2, result);
}
catch (DivideByZeroException ex)
{
    Console.WriteLine(ex.Message);
}
    Console.ReadLine();
}
```

如果发生除零异常（为 num2 输入 0），异常将被捕获。然而，如果为 num1 或 num2 输入字母字符，则会引发 FormatException 异常。由于你只捕获了 DivideByZeroException 异常，因此该异常未被处理并导致运行时错误。

## 处理多个异常

为了处理不同类型的异常，你可以在 try-catch 语句中设置一个或多个 catch 块。以下示例展示了如何捕获三种不同的异常：

- DivideByZeroException — 在尝试将整数或十进制值除以零时抛出。
- FormatException — 当参数的格式不符合被调用方法的参数规范时抛出。
- Exception — 表示应用程序执行期间发生的错误。

此示例处理这三种不同的异常，然后打印出自定义错误消息：

```
static void Main(string[] args)
{
    int num1, num2, result;
    try
    {
        Console.Write("Please enter the first number:");
        num1 = int.Parse(Console.ReadLine());

        Console.Write("Please enter the second number:");
        num2 = int.Parse(Console.ReadLine());

        result = num1 / num2;
        Console.WriteLine("The result of {0}/{1} is {2}",
            num1, num2, result);
    }
    catch (DivideByZeroException ex)
    {
        Console.WriteLine("Division by zero error.");
    }
```

## 第 I 部分：C# 基础

(继续)

```
catch (FormatException ex)
{
    Console.WriteLine("Input error.");
}
catch (Exception ex)
{
    Console.WriteLine(ex.Message);
}
Console.ReadLine();
```

在此程序中，为 num1 输入数值而为 num2 输入字母字符会产生 FormatException 异常，该异常会被捕获并显示如下？

```
Please enter the first number:6
Please enter the second number:a
Input error.
```

为第二个数字输入 0 会抛出 DivideByZeroException 异常，该异常会被捕获并显示不同的错误消息：

```
Please enter the first number:7
Please enter the second number:0
Division by zero error.
```

到目前为止，所有语句都位于 Main() 函数中。如果有一个名为 PerformDivision() 的函数来除两个数字并返回结果，会发生什么情况，如下所示？

```
class Program
{
    static void Main(string[] args)
    {
        int num1, num2;
        try
        {
            Console.Write("Please enter the first number:");
            num1 = int.Parse(Console.ReadLine());

            Console.Write("Please enter the second number:");
            num2 = int.Parse(Console.ReadLine());

            Program myApp = new Program();

            Console.WriteLine("The result of {0}/{1} is {2}",
                num1, num2,
                myApp.PerformDivision(num1, num2));
        }
        catch (DivideByZeroException ex)
        {
            Console.WriteLine("Division by zero error.");
        }
        catch (FormatException ex)
        {
            Console.WriteLine("Input error.");
        }
        catch (Exception ex)
        {
            Console.WriteLine(ex.Message);
        }
        Console.ReadLine();
    }
}
```

```
private int PerformDivision(int num1, int num2)
{
    return num1 / num2;
}
```

如果 num2 为零，则会在 PerformDivision() 函数内部引发异常。你可以在 PerformDivision() 函数中捕获该异常，也可以在调用函数中捕获该异常——本例中为 Main()。当在 PerformDivision() 函数内部引发异常时，系统会搜索该函数是否存在用于该异常的 catch 块。如果未找到，则异常会沿调用栈向上传递并由调用函数处理。如果调用函数中没有 try-catch 块，则异常会继续沿调用栈向上传递，直到被处理为止。如果调用栈中不再有帧，则默认异常处理器会处理该异常，你的程序会出现运行时错误。

## 使用 throw 语句抛出异常

而不是等待系统遇到错误并引发异常，你可以通过抛出异常以编程方式引发异常。请考虑以下示例：

```
private int PerformDivision(int num1, int num2)
{
    if (num1 == 0) throw new ArithmeticException();
    if (num2 == 0) throw new DivideByZeroException();
    return num1 / num2;
}
```

在此程序中，当 num1 为零时，PerformDivision() 函数会抛出 ArithmeticException 异常；当 num2 为零时，它会抛出 DivideByZeroException 异常。由于 PerformDivision() 中没有 catch 块，因此异常由调用的 Main() 函数处理。在 Main() 中，你可以像这样捕获 ArithmeticException 异常：

```
class Program
{
    static void Main(string[] args)
    {
        int num1, num2, result;
        try
        {
            Console.Write("Please enter the first number:");
            num1 = int.Parse(Console.ReadLine());
            Console.Write("Please enter the second number:");
            num2 = int.Parse(Console.ReadLine());

            Program myApp = new Program();

            Console.WriteLine("The result of {0}/{1} is {2}", num1, num2, myApp.PerformDivision(num1, num2));
        }
        catch (ArithmeticException ex)
        {
            Console.WriteLine("Numerator cannot be zero.");
        }
        catch (DivideByZeroException ex)
        {
            Console.WriteLine("Division by zero error.");
        }
        catch (FormatException ex)
        {
            Console.WriteLine("Input error");
        }
        catch (Exception ex)
        {
            Console.WriteLine(ex.Message);
        }
        Console.ReadLine();
    }

    private int PerformDivision(int num1, int num2)
    {
        if (num1 == 0) throw new ArithmeticException();
        if (num2 == 0) throw new DivideByZeroException();
        return num1 / num2;
    }
}
```

关于多个 catch 块的放置，有一个有趣的地方是，你应先放置要捕获的所有特定异常，然后再放置通用异常。由于 Exception 类是所有异常类的基类，因此它应始终放在 catch 块的最后，以便未在之前的 catch 块中捕获的任何异常都能被捕获。在此示例中，当 ArithmeticException 异常放在 DivideByZeroException 异常之前时，IntelliSense 会显示错误（参见图 12-3）。

![](img/a977a875c7c627b45d939729705a252e_407_0.png)

## 图 12-3

这是因为 DivideByZeroException 是从 ArithmeticException 类派生的，所以如果发生除零异常，该异常总是会被 ArithmeticException 异常处理，而 DivideByZeroException 异常永远不会被捕获。为了解决这个问题，你必须先捕获 DivideByZeroException 异常，然后再捕获 ArithmeticException 异常：

```
static void Main(string[] args)
{
    int num1, num2, result;
    try
    {
        Console.Write("Please enter the first number:");
        num1 = int.Parse(Console.ReadLine());

        Console.Write("Please enter the second number:");
        num2 = int.Parse(Console.ReadLine());

        Program myApp = new Program();

        Console.WriteLine("The result of {0}/{1} is {2}",
            num1, num2,
            myApp.PerformDivision(num1, num2));
    }
    catch (DivideByZeroException ex)
    {
        Console.WriteLine("Division by zero error.");
    }
    catch (ArithmeticException ex)
    {
        Console.WriteLine("Numerator cannot be zero.");
    }
    catch (FormatException ex)
    {
        Console.WriteLine("Input error.");
    }
    catch (Exception ex)
    {
        Console.WriteLine(ex.Message);
    }
    Console.ReadLine();
}
```

以下是输入 num1 和 num2 的不同值时的输出：

```
Please enter the first number:5
Please enter the second number:0
Division by zero error.

Please enter the first number:0
Please enter the second number:5
Numerator cannot be zero.

Please enter the first number:a
Input error.
```
