
Ultimately, the intended recipient of the exception is the programmer writing code that calls your API—possibly incorrectly. Therefore, you should provide as much information to her that indicates both what the programmer did wrong and—perhaps more important—how to fix it. The exception type is a critical piece of the communication mechanism. Therefore, you must choose the type carefully.

### BEGINNER TOPIC

### Checked and Unchecked Conversions

As we first discussed in a Chapter 2 Advanced Topic, C# provides special keywords for marking a code block with instructions to the runtime for what should happen if the target data type is too small to contain the assigned data. By default, if the target data type cannot contain the assigned data, the data will truncate during assignment. For an example, see Listing 11.7.

**LISTING 11.7:** Overflowing an Integer Value

```csharp
using System;

public class Program
{
    public static void Main()
    {
        // int.MaxValue equals 2147483647
        int n = int.MaxValue;
        n = n + 1;
        System.Console.WriteLine(n);
    }
}
```

The results of Listing 11.7 appear in Output 11.1.

**OUTPUT 11.1**

`-2147483648`

The code in Listing 11.7 writes the value -2147483648 to the console. However, placing the code within a checked block or using the checked option when running the compiler will cause the runtime to throw an exception of type `System.OverflowException`. The syntax for a checked block uses the `checked` keyword, as shown in Listing 11.8.

### Rethrowing a Wrapped Exception

**LISTING 11.8: A Checked Block Example**

```csharp
using System;

public class Program
{
    public static void Main()
    {
        checked
        {
            // int.MaxValue equals 2147483647
            int n = int.MaxValue;
            n = n + 1;
            System.Console.WriteLine(n);
        }
    }
}
```

If the calculation involves only constants, the calculation will be checked by default. The results of Listing 11.8 appear in Output 11.2.

**OUTPUT 11.2**

```
Unhandled Exception: System.OverflowException: Arithmetic operation
resulted in an overflow. at Program.Main() in ...Program.cs:line 12
```

In addition, depending on the version of Windows and whether a debugger is installed, a dialog may appear that prompts the user to send an error message to Microsoft, check for a solution, or debug the application. Also, the location information (Program.cs:line X) will appear only in debug compilations—that is, compilations using the /Debug option of the Microsoft csc.exe compiler. The result is that an exception is thrown if, within the checked block, an overflow assignment occurs at runtime.

The C# compiler provides a command-line option for changing the default checked behavior from unchecked to checked. C# also supports an unchecked block that truncates the data instead of throwing an exception for assignments within the block (see Listing 11.9).

**LISTING 11.9: An Unchecked Block Example**

```csharp
using System;

public class Program
{
    public static void Main()
    {
        unchecked
        {
            // int.MaxValue equals 2147483647
            int n = int.MaxValue;
            n = n + 1;
            System.Console.WriteLine(n);
        }
    }
}
```

The results of Listing 11.9 appear in Output 11.3.

**OUTPUT 11.3**

`-2147483648`

Even if the checked option is on during compilation, the unchecked keyword in the code in Listing 11.9 will prevent the runtime from throwing an exception during execution.

Equivalent checked and unchecked expressions are available for cases where statements are not allowed. For example, a field initializer may consist of an expression rather than a statement:

```csharp
int _Number = unchecked(int.MaxValue + 1);
```

## SUMMARY

Throwing an exception causes a significant performance hit. A single exception causes lots of runtime stack information to be loaded and processed—data that would not otherwise be loaded—and it takes a considerable amount of time to handle. As pointed out in Chapter 5, you should use exceptions only to handle exceptional circumstances; APIs should provide mechanisms to check whether an exception will be thrown instead of forcing a particular API to be called to determine whether an exception will be thrown.

The next chapter introduces generics—a C# 2.0 feature that significantly enhances code written in C# 1.0. In fact, it essentially deprecates any use of the System.Collections namespace, which was formerly used in nearly every project.

## 12 Generics

AS YOUR PROJECTS BECOME MORE SOPHISTICATED, you will need a better way to reuse and customize existing software. To facilitate code reuse, especially the reuse of algorithms, C# includes a feature called **generics**. Just as methods are powerful because they can take arguments, so types and methods that take type arguments have significantly more functionality.

