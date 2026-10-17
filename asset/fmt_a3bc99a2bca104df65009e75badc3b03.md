
此更改为表单底部留出了空间。你将使用此空间来显示来自 `Auditor` 和 `Shipper` 组件引发事件时收到的消息。第 25 章“为通用 Windows平台应用实现用户界面”提供了有关使用 `Grid` 控件布局用户界面的更多细节。

14. 滚动到 XAML 格底部，在倒数第二个 `</Grid>` 标签之前添加**粗体**所示的 `ScrollView` 和 `TextBlock` 元素：

点击此处查看图像

```
...
  <ScrollView Grid.Row="4"
  VerticalScrollBarVisibility="Visible">
    <TextBlock x:Name="messageBar" FontSize="18" />
  </ScrollView>
</Grid>
```

此标记在屏幕底部添加了 `TextBlock`。你将使用它来显示 `Auditor` 和 `Shipper` 组件引发事件时收到的消息。

15. 在代码和文本编辑器中显示 `MainPage.xaml.cs` 文件。然后找到 `CheckoutButtonClicked` 方法，移除如下**粗体**所示的 `try` 块（注：此处为描述逻辑）：

```
private void CheckoutButtonClicked(object sender, RoutedEventArgs e)
try {
    // 执行结账处理
    this.checkoutController.StartCheckout(this.order);
    // 清空订单详情以便再次结账
    this.order = new Order
    {
        Date = DateTime.Now,
        Items = new List<OrderItem>(),
        OrderID = Guid.NewGuid(),
        TotalValue = 0
    }
this.orderDetails = null;
```

16. 在 `MainPage` 类中添加一个名为 `displayMessage` 的私有方法。该方法接受一个 `string` 参数并返回 `void`。在方法体中，添加一条语句将 `message` 参数追加到 `messageBar` 控件的 `Text` 属性，并紧跟一个换行符，如下**粗体**所示：

点击此处查看代码图像

```
private void displayMessage(string message)
{
    this.messageBar.Text += message + Environment.NewLine;
}
```

此代码将消息显示在表单底部区域。

17. 找到 `MainPage` 类的构造函数，添加如下**粗体**所示的代码：

```
public MainPage()
{
    this.auditor = new Auditor();
    this.shipper = new Shipper();
    this.checkoutController = new CheckoutController();
    this.auditor.AuditOrder +=;
    this.checkoutController.CheckoutProcessing +=;
    this.auditor.AuditProcessingComplete += this.displayMessage;
    this.shipper.ShipProcessingComplete += this.displayMessage;
}
```

这些语句订阅了 `Auditor` 和 `Shipper` 的事件。当事件引发时，会运行 `displayMessage` 方法。注意同一个方法处理了两个事件。

18. 在“调试”菜单中选择“启动”以编译并运行应用程序。

19. 当宽导入器出现时，选择某些项目（至少一个受年龄限制），然后选择“结账”。

20. 验证“审计记录已写入”消息出现在表单底部，随后是“生成发货单”消息。

# 导入器

| 锤子 | 名称：电锯 | 订单详情 |
|---|---|---|
| 24盎司重型羊角锤 | 描述：旋转动作，高功率 | |
| £18.35 | 价格：£88.00 | |
| 否 | 限制：是 | |
| | 总计：£0.00 | |
| | | 结账 |

Audit record written for Order 24975f99-cddf-4521-850d-2547ccde33
Dispatch note generated for Order 24975f99-cddf-4521-850d-2547ccde33

21. 再次放置订单并注意每次选择“结账”时出现的新消息。当消息区域填满时，你可能需要向下滚动。

22. 完成后，返回 Visual Studio 2022 并停止调试。

## 总结

在本章中，你学习了如何使用委托来引用并调用方法。你还了解了如何使用委托定义可以运行的 Lambda 表达式。最后，你学习了如何定义和使用事件来触发方法的执行。

- 如果你想继续下一章，请保持 Visual Studio 2022 运行并转到第 21 章。

• 如果你现在想退出 Visual Studio 2022，请在“文件”菜单上选择“退出”。如果看到“保存”对话框，选择“是”并保存项目。

## 快速参考

| 目标 | 执行此操作 |
|---|---|
| 声明委托类型 | 编写关键字 `delegate`，紧接着是返回类型，然后是委托类型的名称，最后是任何参数类型。例如：

