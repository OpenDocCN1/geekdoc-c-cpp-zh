a call of the form Method(42) will resolve as Method(int thing) because that is an exact match from the argument type to the parameter type. Were that method to be removed, overload resolution would choose the long version, because long is more specific than either double or object.

The C# specification includes additional rules governing implicit conversion between byte, ushort, uint, ulong, and the other numeric types. In general, though, it is better to use a cast to make the intended target method more recognizable.

# Basic Error Handling with Exceptions

This section examines how to handle error reporting via a mechanism known as **exception handling**.

With exception handling, a method is able to pass information about an error to a calling method without using a return value or explicitly providing any parameters to do so. Listing 5.22 contains a slight modification to Listing 1.16, the HeyYou program from Chapter 1. Instead of requesting the last name of the user, it prompts for the user's age.

LISTING 5.22: Converting a string to an int

```
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
      $"Hi { firstName }!  You are { age+12 } months old.");
  }
}
```
```