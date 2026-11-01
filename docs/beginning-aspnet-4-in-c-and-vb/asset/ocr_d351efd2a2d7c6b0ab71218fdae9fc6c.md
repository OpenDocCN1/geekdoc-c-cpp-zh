```
    'An exception was thrown. Message was: {0}', ex.Message);
}
finally
{
    Console.WriteLine("Thank you");
}
}
}
}
```

*code snippet SimpleExceptions.cs*

The core of this code is a while loop, which continually uses Console.ReadLine() to ask for user input. ReadLine() returns a string, so your first task is to convert it to an int using the System.Convert.ToInt32() method. The System.Convert class contains various useful methods to perform data conversions and provides an alternative to the int.Parse() method. In general, System.Convert contains methods to perform various type conversions. Recall that the C# compiler resolves int to instances of the System.Int32 base class.

> It is also worth pointing out that the parameter passed to the catch block is scoped to that catch block — which is why you are able to use the same parameter name, ex, in successive catch blocks in the preceding code.

In the preceding example, you also check for an empty string, because this is your condition for exiting the while loop. Notice how the break statement actually breaks right out of the enclosing try block as well as the while loop because this is valid behavior. Of course, when execution breaks out of the try block, the Console.WriteLine() statement in the finally block is executed. Although you just display a greeting here, more commonly you will be doing tasks like closing file handles and calling the Dispose() method of various objects to perform any cleaning up. After the computer leaves the finally block, it simply carries on executing into the next statement that it would have executed had the finally block not been present. In the case of this example, though, you iterate back to the start of the while loop, and enter the try block again (unless the finally block was entered as a result of executing the break statement in the while loop, in which case you simply exit the while loop).

```
Next, you check for your exception condition:

if (index < 0 || index > 5)
{
    throw new IndexOutOfRangeException("You typed in " + userInput);
}
```

When throwing an exception, you need to choose what type of exception to throw. Although the class System.Exception is available, it is intended only as a base class. It is considered bad programming practice to throw an instance of this class as an exception, because it conveys no information about the nature of the error condition. Instead, the .NET Framework contains many other exception classes that are derived from System.Exception. Each of these matches a particular type of exception condition, and you are free to define your own ones as well. The idea is that you give as much information as possible about the particular exception condition by throwing an instance of a class that matches the particular error condition. In the preceding example, System.IndexOutOfRangeException is the best choice for the circumstances. IndexOutOfRangeException has several constructor overloads. The one chosen in the example takes a string, which describes the error. Alternatively, you might choose to derive your own custom Exception object that describes the error condition in the context of your application.