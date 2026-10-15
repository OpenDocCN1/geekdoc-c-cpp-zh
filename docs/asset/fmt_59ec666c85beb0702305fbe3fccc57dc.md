
即使在编译期间启用了 `checked` 选项，清单10.8代码中的 `unchecked` 关键字也会阻止运行时在执行期间抛出异常。

对于不允许使用语句的情况，还可以使用等价的 `checked` 和 `unchecked` 表达式。例如，字段初始化器可以包含表达式，而不是语句：

``` 
int _Number = unchecked(int.MaxValue + 1);
```

## 小结

抛出异常会显著影响性能。一个异常会导致大量运行时栈信息被加载和处理——这些数据在正常情况下是不会被加载的——而且处理起来相当耗时。正如第4章指出的，应该只在处理异常情况时才使用异常；API 应提供机制来检查是否将抛出异常，而不是强制调用某个特定 API 来确定是否将抛出异常。

下一章将介绍泛型——这是 C# 2.0 的一个特性，能显著增强用 C# 1.0 编写的代码。事实上，它基本上废弃了对 `System.Collections` 命名空间的使用，而该命名空间以前几乎在每个项目中都会用到。

# 11 泛型

随着项目变得越来越复杂，你将需要更好的方式来复用和定制现有软件。为了促进代码复用，尤其是算法的复用，C# 包含一个称为泛型（generics）的特性。正如方法因可以接受参数而强大，接受类型参数的类型和方法也拥有显著更多的功能。

泛型在词法上与 Java 的泛型类型和 C++ 的模板相似。在这三种语言中，这些特性都使算法和模式只需实现一次，而不需要针对算法或模式所操作的每种类型分别实现。然而，C# 泛型在实现细节及其对各自语言类型系统的影响方面，与 Java 泛型和 C++ 模板都有很大不同。泛型是在 2.0 版本中添加到运行时和 C# 中的。

![](img/25683ccec0773ba5b8794b11f2b12877_493_0.png)

```
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
        Console.Beep();  // Added in C# 2.0
        break;
}
}
while (key.Key != ConsoleKey.X);  // Use X to quit
}
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
```

清单11.2的结果见下一页的输出11.1。

# 第 11 章 泛型

## 输出 11.1

![](img/25683ccec0773ba5b8794b11f2b12877_496_0.png)

使用声明为 `System.Collections.Stack` 的变量 `path`，你可以通过 `path.Push(currentPosition)` 将自定义类型 `Cell` 传入 `Stack.Push()` 方法，从而保存上一次移动。如果用户输入 Z（或按 Ctrl+Z），你可以使用 `Pop()` 方法从栈中取回上一次移动，将光标位置设为前一个位置，并调用 `Undo()`，从而撤销该移动。

尽管这段代码可以工作，但 `System.Collections.Stack` 类有一个根本缺陷。如清单11.1所示，`Stack` 类收集的是 `object` 类型的值。由于 CLR 中的每个对象都派生自 `object`，`Stack` 不会验证你放入其中的元素是否同质或是否为预期类型。例如，除了传入 `currentPosition`，你还可以传入一个字符串，其中 X 和 Y 用小数点连接。但是，编译器必须允许这些不一致的数据类型，因为 `stack` 类的设计是接受任何对象，而不管其更具体的类型是什么。

此外，使用 `Pop()` 方法从栈中取回数据时，你必须将返回值强制转换为 `Cell`。但如果 `Pop()` 方法返回的值的类型不是 `Cell`，就会抛出异常。通过使用强制转换将类型检查推迟到运行时，会使程序更加脆弱。在不使用泛型的情况下创建可处理多种数据类型的类的根本问题在于，它们必须使用一个通用基类（或接口），通常是 `object`。

将值类型（如结构或整数）与使用 `object` 的类一起使用会使问题更加严重。例如，如果你将值类型传递给 `Stack.Push()` 方法，运行时会自动装箱它。类似地，当你取回值类型时，需要显式拆箱，并将从 `Pop()` 方法获取的对象引用强制转换为值类型。将引用类型强制转换为基类或接口的性能影响可以忽略不计，但值类型的装箱操作会带来更多开销，因为它必须分配内存、复制值，然后在之后对这块内存进行垃圾回收。

C# 是一种鼓励“类型安全”的语言：该语言的设计使得许多类型错误（例如将整数赋给 `string` 类型的变量）可以在编译时被捕获。根本问题在于 `stack` 类并不像人们期望 C# 程序那样类型安全。如果要改变 `stack` 类以强制类型安全，将栈的内容限制为特定数据类型（不使用泛型类型），你必须创建一个专用的栈类，如清单11.3所示。

## 清单 11.3：定义专用的栈类

```
public class CellStack
{
    public virtual Cell Pop();
    public virtual void Push(Cell cell);
    // ...
}
```

由于 `CellStack` 只能存储 `Cell` 类型的对象，这种解决方案需要自定义实现栈方法，这并不理想。实现整数类型安全的栈还需要另一种自定义实现；每种实现看起来都与其它实现极为相似。于是会存在大量重复、冗余的代码。

## 初学者专题

## 另一个示例：可为空的值类型

第2章介绍了在声明值类型变量时使用可为空修饰符 `?` 来声明可能包含 `null` 的变量的能力。C# 直到 2.0 版本才开始支持这一功能，因为正确的实现需要泛型。在引入泛型之前，程序员基本上面临两种选择。

第一种选择是为每个需要处理 `null` 值的值类型声明一个可为空的数据类型，如清单11.4所示。

## 清单 11.4：声明各种存储 null 的值类型版本

