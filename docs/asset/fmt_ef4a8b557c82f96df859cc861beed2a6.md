
```csharp
public class Program {
    static void Main() {
        var keywords = new CSharpBuiltInTypes();
        foreach (string keyword in keywords) {
            Console.WriteLine(keyword);
        }
    }
}
```

列表 17.13 的结果出现在输出 17.5 中。

### 输出 17.5

```
object
byte
uint
ulong
float
char
bool
ushort
decimal
int
sbyte
short
long
void
double
string
```

此列表的输出是 C# 内置类型的列表。

# 迭代器与状态

当在 `foreach` 语句中首次调用 `GetEnumerator()` 时（例如列表 17.13 中的 `foreach (string keyword in keywords)`），会创建一个迭代器对象，并将其状态初始化为一种特殊的“开始”状态，该状态表示迭代器中尚未执行任何代码，因此尚未产生任何值。只要调用处的 `foreach` 状态继续执行，迭代器就会保持其状态。每当循环请求下一个值时，控制就会进入迭代器，并从上一次循环的地方继续执行，存储在迭代器对象中的状态信息用于确定控制必须在何处恢复。当调用处的 `foreach` 语句终止时，迭代器的状态将不再保存。

再次调用 `getEnumerator()` 总是安全的，在需要时将创建“新的”枚举器对象。

图 17.8 显示了所发生过程的高级序列图。记住 `MoveNext()` 方法出现在接口上。

![](img/b18af4770e9195628243fa73ff1469b4_796_0.png)

图 17.8: 发生过程的序列图

# 迭代器与状态

当 `GetEnumerator()` 在 `foreach` 语句中首次调用时（例如列表 17.13 中的 `foreach (string keyword in keywords)`），会创建一个迭代器对象，并将其状态初始化为一种特殊的“开始”状态，该状态表示迭代器中尚未执行任何代码，因此尚未产生任何值。只要调用处的 `foreach` 状态继续执行，迭代器就会保持其状态。每当循环请求下一个值时，控制就会进入迭代器，并从上一次循环的地方继续执行，存储在迭代器对象中的状态信息用于确定控制必须在何处恢复。当调用处的 `foreach` 语句终止时，迭代器的状态将不再保存。

再次调用 `getEnumerator()` 总是安全的，在需要时将创建“新的”枚举器对象。图 17.8 显示了所发生过程的高级序列图。记住 `MoveNext()` 方法出现在接口上。

# 迭代器与状态

当 `GetEnumerator()` 在 `foreach` 语句中首次调用时（例如列表 17.13 中的 `foreach (string keyword in keywords)`），会创建一个迭代器对象，并将其状态初始化为一种特殊的“开始”状态，该状态表示迭代器中尚未执行任何代码，因此尚未产生任何值。只要调用处的 `foreach` 状态继续执行，迭代器就会保持其状态。每当循环请求下一个值时，控制就会进入迭代器，并从上一次循环的地方继续执行，存储在迭代器对象中的状态信息用于确定控制必须在何处恢复。当调用处的 `foreach` 语句终止时，迭代器的状态将不再保存。

再次调用 `getEnumerator()` 总是安全的，在需要时将创建“新的”枚举器对象。图 17.8 显示了所发生过程的高级序列图。记住 `MoveNext()` 方法出现在接口上。

...语句，你可以从循环结构内部返回值。列表 17.16 使用了 `foreach` 循环。每当 `GetEnumerator()` 内部的 `foreach` 执行时，它都会返回下一个值。

# 列表 17.16：在循环中放置 yield return 语句

```csharp
public class BinaryTree<T>: IEnumerable<T>
{
    //

#region IEnumerable<T>
public IEnumerator<T> GetEnumerator()
{
    // 返回此节点上的项
    yield return Value;

    // 遍历对中的每个元素
    foreach (BinaryTree<T>? tree in SubItems)
    {
        if (tree != null)
        {
            // 由于对中的每个元素都是树，
            // 遍历该树并产生每个元素
            foreach (T item in tree)
            {
                yield return item;
            }
        }
    }
}
#endregion

#region IEnumerable Members
System.Collections.IEnumerator
System.Collections.IEnumerable.GetEnumerator()
{
    return GetEnumerator();
}
#endregion
```

在 17.16 中，第一次迭代返回二叉树中的根元素。在第二次迭代期间，你遍历了子元素对。如果子元素对包含非空值，你将遍历到该子节点并产生它的元素。注意，`foreach (T item in tree)` 是对子节点的递归调用。

