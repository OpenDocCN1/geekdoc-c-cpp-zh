

引用类型会碎片化堆并拖慢你的速度。如果你创建的类型旨在存储数据值，值类型是首选。

决定将类型设为值类型还是引用类型是一个重要的决定。将值类型转换为类类型是一项深远的变更。考虑这个类型：

```
public struct Employee
{
    // Properties elided
    public string Position
    {
        get;
        set;
    }

    public decimal CurrentPayAmount
    {
        get;
        set;
    }

    public void Pay(BankAccount b)
    {
        b.Balance += CurrentPayAmount;
    }
}
```

这个相当简单的类型包含一个方法，用于让你支付员工工资。时间流逝，系统运行良好。然后你决定员工有不同类别：销售人员获得佣金，经理获得奖金。你决定将 Employee 类型改为类：

```
public class Employee
{
    // Properties elided
    public string Position
    {
        get;
        set;
    }

    public decimal CurrentPayAmount
    {
        get;
        set;
    }

    public virtual void Pay(BankAccount b)
    {
        b.Balance += CurrentPayAmount;
    }
}
```

这会破坏使用你的 Employee 结构体的大量现有代码。按值返回变为按引用返回。之前按值传递的参数现在按引用传递。这段小代码的行为发生了剧烈变化：

```
Employee e1 = Employees.Find(e => e.Position == "CEO");
BankAccount CEOBankAccount = new BankAccount();
decimal Bonus = 10000;
e1.CurrentPayAmount += Bonus; // Add one time bonus.
e1.Pay(CEOBankAccount);
```

曾经只是一次性加薪以添加奖金，现在变成了永久性加薪。原本使用按值复制的地方，现在放置了引用。编译器会很高兴地为你做出这些更改。CEO 可能也很高兴。但另一方面，CFO 会报告这个错误。你事后无法改变对值类型和引用类型的看法：这会改变行为。

这个问题发生的原因是 Employee 类型不再遵循值类型的准则。除了存储定义员工的数据元素外，你还添加了责任——在此示例中，即支付员工工资。责任是类类型的领域。类可以轻松定义常见责任的多态实现；结构体不能，并且应限于存储值。

.NET 文档建议你将类型的大小作为值类型和引用类型之间的决定性因素。实际上，更好的因素是类型的用途。简单结构或数据载体类型是值类型的绝佳候选。确实，值类型在内存管理方面更高效：

堆碎片化更少，垃圾更少，间接引用更少。更重要的是，值类型在从方法或属性返回时会被复制。没有暴露内部结构引用的危险。但你在功能方面付出了代价。值类型对常见面向对象技术的支持非常有限。你不能创建值类型的对象层次结构。你应该将所有值类型视为密封的。你可以创建实现接口的值类型，但需要装箱，而 Item 17 显示这会导致性能下降。将值类型视为存储容器，而不是面向对象意义上的对象。

你会创建比值类型更多的引用类型。如果对所有这些问题都回答“是”，则应该创建值类型。将这些与之前的 Employee 示例进行比较：

- 1. 此类型的主要职责是数据存储吗？
- 2. 其公共接口是否完全由访问其数据成员的属性定义？
- 3. 我确定此类型永远不会有子类吗？
- 4. 我确定此类型永远不会被多态处理吗？

将低级数据存储类型构建为值类型。使用引用类型构建应用程序的行为。你可以获得从类对象导出的数据复制的安全性。你可以获得基于栈和内联值存储带来的内存使用优势，并且可以利用标准面向对象技术来创建应用程序的逻辑。当对预期用途存疑时，使用引用类型。

## Item 19: 确保 0 是值类型的有效状态

默认的 .NET 系统初始化将所有对象设置为全 0。你无法阻止其他程序员创建初始化为全 0 的值类型实例。将其作为你的类型的默认值。

一个特殊情况是枚举。永远不要创建不包含 0 作为有效选项的枚举。所有枚举都派生自 System.ValueType。枚举的值从 0 开始，但你可以修改该行为：

