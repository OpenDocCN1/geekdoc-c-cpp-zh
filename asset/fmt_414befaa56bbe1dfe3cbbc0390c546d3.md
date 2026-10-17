
```csharp
public int Age { get; set; }
}
List<Person> personnel = new List<Person>();
new Person() { ID = 1, Name = "John", Age = 53 },
new Person() { ID = 2, Name = "Sid", Age = 28 },
new Person() { ID = 3, Name = "Fred", Age = 34 },
```

（注：原始文本中存在大量重复和断裂的代码片段，已根据语义进行了逻辑合并与纠错）

```csharp
public MainPage() {
    ...
    this.auditor = new Auditor();
    this.shipper = new Shipper();
    this.checkoutController = new CheckoutController();
}
```

```csharp
public MainPage()
{
    ...
    this.checkoutController = new CheckoutController();
    this.checkoutController.CheckoutProcessing += this.auditor.AuditOrder;
    this.checkoutController.CheckoutProcessing += this.shipper.ShipOrder;
}
```

```csharp
private void CheckoutButtonClick(object sender, RoutedEventArgs e)
{
    try
    {
        // 执行结账处理
        this.checkoutController.StartCheckoutProcessing(this.order);
        // 显示订单摘要
    }
    ...
}
```

```csharp
this.stopMachinery += folder.StopFolding;
void StopFolding(int shutDownTime); // 在指定的秒数后关闭
void FinishFolding(0)
{
    folder.StopFolding(0); // 立即关闭
    this.stopMachinery += folder.FinishFolding;
    this.stopMachinery += ((Q) => folder.StopFolding(0));
}
event delegateTypeName eventName;
class TemperatureMonitor
{
    public delegate void StopMachineryDelegate();
    ...
}
```

```csharp
class TemperatureMonitor
{
    public delegate void StopMachineryDelegate();
    public event StopMachineryDelegate MachineOverheating;
}
```

```csharp
class TemperatureMonitor
{
    public delegate void StopMachineryDelegate();
    public delegate event StopMachineryDelegate MachineOverheating;
    ...
}
TemperatureMonitor tempMonitor = new TemperatureMonitor();
tempMonitor.MachineOverheating += () => { folder.StopFolding(0); };
tempMonitor.MachineOverheating += welder.FinishWelding;
tempMonitor.MachineOverheating += painter.PaintOff;
class TemperatureMonitor
{
    public delegate void StopMachineryDelegate();
    public delegate event StopMachineryDelegate MachineOverheating;
    ...
    private void Notify()
    {
        if (this.MachineOverheating != null)
        {
            this.MachineOverheating();
        }
    }
}
...
public delegate void RoutedEventHandler(Object sender, RoutedEventArgs e);
public class ButtonButtonBase: ...
{
    public event RoutedEventHandler Click;
    ...
}
public class Button: ButtonBase
{
    ...
}
```

```csharp
partial class MainPage : 
global::Windows.UI.Xaml.Controls.Page,
global::Windows.UI.Xaml.Markup.IComponentConnector,
global::Windows.UI.Xaml.Markup.IComponentConnector
{
    public void Connect(int connectionId, object target)
    {
        switch(connectionId)
        {
            case 1:
                {
                    this.okay = (global::Windows.UI.Xaml.Controls.Button)(target);
                    ...
                    ((global::Windows.UI.Xaml.Controls.Button)this.okay).Click += this.okayClick;
                }
                break;
            default:
                break;
        }
        this._contentLoaded = true;
    }
    public sealed partial class MainPage : Page
    {
        private void okayClick(object sender, RoutedEventArgs e)
        {
            // 你的处理 Click 事件的代码
        }
        private void CheckoutButtonClicked(object sender, RoutedEventArgs e)
        {
            try
            {
                // 执行结账处理
                this.checkoutController.StartCheckoutProcessing(this.order);
                // 显示订单摘要
                MessageDialog dlg = new MessageDialog(...);
                dlg.ShowAsync();
            }
        }
    }
}
```

