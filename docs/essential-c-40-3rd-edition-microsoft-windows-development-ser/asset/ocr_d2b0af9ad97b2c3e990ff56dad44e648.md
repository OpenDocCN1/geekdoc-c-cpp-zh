a Method(42) call will resolve in ascending order, starting with Method(int thing) and proceeding up to Method(long thing), and so on, if the former method does not exist.

The C# specification includes additional rules governing implicit conversion between byte, ushort, uint, ulong, and the other numeric types, but in general it is better to use a cast to make the intended target method more recognizable.

# Basic Error Handling with Exceptions

An important aspect of calling methods relates to error handling; specifically, how to report an error back to the caller. This section examines how to handle error reporting via a mechanism known as **exception handling**.

With exception handling, a method is able to pass information about an error to a calling method without explicitly providing any parameters to do so. Listing 4.19 contains a slight modification to the HeyYou program from Chapter 1. Instead of requesting the last name of the user, it prompts for the user’s age.

# LISTING 4.19: Converting a string to an int

```
using System;

class ExceptionHandling
{
    static void Main()
    {
        string firstName;
        string ageText;
        int age;

        Console.WriteLine("Hey you!");

        Console.Write("Enter your first name: ");
        firstName = System.Console.ReadLine();

        Console.Write("Enter your age: ");
        ageText = Console.ReadLine();
        age = int.Parse(ageText);

        Console.WriteLine(
            "Hi {0}! You are {1} months old.",
            firstName, age*12);
    }
}
```