```
struct NullableInt
{
    /// <summary>
    /// Provides the value when HasValue returns true.
    /// </summary>
    public int Value{ get; private set; }
    /// <summary>
    /// Indicates whether there is a value or whether
    /// the value is "null".
    /// </summary>
    public bool HasValue{ get; private set; }
    // ...
}
struct NullableGuid
{
    /// <summary>
    /// Provides the value when HasValue returns true.
    /// </summary>
    public Guid Value{ get; private set; }
    /// <summary>
    /// Indicates whether there is a value or whether
    /// the value is "null".
    /// </summary>
    public bool HasValue{ get; private set; }
    ...
}
...
```

清单11.4展示了 `NullableInt` 和 `NullableGuid` 可能的实现。如果程序需要额外的可为空值类型，你将不得不创建另一个结构，并修改属性以使用所需的值类型。对实现的任何改进（添加从基础类型到...的用户定义隐式转换）

`nullable` 类型（例如）将需要修改所有 `nullable` 类型声明。

实现 `nullable` 类型而不使用泛型的另一种策略是创建一个包含类型为 `object` 的 `Value` 属性的单一类型，如 Listing 11.5 所示。

## LISTING 11.5: Declaring a Nullable Type That Contains a Value Property of Type object

```
struct Nullable
{
    /// <summary>
    /// Provides the value when HasValue returns true.
    /// </summary>
    public object Value{ get; private set; }
    /// <summary>
    /// Indicates whether there is a value or whether
    /// the value is "null".
    /// </summary>
    public bool HasValue{ get; private set; }
    ...
}
```

尽管这种选项只需要一个 `nullable` 类型的实现，但在设置 `Value` 属性时，运行时始终会对值类型进行装箱。此外，从 `Value` 属性检索底层值需要进行强制转换操作，这在运行时可能无效。

这两种选项都不是特别有吸引力。为消除此问题，C# 2.0 向 C# 引入了泛型。事实上，`nullable` 类型实际上是以泛型类型 `Nullable<T>` 实现的。

## Introducing Generic Types

泛型提供了一种创建可专门化以处理特定类型的数据结构的机制。程序员定义这些参数化类型，使得特定泛型类型的每个变量具有相同的内部算法，但数据类型和方法签名可以根据为类型参数提供的类型参数而变化。

为了最小化开发人员的学习曲线，C# 设计者选择了在表面上类似于 C++ 模板的语法。在 C# 中，泛型类和结构的语法使用尖括号来在类型声明中声明泛型类型参数，并在使用类型时指定泛型类型参数。

## Using a Generic Class

Listing 11.6 显示了如何指定泛型类使用的实际类型参数。你通过在对象创建表达式和声明语句中都使用尖括号表示法指定 `Cell`，来指示 `path` 变量为“`Stack` of `Cell`”类型。换句话说，当使用泛型数据类型声明变量时，C# 要求开发人员识别泛型类型使用的实际类型参数。Listing 11.6 使用新的泛型 `Stack` 类说明了这一过程。

```
```csharp
using System;
using System.Collections.Generic;

class Program
{
    // ...

    public void Sketch()
    {
        Stack<Cell> path;        // Generic variable declaration
        path = new Stack<Cell>(); // Generic object instantiation
        Cell currentPosition;
        ConsoleKeyInfo key;

        do
        {
            // Etch in the direction indicated by the
            // arrow keys entered by the user.
            key = Move();

            switch (key.Key)
            {
                case ConsoleKey.Z:
                    // Undo the previous Move.
                    if (path.Count >= 1)
                    {
                        // No cast required.
                        currentPosition = path.Pop();
                        Console.SetCursorPosition(
                            currentPosition.X, currentPosition.Y);
                        Undo();
                    }
```

```
break;
case ConsoleKey.DownArrow:
case ConsoleKey.UpArrow:
case ConsoleKey.LeftArrow:
case ConsoleKey.RightArrow:
    // SaveState()
    currentPosition = new Cell(
        Console.CursorLeft, Console.CursorTop);
    // Only type Cell allowed in call to Push().
    path.Push(currentPosition);
    break;
default:
    Console.Beep();  // Added in C# 2.0
    break;
}
} while (key.Key != ConsoleKey.X);  // Use X to quit.
}
}
```

Listing 11.6 的结果出现在 Output 11.2 中。

## OUTPUT 11.2

![](img/25683ccec0773ba5b8794b11f2b12877_501_0.png)

在 Listing 11.6 中显示的 `path` 声明中，你声明一个变量并用 `System.Collections.Generic.Stack<Cell>` 类的新实例对其进行初始化。你在尖括号中指定栈元素的类型为 `Cell`。因此，添加到 `path` 中并从中检索的每个对象都是 `Cell` 类型。进而，你不再需要对 `path.Pop()` 的返回值进行强制转换，也无需确保只有 `Cell` 类型对象被添加到 `path` 的 `Push()` 方法中。

## Defining a Simple Generic Class

泛型允许你编写算法和模式，并为不同数据类型重用代码。Listing 11.7 创建了一个与 Listing 11.6 代码中使用的 `System.Collections.Generic.Stack<T>` 类类似的泛型 `Stack<T>` 类。你在类名后用尖括号指定一个类型参数（在本例中为 `T`）。泛型 `Stack<T>` 然后可以提供一个单一的类型参数，该参数在类中 `T` 出现的地方被“替换”。因此栈可以存储任何声明类型的项目，而无需重复代码或将项目转换为类型 `object`。类型参数 `T` 是一个占位符，必须提供类型参数。在 Listing 11.7 中，你可以看到类型参数将用于内部 `Items` 数组、`Push()` 方法的参数类型以及 `Pop()` 方法的返回类型。

## LISTING 11.7: Declaring a Generic Class, Stack<T>

```
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
