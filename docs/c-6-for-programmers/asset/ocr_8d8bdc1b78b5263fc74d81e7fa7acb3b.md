# 3.2.2 using Directive

Line 3

```
using System;
```

is a using directive that tells the compiler where to look for a class that's used in this app. A great strength of Visual C# is its rich set of predefined classes that you can reuse rather than "reinventing the wheel." These classes are organized under namespaces—named collections of related classes. Collectively, .NET's predefined namespaces are known as .NET Framework Class Library. Each using directive identifies a namespace containing classes that a C# app should be able to use. The using directive in line 3 indicates that this example intends to use classes from the System namespace, which contains the predefined Console class (discussed shortly) used in line 10, and many other useful classes.

![](bbox=[0.18, 0.36, 0.24, 0.44])

> Error-Prevention Tip 3.2
> Forgetting to include a using directive for a namespace that contains a class used in your app typically results in a compilation error, containing a message such as "The name 'Console' does not exist in the current context." When this occurs, check that you provided the proper using directives and that the names in them are spelled correctly, including proper use of uppercase and lowercase letters. In the editor, when you hover over an error's red squiggly line, Visual Studio displays a box containing the link "Show potential fixes." If a using directive is missing, one potential fix shown is to add the using directive to your code—simply click that fix to have Visual Studio edit your code.

For each new .NET class we use, we indicate the namespace in which it's located. This information is important, because it helps you locate descriptions of each class in the .NET documentation. A web-based version of this documentation can be found at

```
https://msdn.microsoft.com/library/w0x726c2
```

This also can be accessed via the Help menu. You can click the name of any .NET class or method, then press the F1 key to get more information. Finally, you can learn about the contents of a given namespace by going to

```
https://msdn.microsoft.com/namespace
```

So

```
https://msdn.microsoft.com/System
```

takes you to namespace System's documentation.

# 3.2.3 Blank Lines and Whitespace

Line 4 is simply a blank line. Blank lines and space characters make code easier to read, and together with tab characters are known as whitespace. Space characters and tabs are known specifically as whitespace characters. Whitespace is ignored by the compiler.

# 3.2.4 Class Declaration

Line 5

```
class Welcome1
```