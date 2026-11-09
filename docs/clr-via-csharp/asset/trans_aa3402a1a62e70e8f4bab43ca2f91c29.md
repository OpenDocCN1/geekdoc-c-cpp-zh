
## 类和接口继承

在 Microsoft .NET Framework 中，有一个名为 **System.Object** 的类，它定义了四个公共实例方法：**ToString**、**Equals**、**GetHashCode** 和 **GetType**。这个类是所有其他类的根类或最终基类——所有类都会继承 **Object** 的四个实例方法。这也意味着，为操作 **Object** 类的实例而编写的代码，实际上可以对任何类的实例执行操作。

由于 Microsoft 的某个人已经实现了 **Object** 的方法，任何从 **Object** 派生的类实际上都继承了以下内容：

- **方法签名** 这使代码可以认为自己操作的是 **Object** 类的实例，而实际上它可能操作的是某个其他类的实例。
- **这些方法的实现** 这使定义从 **Object** 派生的类的开发者无需手动实现 **Object** 的方法。

在 CLR 中，一个类总是派生自一个且仅一个类（该最终必须派生自 **Object**）。这个基类提供了一组方法签名以及这些方法的实现。定义新类的一个很棒的地方在于，它可以成为将来由其他开发者定义的另一个类的基类——所有方法签名及其实现都会被新的派生类继承。

CLR 还允许开发者定义*接口*，这实际上只是一种为一组方法签名命名的方式。这些方法完全不附带任何实现。类通过指定接口名称来继承接口，并且在该类显式提供接口方法的实现之后，CLR 才会认为该类型定义有效。当然，实现接口方法可能很繁琐，这就是为什么我把接口继承称为实现多重继承的一种简化机制。C# 编译器和 CLR 实际上允许一个类继承多个接口，当然，该类必须为所有继承的接口方法提供实现。

类继承的一大特性是，它允许派生类型的实例在所有期望基类型实例的上下文中被替换使用。类似地，接口继承允许实现了接口的类型的实例在所有期望该命名接口类型实例的上下文中被替换使用。现在我们将看看如何定义接口，以便让讨论更加具体。

### 定义接口

如上一节所述，接口是一组有名称的方法签名。请注意，接口还可以定义事件、无参数属性和带参数的属性（C# 中的索引器），因为如前几章所示，所有这些都只是映射到方法的语法简写。然而，接口不能定义任何构造函数方法。此外，接口不允许定义任何实例字段。

尽管 CLR 确实允许接口定义静态方法、静态字段、常量和静态构造函数，但符合公共语言基础结构（CLI）的接口不得包含任何这些静态成员，因为有些编程语言无法定义或访问它们。事实上，C# 会阻止接口定义任何这些静态成员。

在 C# 中，你使用 **interface** 关键字来定义接口，为其指定名称及其一组实例方法签名。以下是框架类库（FCL）中定义的几个接口的定义：

```csharp
public interface IDisposable {
    void Dispose();
}

public interface IEnumerable {
    IEnumerator GetEnumerator();
}

public interface IEnumerable<out T> : IEnumerable {
    new IEnumerator<T> GetEnumerator();
}

public interface ICollection<T> : IEnumerable<T>, IEnumerable {
    void Add(T item);
    void Clear();
    Boolean Contains(T item);
    void CopyTo(T[] array, Int32 arrayIndex);
    Boolean Remove(T item);
    Int32 Count { get; } // Read-only property
    Boolean IsReadOnly { get; } // Read-only property
}
```

对 CLR 来说，接口定义就像类型定义一样。也就是说，CLR 会为接口类型对象定义内部数据结构，并且可以使用反射来查询接口类型的特性。与类型一样，接口可以在文件范围内定义，也可以嵌套在另一个类型中定义。定义接口类型时，你可以指定所需的任何可见性/可访问性（public、protected、internal 等）。

