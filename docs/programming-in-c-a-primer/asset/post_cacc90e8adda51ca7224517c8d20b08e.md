
# 18.9 USING FINALLY STATEMENT

C# supports another statement known as a finally statement that can be used to handle an exception that is not caught by any of the previous catch statements. A finally block can be used to handle any exception generated within a try block. It may be added immediately after the try block or after the last catch block shown as follows:

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

When a finally block is defined, the program is guaranteed to execute, regardless of how control leaves the try, whether it is due to normal termination, due to an exception occurring or due to a jump statement. Figure 18.3 illustrates this. As a result, we can use it to perform certain house-keeping operations such as closing files and releasing system resources.

In Program 18.4, we may include the last two statements inside a finally block as shown below:

```
finally
{
    int y = a[1]/a[0];
    Console.WriteLine("y = " +y);
}
```

This will produce the same output.

![](img/bae4ee2c7c29c052feb3b9a9c5659998_361_0.png)

Fig. 18.3 Execution paths of try-catch-finally blocks

# 18.10 NESTED TRY BLOCKS

C# permits us to nest try blocks inside each other. Example:

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

For simplicity, we have shown only one catch handler in each try block. However, we can string several catch handlers together in each place.

When nested try blocks are executed, the exceptions that are thrown at various points are handled as follows:

- The points P1 and P4 are outside the inner try block and therefore any exceptions thrown at these points will be handled by the catch in the outer block. The inner block is simply ignored.
- Any exception thrown at point P2 will be handled by the inner catch handler and the inner finally will be executed. The execution will continue at point P4 in the program.
- If there is no suitable catch handler to catch an exception thrown at P2, the control will leave the inner block (after executing the inner finally) and look for a suitable catch handler in the outer block. If a suitable one is found, then that handler is executed followed by the outer finally code. Remember, the code at point P4 will be skipped.
- If an exception is thrown at point P3, it is treated as if it had been thrown by the outer try block and, therefore, the control will immediately leave the inner block (of course, after executing the inner finally) and search for a suitable catch handler in the outer block.
- In case, a suitable catch handler is not found, then the system will terminate program execution with an appropriate message.

Program 18.5 shows a simple implementation of nested try blocks. The program uses nested methods, each having its own try .... catch blocks.

The Main method invokes the Division() method which throws an exception. Although the Division() method has a catch block, it does not match the type of exception. The control is therefore transferred to the try block in Main and the program looks for a matching catch handler. It finds one there and executes it.

# Program 18.5

# IMPLEMENTING NESTED TRY BLOCKS

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

# 18.11 THROWING OUR OWN EXCEPTIONS

There may be times when we would like to throw our own exceptions. We can do this by using the keyword throw as follows:

```
throw new Throwable_subclass;
```

Examples:

```
throw new ArithmeticException();
throw new FormatException();
```

Program 18.6 demonstrates the use of a user-defined subclass of Exception class. An object of a class that extends Throwable can be thrown and caught.

# Program 18.6 | THROWING OUR OWN EXCEPTION

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

A run of Program 18.6 produces:

Caught my exception
Number is too small
I am always here

The object e which contains the error message "Number is too small" is caught by the catch block which then displays the message using the Message property.

Note that Program 18.7 also illustrates the use of finally block. The last line of the output is produced by the finally block.

A rule of thumb when creating our own exceptional classes is that we must implement all the three System.Exception constructors as illustrated in the example program.

Program 18.7 creates a new type of user-defined exception MyException and it is being used to catch an exception with its own customized message.

# Program 18.7 | CUSTOM EXCEPTION

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

Program 18.8 uses different types of system-defined exception classes in multiple catch blocks. These blocks catch the exceptions thrown and display the exception messages.

# Program 18.8   MULTIPLE CATCH

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
