
# 通过显式接口方法提高编译时类型安全

接口是非常棒，因为它们为类型定义了一种标准方式。有时在与其他代码集成时，你可能需要实现一个非泛型接口，因为该接口的泛型版本根本不存在。在这种情况下，如果接口的任何方法接收或返回 `Object`，你将失去编译时类型安全，并且会在值类型上发生装箱。你可以通过使用“通过显式接口方法提高编译时类型安全”技术，在某种程度上缓解这种情况。

泛型接口的第三个好处是，类可以根据不同的类型参数多次实现同一个接口。以下代码展示了这种用法有多用：

```csharp
using System;

// 此类实现了两次泛型 IComparable<T> 接口 
public sealed class Number: IComparable<Int32>, IComparable<String> {
    private Int32 m_val = 10;
```

# 第 13 章 接口 317

有时在与其他代码集成时，你可能需要实现一个非泛型接口，因为该接口的泛型版本根本不存在。在这种情况下，如果接口的任何方法接收或返回 `Object`，你将失去编译时类型安全，并且会在值类型上发生装箱。你可以通过使用“通过显式接口方法提高编译时类型安全”技术，在某种程度上缓解这种情况。

泛型接口的第三个好处是，类可以根据不同的类型参数多次实现同一个接口。以下代码展示了这种用法有多用：

```csharp

using System;

// 此类实现了两次泛型 IComparable<T> 接口

public sealed class Number: IComparable<Int32>, IComparable<String> {

    private Int32 m_val = 10;

    // 此方法实现了 IComparable<Int32> 的 CompareTo

    public Int32 CompareTo(Int32 n) {

        return m_val.CompareTo(n);

    }

    // 此方法实现了 IComparable<String> 的 CompareTo

    public Int32 CompareTo(String s) {

        return m_val.CompareTo(Int32.Parse(s));

    }

}

public static class Program {

    public static void Main() {

        Number n = new Number();

        // 这里，我将 n 中的值与 Int32 (10) 进行比较

        IComparable<Int32> cInt32 = n;

        Int32 result = cInt32.CompareTo(10);

        // 这里，我将 n 中的值与 String ("S") 进行比较

        IComparable<String> cString = n;

        result = cString.CompareTo("S");

    }

}

```

接口的泛型类型参数还可以标记为逆变（contravariant）和协变（covariant），这为使用泛型接口提供了更大的活性。关于更多逆变和协变，请参见第 12 章中的“委托和接口的逆变与协变泛型类型参数”部分。

# 泛型与接口约束

在上节中，我讨论了使用泛型接口的好处。在本节中，我将讨论将泛型类型参数约束在接口上的用处。

第一个好处是，你可以将单个泛型类型参数约束在多个接口上。当你这样做时，你传递的参数类型必须实现所有的接口约束。这是一个示例：

```csharp

public static class SomeType {

    private static void Test() {

        Int32 x = 5;

        Guid g = new Guid();

        // 对 M 的此调用编译通过，因为

        // Int32 实现了 IComparable 和 IConvertible

        M(x);

        // 对 M 的此调用会导致编译器错误，因为

        // Guid 实现了 IComparable 但没有实现 IConvertible

        M(g);

    }

    // M 的类型参数 T 被约束为仅适用于实现了

    // 同时 IComparable 和 IConvertible 接口的类型

    private static Int32 M<T>(T t) where T : IComparable, IConvertible {

    }

}

```

这实际上非常酷！当你定义方法的参数时，每个参数的类型都表示参数必须是该参数类型或其派生类型。如果参数类型是接口，则表示只要该类实现了该接口，参数就可以是任何类。使用多个接口约束实际上允许方法指示传递的参数必须实现接口。

事实上，如果我们将 `T` 约束为一个类和两个接口，我们是在说参数的类型必须是指定的基类（或其派生类），并且它还实现这两个接口。这种灵活性允许方法真正规定调用者可以传递什么，如果调用者不满足这些约束，将生成编译器错误。

接口约束的第二个好处是减少了值类型实例的装箱。在之前的代码段中，`M` 方法传递了 `x`（`Int32` 的实例，这是一个值类型）。当 `x` 传递给 `M` 时，不会发生装箱。如果 `M` 内部的代码调用了 `t.CompareTo(...)`，则在调用时不会发生装箱（传递给 `CompareTo` 的参数可能仍会装箱）。

另一方面，如果 `M` 声明如下所示：

```csharp

private static Int32 M(IComparable t) {

...

}

```

那么，为了将 `x` 传递给 `M`，C# 编译器会发出某些中间语言 `IL` 指令，导致直接在值类型上调用接口方法而不进行装箱。除了接口约束外，没有其他方法可以让 C# 编译器发出这些 `IL` 指令，因此，在值类型上调用接口方法始终会导致装箱。

# 实现具有相同方法名和签名的多个接口

有时，你发现自己定义了一个实现多个接口的类型，并定义了具有相同名称和签名的方法。例如，假设定义了两个接口：

```csharp

public interface IWindow {

  Object GetMenu();

}

public interface IRestaurant {

  Object GetMenu();

}

```

假设你想定义一个同时实现这两个接口的类型。你必须通过显式接口方法实现来实现该类型的成员：

