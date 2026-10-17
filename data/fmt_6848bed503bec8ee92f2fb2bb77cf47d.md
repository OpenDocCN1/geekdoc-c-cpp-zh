
```csharp
carRepository.Search(txtSearch.Text).Output(
    a => 1stResultItems.Add(a.DisplayValue));
```

- 4. 启动应用程序，在文本框中输入值并点击 `btnPrintListBox` 按钮。列表框应显示匹配汽车的信息。
- 5. 为 `btnPrintToComboBox` 按钮添加 `Click` 事件。
- 6. 重复步骤 5，清空组合框并在 Lambda 表达式中指向其 `Add` 方法。
- 7. 启动应用程序，在文本框中输入值并点击 `btnPrintToComboBox` 按钮。组合框应显示匹配汽车的信息。

目前的表单类：

```csharp
public partial class Form1 : Form
{
    Repository<Car> carRepository = new Repository<Car>();

    public Form1() ...

    private void btnSearch_Click(object sender, EventArgs e) ...

    private void btnPrintListBox_Click(object sender, EventArgs e)
    {
        1stResult.Items.Clear();
        carRepository.Search(txtSearch.Text)
            .Output(a => 1stResult.Items.Add(a.DisplayValue));
    }
}
```

```csharp
private void btnPrintToComboBox_Click(object sender, EventArgs e)
{
    cboResult.Items.Clear();
    carRepository.Search(txtSearch.Text)
        .Output(a => cboResult.Items.Add(a.DisplayValue));
}
```

# 使用 Func

在本练习中，你将创建一个名为 `FirstMatch` 的 `Func`，它返回匹配文本框中输入的搜索文本的第一个项目。

- 1. 为 `btnCallFunc` 按钮添加 `Click` 事件。
- 2. 创建一个 `Func` 委托 `FirstMatch`，接受一个字符串参数并调用 `carRepository` 上的 `Search` 方法，返回匹配搜索的第一辆汽车。使用 Lambda 表达式调用 `Search` 方法：

```csharp
Func<string, Car> FirstMatch = search => // 定义 Func 委托
    carRepository.Search(search).FirstOrDefault();
```

- 3. 使用文本框中的文本调用 `FirstMatch` 方法并将结果存储在标签中。
- 4. 启动应用程序，在文本框中输入值并点击 `btnCallFunc` 按钮。列表框应显示匹配汽车的信息。

目前的表单类：

```csharp
public partial class Form1 : Form
{
    Repository<Car> carRepository = new Repository<Car>();

    public Form1() ...
}
```

# 使用 Predicate

在本练习中，你将创建一个名为 `Contains` 的 `Predicate`，如果存在匹配则返回 `true`，否则返回 `false`。

- 1. 为 `btnCallPredicate` 按钮添加 `Click` 事件。
- 2. 创建一个 `Predicate` 委托 `Contains`，接受一个字符串参数并调用 `carRepository` 上的 `Search` 方法，如果存在匹配则返回 `true`。使用 Lambda 表达式调用 `Search` 方法：

```csharp
Predicate<string> Contains = search => carRepository.Search(search).Count() > 0;
```

- 3. 使用文本框中的文本调用 `Contains` 方法并将结果存储在标签中。
- 4. 启动应用程序，在文本框中输入值并点击 `btnCallPredicate` 按钮。标签应显示匹配汽车的信息。

# 事件与泛型

使用泛型事件从对象向调用者发送信息可能是非常有用的。使用普通事件，你必须预先指定数据类型，这强制事件只能与该类型工作。然而，使用泛型事件，你可以在注册事件时指定要使用的类型，使得事件可以与任何类型配合。

要声明泛型事件，你使用 `EventHandler<T>` 类，这节省了一行代码，因为你不需要显式为它指定委托；它在后台已经提供了一个。

# C# 初学者教程

每个事件包含两个参数：类型为 `object` 的发送者（`sender`），它是事件源的对象或控件；以及 `EventArgs`，它可能包含需要发送给订阅者（接收者）的对象或控件的数据。要通过事件传递自定义数据，你需要创建一个包含相应属性的自定义 `EventArgs`。

要创建 `EventArgs` 类，你需要添加一个派自 `EventArgs` 类的新类并向其添加属性。由于泛型类型 `T` 在触发事件的类始终可用，因此你可以在 `EventArgs` 类中安全地使用它。

# 示例：泛型事件

在这个示例中，你将看到如何使用泛型事件将数据传递给订阅者。

在交给你的任务规范中规定，你应该能够从名为 `Buffer` 的类的列表中删除项，并在项被删除时触发一个事件。首要任务是创建一个继承自 `EventArgs` 类的 `RemovedItemEventArgs` 类。

