
# Adventure Works 客户

```csharp
Console.WriteLine($"SerialPI complete: Duration: {milliseconds} ms");

Console.WriteLine($"Points in circle: {pointsList.Count}");
}
}
```

```csharp
object myLockObject = new object();

...

lock (myLockObject)
{
    // Code that requires exclusive access
    // to a shared resource
    ...
}
```

```csharp
SemaphoreSlim semaphore = new SemaphoreSlim(3);

...
semaphore.Wait();
// Access a resource from the pool
...
semaphore.Release();
```

```csharp
ReaderWriterLockSlim readerWriterLock = new ReaderWriterLockSlim();
Task readerTask = Task.Factory.StartNew(() =>
{
    ReaderWriterWriterLock.EnterReadLock();
    // Read shared resource
    ReaderWriterWriterLock.ExitReadLock();
});
Task writeTask = Task.Factory.StartNew(() =>
{
    ReaderWriterWriterLock.EnterWriteLock();
    // Write to shared resource
    ReaderWriterWriterLock.ExitWriteLock();
});
```

```csharp
CancellationTokenSource = new
CancellationTokenSource();
CancellationToken = cancellationTestSource.Token;
...

// Semaphore that protects a pool of 3 resources
SemaphoreSlim = new SemaphoreSlim(3);
// Wait on the semaphore, and throw an
// OperationCanceledException if
// another thread calls Cancel on
// cancellationTokenSource
semaphore.Wait(cancellationToken);
```

```xml
<Page x:Class="Customers.MainPage"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:local="using:Customers"
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
mc:Ignorable="d"
Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
<Grid>
</Grid>
</Page>
```

```xml
xmlns:local="using:Customers"
```

```csharp
// The Blank Page item template is documented at http://go.microsoft.com/fwlink/?LinkId=402352&clcid=0x409
namespace Customers
{
    /// <summary>
    /// An empty page that can be used on its own or navigated to within a Frame.
    /// </summary>
    public sealed partial class MainPage : Page
    {
        public MainPage()
        {
            this.InitializeComponent();
        }
    }
}
```

```xml
x:Class="Customers.MainPage"
```

```xml
<Page
  x:Class="Customers.MainPage"
  ...>
  <Button Content="Click Me"/>
</Page>
```

```xml
<Grid>
    <TextBlock />
</Grid>
```

```xml
<TextBox x:Name="id" HorizontalAlignment="Left" Margin="300,240,0,0" TextWrapping="Wrap"
Text="" VerticalAlignment="Top" FontSize="20" IsReadOnly="True"/>
<TextBox x:Name="firstName" HorizontalAlignment="Left" Margin="550,240,0,0"
TextWrapping="Wrap" Text="" VerticalAlignment="Top" Width="300" FontSize="20"/>
<TextBox x:Name="lastName" HorizontalAlignment="Left" Margin="875,240,0,0"
TextWrapping="Wrap" Text="" VerticalAlignment="Top" Width="300" FontSize="20"/>
```

```xml
<ComboBox x:Name="title" HorizontalAlignment="Left" Margin="420,240,0,0" VerticalAlignment="Top" Width="100" FontSize="20"/>
```

```xml
<ComboBox xName="title" HorizontalAlignment="Left" Margin="420,240,0,0" VerticalAlignment="Top" Width="75" FontSize="20">
  <ComboBoxItem Content="Mr"/>
  <ComboBoxItem Content="Mrs"/>
  <ComboBoxItem Content="Ms"/>
  <ComboBoxItem Content="Miss"/>
</ComboBox>
```

```xml
<TextBlock HorizontalAlignment="Left" Margin="300,390,0,0" TextWrapping="Wrap"
Text="Email" VerticalAlignment="Top" FontSize="20"/>
<TextBox x:Name="email" HorizontalAlignment="Left" Margin="450,390,0,0"
TextWrapping="Wrap" Text="" VerticalAlignment="Top" Width="400" FontSize="20"/>
<TextBlock HorizontalAlignment="Left" Margin="300,540,0,0" TextWrapping="Wrap"
Text="Phone" VerticalAlignment="Top" FontSize="20"/>
<TextBox x:Name="phone" HorizontalAlignment="Left" Margin="450,540,0,0"
TextWrapping="Wrap" Text="" VerticalAlignment="Top" Width="200" FontSize="20"/>
```

```xml
<Grid>
  <Grid Margin="10,20,10,20">
  </Grid>
  <TextBlock HorizontalAlignment="Left" TextWrapping="Wrap"
  Text="Adventure Works Customers" ... />
  ...
</Grid>
```

```xml
<Grid Margin="10,20,10,20">
  <Grid.RowDefinitions>
    <RowDefinition Height="2*"/>
    <RowDefinition Height="*"/>
    <RowDefinition Height="10*"/>
    <RowDefinition Height="2*"/>
  </Grid.RowDefinitions>
</Grid>
```

