

```xml
<Style x:Key="PageStyle" TargetType="Page">
  ...
</Style>
<Style x:Key="FontStyle" TargetType="TextBlock">
  <Setter Property="FontFamily" Value="Segoe Print"/>
</Style>
```

<Style x:Key="FontStyle" TargetType="TextBlock">
</Style>
<Style x:Key="HeaderStyle" TargetType="TextBlock" BasedOn={StaticResource FontStyle}>
  <Setter Property="HorizontalAlignment" Value="Center"/>
  <Setter Property="TextWrapping" Value="Wrap"/>
  <Setter Property="VerticalAlignment" Value="Center"/>
  <Setter Property="Foreground" Value="SteelBlue"/>
</Style>
```

<Style x:Key="HeaderStyle" TargetType="TextBlock" BasedOn="{StaticResource FontStyle}">
</Style>
<Style x:Key="TabularHeaderStyle" TargetType="TextBlock" BasedOn="{StaticResource HeaderStyle}">
  <Setter Property="FontSize" Value="40"/>
</Style>
<Style x:Key="ColumnarHeaderStyle" TargetType="TextBlock" BasedOn="{StaticResource HeaderStyle}">
  <Setter Property="FontSize" Value="30"/>
</Style>
```

# Adventure Works Customers

```xml
<TextBlock Grid.Row="0" Style="{StaticResource TabularHeaderStyle}" Text="Adventure Works Customers"/>
```

# 客户

```xml
<TextBlock Grid.Row="0" Style="{StaticResource ColumnarHeaderStyle}" Text="Customers" />
```

```xml
<Style x:Key="HeaderStyle" TargetType="TextBlock" BasedOn="StaticResource FontStyle">
  <Setter Property="HorizontalAlignment" Value="Center"/>
  <Setter Property="TextWrapping" Value="Wrap"/>
  <Setter Property="VerticalAlignment" Value="Center"/>
  <Setter Property="Foreground" Value="SteelBlue"/>
  <Setter Property="RenderTransformOrigin" Value="0.5,0.5"/>
  <Setter Property="RenderTransform">
    <Setter.Value>
      <CompositeTransform Rotation="-5"/>
    </Setter.Value>
  </Setter>
</Style>
```

```xml
<Style x:Key="LabelStyle" TargetType="TextBlock" BasedOn="{StaticResource FontStyle}">
  <Setter Property="FontSize" Value="20"/>
  <Setter Property="HorizontalAlignment" Value="Center"/>
  <Setter Property="TextWrapping" Value="Wrap"/>
  <Setter Property="VerticalAlignment" Value="Center"/>
  <Setter Property="Foreground" Value="AntiqueWhite"/>
</Style>
```

```xml
<Grid x:Name="customersTabularView" Margin="10,20,10,20" Visibility="Visible">
  ...
  <Grid Grid.Row="2">
    ...
    <TextBlock Grid.Row="0" Grid.Column="1" Style="{StaticResource TLabel} Text="ID"/>
    <TextBlock Grid.Row="0" Grid.Column="3" Style="{StaticResource TLabel} Text="Title"/>
    <TextBlock Grid.Row="0" Grid.Column="5" Style="{StaticResource TLabel} Text="First Name"/>
    <TextBlock Grid.Row="0" Grid.Column="7" Style="{StaticResource TLabel} Text="Last Name"/>
    ...
    <TextBlock Grid.Row="3" Grid.Column="1" Style="{StaticResource TLabel} Text="Email"/>
    ...
    <TextBlock Grid.Row="5" Grid.Column="1" Style="{StaticResource TLabel} Text="Phone"/>
    ...
  </Grid>
  <Grid x:Name="customersColumnarView" Margin="10,20,10,20" Visibility="Collapsed">
    ...
    <Grid Grid.Row="1">
      ...
      <TextBlock Grid.Row="0" Grid.Column="0" Style="{StaticResource TLabel} Text="ID"/>
      <TextBlock Grid.Row="1" Grid.Column="0" Style="{StaticResource TLabel} Text="Title"/>
      <TextBlock Grid.Row="2" Grid.Column="0" Style="{StaticResource TLabel} Text="First Name"/>
      <TextBlock Grid.Row="3" Grid.Column="0" Style="{StaticResource TLabel} Text="Last Name"/>
      ...
      <TextBlock Grid.Row="4" Grid.Column="0" Style="{StaticResource TLabel} Text="Email"/>
      ...
      <TextBlock Grid.Row="5" Grid.Column="0" Style="{StaticResource TLabel} Text="Phone"/>
    />
  </Grid>
</Grid>
```

```xml
<Style x:Key="PageStyle" TargetType="Page">
    <Setter Property="Background" Value="{StaticResource WoodBrush}"/>
</Style>
```

```xml
<Grid Style="{StaticResource PageStyle}">
```

```xml
<Rectangle Grid.Row="0" RowSpan="6" Grid.Column="1" Grid.ColumnSpan="7" ...>
<Rectangle.Fill>
  <LinearGradientBrush EndPoint="0.5,0.1" StartPoint="0.5,0.0">
    <GradientStop Color="#FF0E3899"/>
    <GradientStop Color="#FF141415" Offset="0.9"/>
  </LinearGradientBrush>
</Rectangle.Fill>
</Rectangle>
```

```csharp
public class Customer
{
    private int _customerID;
    public int CustomerID
    {
        get => _customerID;
        set { _customerID = value; }
    }
    private string _title;
    public string Title
    {
        get => _title;
        set { _title = value; }
    }
    private string _firstName;
    public string FirstName
    {
        get => _firstName;
        set { _firstName = value; }
    }
    private string _lastName;
    public string LastName
    {
        get => _lastName;
        set { _lastName = value; }
    }
    private string _email;
    public string Email
    {
        get => _email;
        set { _email = value; }
    }
    private string _phone;
    public string Phone
    {
        get => _phone;
        set { _phone = value; }
    }
}
```

```csharp
public MainPage()
{
    InitializeComponent();
    Customer customer = new Customer
    {
        CustomerID = 1,
        Title = "Mr",
        LastName = "Sharp",
        Email = "john@contoso.com",
        Phone = "111-1111"
    };
    this.DataContext = customer;
}
```

