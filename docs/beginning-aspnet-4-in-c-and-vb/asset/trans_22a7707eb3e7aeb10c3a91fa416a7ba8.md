
```csharp
this.LastName == other.LastName;
}
```

代码片段 StructuralComparison/Person.cs

现在创建了两个包含 Person 项的数组。两个数组都包含变量名为 `janet` 的同一个 Person 对象，以及两个内容相同但不同的 Person 对象。比较运算符 `!=` 返回 `true`，因为确实有两个不同的数组分别由两个变量名 `persons1` 和 `persons2` 引用。由于 Array 类没有重写带一个参数的 `Equals()` 方法，因此与使用 `==` 运算符比较引用时的情况相同，它们并不相同：

```csharp
var janet = new Person { FirstName = "Janet", LastName = "Jackson" };
Person[] persons1 = {
    new Person
    {
        FirstName = "Michael",
        LastName = "Jackson"
    },
    janet
};
Person[] persons2 = {
    new Person
    {
        FirstName = "Michael",
        LastName = "Jackson"
    },
    janet
};
if (persons1 != persons2)
    Console.WriteLine("not the same reference");
```

代码片段 StructuralComparison/Program.cs

调用 `IStructuralEquatable` 定义的 `Equals()` 方法，即第一个参数类型为 `object`、第二个参数类型为 `IEqualityComparer` 的方法，你可以通过传递实现 `IEqualityComparer<T>` 的对象来定义比较方式。`EqualityComparer<T>` 类提供了 `IEqualityComparer` 的默认实现。该实现会检查类型是否实现了 `IEquatable` 接口，如果实现了则调用 `IEquatable.Equals()` 方法；如果类型未实现 `IEquatable`，则调用基类 `Object` 的 `Equals()` 方法进行比较。

`Person` 实现了 `IEquatable<Person>`，其中比较的是对象的内容，而两个数组确实包含相同的内容：

```csharp
if ((persons1 as IStructuralEquatable).Equals(persons2,
    EqualityComparer<Person>.Default))
{
    Console.WriteLine("the same content");
}
```

接下来你将看到如何使用元组完成相同的事情。这里创建了两个具有相同内容的元组实例。当然，因为引用 `t1` 和 `t2` 引用两个不同的对象，所以 `!=` 比较返回 `true`：

```csharp
var t1 = Tuple.Create<int, string>(1, "Stephanie");
var t2 = Tuple.Create<int, string>(1, "Stephanie");
if (t1 != t2)
    Console.WriteLine("not the same reference to the tuple");
```

| 类别 | 运算符 |
|---|---|
| 赋值 | `= += -= *= /= %= &= |= ^= <<= >>=` |
| 成员访问（用于对象和结构） | `.` |
| 索引（用于数组和索引器） | `[]` |
| 强制转换 | `()` |
| 条件（三元运算符） | `?:` |
| 委托串联和移除（在第 8 章“委托、Lambda 和事件”中讨论） | `+ -` |
| 对象创建 | `new` |
| 类型信息 | `sizeof is typeof as` |
| 溢出异常控制 | `checked unchecked` |
| 间接寻址和地址 | `* -> &` |
| 命名空间别名限定符（在第 2 章“C# 核心”中讨论） | `::` |
| 空合并运算符 | `??` |

但请注意，四个特定运算符（`sizeof`、`*`、`->` 和 `&`，如下表所列）仅可在不安全代码（绕过 C# 类型安全检查的代码）中使用，这将在第 13 章“内存管理和指针”中讨论。还需要注意，`sizeof` 运算符关键字在与 .NET Framework 1.0 和 1.1 的早期版本一起使用时，需要不安全模式。自 .NET Framework 2.0 版本起，这不再是必需的要求。

| 类别 | 运算符 |
|---|---|
| 运算符关键字 | `sizeof`（仅用于 .NET Framework 1.0 和 1.1 版本） |
| 运算符 | `* -> &` |