```csharp
public class Auditor
{
    public delegate void AuditingCompleteDelegate(string message);
    ...
}
public class Auditor
{
    public delegate void AuditingCompleteDelegate(string message);
    public event AuditingCompleteDelegate AuditProcessingComplete;
    ...
    public void AuditOrder(Order order)
    {
        this.doAuditing(order);
    }
}
private async void doAuditing(Order order)
{
    List<OrderItem> ageRestrictedItems = findAgeRestrictedItems(order);
    if (ageRestrictedItems != null)
    {
        ...
    }
    if (AuditProcessingComplete != null)
    {
        AuditProcessingComplete("Processing complete");
    }
}
}
```

```csharp
public class Shipper
{
    public delegate void ShippingCompleteDelegate(string message);
    ...
}
```

```csharp
var customers = new[]
{
    new { CustomerID = 1, FirstName = "Kim", LastName = "Abercrombie", CompanyName = "Alpine Ski House" },
    new { CustomerID = 2, FirstName = "Jeff", LastName = "Hay", CompanyName = "Coho Winery" },
    new { CustomerID = 3, FirstName = "Charlie", LastName = "Herb", CompanyName = "Alpine Ski House" },
    new { CustomerID = 4, FirstName = "Chris", LastName = "Preston", CompanyName = "Trey Research" },
    new { CustomerID = 5, FirstName = "Dave", LastName = "Barnett", CompanyName = "Wingtip Toys" },
    new { CustomerID = 6, FirstName = "Ann", LastName = "Beebee", CompanyName = "Coho Winery" },
    new { CustomerID = 7, FirstName = "John", LastName = "Kane", CompanyName = "Wingtip Toys" },
    new { CustomerID = 8, FirstName = "David", LastName = "Simpson", CompanyName = "Trey Research" },
    new { CustomerID = 9, FirstName = "Greg", LastName = "Chapman", CompanyName = "Wingtip Toys" },
    new { CustomerID = 10, FirstName = "Tim", LastName = "Litton", CompanyName = "Wide World Importers" }
};

var addresses = new[]
{
    new { CompanyName = "Alpine Ski House", City = "Berne", Country = "Switzerland" },
    new { CompanyName = "Coho Winery", City = "San Francisco", Country = "United States" },
    new { CompanyName = "Trey Research", City = "New York", Country = "United States" },
    new { CompanyName = "Wingtip Toys", City = "London", Country = "United Kingdom" },
    new { CompanyName = "Wide World Importers", City = "Tetbury", Country = "United Kingdom" }
};

IEnumerable<string> customerFirstNames = customers.Select(cust => cust.FirstName);
foreach (string name in customerFirstNames)
{
    Console.WriteLine(name);
}
```

Kim
Jeff
Charlie
Chris
Dave
Ann
David
Greg
Tim

```csharp
public static IEnumerable<TResult> Select<TSource, TResult>
```

```csharp
IEnumerable<string> companyNames = addresses
  .OrderBy(addr => addr.CompanyName)
  .Select(comp => comp.CompanyName);
```

```csharp
foreach (string name in companyNames)
{
    Console.WriteLine(name);
}
var companiesGroupedByCountry = addresses
  .GroupBy(addr => addr.Country);
```

```csharp
foreach (var companiesPerCountry in companiesGroupedByCountry)
{
    Console.WriteLine($"Country: {companiesPerCountry.Key}\t{companiesPerCountry.Count()} companies");
}
foreach (var company in companiesPerCountry)
{
    Console.WriteLine($"Country: {company.CompanyName}");
}
```

Country: Switzerland 1 companies
Alpine Ski House
Country: United States 2 companies
Coho Winery
Trey Research
Country: United Kingdom 2 companies
Wingtip Toys
Wide World Importers

```csharp
int numberOfCompanies = addresses
  .Select(addr => addr.CompanyName).Count();
Console.WriteLine($"Number of companies: {numberOfCompanies}");
int numberOfDistinctCountries = addresses
  .Select(addr => addr.Country).Distinct().Count();
Console.WriteLine($"Number of distinct countries: {numberOfDistinctCountries}");
```

```csharp
var companiesAndCustomers = customers
  .Select(c => new { c.FirstName, c.LastName, c.CompanyName })
  .Join(addresses, custs => custs.CompanyName, addrs => addrs.Country, (custs, addrs) => new { custs.FirstName, custs.LastName, addrs.Country });
```

```csharp
foreach (var row in companiesAndCustomers)
{
    Console.WriteLine(row);
}
```
