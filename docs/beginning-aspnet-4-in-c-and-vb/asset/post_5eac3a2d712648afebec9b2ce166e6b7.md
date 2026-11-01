
## Variable Scope

The scope of a variable is the region of code from which the variable can be accessed. In general, the scope is determined by the following rules:

- A field (also known as a member variable) of a class is in scope for as long as its containing class is in scope.
- A local variable is in scope until a closing brace indicates the end of the block statement or method in which it was declared.
- A local variable that is declared in a for, while, or similar statement is in scope in the body of that loop.

### Scope Clashes for Local Variables

It's common in a large program to use the same variable name for different variables in different parts of the program. This is fine as long as the variables are scoped to completely different parts of the program so that there is no possibility for ambiguity. However, bear in mind that local variables with the same name can't be declared twice in the same scope. For example, you can't do this:

```
int x = 20;
// some more code
int x = 30;
```

Consider the following code sample:

```
using System;
namespace Wrox.ProCSharp.Basics
{
    public class ScopeTest
    {
        public static int Main()
        {
            for (int i = 0; i < 10; i++)
            {
                Console.WriteLine(i);
            } // i goes out of scope here
            // We can declare a variable named i again, because
            // there's no other variable with that name in scope
            for (int i = 9; i >= 0; i--)
            {
                Console.WriteLine(i);
            } // i goes out of scope here.
            return 0;
        }
    }
}
```

code snippet Scope.cs

This code simply prints out the numbers from 0 to 9, and then back again from 9 to 0, using two for loops. The important thing to note is that you declare the variable i twice in this code, within the same method. You can do this because i is declared in two separate loops, so each i variable is local to its own loop.

The next few sections look in detail at the syntax for value and reference types. Conceptually, the difference is that a value type stores its value directly, whereas a reference type stores a reference to the value.

These types are stored in different places in memory; value types are stored in an area known as the stack, and reference types are stored in an area known as the managed heap. It is important to be aware of whether a type is a value type or a reference type because of the different effect each assignment has.

For example, int is a value type, which means that the following statement will result in two locations in memory storing the value 20:

```
// i and j are both of type int
 i = 20;
 j = i;
```

However, consider the following code. For this code, assume that you have defined a class called Vector. Assume that Vector is a reference type and has an int member variable called Value:

```
Vector x, y;
 x = new Vector();
 x.Value = 30; // Value is a field defined in Vector class
 y = x;
 Console.WriteLine(y.Value);
 y.Value = 50;
 Console.WriteLine(x.Value);
```

The crucial point to understand is that after executing this code, there is only one Vector object around. x and y both point to the memory location that contains this object. Because x and y are variables of a reference type, declaring each variable simply reserves a reference — it doesn't instantiate an object of the given type. In neither case is an object actually created. To create an object, you have to use the new keyword, as shown. Because x and y refer to the same object, changes made to x will affect y and vice versa. Hence the code will display 30 and then 50.

> C++ developers should note that this syntax is like a reference, not a pointer. You use the . notation, not ->, to access object members. Syntactically, C# references look more like C++ reference variables. However, behind the superficial syntax, the real similarity is with C++ pointers.

If a variable is a reference, it is possible to indicate that it does not refer to any object by setting its value to null:

```
y = null;
```

If a reference is set to null, then clearly it is not possible to call any nonstatic member functions or fields against it; doing so would cause an exception to be thrown at runtime.

In C#, basic data types such as bool and long are value types. This means that if you declare a bool variable and assign it the value of another bool variable, you will have two separate bool values in memory. Later, if you change the value of the original bool variable, the value of the second bool variable does not change. These types are copied by value.

In contrast, most of the more complex C# data types, including classes that you yourself declare, are reference types. They are allocated upon the heap, have lifetimes that can span multiple function calls, and can be accessed through one or several aliases. The Common Language Runtime (CLR) implements an elaborate algorithm to track which reference variables are still reachable and which have been orphaned. Periodically, the CLR will destroy orphaned objects and return the memory that they once occupied back to the operating system. This is done by the garbage collector.

With .NET, a short is no longer quite so short; it is now 16 bits long. The int type is 32 bits long. The long type reserves 64 bits for values. All integer-type variables can be assigned values in decimal or in hex notation. The latter requires the 0x prefix:

```
long x = 0x12ab;
```

If there is any ambiguity about whether an integer is int, uint, long, or ulong, it will default to an int. To specify which of the other integer types the value should take, you can append one of the following characters to the number:

```
uint ui = 1234U;
long l = 1234L;
ulong ul = 1234UL;
```

You can also use lowercase u and l, although the latter could be confused with the integer 1 (one).

## Floating-Point Types

Although C# provides a plethora of integer data types, it supports floating-point types as well.

| NAME | CTS TYPE | DESCRIPTION | SIGNIFICANT FIGURES | RANGE (APPROXIMATE) |
|---|---|---|---|---|
| float | System.Single | 32-bit single-precision floating point | 7 | ±1.5 × 10⁻⁴⁵ to ±3.4 × 10³⁸ |
| double | System.Double | 64-bit double-precision floating point | 15/16 | ±5.0 × 10⁻³²⁴ to ±1.7 × 10³⁰⁸ |

The float data type is for smaller floating-point values, for which less precision is required. The double data type is bulkier than the float data type but offers twice the precision (15 digits).

If you hard-code a non-integer number (such as 12.3) in your code, the compiler will normally assume that you want the number interpreted as a double. If you want to specify that the value is a float, you append the character F (or f) to it:

```
float f = 12.3F;
```

## The Decimal Type

The decimal type represents higher-precision floating-point numbers, as shown in the following table.

| NAME | CTS TYPE | DESCRIPTION | SIGNIFICANT FIGURES | RANGE (APPROXIMATE) |
|---|---|---|---|---|
| decimal | System.Decimal | 128-bit high-precision decimal notation | 28 | ±1.0 × 10⁻²⁸ to ±7.9 × 10²⁸ |

One of the great things about the CTS and C# is the provision of a dedicated decimal type for financial calculations. How you use the 28 digits that the decimal type provides is up to you. In other words, you can track smaller dollar amounts with greater accuracy for cents or larger dollar amounts with more rounding in the fractional area. Bear in mind, however, that decimal is not implemented under the hood as a primitive type, so using decimal will have a performance effect on your calculations.

To specify that your number is a decimal type rather than a double, float, or an integer, you can append the M (or m) character to the value, as shown in the following example:

```
decimal d = 12.30M;
```
