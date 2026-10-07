
# Rethrowing a Wrapped Exception 621

To change an entire project to be unchecked or checked, set the CheckForOverflowUnder property to false or true, respectively.

```xml
<PropertyGroup>
  <CheckForOverflowUnder>true</CheckForOverflowUnder>
</PropertyGroup>
```

C# also supports an unchecked block that truncates the data instead of throwing an exception for the block (see Listing 11.8 with Output 11.3).

# Listing 11.8: An Unchecked Block Example

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
            Console.WriteLine(n);
        }
    }
}
```

# OUTPUT 11.3

```
-2147483648
```

Even if the checked option is on during compilation, the unchecked keyword in the code in Listing 11.8 will prevent the runtime from throwing an exception during execution.

Equivalent checked and unchecked expressions are available for cases where statements are not allowed. For example, a field initializer may consist of an expression rather than a statement:

```csharp
int number = unchecked(int.MaxValue + 1);
```

# Summary

Throwing an exception produces a significant performance hit. A single exception causes lots of runtime stack information to be loaded and processed—data that would not otherwise be loaded—and it takes a considerable amount of time to handle. As pointed out in Chapter 5, you should use exceptions only to handle exceptional circumstances; APIs should provide mechanisms to check whether an exception will be thrown instead of forcing a particular API to be called to determine whether an exception will be thrown.

The next chapter introduces generics.¹10 In fact, it essentially deprecates any use of the System.Collections namespace, which was formerly used in nearly every project.

+ 10. A feature starting in C# 2.0.

# 12 Generics

As your projects become more sophisticated, you will need a better way to reuse and customize existing software. To facilitate code reuse, especially, C# includes a feature called generics.

Generics are lexically like generic types in Java and templates in C++. In all three languages, these features enable the implementation of algorithms and patterns once, rather than requiring separate implementations for each type that the algorithm or pattern operates on. However, C# generics are very different from both Java generics and C++ templates in the details of their implementation and impact on the type system of their respective languages. Just as methods are powerful because they can take arguments, so types and methods that take arguments have significantly more functionality.

![](img/ffe0f34eac7523830420733690014d17_657_0.png)

Generics were added to the runtime and C# in version 2.0.

# C# without Generics

We begin the discussion of generics by examining a class that does not use generics. This class, System.Collections.Stack, represents a collection of objects such that the last item to be added to the collection is the first item retrieved from the collection (last in, first out [LIFO]). Push() and Pop(), the two main methods of the Stack class, add items to the stack and remove them from the stack, respectively. The declarations for the methods on the Stack class appear in Listing 12.1.

Listing 12.1: The System.Collections.Stack Method Signatures

```csharp
public class Stack
{
    public virtual object Pop()
    {
        // ...
    }
    public virtual void Push(object obj)
    {
        // ...
    }
}
```

Programs frequently use stack type collections to facilitate multiple undo operations. For example, Listing 12.2, with results shown in Output 12.1, uses the System.Collections.Stack class for undo operations within a program that simulates an Etch A Sketch toy.

Listing 12.2: Supporting Undo in a Program Similar to an Etch A Sketch Toy

```csharp
using System.Collections.Generic;

public class Program
{
    // ...
    public static void Sketch()
    {
        Stack<Cell> path = new();
    }
```

```csharp
Cell currentPosition;
ConsoleInfo key;
// ...

do {
    // Etch in the direction indicated by the
    // arrow keys that the user enters
    key = Move();

    switch(key.Key) {
        case ConsoleKey.Z:
            // Undo the previous Move
            if(path.Count >= 1)
            {
                currentPosition = (Cell)path.Pop();
                Console.SetCursorPosition(
                    currentPosition.X, currentPosition.Y
                    // ...
                );
                Undo();
            }
            break;
        case ConsoleKey.DownArrow:
            // ...
        case ConsoleKey.UpArrow:
            // ...
        case ConsoleKey.LeftArrow:
            // ...
        case ConsoleKey.RightArrow:
            // SaveState();
            if(Console.CursorLeft < Console.WindowWidth - 2)
            {
                currentPosition = new Cell(
                    Console.CursorLeft + 1, Console.CursorTop);
            }
            path.Push(currentPosition);
            // ...
            break;

        default:
            Console.Beep();
            break;
    }
} while(key.Key != ConsoleKey.X); // Use X to quit.
```

# 626 Chapter 12: Generics

```csharp
// ...
}
public struct Cell
{
    public int X { get; }
    public int Y { get; }

    public Cell(int x, int y)
    {
        X = x;
        Y = y;
    }
```

OUTPUT 12.1

![](img/ffe0f34eac7523830420733690014d17_660_0.png)

Using the variable path, which is declared as a System.Collections.Stack, you save the previous move by passing a custom type, Cell, into the Stack.Push() method using path.Push(currentPosition). If the user enters a Z (or presses Ctrl+Z), you undo the previous move by retrieving it from the stack using a Pop(), setting the cursor position to be the previous position, and calling Undo().

Although this code is functional, the System.Collections.Stack class has a fundamental shortcoming. As shown in Listing 12.1, the Stack class collects values of type object. Because every object in the Common Language Runtime (CLR) derives from object. Stack provides no validation that the elements you place into it are homogenous or of the intended type. For, instead of passing currentPosition, you can pass a string where X and Y are concatenated with a decimal point between them. However, the compiler must allow the inconsistent data types because the stack class is written to take any object, regardless of its more specific type.

Furthermore, when retrieving the data from the stack using the Pop() method, you must cast the return value to a Cell. But if the type of the value returned from the Pop() method is not Cell, an exception is thrown. By deferring checking until runtime by using a cast, you make the program more brittle. The fundamental problem with creating classes that can work with multiple data types without generics is they must work with a common base class (or interface), usually object.

Using value types, as a struct or an integer, with classes that use object exacerbates the problem. If you pass a value to the Stack.Push() method, for example, the runtime automatically boxes it. Similarly, when you retrieve a value, you need to unbox the data and the object reference you obtain from the Pop() method into a value type. Casting a reference to a base class or interface has a negligible performance impact, but the box operation for a value type introduces more overhead, because it must allocate memory, copy the value, and then later garbage-collect that memory.

C# is a language that encourages type safety: The language is designed so that many errors, such as assigning an integer to a variable of type string, can be caught at compile time. The fundamental problem is that the Stack class is not type-safe as one expects a C# program to be. To change the Stack class to enforce type safety by restricting the contents of the stack to a particular data type (without using generics), you must create a specialized stack class, as in Listing 12.3.

# 12.3: Defining a Specialized Stack Class

```csharp
public class CellStack
{
    public Cell Pop() { return new Cell(); } // would return
    // that last cell
}
```