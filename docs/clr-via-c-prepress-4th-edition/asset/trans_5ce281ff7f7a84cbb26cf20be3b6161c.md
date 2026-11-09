
有时，人们会在泛型类型上定义静态构造函数，以确保类型实参满足某些条件。例如，如果你想定义一个只能与枚举类型一起使用的泛型类型，可以这样做：

```csharp
internal sealed class GenericTypeThatRequiresAnEnum<T> {
    static GenericTypeThatRequiresAnEnum() {
        if (!typeof(T).IsEnum) {
            throw new ArgumentException("T must be an enumerated type");
        }
    }
}
```

CLR 有一个称为约束的功能，它为你提供了一种更好的方式来定义泛型类型，并指明哪些类型实参对该类型有效。我将在本章后面讨论约束。遗憾的是，约束不支持将类型实参限制为只能是枚举类型，这就是为什么前面的示例需要静态构造函数来确保该类型是枚举类型。

## 泛型类型与继承

泛型类型也是一种类型，因此它可以派生自任何其他类型。当你使用泛型类型并指定类型实参时，你是在 CLR 中定义一个新的类型对象，而这个新类型对象派生自该泛型类型所派生自的类型。换句话说，由于 `List<T>` 派生自 `Object`，所以 `List<String>` 和 `List<Guid>` 也派生自 `Object`。类似地，由于 `DictionaryStringKey<TValue>` 派生自 `Dictionary<String, TValue>`，所以 `DictionaryStringKey<Guid>` 也派生自 `Dictionary<String, Guid>`。理解“指定类型实参与继承层次结构无关”这一点，将帮助你认识到可以执行和不能执行哪种类型转换。

例如，如果一个链表节点类定义如下：

```csharp
internal sealed class Node<T> {
    public T m_data;
    public Node<T> m_next;

    public Node(T data) : this(data, null) {
    }

    public Node(T data, Node<T> next) {
        m_data = data; m_next = next;
    }

    public override String ToString() {
        return m_data.ToString() +
            ((m_next != null) ? m_next.ToString() : String.Empty);
    }
}
```

那么我可以编写一些代码来构建一个链表，大致如下：

```csharp
private static void SameDataLinkedList() {
    Node<char> head = new Node<char>('C');
    head = new Node<char>('B', head);
    head = new Node<char>('A', head);
    Console.WriteLine(head.ToString());  // Displays "ABC"
}
```

在刚才展示的 `Node` 类中，`m_next` 字段必须引用另一个节点，而该节点的 `m_data` 字段具有同一种数据类型。这意味着链表中包含的节点里，所有数据项都必须是相同类型（或派生类型）。例如，我不能使用 `Node` 类创建一个链表，让其中一个元素包含 `Char`，另一个元素包含 `DateTime`，还有一个元素包含 `String`。好吧，如果我在所有地方都使用 `Node<Object>`，那也可以，但这样会失去编译时类型安全，而且值类型会被装箱。

因此，更好的做法是定义一个非泛型的 `Node` 基类，然后定义一个泛型 `TypedNode` 类（使用 `Node` 类作为基类）。现在，我可以拥有一个链表，其中每个节点都可以是特定的数据类型（而不是 `Object`），获得编译时类型安全，并避免值类型装箱。下面是新的类定义：

```csharp
internal class Node {
    protected Node m_next;

    public Node(Node next) {
        m_next = next;
    }
}

internal sealed class TypedNode<T> : Node {
    public T m_data;

    public TypedNode(T data) : this(data, null) {
    }

    public TypedNode(T data, Node next) : base(next) {
        m_data = data;
    }

    public override String ToString() {
        return m_data.ToString() +
            ((m_next != null) ? m_next.ToString() : String.Empty);
    }
}
```

现在我可以编写代码来创建一个链表，其中每个节点都是不同的数据类型。代码可能大致如下：

```csharp
private static void DifferentDataLinkedList() {
    Node head = new TypedNode<Char>('A', null);
    head = new TypedNode<DateTime>(DateTime.Now, head);
    head = new TypedNode<String>("Today is ", head);
    Console.WriteLine(head.ToString());
}
```

## 泛型类型标识

有时，泛型语法会让开发人员感到困惑。毕竟，源代码中可能散布着大量小于号（<）和大于号（>），这会影响可读性。为了改善语法，一些开发人员会定义一个新的非泛型类类型，它派生自某个泛型类型，并指定所有类型实参。例如，为了简化下面这样的代码：

