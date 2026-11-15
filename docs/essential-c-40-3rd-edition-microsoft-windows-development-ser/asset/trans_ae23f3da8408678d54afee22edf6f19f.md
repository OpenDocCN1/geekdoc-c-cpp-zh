

{
    // The binary tree at this location is null.
    throw new IndexOutOfRangeException();
}
currentLevel++;
}
return currentNode.Value;
}
set
{
    // ...
}
}
}

branches 中的每个项目都是一个 PairItem，并指示在二叉树中应导航到哪个分支。

## 返回 null 或空集合

返回数组或集合时，必须通过返回 null 或一个不包含任何项的集合实例来指示项数为零。通常更好的选择是返回一个不包含任何项的集合实例。这样做可以避免强制调用者在遍历集合中的项之前检查是否为 null。例如，对于大小为零的 IEnumerable<T> 集合，调用者可以立即安全地对集合使用 foreach 循环，而无需担心生成的 GetEnumerator() 调用会引发 NullReferenceException。

偏离此准则的少数情况之一是，当 null 有意表示与零项不同的含义时。例如，字符串类型电话号码的 null 值可能表示电话号码未设置，而空字符串可以明确表示没有电话号码。

## 迭代器

本章前面详细介绍了 foreach 循环的内部工作原理。本节讨论如何使用迭代器为自定义集合创建 IEnumerable<T> 和非泛型 IEnumerable 接口的自有实现。迭代器提供了简洁的语法来指定如何遍历集合类中的数据，尤其是使用 foreach 循环时。迭代器允许集合的最终用户在不了解其内部结构的情况下导航该结构。

### 高级主题

### 迭代器的起源

1972 年，Barbara Liskov 及其在 MIT 的科学家团队开始研究编程方法论，专注于用户定义的数据抽象。为了证明其大部分工作，他们创建了一种名为 CLU 的语言，该语言具有名为“clusters”的概念（CLU 是其前三个字母），这是程序员今天使用的主要数据抽象（即对象）的前身。作为研究的一部分，该团队意识到，尽管他们能够使用 CLU 语言将某些数据表示从其类型的最终用户中抽象出来，但他们始终发现自己必须揭示数据的内部结构，才能让其他人智能地使用它。在困惑中，诞生了一种名为迭代器的语言构造。（CLU 语言为后来被称为面向对象编程的事物提供了许多洞察。）

如果类希望使用 foreach 循环构造支持迭代，则必须实现枚举器模式。如前一节所示，在 C# 中，foreach 循环构造由编译器根据从 IEnumerable<T> 接口获取的 IEnumerable<T> 接口展开为 while 循环构造。

枚举器模式的问题在于手动实现可能很麻烦，因为它维护一个内部状态机。对于列表集合类型类，这个内部状态机可能很简单，但对于需要递归遍历的数据结构（例如二叉树），状态机可能非常复杂。为了克服实现此模式所面临的挑战和工作量，C# 2.0 引入了一种构造，使类更容易规定 foreach 循环如何遍历其内容。

## 定义迭代器

迭代器是实现类方法的一种手段，它们是更复杂的枚举器模式的语法快捷方式。当 C# 编译器遇到迭代器时，它会将其内容展开为实现枚举器模式的 CIL 代码。因此，实现迭代器没有运行时依赖项。由于 C# 编译器通过 CIL 代码生成来处理实现，使用迭代器没有真正的运行时性能优势。但是，与手动实现枚举器模式相比，选择迭代器可以显著提高程序员的生产力。要开始，下一节将探讨如何在代码中定义迭代器。

## 迭代器语法

迭代器提供了迭代器接口的简写实现，即 `IEnumerable<T>` 和 `IEnumerator<T>` 接口的组合。清单 16.12 通过创建 `GetEnumerator()` 方法为泛型 `BinaryTree<T>` 类型声明了一个迭代器。接下来，您将为迭代器接口添加支持。

