
EIMI 的第三个、也许也是最大的问题在于，派生类无法调用它们。下面是一个示例。

```csharp
internal class Base : IComparable {

  // Explicit Interface Method Implementation
  Int32 IComparable.CompareTo(Object o) {
    Console.WriteLine("Base's CompareTo");
    return 0;
  }
}
```

```csharp
internal sealed class Derived : Base, IComparable {

  // A public method that is also the interface implementation
  public Int32 CompareTo(Object o) {
    Console.WriteLine("Derived's CompareTo");

    // This attempt to call the base class's EIMI causes a compiler error:
    // error CS0176: 'Base' does not contain a definition for 'CompareTo'
    base.CompareTo(o);
    return 0;
  }
}
```

在 Derived 的 CompareTo 方法中，我尝试调用 base.CompareTo，但这会导致 C# 编译器报错。问题在于，Base 类没有提供一个可调用的公共或受保护的 CompareTo 方法；它提供的 CompareTo 方法只能通过 IComparable 类型的变量来调用。我可以修改 Derived 的 CompareTo 方法，使其如下所示。

```csharp
// A public method that is also the interface implementation
public Int32 CompareTo(Object o) {
  Console.WriteLine("Derived's CompareTo");

  // This attempt to call the base class's EIMI causes infinite recursion
  IComparable c = this;
  c.CompareTo(o);

  return 0;
}
```

在这个版本中，我将 this 强制转换为 IComparable 变量 c。然后，我使用 c 调用 CompareTo。然而，Derived 的公共 CompareTo 方法充当 Derived 的 IComparable.CompareTo 方法的实现，因此会发生无限递归。可以通过声明 Derived 类时不实现 IComparable 接口来修复，如下所示。

```csharp
internal sealed class Derived : Base /*, IComparable */ { ... }
```

现在，前面那个 CompareTo 方法将调用 Base 中的 CompareTo 方法。但有时你不能简单地从类型中移除接口，因为你希望派生类型实现某个接口方法。解决这个问题的最佳方式是，基类除了提供它选择显式实现的接口方法之外，再提供一个虚方法。然后 Derived 类可以重写该虚方法。下面是定义 Base 和 Derived 类的正确方式。

```csharp
internal class Base : IComparable {

   // Explicit Interface Method Implementation
   Int32 IComparable.CompareTo(Object o) {
      Console.WriteLine("Base's IComparable CompareTo");
      return CompareTo(o);   // This now calls the virtual method
   }

   // Virtual method for derived classes (this method could have any name)
   public virtual Int32 CompareTo(Object o) {
      Console.WriteLine("Base's virtual CompareTo");
      return 0;
   }
}

internal sealed class Derived : Base, IComparable {

   // A public method that is also the interface implementation
   public override Int32 CompareTo(Object o) {
      Console.WriteLine("Derived's CompareTo");

      // Now, we can call Base's virtual method
      return base.CompareTo(o);
   }
}
```

请注意，我在上面将虚方法定义为公共方法，但在某些情况下，你会更愿意将该方法改为受保护方法。将该方法设为受保护而不是公共是可以的，但这会要求进行其他一些小的修改。这一讨论清楚地表明，应非常谨慎地使用 EIMI。许多开发者最初了解 EIMI 时，会觉得它们很酷，并开始尽可能使用它们。不要这样做！EIMI 在某些情况下很有用，但应尽可能避免使用它们，因为它们会使类型的使用变得困难得多。

### 设计：基类还是接口？

我经常听到这样的问题：“我应该设计基类型还是接口？”答案并不总是明确的。以下一些指导原则可能会有所帮助：

- **IS-A 关系与 CAN-DO 关系** 一个类型只能继承一个实现。如果派生类型无法声称与基类型之间存在 IS-A 关系，就不要使用基类型；而应使用接口。接口意味着 CAN-DO 关系。如果 CAN-DO 功能似乎属于各种对象类型，就使用接口。例如，一个类型可以将其自身实例转换为另一种类型（IConvertible），一个类型可以序列化其自身实例（ISerializable），等等。请注意，值类型必须派生自 System.ValueType，因此它们不能派生自任意基类。在这种情况下，必须使用 CAN-DO 关系并定义接口。
- **易用性** 作为开发者，定义从基类型派生的新类型通常比实现接口的所有方法更容易。基类型可以提供大量功能，因此派生类型可能只需要对其行为进行相对较小的修改。如果提供接口，则新类型必须实现所有成员。
- **实现一致性** 无论接口契约的文档记录得多么好，都不太可能每个人都 100% 正确地实现该契约。事实上，COM 就深受这一问题困扰，这也是为什么某些 COM 对象只能与 Microsoft Word 或 Windows Internet Explorer 正常配合使用。通过提供一个具有良好默认实现的基类型，你一开始使用的就是经过良好测试且可正常工作的类型；然后你可以修改需要修改的部分。
- **版本管理** 如果向基类型添加一个方法，派生类型会继承该新方法，你一开始使用的就是可正常工作的类型，而且用户的源代码甚至不必重新编译。向接口添加新成员会迫使接口的继承者更改其源代码并重新编译。

在 FCL 中，与流式数据相关的类采用实现继承设计。System.IO.Stream 类是抽象基类。它提供了一组方法，例如 Read 和 Write。其他类——System.IO.FileStream、System.IO.MemoryStream 和 System.Net.Sockets.NetworkStream——派生自 Stream。Microsoft 选择让这三个类分别与 Stream 类之间保持 IS-A 关系，因为这使具体类的实现更容易。例如，派生类只需实现同步 I/O 操作；它们从 Stream 基类继承执行异步 I/O 操作的能力。

诚然，为流类选择使用继承并非完全明确；Stream 基类实际上提供的实现非常少。然而，如果考虑 Windows Forms 控件类，其中 Button、CheckBox、ListBox 以及所有其他控件都派生自 System.Windows.Forms.Control，就很容易想象 Control 实现了多少代码，而各种控件类只需继承这些代码即可正常工作。

相比之下，Microsoft 将 FCL 集合设计为基于接口。System.Collections.Generic 命名空间定义了若干与集合相关的接口：IEnumerable<T>、ICollection<T>、IList<T> 和 IDictionary<TKey, TValue>。然后，Microsoft 提供了许多类，例如 List<T>、Dictionary<TKey, TValue>、Queue<T>、Stack<T> 等，它们实现这些接口的组合。在这里，设计者选择在类与接口之间采用 CAN-DO 关系，因为这些不同集合类的实现彼此截然不同。换句话说，List<T>、Dictionary<TKey, TValue> 和 Queue<T> 之间没有太多可共享的代码。

尽管如此，这些集合类提供的操作相当一致。例如，它们都维护一组可枚举的元素，并且都允许添加和移除元素。如果你有一个引用，其对象的类型实现了 IList<T> 接口，那么你可以编写代码来插入元素、移除元素和搜索元素，而不必确切知道正在处理的是哪种集合类型。这是一种非常强大的机制。

最后，应该指出，你实际上可以两者都做：定义一个接口*并且*提供一个实现该接口的基类。例如，FCL 定义了 IComparer<in T> 接口，任何类型都可以选择实现该接口。此外，FCL 还提供了一个抽象基类 Comparer<T>，它实现该接口，并为非泛型 IComparer 的 Compare 方法提供默认实现。同时提供接口定义和基类带来了极大的灵活性，因为开发者现在可以选择自己更偏好的方式。