Generics are lexically like generic types in Java and templates in C++. In all three languages, these features enable the implementation of algorithms and patterns once, rather than requiring separate implementations for each type the algorithm or pattern operates on. However, C# generics are very different from both Java generics and C++ templates in the details of their implementation and impact on the type system of their respective languages. Generics were added to the runtime and C# in version 2.0.

![](img/ef6a8a417630b222bfb3f3b949facff0_523_0.png)

### C# without Generics

We begin the discussion of generics by examining a class that does not use generics. This class, `System.Collections.Stack`, represents a collection of objects such that the last item to be added to the collection is the first item retrieved from the collection (last in, first out [LIFO]). Push() and Pop(), the two main methods of the Stack class, add items to the stack and remove them from the stack, respectively. The declarations for the methods on the Stack class appear in Listing 12.1.

**LISTING 12.1: The System.Collections.Stack Method Signatures**

```csharp
public class Stack
{
    public virtual object Pop() { ... }
    public virtual void Push(object obj) { ... }
    // ...
}
```

Programs frequently use stack type collections to facilitate multiple undo operations. For example, Listing 12.2 uses the System.Collections.Stack class for undo operations within a program that simulates the Etch A Sketch game.

**LISTING 12.2: Supporting Undo in a Program Similar to the Etch A Sketch Game**

```csharp
using System;
using System.Collections;

class Program
{
    // ...
    public void Sketch()
    {
        Stack path = new Stack();
        Cell currentPosition;
        ConsoleKeyInfo key; // Added in C# 2.0
        do
        {
            // Etch in the direction indicated by the
            // arrow keys that the user enters
            key = Move();
            switch (key.Key)
            {
                case ConsoleKey.Z:
                    // Undo the previous Move
                    if (path.Count >= 1)
                    {
                        currentPosition = (Cell)path.Pop();
                        Console.SetCursorPosition(
                            currentPosition.X, currentPosition.Y);
                        Undo();
                    }
                    break;

                case ConsoleKey.DownArrow:
                case ConsoleKey.UpArrow:
                case ConsoleKey.LeftArrow:
                case ConsoleKey.RightArrow:
                    // SaveState()
                    currentPosition = new Cell(
                        Console.CursorLeft, Console.CursorTop);
                    path.Push(currentPosition);
                    break;

                default:
                    Console.Beep(); // Added in C# 2.0
                    break;
            }
        }
        while (key.Key != ConsoleKey.X); // Use X to quit
    }

    public struct Cell
    {
        // Use read-only field prior to C# 6.0
        public int X { get; }
        public int Y { get; }
        public Cell(int x, int y)
        {
            X = x;
            Y = y;
        }
    }
}
```

The results of Listing 12.2 appear in Output 12.1.

**OUTPUT 12.1**

![](img/ef6a8a417630b222bfb3f3b949facff0_526_0.png)

Using the variable *path*, which is declared as a `System.Collections.Stack`, you save the previous move by passing a custom type, `Cell`, into the `Stack.Push()` method using `path.Push(currentPosition)`. If the user enters a Z (or presses Ctrl+Z), you undo the previous move by retrieving it from the stack using a `Pop()` method, setting the cursor position to be the previous position, and calling `Undo()`.

Although this code is functional, there is a fundamental shortcoming in the `System.Collections.Stack` class. As shown in Listing 12.1, the `Stack` class collects values of type `object`. Because every object in the Common Language Runtime (CLR) derives from `object`, `Stack` provides no validation that the elements you place into it are homogenous or are of the intended type. For example, instead of passing `currentPosition`, you can pass a *string* in which X and Y are concatenated with a decimal point between them. However, the compiler must allow the inconsistent data types because the stack class is written to take any object, regardless of its more specific type.

Furthermore, when retrieving the data from the stack using the `Pop()` method, you must cast the return value to a `Cell`. But if the type of the value returned from the `Pop()` method is not `Cell`, an exception is thrown. By deferring type checking until runtime by using a cast, you make the
