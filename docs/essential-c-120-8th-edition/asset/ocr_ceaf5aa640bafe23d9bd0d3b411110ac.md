statement for lastName, Listing 1.18 writes out the entire output string interpolation. With string interpolation, the compiler interprets the interior of the curly brackets within the string regions in which you can embed code (expressions) that the compiler will evaluate and convert to strings. Rather than executing lots of code snippets individually and combining the results as a string at the end, string interpolation allows you to do this in a single step. This makes the code easier to understand.

Prior to C# 6.0, C# used a different approach, that supplies composite formatting. With composite formatting, the code supplies a format string to define the output format—see Listing 1.19.

LISTING 1.19: Formatting Using Console.WriteLine()'s Composite Formatting

```
public class HeyYou
{
    public static void Main()
    {
        string firstName;
        string lastName;

        Console.WriteLine("Hey you!");

        Console.Write("Enter your first name: ");
        firstName = Console.ReadLine();

        Console.Write("Enter your last name: ");
        lastName = Console.ReadLine();

        Console.WriteLine(
            "Your full name is {0} {1}.", firstName, lastName);
    }
}
```

In this example, the format string is Your full name is {0} {1}. It identifies two indexed placeholders for data insertion in the string. Each placeholder corresponds to the order of the arguments that appear after the format string.

Note that the index value begins at zero. Each inserted argument (known as a format item) appears after the format string in the order corresponding to the index value. In this example, since firstName is the first argument to follow immediately