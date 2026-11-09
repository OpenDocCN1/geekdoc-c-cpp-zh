
如此看来，在使用泛型时，你可以声明泛型类型的变量、执行一些变量赋值、调用由 **Object** 定义的方法，差不多就这些了！这使得泛型实际上毫无用处。幸运的是，编译器和 CLR 支持一种称为*约束*的机制，你可以利用它让泛型重新变得有用。

约束是一种限制可为泛型实参指定的类型数量的方式。限制类型数量使你能够对这些类型做更多事情。下面是 **Min** 方法的一个新版本，它指定了一个约束（以粗体显示）：

```csharp
public static T Min<T>(T o1, T o2) where T : IComparable<T> {
    if (o1.CompareTo(o2) < 0) return o1;
    return o2;
}
```

C# 的 **where** 标记告诉编译器，为 T 指定的任何类型都必须实现同一类型 (T) 的泛型 **IComparable** 接口。由于这个约束，编译器现在允许该方法调用 **CompareTo** 方法，因为该方法由 **IComparable<T>** 接口定义。

现在，当代码引用泛型类型或方法时，编译器负责确保指定了满足约束的类型实参。例如，以下代码会导致编译器发出如下消息：'error CS0311: The type 'object' cannot be used as type parameter 'T' in the generic type or method 'SomeType.Min<T>(T, T)'. There is no implicit reference conversion from 'object' to 'System.IComparable<object>'.'

```csharp
private static void CallMin() {
    Object o1 = "Jeff", o2 = "Richter";
    Object oMin = Min<Object>(o1, o2);   // Error CS0311
}
```

编译器发出该错误是因为 **System.Object** 未实现 **IComparable<Object>** 接口。事实上，**System.Object** 根本没有实现任何接口。

既然你已经对约束是什么以及它们如何工作有了大致了解，我们将开始更深入地研究它们。约束可以应用于泛型类型的类型参数，也可以应用于泛型方法的类型参数（如 **Min** 方法所示）。CLR 不允许基于类型参数名称或约束进行重载；只能基于元数（arity）重载类型或方法。以下示例说明了我的意思：

```csharp
// It is OK to define the following types:
internal sealed class AType {}
internal sealed class AType<T> {}
internal sealed class AType<T1, T2> {}

// Error: conflicts with AType<T> that has no constraints
internal sealed class AType<T> where T : IComparable<T> {}
```

## 主要约束

类型参数可以指定零个主约束或一个主约束。主约束可以是标识非密封类的引用类型。不能指定以下特殊引用类型之一：**System.Object**、**System.Array**、**System.Delegate**、**System.MulticastDelegate**、**System.ValueType**、**System.Enum** 或 **System.Void**。

当指定引用类型约束时，你是在向编译器承诺：指定的类型实参将是同一类型，或派生自该约束类型的类型。例如，请看以下泛型类：

```
    internal sealed class PrimaryConstraintOfStream<T> where T : Stream {
        public void M(T stream) {
            stream.Close(); // OK
        }
    }
```

在此类定义中，类型参数 T 具有 **Stream** 的主约束（定义于 **System.IO** 命名空间）。这告诉编译器，使用 **PrimaryConstraintOfStream** 的代码必须指定 **Stream** 或派生自 **Stream** 的类型实参（例如 **FileStream**）。如果类型参数未指定主约束，则假定为 **System.Object**。然而，如果在源代码中显式指定 **System.Object**，C# 编译器会发出错误消息 **"error CS0702: Constraint cannot be special class 'object'"**。

有两个特殊的主约束：**class** 和 **struct**。**class** 约束向编译器承诺：指定的类型实参将是引用类型。任何类类型、接口类型、委托类型或数组类型都满足此约束。例如，请看以下泛型类：

```
    internal sealed class PrimaryConstraintOfClass<T> where T : class {
        public void M() {
            T temp = null; // Allowed because T must be a reference type
        }
    }
```

在此示例中，将 **temp** 设置为 **null** 是合法的，因为已知 T 是引用类型，并且所有引用类型变量都可以设置为 **null**。如果 T 未受约束，上面的代码将无法编译，因为 T 可能是值类型，而值类型变量不能设置为 **null**。

