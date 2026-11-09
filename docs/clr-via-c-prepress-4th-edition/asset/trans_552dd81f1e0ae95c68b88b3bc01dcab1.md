
因为每种类型都支持赋值和对 Object 定义的方法（如 ToString 和 Equals）的调用。

现在来看下面的方法：

```csharp
private static T Min<T>(T o1, T o2) {
    if (o1.CompareTo(o2) < 0) return o1;
    return o2;
}
```

Min 方法试图使用 `o1` 变量调用 CompareTo 方法。但是有很多类型没有提供 CompareTo 方法，因此 C# 编译器无法编译这段代码并保证该方法适用于所有类型。如果你尝试编译上述代码，编译器会发出以下消息：'error CS1061: 'T' does not contain a definition for 'CompareTo' and no extension method 'CompareTo' accepting a first argument of type 'T' could be found (are you missing a using directive or an assembly reference?)'

因此，使用泛型时，你似乎可以声明泛型类型的变量，进行一些变量赋值，调用 Object 定义的方法，仅此而已！这使得泛型几乎毫无用处。幸运的是，编译器和 CLR 支持一种名为约束（constraints）的机制，你可以利用它让泛型重新变得有用。

约束是一种限制可指定为泛型实参的类型数量的方式。限制类型数量允许你对这些类型做更多操作。下面是 Min 方法的一个新版本，它指定了一个约束（以粗体显示）：

```csharp
public static T Min<T>(T o1, T o2) where T : IComparable<T> {
    if (o1.CompareTo(o2) < 0) return o1;
    return o2;
}
```

C# 的 `where` 标记告诉编译器，为 T 指定的任何类型都必须实现相同类型 (T) 的泛型 IComparable 接口。由于这个约束，编译器现在允许该方法调用 CompareTo 方法，因为该方法是由 `IComparable<T>` 接口定义的。

现在，当代码引用泛型类型或方法时，编译器负责确保指定满足约束的类型实参。例如，以下代码会导致编译器发出以下消息：'error CS0311: The type 'object' cannot be used as type parameter 'T' in the generic type or method 'SomeType.Min<T>(T, T)'. There is no implicit reference conversion from 'object' to 'System.IComparable<object>'.'

编译器发出该错误是因为 System.Object 没有实现 `IComparable<Object>` 接口。事实上，System.Object 根本不实现任何接口。

现在你已经对约束是什么以及它们如何工作有了概念，我们将开始更深入地研究它们。约束可以应用于泛型类型的类型参数，也可以应用于泛型方法的类型参数（如 Min 方法所示）。CLR 不允许基于类型参数名称或约束进行重载；你只能基于元数（arity）重载类型或方法。下面的例子说明我的意思：

```csharp
// It is OK to define the following types:
internal sealed class AType {}
internal sealed class AType<T> {}
internal sealed class AType<T1, T2> {}

// Error: conflicts with AType<T> that has no constraints
internal sealed class AType<T> where T : IComparable<T> {}

// Error: conflicts with AType<T1, T2>
internal sealed class AType<T3, T4> {}

internal sealed class AnotherType {
    // It is OK to define the following methods:
    private static void M() {}
    private static void M<T>() {}
    private static void M<T1, T2>() {}

    // Error: conflicts with M<T> that has no constraints
    private static void M<T>() where T : IComparable<T> {}

    // Error: conflicts with M<T1, T2>
    private static void M<T3, T4>() {}
}
```

重写虚泛型方法时，重写方法必须指定相同数量的类型参数，并且这些类型参数将继承基类方法在它们上面指定的约束。事实上，重写方法完全不允许在其类型参数上指定任何约束。然而，它可以更改类型参数的名称。类似地，实现接口方法时，该方法必须指定与接口方法相同数量的类型参数，并且这些类型参数将继承接口方法在它们上面指定的约束。下面是一个通过虚方法演示此规则的示例：

```csharp
internal class Base {
    public virtual void M<T1, T2>()
        where T1 : struct
        where T2 : class {
    }
}

internal sealed class Derived : Base {
    public override void M<T3, T4>()
        where T3 : EventArgs // Error
        where T4 : class    // Error
    {
    }
}
```

