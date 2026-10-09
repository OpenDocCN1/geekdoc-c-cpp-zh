
使程序更加脆弱。创建一个没有使用泛型却能处理多种数据类型的类，其根本问题在于它必须基于一个公共基类（通常是 `object`，即接口）来工作。

使用值类型（例如结构体或整数）时，那些基于 `object` 类的类会加剧这一问题。例如，如果你将一个值类型传递给 `Stack.Push()` 方法，运行时会自动对其进行装箱（boxing）。同样，当检索值类型时，你需要显式地取消装箱，并将从 `Pop()` 方法获取的对象引用强制转换为值类型。将引用类型强制转换为基类或接口的性能影响微乎其微，但值类型的装箱操作会引入更多开销，因为它必须分配内存、复制值，然后稍后由垃圾回收器回收该内存。

C# 是一门鼓励类型安全的语言：该语言的设计使得许多类型错误（例如将整数赋值给类型为 `string` 的变量）可以在编译时被捕获。根本问题在于 `Stack` 类的类型安全性不如人们期望 C# 程序所具备的那样高。要将 `Stack` 类改为强制类型安全，以限制堆栈内容必须是特定的数据类型（在不使用泛型类型的情况下），你必须创建一个专门的堆栈类，如清单 12.3 所示。

## 清单 12.3：定义一个专门的堆栈类

```csharp
public class CellStack
{
    public virtual Cell Pop();
    public virtual void Push(Cell cell);
    // ...
}
```

由于 `CellStack` 只能存储类型为 `Cell` 的对象，这种解决方案需要自定义堆栈方法的实现，这不是理想的方案。实现一个类型安全的整数堆栈需要另一个自定义实现；每个实现看起来都惊人地相似。这将导致大量重复和冗余的代码。

## 入门主题

### 另一个示例：可空值类型

第 3 章介绍了使用可空修饰符 `?` 声明可以包含 null 的变量的功能。C# 直到 2.0 版本才开始支持此功能，因为正确的实现需要泛型。在引入泛型之前，程序员基本上面临两个选择。

第一个选项是为每个需要处理 null 值的值类型声明一个可空数据类型，如清单 12.4 所示。

## 清单 12.4：声明存储 null 的各种值类型版本

```csharp
struct NullableInt
{
    /// <summary>
    /// 当 HasValue 返回 true 时提供值
    /// </summary>
    public int Value { get; private set; }

    /// <summary>
    /// 指示是否存在值，
    /// 或者值是否为 "null"
    /// </summary>
    public bool HasValue { get; private set; }

    // ...
}

struct NullableGuid
{
    /// <summary>
    /// 当 HasValue 返回 true 时提供值
    /// </summary>
    public Guid Value { get; private set; }

    /// <summary>
    /// 指示是否存在值，
    /// 或者值是否为 "null"
    /// </summary>
    public bool HasValue { get; private set; }

    // ...
}
```

清单 12.4 展示了 `NullableInt` 和 `NullableGuid` 的可能实现。如果程序需要额外的可空值类型，你就必须创建另一个结构体，并将其属性修改为使用所需的值类型。对该实现的任何改进（例如，添加从基础类型到可空类型的用户定义隐式转换）都将需要修改所有可空类型声明。

在没有泛型的情况下实现可空类型的另一种策略是创建一个具有类型为 `object` 的 `Value` 属性的单一类型，如清单 12.5 所示。

## 清单 12.5：声明包含类型为 object 的 Value 属性的可空类型

```csharp
struct Nullable
{
    /// <summary>
    /// 当 HasValue 返回 true 时提供值
    /// </summary>
    public object Value { get; private set; }

    /// <summary>
    /// 指示是否存在值，
    /// 或者值是否为 "null"
    /// </summary>
    public bool HasValue { get; private set; }

    // ...
}
```

