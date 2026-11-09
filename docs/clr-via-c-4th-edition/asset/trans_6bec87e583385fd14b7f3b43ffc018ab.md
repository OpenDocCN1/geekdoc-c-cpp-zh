

## 参数和返回类型指南

在声明方法的参数类型时，应尽可能使用最弱的类型，优先选择接口而非基类。例如，如果你正在编写一个操作集合项的方法，最好使用诸如 `IEnumerable<T>` 这样的接口来声明参数，而不是使用诸如 `List<T>` 这样的强数据类型，或甚至 `ICollection<T>` 或 `IList<T>` 这样的更强接口类型。

```csharp
// Desired: This method uses a weak parameter type
public void ManipulateItems<T>(IEnumerable<T> collection) { ... }

// Undesired: This method uses a strong parameter type
public void ManipulateItems<T>(List<T> collection) { ... }
```

原因当然在于，调用者可以传入数组对象、`List<T>` 对象、String 对象等任何其类型实现了 `IEnumerable<T>` 的对象来调用第一个方法。而第二个方法只允许传入 `List<T>` 对象，不接受数组或 String 对象。显然，第一个方法更好，因为它更加灵活，可以用于更广泛的场景。

自然，如果你编写的方法需要的是一个列表（不仅仅是任意可枚举对象），那么你应该将参数类型声明为 `IList<T>`。仍然应避免将参数类型声明为 `List<T>`。使用 `IList<T>` 允许调用者传入数组及任何其类型实现了 `IList<T>` 的其他对象。

请注意，我的示例讨论的是集合，这些集合是使用接口架构设计的。如果我们讨论的是使用基类架构设计的类，这个概念同样适用。因此，例如，如果我实现一个从流中处理字节的方法，我们会看到以下代码。

```csharp
// Desired: This method uses a weak parameter type
public void ProcessBytes(Stream someStream) { ... }

// Undesired: This method uses a strong parameter type
public void ProcessFiles(FileStream fileStream) { ... }
```

第一个方法可以处理来自任何类型的流的字节：`FileStream`、`NetworkStream`、`MemoryStream` 等等。第二个方法只能操作 `FileStream`，因此其功能受限得多。

另一方面，通常最好使用尽可能强的类型来声明方法的返回类型（尽量不要过早地限定为某个具体类型）。例如，最好声明一个返回 `FileStream` 对象的方法，而不是返回 `Stream` 对象。

```csharp
// Desired: This method uses a strong return type
public FileStream OpenFile() { ... }

// Undesired: This method uses a weak return type
public Stream OpenFile() { ... }
```

在这里，首选第一个方法，因为它允许调用者将返回的对象视为 `FileStream` 对象或 `Stream` 对象。而第二个方法要求调用者将返回的对象视为 `Stream` 对象。基本上，最好让调用者在调用方法时拥有尽可能多的灵活性，从而使方法能在最广泛的场景中使用。

有时，你希望保留更改方法内部实现的能力，而不影响调用者。在刚刚展示的示例中，`OpenFile` 方法不太可能更改其内部实现，改为返回除了 `FileStream` 对象（或类型派生自 `FileStream` 的对象）之外的其他内容。然而，如果你有一个返回 `List<String>` 对象的方法，你很可能希望将来更改此方法的内部实现，使其改为返回 `String[]`。在希望给自己留一些灵活性来更改方法返回内容的场景中，应选择较弱的返回类型。下面是一个示例。

```csharp
    // Flexible: This method uses a weaker return type
    public IList<String> GetStringCollection() { ... }

    // Inflexible: This method uses a stronger return type
    public List<String> GetStringCollection() { ... }
```

在这个示例中，尽管 `GetStringCollection` 方法内部使用 `List<String>` 对象并返回它，但最好将该方法的原型声明为返回 `IList<String>`。将来，`GetStringCollection` 方法可以将内部集合改为使用 `String[]`，而调用者无需更改任何源代码。事实上，他们甚至不需要重新编译代码。请注意，在这个示例中，我使用的是最弱类型中最强的类型。例如，我没有使用 `IEnumerable<String>` 甚至 `ICollection<String>`。

### 常量性（Const-ness）

在某些语言（如非托管 C++）中，可以将方法或参数声明为常量，从而禁止实例方法中的代码更改对象的任何字段，或防止代码修改传入方法的任何对象。CLR 不提供此功能，许多程序员一直对缺少此功能感到遗憾。由于 CLR 不提供此功能，因此没有任何语言（包括 C#）可以提供此功能。

首先，你应该注意，在非托管 C++ 中，将实例方法或参数标记为 const 只能确保程序员无法编写修改对象或参数的正常代码。在方法内部，始终可以编写通过转换掉 const 性质或获取对象/参数地址并写入该地址来改变对象/参数的代码。从某种意义上说，非托管 C++ 对程序员撒了谎，让他们相信常量对象/参数不能被写入，尽管它们实际上可以被写入。

在设计类型的实现时，开发人员可以直接避免编写操作对象/参数的代码。例如，字符串是不可变的，因为 `String` 类不提供任何可以更改字符串对象的方法。

另外，微软很难让 CLR 具备验证常量对象/参数是否未被修改的能力。CLR 必须在每次写入时验证写入是否发生在常量对象上，这会严重影响性能。当然，检测到违规将导致 CLR 抛出异常。此外，常量支持给开发人员增加了许多复杂性。例如，如果类型是不可变的，则所有派生类型都必须遵守这一点。此外，不可变类型可能必须由同样属于不可变类型的字段组成。

这些只是 CLR 不支持常量对象/参数的部分原因。

## 属性

本章内容：

- 无参属性 ........ 227
- 有参属性 ........ 242
- 调用属性访问器方法的性能 .... 247
- 属性访问器的可访问性 .... 248
- 泛型属性访问器方法 .... 248

在本章中，我将讨论属性。属性允许源代码使用简化的语法来调用方法。公共语言运行时（CLR）提供两种属性：无参属性，通常简称为*属性*；以及有参属性，不同的编程语言对其有不同的称呼。例如，C# 将可传参的属性称为*索引器*，而 Microsoft Visual Basic 将其称为*默认属性*。我还会讨论如何使用对象和集合初始化器来初始化属性，以及如何使用 C# 的匿名类型和 System.Tuple 类型将一堆属性打包在一起。

### 无参属性

许多类型定义了可以检索或更改的状态信息。通常，这些状态信息是通过类型的字段成员实现的。例如，下面是一个包含两个字段的类型定义。

```csharp
public sealed class Employee {
    public String Name;  // The employee's name
    public Int32 Age;    // The employee's age
}
```

如果你创建此类型的一个实例，就可以使用类似于下面的代码轻松获取或设置这些状态信息。

```csharp
Employee e = new Employee();
e.Name = "Jeffrey Richter";  // Set the employee's Name.
e.Age = 48;                  // Set the employee's Age.

Console.WriteLine(e.Name);   // Displays "Jeffrey Richter"
```

