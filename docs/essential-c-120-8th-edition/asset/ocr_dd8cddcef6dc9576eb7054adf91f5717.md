# Chapter 5: Parameters and Methods

# Language Contrast: C++—Header Files

Unlike in C++, C# classes never separate the implementation from the declaration. In C#, there is no header (.h) file or implementation (.cpp) file. Instead, declaration and implementation appear together in the same file. (C# supports an advanced feature called partial methods, where the method's defining declaration is separate from its implementation, but for the purposes of this chapter, we consider only nonpartial methods.) The lack of a separate declaration and implementation in C# removes the requirement to maintain redundant header declaration information in two places found in languages that have separate header and implementation files, such as C++.

# Local Functions

C# 7.0 introduced the ability to declare functions within methods. In other words, rather than always declaring a method within a class, the method (technically function) could be declared within another method (see Listing 5.7).

Listing 5.7: Declaring a Local Function

```
public static void Main()
{
    string GetUserInput(string prompt)
    {
        string? input;
        do
        {
            Console.Write(prompt + ": ");
            input = Console.ReadLine();
        }
        while(string.IsNullOrOrWhiteSpace(input));
        return input;
    }

    string firstName = GetUserInput("First Name");
    string lastName = GetUserInput("Last Name");
    string email = GetUserInput("Email Address");
}
```

```
Console.WriteLine($"{{firstName}{lastName}} {{email}}}");
n//...
```