使用 C# 运算符时需要小心的最大陷阱之一是，与其他 C 风格语言一样，C# 对赋值（`=`）和比较（`==`）使用不同的运算符。例如，以下语句表示让 `x` 等于 3：

```csharp
x = 3;
```

如果现在要将 `x` 与某个值进行比较，则需要使用双等号 `==`：

```csharp
if (x == 3)
{
}
```

幸运的是，C# 严格的类型安全规则可防止在逻辑语句中执行赋值而非比较这一非常常见的 C 错误。这意味着在 C# 中，以下语句将生成编译错误：

```csharp
if (x = 3)
{
}
```

习惯于使用与号（`&`）字符连接字符串的 Visual Basic 程序员需要做出调整。在 C# 中，使用加号（`+`）进行连接，而 `&` 符号表示两个不同整数值之间的按位与。符号 `|` 允许你在两个整数之间执行按位或。Visual Basic 程序员可能还不认识取模运算符（`%`）。

## 比较运算符（`==`）

最好将比较运算符视为严格值比较和严格引用比较之间的中间选项。在大多数情况下，编写以下代码意味着你在比较引用：

```csharp
bool b = (x == y); // x, y object references
```

然而，人们公认有些类如果被视为值，其含义会更直观。在这些情况下，最好重写比较运算符以执行值比较。重写运算符将在下文中讨论，这方面的一个明显例子是 `System.String` 类，Microsoft 已为其重写了该运算符，以比较字符串的内容而不是其引用。

## 比较值类型的相等性

在比较值类型的相等性时，与引用类型的原理相同：`ReferenceEquals()` 用于比较引用，`Equals()` 用于值比较，而比较运算符被视为中间情况。然而，最大的区别在于，值类型需要装箱转换为引用，以便在其上执行方法。此外，Microsoft 已经在 `System.ValueType` 类中重载了实例 `Equals()` 方法，以测试适用于值类型的相等性。如果你调用 `a.Equals(sB)`，其中 `a` 和 `sB` 是某个结构的实例，返回值将为 true 或 false，具体取决于 `a` 和 `sB` 在其所有字段中是否包含相同的值。另一方面，对于你自己的结构，默认情况下没有可用的 `==` 重载。在任何表达式中编写 `(sA == sB)` 都将导致编译错误，除非你在代码中为相关结构提供了 `==` 重载。

另一点是，`ReferenceEquals()` 应用于值类型时总是返回 false，因为要调用此方法，值类型需要装箱为对象。即使你编写以下代码，仍然会得到 false 的结果：

```csharp
bool b = ReferenceEquals(v, v); // v is a variable of some value type
```

原因是每次转换参数时 `v` 都会被单独装箱，这意味着你会得到不同的引用。因此，调用 `ReferenceEquals()` 来比较值类型确实没有意义。

尽管 `System.ValueType` 提供的 `Equals()` 默认重写几乎肯定足以满足你定义的大多数结构，但你可能希望为自己的结构再次重写它以提高性能。另外，如果值类型包含引用类型作为字段，你可能希望重写 `Equals()` 为这些字段提供适当的语义，因为默认的 `Equals()` 重写只会比较它们的地址。

## 运算符重载

本节介绍你可以为类或结构定义的另一类成员：运算符重载。

运算符重载对于 C++ 开发人员来说应该很熟悉。然而，由于这个概念对 Java 和 Visual Basic 开发人员来说都是新的，我们在这里进行解释。C++ 开发人员可能更愿意跳到主要的运算符重载示例。

运算符重载的意义在于，你并不总是只想调用对象上的方法或属性。通常，你需要将数量相加、相乘，或执行逻辑操作（如比较对象）。假设你定义了一个表示数学矩阵的类。那么，在数学世界中，矩阵可以像数字一样相加和相乘。因此，你想编写如下代码是完全合理的：

```csharp
Matrix a, b, c;
// assume a, b and c have been initialized
Matrix d = c * (a + b);
```