按照约定，接口类型名称以大写字母 I 为前缀，这样可以很容易地在源代码中发现接口类型。CLR 确实支持泛型接口（从前面的某些示例可以看出），也支持接口中的泛型方法。本章后面以及第 12 章“泛型”中，我将讨论泛型接口提供的众多特性中的一些；在该章中我会更广泛地介绍泛型。

接口定义可以“继承”其他接口。然而，我在这里使用“继承”一词比较宽松，因为接口继承的工作方式与类继承并不完全相同。我更愿意把接口继承看作包含其他接口的契约。

例如，`ICollection<T>` 接口定义包含 `IEnumerable<T>` 和 `IEnumerable` 接口的契约。这意味着：

- 任何继承 `ICollection<T>` 接口的类都必须实现由 `ICollection<T>`、`IEnumerable<T>` 和 `IEnumerable` 接口定义的所有方法。
- 任何期望对象类型实现 `ICollection<T>` 接口的代码，都可以假定该对象的类型也实现了 `IEnumerable<T>` 和 `IEnumerable` 接口的方法。

### 继承接口

在本节中，我将展示如何定义实现接口的类型，然后展示如何创建该类型的实例并使用该对象调用接口的方法。C# 实际上使这件事相当简单，但幕后发生的事情要稍微复杂一些。我将在本章后面解释幕后发生的事情。

`System.IComparable<T>` 接口（在 MSCorLib.dll 中）定义如下：

```csharp
public interface IComparable<in T> {
    Int32 CompareTo(T other);
}
```

以下代码展示了如何定义实现此接口的类型，还展示了比较两个 **Point** 对象的代码：

```csharp
using System;

// Point is derived from System.Object and implements IComparable<T> for Point.
public sealed class Point : IComparable<Point> {
    private Int32 m_x, m_y;

    public Point(Int32 x, Int32 y) {
        m_x = x;
        m_y = y;
    }

    // This method implements IComparable<T>.CompareTo() for Point
    public Int32 CompareTo(Point other) {
        return Math.Sign(Math.Sqrt(m_x * m_x + m_y * m_y)
            - Math.Sqrt(other.m_x * other.m_x + other.m_y * other.m_y));
    }

    public override String ToString() {
        return String.Format("({0}, {1})", m_x, m_y);
    }
}
```

```csharp
((IDisposable)d).Dispose();

/*********************** Third Example ***********************/
b = new Derived();

// Calls Dispose by using b's type: "Base's Dispose"
b.Dispose();

// Calls Dispose by using b's object's type: "Derived's Dispose"
((IDisposable)b).Dispose();
}

// This class is derived from Object and it implements IDisposable
internal class Base : IDisposable {
    // This method is implicitly sealed and cannot be overridden
    public void Dispose() {
        Console.WriteLine("Base's Dispose");
    }
}

// This class is derived from Base and it re-implements IDisposable
internal class Derived : Base, IDisposable {
    // This method cannot override Base's Dispose. 'new' is used to indicate
    // that this method re-implements IDisposable's Dispose method
    new public void Dispose() {
        Console.WriteLine("Derived's Dispose");

        // NOTE: The next line shows how to call a base class's implementation (if desired)
        // base.Dispose();
    }
}
```

### 关于调用接口方法的更多内容

FCL 的 **System.String** 类型继承 **System.Object** 的方法签名及其实现。此外，**String** 类型还实现了几个接口：IComparable、ICloneable、IConvertible、IEnumerable、IComparable<String>、IEnumerable<Char> 和 IEquatable<String>。这意味着 **String** 类型不需要实现（或重写）其 **Object** 基类型提供的方法。然而，**String** 类型必须实现所有接口中声明的方法。

CLR 允许定义接口类型的字段、参数或局部变量。使用接口类型的变量可以调用该接口定义的方法。此外，CLR 还允许调用 **Object** 定义的方法，因为所有类都继承 **Object** 的方法。以下代码演示了这一点：