正如在 `CSharpBuiltInTypes` 和 `Pair<T>` 中观察到的那样，你现在可以使用 `foreach` 循环来遍历 `BinaryTree<T>`。列表 17.17 演示了这一过程，输出 17.6 显示了结果。

# 第 17 章：构建自定义集合

## 列表 17.17：在 BinaryTree<string> 上使用 foreach

```csharp
// JFK
var jfkFamilyTree = new BinaryTree<string>(
  "John Fitzgerald Kennedy")
{
  SubItems = new Pair<BinaryTree<string>>(
    new BinaryTree<string>("Joseph Patrick Kennedy")
    {
      // 祖父母（父系 side）
      SubItems = new Pair<BinaryTree<string>>(
        new BinaryTree<string>("Patrick Joseph Kennedy"),
        new BinaryTree<string>("Mary Augusta Hickey")
      )
    }),
    // 祖父母（母系 side）
    SubItems = new Pair<BinaryTree<string>>(
      new BinaryTree<string>("John Francis Fitzgerald"),
      new BinaryTree<string>("Mary Josephine Hannon")
    )
  )
}

foreach (string name in jfkFamilyTree)
{
  Console.WriteLine(name);
}
```

# 输出 17.6

John Fitzgerald Kennedy

Joseph Patrick Kennedy

Patrick Joseph Kennedy

Mary Augusta Hickey

Rose Elizabeth Fitzgerald

John Francis Fitzgerald

Mary Josephine Hannon

## 高级主题

### 递归迭代器的危险性

列表 17.16 中的代码在遍历二叉树时创建了“嵌套”迭代器。结果是当值由某个节点产生时，该值先由该节点的迭代器产生，然后由其父节点的迭代器产生，依此类推，直到最后由根节点的迭代器产生给原始循环。一个深度为 $n$ 层的值实际上必须通过 $n$ 个迭代器的链链向上传递其值。如果二叉树相对浅，这通常不是问题；然而，不平衡的二叉树可能非常深，因此递归迭代的开销很大。

# 指南

在遍历可能深层的数据结构时，**考虑**使用非递归算法。

# 高级/初学者主题

## struct 对比 class

将 `Pair<T>` 定义为 `struct` 而不是 `class` 的有趣副作用是，`SubItems.First` 和 `SubItems.Second` 无法直接赋值，即使 setter 是公共的。如果你将 setter 修改为公共，以下代码将产生编译器错误，指示 `SubItems` 无法被修改“因为它不是一个变量”：

```csharp
jfkFamilyTree.SubItems.First =
new BinaryTree<string>{
  "Joseph Patrick Kennedy";};
```

问题在于 `SubItems` 是一个 `Pair<T>` 类型的属性，这是一个 `struct`。因此，当属性返回值时，会创建 `SubItems` 的副本，将 `First` 赋值给一个在语句结束时立即丢失的副本是具有误导性的。幸运的是，C# 编译器阻止了这种情况。

为了解决这个问题，不要为 `First` 赋值（列表 17.17 中的方法），使用 `class` 而不是 `struct` 作为 `Pair<T>`，不要创建 `SubItems` 属性而是使用字段，或者在 `BinaryTree<T>` 中提供可以直接访问 `SubItems` 成员的属性。

# 取消后续迭代：yield break

有时你可能想要取消后续迭代。你可以包含一个 `if` 语句使得代码中不再执行后续语句。然而，你也可以使用 `yield return Next()` 返回 `false` 并控制权立即返回调用者并结束循环。列表 17.18 显示了此类方法的示例。

# 第 17 章：构建自定义集合

- 列表 17.18：通过 yield break 跳出迭代

```csharp
public System.Collections.Generic.IEnumerator<T>
    GetEnumerator()
{
    if(First == null) || (Second == null)
    {
        yield break;
    }
    yield return Second;
    yield return First;
}
```

如果 `Pair<T>` 类中的任一元素为空，该方法将取消迭代。

`yield break` 语句类似于 `return` 语句；它是提前退出的方法。请谨慎使用。

## 高级主题

### 迭代器的工作原理

当 C# 编译器遇到迭代器时，它会展开成你可能手动编写的代码。因为编译器获取 `yield return` 语句并生成对应于枚举器模式的类，迭代器的性能特性与手动实现枚举器模式的类相同。- 列表 17.19：编译器生成的等价代码：

