
Inheritance is a powerful feature that makes it possible for you to extend the functionality of a class by creating a new class that derives from it. However, sometimes using inheritance is not the most appropriate mechanism for adding new behaviors, especially if you need to quickly extend a type without affecting existing code.

For example, suppose you want to add a new feature to the int type, such as a method named Negate that returns the negative equivalent value that an integer currently contains. (Of course, you could use the unary minus operator [- to perform the same task, but bear me...) One way to achieve this is to define a new type named Int32 that inherits from System.Int32 (int is an alias for System.Int32) and adds the Negate method:

Click here to view image

```csharp
class Neg32 : System.Int32
{
    public int Negate()
    {
        ...
    }
}
```

The theory is that Neg32 will inherit all the functionality associated with the System.Int32 type in addition to the Negate method. There are two reasons why you might not want to follow this approach, however:

- This method applies only to the Neg32 type. If you want to use it with existing variables in your code, you must change the definition of every int variable to the Neg32 type.

- The System.Int32 type is actually a structure, not a class, and you cannot use inheritance with structures.

This is where extension methods become very useful. Using extension method, you can extend an existing type (a class or structure) with additional static methods. These static methods become immediately available to your code in any statements that refer to data of the type being extended.

You define an extension method in a static class and specify the type to which the method applies as the first parameter to the method, along with the this keyword. Here's an example showing how you can implement the Negate extension method for the int type:

Click here to view code image

```csharp
static class Utils
{
    public static int Negate(this int i)
    {
        return -i;
    }
}
```

The syntax looks a little odd, but it is this keyword prefixing the parameter to Negate that identifies it as an extension method, and the fact that that this prefixes is an int means that you're extending the int type.

To use the extension method, bring the Utils class into scope. (If necessary, add a using statement that specifies the namespace to which the Utils class belongs, or a using static statement that specifies the Utils class directly.) Then you can use dot notation (.) to refer to the method, like this:

Click here to view code image

```csharp
int x = 591;
Console.WriteLine($"x.Negate {x.Negate()}");
```

Notice that you don't need to reference the Utils class anywhere in the statement that calls the Negate method. The C# compiler automatically detects all extension methods for a given type from all the static classes that are in scope.

You can also invoke the Utils.Negate method by passing an int as the parameter, using the regular syntax you've seen before, although this use obviates the purpose of defining the method as an extension method:

Click here to view code image

```csharp
int x = 591; Console.WriteLine($"x.Negate {Utils.Negate(x)}");
```

In the following exercise, you'll add an extension method to the int type. With this extension method, you can convert the value in an int variable from base 10 to a representation of that value in a different number base.

## To create an extension method

1. In Visual Studio 2022, open the ExtensionMethod solution, which is located in the \Microsoft Press\VCSBS\Chapter 12\ExtensionMethod folder in your Documents folder.

2. Display the Utils.cs file in the Code and Text Editor window.

This file contains a static class named Utils in a namespace named Extensions. Remember that you must define extension methods inside a static class. The class is empty apart from the // TODO: comment.

3. Delete the comment and declare a public static method in the Utils class named ConvertToBase. The method should take two parameters:

   - An int parameter i, prefixed with the this keyword to indicate that the method is an extension method for the int type
   - Another ordinary int parameter named baseToConvertTo

The method will convert the value in i to the base indicated by baseToConvertTo. The method should return an int containing the converted value.

The ConvertToBase method should look like this:

Click here to view code image

```csharp
static class Utils
{
    public static int ConvertToBase(int i, int baseToConvertTo)
    {
    }
}
```

4. Add an if to the ConvertToBase method that checks that the value of the baseToConvertTo parameter is between 2 and 10.

The algorithm used by this exercise does not work reliably outside this range of values. Throw an ArgumentException with a suitable message if the value of baseToConvertTo is outside this range.

The ConvertToBase method should look like this:

```csharp
public static int ConvertToBase(int i, int baseToConvertTo)
{
    if (baseToConvertTo < 2 || baseToConvertTo > 10)
    {
        throw new ArgumentException("Value cannot be converted to base " + baseToConvertTo.ToString());
    }
}
```

5. Add the following statements shown in bold to the ConvertToBase method, after the statement block that throws the ArgumentException exception.

Click here to code image

```csharp
public static int ConvertToBase(int i, int baseToConvertTo)
{
    int result = 0;
    int iterations = 0;
    do {
        int nextDigit = i % baseToConvertTo;
        i /= baseToConvertTo;
        result += nextDigit * (int)Math.Pow(10, iterations);
        iterations++;
    } while (i != 0);
    return result;
}
```

This code implements a well-known algorithm that converts a number from base 10 to a different base. (Chapter 5, "Using compound assignment and iteration statements") presents a version of this algorithm for converting a decimal number to an octal.

6. Display the Program.cs file in the Code and Text Editor window.

7. Add the following directive using the System; directive at the top of the file:

```csharp
using Extensions;
```

This statement brings the namespace containing the Utils class into scope. The compiler might display the warning "using directive is unnecessary"; however, the ConvertToBase extension method will not be visible in the Program.cs file if you don't perform this task.

8. Add the following statements shown in bold to the doWork method of the Program class, replacing the // TODO: comment:

Click here to view image

```csharp
static void doWork()
{
    int x = 591;
    for (int i = 2; i <= 10; i++)
    {
        Console.WriteLine($"{x} in base {i} is {x.ConvertToBase(i)}");
    }
}
```

Notice that ConvertToBase appears as an extension method in IntelliSense when you type the period (.) after the Console.WriteLine statement.

![](img/4f6c1423ece9eb79a4a4e5db81746d_473_0.png)

9. On the Debug menu, select Start Without Debugging. Confirm that the program displays messages to the console showing the value 591 in the different bases, like this:

```
Microsoft Visual Studio Debug Console
591 in base 2 is 101001111
591 in base 3 is 210220
591 in base 4 is 21033
591 in base 5 is 4331
591 in base 6 is 2423
591 in base 7 is 1503
591 in base 8 is 1117
591 in base 9 is 726
591 in base 10 is 591
:\Users\student\Documents\Microsoft Press\VCSB\ExtensionMethod.exe (process 3104) exited with code 0.
Press any key to close this window . .
```

10. Press Enter to close the program and return to Visual Studio 2022.

## Summary

In this chapter, you learned how to use inheritance to define a hierarchy of classes, and you should now understand how to override inherited methods and implement virtual methods. You also learned how to add an extension method to an existing type.

- If you want to continue to the next chapter, keep Visual Studio 2022 running and turn to Chapter 13.
- If you want to exit Visual Studio 2022 now, on the File menu, select Exit. If you see a Save dialog, select Yes and save the project.

## Quick reference

| To | Do this |