```csharp
List<DateTime> dtl = new List<DateTime>();
```

一些开发人员可能会先定义一个像这样的类：

```csharp
internal sealed class DateTimeList : List<DateTime> {
    // No need to put any code in here!
}
```

现在，创建列表的代码可以更简单地重写（不带小于号和大于号），如下所示：

```csharp
DateTimeList dtl = new DateTimeList();
```

虽然这看起来很方便，尤其是当你将这个新类型用于参数、局部变量和字段时，但你绝不应该仅仅为了让源代码更易读而显式定义一个新类。原因在于你会失去类型标识和等价性，正如你在以下代码中所看到的：

```csharp
Boolean sameType = (typeof(List<DateTime>) == typeof(DateTimeList));
```

当上面的代码运行时，`sameType` 将被初始化为 `false`，因为你比较的是两个不同的类型对象。这也意味着，一个原型声明为接受 `DateTimeList` 的方法将无法接受传入的 `List<DateTime>`。然而，一个原型声明为接受 `List<DateTime>` 的方法可以接受传入的 `DateTimeList`，因为 `DateTimeList` 派生自 `List<DateTime>`。程序员可能会很容易被这一切弄糊涂。

幸运的是，C# 确实提供了一种使用简化语法来引用泛型封闭类型的方法，而且完全不会影响类型等价性；你可以在源代码文件顶部使用老牌的 `using` 指令。下面是一个示例：

```csharp
using DateTimeList = System.Collections.Generic.List<System.DateTime>;
```

在这里，`using` 指令实际上只是定义了一个名为 `DateTimeList` 的符号。在代码编译时，编译器会将所有出现的 `DateTimeList` 替换为 `System.Collections.Generic.List<System.DateTime>`。这只是让开发人员能够使用简化语法，而不会影响代码的实际含义，因此类型标识和等价性得以保持。所以现在，当下面这一行执行时，`sameType` 将被初始化为 `true`。

```csharp
Boolean sameType = (typeof(List<DateTime>) == typeof(DateTimeList));
```

作为另一种便利，你可以使用 C# 的隐式类型局部变量功能，编译器会根据你赋给方法局部变量的表达式类型来推断该变量的类型：

```csharp
using System;
using System.Collections.Generic;
...
internal sealed class SomeType {
    private static void SomeMethod() {
        // Compiler infers that dtl is of type
        // System.Collections.Generic.List<System.DateTime>
        var dtl = new List<DateTime>();

        ...
    }
}
```

## 代码爆炸

当使用泛型类型参数的方法被 JIT 编译时，CLR 会获取该方法的 IL，替换指定的类型实参，然后生成特定于该方法在指定数据类型上操作的本机代码。这正是你想要的，也是泛型的主要特性之一。然而，这也有一个缺点：CLR 会为每一种方法/类型组合不断生成本机代码。这被称为代码爆炸。这最终可能会大幅增加应用程序的工作集，从而损害性能。

幸运的是，CLR 内置了一些优化来减少代码爆炸。首先，如果某个方法因特定的类型实参而被调用，之后又使用相同的类型实参再次调用该方法，那么 CLR 只会为这个“方法/类型”组合编译一次代码。因此，如果一个程序集使用 `List<DateTime>`，而另一个完全不同的程序集（加载在同一 AppDomain 中）也使用 `List<DateTime>`，CLR 将只为 `List<DateTime>` 的方法编译一次。这会大幅减少代码爆炸。

CLR 还有另一项优化：CLR 认为所有引用类型实参都是相同的，因此代码同样可以共享。例如，CLR 为 `List<String>` 的方法编译的代码可以用于 `List<Stream>` 的方法，因为 `String` 和 `Stream` 都是引用类型。事实上，对于任何引用类型，都会使用相同的代码。CLR 能够执行这项优化，是因为所有引用类型实参或变量实际上都只是指向堆上对象的指针（在 32 位 Windows 系统上为 32 位，在 64 位 Windows 系统上为 64 位），而对象指针都以相同的方式操作。

但是，如果任何类型实参是值类型，CLR 就必须专门为该值类型生成本机代码。原因在于值类型的大小可能不同。而且，即使两个值类型大小相同（例如 `Int32` 和 `UInt32` 都是 32 位），CLR 仍然无法共享代码，因为可以使用不同的本机 CPU 指令来操作这些值。
