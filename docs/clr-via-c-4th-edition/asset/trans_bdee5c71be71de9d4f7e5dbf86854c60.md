
C# 提供了五个关键字，可应用于类型和/或类型成员，它们影响组件的版本控制。这些关键字直接映射到 CLR 支持的功能，用于支持组件的版本控制。表6-2 包含与组件版本控制相关的 C# 关键字，并说明每个关键字如何影响类型或类型成员的定义。

**表6-2** C# 关键字及其对组件版本控制的影响

| C# 关键字 | 类型 | 方法/属性/事件 | 常量/字段 |
|---|---|---|---|
| abstract | 指示不能构造该类型的任何实例 | 指示派生类型在构造其实例之前必须重写并实现此成员 | （不允许） |
| virtual | （不允许） | 指示该成员可由派生类型重写 | （不允许） |
| override | （不允许） | 指示派生类型正在重写基类型的成员 | （不允许） |
| sealed | 指示该类型不能用作基类型 | 指示该成员不能被派生类型重写。此关键字只能应用于重写虚方法的方法 | （不允许） |
| new | 当应用于嵌套类型、方法、属性、事件、常量或字段时，指示该成员与基类中可能存在的类似成员没有关系 |  |  |

在下一节“在版本控制类型时处理虚方法”中，我将演示所有这些关键字的价值和用法。但在讨论版本控制场景之前，让我们先关注 CLR 实际上是如何调用虚方法的。

## CLR 如何调用虚方法、属性和事件

在本节中，我将专注于方法，但这一讨论同样适用于虚属性和虚事件。属性和事件实际上是以方法的形式实现的；这将在它们对应的章节中展示。

方法表示在类型（静态方法）或类型的实例（非静态方法）上执行某些操作的代码。所有方法都有名称、签名和返回类型（可能是 void）。CLR 允许一个类型定义多个同名方法，只要每个方法具有不同的参数集或不同的返回类型。因此，只要方法具有不同的返回类型，就可以定义两个名称和参数都相同的方法。然而，除了 IL 汇编语言之外，我不知道还有哪种语言利用了这种“特性”；大多数语言（包括 C#）要求方法通过参数来区分，在确定唯一性时忽略方法的返回类型。（实际上，C# 在定义转换运算符方法时放宽了这一限制；详见第8章。）

现在，让我们把这些内容结合起来，看看 C# 如何使用这些不同的 IL 指令。

```csharp
using System;

public sealed class Program {
    public static void Main() {
        Console.WriteLine(); // Call a static method

        Object o = new Object();
        o.GetHashCode(); // Call a virtual instance method
        o.GetType();     // Call a nonvirtual instance method
    }
}
```

如果你编译上述代码并查看生成的 IL，你会看到以下内容。

```
.method public hidebysig static void Main() cil managed {
.entrypoint
// Code size 26 (0x1a)
.maxstack 1
.locals init (object o)
IL_0000: call void System.Console::WriteLine()
IL_0005: newobj instance void System.Object::.ctor()
IL_000a: stloc.0
IL_000b: ldloc.0
IL_000c: callvirt instance int32 System.Object::GetHashCode()
IL_0011: pop
IL_0012: ldloc.0
IL_0013: callvirt instance class System.Type System.Object::GetType()
IL_0018: pop
IL_0019: ret
} // end of method Program::Main
```

请注意，C# 编译器使用 `call` IL 指令来调用 Console 的 WriteLine 方法。这符合预期，因为 WriteLine 是一个静态方法。接下来，请注意 `callvirt` IL 指令用于调用 GetHashCode。这也符合预期，因为 GetHashCode 是一个虚方法。最后，请注意 C# 编译器也使用 `callvirt` IL 指令来调用 GetType 方法。这令人惊讶，因为 GetType 不是虚方法。然而，这是可行的，因为在 JIT 编译此代码时，CLR 会知道 GetType 不是虚方法，因此 JIT 编译后的代码将直接以非虚方式调用 GetType。

当然，问题是，C# 编译器为什么不直接发出 `call` 指令呢？答案是，C# 团队决定让 JIT 编译器生成代码来验证用于调用的对象不为 null。这意味着对非虚实例方法的调用会稍微慢一些。这也意味着下面的 C# 代码会抛出 NullReferenceException。在某些其他编程语言中，下面代码的意图可以正常运行。

