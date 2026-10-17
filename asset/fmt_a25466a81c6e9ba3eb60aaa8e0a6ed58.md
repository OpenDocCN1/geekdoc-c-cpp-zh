
CLR 有一项名为“约束”（constraints）的功能，它为你提供了一种更好的方法来定义类型参数的有效范围。我将在本章稍后的部分讨论约束。遗憾的是，约束不支持将类型参数限制为枚举类型，这就是为什么之前的示例需要一个静态构造函数来确保该类型是枚举类型。

# 泛型类型与继承

泛型类型是一种类型，像类型一样，它可以派自任何其他类型。当你使用泛型类型并指定类型参数时，你正在 CLR 中定义一个新对象，而这个新类型对象派自该泛型类型所派自的类型。换句话说，由于 `List<T>` 派自 `Object`，因此 `List<String>` 和 `List<Guid>` 也派自 `Object`。同样，由于 `Dictionary<StringKey, TValue>` 也派自 `Dictionary<String, TValue>`。理解指定类型参数与继承层次无关，将帮助你识别哪些转换可以进行，哪些不能进行。

例如，如果一个链表节点类定义如下：

```
internal sealed class Node<T> {

    public T m_data;

    public Node<T> m_next;

    public Node(T data) : this(data, null) {

    }

    public Node(T data, Node<T> next) {

        m_data = data; m_next = next;

    }

}
```

# 286 第二部分 设计类型

```
}

public override String ToString() {

    return m_data.ToString() +

    ((m_next != null) ? m_next.ToString() : String.Empty);

}
```

那么我可以写一些代码来构建一个像这样的链表：

```
private static void SameDataLinkedListList() {

    Node<char> head = new Node<char>('C');

    head = new Node<char>('B', head);

    head = new Node<char>('A', head);

    Console.WriteLine(head.ToString());

}
```

在所示的 `Node` 类中，`m_next` 必须引用另一个在 l `m_data` 字段中具有相同种类数据类型的节点。这意味着链表必须包含所有数据项类型均为相同类型（或派生类型）的节点。例如，我无法使用 `Node` 类创建一个其中一个元素包含 `char`，另一个元素包含 `DateTime`，而另一个元素包含 `String` 的链表。嗯，如果我处处都使用 `Node<object>`，但我就会失去编译时类型安全，并且值类型会被装箱。

因此，更好的方法是定义一个非泛型的 `Node` 基类，并使用 `Node` 类作为基类定义一个泛型的 `TypedNode` 类。现在，我可以有一个链表，其中每个节点都可以是特定的数据类型（而不是 `Object`），获得编译时类型安全并避免值类型的装箱。以下是新的类定义：