### 清单 16.12：迭代器接口模式

```csharp
using System;
using System.Collections.Generic;

public class BinaryTree<T>:
    IEnumerable<T>
{
    public BinaryTree ( T value )
    {
        Value = value;
    }

    #region IEnumerable<T>
    public IEnumerator<T> GetEnumerator()
    {
        ...
    }
    #endregion IEnumerable<T>

    public T Value
    {
        get{ return _value; }
        set{ _value = value; }
    }
}
private T _value;

public Pair<BinaryTree<T>> SubItems
{
    get{ return _subItems; }
    set{ _subItems = value; }
}

private Pair<BinaryTree<T>> _subItems;

}

public struct Pair<T>
{
    public Pair(T first, T second)
    {
        _first = first;
        _second = second;
    }

    public T First
    {
        get{ return _first; }
        private set{_first = value; }
    }

    private T _first;
    public T Second
    {
        get{ return _second; }
        private set{_second = value; }
    }

    private T _second;
}
```

首先，添加 IEnumerable<T>.GetEnumerator() 方法的声明。

## 从迭代器产生值

迭代器类似于函数，但它们不是返回值，而是产生值。对于 BinaryTree<T>，迭代器的产生类型对应于类型参数 T。如果使用非泛型版本的 IEnumerator，则返回类型将改为 object。为了正确实现迭代器模式，需要维护一个内部状态机，以便在枚举集合时跟踪当前位置。在 BinaryTree<T> 的情况下，需要跟踪树中哪些元素已被枚举，哪些尚未枚举。

迭代器具有内置状态机，用于跟踪当前元素和下一个元素。每次迭代器遇到 yield return 语句时，它都会返回一个值。然后，当下一次迭代开始时，代码将从上一个 yield return 语句之后立即开始执行。在清单 16.13 中，您将按顺序返回 C# 原始数据类型关键字。

### 清单 16.13：按顺序产生 C# 关键字

```csharp
using System;
using System.Collections.Generic;

public class CSharpPrimitiveTypes: IEnumerable<string>
{
    public IEnumerator<string> GetEnumerator()
    {
        yield return "object";
        yield return "byte";
        yield return "uint";
        yield return "ulong";
        yield return "float";
        yield return "char";
        yield return "bool";
        yield return "ushort";
        yield return "decimal";
        yield return "int";
        yield return "sbyte";
        yield return "short";
        yield return "long";
        yield return "void";
        yield return "double";
        yield return "string";
    }

    // IEnumerator also required because IEnumerable<T>
    // derives from it.
    System.Collections.IEnumerator
    System.Collections.IEnumerable.GetEnumerator()
    {
        // Invoke IEnumerable<string>.GetEnumerator() above
        return GetEnumerator();
    }
}

public class Program
{
    static void Main()
    {
        CSharpPrimitiveTypes primitives =
        new CSharpPrimitiveTypes();
        foreach (string primitive in primitives)
        {
            Console.WriteLine(primitive);
        }
    }
}
```

清单 16.13 的结果显示在输出 16.5 中。

### 输出 16.5：

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

此清单的输出是 C# 原始类型的列表。1

## 迭代器与状态

当迭代器首次在 foreach 语句中被调用时（例如清单 16.13 中的 foreach (string primitive in primitives)），其状态在枚举器中初始化。只要调用站点的 foreach 语句继续执行，迭代器就会维护其状态。当您产生一个值、处理它并恢复调用站点的 foreach 语句时，迭代器将从上次循环中断开的地方继续执行，并

1. 在 C# 2.0 编译器的 alpha 版本中，yield 是一个关键字，而不是上下文关键字。但是，此类更改可能会导致 C# 1.0 和 C# 2.0 之间不兼容。相反，yield 成为必须出现在 return 之前的上下文关键字。因此，未发生任何代码破坏性更改，因为 C# 1.0 不允许在 return 关键字之前出现任何文本（注释除外）。