```csharp
using System;
using System.Collections;
using System.Collections.Generic;

public struct Pair<T> : IEquatable<T>, IEnumerable<T>
{
    public Pair(T first, T second)
    {
        First = first;
        Second = second;
    }

    public T First { get; }

    public T Second { get; }

    public T this[int index]
    {
        get
        {
            int pairItem = index;
            int pairItem2 = index;
            T result;
            if (pairItem == 0)
            {
                if (pairItem2 != 1)
                {
                    throw new NotImplementedException(string.Format("The {0} has not been implemented", index.ToString()));
                }
                result = Second;
            }
            else
            {
                result = First;
            }
            return result;
        }
    }

    public IEnumerator<T> GetEnumerator()
    {
        yield return First;
        yield return Second;
        yield break;
    }

    IEnumerator IEnumerable.GetEnumerator()
    {
        return GetEnumerator();
    }
}
```

# 第 17 章：构建自定义集合

因为编译器获取 `yield return` 语句并生成对应于你可能手动编写的代码，迭代器的性能特性与手动实现枚举器模式的类相同。虽然没有性能提升，但程序员生产力的提高是显著的。

## 高级主题

# 上文关键字

许多 C# 关键字是“保留”的，除非前面有 `@` 符号，否则不能作为标识符。`yield` 关键字是一个上下文关键字，而不是保留关键字；因此，声明一个名为 `yield` 的局部变量是合法的（尽管令人困惑）。通过封装返回 `IEnumerable<T>` 或 `IEnumerable` 的属性或方法来实现额外的迭代器。例如，如果你想反向遍历 `Pair<T>` 的元素，请提供一个 `GetReverseEnumerator()` 方法，如列表 17.20 所示。

# 列表 17.20：在返回 IEnumerable<T> 的方法中使用 yield return

```csharp
public struct Pair<T>: IEnumerable<T>
{
    // ...
    public IEnumerable<T> GetReverseEnumerator()
    {
        yield return Second;
        yield return First;
    }
    // ...
}
```

```csharp
public void Main() {
    var game = new Pair<string>("Redskins", "Eagles");
    foreach (string name in game.GetReverseEnumerator())
    {
        Console.WriteLine(name);
    }
}
```

注意你返回的是 `IEnumerable<T>`，而不是 `IEnumerator<T>`。这与 `IEnumerable<T>.GetEnumerator()` 不同，后者返回的是 `IEnumerator<T>`。`Main()` 中的代码演示了如何使用 `foreach` 循环调用 `GetReverseEnumerator()`。

## yield 语句的要求

你只能在返回 `IEnumerator<T>` 或 `IEnumerable<T>` 类型（或非泛型等效项）的成员中使用 `yield return` 语句。体体包含 `yield return` 语句的成员不能有简单的 `return`。如果成员使用了 `yield return` 语句，C# 编译器会生成必要的代码来维护迭代器的状态。相比之下，如果成员使用 `return` 语句而不是 `yield return`，则程序员需要负责维护自己的状态机并返回迭代器接口的实例。此外，就如同具有返回类型的方法中的所有代码路径必须包含带值的返回语句（假设它们没有抛出异常）一样，迭代器中的所有代码路径如果要返回数据，必须包含 `yield return` 语句。

# 第 17 章：构建自定义集合

以下是对 `yield` 语句结果的附加限制如果被违反将会导致编译器错误：

- `yield` 语句只能出现在方法、用户定义操作符、或者索引器或属性的 `get` 访问器内部。该成员不能接受任何 `ref` 或 `out` 参数。

- `yield` 语句不能出现在匿名方法或 lambda 表达式的内部（见第 13 章）。

- `yield` 语句不能出现在 `try` 语句的 `catch` 和 `finally` 子句中。此外，只有在没有 `catch` 块的情况下，`yield` 语句才能出现在 `try` 块中。

## 总结

在本章中，我们回顾了关键集合类，并考虑了它们如何根据支持的接口进行分类。每个类都侧重于向集合插入项和从集合中检索项，使用了通过键、先进先出（FIFO）或后进先（LIFO）等机制。我们还探索了如何遍历集合。此外，本章解释了如何通过自定义迭代器来定义自定义集合，以便枚举集合中的项。（迭代器涉及一个关键字 `yield`，C# 使用它来生成实现 `foreach` 循环所用迭代器模式的底层 CIL 代码。）

在第 18 章中，我们将探索反射（reflection），这是一个之前简要提到过的话题，尽管几乎没有进行解释。反射允许我们在运行时检查类型的 CIL 代码结构。

# 第 18 章：反射、属性与动态编程
