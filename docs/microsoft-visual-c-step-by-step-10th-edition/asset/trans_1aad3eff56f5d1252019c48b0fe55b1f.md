
```csharp
private void CheckoutButtonClicked(object sender, RoutedEventArgs e)
{
    try
    {
        // 执行结账处理
        this.checkoutController.StartCheckoutProcessing(this.order);
        // 此处为被删除的代码
        // 清空订单详情，以便用户可以开始新订单
        this.order = new Order
        {
            Date = DateTime.Now,
            Items = new List<OrderItem>(),
            OrderID = Guid.NewGuid(),
            TotalValue = 0
        };
        this.orderDetails.DataContext = null;
        this.orderValue.Header = `$${order.TotalValue:C}`;
        this.listListView.Visibility = Visibility.Collapsed;
        this.checkout.IsEnabled = false;
    }
    catch (Exception ex)
    {
        ...
    }
}
```

```csharp
private void displayMessage(string message)
{
    this.messageBar.Text += $" {message}{Environment.NewLine}";
}
```

```csharp
public MainPage()
{
    ...	this.auditor = new Auditor();
    this.shipper = new Shipper();
    this.checkoutController = new CheckoutController();
    this.checkoutController.CheckoutProcessing += this.auditor.AuditOrder;
    this.checkoutController.CheckoutProcessing += this.shipper.ShipOrder;
    this.auditor.AuditProcessingComplete += this.displayMessage;
    this.shipper.ShipProcessingComplete += this.displayMessage;
}
```

```csharp
delegate void myDelegate();
private void myMethod() { ... }
...
myDelegate del = new myDelegate(this.myMethod);
```

```csharp
class MyClass
{
    public delegate void MyDelegate();
    ...
    public event mydelegate MyEvent;
}
```

```csharp
class MyEventHandlingClass
{
    private MyClass myClass = new MyClass();
    ...
    public void Start()
    {
        myClass.MyEvent +=
            new MyClass.MyDelegate (this.eventHandlingMethod);
    }
    private void eventHandlingMethod()
    {
        ...
    }
}
```

```csharp
public void Start()
{
    myClass.MyEvent +=
        this.eventHandlingMethod;
}
```

```csharp
class MyEventHandlingClass
{
    private MyClass myClass = new MyClass();
    ....
    public void Stop()
    {
        myClass.MyEvent -=
        new myClass.MyDelegate (this.eventHandlingMethod);
    }
    ....
}
```

```csharp
public void Stop()
{
    myClass.MyEvent -= this.eventHandlingMethod;
}
```

```csharp
class MyClass
{
    public event mydelegate MyEvent;
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
```

```csharp
var customers = new[] {
    new { CustomerID = 1, FirstName = "Kim", LastName = "Abercrombie",
        CompanyName = "Alpine Ski House" },
    new { CustomerID = 2, FirstName = "Jeff", LastName = "May",
        CompanyName = "Coho Winery" },
    new { CustomerID = 3, FirstName = "Charlie", LastName = "Herb",
        CompanyName = "Alpine Ski House" },
    new { CustomerID = 4, FirstName = "Chris", LastName = "Preston",
        CompanyName = "Trey Research" },
    new { CustomerID = 5, FirstName = "Dave", LastName = "Barnett",
        CompanyName = "Wingtip Toys" },
    new { CustomerID = 6, FirstName = "Ann", LastName = "Beebe",
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
    new { CompanyName = "Wingtip Toys", City = "London",
        Country = "United Kingdom" },

    new { CompanyName = "Wide World Importers", City = "Tetbury",
        Country = "United Kingdom" }
};
```

```csharp
IEnumerable<string> customerFirstNames =
    customers.Select(cust => cust.FirstName);
foreach (string name in customerFirstNames)
{
    Console.WriteLine(name);
}
```
