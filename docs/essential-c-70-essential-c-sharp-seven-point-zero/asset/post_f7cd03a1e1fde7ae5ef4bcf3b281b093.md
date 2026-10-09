
program more brittle. The fundamental problem with creating classes that can work with multiple data types without generics is that they must work with a common base class (or interface), usually object.

Using value types, such as a struct or an integer, with classes that use object exacerbates the problem. If you pass a value type to the Stack.Push() method, for example, the runtime automatically boxes it. Similarly, when you retrieve a value type, you need to explicitly unbox the data and cast the object reference you obtain from the Pop() method into a value type. Casting a reference type to a base class or interface has a negligible performance impact, but the box operation for a value type introduces more overhead, because it must allocate memory, copy the value, and then later garbage-collect that memory.

C# is a language that encourages type safety: The language is designed so that many type errors, such as assigning an integer to a variable of type string, can be caught at compile time. The fundamental problem is that the Stack class is not as type-safe as one expects a C# program to be. To change the Stack class to enforce type safety to restrict the contents of the stack to be a particular data type (without using generic types), you must create a specialized stack class, as in Listing 12.3.

## LISTING 12.3: Defining a Specialized Stack Class

```csharp
public class CellStack
{
    public virtual Cell Pop();
    public virtual void Push(Cell cell);
    // ...
}
```

Because CellStack can store only objects of type Cell, this solution requires a custom implementation of the stack methods, which is less than ideal. Implementing a type-safe stack of integers would require yet another custom implementation; each implementation would look remarkably like every other one. There would be lots of duplicated, redundant code.

## BEGINNER TOPIC

### Another Example: Nullable Value Types

Chapter 3 introduced the capability of declaring variables that could contain null by using the nullable modifier, `?`, when declaring a value type variable. C# began supporting this functionality only in version 2.0 because the right implementation required generics. Prior to the introduction of generics, programmers faced essentially two options.

The first option was to declare a nullable data type for each value type that needs to handle null values, as shown in Listing 12.4.

## LISTING 12.4: Declaring Versions of Various Value Types That Store null

```csharp
struct NullableInt
{
    /// <summary>
    /// Provides the value when HasValue returns true
    /// </summary>
    public int Value { get; private set; }

    /// <summary>
    /// Indicates whether there is a value or whether
    /// the value is "null"
    /// </summary>
    public bool HasValue { get; private set; }

    // ...
}

struct NullableGuid
{
    /// <summary>
    /// Provides the value when HasValue returns true
    /// </summary>
    public Guid Value { get; private set; }

    /// <summary>
    /// Indicates whether there is a value or whether
    /// the value is "null"
    /// </summary>
    public bool HasValue { get; private set; }

    // ...
}
```

Listing 12.4 shows possible implementations of NullableInt and NullableGuid. If a program required additional nullable value types, you would have to create yet another struct with the properties modified to use the desired value type. Any improvement of the implementation (e.g., adding a user-defined implicit conversion from the underlying type to the nullable type) would require modifying all the nullable type declarations.

An alternative strategy for implementing a nullable type without generics is to make a single type with a Value property of type object, as shown in Listing 12.5.

## LISTING 12.5: Declaring a Nullable Type That Contains a Value Property of Type object

```csharp
struct Nullable
{
    /// <summary>
    /// Provides the value when HasValue returns true
    /// </summary>
    public object Value { get; private set; }

    /// <summary>
    /// Indicates whether there is a value or whether
    /// the value is "null"
    /// </summary>
    public bool HasValue { get; private set; }

    // ...
}
```

Although this option requires only one implementation of a nullable type, the runtime always boxes value types when setting the Value property. Furthermore, retrieving the underlying value from the Value property requires a cast operation, which might potentially be invalid at runtime.

Neither option is particularly attractive. To eliminate this problem, C# 2.0 introduced generics to C#. (And, in fact, nullable types are implemented as the generic type `Nullable<T>`.)

## Introducing Generic Types

Generics provide a facility for creating data structures that can be specialized to handle specific types. Programmers define these parameterized types so that each variable of a particular generic type has the same internal algorithm, but the types of data and method signatures can vary on the basis of the type arguments provided for the type parameters.

To minimize the learning curve for developers, C# designers chose syntax that superficially resembles C++ templates. In C#, the syntax for generic classes and structures uses angle brackets to both declare the generic type parameters in the type declaration and specify the generic type arguments when the type is used.

## Using a Generic Class

Listing 12.6 shows how you can specify the actual type argument used by the generic class. You instruct the `path` variable to be the “Stack of Cell” type by specifying `Cell` within angle bracket notation in both the object creation expression and the declaration statement. In other words, when declaring a variable (`path` in this case) using a generic data type, C# requires the developer to identify the actual type arguments used by the generic type. Listing 12.6 illustrates this process with the new generic `Stack` class.

## LISTING 12.6: Implementing Undo with a Generic Stack Class

```csharp
using System;
using System.Collections.Generic;

class Program
{
    // ...

    public void Sketch()
    {
        Stack<Cell> path;     // Generic variable declaration
        path = new Stack<Cell>();  // Generic object instantiation
        Cell currentPosition;
        ConsoleKeyInfo key;

        do
        {
            // Etch in the direction indicated by the
            // arrow keys entered by the user
            key = Move();

            switch (key.Key)
            {
                case ConsoleKey.Z:
                    // Undo the previous Move
                    if (path.Count >= 1)
                    {
                        // No cast required
                        currentPosition = path.Pop();
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
                    // Only type Cell allowed in call to Push()
                    path.Push(currentPosition);
                    break;

                default:
                    Console.Beep(); // Added in C# 2.0
                    break;
            }
        } while (key.Key != ConsoleKey.X); // Use X to quit
    }
}
```

The results of Listing 12.6 appear in Output 12.2.

## OUTPUT 12.2

![](img/ef6a8a417630b222bfb3f3b949facff0_531_0.png)

In the path declaration shown in Listing 12.6, you declare a variable and initialize it with a new instance of the `System.Collections.Generic.Stack<Cell>` class. You specify in angle brackets that the data type of the stack's elements is `Cell`. As a result, every object added to and retrieved from `path` is of type `Cell`. In turn, you no longer need to cast the return of `path.Pop()` or ensure that only `Cell` type objects are added to `path` in the `Push()` method.

## Defining a Simple Generic Class

Generics allow you to author algorithms and patterns and to reuse the code for different data types. Listing 12.7 creates a generic `Stack<T>` class similar to the `System.Collections.Generic.Stack<T>` class used in the code in Listing 12.6. You specify a **type parameter** (in this case, `T`) within angle brackets after the class name. The generic `Stack<T>` can then be supplied with a single type argument that is substituted everywhere `T` appears in the class. Thus, the stack can store items of any stated type, without duplicating code or converting the item to type object. The type parameter `T` is a placeholder that must be supplied with a type argument. In Listing 12.7, you can see that the type parameter will be used for the internal `Items` array, the type for the parameter to the `Push()` method, and the return type for the `Pop()` method.

## LISTING 12.7: Declaring a Generic Class, Stack<T>

```csharp
public class Stack<T>
{
    // Use read-only field prior to C# 6.0
    private T[] InternalItems { get; }

    public void Push(T data)
    {
        ...
    }

    public T Pop()
    {
        ...
    }
}
```