注意，泛型类型 `T` 被传递给该类并用于存储被删除的项。

```csharp
public class RemovedItemEventArgs<T> : EventArgs
{
    public T RemovedItem { get; set; }

    public RemovedItemEventArgs(T removedItem)
    {
        RemovedItem = removedItem;
    }
}
```

`Buffer` 类包含一个泛型类型 `T`，并包含一个存储项的集合。

```csharp
public class Buffer<T>
{
    public List<T> items = new List<T>();
}
```

# C# 初学者教程

向 `Buffer` 类添加该事件。当项从集合中删除时，该事件将被触发。

```csharp
public event EventHandler<RemovedItemEventArgs<T>> ItemRemoved;
```

向 `Buffer` 类添加 `RemoveItem` 方法，它将从指定索引处从集合中删除项并向订阅者触发事件。

```csharp
public void RemoveItem(int index)
{
    var item = items.ElementAtOrDefault(index);
    // 创建 EventArgs 并触发事件
    var eventArgs = new RemovedItemEventArgs<T>(item);
    ItemRemoved(this, eventArgs);
    items.RemoveAt(index);
}
```

完成 `Buffer` 类后，我们移动到表单，在表单中将事件订阅到按钮上。将 `Buffer` 类的实例添加到表单中并填充以下数据。

```csharp
Buffer<string> buffer = new Buffer<string>();
buffer.items.Add("First string");
buffer.items.Add("Second string");
buffer.items.Add("Third string");
```

在按钮的 `Click` 事件中订阅该事件，并从集合中删除第二个项，然后在列表框中显示剩余项。

```csharp
private void btnEvent_Click(object sender, EventArgs e)
{
    // 订阅事件
    buffer.ItemRemoved += buffer_ItemRemoved;
    // 移除第二个项 "Second string"
    buffer.RemoveItem(1);
    // 在列表框中显示剩余项
    lstResult.Items.Clear();
}
```

规则将由 `RuleComparer` 类的实例进行评估，该类实现了 `IComparer` 接口，以定义如何比较两个 `object` 值。它还将实现一个泛型方法 `EvaluateRules<T>`，该方法将接受一个 `T` 类型的项和一个 `BusinessRule<T>` 对象的列表。这些方法使用反射从 `T` 的项中获取属性值以及每个规则中的属性 `Property`，并将该属性与每个规则对象的 `Value` 属性中的值进行比较。因此，本质上，你从对象（类型为 `T`）的属性中获取给定值，使用反射获取规则对象指定的属性属性值，并将其与规则对象提供的另一个属性值进行比较。

# C# 初学者教程

传递到方法的 `List<BusinessRule<T>>` 集合中的每个规则对象都将被分别评估，所有规则的加权结果将决定 `EvaluateRules<T>` 方法返回成功（`true`）还是失败（`false`）。

为了实现此功能，你需要添加两个类和一个枚举（`enum`）。

枚举：名为 `RuleOperator` 的枚举将定义 `EvaluateRules<T>` 方法在评估规则时可以进行的不同比较类型。每个规则对象都将有一个属性，用于指定要比较的属性值以及要比较的指定值。你将添加的运算符有：`GreaterThan`（大于）、`LessThan`（小于）、`Equal`（等于）、`NotEqual`（不等于）、`Contains`（包含）和 `NotContains`（不包含）；最后两个值将用于检查列表是否包含某个值。

`BusinessRule<T>` 类：第一个类是泛型公共 `BusinessRule<T>` 类，它将为给定类型 `T` 的项定义单个规则。该类具有以下公共属性：

- 一个名为 `Property` 的字符串属性，它存储项中你想要与第二个对象属性 `Value` 进行比较的属性名称。
- 第三个属性是名为 `Items` 的 `IEnumerable<T>`，它是与规则评估类型相同的项的列表；该方法扫描集合中的所有项，以确定规则是否成功。
- 第四个是名为 `Comparator` 的 `RuleOperator` 属性，它包含来自 `RuleOperator` 枚举的值之一，它将决定如何比较这两个值。
- 最后一个属性是可空布尔类型 (`bool?`) `Success`；在规则被评估之前它为 `null`；如果 `EvaluateRules<T>` 对该规则返回成功则为 `true`，如果评估不成功或失败则为 `false`。

`RuleComparator` 类：`RuleComparator` 实例将针对类型为 `T` 的项评估 `BusinessRule<T>` 规则列表。为了使用标准运算符（如 `<` `>`）比较对象值，该类必须实现 `IComparer` 接口。.NET 框架提供了一些比较器类供你使用，如果你不想自己实现的话；这里使用的是 `CaseInsensitiveComparer`，它适用于字符串值。`IComparer` 实现的 `Compare` 方法返回一个整数，负值表示第一个对象的值小于第二个对象的值，零表示相等，正值表示第一个对象的值大于第二个对象的值。由于此特定的比较器可以比较双精度数值和字符串，因此你需要创建两种场景：一种是比较解析双精度的值，另一种是作为字符串比较。你可以使用创建的相同 `ISNumeric` 方法来检查值是否为数值。

