
| Structure | Conversion Method |
|---|---|
| Decimal | static decimal Parse(string str) |
| Double | static double Parse(string str) |
| Single | static float Parse(string str) |
| Int64 | static long Parse(string str) |
| Int32 | static int Parse(string str) |
| Int16 | static short Parse(string str) |
| UInt64 | static ulong Parse(string str) |
| UInt32 | static uint Parse(string str) |
| UInt16 | static ushort Parse(string str) |
| Byte | static byte Parse(string str) |
| SByte | static sbyte Parse(string str) |

The Parse() methods will throw a FormatException if str does not contain a valid number as defined by the invoking type. ArgumentNullException is thrown if str is null, and OverflowException is thrown if the value in str exceeds the bounds of the invoking type.

The parsing methods give you an easy way to convert a numeric value, read as a string from the keyboard or a text file, into its proper internal format. For example, the following program averages a list of numbers entered by the user. It first asks the user for the number of values to be averaged. It then reads that number using ReadLine() and uses Int32.Parse() to convert the string into an integer. Next, it inputs the values, using Double.Parse() to convert the strings into their double equivalents.

```csharp
// This program averages a list of numbers entered by the user.

using System;
using System.IO;

class AvgNums {
    static void Main() {
        string str;
        int n;
        double sum = 0.0;
        double avg, t;

        Console.Write("How many numbers will you enter: ");
        str = Console.ReadLine();
        try {
            n = Int32.Parse(str);
        } catch (FormatException exc) {
            Console.WriteLine(exc.Message);
            return;
        } catch (OverflowException exc) {
            Console.WriteLine(exc.Message);
            return;
        }

        Console.WriteLine("Enter " + n + " values.");
        for(int i=0; i < n ; i++) {
          Console.Write(": ");
          str = Console.ReadLine();
          try {
            t = Double.Parse(str);
          } catch(FormatException exc) {
            Console.WriteLine(exc.Message);
            t = 0.0;
          }
          catch(OverflowException exc) {
            Console.WriteLine(exc.Message);
            t = 0;
          }
          sum += t;
        }
        avg = sum / n;
        Console.WriteLine("Average is " + avg);
    }
}
```

Here is a sample run:

```
How many numbers will you enter: 5
Enter 5 values.
: 1.1
: 2.2
: 3.3
: 4.4
: 5.5
Average is 3.3
```

One other point: You must use the right parsing method for the type of value you are trying to convert. For example, trying to use Int32.Parse() on a string that contains a floating-point value will not produce the desired result.

As explained, Parse() will throw an exception on failure. You can avoid generating an exception when converting numeric strings by using the TryParse() method, which is defined for all of the numeric structures. Here is an example. It shows one version of TryParse() as defined by Int32.

```csharp
static bool TryParse(string str, out int result)
```

The numeric string is passed in str. The result is returned in result. It performs the conversion using the default locale and numeric style. (A second version of TryParse() is available that lets you specify the numeric style and locale.) If the conversion fails, such as when str does not contain a numeric string in the proper form, TryParse() returns false. Otherwise, it returns true. Therefore, you must check the return value to confirm that a successful conversion has occurred.

## Delegates, Events, and Lambda Expressions

This chapter examines three innovative C# features: delegates, events, and lambda expressions. A delegate provides a way to encapsulate a method. An event is a notification that some action has occurred. Delegates and events are related because an event is built upon a delegate. Both expand the set of programming tasks to which C# can be applied. The lambda expression is a new syntactic feature provided by C# 3.0. It offers a streamlined, yet powerful way to define what is, essentially, a unit of executable code. Lambda expressions are often used when working with delegates and events because a delegate can refer to a lambda expression. (Lambda expressions are also very important to LINQ, which is described in Chapter 19.) Also examined are anonymous methods, covariance, contravariance, and method group conversions.

### Delegates

