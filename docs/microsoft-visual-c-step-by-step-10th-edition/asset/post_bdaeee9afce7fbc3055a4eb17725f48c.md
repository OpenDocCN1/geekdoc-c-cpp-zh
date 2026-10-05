
```csharp
public async Task<ActionResult<IEnumerable<CustomerModel>>> FindCustomers(
    string title = "%", string firstName = "%", string lastName = "%",
    string email = "%", string phone = "%")
{
    var query = from c in _context.Customers
        where EF.Functions.Like(c.Title, title) &&
        EF.Functions.Like(c.FirstName, firstName) &&
        EF.Functions.Like(c.LastName, lastName) &&
        EF.Functions.Like(c.EmailAddress, email) &&
        EF.Functions.Like(c.Phone, phone)
        select c;

    return await query.ToListAsync();
}
```

```csharp
private bool _isBusy;
public bool IsBusy
{
    get => this._isBusy;
    set
    {
        this._isBusy = value;
        this.OnPropertyChanged(nameof(IsBusy));
    }
}

private string _lastError = null;
public string LastError
{
    get => this._lastError;
    private set
    {
        this._lastError = value;
        this.OnPropertyChanged(nameof(LastError));
    }
}
```

```csharp
private List<Customer> customers;
public int CustomerCount { get => customers is null ? 0 : customers.Count; }
private int currentCustomer;
public int CurrentCustomerIndex { get => currentCustomer + 1; }
```

```csharp
private void Next()
{
    if (this.customers.Count - 1 > this.currentCustomer)
    {
        this.currentCustomer++;
        this.OnPropertyChanged(nameof(Current));
        this.OnPropertyChanged(nameof(CurrentCustomerIndex));
        ...
    }
}
```

```csharp
private void Previous()
{
    if (this.currentCustomer > 0)
    {
        this.currentCustomer--;
        this.OnPropertyChanged(nameof(Current));
        this.OnPropertyChanged(nameof(CurrentCustomerIndex));
        ...
    }
}
```

```csharp
private void First()
{
    this.currentCustomer = 0;
    this.OnPropertyChanged(nameof(Current));
    this.OnPropertyChanged(nameof(CurrentCustomerIndex));
    ...
}
```

```csharp
private void Last()
{
    this.currentCustomer = this.customers.Count - 1;
    this.OnPropertyChanged(nameof(Current));
    this.OnPropertyChanged(nameof(CurrentCustomerIndex));
    ...
}
```

```xml
<Page>
...
  Style="{StaticResource PageStyle}">
  <Grid>
    <ProgressRing HorizontalAlignment="Center" VerticalAlignment="Center"
      Foreground="AntiqueWhite" Height="100" Width="100"
      IsActive="{Binding IsBusy}" Canvas.ZIndex="1"/>
    <Grid x:Name="customersTabular" Margin="10,20,10,20" Visibility="Visible">
    ...
  </Grid>
</Page>
```

```xml
...
<Grid x:Name="customersTabularView" Margin="40,54,0,0" Visibility="Visible">
  ...
  <Grid Grid.Row="2">
    ...
    <TextBox Grid.Row="5" Grid.Column="3" Grid.ColumnSpan="3" x:Name="phone" .../>
    <TextBlock Grid.Row="6" Grid.Column="1" Grid.ColumnSpan="7"
               Style="StaticResource ErrorMessageStyle" Text="{Binding Error}"/>
  </Grid>
</Grid>
...
```

```xml
...
<Grid x:Name="customersColumnarView" Margin="10,20,10,20" Visibility="Collapsed">
  <Grid Grid.Row="1">
    ...
    <Grid.RowDefinitions>
      <RowDefinition/>
      <RowDefinition/>
      <RowDefinition/>
      <RowDefinition/>
      <RowDefinition/>
      <RowDefinition/>
    </Grid.RowDefinitions>
    ...
  </Grid>
</Grid>
```

```xml
..
<TextBox Grid.Row="5" Grid.Column="1" x:Name="cPhone ... />
<TextBlock Grid.Row="6" Grid.Column="0" Grid.ColumnSpan="2"
      Style="{StaticResource ErrorStyle}" Text="{Binding LastError}"/>
</Grid>
```

