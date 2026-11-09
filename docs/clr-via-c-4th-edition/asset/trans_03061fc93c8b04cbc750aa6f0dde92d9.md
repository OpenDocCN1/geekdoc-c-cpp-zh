
```csharp
// Compiler infers that dt1 is of type
// System.Collections.Generic.List<System.DateTime>
var dt1 = new List<DateTime>();
...
}
}
```

### 代码膨胀

当使用泛型类型参数的方法被 JIT 编译时，CLR 会获取该方法的 IL，替换指定的类型实参，然后生成本机代码，这些代码特定于该方法操作指定的数据类型。这正是你想要的，也是泛型的主要特性之一。然而，这有一个缺点：CLR 会为每个方法/类型组合不断生成本机代码。这被称为*代码膨胀*。这最终可能大幅增加应用程序的工作集，从而损害性能。

幸运的是，CLR 内置了一些优化来减少代码膨胀。首先，如果针对某个特定类型实参调用了一个方法，之后又使用相同的类型实参再次调用该方法，CLR 只会为这个方法/类型组合编译一次代码。因此，如果一个程序集使用 List<DateTime>，而另一个完全不同的程序集（加载在同一 AppDomain 中）也使用 List<DateTime>，CLR 只会为 List<DateTime> 的方法编译一次。这大幅减少了代码膨胀。

CLR 还有另一个优化：CLR 将所有引用类型实参视为相同，因此代码同样可以共享。例如，CLR 为 List<String> 的方法编译的代码可以用于 List<Stream> 的方法，因为 String 和 Stream 都是引用类型。事实上，对于任何引用类型，都会使用相同的代码。CLR 能执行此优化，是因为所有引用类型实参或变量实际上只是指向堆上对象的指针（在 32 位 Windows 系统上均为 32 位，在 64 位 Windows 系统上为 64 位），并且所有对象指针都以相同方式操作。

但如果任何类型实参是值类型，CLR 必须专门为该值类型生成本机代码。原因是值类型的大小可能不同。而且即使两个值类型大小相同（例如 Int32 和 UInt32，二者都是 32 位），CLR 仍然无法共享代码，因为可能使用不同的本机 CPU 指令来操作这些值。

### 泛型接口

显然，能够定义泛型引用类型和值类型是泛型的主要特性。然而，CLR 还必须支持泛型接口，这一点至关重要。如果没有泛型接口，任何时候你试图通过非泛型接口（例如 IComparable）操作值类型，装箱和编译时类型安全的丧失都会再次发生。这会严重限制泛型类型的实用性。因此，CLR 确实支持泛型接口。引用类型或值类型

例如，如果定义如下泛型委托：

```csharp
public delegate TReturn CallMe<TReturn, TKey, TValue>(TKey key, TValue value);
```

编译器会将其转换为一个逻辑上如下所示的类。

```csharp
public sealed class CallMe<TReturn, TKey, TValue> : MulticastDelegate {
    public CallMe(Object object, IntPtr method);
    public virtual TReturn Invoke(TKey key, TValue value);
    public virtual IAsyncResult BeginInvoke(TKey key, TValue value,
        AsyncCallback callback, Object object);
    public virtual TReturn EndInvoke(IAsyncResult result);
}
```

> **注意** 建议尽可能使用 Framework Class Library (FCL) 中预定义的泛型 Action 和 Func 委托。我在第 17 章“委托定义已经够多了（泛型委托）”一节中描述了这些委托类型。

### 委托和接口的逆变与协变泛型类型实参

委托的每个泛型类型参数都可以标记为协变或逆变。此特性允许你将一个泛型委托类型的变量强制转换为*同一个*委托类型，只是泛型参数类型不同。泛型类型参数可以是以下任意一种：

- **不变** 表示泛型类型参数不能更改。到目前为止，本章中我只展示了不变的泛型类型参数。
- **逆变** 表示泛型类型参数可以从一个类更改为派生自它的类。在 C# 中，使用 in 关键字表示逆变泛型类型参数。逆变泛型类型参数只能出现在输入位置，例如方法的参数。
- **协变** 表示泛型类型实参可以从一个类更改为它的某个基类。在 C# 中，使用 out 关键字表示协变泛型类型参数。协变泛型类型参数只能出现在输出位置，例如方法的返回类型。

例如，假设存在以下委托类型定义（顺便说一句，它确实存在）。

```csharp
public delegate TResult Func<in T, out TResult>(T arg);
```

这里，泛型类型参数 T 用 in 关键字标记，使其成为逆变；泛型类型参数 TResult 用 out 关键字标记，使其成为协变。

那么现在，如果我有一个如下声明的变量。

```csharp
Func<Object, ArgumentException> fn1 = null;
```

我可以将它强制转换为另一个 Func 类型，其中泛型类型参数不同。

```csharp
Func<String, Exception> fn2 = fn1; // No explicit cast is required here
Exception e = fn2("");
```

这表示 fn1 引用一个接受 Object 并返回 ArgumentException 的函数。fn2 变量希望引用一个接受 String 并返回 Exception 的方法。因为可以将 String 传递给需要 Object 的方法（因为 String 派生自 Object），并且因为可以取得返回 ArgumentException 的方法的结果并将其视为 Exception（因为 Exception 是 ArgumentException 的基类），所以上面的代码可以编译，并且在编译时已知它保持类型安全。

> **注意** 变体仅当编译器能验证类型之间存在引用转换时才适用。换句话说，值类型不可能使用变体，因为需要装箱。在我看来，正是这一限制使得这些变体特性不那么有用。例如，如果我有以下方法。
> 
> ```csharp
> void ProcessCollection(IEnumerable<Object> collection) { ... }
> ```
> 
> 我不能在传入对 List<DateTime> 对象的引用的情况下调用它，因为 DateTime 值类型和 Object 之间不存在引用转换，即使 DateTime 派生自 Object。可以通过如下声明 ProcessCollection 来解决此问题。
> 
> ```csharp
> void ProcessCollection<T>(IEnumerable<T> collection) { ... }
> ```
> 
> 另外，ProcessCollection(IEnumerable<Object> collection) 的一大好处是只有一份 JIT 编译后的代码版本。然而，对于 ProcessCollection<T>(IEnumerable<T> collection)，也只有一份由所有作为引用类型的 T 共享的 JIT 编译后的代码版本。对于作为值类型的 T，你确实会得到其他版本的 JIT 编译后的代码，但现在至少可以在传入值类型集合的情况下调用该方法。
> 
> 此外，如果使用 out 或 ref 关键字将该类型的参数传递给方法，则不允许在泛型类型参数上使用变体。例如，下面的代码行会导致编译器生成以下错误消息：Invalid variance: The type parameter 'T' must be invariantly valid on 'SomeDelegate<T>'. 'T' is contravariant.
> 
> ```csharp
> delegate void SomeDelegate<in T>(ref T t);
> ```

当使用接受泛型实参并返回类型的委托时，建议尽可能始终为逆变和协变指定 in 和 out 关键字，因为这样做没有不良影响，并且能使委托用于更多场景。

