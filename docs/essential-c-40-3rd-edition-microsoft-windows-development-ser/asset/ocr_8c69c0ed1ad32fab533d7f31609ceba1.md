Frequently, programmers use whitespace to indent code for greater readability. Consider the two variations on HelloWorld, as shown in Listing 1.7 and Listing 1.8.

# LISTING 1.7: No Indentation Formatting

```
class HelloWorld
{
    static void Main()
    {
    System.Console.WriteLine("Hello Inigo Montoya");
    }
}
```

# LISTING 1.8: Removing Whitespace

```
class HelloWorld(static void Main()
{System.Console.WriteLine("Hello Inigo Montoya");}}
```

Although these two examples look significantly different from the original program, the C# compiler sees them as identical.

# BEGINNER TOPIC

# Formatting Code with Whitespace

Indenting the code using whitespace is important for greater readability. As you begin writing code, you need to follow established coding standards and conventions in order to enhance code readability.

The convention used in this book is to place curly braces on their own line and to indent the code contained between the curly brace pair. If another curly brace pair appears within the first pair, all the code within the second set of braces is also indented.

This is not a uniform C# standard, but a stylistic preference.

# Working with Variables

Now that you've been introduced to the most basic C# program, it's time to declare a local variable. Once a variable is declared, you can assign it a value, replace that value with a new value, and use it in calculations,