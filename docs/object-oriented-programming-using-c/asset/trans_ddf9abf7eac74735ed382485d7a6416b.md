

# 反馈 5

首先，为了打印账单，`RentCollector` 需要知道应收租金。对于房屋（House），没有定义 `DetermineRent()` 方法——但这并不意味着它不存在。

它必须存在，因为 `House` 继承了 `Building` 的属性和方法！

我们只在方法是额外方法或被重写的方法时才在子类中显示它们。

租金收集者需要一个 `Building`，而 `House` 是 `Building` 的一种类型。因此，虽然 `RentCollector` 和 `House` 之间没有显示关联，但 `RentCollector` 可以为房屋打印账单。在任何需要 `Building` 对象的地方，我们都可以用 `House` 对象代替，因为它是 `Building` 的一种。这是多态的一个示例，我们将在第 4 章中看到其他示例。

# 活动 6

修改此 UML 图，显示 `DetermineRent()` 在 `House` 中被重写了（即被替换）。

![](img/e143b38d00f95425fa4f3efca0527189_68_0.png)

# 使用 C# 的面向对象编程

# 继承与方法重写

# 反馈 6

![](img/e143b38d00f95425fa4f3efca0527189_69_0.png)

通过在 `House` 中显示 `DetermineRent()`，我们展示了该方法重写了基类（Building）中定义的方法。

有趣的是，NET CLR 引擎将根据调用方法的对象类型使用正确的 `DetermineRent()` 方法。因此，如果为房屋打印账单，`RentCollector` 将调用 `House` 中定义的方法；而对于任何其他类型的建筑，它将使用 `Building` 中定义的方法。这是自动完成的——`RentCollector` 类中的代码并不区分 `Building` 的类型。

重写将在本章稍后部分进行详细讨论。

# 3.4 在 C# 中实现继承

创建父类不需要特殊功能。因此，除非被明确禁止，否则任何类都可以成为子类。

子类使用 **符号** 指明它正在从父类继承特性。例如....

```csharp
class MySubClass : MySuperclass
{
    // 额外的实例变量和
    // 额外的方法
}
```

# 3.5 构造函数

构造函数是从类创建对象的方法。每个类（无论是父类还是子类）都应该在构造函数中封装自己的初始化，通常与设置实例变量的初始状态有关。构造函数是与类同名的方法。

父类（或基类）的构造函数应该处理通用初始化。

# 使用 C# 的面向对象编程

# 继承与方法重写

每个子类都可以有自己的构造函数进行特殊初始化，但它通常必须调用基类构造函数的行为。它使用关键字 `base` 实现这一点。

```csharp
class MySubClass : MySuperClass
{
    public MySubClass (sub-parameters) : base (super-parameters)
    {
        // 其他初始化
    }
}
```

通常传递给 `MySubClass` 的某些参数是父类实例变量的初始化值，这些值将作为参数传递给父类构造函数。换句话说，父类参数是子参数的部分（或全部）。

下面显示了两个构造函数，一个用于 `Publication` 类，一个用于 `Book`。`Book` 构造函数需要四个参数，其中三个立即传递给基类构造函数以初始化其实例变量。

![](img/e143b38d00f95425fa4f3efca0527189_70_0.png)

www.simcorp.com
降低风险 | 减少成本 | 促进增长

# 使用 C# 的面向对象编程

# 继承与方法重写

```csharp
// Publication 类的构造函数
public Publication(String title, double price, int copies)
{
    this.title = title;
    // 等
}
```

```csharp
// Book 类的构造函数
public Book(String title, double price, int copies, String author)
    : base(title, price, copies)
{
    this.author = author;
}
```

因此，在创建书籍对象时，我们首先创建一个出版（Publication）对象。`Books` 的构造函数通过调用 `Publication` 的构造函数来实现这一点。

# 3.6 构造函数规则

存在规范父级构造函数调用的规则。

如果父类有一个无参数（或默认）构造函数，那么当子类构造函数中没有显式调用 `base` 时，它将被自动调用，尽管出于清晰性考虑，显式调用仍然是做法。

然而，如果父类没有无参数构造函数但有一个带参数的构造函数，则**必须**使用 `: base` 显式调用。为了说明这一点....