虽然这种选项只需要一个可空类型的实现，但在设置 `Value` 属性时，运行时总是会对值类型进行装箱。此外，从 `Value` 属性中检索底层值需要强制转换操作，这在运行时可能是无效的。

这两个选项都不是很吸引人。为了解决这个问题，C# 2.0 向 C# 引入了泛型。（实际上，可空类型是通过泛型类型 `Nullable<T>` 实现的。）

## 介绍泛型类型

泛型提供了一种创建可以专门用于处理特定类型的数据结构的机制。程序员定义这些参数化类型，使得特定泛型类型的每个变量都具有相同的内部算法，但数据和方法签名的类型可以根据提供给类型参数的类型参数而变化。

为了最小化开发人员的学习曲线，C# 设计者选择了在表面上类似于 C++ 模板的语法。在 C# 中，泛型类和结构体的语法使用尖括号来在类型声明中声明泛型类型参数，并在使用该类型时指定泛型类型实参。

## 使用泛型类

清单 12.6 展示了如何指定泛型类使用的实际类型实参。通过在对象创建表达式和声明语句中的尖括号表示法内指定 `Cell`，你指示 `path` 变量为“Cell 堆栈”类型。换句话说，当使用泛型数据类型声明变量（在本例中为 `path`）时，C# 要求开发人员指定泛型类型使用的实际类型实参。清单 12.6 通过新的泛型 `Stack` 类展示了这一过程。

## 清单 12.6：使用泛型堆栈类实现撤销功能

```csharp
using System;
using System.Collections.Generic;

class Program
{
    // ...

    public void Sketch()
    {
        Stack<Cell> path;     // 泛型变量声明
        path = new Stack<Cell>();  // 泛型对象实例化
        Cell currentPosition;
        ConsoleKeyInfo key;

        do
        {
            // 沿用户输入的箭头键指示的方向刻蚀
            key = Move();

            switch (key.Key)
            {
                case ConsoleKey.Z:
                    // 撤销上一步移动
                    if (path.Count >= 1)
                    {
                        // 不需要强制转换
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
                    // 调用 Push() 时仅允许 Cell 类型
                    path.Push(currentPosition);
                    break;

                default:
                    Console.Beep(); // 在 C# 2.0 中添加
                    break;
            }
        } while (key.Key != ConsoleKey.X); // 使用 X 退出
    }
}
```

清单 12.6 的结果如输出 12.2 所示。

## 输出 12.2

![](img/ef6a8a417630b222bfb3f3b949facff0_531_0.png)

在清单 12.6 中显示的 `path` 声明中，你声明了一个变量，并用 `System.Collections.Generic.Stack<Cell>` 类的新实例对其进行初始化。你用尖括号指定堆栈元素的数据类型为 `Cell`。结果是，添加到 `path` 并从其中检索的每个对象都是 `Cell` 类型。反过来，你不再需要强制转换 `path.Pop()` 的返回值，也不需要确保在 `Push()` 方法中只向 `path` 添加 `Cell` 类型对象。

## 定义一个简单的泛型类

泛型允许你编写算法和模式，并为不同的数据类型重用代码。清单 12.7 创建了一个与清单 12.6 代码中使用的 `System.Collections.Generic.Stack<T>` 类类似的泛型 `Stack<T>` 类。你在类名后的尖括号内指定一个**类型参数**（在本例中为 `T`）。然后，可以为泛型 `Stack<T>` 提供单个类型实参，该实参将替换类中出现的所有 `T`。因此，堆栈可以存储任何指定类型的项，而无需重复代码或将项转换为 `object` 类型。类型参数 `T` 是一个占位符，必须提供类型实参。在清单 12.7 中，你可以看到类型参数将用于内部的 `Items` 数组、`Push()` 方法的参数类型以及 `Pop()` 方法的返回类型。

## 清单 12.7：声明泛型类 Stack<T>

```csharp
public class Stack<T>
{
    // 在 C# 6.0 之前使用只读字段
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
