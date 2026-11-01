
```csharp
public IEnumerable<Championship> Years
{
    get
    {
        FIDataContext.Data = data;
        return (from r in data.Races
                orderby r.Date ascending
                select new Championship
                {
                    Year = r.Date.Year,
                }).Distinct();
    }
}
```
代码片段 Formula1Demo/TreeUC.xaml.cs

Championship 类有一个简单的自动属性用于年份。Races 属性的类型为 Lazy<IEnumerable<F1Race>>。Lazy<T> 类在 .NET 4 中新增，用于延迟初始化。使用 TreeView 控件时，这非常方便。如果树背后的数据很大，并且你不想提前加载整棵树，而只在用户进行选择时加载，则可以通过分页实现延迟加载。

在简单场景中，只需为 DataGrid 的 ItemsSource 属性赋值。默认情况下，DataGrid 根据绑定数据的属性创建列：
```xml
<UserControl x:Class="Formula1Demo.GridUC"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
mc:Ignorable="d"
d:DesignHeight="300" d:DesignWidth="300">

<Grid>
    <Grid.RowDefinitions>
        <RepeatButton Margin="5" Click="OnPrevious">Previous</RepeatButton>
        <RepeatButton Margin="5" Click="OnNext">Next</RepeatButton>
    </Grid.RowDefinitions>
    <StackPanel Orientation="Horizontal" Grid.Row="0">
        <Button Click="OnPrevious">Previous</Button>
        <Button Click="OnNext">Next</Button>
    </StackPanel>
    <DataGrid Grid.Row="1" ItemsSource="{Binding}" />
</Grid>
</UserControl>
```
代码片段 Formula1Demo/GridUC.xaml

代码隐藏使用与之前的 TreeView 示例相同的 Formula1 数据库。UserControl 的 DataContext 被设置为 Races 属性。该属性返回 IEnumerable<object>。而不是分配强类型枚举，使用 object 是为了能够使用 LINQ 查询创建匿名类。LINQ 查询创建具有 Year、Country、Position、Racer 和 Car 属性的匿名类，并使用复合查询访问 Races 和 RaceResults。它还访问 Races 的其他关联以获取国家、车手和车队信息。通过 Skip() 和 Take() 方法实现了分页功能。页面的大小固定为 50 项，当前页面通过 OnNext() 和 OnPrevious() 处理程序更改：
```csharp
using System.Collections.Generic;
using System.Linq;
using System.Windows;
using System.Windows.Controls;

namespace Formula1Demo
{
    public partial class GridUC : UserControl
    {
        private int currentPage = 0;
        private int pageSize = 50;
        private Formula1Entities data = new Formula1Entities();
        public GridUC()
        {
            InitializeComponent();
            this.DataContext = Races;
        }

        public IEnumerable<object> Races
        {
            get
            {
                return (from r in data.Races
                        from rr in r.RaceResults
                        orderby r.Date ascending
                        select new
                        {
                            Year = r.Date.Year,
Country = rr.Circuit.Country,
Position = rr.Position,
Racer = rr.Racer.Firstname + " " + rr.Racer.Lastname,
Car = rr.Team.Name
}).Skip(currentPage * pageSize).Take(pageSize);

}

private void OnPrevious(object sender, RoutedEventArgs e)
{
    if (currentPage > 0)
    {
        currentPage--;
        this.DataContext = Races;
    }
}

private void OnNext(object sender, RoutedEventArgs e)
{
    currentPage++;
    this.DataContext = Races;
}
}
```
代码片段 Formula1Demo/GridUC.xaml.cs

图 36-15 显示了使用默认网格样式和标题的运行中应用程序。

![](img/d7d2ffa0a76feaab821930e95daace93_1130_0.png)

图 36-15

## 自定义列

将 DataGrid 的 AutoGenerateColumns 属性设置为 False 不会生成默认列。你可以使用 Column 属性创建自定义列。你还可以指定派生自 DataGridColumn 的元素。存在可用的预定义类。DataGridTextColumn 可用于读取和编辑文本。DataGridHyperlinkColumn 用于显示超链接。DataGridCheckBoxColumn 为布尔数据显示复选框。对于列中的项目列表，你可以使用 DataGridComboBoxColumn。未来将提供更多 DataGridColumn 类型，但如果你现在需要不同的表示形式，可以使用 DataGridTemplateColumn 来定义和绑定你想要的任何元素。

示例代码使用绑定到 Position 和 Racer 属性的 DataGridTextColumn 元素。Header 属性被设置为字符串以便显示。当然，你也可以使用模板为列定义完整的自定义标题：
<DataGrid ItemsSource="{Binding}" AutoGenerateColumns="False">
    <DataGrid.Columns>
        <DataGridTextColumn Binding="{Binding Position, Mode=OneWay}"
```csharp
public class Championship
{
    public int Year { get; set; }
    public Lazy<IEnumerable<F1Race>> Races
    {
        get
        {
            return new Lazy<IEnumerable<F1Race>>(() =>
            {
                return from r in FIDataContext.Data.Races
                       where r.Date.Year == Year
                       orderby r.Date
                       select new F1Race
                       {
                           Date = r.Date,
                           Country = r.Circuit.Country
                       };
            });
        }
    }
}
```
代码片段 Formula1Demo/Championship.cs

F1Race 类再次定义了 Results 属性，该属性使用 Lazy<T> 类型返回 F1RaceResult 对象的列表：
```csharp
public class F1Race
{
    public string Country { get; set; }
    public DateTime Date { get; set; }
    public Lazy<IEnumerable<F1RaceResult>> Results
    {
        get
```csharp
public class FIRaces
{
    private int lastpageSearched = -1;
    private IEnumerable<object> cache = null;
    private Formula1Entities data = new Formula1Entities();

    public IEnumerable<object> GetRaces(int page, int pageSize)
    {
        if (lastpageSearched == page)
            return cache;
        lastpageSearched = page;

        var q = (from x in data.Races
                 from rr in x.RaceResults
                 orderby r.Date ascending
                 select new
                 {
                     Year = r.Date.Year,
                     Country = r.Circuit.Country,
                     Position = rr.Position,
                     Racer = rr.Racer.Firstname + " " + rr.Racer.Lastname,
                     Car = rr.Team.Name,
                     Points = rr.Points
                 }).Skip(page * pageSize).Take(pageSize);
        cache = q;
        return cache;
    }
}
```
代码片段 Formula1Demo/F1Races.cs

现在只剩下用户设置页码并更改 ObjectDataProvider 的参数。

在用户界面中定义了一个 TextBox 和一个 Button：
```xml
<StackPanel Orientation="Horizontal" Grid.Row="0">
    <TextBlock Margin="5" Padding="4" VerticalAlignment="Center" Text="Page:"></TextBlock>
    <TextBox Margin="5" Padding="4" VerticalAlignment="Center" x:Name="textPageNumber" Text="0" />
    <Button Click="OnGetPage">Get Page</Button>
</StackPanel>
```
代码片段 Formula1Demo/GridGroupingUC.xaml

按钮的代码隐藏中的 OnGetPage() 处理程序访问 ObjectDataProvider 并更改方法的第一个参数。然后它调用 Refresh 方法，以便 ObjectDataProvider 请求新页面：
```csharp
private void OnGetPage(object sender, RoutedEventArgs e)
{
    int page = int.Parse(textPageNumber.Text);
    var odp = (sender as FrameworkElement).FindResource("races")
        as ObjectDataProvider;
    odp.MethodParameters[0] = page;
    odp.Refresh();
}
```
代码片段 Formula1Demo/GridGroupingUC.xaml.cs
