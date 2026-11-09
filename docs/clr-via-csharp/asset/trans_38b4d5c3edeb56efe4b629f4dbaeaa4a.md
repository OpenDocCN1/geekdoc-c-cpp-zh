
有时在与其他代码集成时，你可能必须实现一个非泛型接口，因为该接口的泛型版本根本不存在。在这种情况下，如果接口的任何方法接受或返回 **Object**，你将失去编译时类型安全，并且对值类型会发生装箱。你可以通过使用我在本章末尾附近的“使用显式接口方法实现改进编译时类型安全”一节中描述的技术，在一定程度上缓解这种情况。

泛型接口的第三个好处是，一个类可以多次实现同一个接口，只要使用不同的类型参数。下面的代码展示了一个示例，说明这可能多么有用：

```csharp
using System;

// This class implements the generic IComparable<T> interface twice
public sealed class Number: IComparable<Int32>, IComparable<String> {
    private Int32 m_val = 5;

    // This method implements IComparable<Int32>'s CompareTo
    public Int32 CompareTo(Int32 n) {
        return m_val.CompareTo(n);
    }

    // This method implements IComparable<String>'s CompareTo
    public Int32 CompareTo(String s) {
        return m_val.CompareTo(Int32.Parse(s));
    }
}

public static class Program {
    public static void Main() {
        Number n = new Number();

        // Here, I compare the value in n with an Int32 (5)
        IComparable<Int32> cInt32 = n;
        Int32 result = cInt32.CompareTo(5);

        // Here, I compare the value in n with a String ("5")
        IComparable<String> cString = n;
        result = cString.CompareTo("5");
    }
}
```

接口的泛型类型参数还可以标记为逆变和协变，这为使用泛型接口提供了更大的灵活性。关于逆变和协变的更多信息，请参见第12章中的“委托和接口的逆变与协变泛型类型参数”一节。

```csharp
private static Int32 M(IComparable t) {
   ...
}
```

然后，为了将 `x` 传递给 `M`，`x` 必须被装箱。

对于接口约束，C# 编译器会发出某些中间语言 (IL) 指令，这些指令导致直接在值类型上调用接口方法而不对其进行装箱。除了使用接口约束之外，没有其他方法可以让 C# 编译器发出这些 IL 指令，因此，在值类型上调用接口方法总是会导致装箱。

## 实现多个具有相同方法名称和签名的接口

有时，你可能会发现自己定义了一个类型，它实现了多个接口，而这些接口定义了具有相同名称和签名的方法。例如，假设定义了两个接口如下：

```csharp
public interface IWindow {
   Object GetMenu();
}

public interface IRestaurant {
   Object GetMenu();
}
```

假设你想定义一个实现这两个接口的类型。你必须通过使用显式接口方法实现来定义该类型的成员，如下所示：

```csharp
// This type is derived from System.Object and
// implements the IWindow and IRestaurant interfaces.
public sealed class MarioPizzeria : IWindow, IRestaurant {

   // This is the implementation for IWindow's GetMenu method.
   Object IWindow.GetMenu() { ... }

   // This is the implementation for IRestaurant's GetMenu method.
   Object IRestaurant.GetMenu() { ... }

   // This (optional method) is a GetMenu method that has nothing
   // to do with an interface.
   public Object GetMenu() { ... }
}
```

因为这个类型必须实现多个独立的 **GetMenu** 方法，所以你需要告诉 C# 编译器哪个 **GetMenu** 方法包含针对特定接口的实现。

使用 **MarioPizzeria** 对象的代码必须强制转换为特定的接口才能调用所需的方法。以下代码演示了这一点：

```csharp
MarioPizzeria mp = new MarioPizzeria();

// This line calls MarioPizzeria's public GetMenu method
mp.GetMenu();

// These lines call MarioPizzeria's IWindow.GetMenu method
IWindow window = mp;
window.GetMenu();

// These lines call MarioPizzeria's IRestaurant.GetMenu method
IRestaurant restaurant = mp;
restaurant.GetMenu();
```

## 使用显式接口方法实现改进编译时类型安全

接口很棒，因为它们定义了类型之间相互通信的标准方式。前面我谈到了泛型接口，以及它们如何改进编译时类型安全并减少装箱。不幸的是，有时你可能需要实现一个非泛型接口，因为泛型版本不存在。如果接口的任何方法接受 **System.Object** 类型的参数或返回 **System.Object** 类型的值，你将失去编译时类型安全，并且会发生装箱。在本节中，我将向你展示如何使用 EIMI 在一定程度上改善这种情况。

看看非常常见的 **IComparable** 接口：

```csharp
public interface IComparable {
    Int32 CompareTo(Object other);
}
```