```xml
<Grid.Row="2">
  <Grid.RowDefinitions>
    ...
  </Grid.RowDefinitions>
  <Grid.ColumnDefinitions>
    ...
  </Grid.ColumnDefinitions>
  ...
  <TextBox ... x:Name="email" .../> .../>
  <TextBlock Grid.Row="5" Grid.Column="1" HorizontalAlignment="Center" TextWrapping="Wrap" Text="电话" VerticalAlignment="Center" FontSize="20"/>
  <TextBox Grid.Row="5" Grid.Column="3" Grid.ColumnSpan="3" x:Name="phone" HorizontalAlignment="Left" TextWrapping="Wrap" Text="" VerticalAlignment="Center" Width="200" FontSize="20"/>
</Grid>
```

```xml
<Grid>
  <Grid x:Name="customersTabularView" Margin="10,20,10,20" Visibility="Collapsed">
  ...
  </Grid>
</Grid>
```

```xml
<Grid>
  <Grid x:Name="customersTabularView" Margin="10,20,10,20" Visibility="Collapsed">
    ...
  </Grid>
  <Grid x:Name="customersColumnarView" Margin="10,20,10,20" Visibility="Visible">
  </Grid>
</Grid>
```

```xml
<Grid x:Name="customersColumnarView" Margin="10,20,10,20" Visibility="Visible">
  <Grid.RowDefinitions>
    <RowDefinition Height="*"/>
    <RowDefinition Height="10*"/>
  </Grid.RowDefinitions>
</Grid>
```

```xml
<Grid x:Name="customersColumnarView" Margin="10,20,10,20" Visibility="Visible">
  <Grid.RowDefinitions>
    ...
  </Grid.RowDefinitions>
  <TextBlock Grid.Row="0" HorizontalAlignment="Center" TextWrapping="Wrap"
    Text="客户" VerticalAlignment="Center" FontSize="30"/>
</Grid>
```

```xml
<TextBlock Grid.Row="0" ... />
<Grid Grid.Row="1">
  <Grid.ColumnDefinitions>
    <ColumnDefinition/>
    <ColumnDefinition/>
  </Grid.ColumnDefinitions>
  <Grid.RowDefinitions>
    <RowDefinition/>
    <RowDefinition/>
    <RowDefinition/>
    <RowDefinition/>
    <RowDefinition/>
    <RowDefinition/>
  </Grid.RowDefinitions>
</Grid>
```

```xml
<Grid.RowDefinitions>
  ..
</Grid.RowDefinitions>
<TextBlock Grid.Row="0" Grid.Column="0" HorizontalAlignment="Center"
TextWrapping="Wrap" Text="" VerticalAlignment="Center" FontSize="20"/>
<TextBlock Grid.Row="1" Grid.Column="0" HorizontalAlignment="Center"
TextWrapping="Wrap" Text="标题" VerticalAlignment="Center" FontSize="20"/>
<TextBlock Grid.Row="2" Grid.Column="0" HorizontalAlignment="Center"
TextWrapping="Wrap" Text="名" VerticalAlignment="Center" FontSize="20"/>
<TextBlock Grid.Row="3" Grid.Column="0" HorizontalAlignment="Center"
TextWrapping="Wrap" Text="姓" VerticalAlignment="Center" FontSize="20"/>
```

```xml
<TextBlock Grid.Row="3" Grid.Column="0" HorizontalAlignment="Center"
<TextWrapping="Wrap" Text="姓" .../ />
<TextBox Grid.Row="0" Grid.Column="1" x="cid" HorizontalAlignment="Stretch"
<TextWrapping="Wrap" Text="VerticalAlignment="Center" FontSize="20" IsReadOnly="True"/>
<TextBox Grid.Row="1" Grid.Column="1" x="FirstName" HorizontalAlignment="Stretch"
<TextWrapping="Wrap" Text="VerticalAlignment="Center" FontSize="20"/>
<TextBox Grid.Row="2" Grid.Column="1" x="LastName" HorizontalAlignment="Stretch"
<TextWrapping="Wrap" Text="VerticalAlignment="Center" FontSize="20"/>
<TextBox Grid.Row="3" Grid.Column="1" x="cLastName" HorizontalAlignment="Stretch"
<TextWrapping="Wrap" Text="VerticalAlignment="Center" FontSize="20"/>
<ComboBox Grid.Row="4" Grid.Column="1" x="cTitle" HorizontalAlignment="Stretch"
VerticalAlignment="Center" Content="" FontSize="20">
<ComboBoxItem Content="先生"/>
<ComboBoxItem Content="夫人"/>
<ComboBoxItem Content="女士"/>
<ComboBoxItem Content="小姐"/>
</ComboBox>
```

```xml
<ComboBox ...>
...
</ComboBox>
<TextBlock Grid.Row="4" Grid.Column="0" HorizontalAlignment="Center" TextWrapping="Wrap"
Text="邮箱" VerticalAlignment="Center" FontSize="20"/>
```
