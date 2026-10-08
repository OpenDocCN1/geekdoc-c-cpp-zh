
## Common Programming Error 7.5

![](img/57baed2319be0bb1b5f98674846f2711_288_0.png)

Declaring a method outside the body of a class declaration or inside the body of another method is a syntax error.

## Common Programming Error 7.6

![](img/57baed2319be0bb1b5f98674846f2711_288_1.png)

Redaring a method parameter as a local variable in the method's body is a compilation error.

## Common Programming Error 7.7

![](img/57baed2319be0bb1b5f98674846f2711_288_2.png)

Forgetting to return a value from a method that should return one is a compilation error. If a return type other than void is specified, the method must use a return statement to return a value, and that value must be consistent with the method's return type. Returning a value from a method whose return type has been declared void is a compilation error.

## static Members Can Only Access the Class Members Directly

A static method or property can call only static methods or properties of the class directly (i.e., using the method name itself) and can manipulate only static variables in the same class. To access a non-static member, a static method or property must use a reference to an object of that class. Recall that static methods relate to a class as a whole, whereas non-static methods are associated with a specific object (instance) of the class and may manipulate the instance variables of object (as well as the class's static members).

Many objects of a class, each with its own copies of instance variables, may exist at the same time. Suppose a static method were to invoke a non-static method directly. How would the method know which object's instance variables to manipulate? What would happen if no objects of the class existed at the time the non-static method was invoked?

## Software Engineering Observation 7.3

![](img/57baed2319be0bb1b5f98674846f2711_288_3.png)

A static method cannot access non-static members of the same class directly.

## 7.6 Argument Promotion and Casting

Another important feature of method calls is argument promotion—implicitly converting an argument's value to the type that the method expects to receive (if possible) in its responding parameter. For example, an app can call Math.Sqrt with an integer argument even though the method expects to receive a double argument. The statement

```
Console.WriteLine(Math.Sqrt(4));
```

correct evaluates Math.Sqrt(4) and displays the value 2.0. Sqrt's parameter list carries C# to convert the int value 4 to the double value 4.0 before passing the value to Sqrt. Such conversions may lead to compilation errors if C#'s promotion rules are not satisfied. The promotion rules specify which conversions are allowed—that is, which can be performed without losing data. In the Sqrt example above, an int is converted to a double without changing its value. However, converting a double to an int truncates the fractional part of the double value—part of the value is lost. Double variables can hold much larger (and much smaller) than int variables, assigning a double to an int can cause a loss of information when the double value doesn't fit in the int. Converting large integers to small integer types (e.g., long to int) can also produce incorrect results.

### 7.6.1 Promotion Rules

The promotion rules apply to expressions containing values of two or more simple types and to simple-type values passed as arguments to methods. Each value is promoted to the appropriate type (Actually, the expression uses a temporary copy of each promoted value—the types of the original values remain unchanged.) Figure 7.4 shows the simple types affected and to which they can be promoted. Values of all simple types can also be implicitly converted to type object. We demonstrate implicit conversions in Chapter 19.

| Type | Conversion types |
|---|---|
| bool | no possible implicit conversions to other simple types |
| byte | ushort, short, int, uint, long, decimal, float or double |
| char | ushort, int, uint, long, decimal, float or double |
| decimal | no possible implicit conversions to other simple types |
| double | no possible implicit conversions to other simple types |
| float | double |
| int | long, decimal, float or double |
| long | decimal, float or double |
| sbyte | short, int, long, decimal, float or double |
| short | int, long, decimal, float or double |
| uint | long, long, decimal, float or double |
| long | decimal, float or double |
| ushort | int, uint, long, decimal, float or double |

> Fig. 7.4 | Explicit conversions between simple types.

### 7.6.2 Sometimes Explicit Casts Are Required

By default, to prevent a compilation error in cases where implicit conversion between simple types, the compiler requires you to use a cast operator to force the conversion. This enables you to "take control" from the compiler. This essentially say, "I know this conversion might cause loss of information, but for my purposes here, that's fine." Suppose you create a method Square that calculates the square of an int argument. To call Square with the whole part of a double argument doubleValue, you would write Square(int doubleValue). This method explicitly casts (converts) the value of doubleValue to an integer for use in Square. Thus, if doubleValue's value is 4.5, the method returns 4 and not 20.25.

## Common Programming Error 7.8

Converting a simple-type value to a value of another simple type may change the value if the promotion is not allowed. For example, converting a floating-point value to an integer may introduce truncation errors (loss of the fractional part) in the result.

## 7.7 The .NET Framework Class Library

Many defined classes are grouped into categories of classes named namespaces. Together, these namespaces are referred to as the .NET Framework Class Library.

**using Directives and Namespaces**
Throughout the text, using directives allow us to use library classes from the Framework Class Library without specifying their namespace names. For example, an app would include the declaration

```
using System;
```

in order to use the class names from the System namespace without fully qualifying their names. This allows you to use the unqualified name Console rather than the fully qualified name System.Console; in your code.

## Software Engineering Observation 7.4

The C# compiler does not require using declarations in a source-code file if the fully qualified class name is specified every time a class name is used. Most programmers prefer the more concise programming style enabled by using declarations.

![](img/57baed2319be0bb1b5f98674846f2711_290_0.png)

You might have noticed in each project containing multiple classes that each class's source-code file did not need additional using directives to use the other classes in the project. There's a special relationship between classes in a project—by default, such classes are in the same namespace and can be used by other classes in the project. Thus, a using declaration is not required when one class in a project uses another in the same project—such as when class AccountTest used class Account in Chapter 4's examples. Also, any classes that are not explicitly placed in a namespace are implicitly placed in the global namespace.

## .NET Namespaces

A strength of C# is the large number of classes in the namespaces of the .NET Framework Class Library. Some key Framework Library namespaces are described in Fig. 7.5, which represents only a small portion of the classes in the .NET Class Library.

## 7.7 The .NET Framework Class Library

| Namespace | Description |
|---|---|
| System.Windows.Forms | Contains the classes required to create and manipulate GUIs. (Various classes in this namespace are discussed in Chapter 14, Graphical Interfaces with Forms: Part 1, and Chapter 15, Graphical Interfaces with Forms: Part 2.) |
| System.Windows.Controls System.Windows.Input System.Windows.Media System.Windows.Shapes | Contains the classes of Presentation Foundation for GUIs, 2-D and 3-D graphics, multimedia and animation. (See the online classes.) |
| System.Linq | Contains the classes that support Language Integrated Query (LINQ). (See Chapter 9, Introduction to LINQ and several other chapters throughout the book.) |
| System.Data.Entity | Contains the classes for manipulating data in databases (i.e., organized collections of data), including support for LINQ to Entities. (See Chapter 22, Databases and LINQ.) |
| System.IO | Contains the classes that enable programs to output data. (See Chapter 17, Files and Streams.) |
| System.Web | Contains the classes used for creating and maintaining web apps, which are accessible over the Internet. (See the online ASP.NET Web App chapter.) |
| System.Xml | Contains the classes for creating and manipulating XML data. Data can be read or written to XML files. (See the online XML and LINQ to XML chapter.) |
| System.Xml.Linq | Contains the classes that support Language Integrated Query (LINQ) for XML documents. (See the online XML and LINQ to XML chapter, and other chapters throughout the book.) |
| System.Collections.Generic | Contains the classes that define data structures for maintaining collections. (See Chapter 21, Generic Collections; Functional Programming with LINQ/PLINQ.) |
| System.Text | Contains the classes that enable programs to manipulate characters and strings. (See Chapter 16, Strings and Characters: A Deeper Look.) |

> Fig. 7.5 | .NET Framework Class Library namespaces (a subset).

# Locating Additional Information about .NET Class's Methods

You can locate additional information about a .NET class methods in the .NET Framework Class Library reference

```
https://msdn.microsoft.com/library/mt472912
```

When you visit this site, you will see an alphabetical listing of all the namespaces in the Framework Class Library. Locate the namespace and click its link to see an alphabetical listing of all its classes, with a brief description of each. Click a class's link to see more