```
public enum Planet
{
    // Explicitly assign values.
    // Default starts at 0 otherwise.
    Mercury = 1,
    Venus = 2,
    Earth = 3,
    Mars = 4,
    Jupiter = 5,
    Saturn = 6,
    Neptune = 7,
    Uranus = 8
    // First edition included Pluto.
}
```

```
Planet sphere = new Planet();
```

sphere 是 0，这不是一个有效值。任何依赖于（正常）事实的代码，即枚举被限制在定义的枚举值集合中，都将无法工作。当你为枚举创建自己的值时，请确保 0 是其中之一。如果你在枚举中使用位模式，请将 0 定义为所有其他属性的缺失。

目前，你迫使所有用户显式初始化该值：

```
Planet sphere2 = Planet.Mars;
```

这使得构建包含此类型的其他值类型变得更加困难：

```
public struct ObservationData
{
    private Planet whichPlanet; //what am I looking at?
    private double magnitude; // perceived brightness.
}
```

创建新 ObservationData 对象的用户将创建一个无效的 Planet 字段：

```
ObservationData d = new ObservationData();
```

新创建的 ObservationData 具有 0 的 magnitude，这是合理的。但行星无效。你需要使 0 成为有效状态。如果可能，选择最佳默认值作为值 0。Planet 枚举没有明显的默认值。当用户不选择时，选择某个任意行星没有任何意义。如果你遇到这种情况，请使用 0 情况作为稍后可以更新的未初始化值：

```
public enum Planet2
{
    None = 0,
    Mercury = 1,
    Venus = 2,
    Earth = 3,
    Mars = 4,
    Jupiter = 5,
    Saturn = 6,
    Neptune = 7,
    Uranus = 8
}
```

```
Planet2 sphere = new Planet2();
```

sphere 现在包含 None 的值。将此未初始化默认值添加到 Planet 枚举会向上传播到 ObservationData 结构。新创建的 ObservationData 对象具有 0 的 magnitude 和 None 的目标。添加显式构造函数，以允许你的类型的用户显式初始化所有字段：

```
public struct ObservationData
{
    Planet2 whichPlanet; //what am I looking at?
    double magnitude; // perceived brightness.
    ObservationData(Planet2 target,
    double mag)
    {
    whichPlanet = target;
    magnitude = mag;
    }
}
```

但请记住，默认构造函数仍然可见且是结构的一部分。用户仍然可以创建系统初始化的变体，你无法阻止他们。

这仍然有些缺陷，因为观察无物并不真正合理。你可以通过将 ObservationData 更改为类来解决此特定情况，这意味着无参数构造函数不需要可访问。但是，当你创建枚举时，你无法强迫其他开发者遵守这些规则。你所能做的最好的就是创建 0 位模式有效的枚举类型，即使这不是一个完美的抽象。

在离开枚举去讨论其他值类型之前，你需要了解一些用作标志的枚举的特殊规则。使用 Flags 特性的枚举应始终将 None 值设置为 0：

```
[Flags]
public enum Styles
{
    None = 0,
    Flat = 1,
    Sunken = 2,
    Raised = 4,
}
```

许多开发者将按位 AND 运算符与标志枚举一起使用。0 值会导致位标志出现严重问题。如果 Flat 的值为 0，则以下测试永远不会起作用：

```
if ((flag & Styles.Flat) != 0) // Never true if Flat == 0.
    DoFlatThings();
```

如果你使用 Flags，请确保 0 是有效的，并且它表示“所有标志的缺失。”

另一个常见的初始化问题涉及包含引用的值类型。字符串是常见示例：

```
public struct LogMessage
{
    private int ErrLevel;
    private string msg;
}
```

```
LogMessage MyMessage = new LogMessage();
```

MyMessage 在其 msg 字段中包含一个 null 引用。无法强制执行不同的初始化，但你可以使用属性来本地化问题。你创建了一个属性，将 msg 的值导出给所有客户端。向该属性添加逻辑，以返回空字符串而不是 null：