Let's begin by defining the term delegate. In straightforward language, a delegate is an object that can refer to a method. Therefore, when you create a delegate, you are creating an object that can hold a reference to a method. Furthermore, the method can be called through this reference. In other words, a delegate can invoke the method to which it refers. As you will see, this is a very powerful concept.

It is important to understand that the same delegate can be used to call different methods during the runtime of a program by simply changing the method to which the delegate refers. Thus, the method that will be invoked by a delegate is not determined at compile time, but rather at runtime. This is the principal advantage of a delegate.

> Note If you are familiar with C/C++, then it will help to know that a delegate in C# is similar to a function pointer in C/C++.

A delegate type is declared using the keyword delegate. The general form of a delegate declaration is shown here:

```
delegate ret-type name(parameter-list);
```

Here, ret-type is the type of value returned by the methods that the delegate will be calling. The name of the delegate is specified by name. The parameters required by the methods called through the delegate are specified in the parameter-list. Once created, a delegate instance can refer to and call methods whose return type and parameter list match those specified by the delegate declaration.

A key point to understand is that a delegate can be used to call any method that agrees with its signature and return type. Furthermore, the method can be either an instance method associated with an object or a static method associated with a class. All that matters is that the return type and signature of the method agree with those of the delegate.

To see delegates in action, let's begin with the simple example shown here:

```csharp
// A simple delegate example.

using System;

// Declare a delegate type.
delegate string StrMod(string str);

class DelegateTest {
// Replaces spaces with hyphens.
static string ReplaceSpaces(string s) {
Console.WriteLine("Replacing spaces with hyphens.");
return s.Replace(' ', '-');
}

// Remove spaces.
static string RemoveSpaces(string s) {
string temp = "";
int i;

Console.WriteLine("Removing spaces.");
for(i=0; i < s.Length; i++)
if(s[i] != ' ') temp += s[i];

return temp;
}

// Reverse a string.
static string Reverse(string s) {
string temp = "";
int i, j;

Console.WriteLine("Reversing string.");
for(j=0, i=s.Length-1; i >= 0; i--, j++)
temp += s[i];

return temp;
}

static void Main() {
// Construct a delegate.
StrMod strOp = new StrMod(ReplaceSpaces);
string str;

// Call methods through the delegate.
str = strOp("This is a test.");
Console.WriteLine("Resulting string: " + str);
Console.WriteLine();

strOp = new StrMod(RemoveSpaces);
str = strOp("This is a test.");
Console.WriteLine("Resulting string: " + str);
Console.WriteLine();

strOp = new StrMod(Reverse);
str = strOp("This is a test.");
Console.WriteLine("Resulting string: " + str);
}
}
```

The output from the program is shown here:

```
Replacing spaces with hyphens.
Resulting string: This-is-a-test.

Removing spaces.
Resulting string: Thisisatest.

Reversing string.
Resulting string: .tset a si sihT
```

Let's examine this program closely. The program declares a delegate type called StrMod, shown here:

```
delegate string StrMod(string str);
```

Notice that StrMod takes one string parameter and returns a string.

Next, in DelegateTest, three static methods are declared, each with a single parameter of type string and a return type of string. Thus, they match the StrMod delegate. These methods perform some type of string modification. Notice that ReplaceSpaces() uses one of string's methods, called Replace(), to replace spaces with hyphens.

In Main(), a StrMod reference called strOp is created and assigned a reference to ReplaceSpaces(). Pay close attention to this line:

```
StrMod strOp = new StrMod(ReplaceSpaces);
```

Notice how the method ReplaceSpaces() is passed as a parameter. Only its name is used; no parameters are specified. This can be generalized. When instantiating a delegate, you specify only the name of the method to which you want the delegate to refer. Of course, the method's signature must match that of the delegate's declaration. If it doesn't, a compile-time error will result.

Next, ReplaceSpaces() is called through the delegate instance strOp, as shown here:

```
str = strOp("This is a test.");
```

Because strOp refers to ReplaceSpaces(), ReplaceSpaces() is invoked.
