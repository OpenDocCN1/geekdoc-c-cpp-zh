
## 重新抛出异常

有时在捕获异常后，你希望在采取一些纠正措施后，将相同的（或新的类型）异常重新抛回给调用函数。请看下面的示例：

```csharp
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

            Console.WriteLine("The result of {0}/({1}) is {2}",
                num1, num2,
                myApp.PerformDivision(num1, num2));
        }
        catch (Exception ex)
        {
            Console.WriteLine(ex.Message);
            if (ex.InnerException != null)
                Console.WriteLine(ex.InnerException.ToString());
        }
        Console.ReadLine();
    }

    private int PerformDivision(int num1, int num2)
    {
        try
        {
            return num1 / num2;
        }
        catch (DivideByZeroException ex)
        {
            throw new Exception("Division by zero error.", ex);
        }
    }
}
```

在这里，PerformDivision() 函数尝试捕获 DivideByZeroException 异常，一旦成功，它会使用以下带有两个参数的语句重新抛出一个新的通用 Exception 异常：

```csharp
throw new Exception("Division by zero error.", ex);
```

第一个参数表示要抛出的异常的描述，而第二个参数用于内部异常。内部异常表示导致当前异常的异常。当此异常被重新抛出时，它由 Main() 函数中的 catch 块处理：

```csharp
catch (Exception ex)
{
    Console.WriteLine(ex.Message);
    if (ex.InnerException != null)
        Console.WriteLine(ex.InnerException.ToString());
}
```

要检索异常的来源，可以检查 InnerException 属性并使用 ToString() 方法打印其详细信息。当 num2 为零时的输出如下：

```text
Please enter the first number:5
Please enter the second number:0
Division by zero error.
System.DivideByZeroException: Attempted to divide by zero.
at ConsoleApp.Program.PerformDivision(Int32 num1, Int32 num2) in C:\Documents and Settings\Wei-Meng Lee\My Documents\Visual Studio 2008\Projects\ConsoleApp\ConsoleApp\Program.cs:line 43
```

正如你所见，异常的消息是“Division by zero error”（由你自己设置），而 InnerException 属性显示了错误的真正原因——“Attempted to divide by zero。”

## 异常链

InnerException 属性的类型为 Exception，可用于存储先前异常的列表。这被称为异常链。

要了解异常链的工作原理，请考虑以下程序：

```csharp
class Program
{
    static void Main(string[] args)
    {
        Program myApp = new Program();

        try
        {
            myApp.Method1();
        }
        catch (Exception ex)
        {
            Console.WriteLine(ex.Message);
            if (ex.InnerException != null)
                Console.WriteLine(ex.InnerException.ToString());
        }
        Console.ReadLine();
    }

    private void Method1()
    {
        try
        {
            Method2();
        }
        catch (Exception ex)
        {
            throw new Exception(
                "Exception caused by calling Method2() in Method1().", ex);
        }
    }

    private void Method2()
    {
        try
        {
            Method3();
        }
        catch (Exception ex)
        {
            throw new Exception(
                "Exception caused by calling Method3() in Method2().", ex);
        }
    }

    private void Method3()
    {
        try
        {
            int num1 = 5, num2 = 0;
            int result = num1 / num2;
        }
        catch (DivideByZeroException ex)
        {
            throw new Exception("Division by zero error in Method3().", ex);
        }
    }
}
```

在此程序中，Main() 函数调用 Method1()，后者依次调用 Method2()。Method2() 然后调用 Method3()。在 Method3() 中，发生了除零异常，你通过传入当前异常（DivideByZeroException）重新抛出一个新的 Exception 异常。该异常被 Method2() 捕获，后者通过传入当前异常重新抛出一个新的 Exception 异常。Method1() 随后捕获异常并重新抛出一个新的 Exception 异常。最后，Main() 函数捕获异常并打印出结果，如图 12-4 所示。

![](img/a977a875c7c627b45d939729705a252e_412_0.png)

图 12-4

如果你在 Main() 函数内的 catch 块中设置断点，你会看到 InnerException 属性包含每个异常的详细信息，并且所有异常都通过 InnerException 属性链接起来（参见图 12-5）。

![](img/a977a875c7c627b45d939729705a252e_412_1.png)

图 12-5

## 使用异常对象

与其使用你抛出的每个异常类的默认描述，你可以通过创建异常的实例然后设置 Message 属性来自定义异常的描述。你还可以指定 HelpLink 属性以指向开发者可以找到有关异常的更多信息的 URL。例如，你可以使用以下代码创建 ArithmeticException 类的新实例：

```csharp
if (num1 == 0)
{
    ArithmeticException ex =
        new ArithmeticException("Value of num1 cannot be 0.")
    {
        HelpLink = "http://www.learn2develop.net"
    };
    throw ex;
}
```

下面是如何通过自定义各种现有异常类来修改前一个程序：

```csharp
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

            Console.WriteLine("The result of {0}/({1}) is {2}",
                num1, num2,
                myApp.PerformDivision(num1, num2));
        }
        catch (DivideByZeroException ex)
        {
            Console.WriteLine(ex.Message);
        }
        catch (ArithmeticException ex)
        {
            Console.WriteLine(ex.Message);
        }
        catch (FormatException ex)
        {
            Console.WriteLine(ex.Message);
        }
        catch (Exception ex)
        {
            Console.WriteLine(ex.Message);
        }
        Console.ReadLine();
    }

    private int PerformDivision(int num1, int num2)
    {
        if (num1 == 0)
        {
            ArithmeticException ex =
                new ArithmeticException("Value of num1 cannot be 0.")
            {
                HelpLink = "http://www.learn2develop.net"
            };
            throw ex;
        }

        if (num2 == 0)
        {
            DivideByZeroException ex =
                new DivideByZeroException("Value of num2 cannot be 0.")
            {
                HelpLink = "http://www.learn2develop.net"
            };
            throw ex;
        }

        return num1 / num2;
    }
}
```

当为 num1 和 num2 输入不同的值时的输出如下：

```text
Please enter the first number:0
Please enter the second number:5
Value of num1 cannot be 0.

Please enter the first number:5
Please enter the second number:0
Value of num2 cannot be 0.
```

## finally 语句

到目前为止，你已经知道可以使用 try-catch 块来封装潜在危险的代码。这对于文件操作、用户输入等操作尤其有用。请考虑以下示例：

```csharp
FileStream fs = null;
try
{
    //---opens a file for reading---
    fs = File.Open(@"C:\textfile.txt",
        FileMode.Open, FileAccess.Read);

    //---tries to write some text into the file---
    byte[] data = ASCIIEncoding.ASCII.GetBytes("some text");
    fs.Write(data, 0, data.Length);

    //---close the file---
    fs.Close();
}
catch (Exception ex)
{
    Console.WriteLine(ex.ToString());
}

//---an error will occur here---
fs = File.Open(@"C:\textfile.txt", FileMode.Open, FileAccess.Read);
```
