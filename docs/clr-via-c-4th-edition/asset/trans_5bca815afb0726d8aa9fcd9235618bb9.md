
尽管 CLR 确实允许接口定义静态方法、静态字段、常量和静态构造函数，但符合公共语言规范（CLS）的接口不得包含任何这些静态成员，因为有些编程语言无法定义或访问它们。事实上，C# 会阻止接口定义任何这些静态成员。

在 C# 中，你使用 interface 关键字来定义接口，为其指定名称和一组实例方法签名。下面是框架类库（FCL）中定义的几个接口的定义。

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

对 CLR 而言，接口定义就像类型定义一样。也就是说，CLR 会为接口类型对象定义一个内部数据结构，并且可以使用反射来查询接口类型的特性。与类型一样，接口可以定义在文件作用域中，也可以嵌套定义在另一个类型中。定义接口类型时，你可以指定任意想要的可见性/可访问性（public、protected、internal 等）。

按照惯例，接口类型名称以大写字母 I 为前缀，这使得在源代码中很容易识别接口类型。CLR 确实支持泛型接口（从前面的一些示例中可以看到），也支持接口中的泛型方法。本章后面以及第 12 章“泛型”中，我将讨论泛型接口提供的许多特性中的一部分，那一章会更广泛地介绍泛型。

接口定义可以“继承”其他接口。不过，我在这里使用“继承”一词比较宽松，因为接口继承的工作方式并不完全像类继承。我更愿意把接口继承理解为包含其他接口的契约。例如，ICollection<T> 接口定义包含 IEnumerable<T> 和 IEnumerable 接口的契约。这意味着：

- 任何继承 `ICollection<T>` 接口的类都必须实现 `ICollection<T>`、`IEnumerable<T>` 和 `IEnumerable` 接口定义的所有方法。
- 任何期望某个对象的类型实现 `ICollection<T>` 接口的代码，都可以假定该对象的类型也实现了 `IEnumerable<T>` 和 `IEnumerable` 接口的方法。

## 继承接口

在本节中，我将演示如何定义实现某个接口的类型，然后演示如何创建该类型的实例，并使用该对象调用接口的方法。C# 实际上让这件事变得相当简单，但幕后发生的事情要稍微复杂一些。本章后面我会解释幕后发生了什么。

`System.IComparable<T>` 接口（在 MSCorLib.dll 中）定义如下。

```csharp
public interface IComparable<in T> {
    Int32 CompareTo(T other);
}
```

下面的代码演示如何定义实现该接口的类型，还演示了比较两个 Point 对象的代码。

```csharp
using System;

// Point is derived from System.Object and implements IComparable<T> for Point.
public sealed class Point : IComparable<Point> {
    private Int32 m_x, m_y;

    public Point(Int32 x, Int32 y) {
        m_x = x;
        m_y = y;
    }

    // This method implements IComparable<T>.CompareTo() for Point.
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
public static class Program {
    public static void Main() {
        Point[] points = new Point[] {
            new Point(3, 3),
            new Point(1, 2),
        };

        // Here is a call to Point's IComparable<T> CompareTo method
        if (points[0].CompareTo(points[1]) > 0) {
            Point tempPoint = points[0];
            points[0] = points[1];
            points[1] = tempPoint;
        }
        Console.WriteLine("Points closest to (0, 0) to farthest:");
        foreach (Point p in points)
            Console.WriteLine(p);
    }
}
```

C# 编译器要求实现接口的方法必须标记为 public。CLR 要求接口方法必须标记为 virtual。如果你在源代码中没有显式将方法标记为 virtual，编译器会将该方法标记为 virtual 和 sealed；这会阻止派生类重写该接口方法。如果你显式将方法标记为 virtual，编译器会将该方法标记为 virtual（并保持未 sealed）；这允许派生类重写该接口方法。

如果接口方法是 sealed，派生类就不能重写该方法。不过，派生类可以重新继承同一个接口，并可以为该接口的方法提供自己的实现。在对象上调用接口方法时，会调用与该对象类型关联的实现。下面是一个演示这一点的示例。

```csharp
using System;

public static class Program {
    public static void Main() {
        /********************** First Example ***********************/
        Base b = new Base();

        // Calls Dispose by using b's type: "Base's Dispose"
        b.Dispose();

        // Calls Dispose by using b's object's type: "Base's Dispose"
        ((IDisposable)b).Dispose();


        /********************** Second Example ***********************/
        Derived d = new Derived();

        // Calls Dispose by using d's type: "Derived's Dispose"
        d.Dispose();

        // Calls Dispose by using d's object's type: "Derived's Dispose"
        ((IDisposable)d).Dispose();

        /*************************** Third Example ***************************/
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
}
```

## 更多关于调用接口方法的内容

FCL 的 System.String 类型继承 System.Object 的方法签名及其实现。此外，String 类型还实现了几个接口：IComparable、ICloneable、IConvertible、IEnumerable、IComparable<String>、IEnumerable<Char> 和 IEquatable<String>。这意味着 String 类型不需要实现（或重写）其 Object 基类型提供的方法。不过，String 类型必须实现所有接口中声明的方法。

CLR 允许你定义接口类型的字段、参数或局部变量。使用接口类型的变量可以调用该接口定义的方法。此外，CLR 还允许你调用 Object 定义的方法，因为所有类都继承 Object 的方法。下面的代码演示了这一点。

```csharp
    // The s variable refers to a String object.
    String s = "Jeffrey";
    // Using s, I can call any method defined in
    // String, Object, IComparable, ICloneable, IConvertible, IEnumerable, etc.
    
    // The cloneable variable refers to the same String object
    ICloneable cloneable = s;
```
