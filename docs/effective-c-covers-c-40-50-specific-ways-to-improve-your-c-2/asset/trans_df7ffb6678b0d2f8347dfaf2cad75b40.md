
最终，人们会使用你类型中的信息。人们能理解文本输出，因此你希望以最简单的方式提供它：在所有类型中重写 ToString()。使 ToString() 的输出简短且合理。

## 第 6 条：理解众多不同相等概念之间的关系

当你创建自己的类型（无论是类还是结构体）时，你定义该类型中相等的含义。C# 提供了四个不同的函数来确定两个不同的对象是否“相等”：

```
public static bool ReferenceEquals
    (object left, object right);
public static bool Equals
    (object left, object right);
public virtual bool Equals(object right);
public static bool operator ==(MyClass left, MyClass right);
```

该语言允许你创建所有这四个方法的自定义版本。但仅仅因为你可以，并不意味着你应该这样做。你永远不应该重新定义前两个静态函数。你通常会创建自己的实例 Equals() 方法来定义你自己类型的语义，并且你偶尔会重写 operator==()，通常出于值类型的性能考虑。此外，这四个函数之间存在关系，因此当你更改其中一个时，可能会影响其他函数的行为。是的，需要四个函数来测试相等性是复杂的。但不用担心——你可以简化它。

当然，这四个方法并不是相等性的唯一选项。重写 Equals() 的类型应实现 IEquatable<T>。实现值语义的类型应实现 IStructuralEquality 接口。这意味着有六种不同的方式来表达相等性。

就像 C# 中许多复杂的元素一样，这一点源于 C# 允许你创建值类型和引用类型。引用类型的两个变量如果引用同一个对象，则相等，这被称为对象标识。值类型的两个变量如果类型相同且包含相同内容，则相等。这就是为什么相等性测试需要这么多不同的方法。

让我们从你永远不应该更改的两个函数开始。Object.ReferenceEquals() 如果两个变量引用同一个对象，则返回 true——也就是说，这两个变量具有相同的对象标识。无论被比较的类型是引用类型还是值类型，此方法始终测试对象标识，而不是对象内容。是的，这意味着当你使用它来测试值类型的相等性时，ReferenceEquals() 始终返回 false。即使你将值类型与其自身进行比较，ReferenceEquals() 也返回 false。这是由于装箱造成的，将在第 45 条中介绍。

```
int i = 5;
int j = 5;
if (Object.ReferenceEquals(i, j))
    Console.WriteLine("Never happens.");
else
    Console.WriteLine("Always happens.");

if (Object.ReferenceEquals(i, i))
    Console.WriteLine("Never happens.");
else
    Console.WriteLine("Always happens.");
```

你永远不会重新定义 Object.ReferenceEquals()，因为它正好做了它应该做的事情：测试两个不同变量的对象标识。

你永远不会重新定义的第二个函数是 static Object.Equals()。当你不知道两个参数的运行时类型时，此方法测试两个变量是否相等。请记住，System.Object 是 C# 中一切事物的最终基类。每当你比较两个变量时，它们都是 System.Object 的实例。值类型和引用类型都是 System.Object 的实例。那么，当相等性的含义取决于类型时，此方法如何在不知道类型的情况下测试两个变量的相等性呢？答案很简单：此方法将该责任委托给涉及的类型之一。静态 Object.Equals() 方法的实现大致如下：

```
public static new bool Equals(object left, object right)
{
    // Check object identity
    if (Object.ReferenceEquals(left, right) )
        return true;
    // both null references handled above
    if (Object.ReferenceEquals(left, null) ||
        Object.ReferenceEquals(right, null))
        return false;

    return left.Equals(right);
}
```

此示例代码介绍了一种我尚未讨论的方法：即实例 Equals() 方法。我将稍后详细解释，但我还没有准备好结束对静态 Equals() 的讨论。目前，我希望你理解静态 Equals() 使用左参数的实例 Equals() 方法来确定两个对象是否相等。

与 ReferenceEquals() 一样，你永远不会重载或重新定义你自己的静态 Object.Equals() 版本，因为它已经正好做了它需要做的事情：在不知道运行时类型时确定两个对象是否相同。因为静态 Equals() 方法委托给左参数的实例 Equals()，所以它使用该类型的规则。

现在你明白为什么永远不需要重新定义静态 ReferenceEquals() 和 static Equals() 方法了。是时候讨论你将要重写的方法了。但是首先，让我们简要讨论一下相等关系的数学属性。你需要确保你的定义和实现与其他程序员的期望一致。这意味着你需要牢记相等性的数学属性：相等性是自反的、对称的和传递的。自反属性意味着任何对象都等于其自身。无论涉及什么类型，a == a 始终为 true。对称属性意味着顺序无关紧要：如果 a == b 为 true，则 b == a 也为 true。如果 a == b 为 false，则 b == a 也为 false。最后一个属性是，如果 a == b 和 b == c 都为 true，则 a == c 也必须为 true。这就是传递属性。

现在是时候讨论实例 Object.Equals() 函数了，包括何时以及如何重写它。当默认行为与你的类型不一致时，你会创建自己的 Equals() 实例版本。Object.Equals() 方法使用对象标识来确定两个变量是否相等。默认的 Object.Equals() 函数的行为与 Object.ReferenceEquals() 完全相同。但是等等——值类型不同。System.ValueType 确实重写了 Object.Equals()。请记住，ValueType 是你创建的所有值类型（使用 struct 关键字）的基类。值类型的两个变量如果类型相同且内容相同，则相等。ValueType.Equals() 实现了该行为。不幸的是，ValueType.Equals() 没有高效的实现。ValueType.Equals() 是所有值类型的基类。为了提供正确的行为，它必须在不知道对象运行时类型的情况下，比较任何派生类型中的所有成员变量。在 C# 中，这意味着使用反射。如你将在第 43 条中看到，反射有许多缺点，尤其是在性能是目标时。相等性是程序中频繁调用的基本构造之一，因此性能是一个值得追求的目标。在几乎所有情况下，你都可以为任何值类型编写一个更快的 Equals() 重写。值类型的建议很简单：每当你创建一个值类型时，始终创建 ValueType.Equals() 的重写。

你应该仅在想要更改引用类型的定义语义时才重写实例 Equals() 函数。.NET Framework 类库中的许多类在相等性方面使用值语义而不是引用语义。两个字符串对象如果包含相同内容，则相等。两个 DataRowView 对象如果引用同一个 DataRow，则相等。关键是，如果你的类型应该遵循值语义（比较内容）而不是引用语义（比较对象标识），你应该编写自己的 instance Object.Equals() 重写。

既然你知道何时编写 Object.Equals() 的自定义重写，你就必须了解如何实现它。值类型的相等关系对装箱有许多影响，将在第 45 条中讨论。对于引用类型，你的实例方法需要遵循预定义的行为，以避免给你的类的用户带来奇怪的惊喜。每当你重写 Equals() 时，你都希望为该类型实现 IEquatable<T>。我将在本条目稍后解释原因。以下是重写 System.Object.Equals 的标准模式。高亮显示了实现 IEquatable<T> 的更改。

```
public class Foo : IEquatable<Foo>
{
    public override bool Equals(object right)
    {
        // check null:
        // this pointer is never null in C# methods.
        if (object.ReferenceEquals(right, null))
            return false;

        if (object.ReferenceEquals(this, right))
            return true;
    }
}
```