该类将具有三个方法，第一个名为 `ISNumeric`，用于检查对象值是否为数值并根据结果返回 `true` 或 `false`。第二个 `int` 方法名为 `Compare`，拥有两个对象 `value1` 和 `value2`，属于 `IComparer` 接口；第三个方法名为 `EvaluateRules<T>`，接受一个 `T` 参数 `item` 和一个 `List<BusinessRule<T>>` 参数 `rules`。该方法的目的是遍历集合中的规则，并根据传入的 `T` 对象中的给定属性对每个规则进行评估。你可以阅读此用例开头的方法。定义定义规则：你通过在表单的方法中创建 `List<BusinessRule<T>>` 集合来定义规则，并将其传递给处理器以评估其方法之一，例如你在另一个用例中创建的通用 `Add` 方法。所有规则都必须成功，评估才被视为成功。

```csharp
// 创建供处理器评估的规则
var rules = new List<BusinessRule<ICustomer>>() {
    new BusinessRule<ICustomer> {
        Property = "Id", Value = 1, Comparer = RuleOperator.LessThan
    },
    new BusinessRule<ICustomer> { 
        Property = "SocialSecurityNumber",
        Items = processor.GetICustomer(),
        Comparer = RuleOperator.NotContains
    }
};
```

```csharp
// 将规则集合传递给 Add 方法
var success = processor.Add(customer, rules);
```

# C# 入门

`BusinessRule<T>` 类将实现 `RuleOperator` 枚举和 `BusinessRule<T>` 类；为了简单起见，它们将放在 `.cs` 文件夹中；如果你需要，也可以将其放在单独的文件中。

1. 创建 Car Rental 解决方案的副本，以便在出现问题时可以返回初始点。
2. 打开 Car Rental 解决方案。
3. 在业务层（Business Layer）项目的 `Classes` 文件夹中添加一个名为 `BusinessRule` 的类。
4. 将类的访问性更改为 `public`。
5. 将其泛型化为 `T`。

```csharp
public class BusinessRule<T>
```

6. 在类上方、命名空间内部添加一个名为 `RuleOperator` 的公共枚举。
7. 为该枚举添加以下值：`GreaterThan`, `LessThan`, `Equal`, `NotEqual`, `Contains`, `NotContains`。
8. 为该类添加以下公共属性：`string` 类型的 `Property`、`object` 类型的 `Value`、`IEnumerable<T>` 类型的 `Items`、`RuleOperator` 类型的 `Comparer` 以及 `bool?`（可空 `bool`）类型的 `Success`。

`BusinessRule` 类和 `RuleOperator` 枚举的完整代码：

```csharp
public enum RuleOperator
{
    GreaterThan,
    LessThan,
    Equal,
    NotEqual,
    Contains,
    NotContains
}

public class BusinessRule<T>
{
    public string Property { get; set; }
    public object Value { get; set; }
    public IEnumerable<T> Items { get; set; }
    public RuleOperator Comparer { get; set; }
    public bool? Success { get; set; }
}
```

# RuleComparer 类

此类中方法的目的是评估传入的类型为 `BusinessRule<T>` 的业务规则。

# Compare 方法

1. 在业务层（Business Layer）项目的 `Classes` 文件夹中添加一个名为 `RuleComparer` 的类。
2. 在类中实现 `IComparer` 接口。这将添加一个名为 `Compare` 的方法，该方法接受两个对象数据类型的参数，并对它们进行相互比较。
3. 为了能够在 `Compare` 方法中评估值，你需要添加一个名为 `IsNumeric` 的方法，用于检查对象值是否为数值。你已经在表单中创建了这个方法，因此只需将其复制并粘贴到 `RuleComparer` 类中。
4. 在 `Compare` 方法中使用 `IsNumeric` 方法来确定方法定义的 `value1` 和 `value2` 参数值是否为数值。
5. 如果两个值都是数值，在将它们发送到 `CaseInsensitiveComparer` 的 `Compare` 方法比较之前，将它们解析为 `double` 数据类型。

```csharp
if (IsNumeric(value1) && IsNumeric(value2))
    return ((new CaseInsensitiveComparer()).Compare(
        Double.Parse(value1.ToString()),
        Double.Parse(value2.ToString())
    ));
```

如果值不是数值，则在不解析值的情况下调用 `CaseInsensitiveComparer` 的 `Compare` 方法。
