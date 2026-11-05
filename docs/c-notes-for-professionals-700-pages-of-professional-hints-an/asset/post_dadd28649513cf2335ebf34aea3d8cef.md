
### Section 1.4: Creating a new program using Mono

First install Mono by going through the install instructions for the platform of your choice as described in their installation section.

Mono is available for Mac OS X, Windows and Linux.

After installation is done, create a text file, name it HelloWorld.cs and copy the following content into it:

```csharp
public class Program
{
    public static void Main()
    {
        System.Console.WriteLine("Hello, world!");
        System.Console.WriteLine("Press any key to exit...");
        System.Console.Read();
    }
}
```

If you are using Windows, run the Mono Command Prompt which is included in the Mono installation and ensures that the necessary environment variables are set. If on Mac or Linux, open a new terminal.

To compile the newly created file, run the following command in the directory containing HelloWorld.cs:

```
mcs -out:HelloWorld.exe HelloWorld.cs
```

The resulting HelloWorld.exe can then be executed with:

```
mono HelloWorld.exe
```

which will produce the output:

```
Hello, world!
Press any key to exit..
```

### Section 1.5: Creating a new query using LinqPad

LinqPad is a great tool that allows you to learn and test features of .Net languages (C#, F# and VB.Net.)

- 1. Install LinqPad
- 2. Create a new Query (Ctrl + N)

![](img/5da9b5c72747b887ec63f57c832400bf_32_0.png)

- 3. Under language, select "C# statements"

![](img/5da9b5c72747b887ec63f57c832400bf_32_1.png)

- 4. Type the following code and hit run (F5)

```csharp
string hw = "Hello World";

hw.Dump(); //or Console.WriteLine(hw);
```

![](img/5da9b5c72747b887ec63f57c832400bf_32_2.png)

- 5. You should see "Hello World" printed out in the results screen.

![](img/5da9b5c72747b887ec63f57c832400bf_33_0.png)

- 6. Now that you have created your first .Net program, go and check out the samples included in LinqPad via the "Samples" browser. There are many great examples that will show you many different features of the .Net languages.

![](img/5da9b5c72747b887ec63f57c832400bf_33_1.png)

### Notes:

- 1. If you click on "IL", you can inspect the IL code that your .net code generates. This is a great learning tool.

![](img/5da9b5c72747b887ec63f57c832400bf_34_0.png)

- 2. When using LINQ to SQL or Linq to Entities you can inspect the SQL that’s being generated which is another great way to learn about LINQ.

### Section 1.6: Creating a new project using Xamarin Studio

- 1. Download and install Xamarin Studio Community.
- 2. Open Xamarin Studio.
- 3. Click **File** → **New** → **Solution**.

![](img/5da9b5c72747b887ec63f57c832400bf_35_0.png)

- 4. Click .NET → Console Project and choose C#.
- 5. Click Next to proceed.

**Choose a template for your new project**

- Multiplatform
  - App
  - Library
  - Tests
- Android
  - App
  - Library
  - Tests
- Other
  - .NET
  - ASP.NET
  - Miscellaneous

- Console Project
- Empty Project
- Gtk# 2.0 Project
- Library
- NUnit Library Project

**Console Project**

Creates a new C# console project.

![](img/5da9b5c72747b887ec63f57c832400bf_36_0.png)

- 6. Enter the Project Name and Browse... for a Location to Save and then click Create.

![](img/5da9b5c72747b887ec63f57c832400bf_37_0.png)

- 7. The newly created project will look similar to:

![](img/5da9b5c72747b887ec63f57c832400bf_37_1.png)

- 8. This is the code in the Text Editor:

```csharp
using System;

namespace FirstCsharp
{
    public class MainClass
    {
        public static void Main(string[] args)
        {
            Console.WriteLine("Hello World!");
            Console.ReadLine();
        }
    }
}
```

- 9. To run the code, press F5 or click the Play Button as shown below:

![](img/5da9b5c72747b887ec63f57c832400bf_38_0.png)

- 10. Following is the Output:

![](img/5da9b5c72747b887ec63f57c832400bf_39_0.png)

## Chapter 2: Literals

### Section 2.1: uint literals

`uint` literals are defined by using the suffix U or u, or by using an integral values within the range of `uint`:

```csharp
uint u1 = 5U;
```

### Section 2.2: int literals

`int` literals are defined by simply using integral values within the range of `int`:

```csharp
int i = 5;
```

### Section 2.3: sbyte literals

`sbyte` type has no literal suffix. Integer literals are implicitly converted from `int`:

```csharp
sbyte sb = 127;
```

### Section 2.4: decimal literals

`decimal` literals are defined by using the suffix M or m on a real number:

```csharp
decimal m = 30.5M;
```

### Section 2.5: double literals

`double` literals are defined by using the suffix D or d, or by using a real number:

```csharp
double d = 30.5D;
```

### Section 2.6: float literals

`float` literals are defined by using the suffix F or f, or by using a real number:

```csharp
float f = 30.5F;
```

### Section 2.7: long literals

`long` literals are defined by using the suffix L or l, or by using an integral values within the range of `long`:

```csharp
long l = 5L;
```

### Section 2.8: ulong literal

`ulong` literals are defined by using the suffix UL, ul, Ul, uL, LU, lu, Lu, or lU, or by using an integral values within the range of `ulong`:

```csharp
ulong ul = 5UL;
```

### Section 2.9: string literals

string literals are defined by wrapping the value with double-quotes ":

```csharp
string s = "hello, this is a string literal";
```

String literals may contain escape sequences. See String Escape Sequences

Additionally, C# supports verbatim string literals (See Verbatim Strings). These are defined by wrapping the value with double-quotes ", and prepending it with @. Escape sequences are ignored in verbatim string literals, and all whitespace characters are included:

```csharp
string s = @"The path is:
C:\Windows\System32";
//The backslashes and newline are included in the string
```

### Section 2.10: char literals

char literals are defined by wrapping the value with single-quotes ':

```csharp
char c = 'h';
```

Character literals may contain escape sequences. See String Escape Sequences

A character literal must be exactly one character long (after all escape sequences have been evaluated). Empty character literals are not valid. The default character (returned by default(char) or new char()) is '\0', or the NULL character (not to be confused with the null literal and null references).

### Section 2.11: byte literals

byte type has no literal suffix. Integer literals are implicitly converted from int:

```csharp
byte b = 127;
```

### Section 2.12: short literal

short type has no literal. Integer literals are implicitly converted from int:

```csharp
short s = 127;
```

### Section 2.13: ushort literal

ushort type has no literal suffix. Integer literals are implicitly converted from int:

```csharp
ushort us = 127;
```

### Section 2.14: bool literals

bool literals are either true or false;

```csharp
bool b = true;
```

Version ≥ 7.0

Overloading of the `is` operator was introduced with the pattern matching mechanism of C# 7.0. For details see Pattern Matching

Given a type Cartesian defined as follows

```csharp
public class Cartesian
{
    public int X { get; }
    public int Y { get; }
}
```

An overloadable operator `is` could e.g. be defined for Polar coordinates

```csharp
public static class Polar
{
    public static bool operator is(Cartesian c, out double R, out double Theta)
    {
        R = Math.Sqrt(c.X*c.X + c.Y*c.Y);
        Theta = Math.Atan2(c.Y, c.X);
        return c.X != 0 || c.Y != 0;
    }
}
```

which can be used like this

```csharp
var c = Cartesian(3, 4);
if (c is Polar(var R, *))
{
    Console.WriteLine(R);
}
```

(The example is taken from the Roslyn Pattern Matching Documentation)

### Section 3.2: Overloading equality operators

Overloading just equality operators is not enough. Under different circumstances, all of the following can be called:

- 1. object.Equals and object.GetHashCode
- 2. IEquatable<T>.Equals (optional, allows avoiding boxing)
- 3. operator == and operator != (optional, allows using operators)

When overriding Equals, GetHashCode must also be overridden. When implementing Equals, there are many special cases: comparing to objects of a different type, comparing to self etc.

When NOT overridden, Equals method and == operator behave differently for classes and structs. For classes just references are compared, and for structs values of properties are compared via reflection what can negatively affect performance. == cannot be used for comparing structs unless it is overridden.

Generally equality operation must obey the following rules:

- Must not throw exceptions.
- Reflexivity: A always equals A (may not be true for NULL values in some systems).
- Transitivity: if A equals B, and B equals C, then A equals C.
- If A equals B, then A and B have equal hash codes.
