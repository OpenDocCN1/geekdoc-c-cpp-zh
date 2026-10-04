
C# 提供了可以应用于类型和/或类型成员的关键字，这些关键字会影响组件的版本。这些关键字直接映射到 CLR 支持的组件版本功能。表 6-2 包含了与版本相关的 C# 关键字，并指示了每个关键字如何影响类型或成员。

## 表 6-2 C# 关键字及其对版本控制的影响

| C# 关键字 | 类型 | 方法/属性/事件 | 常量/字段 |
| :--- | :--- | :--- | :--- |
| abstract | 表示无法构造该类型的实例 | 表示在构造派生类型实例之前，派生类型必须重写并实现此成员 | (不允许) |
| virtual | (不允许) | 表示此成员可以被派生类型重写 | (不允许) |
| override | (不允许) | 表示派生类型正在重写基类型的成员 | (不允许) |
| sealed | 表示该类型不能作为基类型使用 | 表示不能被派生类型重写。此关键字只能应用于虚方法 | (不允许) |
| new | 当应用于嵌套类型、方法、属性、常量或字段时，表示该成员与基类中可能存在的类似成员没有关系 | | |

## CLR 如何调用虚方法、属性和事件

在本节中，我将重点讨论方法，但此讨论也适用于虚属性。属性和事件实际上是作为方法实现的；这将在相应的章节中展示。方法代表在类型上（静态方法）或在类型实例上（实例方法）执行某些操作的代码。所有方法都有名称、签名和返回类型（可以是 `void`）。CLR 允许你定义多个具有相同名称的方法，只要每个方法具有不同的参数集或不同的返回类型。然而，对于 IL，我不清楚是否有任何语言利用了这种“特性”；大多数语言（包括 C#）都要求方法在参数上有所不同，并在确定唯一性时忽略方法的返回类型。（实际上，详情请参见第 8 章。）

下方所示的 `Employee` 类定义了不同类型的方法：

```csharp
internal class Employee {
    // 一个非虚实例方法
    public Int32 GetYearsEmployed() { ... }

    // 一个虚方法（隐含为实例）
    public virtual String GetProgress() { ... }

    // 一个静态方法
    public static Employee Lookup(String name) { ... }
}
```

当编译器编译此代码时，它会在生成的程序集的方法表中发射条目。每个条目都有标志，指示该方法是实例的、虚的还是静态的。当编写调用这些任何方法的代码时，编译器会检查方法定义的标志，以确定如何发射 IL 代码以确保正确调用。CLR 提供了两个 IL 指令来调用方法：

- `call` 指令可以用于静态、实例和虚方法。当使用 `call` 指令调用静态方法时，必须指定 CLR 调用的方法类型。当 `call` 指令用于实例或虚方法时，必须指定一个引用对象的变量。`call` 指令假设该变量不空。换句话说，变量的类型指示 CLR 应该调用用的类型。如果变量类型没有定义该方法，将检查基类型是否有匹配的方法。`call` 指令经常用于调用非虚方法。

- `callvirt` IL 指令可以用于实例和虚方法，而不用于静态方法。当使用 `callvirt` 指令调用实例或虚方法时，必须指定一个引用对象的变量。当使用 `callvirt` IL 调用非虚实例方法时，变量的类型指示 CLR 应该调用的方法。当使用 `callvirt` IL 调用虚实例方法时，CLR 会发现对象的类型并以多态方式调用方法。为了确定类型，用于调用的变量不能为空。换句话说，在编译此代码时，JIT 编译器生成代码验证变量值不为空。如果为空，`callvirt` 指令将导致 `NullReferenceException`。这意味着 `callvirt` 的执行速度比 `call` 慢。

现在，我们将这些整合在一起，看看 C# 如何使用这些 IL 指令：

```csharp
using System;

public sealed class Program {
    public static void Main() {
        Console.WriteLine(); // 调用静态方法

        Object o = new Object();
        o.GetHashCode(); // 调用虚实例方法
        o.GetType(); // 调用非虚实例方法
    }
}
```

如果你编译上述代码并查看生成的 IL，你会看到以下内容：

```il
.method hidebysig static void Main()
// entrypoint
// size 26 (0x1a)
// maxstack 1
// locals init (object o)
IL_0000: call System.Console::WriteLine()
IL_0005: newobj void System.Object::.ctor()
IL_000a: stloc.
IL_000b: ldloc.
IL_000c: callvirt
IL_0011: pop
IL_0012: ldloc.
IL_0013: call
IL_0018: pop
IL_0019: ret
```
