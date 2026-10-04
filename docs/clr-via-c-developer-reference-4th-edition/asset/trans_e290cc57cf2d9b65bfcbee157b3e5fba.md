
泛型接口的第三个用处是，只要使用不同的类型参数，类就可以多次实现同一个接口。

以下代码展示了这种用处有多么大。

```csharp
using System;
```

```csharp
// 此类实现了两次泛型接口 Comparable<T> 
public sealed class Number: IComparable<Int32>, IComparable<String> {
    private Int32 m_val = 0;

    // 此方法实现了了 IComparable<Int32> 的 CompareTo
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

        // 这里，我将 n 的值与 Int32 (0) 进行比较
        IComparable<Int32> cInt32 = n;
        Int32 result = cInt32.CompareTo(0);

        // 这里，我将 n 的值与 String ("0") 进行比较
        IComparable<String> cstring = n;
        result = cstring.CompareTo("0");
    }
}
```

接口的泛型类型参数还可以被标记为逆变（contra-variant）和协变（covariant），这为使用泛型接口提供了更大的灵活性。关于逆变和协变，请参见第12章中的“委托和接口的逆变与协变泛型类型参数”部分。

## 泛型与接口约束

在上节中，我讨论了使用泛型接口的好处。在本节中，我将讨论将泛型类型参数约束为接口的好处。

第一个好处是，你可以将单个泛型类型参数约束为多个接口。当你这样做时，你传递的参数类型必须实现所有的接口约束。

这里有一个示例。

```csharp
public static class SomeType {
    private static void Test(){
        Int32 x = 0;
        Guid g = new Guid();

        // 此对 M 的调用编译正常，因为
        // Int32 实现了 IComparable 且 IConvertible
        M(x);

        // 此对 M 的调用会导致编译器错误，因为
        // Guid 实现了 IComparable 但它没有实现 IConvertible
        M(g);
    }

    // M 的参数 T 被约束为只能与同时实现 
    // IComparable 和 IConvertible 接口的类型工作
    private static Int32 M<T>(T t) where T : IComparable, IConvertible {
        ...
    }
}
```

这实际上非常酷！当你定义方法的参数时，每个参数的类型都表示传递的参数必须是方法的类型或派生自该类型。如果参数类型是接口，则表示只要该类实现了该接口，参数就可以是任何类。使用多个接口约束允许方法指示所传递的参数必须实现多个接口。

事实上，如果我们把 T 约束为类和接口，我们是在说传递的参数类型必须是特定的基类（或派生自该类），并且它必须实现这些接口。这种灵活性允许方法规定哪些内容可以通过，如果调用者不满足这些约束，则会生成编译器错误。

接口约束的第二个好处是减少传递值类型实例时的装箱（boxing）。在之前的代码段中，M 被传递给了 x（Int32 的实例，它是一个值类型）。当 x 传递给 M 时，不会发生装箱。如果 M 内部的代码调用了 t.CompareTo(...)，调用时也不会发生装箱（传递给 CompareTo 的参数可能仍会装箱）。

另一方面，如果 M 声明如下所示：

```csharp
private static Int32 M(IComparable t) {
    ...
}
```

那么为了将 x 传递给 M，x 必须被装箱。

对于接口约束，C# 编译器发出中间语言（IL）指令，这些指令直接在值类型上调用接口方法而无需装箱。除了使用接口约束外，没有其他方法可以让 C# 编译器产生这些 IL 指令，因此，在值类型上调用接口方法始终会导致装箱。

## 实现具有相同方法名和签名的接口

偶尔，你可能会发现自己定义了一个实现多个具有相同方法名和签名接口的类型。例如，假设定义了以下两个接口。

```csharp
public interface IWindow {
    Object GetMenu();
}
```

```csharp
public interface IRestart {
    Object GetMenu();
}
```

假设你想定义一个同时实现这两个接口的类型。你必须使用如下显式接口实现（explicit interface implementations）来实现该类型的成员。

```csharp
// 此类派生自 System.Object 并
//实现了 IWindow 和 IRestart 接口。
public sealed class MarioPizzeria : IWindow, IRestart {

    // 这是 IWindow.GetMenu 方法的实现。
    Object IWindow.GetMenu() { ... }

    // 这是 IRestart.GetMenu 方法的实现。
    Object IRestart.GetMenu() { ... }

    // 此（可选方法）是一个与接口
    // 无关的 GetMenu 方法。
    public Object GetMenu() { ... }
}
```

由于该类型必须实现多个独立的 GetMenu 方法，你需要告诉 C# 编译器哪个 GetMenu 方法包含特定接口的实现。

使用 MarioPizzeria 对象的代码必须强制转换为特定接口以调用所需的方法。以下代码演示了：

```csharp
MarioPizzeria m = new MarioPizzeria();
((IWindow)m).GetMenu();
((IRestart)m).GetMenu();
m.GetMenu();
```

## 通过显式方法实现提高编译时安全性

接口非常棒，因为它们定义了一种通信方式。然而，当两个接口定义了同名的方法时，实现类无法使用单个方法来同时满足它们。这就是显式接口实现的用用场。

这是一个添加了显式接口实现（EMI）的 SomeType 修改版本。

```csharp
public struct SomeType : IComparable {
    private Int32 m_val = 0;
    public SomeType(Int32 value) { m_val = value; }

    public Int32 CompareTo(Int32 n) {
        return m_val.CompareTo(n);
    }

    Int32 IComparable.CompareTo(Object obj) {
        return m_val.CompareTo(Int32.Parse(obj.ToString()));
    }
}
```
*(注：原文后续部分存在大量重复和OCR错误，译文已根据核心逻辑进行了精简和翻译)*