```
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

# 第 12 章 泛型 287

现在我可以写代码来创建一个链表，其中每个节点都是不同的数据类型。代码看起来像这样：

```
private static void DataLinkedList() {

    Node head = new TypedNode<char>('.');

    head = new TypedNode<DateTime>(DateTime.Now, head);

    head = new TypedNode<string>("Today is ", head);

    Console.WriteLine(head.ToString());

}
```

# 泛型类型标识性

有时泛型语法会困扰开发人员。毕竟，你的源代码中可能散布着许多小于 (`<`) 和大于 (`>`) 符号，这会损害可读性。为了改进语法，由于一些开发者会定义一个新的派自泛型类型的非泛型类类型，并指定所有的类型参数。例如，为了简化如下代码：

```
List<DateTime> dtl = new List<DateTime>();
```

某些开发者可能会先定义这样一个类：

```csharp
internal sealed class DateTime : List<DateTime> {
    // 这里没有要放的代码！
}
```

现在，创建列表的代码可以写得更简单（没有小于和大于符号），如下：

```
DateTimeList dtl = new DateTimeList();
```

虽然这看起来像是一种便利，特别是当你将新类型用于参数、局部变量和字段时，但你永远不要为了让源代码更易读而定义新类。然而，原型为接受 `DateTime` 的方法将无法接收 `List<DateTime>`。这是因为你正在比较两个不同的类型对象：

```csharp
Boolean sameType = (typeof(DateTime) == typeof(List<DateTime>
```

幸运的是，C# 提供了一种使用简化语法来引用泛型类型而完全不影响等效的方法；你可以使用源文件顶部的旧式 `using` 指令。这是一个示例：

```csharp
using DateTimeList = System.Collections.Generic.List<DateTime>;
```

在这里，`using` 指令实际上定义了一个名为 `DateTimeList` 的符号。随着代码的编译，编译器会将 `DateTimeList` 的所有出现替换为 `System.Collections.Generic.List<DateTime>`。这允许开发人员使用简化语法而不影响代码的实际含义，从而维护了类型标识和等效。因此，现在当执行以下行时，`sameType` 将初始化为 `true`：

```csharp
Boolean sameType = (typeof(List<DateTime>) == typeof(DateTimeList));
```

另一个便利是，你可以使用 C# 的隐式类型局部变量功能，编译器从赋值给方法局部变量的表达式类型中推断局部变量的类型：

```csharp
using System;
using System.Collections.Generic;
internal sealed class SomeType {
    private static void SomeMethod() {
        // 编译器推断 DateTimeList 的类型为
        // System.Collections.Generic.List<DateTime>
        var dtl = new List<DateTime>();
```

# 305 第二部分 设计类型

# 代码爆炸

当使用泛型类型参数的方法进行 JIT 编译时，CLR 获取该方法的 IL，替换指定的类型参数，然后创建特定于该方法操作指定数据类型的原生代码。这正是你所想要的，也是泛型的主要特性之一。然而，这也有缺点：CLR 为每个方法/类型组合保留泛型原生代码。这最终会大幅增加应用程序的工作集，从而影响性能。

幸运的是，CLR 内部内置了一些优化方案来减少代码爆炸。首先，如果一个方法为某个类型参数被调用，那么当使用相同的类型参数再次调用该方法时，CLR 将仅为该方法/类型组合编译一次代码。如果一个程序集使用了 `List<DateTime>`，而另一个完全不同的程序集

# 第 12 章 泛型 289

（在相同的 `AppDomain` 中加载）使用了 `List<DateTime>`，CLR 只会为 `List<DateTime>` 编译一次方法。这大幅减少了代码膨胀。

CLR 还有另一种优化：CLR 认为所有类型参数都是相同的，因此代码可以再次复用。例如，CLR 为 `List<String>` 方法编译的代码可以用于 `List<Stream>`，因为 `String` 和 `Stream` 都是引用类型。对于任何引用类型，都将使用相同的代码。CLR 能够执行此优化，是因为所有引用类型的参数或变量实际上只是指向堆上对象的指针（在 32 位 Windows 系统上为 32 位，在 64 位 Windows 系统上为 64 位），并且对象指针都以相同的方式进行操作。

但如果任何参数是值类型，CLR 必须专门为该值类型生成原生代码，因为值类型的大小各不相同。即使两个类型的大小相同（例如 `Int32` 和 `UInt32`，均为 32 位），CLR 也无法共享代码，因为可以使用不同的原生 CPU 指令来处理这些值。

## 泛型接口

显然，定义泛型引用类型和值类型的能力是泛型的主要特征。然而，允许泛型接口对 CLR 至关重要。如果没有泛型接口，当你使用非泛型接口（如 `IComparable`）来操作值类型时，会再次发生装箱和编译时类型安全性的丢失。这将严重限制泛型类型的用性。因此，CLR 支持泛型接口。引用类型或值类型可以通过指定类型参数来实现泛型接口，或者类型可以通过留留未指定的类型参数来实现泛型接口。让我们来看一些示例。

以下是 `System.Collections.Generic` 命名空间中作为框架类库（FCL）一部分提供的泛型接口定义：

```
public interface IEnumerator<T> : IDisposable, IEnumerator {
  T Current { get; }
}
```

这是一个实现该泛型接口并指定参数的类型示例。注意 `Triangle` 对象可以枚举一个 `Point` 对象集合。还要注意 `Current` 属性的类型是 `Point`：

```
internal sealed class Triangle : IEnumerator<Point> {
  private Point[] m_vertices;
  // IEnumerator<Point> 的 Current 属性类型为 Point
  public Point Current { get { ... } }
}
```

## 290 第二部分 类型设计

现在让我们来看一个实现相同泛型接口但未指定类型参数的示例：

```
internal sealed class ArrayEnumerator<T> : IEnumerator<T> {
    private T[] m_array;
    // IEnumerator<T> 的 Current 属性类型为 T
    public T Current (get { ... })
}
```

注意 `ArrayEnumerator` 对象可以枚举一个 `T` 对象集合（其中 T 是未指定的，仅通过使用泛型 `ArrayEnumerator` 类型稍后指定类型）。还要注意 `Current` 属性现在是未指定的数据类型 `T`。关于泛型接口的更多信息将在第 13 章“接口”中介绍。

## 泛型委托

CLR 支持委托以确保任何类型的对象都能以类型安全的方式传递给回调方法。此外，泛型委托允许值类型实例在没有任何装箱的情况下传递给回调方法。正如第 17 章“委托”中所讨论的，委托实际上是一个带有四个方法的类定义：构造函数、`Invoke` 方法、`BeginInvoke` 方法和 `EndInvoke` 方法。当你定义一个指定类型参数的委托类型时，编译器会定义委托类的方法，类型参数将应用于任何具有指定类型参数/返回值的方法。

例如，你这样定义一个泛型委托：

```
public delegate TReturn<TReturn, TKey, TValue>(TKey key, TValue value);
public sealed CallMe<TReturn, TKey, TValue> : MulticastDelegate {
    public virtual CallMe(Object object, IntPtr method);
    public virtual TReturn Invoke(TKey key, TValue value);
    public virtual AsyncResult BeginInvoke(TKey key, TValue value,
        AsyncCallback callback, Object object);
    public virtual TReturn EndInvoke(AsyncResult result);
}
```

编译器将将其转换为如下所示的类：

> 建议你尽可能使用框架类库（FCL）中预定义的泛型 `Action` 和 `Func` 委托。我在第 17 章“委托”的“不再需要委托定义（泛型委托）”部分中描述了这些类型。

## 委托和接口的逆变与协变泛型参数

委托的每个泛型类型参数都可以标记为协变（covariant）或逆变（contravariant）。此功能允许你将泛型委托类型的变量强制转换为泛型参数类型不同的相同委托。泛型类型参数可以是以下任意一种：

- **不变（Invariant）**：意味着泛型类型参数不能更改。在本章中，我只展示了不变的泛型类型参数。
- **逆变（Contravariant）**：意味着泛型类型参数可以从类变为其派生类。在 C# 中，你通过 `in` 关键字指示逆变泛型类型参数。逆变泛型类型参数只能出现在方法的参数位置。
- **协变（Covariant）**：意味着泛型类型参数可以从一个类变为其基类。在 C# 中，你通过 `out` 关键字指示协变泛型类型参数。协变泛型类型参数只能出现在方法的返回值位置。

# 第 12 章 泛型 293

重要：有时开发者会问，为什么他们必须在泛型类型参数上显式地放入 `in` 或 `out`。他们认为编译器应该能够启用委托或接口声明，并自动检测哪些泛型类型参数是协变或变变的。虽然编译器确实可以自动检测这些，但 C# 团队相信声明一种契约，并且你应该显式地说明你想要允许的内容。例如，如果编译器确定一个泛型类型参数可以是协变的，而随后你向一个接口添加了该类型参数位于输出位置的成员，这将会是非常糟糕的。当你下一次编写代码时，编译器会确定该类型参数应该是是不变的，但如果你之前利用了类型参数是协变的这一事实，那么所有引用其他成员的代码处现在可能都会产生错误。

出于这个原因，编译器在声明泛型参数时强制你进行显式操作。如果你随后尝试在与声明不符的上下文中使用此类型参数，编译器会发出错误，告知你正尝试破坏契约。如果你决定通过在泛型参数上添加 `in` 或 `out` 来破坏契约，你应该预计需要修改一些在使用旧契约的代码处。

# 泛型方法

当你定义一个泛型类、结构体或接口时，在这些类型中定义的任何方法都可以引用由类型指定的类型参数。类型参数可以用作方法的参数、返回值，或者方法内部定义的局部变量。然而，CLR 还支持方法指定其自身的类型参数。这些类型参数也可以用于参数、返回值或局部变量。这里有一个稍显刻意的类型示例，该类型定义了一个泛型参数，并且包含一个拥有其自己的泛型参数的方法：

```csharp
internal sealed class Generic<T> {
    private T m_value;
    public Generic(T value) { m_value = value; }
    public TOutput Output<TOutput>() {
        TOutput result = (TOutput) Convert.ChangeType(m_value, typeof(TOutput));
        return result;
    }
}
```

在这个示例中，你可以看到 `Generic` 类定义了它自己的类型参数 (`T`)，而 `Output` 方法定义了它自己的类型参数 (`TOutput`)。这允许构造一个 `Generic` 类型来与任何类型协作。`Output` 方法可以根据调用时传递的参数，将 `m_value` 字段引用的对象转换为各种类型。类型参数和方法参数的能力提供了极大的灵活性。

# 294 第二部分 设计类型

泛型方法的一个相当不错的例子是 **Swap** 方法：

```csharp
private static void Swap<T>(ref T o1, ref T o2) {
    T temp = o1;
    o1 = o2;
    o2 = temp;
}
```

代码现在可以像这样调用 **Swap**：

```csharp
private static void CallingSwap() {
    Int32 n1 = 1, n2 = 2;
    Console.WriteLine("n1={0}, n2={1}", n1, n2);
    Swap(ref n1, ref n2);
    Console.WriteLine("n1={0}, n2={1}", n1, n2);
}
```
