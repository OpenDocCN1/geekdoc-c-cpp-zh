

# 18.9 使用 FINALLY 语句

C# 支持另一种称为 finally 语句的语句，它可用于处理未被前面任何 catch 语句捕获的异常。finally 块可用于处理 try 块内产生的任何异常。它可以紧接在 try 块之后或最后一个 catch 块之后添加，如下所示：

```
try
{
    ..........
    ..........
}
finally
{
    ..........
    ..........
}
```

```
try
{
    ..........
    ..........
}
catch (...)
{
    ..........
    ..........
}
catch (...)
{
    ..........
    ..........
}
...
...
finally
{
    ..........
    ..........
}
```

当定义了 finally 块时，无论控制流如何离开 try 块（无论是由于正常终止、发生异常还是由于跳转语句），程序都保证会执行 finally 块。图 18.3 说明了这一点。因此，我们可以用它来执行某些清理操作，例如关闭文件和释放系统资源。

在程序 18.4 中，我们可以将最后两条语句包含在 finally 块中，如下所示：

```
finally
{
    int y = a[1]/a[0];
    Console.WriteLine("y = " +y);
}
```

这将产生相同的输出。

![](img/bae4ee2c7c29c052feb3b9a9c5659998_361_0.png)

图 18.3 try-catch-finally 块的执行路径

# 18.10 嵌套 TRY 块

C# 允许我们在彼此内部嵌套 try 块。例如：

```
try
{
    .... (Point P1)
    ....
    try
    {
        .... (Point P2)
        ....
    }
    catch
    {
        .... (Point P3)    Inner try block
        ....
    }
    finally
    {
        ....
        ....
    }
    .... (Point P4)
    ....
}
catch
{
    ....
}
finally
{
    ....
}
```

为了简单起见，我们在每个 try 块中只显示了一个 catch 处理程序。然而，我们可以在每个位置将多个 catch 处理程序串联在一起。

当嵌套的 try 块被执行时，在不同点抛出的异常按如下方式处理：

- 点 P1 和 P4 位于内部 try 块之外，因此在这些点抛出的任何异常都将由外部块中的 catch 处理。内部块被直接忽略。
- 在点 P2 抛出的任何异常将由内部的 catch 处理程序处理，并且内部的 finally 将被执行。程序将在点 P4 继续执行。
- 如果没有合适的 catch 处理程序来捕获在 P2 抛出的异常，控制流将离开内部块（在执行内部的 finally 之后），并在外部块中寻找合适的 catch 处理程序。如果找到合适的处理程序，则执行该处理程序，随后执行外部的 finally 代码。请记住，点 P4 的代码将被跳过。
- 如果在点 P3 抛出异常，该异常将被视为由外部 try 块抛出，因此控制流将立即离开内部块（当然，在执行内部的 finally 之后），并在外部块中搜索合适的 catch 处理程序。
- 如果找不到合适的 catch 处理程序，系统将终止程序执行并显示适当的消息。

程序 18.5 展示了嵌套 try 块的简单实现。该程序使用嵌套的方法，每个方法都有自己的 try....catch 块。

Main 方法调用 Division() 方法，该方法抛出一个异常。尽管 Division() 方法有一个 catch 块，但它与异常类型不匹配。因此，控制权被转移到 Main 中的 try 块，程序寻找匹配的 catch 处理程序。程序在那里找到了一个并执行它。

# 程序 18.5

# 实现嵌套 TRY 块

```csharp
using System;
class NestedTry
{
	static int m = 10;
	static int n = 0;
	static void Division ( )
	{
		try
		{
			int k = m/n;
		}
		catch (ArgumentException e)
		{
			Console.WriteLine("Caught an exception");
		}
		finally
		{
			Console.WriteLine("Inside Division Method");
		}
	}
	public static void Main ( )
	{
		try
		{
			Division ( );
		}
		catch (DivideByZeroException e)
		{
			Console.WriteLine("Caught an exception");
		}
		finally
		{
			Console.WriteLine("Inside Main Method");
		}
	}
}
```

# 18.11 抛出我们自己的异常

有时候我们可能想要抛出自己的异常。我们可以通过使用 throw 关键字来实现这一点，如下所示：

