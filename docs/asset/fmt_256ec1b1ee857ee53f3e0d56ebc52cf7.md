
```
public sealed partial class MainPage : Page
{
    ...
    private void okayClick(object sender, RoutedEventArgs e)
    {
        // your code to handle the Click event
    }
}
```

```
private void CheckoutButtonClicked(object sender, RoutedEventArgs e)
{
    try
    {
        // Perform the checkout processing
        this.checkoutController.StartCheckoutProcessing(this.order);

        // Display a summary of the order
        MessageDialog dlg = new MessageDialog(...);
        dlg.ShowAsync();
        ...
    }
    ...
}
```

```
class Auditor
{
    public delegate void AuditingCompleteDelegate(string message);
    ...
}
```

```
class Auditor
{
    public delegate void AuditingCompleteDelegate(string message);
    public event AuditingCompleteDelegate AuditProcessingComplete;
    ...
}
```

```
public void AuditOrder(Order order)
{
    this.doAuditing(order);
}
```

```
private async void doAuditing(Order order)
{
    List<OrderItem> ageRestrictedItems = findAgeRestrictedItems(order);
    if (ageRestrictedItems.Count > 0)
    {
        try
        {
            ...
        }
        catch (Exception ex)
        {
            ...
        }
        finally
        {
            if (this.AuditProcessingComplete != null)
            {
                this.AuditProcessingComplete(
                    $"Audit record written for Order {order.OrderID}");
            }
        }
    }
}
```

```
class Shipper
{
    public delegate void ShippingCompleteDelegate(string message);
    ...
}
```

```
class Shipper
{
    public delegate void ShippingCompleteDelegate(string message);
    public event ShippingCompleteDelegate ShipProcessingComplete;
    ...
}
```

```
private async void doShipping(Order order)
{
    try
    {
        ...
    }
    catch (Exception ex)
    {
        ...
    }
    finally
    {
        if (this.ShipProcessingComplete != null)
        {
            this.ShipProcessingComplete(
                $"Dispatch note generated for Order {order.OrderID}");
        }
    }
}
```

```
<Grid Background="{StaticResource ApplicationPageBackgroundThemeBrush}">

    <Grid Margin="12,0,12,0" Loaded="MainPageLoaded">

        <Grid.RowDefinitions>

            <RowDefinition Height="*"/>

            <RowDefinition Height="2*"/>

            <RowDefinition Height="*"/>

            <RowDefinition Height="10*"/>

            <RowDefinition Height="*"/>

        </Grid.RowDefinitions>

        ...
```

```
<Grid.RowDefinitions>

    ...

    <RowDefinition Height="10*"/>

    <RowDefinition Height="2*"/>

</Grid.RowDefinitions>
```

```
...

</Grid>

<ScrollViewer Grid.Row="4" VerticalScrollBarVisibility="Visible">

    <TextBlock x:Name="messageBar" FontSize="18" />

</ScrollViewer>

</Grid>

</Grid>

</Page>
```

```
private void CheckoutButtonClicked(object sender, RoutedEventArgs e)
{
    try
    {
        // Perform the checkout processing
        this.checkoutController.StartCheckoutProcessing(this.order);

        // Clear out the order details so the user can start again with a new order
        this.order = new Order { Date = DateTime.Now, Items = new List<OrderItem>(),
                        OrderID = Guid.NewGuid(), TotalValue = 0 };
        this.orderDetails.DataContext = null;
        this.orderValue.Text = $"{order.TotalValue:C}";
        this.listViewHeader.Visibility = Visibility.Collapsed;
        this.checkout.IsEnabled = false;
    }
    catch (Exception ex)
    {
        ...
    }
}
```

```
private void displayMessage(string message)
{
    this.messageBar.Text += message + "\n";
}
```

```
public MainPage()
{
    ...
    this.auditor = new Auditor();
    this.shipper = new Shipper();
    this.checkoutController = new CheckoutController();
    this.checkoutController.CheckoutProcessing += this.auditor.AuditOrder
    this.checkoutController.CheckoutProcessing += this.shipper.ShipOrder;
    this.auditor.AuditProcessingComplete += this.displayMessage;
    this.shipper.ShipProcessingComplete += this.displayMessage;
}
```

```
var customers = new[] {
    new { CustomerID = 1, FirstName = "Kim", LastName = "Abercrombie",
        CompanyName = "Alpine Ski House" },
    new { CustomerID = 2, FirstName = "Jeff", LastName = "Hay",
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
        Country = "Switzerland"},
    new { CompanyName = "Coho Winery", City = "San Francisco",
        Country = "United States"},
    new { CompanyName = "Trey Research", City = "New York",
        Country = "United States"},
    new { CompanyName = "Wingtip Toys", City = "London",
        Country = "United Kingdom"},
    new { CompanyName = "Wide World Importers", City = "Tetbury",
        Country = "United Kingdom"}
};
```

```
IEnumerable<string> customerFirstNames =
    customers.Select(cust => cust.FirstName);
foreach (string name in customerFirstNames)
{
    Console.WriteLine(name);
}
```

```
public static IEnumerable<TResult> Select<TSource, TResult> (
    this IEnumerable<TSource> source,
    Func<TSource, TResult> selector
)
```

```
IEnumerable<string> customerNames =
    customers.Select(cust => $"{cust.FirstName} {cust.LastName}");
```

```
class FullName
{
    public string FirstName{ get; set; }
    public string LastName{ get; set; }
}
...
IEnumerable<FullName> customerNames =
    customers.Select(cust => new FullName
    {
        FirstName = cust.FirstName,
        LastName = cust.LastName
    });
```

```
var customerNames =
    customers.Select(cust => new { FirstName = cust.FirstName, LastName = cust.LastName });
```

```
IEnumerable<string> usCompanies =
    addresses.Where(addr => String.Equals(addr.Country, "United States"))
        .Select(usComp => usComp.CompanyName);
foreach (string name in usCompanies)
{
    Console.WriteLine(name);
}
```

```
IEnumerable<string> companyNames =
    addresses.OrderBy(addr => addr.CompanyName).Select(comp => comp.CompanyName);
foreach (string name in companyNames)
{
    Console.WriteLine(name);
}
```

```
var companiesGroupedByCountry =
    addresses.GroupBy(addrs => addrs.Country);
foreach (var companiesPerCountry in companiesGroupedByCountry)
{
    Console.WriteLine(
        $"Country: {companiesPerCountry.Key}\t{companiesPerCountry.Count()} companies");
    foreach (var companies in companiesPerCountry)
    {
        Console.WriteLine($"\t{companies.CompanyName}");
    }
}
```

```
国家: Switzerland  1 家公司

Alpine Ski House

国家: United States  2 家公司

Coho Winery

Trey Research

国家: United Kingdom 2 家公司

Wingtip Toys

Wide World Importers
```

```
int numberOfCompanies = addresses.Select(addr => addr.CompanyName).Count();

Console.WriteLine($"Number of companies: {numberOfCompanies}");
```

```
int numberOfCountries = addresses.Select(addr => addr.Country).Count();

Console.WriteLine($"Number of countries: {numberOfCountries}");
```

```
int numberOfCountries =
    addresses.Select(addr => addr.Country).Distinct().Count();
```