```csharp

// 此类型派自 System.Object 并

// 实现了 IWindow 和 IRestaurant 接口。

public sealed class MarioPizzeria : IWindow, IRestaurant {

    // 这是 IWindow 的 GetMenu 方法的实现

    Object IWindow.GetMenu() { ... }

    // 这是 IRestaurant 的 GetMenu 方法的实现

    Object IRestaurant.GetMenu() { ... }

    // 此（可选的）方法是一个 GetMenu 方法，与接口

    // 无关。

    public override Object GetMenu() { ... }

}

```

由于此类型必须实现多个且独立的 `GetMenu` 方法，你需要告诉 C# 编译器哪一个 `GetMenu` 方法包含特定接口的实现。

# 320 第二部分 设计类型

使用 `MarioPizzeria` 对象的代码必须转换为特定接口以调用所需的方法。以下代码演示了：

```csharp

MarioPizzeria mp = new MarioPizzeria();

// 此行调用了 MarioPizzeria 的公共 GetMenu 方法

mp.GetMenu();

// 这些行调用了 MarioPizzeria 的 IWindow.GetMenu 方法

IWindow window = mp;

window.GetMenu();

// 这些行调用了 MarioPizzeria 的 IRestaurant.GetMenu 方法

IRestaurant restaurant = mp;

restaurant.GetMenu();

```

# 通过显式接口方法提高编译时类型安全

接口是非常棒，因为它们为类型定义了一种标准方式。有时在与其他代码集成时，你可能需要实现一个非泛型接口，因为该接口的泛型版本根本不存在。在这种情况下，如果接口的任何方法接收或返回 `Object`，你将失去编译时类型安全，并且会在值类型上发生装箱。你可以通过使用“通过显式接口方法提高编译时类型安全”技术，在某种程度上缓解这种情况。

泛型接口的第三个好处是，类可以根据不同的类型参数多次实现同一个接口。以下代码展示了这种用法有多用：

# 第二部分 设计类型

然而，如果我们定义一个接口类型的变量，我们将失去编译时的类型安全，并再次经历不期望的装箱（boxing）：

```sharp

public static void Main() {

    SomeValueType v = new SomeValueType(0);

    IComparable c = v; // 装箱！

    Object o = new Object();

    Int32 n = c.CompareTo(v); // 不期望的装箱

    n = c.CompareTo(o); // 无效转换异常

}

```

事实上，正如本章前面提到的，当将值类型强制转换为接口类型时，CLR 必须对值实例进行装箱。由于这一事实，在之前的 `Main` 方法中发生了两次装箱。

在实现 `IConvertible`、`ICollection`、`IList` 和 `IDictionary` 等接口时，经常使用显式实现（EIMI）。它们允许你创建这些接口方法的类型安全版本，并让你能够减少值类型的装箱操作。

# 小心显式接口方法实现 (EIMI)

理解使用 EIMI 时存在的某些影响来说至关重要。由于这些影响，你应该尽可能避免使用 EIMI。幸运的是，泛型接口可以帮你避开很多 EIMI。但在某些你可能需要使用它们（例如实现两个具有相同名称和签名的接口方法）。以下是 EIMI 的主要问题：

- 没有文档说明某个类型如何具体实现 EIMI 方法，而且没有 Visual Studio 智能感知（IntelliSense）支持。
- 值类型实例在转换为接口时会发生装箱。
- 派生类型无法调用 EIMI。

让我们仔细查看一下这些问题。

在查阅 .NET Framework 参考文档中某个类型的方法时，虽然列出了显式接口方法实现，但没有针对特定类型的帮助；你只需要阅读关于接口方法的通用帮助即可。例如，`Int32` 类型的文档显示它实现了 `IConvertible` 接口的所有方法。这是件好事，因为开发者知道这些方法存在；然而，这一直让开发者感到非常困惑，因为你不能直接在 `Int32` 上调用 `IConvertible` 方法。例如，以下方法将无法编译：

```csharp

public static void main() {

  Int32 x = S;

  Single s = x.ToSingle(null); // 尝试调用 IConvertible 方法

}

```

编译时，C# 编译器会产生以下消息：'messagepill7: 'int' 不包含 'ToSingle' 的定义'。这个错误让开发者感到困惑，因为它清楚地表示 `Int32` 类型没有定义 `ToSingle` 方法，但实际上，它是定义了。

要在 `Int32` 上调用 `ToSingle`，你必须先将 `Int32` 转换为 `IConvertible`，如下所示方法所示：

```csharp

public static void main() {

  Int32 x = S;

  Single s = ((IConvertible) x).ToSingle(null);

}

```

要求这一点并不显而易见，许多开发者无法自己发现。甚至还有一个更棘手的问题：将 `Int32` 值类型转换为 `IConvertible` 也会导致值类型装箱，浪费内存并损害性能。这是我在本节开头提到的大问题中的第二个。

EIMI 的第三个也是最大的问题是它们无法被派生类调用。示例所示：

```csharp

internal class Base : IComparable

{

    // 显式接口方法实现

    IComparable.CompareTo(Object o) {

      Console.WriteLine("Base CompareTo");

      return 0;

    }

}

internal sealed class Derived : Base, IComparable

{

    // 一个同时也是接口实现的公共方法

    public Int32 CompareTo(Object o) {

      Console.WriteLine("Derived CompareTo");

      return 0;

    }

}

// 尝试调用接口方法会报错：

// 错误 CS0109 'Derived' 不包含 'CompareTo' 的定义

Derived d = new Derived();

d.CompareTo(null); 
```