```xml
<Style x:Key="ErrorMessageStyle" TargetType="TextBlock">
  <Setter Property="HorizontalAlignment" Value="Left"/>
  <Setter Property="TextWrapping" Value="Wrap"/>
  <Setter Property="VerticalAlignment" Value="Top"/>
  <Setter Property="FontSize" Value="20"/>
  <Setter Property="Foreground" Value="White"/>
</Style>
```

```xml
<Page.BottomAppBar>
  <CommandBar>
    <AppBarElementContainer VerticalAlignment="Center">
      <TextBlock Padding="0, 0, 20, 0">
        <Run Text="{Binding Path=CurrentCustomerIndex}"/>
        <Run Text=" of "//
        <Run Text="{Binding Path=CustomerListCount}"/>
      </TextBlock>
    </AppBarElementContainer>
  </CommandBar>
</Page.BottomAppBar>
```

```csharp
using System.Net.Http;
using System.Text.Json;
```

```csharp
public class ViewModel: INotifyPropertyChanged
{
    public Command LastCustomer { get; private set; }

    private const string ServerUrl = "https://yourwebservice.azurewebsites.net/";
    private int offset = 0;
    private int count = 0;
    private HttpClient client = null;
    private JsonSerializerOptions options = new()
    {
        PropertyNameCaseInsensitive = true
    };

    public ViewModel()
    {
        ...
    }
}
```

```csharp
public ViewModel()
{
    this.client = new HttpClient();
    this.client.BaseAddress = new Uri(ServerUrl);
    this.client.DefaultRequestHeaders.Accept.Add(
        new MediaTypeWithQualityHeaderValue("application/json")
    );
}
```

```csharp
public async Task GetDataAsync(int offset, int count)
{
    IsBusy = true;
    try
    {
        var response = await client.GetAsync($"/api/customers?offset={offset}&count={count}");
        if (response.IsSuccessStatusCode)
        {
            var customersJsonString = await response.Content.ReadAsStringAsync();
            var customersData = JsonSerializer.Deserialize<List<Customer>>(customersJsonString, options);
            if (customersData != null)
            {
                customers = customersData;
                count = customers.Count;
            }
        }
        else
        {
            LastError = response.ReasonPhrase;
        }
    }
    catch (Exception e)
    {
        LastError = e.Message;
    }
    finally
    {
        IsBusy = false;
        OnPropertyChanged(nameof(CustomerCount));
    }
}
```

```csharp
public sealed class MainPage : Page
{
    internal const BatchSize = 100;
    ...
}
```

```csharp
public MainPage()
{
    ...
    ViewModel viewModel = new ViewModel();
    _ = viewModel.GetDataAsync(0, BatchSize);
    this.DataContext = viewModel;
}
```

```csharp
public class ViewModel: INotifyPropertyChanged
{
    ...
    public Command LastCustomer { get; private set; }
    public Command MoreCustomers { get; private set; }
    public Command Reset { get; private set; }
}
...
```

```csharp
private async Task More()
{
    if (this.customers.Count - 1 > this.currentCustomer)
    {
        this.currentCustomer++;
        this.OnPropertyChanged(nameof(Current));
        this.OnPropertyChanged(nameof(CurrentCustomerIndex));
        ...
    }
}
```

```csharp
public ViewModel()
{
    ...
    this.LastCustomer = new Command(this.Last, ...);
    this.MoreCustomers = new Command(async () => await this.More(),
    () => this.client is not null);
    ...
}
```

```csharp
public ViewModel()
{
    ...
    this.MoreCustomers = new Command(async O => {
        this.customers = null;
        await this.GetDataAsync(0, MainPage.BatchSize);
    }, O => this.client is not null);
    ...
}
```

```xml
<Page.TopAppBar>
  <CommandBar x:Name="lastCustomer" ...>
    <AppBarButton x:Name="lastCustomer" .../>
    <AppBarSeparator/>
    <AppBarButton x:Name="more" Icon="More" Label="More"
      Command="{Binding Path=MoreCustomers}"/>
    <AppBarButton x:Name="reset" Icon="Rotate" Label="Reset"
      Command="{Binding Path=Reset}"/>
  </CommandBar>
</Page.TopAppBar>
```

```csharp
public int CurrentCustomerIndex { get => currentCustomer + 1; }
public Command SearchCustomers { get; private set; }
public Command RunQuery { get; private set; }
public Command CancelSearch { get; private set; }
public Command NextCustomer { get; private set; }
```