```csharp
using System;

public sealed class Program {
    public Int32 GetFive() { return 5; }
    public static void Main() {
        Program p = null;
        Int32 x = p.GetFive(); // In C#, NullReferenceException is thrown
    }
}
```

理论上，前面的代码没有问题。当然，变量 p 是 null，但在调用非虚方法（GetFive）时，CLR 只需要知道 p 的数据类型，即 Program。如果 GetFive 真的被调用，这个参数的值将是 null。因为该参数在 GetFive 方法内部未被使用，所以不会抛出 NullReferenceException。然而，由于 C# 编译器发出的是 `callvirt` 指令而不是 `call` 指令，前面的代码最终会抛出 NullReferenceException。

> **重要提示** 如果你将方法定义为非虚方法，以后绝不应将其更改为虚方法。原因是某些编译器会使用 `call` 指令而不是 `callvirt` 指令来调用非虚方法。如果方法从非虚方法变为虚方法，而引用代码未重新编译，那么虚方法将被以非虚方式调用，导致应用程序产生不可预测的行为。如果引用代码是用 C# 编写的，这不是问题，因为 C# 使用 `callvirt` 调用所有实例方法。但如果引用代码是使用其他编程语言编写的，这可能就是一个问题。

有时，编译器会使用 `call` 指令而不是 `callvirt` 指令来调用虚方法。乍一看，这可能令人惊讶，但下面的代码演示了为什么有时需要这样做。

```csharp
internal class SomeClass {
    // ToString is a virtual method defined in the base class: Object.
    public override String ToString() {

        // Compiler uses the 'call' IL instruction to call
        // Object's ToString method nonvirtually.

        // If the compiler were to use 'callvirt' instead of 'call', this
        // method would call itself recursively until the stack overflowed.
        return base.ToString();
    }
}
```

当调用 base.ToString（一个虚方法）时，C# 编译器会发出 `call` 指令，以确保基类型中的 ToString 方法被非虚调用。这是必需的，因为如果 ToString 被虚调用，该调用将递归执行，直到线程的堆栈溢出，这显然不是我们想要的。

编译器在调用值类型定义的方法时倾向于使用 `call` 指令，因为值类型是密封的。这意味着即使对于它们的虚方法也不存在多态性，从而使调用性能更快。此外，值类型实例的本质保证它永远不会为 null，因此永远不会抛出 NullReferenceException。最后，如果要虚调用值类型的虚方法，CLR 需要拥有对值类型类型对象的引用，以便引用其内部的方法表。这需要对值类型进行装箱。装箱会给堆带来更多压力，导致更频繁的垃圾回收，并损害性能。

无论使用 `call` 还是 `callvirt` 来调用实例方法或虚方法，这些方法总是接收一个隐藏的 `this` 参数作为方法的第一个参数。该 `this` 参数引用正在操作的对象。

在设计类型时，你应尽量最小化定义的虚方法的数量。首先，调用虚方法比调用非虚方法慢。其次，虚方法无法被 JIT 编译器内联，这进一步损害了性能。第三，虚方法使组件的版本控制更加脆弱，如下一节所述。第四，在定义基类型时，通常会提供一组便捷的重载方法。如果你希望这些方法具有多态性，最好的做法是将最复杂的方法设为虚方法，而让所有便捷重载方法保持非虚。顺便说一句，遵循这一指导方针还能提高组件的版本控制能力，而不会对派生类型产生不利影响。下面是一个示例。

```csharp
public class Set {
   private Int32 m_length = 0;

   // This convenience overload is not virtual
   public Int32 Find(Object value) {
      return Find(value, 0, m_length);
   }

   // This convenience overload is not virtual
   public Int32 Find(Object value, Int32 startIndex) {
      return Find(value, startIndex, m_length - startIndex);
   }

   // The most feature-rich method is virtual and can be overridden
   public virtual Int32 Find(Object value, Int32 startIndex, Int32 endIndex) {
      // Actual implementation that can be overridden goes here...
   }

   // Other methods go here
}
```

## 明智地使用类型可见性和成员可访问性

使用 .NET Framework，应用程序由多个程序集中的类型组成，这些程序集由不同公司生产。这意味着开发者对所使用的组件以及这些组件中定义的类型几乎没有控制权。开发者通常无法访问源代码（甚至可能不知道用于创建组件的是哪种编程语言），而且组件往往按照不同的时间表进行版本控制。此外，由于多态性和受保护成员，基类开发者必须信任派生类开发者编写的代码。而且，当然，派生类的开发者必须信任他所编写的代码