尝试编译上述代码会导致编译器发出以下消息："error CS0460: Constraints for override and explicit interface implementation methods are inherited from the base method, so they cannot be specified directly." 如果我们从 Derived 类的 `M<T3, T4>` 方法中移除两个 `where` 行，代码将正常编译。注意，你可以更改类型参数的名称（如示例中：从 T1 到 T3，从 T2 到 T4）；但是，你不能更改（甚至不能指定）约束。

现在让我们讨论编译器/CLR 允许应用于类型参数的不同种类的约束。类型参数可以使用主约束、次要约束和/或构造函数约束进行约束。我将在接下来的三节中讨论这三种约束。

### 主约束

类型参数可以指定零个主约束或一个主约束。主约束可以是标识非密封类的引用类型。你不能指定以下特殊引用类型之一：System.Object、System.Array、System.Delegate、System.MulticastDelegate、System.ValueType、System.Enum 或 System.Void。

指定引用类型约束时，你向编译器保证指定的类型实参要么是与约束类型相同的类型，要么是从约束类型派生的类型。例如，请看下面的泛型类：

```csharp
internal sealed class PrimaryConstraintOfStream<T> where T : Stream {
    public void M(T stream) {
        stream.Close(); // OK
    }
}
```

在这个类定义中，类型参数 T 有一个主约束 Stream（在 System.IO 命名空间中定义）。这告诉编译器，使用 `PrimaryConstraintOfStream` 的代码必须指定一个 Stream 类型或派生自 Stream 的类型（如 FileStream）作为类型实参。如果类型参数没有指定主约束，则假定为 System.Object。但是，如果你在源代码中显式指定 System.Object，C# 编译器会发出错误消息（"error CS0702: Constraint cannot be special class 'object'"）。

有两种特殊的主约束：`class` 和 `struct`。`class` 约束向编译器保证指定的类型实参将是引用类型。任何类类型、接口类型、委托类型或数组类型都满足此约束。例如，请看下面的泛型类：

```csharp
internal sealed class PrimaryConstraintOfClass<T> where T : class {
    public void M() {
        T temp = null; // Allowed because T must be a reference type
    }
}
```

在这个例子中，将 `temp` 设置为 `null` 是合法的，因为已知 `T` 是引用类型，而所有引用类型变量都可以设置为 `null`。如果 `T` 不受约束，上面的代码将无法编译，因为 `T` 可能是值类型，而值类型变量不能设置为 `null`。

`struct` 约束向编译器保证指定的类型实参将是值类型。任何值类型（包括枚举）都满足此约束。然而，编译器和 CLR 将任何 `System.Nullable<T>` 值类型视为特殊类型，而可空类型不满足此约束。原因是 `Nullable<T>` 类型将其类型参数约束为 `struct`，并且 CLR 希望禁止类似 `Nullable<Nullable<T>>` 的递归类型。可空类型将在第 19 章“可空值类型”中讨论。

下面是一个使用 `struct` 约束其类型参数的示例类：

```csharp
internal sealed class PrimaryConstraintOfStruct<T> where T : struct {
    public static T Factory() {
        // Allowed because all value types implicitly
        // have a public, parameterless constructor
        return new T();
    }
}
```

在这个例子中，`new` 出一个 `T` 是合法的，因为已知 `T` 是值类型，而所有值类型都隐式具有公共无参构造函数。如果 `T` 不受约束、约束为引用类型或约束为 `class`，上述代码将无法编译，因为某些引用类型没有公共无参构造函数。

### 次要约束

类型参数可以指定零个或多个次要约束，其中次要约束表示接口类型。指定接口类型约束时，你向编译器保证指定的类型实参将是实现该接口的类型。由于你可以指定多个接口约束，类型实参必须指定一个实现所有接口约束（以及所有主约束，如果指定了的话）的类型。第 13 章将详细讨论接口约束。

还有一种次要约束，称为 *类型参数约束*（有时称为 *裸类型参数约束*）。这种约束的使用频率远低于接口约束。它允许泛型类型或方法表明指定的类型实参之间必须存在某种关系。类型参数可以应用零个或多个类型约束。下面是一个演示类型参数约束用法的泛型方法：

```csharp
private static List<TBase> ConvertList<T, TBase>(IList<T> list)
    where T : TBase {
    List<TBase> baseList = new List<TBase>(list.Count);
    for (Int32 index = 0; index < list.Count; index++) {
        baseList.Add(list[index]);
    }
    return baseList;
}
```