```csharp
delegate void myDelegate();
``` |
| 创建一个用单个特定方法初始化的委托实例 | 使用与类或结构体相同的语法：编写关键字:`new`，紧接着是类型的名称（即委托的名称），然后是括号中的参数。该参数必须是一个签名与委托签名完全匹配的方法。例如：
[点击此处查看代码图像](#)

```csharp
delegate void myDelegate();
private void myFunction() { ... }
delegate del = new myDelegate(this.myMethod);
``` |
| 调用委托 | 使用与方法调用相同的语法。例如：

```csharp
delegate del;
...
del();
``` |
| 声明事件 | 编写关键字 `event`，紧接着是类型的名称（该类型必须是委托类型），然后是事件的名称。例如：

[点击此处查看代码图像](#)

```csharp
class MyClass {
    public delegate void MyDelegate();
    ...
    public event myDelegate MyEvent;
}
``` |
| 订阅事件 | 创建一个委托实例（与事件类型相同），并使用 `+=` 运算符将委托实例附加到事件上。例如：
[点击此处查看代码图像](#)
```csharp
class MyEventHandlingClass {
    private MyClass myClass = new MyClass();
    ...
    public void Start() {
        myClass.MyEvent += new MyClass.MyDelegate(this.eventHandlingMethod);
    }
    private void eventHandlingMethod() {
        ...
    }
}
```
你也可以通过直接指定订阅方法让编译器自动生成新委托：
[点击此处查看代码图像](#)
```csharp
public void Start() {
    myClass.MyEvent += this.eventHandlingMethod;
}
``` |
| 取消订阅事件 | 创建一个委托实例（与事件类型相同），并使用 `-=` 运算符将其从事件中分离出。例如：

[点击此处查看代码图像](#)
```java
class MyEventHandlerClass {
    private MyClass myClass = new MyClass();
    ...
    public void Stop() {
        myClass.MyEvent -=
            new MyClass.MyDelegate(
                (this.eventHandlingMethod);
    }
    ...
}
```
或者：
[点击此处查看代码图像](#)
```java
public void Stop() {
    myClass.MyEvent -=
        this.eventHandlingMethod;
}
``` |
| 触发事件 | 使用与方法调用相同的语法。你必须提供与事件引用的委托所需的类型匹配的参数。不要忘记检查事件是否为空。例如：

点击此处查看代码图像

```csharp
class MyClass
{
    public event myDelegate MyEvent;
    ...
    private void RaiseEvent()
    {
        if (this.MyEvent is not null)
        {
            this.MyEvent();
        }
    }
    ...
}
``` |

## 第 21 章

## 使用查询表达式查询内存数据

完成本章后，你将能够：

- 定义语言集成查询 (LINQ) 查询以检查可枚举集合的内容。
- 使用 LINQ 扩展方法和查询运算符。
- 解释 LINQ 如何延迟执行查询，以及你如何强制立即执行并缓存 LINQ 查询的结果。

你现在已经掌握了 C# 语言的大部分功能。然而，到目前，我略过了该语言的一个重要方面，而该方面可能会被许多应用程序使用：C# 为查询数据提供的支持。

你已经看到定义结构和类来为数据建模，并使用集合和数组在内存中临时存储数据。但是，如何执行常见任务，例如在集合中搜索符合特定标准组的项目呢？例如，如果你有一个 `Customer` 对象集合，如何找到所有位于纽约的客户，或者哪个小镇获得过你服务的客户最多？你可以编写代码来遍历集合并检查每个对象的字段，但这类任务发生得非常频繁，以至于 C# 的设计者决定在语言中包含这些特性以减少你需要编写的代码量。在本章中，你将学习如何使用这些高级 C# 语言特性来查询和操纵数据。

## 什么是 LINQ？

除了最简单的应用程序外，所有应用程序都需要处理数据。在历史上，大多数应用程序都提供自己的逻辑来执行这些操作。

然而，这种策略会导致应用程序中的代码与其处理的数据结构变得紧密耦合。如果数据结构发生变化，你可能需要对处理数据的代码进行大量修改。.NET 框架的设计者对这个问题进行了深思熟虑。他们最终决定通过提供抽象应用程序用于查询数据机制的特性，来让应用程序开发者的生活更轻松。这些特性统称为语言集成查询，或 LINQ。LINQ 的创建者直言不讳地审视了 SQL Server 等关系型数据库系统如何向数据库管理系统发出结构化查询语言 (SQL)语句。SQL 提供了开发者想要检索的数据的高级描述，但没有具体指示数据库管理系统应该如何检索这些数据。这些细节由数据库管理系统控制。因此，调用 SQL 语句的应用程序并不关心数据库管理系统如何存储或检索数据。数据库管理系统使用的格式可以更改（例如，当发布新版本时），而无需应用程序开发人员修改应用程序使用的 SQL 语句。LINQ 提供的语法和语义与 SQL 非常相似，并具有许多相同的优点。你可以更改被查询数据的底层结构，而无需更改实际执行查询的代码。尽管 LINQ 看起来像 SQL，但它灵活灵活，并且可以处理更广泛的逻辑数据结构。例如，LINQ 可以处理分级数据，例如 XML 文档中的数据。然而，本章将集中在 C# 应用程序中使用 LINQ。

解释如何使用支持 LINQ 的 C# 特性的最简单方法，是根据以下组客户和地址信息通过一些简单的示例：

## 客户信息

| CustomerID | FirstName | LastName | CompanyName |
|---|---|---|---|
| 1 | Kim | Abercrombie | Alpine Ski House |
| 2 | Jeff | Hay | Coho Winery |
| 3 | Charlie | Herb | Alpine Ski House |
| 4 | Chris | Preston | Trey Research |
| 5 | Dave | Barnett | Wingtip Toys |
| 6 | Ann | Beebee | Coho Winery |
| 7 | John | Kane | Wingtip Toys |
| 8 | David | Simpson | Trey Research |
| 9 | Greg | Chapman | Wingtip Toys |
| 10 | Tim | Litton | Wide World Importers |

## 地址信息

| CompanyName | City | Country |
|---|---|---|
| Alpine Ski House | Berne | Switzerland |
| Coho Winery | San Francisco | United States |
| Trey Research | New York | United States |
| Wingtip Toys | London | United Kingdom |
| Wide World Importers | Tetbury | United Kingdom |

LINQ 要求数据存储在实现了 `IEnumerable` 或 `IEnumerable<T>` 接口的数据结构中，如第 19 章所述。

“枚举集合。”无论你使用什么数据结构（数组、HashSet<T>、Queue<T> 或任何其他集合类型，甚至是你自己定义的类型），只要它是可枚举的即可。然而，为了保持简单，本章中的示例假设客户信息和地址信息存储在以下代码示例所示 `customers` 和 `addresses` 数组中。

### 注意

在现实应用中，你将通过从文件或数据库读取数据来填充这些数组。

点击查看代码图像

```csharp
var customers = new[] {
    new { CustomerID = 1, FirstName = "Kim", LastName = "Abercromie",
        CompanyName = "Alpine Sky House" },
    new { CustomerID = 2, FirstName = "Jeff", LastName = "Hay",
        CompanyName = "Coho Winery" },
    new { CustomerID = 3, FirstName = "Charlie", LastName = "Herb",
        CompanyName = "Alpine Sky House" },
    new { CustomerID = 4, FirstName = "Chris", LastName = "Preston",
        CompanyName = "Trey Research" },
    new { CustomerID = 5, FirstName = "Dave", LastName = "Barnett",
        CompanyName = "Wingtip Toys" },
    new { CustomerID = 6, FirstName = "Ann", LastName = "Beebee",
        CompanyName = "Coho Winery" },
    new { CustomerID = 7, FirstName = "John", LastName = "Kane",
        CompanyName = "Wingtip Toys" },
    new { CustomerID = 8, FirstName = "David", LastName = "Simpson",
        CompanyName = "Trey Research" },
    new { CustomerID = 9, FirstName = "Greg", LastName = "Chapman",
        CompanyName = "Wingtip Toys" },
    new { CustomerID = 10, FirstName = "Tim", LastName = "Litton", 
        CompanyName = "Wide World Importers" }
};

var addresses = new[] {
    new { CompanyName = "Alpine Ski House", City = "Berne",
        Country = "Switzerland" },
    new { CompanyName = "Coho Winery", City = "San Francisco",
        Country = "United States" },
    new { CompanyName = "Trey Research", City = "New York",
        Country = "United States" },