```
throw new Throwable_subclass;
```

示例：

```
throw new ArithmeticException();
throw new FormatException();
```

程序 18.6 演示了 Exception 类的用户自定义子类的使用。可以抛出并捕获扩展了 Throwable 的类的对象。

# 程序 18.6 | 抛出我们自己的异常

```
using System;
class MyException:Exception
{
    public MyException (string Message) : base (Message)
    {
    }
    public MyException ()
    {
    }
    public MyException (string Message, Exception inner)
        : base (Message, inner)
    {
    }
}
class TestMyException
{
    public static void Main()
    {
        int x = 5, y = 1000;
        try
        {
            float z = (float) x / (float) y ;
            if(z < 0.01)
            {
                throw new MyException("Number is too small!");
            }
        }
        catch (MyException  e)
        {
            Console.WriteLine("Caught my exception");
            Console.WriteLine(e.Message);
        }
        finally
        {
            Console.WriteLine("I am always here");
        }
    }
}
```

运行程序 18.6 会产生：

Caught my exception
Number is too small
I am always here

包含错误消息 "Number is too small" 的对象 e 被 catch 块捕获，然后使用 Message 属性显示该消息。

请注意，程序 18.7 也演示了 finally 块的使用。输出的最后一行由 finally 块产生。

创建我们自己的异常类时的一个经验法则是，我们必须实现 System.Exception 的全部三个构造函数，如示例程序所示。

程序 18.7 创建了一种新的用户自定义异常类型 MyException，并且它被用来捕获带有其自定义消息的异常。

# 程序 18.7 | 自定义异常

```
using System;
using System.Collections.Generic;
using System.Text;

namespace CustomException
{
    public class MyCustomException : System.Exception
    {
        public MyCustomException(string txt) : base(txt) // pass the message up to the base class
        {
        }
    }
    class CustomeExceptionExample
    {
        public void DisplayAll()
        {
            try
            {
                Console.WriteLine("Application started!!");
                double a = 718;
                double b = 0;
                Console.WriteLine("{0} / {1} = {2}", a, b, DivideValues(a, b));
                Console.WriteLine("The error is handled in a try catch block and customised message shown above.");
            }
            // most derived exception type first
            catch (System.DivideByZeroException e)
            {
                Console.WriteLine("\nDivideByZeroException! Msg: {0}", e.Message);
            }
```

```
// catch custom exception
catch (MyCustomException e)
{
	Console.WriteLine(
		"\nMyCustomException! Msg: {0}", 
		e.Message);
}

finally
{
	Console.WriteLine("Application executed!!");
}
```

```
// do the division if legal
public double DivideValues(double a, double b)
{
	if (b == 0)
	{
		MyCustomException e = 
		new MyCustomException(
			"Can't be divided by zero, result is Infinity.");
		Console.WriteLine(e);
	}

	if (a == 0)
	{
		// create a custom exception instance
		MyCustomException e = 
		new MyCustomException(
			"Can't have a zero divisor");
		Console.WriteLine(e);
	}

	return a / b;
}
```

```
static void Main(string[] args)
{
	Console.WriteLine("This is an example of a customised exception developed in C#.");
	CustomExceptionExample cee = new CustomExceptionExample();
	cee.DisplayAll();
}
```

![](img/bae4ee2c7c29c052feb3b9a9c5659998_367_0.png)

程序 18.8 在多个 catch 块中使用不同类型的系统定义的异常类。这些块捕获抛出的异常并显示异常消息。

# 程序 18.8   多重 CATCH

```
using System;
using System.Collections.Generic;
using System.Text;

namespace MultipleCatch
{
    class MultipleCatchBlockExample
    {
        public void execute()
        {
            try
            {
                double val1 = 0;
                double val2 = 121;
                Console.WriteLine("Dividing {0} by {1}...", val1, val2);
                Console.WriteLine("{0} / {1} = {2}",
                    val1, val2, DivideValues(val1, val2));
            }

            // most specific exception type first
            catch (DivideByZeroException ex)
            {
                Console.WriteLine("DivideByZeroException caught!", ex);
            }
            catch (ArithmeticException e)
            {
                Console.WriteLine("ArithmeticException caught!", e);
            }
            // generic exception type last
```

