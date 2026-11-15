System.Exception catch block, will never be invoked. Because of this, following a System.Exception catch block with a general catch block in C# 2.0 or later will result in a compiler warning indicating that the general catch block will never execute.

# Reporting Errors Using a throw Statement

Just as int.Parse() can throw an exception, C# allows developers to throw exceptions from their code, as demonstrated in Listing 4.23 and Output 4.15.

# LISTING 4.23: Throwing an Exception

```
using System;
class ThrowingExceptions
{
    static void Main()
    {
        try
        {
            Console.WriteLine("Begin executing");
            Console.WriteLine("Throw exception...");
            throw new Exception("Arbitrary exception.");
            Console.WriteLine("End executing");
        }
        catch (FormatException exception)
        {
            Console.WriteLine(
                "A FormatException was thrown");
        }
        catch(Exception exception)
        {
            Console.WriteLine(
                "Unexpected error: {0}", exception.Message);
        }
        catch
        {
            Console.WriteLine("Unexpected error!");
        }
        Console.WriteLine(
            "Shutting down...");
    }
}
```