这个接口定义了一个方法，它接受 **System.Object** 类型的参数。如果我定义自己的类型来实现这个接口，类型定义可能如下所示：

```csharp
internal struct SomeValueType : IComparable {
    private Int32 m_x;
    public SomeValueType(Int32 x) { m_x = x; }
    public Int32 CompareTo(Object other) {
        return(m_x - ((SomeValueType) other).m_x);
    }
}
```

使用 **SomeValueType**，我现在可以编写以下代码：

```csharp
public static void Main() {
    SomeValueType v = new SomeValueType(0);
    Object o = new Object();
    Int32 n = v.CompareTo(v); // Undesired boxing
    n = v.CompareTo(o);      // InvalidCastException
}
```

这段代码有两个不理想的特性：

- **不希望的装箱** 当 `v` 作为参数传递给 `CompareTo` 方法时，必须对它进行装箱，因为 `CompareTo` 期望一个 `Object`。
- **缺乏类型安全** 这段代码可以编译，但当 `CompareTo` 方法尝试将 `o` 强制转换为 `SomeValueType` 时，会在方法内部抛出 `InvalidCastException`。

这两个问题都可以通过使用 EIMI 来修复。下面是 `SomeValueType` 的一个修改版本，其中添加了一个 EIMI：

```csharp
internal struct SomeValueType : IComparable {
    private Int32 m_x;
    public SomeValueType(Int32 x) { m_x = x; }

    public Int32 CompareTo(SomeValueType other) {
        return(m_x - other.m_x);
    }

    // NOTE: No public/private used on the next line
    Int32 IComparable.CompareTo(Object other) {
        return CompareTo((SomeValueType) other);
    }
}
```

注意这个新版本中的几处变化。首先，它现在有两个 `CompareTo` 方法。第一个 `CompareTo` 方法不再接受 `Object` 作为参数；它现在改为接受 `SomeValueType`。因为这个参数已经改变，所以将 `other` 强制转换为 `SomeValueType` 的代码不再必要，并且已被移除。其次，将第一个 `CompareTo` 方法改为类型安全意味着 `SomeValueType` 不再遵守通过实现 `IComparable` 接口而施加给它的契约。因此，`SomeValueType` 必须实现一个满足 `IComparable` 契约的 `CompareTo` 方法。这就是第二个 `IComparable.CompareTo` 方法的工作，它是一个 EIMI。

做出这两处更改意味着我们现在获得了编译时类型安全，并且没有装箱：

```csharp
public static void Main() {
    SomeValueType v = new SomeValueType(0);
    Object o = new Object();
    Int32 n = v.CompareTo(v); // No boxing
    n = v.CompareTo(o);      // compile-time error
}
```

然而，如果我们定义一个接口类型的变量，我们将再次失去编译时类型安全，并经历不希望的装箱：

```csharp
public static void Main() {
    SomeValueType v = new SomeValueType();
    IComparable c = v;             // Boxing

    Object o = new Object();
    Int32 n = c.CompareTo(v);       // Undesired boxing
    n = c.CompareTo(o);             // InvalidCastException
}
```

事实上，正如本章前面提到的，当将值类型实例强制转换为接口类型时，CLR 必须对该值类型实例进行装箱。由于这个事实，前面的 Main 方法中会发生两次装箱。

在实现 **IConvertible**、**ICollection**、**IList** 和 **IDictionary** 等接口时，经常会使用 EIMI。它们让你能够创建这些接口方法的类型安全版本，并且使你能够减少值类型的装箱操作。

## 小心使用显式接口方法实现

对你来说，理解使用 EIMI 时存在的一些后果至关重要。而且由于这些后果，你应该尽可能避免使用 EIMI。幸运的是，泛型接口在相当大程度上帮助你避免 EIMI。但有时你仍然需要使用它们（例如实现两个具有相同名称和签名的接口方法）。以下是 EIMI 的主要问题：

- 没有文档说明某个类型如何具体实现 EIMI 方法，也没有 Microsoft Visual Studio IntelliSense 支持。
- 值类型实例在强制转换为接口时会被装箱。
- 派生类型无法调用 EIMI。

让我们更仔细地看看这些问题。

在查看 .NET Framework 参考文档中某个类型的方法时，会列出显式接口方法实现，但不存在特定于类型的帮助；你只能阅读有关接口方法的一般帮助。例如，**Int32** 类型的文档显示它实现了 **IConvertible** 接口的所有方法。这很好，因为开发者知道这些方法存在；然而，这对开发者来说非常令人困惑，因为你不能直接在 **Int32** 上调用 **IConvertible** 方法。例如，以下方法将无法编译：
