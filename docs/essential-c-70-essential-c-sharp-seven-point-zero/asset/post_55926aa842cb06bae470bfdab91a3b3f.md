
## Chapter 2: Data Types

### LISTING 2.19: Assigning null to a String

```csharp
static void Main()
{
    string faxNumber;
    // ...

    // Clear the value of faxNumber
    faxNumber = null;

    // ...
}
```

Assigning the value null to a reference type is not equivalent to not assigning it at all. In other words, a variable that has been assigned null has still been set, whereas a variable with no assignment has not been set and therefore will often cause a compile error if used prior to assignment.

Assigning the value null to a string variable is distinctly different from assigning an empty string, "". Use of null indicates that the variable has no value, whereas "" indicates that there is a value—an empty string. This type of distinction can be quite useful. For example, the programming logic could interpret a homePhone of null to mean that the home phone number is unknown, while a homePhone value of "" could indicate that there is no home phone number.

## The void “Type”

Sometimes the C# syntax requires a data type to be specified, but no data is actually passed. For example, if no return from a method is needed, C# allows you to specify void as the data type instead. The declaration of Main within the HelloWorld program is an example. The use of void as the return type indicates that the method is not returning any data and tells the compiler not to expect a value. void is not a data type per se but rather an indication that there is no data being returned.

## Language Contrast: C++

In both C++ and C#, void has two meanings: as a marker that a method does not return any data and to represent a pointer to a storage location of unknown type. In C++ programs, it is quite common to see pointer types such as void*. C# can also represent pointers to storage locations of unknown type using the same syntax, but this usage is comparatively rare in C# and typically encountered only when writing programs that interoperate with unmanaged code libraries.

Language Contrast: Visual Basic—Returning void Is Like Defining a Subroutine

The Visual Basic equivalent of returning a void in C# is to define a subroutine (Sub/End Sub) rather than a function that returns a value.

## Conversions between Data Types

Given the thousands of types predefined in the various CLI implementations and the unlimited number of types that code can define, it is important that types support conversion from one type to another where it makes sense. The most common operation that results in a conversion is **casting**.

Consider the conversion between two numeric types: converting from a variable of type long to a variable of type int. A long type can contain values as large as 9,223,372,036,854,775,808; however, the maximum size of an int is 2,147,483,647. As such, that conversion could result in a loss of data—for example, if the variable of type long contains a value greater than the maximum size of an int. Any conversion that could result in a loss of magnitude or an exception because the conversion failed requires an **explicit cast**. Conversely, a conversion operation that will not lose magnitude and will not throw an exception regardless of the operand types is an **implicit conversion**.

## Explicit Cast

In C#, you cast using the **cast operator**. By specifying the type you would like the variable converted to within parentheses, you acknowledge that if an explicit cast is occurring, there may be a loss of precision and data, or an exception may result. The code in Listing 2.20 converts a long to an int and explicitly tells the system to attempt the operation.

**LISTING 2.20: Explicit Cast Example**

```csharp
long longNumber = 50918309109;
int intNumber = (int) longNumber;
// Cast Operator
```

With the cast operator, the programmer essentially says to the compiler, “Trust me, I know what I am doing. I know that the value will fit into the target type.” Making such a choice will cause the compiler to allow the conversion. However, with an explicit conversion, there is still a chance that an error, in the form of an exception, might occur while executing if the data is not converted successfully. It is therefore the programmer’s responsibility to ensure the data is successfully converted, or else to provide the necessary error-handling code when the conversion fails.

## Advanced Topic

## Checked and Unchecked Conversions

C# provides special keywords for marking a code block to indicate what should happen if the target data type is too small to contain the assigned data. By default, if the target data type cannot contain the assigned data, the data will truncate during assignment. For an example, see Listing 2.21.

**LISTING 2.21: Overflowing an Integer Value**

```csharp
class Program
{
 static void Main()
 {
// int.MaxValue equals 2147483647
int n = int.MaxValue;
n = n + 1;
System.Console.WriteLine(n);
 }
}
```

Output 2.14 shows the results.

**OUTPUT 2.14**

-2147483648

Listing 2.21 writes the value -2147483648 to the console. However, placing the code within a checked block, or using the checked option when running the compiler, will cause the runtime to throw an exception of type System.OverflowException. The syntax for a checked block uses the checked keyword, as shown in Listing 2.22.

**LISTING 2.22: A Checked Block Example**

```csharp
class Program
{
    static void Main()
    {
        checked
        {
            // int.MaxValue equals 2147483647
            int n = int.MaxValue;
            n = n + 1 ;
            System.Console.WriteLine(n);
        }
    }
}
```

Output 2.15 shows the results.

**OUTPUT 2.15**

```
Unhandled Exception: System.OverflowException: Arithmetic operation
resulted in an overflow at Program.Main() in ...Program.cs:line 12
```

The result is that an exception is thrown if, within the checked block, an overflow assignment occurs at runtime.

The C# compiler provides a command-line option for changing the default checked behavior from unchecked to checked. C# also supports an unchecked block that overflows the data instead of throwing an exception for assignments within the block (see Listing 2.23).

**LISTING 2.23: An Unchecked Block Example**

```csharp
using System;

class Program
{
    static void Main()
    {
        unchecked
        {
            // int.MaxValue equals 2147483647
            int n = int.MaxValue;
            n = n + 1 ;
            System.Console.WriteLine(n);
        }
    }
}
```

Output 2.16 shows the results.

**OUTPUT 2.16**

-2147483648

Even if the checked option is on during compilation, the unchecked keyword in the preceding code will prevent the runtime from throwing an exception during execution.

Readers might wonder why, when adding 1 to int.MaxValue unchecked, the result yields -2147483648. The behavior is caused by wraparound semantics. The binary representation of int.MaxValue is 01111111111111111111111111111111, where the first digit (0) indicates a positive value. Incrementing this value yields the next value of 10000000000000000000000000000000, the smallest integer (int.MinValue), where the first digit (1) signifies the number is negative. Adding 1 to int.MinValue would result in 10000000000000000000000000000001 (-2147483647) and so on.

You cannot convert any type to any other type simply because you designate the conversion explicitly using the cast operator. The compiler will still check that the operation is valid. For example, you cannot convert a long to a bool. No such conversion is defined, and therefore, the compiler does not allow such a cast.

> **Language Contrast: Converting Numbers to Booleans**
>
> It may be surprising to learn that there is no valid cast from a numeric type to a Boolean type, since this is common in many other languages. The reason no such conversion exists in C# is to avoid any ambiguity, such as whether -1 corresponds to true or false. More important, as you will see in the next chapter, this constraint reduces the chance of using the assignment operator in place of the equality operator (e.g., avoiding if(x=42){...} when if(x==42){...} was intended).

## Implicit Conversion

In other instances, such as when going from an int type to a long type, there is no loss of precision, and no fundamental change in the value of the type occurs. In these cases, the code needs to specify only the assignment operator; the conversion is **implicit**. In other words, the compiler is able