![](img/e143b38d00f95425fa4f3efca0527189_71_0.png)

上方左侧：由于父类有无参数构造函数，拥有一个没有构造函数的子类是合法的，但不是良好的做法。

中间：子类构造函数没有调用基构造函数，则将调用无参数的父类构造函数。

右侧：父类没有无参数构造函数，子类必须有一个构造函数，它必须使用关键字 `base` 调用父构造函数并传递所需的参数。这是因为一个只有带参数构造函数的（父）类只能通过提供所需的参数（s）进行初始化。

# 3.7 访问控制

为了强制封装，我们通常将实例变量设为私有，并根据需要提供访问器/修改器方法（在 C# 中我们使用属性）。

`Publication` 的 `SelfCopy()` 方法需要更改变量 'copies' 的值。`Book` 和 `Magazine` 都需要修改 'copies' 的值。在 C# 中有三种方法可以实现这一点：

- 1) 将 'copies' 设为私有，并创建必要的访问器方法；
- 2) 将 'copies' 设为受保护（protected），这对于子类是的；
- 3) 在 C# 中创建属性，这会更简单。

通常，我们将变量设为私有，并根据需要提供访问器/修改器方法（在 C# 中我们使用属性）。

这里我们将展示对 'copies' 的访问：

# 使用 C# 的面向对象编程

# 继承与方法重写

在父类中显示 `DetermineRent()` 是在展示该方法重写了基类（Building）中定义的方法。

```csharp
private int copies;
public int GetCopies()
{
    return copies;
}
public void SetCopies(int newValue)
{
    copies = newValue;
}
```

![](img/e143b38d00f95425fa4f3efca0527189_73_0.png)

有趣的是，NET CLR 引擎将根据调用方法的对象类型使用正确的 `DetermineRent()` 方法。因此，如果为房屋打印账单，`RentCollector` 将调用 `House` 中定义的方法；而对于任何其他类型的建筑，它将使用 `Building` 中定义的方法。这是自动完成的——`RentCollector` 类中的代码并不区分 `Building` 的类型。

重写将在本章稍后部分进行详细讨论。

在沃尔沃集团（Volvo Group）工作意味着在全球180多个国家拥有10万名朋友和同事。无论你想要什么样的未来，请访问我们的网站 www.volvroup.com。我们期待与你交流！

请点击广告

沃尔沃
所有 Volvo

VIDEO TRUCKS | HEAVY TRUCKS | MACH TRUCK | VIDEO BUSES | VOLVO CONSTRUCTION EQUIPMENT | VIDEO PHONE | VIDEO AUDIO | VOLVO FINANCIAL SERVICES | VIDEO 3D | VOLVO PARTS | VIDEO TECHNOLOGY | LOGISTICS | ASIA AND AFRICA

在 bookboom.com 下载免费电子书

# 面向对象 C#

这些方法允许父类控制对私有变量的访问。

目前它们实际上没有实施任何限制，但假设我们想要确保 'copies' 不被设置为负值。

- (a) 'copies' 是**私有的 (private)**，我们可以在 `SetCopies()` 方法中放入验证（即一个语句），并确定值绝不会被破坏。
- (b) 'copies' 是部分暴露的**受保护的 (protected)**，我们需要查看子类方法更改实例变量的所有场合并在每处进行验证。

我们甚至可以考虑将这些方法设为**受保护的 (protected)** 而不是公共，这样它们的使用仅限于子类，其他类无法干扰 'copies' 的使用。

在子类 `Book` 和 `Magazine` 中制作这些方法的方法：

```csharp
// 在 Book 中
public void OrderCopies(int orderQty)
{
    SetCopies(GetCopies() + orderQty);
}
```

```csharp
// 以及在 Magazine 中
public void RecNewIssue(String newIssue)
{
    SetCopies(orderQty);
    currIssue = newIssue;
}
```

这些语句等同于
copies = copies + orderQty;
以及在 'Magazine' 中
copies = orderQty;

在 C# 中，可以定义属性来真实地隐藏访问器方法并使代码更简单。“属性”一词在 C# 中有一个特定的含义，与类的“属性”并不相同。

在下面的代码中，定义了两个变量：'price' 和 'copies'，并为每个变量定义了一个属性……名称与变量名相同，但首字母大写。

