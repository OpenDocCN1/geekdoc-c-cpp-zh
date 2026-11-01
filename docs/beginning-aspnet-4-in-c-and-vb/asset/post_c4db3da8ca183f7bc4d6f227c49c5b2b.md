
The program then continues to ask for more numbers for processing until the user simply presses the Enter key without entering anything.

![](img/d7d2ffa0a76feaab821930e95daace93_417_0.png)

The code for SimpleExceptions looks like this:

```csharp
using System;

namespace Wrox.ProCSharp.AdvancedCSharp
{
    public class MainEntryPoint
    {
        public static void Main()
        {
            while (true)
            {
                try
                {
                    string userInput;

                    Console.Write("Input a number between 0 and 5 * " +
                        "(or just hit return to exit): ");
                    userInput = Console.ReadLine();

                    if (userInput == "")
                    {
                        break;
                    }

                    int index = Convert.ToInt32(userInput);

                    if (index < 0 || index > 5)
                    {
                        throw new IndexOutOfRangeException(
                            "You typed in " + userInput);
                    }

                    Console.WriteLine("Your number was " + index);
                }
                catch (IndexOutOfRangeException ex)
                {
                    Console.WriteLine("Exception: " +
                        "Number should be between 0 and 5. {0}", ex.Message);
                }
                catch (Exception ex)
                {
                    Console.WriteLine(
                        "An exception was thrown. Message was: {0}", ex.Message);
                }
                finally
                {
                    Console.WriteLine("Thank you");
                }
            }
        }
    }
}
```

*code snippet SimpleExceptions.cs*

The core of this code is a while loop, which continually uses Console.ReadLine() to ask for user input. ReadLine() returns a string, so your first task is to convert it to an int using the System.Convert.ToInt32() method. The System.Convert class contains various useful methods to perform data conversions and provides an alternative to the int.Parse() method. In general, System.Convert contains methods to perform various type conversions. Recall that the C# compiler resolves int to instances of the System.Int32 base class.

> It is also worth pointing out that the parameter passed to the catch block is scoped to that catch block — which is why you are able to use the same parameter name, ex, in successive catch blocks in the preceding code.

In the preceding example, you also check for an empty string, because this is your condition for exiting the while loop. Notice how the break statement actually breaks right out of the enclosing try block as well as the while loop because this is valid behavior. Of course, when execution breaks out of the try block, the Console.WriteLine() statement in the finally block is executed. Although you just display a greeting here, more commonly you will be doing tasks like closing file handles and calling the Dispose() method of various objects to perform any cleaning up. After the computer leaves the finally block, it simply carries on executing into the next statement that it would have executed had the finally block not been present. In the case of this example, though, you iterate back to the start of the while loop, and enter the try block again (unless the finally block was entered as a result of executing the break statement in the while loop, in which case you simply exit the while loop).

Next, you check for your exception condition:

if (index < 0 || index > 5)
{
    throw new IndexOutOfRangeException("You typed in " + userInput);
}

When throwing an exception, you need to choose what type of exception to throw. Although the class System.Exception is available, it is intended only as a base class. It is considered bad programming practice to throw an instance of this class as an exception, because it conveys no information about the nature of the error condition. Instead, the .NET Framework contains many other exception classes that are derived from System.Exception. Each of these matches a particular type of exception condition, and you are free to define your own ones as well. The idea is that you give as much information as possible about the particular exception condition by throwing an instance of a class that matches the particular error condition. In the preceding example, System.IndexOutOfRangeException is the best choice for the circumstances. IndexOutOfRangeException has several constructor overloads. The one chosen in the example takes a string, which describes the error. Alternatively, you might choose to derive your own custom Exception object that describes the error condition in the context of your application.

Suppose that the user then types a number that is not between 0 and 5. This will be picked up by the if statement and an IndexOutOfRangeException object will be instantiated and thrown. At this point, the computer will immediately exit the try block and hunt for a catch block that handles IndexOutOfRangeException. The first catch block it encounters is this:

catch (IndexOutOfRangeException ex)
{
    Console.WriteLine
    ("Exception: Number should be between 0 and 5. {0}", ex.Message);
}

Because this catch block takes a parameter of the appropriate class, the catch block will be passed the exception instance and executed. In this case, you display an error message and the Exception.Message property (which corresponds to the string you passed to the IndexOutOfRangeException's constructor). After executing this catch block, control then switches to the finally block, just as if no exception had occurred.

Notice that in the example, you have also provided another catch block:

catch (Exception ex)
{
    Console.WriteLine("An exception was thrown. Message was: {0}", ex.Message);
}

This catch block would also be capable of handling an IndexOutOfRangeException if it weren't for the fact that such exceptions will already have been caught by the previous catch block. A reference to a base class can also refer to any instances of classes derived from it, and all exceptions are derived from System.Exception. So why isn't this catch block executed? The answer is that the computer executes only the first suitable catch block it finds from the list of available catch blocks. So why is this second catch block even here? Well, it is not only your code that is covered by the try block. Inside the block, you actually make three separate calls to methods in the System namespace (Console.ReadLine(), Console.Write(), and Convert.ToInt32()), and any of these methods might throw an exception.

If you type in something that is not a number — say a or hello — the Convert.ToInt32() method will throw an exception of the class System.FormatException to indicate that the string passed into ToInt32() is not in a format that can be converted to an int. When this happens, the computer will trace back through the method calls, looking for a handler for this exception. Your first catch block (the one that takes an IndexOutOfRangeException) will not do. The computer then looks at the second catch block. This one will do because FormatException is derived from Exception, so a FormatException instance can be passed as a parameter here.

The structure of the example is actually fairly typical of a situation with multiple catch blocks. You start with catch blocks that are designed to trap very specific error conditions. Then, you finish with more general blocks that will cover any errors for which you have not written specific error handlers. Indeed, the order of the catch blocks is important. If you had written the previous two blocks in the opposite order, the code would not have been compiled, because the second catch block is unreachable (the Exception catch block would catch all exceptions). Therefore, the uppermost catch blocks should be the most granular options available and ending with the most general options.

Now that you have analyzed the code for the example, you can run it. The following output illustrates what happens with different inputs and demonstrates both the IndexOutOfRangeException and the FormatException being thrown:

SimpleExceptions
Input a number between 0 and 5 (or just hit return to exit):4
Your number was 4
Thank you
Input a number between 0 and 5 (or just hit return to exit):0
Your number was 0
Thank you
Input a number between 0 and 5 (or just hit return to exit):10