**struct** 约束向编译器承诺：指定的类型实参将是值类型。任何值类型（包括枚举）都满足此约束。然而，编译器和 CLR 将任何 **System.Nullable<T>** 值类型视为特殊类型，并且可空类型不满足此约束。原因在于 **Nullable<T>** 类型将其类型参数约束为 **struct**，而 CLR 希望禁止像 Nullable<Nullable<T>> 这样的递归类型。可空类型将在第 19 章“可空值类型”中讨论。

下面是一个使用 **struct** 约束来约束其类型参数的示例类：

```csharp
internal sealed class PrimaryConstraintOfStruct<T> where T : struct {
    public static T Factory() {
        // Allowed because all value types implicitly
        // have a public, parameterless constructor
        return new T();
    }
}
```

在此示例中，实例化一个 `T` 是合法的，因为已知 `T` 是值类型，并且所有值类型都隐式具有公共无参构造函数。如果 `T` 未受约束、受约束为引用类型，或受约束为 **class**，则上面的代码将无法编译，因为某些引用类型没有公共无参构造函数。

### 次要约束

类型参数可以指定零个或多个次要约束，其中次要约束表示接口类型。当指定接口类型约束时，你是在向编译器承诺：指定的类型实参将是实现该接口的类型。而且，由于可以指定多个接口约束，类型实参必须指定一个实现所有接口约束（以及所有主约束，如果指定了的话）的类型。第 13 章将详细讨论接口约束。

还有另一种次要约束，称为*类型参数约束*（有时称为*裸类型约束*）。这种约束的使用频率远低于接口约束。它允许泛型类型或方法表明指定类型实参之间必须存在关系。类型参数可以应用零个或多个类型约束。下面是一个演示类型参数约束用法的泛型方法：

```csharp
private static List<TBase> ConvertIList<T, TBase>(IList<T> list)
    where T : TBase {
    List<TBase> baseList = new List<TBase>(list.Count);
    for (Int32 index = 0; index < list.Count; index++) {
        baseList.Add(list[index]);
    }
    return baseList;
}
```

**ConvertIList** 方法指定了两个类型参数，其中 `T` 参数受 `TBase` 类型参数约束。这意味着无论为 `T` 指定什么类型实参，该类型实参都必须与为 `TBase` 指定的任何类型实参兼容。下面是一个展示对 **ConvertIList** 的一些合法和非法调用的方法：

```csharp
internal sealed class ConstructorConstraint<T> where T : new() {
    public static T Factory() {
        // Allowed because all value types implicitly
        // have a public, parameterless constructor and because
        // the constraint requires that any specified reference
        // type also have a public, parameterless constructor
        return new T();
    }
}
```

在此示例中，**实例化一个 T** 是合法的，因为已知 T 是具有公共无参构造函数的类型。所有值类型确实如此，并且构造函数约束要求作为类型实参指定的任何引用类型也必须如此。

有时，开发者希望使用构造函数约束来声明类型参数，而该构造函数本身接受各种参数。到目前为止，CLR（因此也包括 C# 编译器）仅支持无参构造函数。Microsoft 认为这对于几乎所有场景来说都足够好，我也同意。

### 其他可验证性问题

在本节的剩余部分，我想指出另外几种代码构造，由于可验证性问题，它们在与泛型一起使用时会出现意外行为，以及如何使用约束使代码再次可验证。

### 转换泛型类型变量

除非转换为与约束兼容的类型，否则将泛型类型变量转换为另一种类型是非法的。

```csharp
private static void CastingAGenericTypeVariable1<T>(T obj) {
    Int32 x = (Int32) obj;  // Error
    String s = (String) obj; // Error
}
```

编译器对上面两行都发出错误，因为 T 可能是任何类型，并且无法保证转换会成功。你可以通过先转换为 **Object** 来修改此代码，使其编译通过：

```csharp
private static void CastingAGenericTypeVariable2<T>(T obj) {
    Int32 x = (Int32) (Object) obj;  // No error
    String s = (String) (Object) obj; // No error
}
```

虽然这段代码现在可以编译，但 CLR 仍可能在运行时抛出 **InvalidCastException**。
