+   - In case, a suitable catch handler is not found, then the system will terminate program execution with an appropriate message.

Program 18.5 shows a simple implementation of nested try blocks. The program uses nested methods, each having its own try .... catch blocks.

The Main method invokes the Division() method which throws an exception. Although the Division() method has a catch block, it does not match the type of exception. The control is therefore transferred to the try block in Main and the program looks for a matching catch handler. It finds one there and executes it.

# Program 18.5

# IMPLEMENTING NESTED TRY BLOCKS

```
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
```