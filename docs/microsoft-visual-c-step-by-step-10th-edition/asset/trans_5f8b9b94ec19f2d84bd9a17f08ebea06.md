

14. 返回代码和文本编辑器窗口中的 `DrawingShape` 类。
将此类中的 `SetColor` 方法替换为此处显示的 `Color` 属性：

[点击查看代码图像]

```
public Color ColorColor{
    set {
        if (this.shape is not null) {
            SolidColorBrush brush = new SolidColorBrush(value);
            this.shape.Fill = brush;
        }
    }
}
```

> 注意
set 访问器的代码与原始 `SetColor` 方法几乎相同，只是创建 `SolidColorBrush` 对象的语句传递了 `value` 参数。此外，这是一个方法语法比使用表达式成员（expression-bodied member）更合适的示例。

15. 返回代码和文本编辑器窗口中的 `DrawingPad.xaml.cs` 文件。
在 `drawingCanvas_Tapped` 方法中，修改设置 `Square` 对象颜色的语句，以匹配以下代码：

[点击此处代码图像]

```
if (mySquare is IColor){
    IColor colorSquare = mySquare;
    colorSquare.Color = Colors.BlueViolet;
}
```

16. 同样，在 `drawingCanvas_RightTapped` 方法中，如**加粗**所示修改设置 `Circle` 对象颜色的语句。

[点击此处代码图像](_ )

```
if (myCircle is IColor)
{
    IColor colorCircle = myCircle;
    colorCircle.Color = Colors.HotPink;
}
```

- 17. 在“调试”菜单上，选择“启动调试”以生成并运行项目。

- 18. 验证应用程序的运行方式与之前相同。如果你在画布上点击屏幕或点击左鼠标键，应用程序将绘制一个正方形；如果你点击、按住或点击右键，应用程序将绘制一个圆：

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_570_0.png)

- 19. 返回 Visual Studio 2022 编程环境并停止调试。

# 使用属性进行模式匹配

C# 包含了模式匹配功能，可以利用类型中的属性值。例如，假设你正在应用程序中模拟银行账户。你定义了以下接口：

[点击查看代码图像]

```
interface IBankAccount
{
    decimal Balance { get; }
    decimal OverdraftLimit { get; }
    void Deposit(decimal amount);
    decimal Withdraw(decimal amount);
}
```

你实现了几种类型的银行账户，每种账户都有不同的限制和利率：

[点击查看代码图像]

```
class CurrentAccount : IBankAccount
{
    // 未显示实现细节
    ...
}
class DepositAccount : IBankAccount
{
    // 未显示实现细节
}
class HighInterestSavingsAccount : IBankAccount
{
    // 未显示实现细节
    ...
}
```

你想编写一个方法来计算任何此类类型账户的应收利息。支付的金额取决于余额和账户类型。`switch` 语句允许你根据模式匹配能力快速、方便地执行一组复杂的规则，模式匹配能力允许你确定对象的类型及其属性的值。以下代码显示了 `CalculateInterest` 方法：

[点击查看代码图像]

```
public static decimal CalculateInterest(IBankAccount acc) =>
    acc switch
    {
        CurrentAccount ca when ca.Balance < 500 => 0.05m,
        CurrentAccount ca when ca.Balance >= 500 && ca < 5000 => 0.5m,
        CurrentAccount ca when ca.Balance >= 5000 => 0.75m,
        DepositAccount da when da.Balance >= 2000 => 0.75m,
        DepositAccount da => 0.5m,
        HighInterestSavingsAccount his when his.Balance >= 5000 => 2.0m,
        HighInterestSavingsAccount his => 1.2m,
        _ => throw new ArgumentException("Unknown account type")
    };
```

每个 switch 表达式的 `when` 子句启用了 `Balance` 属性。这种方法清晰简洁；它读起来像是用户对如何计算利息的规范，而不是一段 C# 代码。

# 生成自动属性

在本章早期提到，属性的主要目的是从外部隐藏字段的实现。如果你的属性实际上执行了有用的工作，那没问题；但如果 `get` 和 `set` 访问器只是封装了读取或向字段赋值的操作，那么你可能会怀疑这种方法的价值。

即使在这些情况下，至少有两个理由你应该定义属性而不是将数据暴露为公共字段：

- **与应用程序的兼容性** 字段和属性在程序集中使用不同的元数据来暴露自己。如果你开发了一个类并决定使用公共字段，任何使用该类的应用程序都将这些项引用为字段。虽然你在读写属性时使用相同的 C# 语法，但编译后的代码实际上非常不同——C# 编译器向你隐藏了这些差异。如果你以后决定确实需要将这些字段更改为属性（可能业务需求发生了变化，你需要在赋值时执行额外的逻辑），那么现有的应用程序在不重新编译的情况下无法使用更新后的类。如果你已经在整个组织内的大量设备上部署了该应用程序，这将很尴尬。虽然有方法可以规避，但通常情况下最好避免陷入这种情况。

- **与接口的兼容性** 如果你正在实现一个接口且接口将某项定义为属性，你必须编写与接口规范匹配的属性，即使该属性只是在私有字段中读写数据。你不能简单通过暴露同名的公共字段来实现属性。

C# 语言的设计者意识到，程序员是忙碌的人，不应该浪费时间编写超出需要的内容。为此，C# 编译器可以自动生成属性的代码，如下：

[点击查看代码图像]

```
class Circle
{
    public int Radius{ get; set; }
    ...
}
```

在此示例中，`Circle` 类包含一个名为 `Radius` 的属性。除了该属性的类型外，你没有指定属性如何工作——`get` 和 `set` 访问器是空的。C# 编译器将此定义转换为私有字段和类似于下面的内容的默认实现：

[点击查看代码图像]

```
class Circle
{
    private int _radius;
    public int Radius{
        get{
            return this._radius;
        }
        set
{
            this._radius = value;
        }
    }
    ...
}
```

因此，只需少量努力，你就可以自动生成的代码实现简单的属性。如果你以后需要包含额外的逻辑，可以在不破坏任何现有应用程序的情况下这样做。

> 注意
定义自动属性的语法与在接口中定义属性的语法几乎相同。异常是自动属性可以指定访问修饰符，例如 `private`、`public` 或 `protected`。

你可以通过从属性声明中省略空的 `set` 访问器来创建一个只读自动属性，如下：

[点击查看代码图像]

```
class Circle
{
    public DateTime CircleCreated { get; }
...
}
```

这在你想要创建一个不可变属性的场景中非常有用——即在对象构造时设置且随后无法更改的属性。例如，你可能想要设置对象的创建日期或创建用户的用户名，或者你可能想为对象生成一个唯一标识符。这些是你通常只想设置一次然后防止它们被修改的值。考虑到这一点，C# 允许你通过两种方式之一初始化只读自动属性。你可以从构造函数初始化属性，如下：

```
class Circle
{
    public Circle()
    {
        CircleCreatedDate = DateTime.Now;
    }
    public DateTime CircleCreated { get; }
}
```

