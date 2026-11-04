tially say, “I know this conversion might cause loss of information, but for my purposes here, that’s fine.” Suppose you create a method Square that calculates the square of an int argument. To call Square with the whole part of a double argument named doubleValue, you’d write Square((int) doubleValue). This method call explicitly casts (converts) the value of doubleValue to an integer for use in method Square. Thus, if doubleValue’s value is 4.5, the method receives the value 4 and returns 16, not 20.25.

> **Common Programming Error 7.8**
> Converting a simple-type value to a value of another simple type may change the value if the promotion is not allowed. For example, converting a floating-point value to an integral value may introduce truncation errors (loss of the fractional part) in the result.

# 7.7 The .NET Framework Class Library

Many predefined classes are grouped into categories of related classes called namespaces. Together, these namespaces are referred to as the .NET Framework Class Library.

# *using* Directives and Namespaces

Throughout the text, using directives allow us to use library classes from the Framework Class Library without specifying their namespace names. For example, an app would include the declaration

```
```
using System;
```
```

in order to use the class names from the System namespace without fully qualifying their names. This allows you to use the unqualified name Console, rather than the fully qualified name System.Console, in your code.

> **Software Engineering Observation 7.3**
> The C# compiler does not require using declarations in a source-code file if the fully qualified class name is specified every time a class name is used. Many programmers prefer the more concise programming style enabled by using declarations.

You might have noticed in each project containing multiple classes that in each class’s source-code file we did not need additional using directives to use the other classes in the project. There’s a special relationship between classes in a project—by default, such classes are in the same namespace and can be used by other classes in the project. Thus, a using declaration is not required when one class in a project uses another in the same project—such as when class AccountTest used class Account in Chapter 4’s examples. Also, any classes that are not explicitly placed in a namespace are implicitly placed in the so-called global namespace.

# .NET Namespaces

A strength of C# is the large number of classes in the namespaces of the .NET Framework Class Library. Some key Framework Class Library namespaces are described in Fig. 7.4, which represents only a small portion of the reusable classes in the .NET Framework Class Library.