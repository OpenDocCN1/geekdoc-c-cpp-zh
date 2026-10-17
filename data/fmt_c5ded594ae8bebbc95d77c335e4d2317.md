
```
<TextBlock Grid.Row="0" Grid.Column="0" Text="Culture Name:" />
<TextBlock Grid.Row="0" Grid.Column="1" Text="{Binding
CultureInfo.Name}"
    Width="1000" />
<TextBlock Grid.Row="0" Grid.Column="2" Text="Neutral Culture"
    Visibility="{Binding CultureInfo.IsNeutralCulture,
    Converter={StaticResource boolToVisibility}}" />
<TextBlock Grid.Row="1" Grid.Column="0" Text="English Name:" />
<TextBlock Grid.Row="1" Grid.Column="1" Grid.ColumnSpan="2"
    Text="{Binding CultureInfo.EnglishName}" />
<TextBlock Grid.Row="2" Grid.Column="0" Text="Native Name:" />
<TextBlock Grid.Row="2" Grid.Column="1" Grid.ColumnSpan="2"
           Text="{Binding CultureInfo.NativeName}" />
<TextBlock Grid.Row="3" Grid.Column="0" Text="Default Calendar:"
           />
<TextBlock Grid.Row="3" Grid.Column="1" Grid.ColumnSpan="2"
           Text="{Binding CultureInfo.Calendar,
                 Converter={StaticResource calendarConverter}}" />
<TextBlock Grid.Row="4" Grid.Column="0" Text="Optional
Calendars:" />
<ListBox Grid.Row="4" Grid.Column="1" Grid.ColumnSpan="2"
         ItemsSource="{Binding CultureInfo.OptionalCalendars}">
  <ListBox.ItemTemplate>
    <DataTemplate>
      <TextBlock Text="{Binding
                   Converter={StaticResource calendarConverter}}" />
    </DataTemplate>
  </ListBox.ItemTemplate>
</ListBox>
```

将布尔值转换为`Visibility`枚举的转换器定义在`BooleanToVisibilityConverter`类中（代码文件`WPFCultureDemo\\Converters\\BooleanToVisibilityConverter.cs`）：

```
using System;
using System.Globalization;
using System.Windows;
using System.Windows.Data;

namespace CultureDemo.Converters
{
    public class BooleanToVisibilityConverter: IValueConverter
    {
        public object Convert(object value, Type targetType, object parameter,
            CultureInfo culture)
        {
            bool b = (bool)value;
            if (b)
                return Visibility.Visible;
            else
                return Visibility.Collapsed;
        }

        public object ConvertBack(object value, Type targetType,
            object parameter, CultureInfo culture)
        {
            throw new NotImplementedException();
        }
    }
}
```

用于显示日历文本的转换器稍微复杂一些。以下是`CalendarTypeToCalendarInformationConverter`类中`Convert`方法的实现。该实现使用类名和日历类型名来返回有用的日历值（代码文件`WPFCultureDemo/Converters/CalendarTypeToCalendarInformationConve...`）

```
public object Convert(object value, Type targetType, object parameter,
CultureInfo culture)
{
    var c = value as Calendar;
    if (c == null) return null;
    var calText = new StringBuilder(50);
    calText.Append(c.ToString());
    calText.Remove(0, 21); // remove the namespace
    calText.Replace("Calendar","");
    GregorianCalendar gregCal = c as GregorianCalendar;
    if (gregCal != null)
    {
        calText.Append($" {{{gregCal.CalendarType}}}");
    }
    return calText.ToString();
}
```

`CultureData`类包含用于显示数字、日期和时间格式的示例信息的属性。这些属性与以下`TextBlock`元素绑定：

```
<TextBlock Grid.Row="0" Grid.Column="0" Text="Number" />
<TextBlock Grid.Row="0" Grid.Column="1" Text="{Binding NumberSample}" />
<TextBlock Grid.Row="1" Grid.Column="0" Text="Full Date" />
<TextBlock Grid.Row="1" Grid.Column="1" Text="{Binding DateSample}" />
<TextBlock Grid.Row="2" Grid.Column="0" Text="Time" />
<TextBlock Grid.Row="2" Grid.Column="1" Text="{Binding TimeSample}" />
```

有关区域的信息显示在XAML代码的最后部分。如果`RegionInfo`不可用，则隐藏整个`GroupBox`。`TextBlock`元素绑定`RegionInfo`类型的`DisplayName`、`CurrencySymbol`、`ISOCurrencySymbol`和`IsMetric`属性：

```
<GroupBox x:Name="groupRegion" Header="Region Information" Grid.Row="6" Grid.Column="0" Grid.ColumnSpan="3" Visibility="{Binding RegionInfo, Converter={StaticResource nullToVisibility}}">
<Grid>
    <Grid.RowDefinitions>
        <RowDefinition />
        <RowDefinition />
        <RowDefinition />
    </Grid.RowDefinitions>
    <Grid.ColumnDefinitions>
        <ColumnDefinition />
        <ColumnDefinition />
        <ColumnDefinition />
    </Grid.ColumnDefinitions>
    <TextBlock Grid.Row="0" Grid.Column="0" Text="Region" />
    <TextBlock Grid.Row="0" Grid.Column="1" Grid.ColumnSpan="2" Text="{Binding RegionInfo.DisplayName}" />
    <TextBlock Grid.Row="1" Grid.Column="0" Text="Currency" />
    <TextBlock Grid.Row="1" Grid.Column="1" Text="{Binding RegionInfo.CurrencySymbol}" />
    <TextBlock Grid.Row="1" Grid.Column="2" Text="{Binding RegionInfo.ISOCurrencySymbol}" />
    <TextBlock Grid.Row="2" Grid.Column="1" Text="Is Metric" Visibility="{Binding RegionInfo.IsMetric,
Converter={StaticResource boolToVisiblity}" />
</Grid>
```

启动应用程序时，可以在树视图中看到所有可用的文化，选择一种文化会列出其特征，如图 28.6 所示。

![](img/3d365b72b289213a91ade7eb366b8f35_1041_0.png)

### Figure 28.6

### Sorting

示例`SortingDemo`使用了以下依赖项和命名空间：

#### Dependencies

```
NETStandard.Library
System.Collections.NonGeneric
```

#### Namespaces

```
System
System.Collections
System.Collections.Generic
System.Globalization
static System.Console
```

字符串的排序因文化而异。默认情况下用于比较字符串排序的算法是特定于文化的。例如，在芬兰语中，字符 V 和 W 被视为相同。为了演示这种行为，使用芬兰语排序，以下代码创建了一个小型控制台应用程序，其中一些美国州未排序地存储在数组中。

下面显示的`DisplayNames`方法用于在控制台上显示数组或集合的所有元素（代码文件`SortingDemo/Program.cs`）：

```
public static void DisplayNames(string title,
IEnumerable<string> e)
{
    WriteLine(title);
    WriteLine(string.Join("-", e));
    WriteLine();
}
```

在`Main`方法中，在创建包含部分美国州的数组后，线程属性`CurrentCulture`被设置为芬兰文化，以便以下`Array.Sort`使用芬兰排序顺序。调用`DisplayNames`方法会在控制台上显示所有州：

```
public static void Main()
{
    string[] names = {"Alabama","Texas","Washington","Virginia",
"Wisconsin","Wyoming","Kentucky","Missouri","Utah",
"Hawaii","Kansas","Louisiana","Alaska","Arizona"};

    CultureInfo.CurrentCulture = new CultureInfo("fi-FI");

    Array.Sort(names);
    DisplayNames("Sorted using the Finnish culture", names);
    // etc.
}
```

在第一次以芬兰排序顺序显示部分美国州之后，数组会再次排序。如果你想要一种与用户文化无关的排序，这在将排序后的数组发送到服务器或存储时很有用，可以使用不变文化。

你可以通过向`Array.Sort`传递第二个参数来实现。`Sort`方法期望第二个参数实现`IComparer`。`System.Collections`命名空间中的`Comparer`类实现了`IComparer`。`Comparer.DefaultInvariant`返回一个使用不变文化比较数组值以进行文化无关排序的`Comparer`对象：

```
public static void Main()
{
    // etc.
    // sort using the invariant culture
    Array.Sort(names,
System.Collections.Comparer.DefaultInvariant);
    DisplayNames("Sorted using the invariant culture", names);
}
```

程序输出显示了使用芬兰文化和文化无关文化的不同排序结果——使用不变排序顺序时 Virginia 在 Washington 之前，而使用芬兰语时则相反：

```
Sorted using the Finnish culture
Alabama-Alaska-Arizona-Hawaii-Kansas-Kentucky-Louisiana-
Missouri-Texas-Utah-
Washington-Virginia-Wisconsin-Wyoming

Sorted using the invariant culture
Alabama-Alaska-Arizona-Hawaii-Kansas-Kentucky-Louisiana-
```

> **NOTE** *如果对集合的排序应与文化无关，则集合必须使用不变文化进行排序。这在将排序结果发送到服务器或存储在文件内时特别有用。要向用户显示排序后的集合，最好使用用户的文化进行排序。*

除了特定于区域的格式和度量系统外，文本和图片也可能因文化而异。这就是资源发挥作用的地方。

### Resources

你可以将图片或字符串表等资源放入资源文件或卫星程序集中。此类资源在本地化应用程序时非常有帮助，而 .NET 具有内置支持来搜索本地化资源。在了解如何使用资源来本地化应用程序之前，以下部分解释了如何在不考虑语言方面时创建和读取资源。

#### Resource Readers and Writers

在 .NET Core 中，资源读取器和写入器与完整 .NET 版本相比有限（截至本文撰写时）。然而，对于许多场景——包括多平台支持——所需的功能是可用的。

`CreateResource`示例应用程序动态创建资源文件并从文件中读取资源。此示例使用了以下依赖项和命名空间：

##### Dependencies

- `NETStandard.Library`
- `System.Resources.ReaderWriter`

##### Namespaces

- `System.Collections`
- `System.IO`
- `System.Resources`
- `static System.Console`

`ResourceWriter`使你能够创建二进制资源文件。写入器的构造函数需要一个使用`File`类创建的`Stream`。你使用`AddResource`方法添加资源。.NET Core 的简单资源写入器需要键和值都为字符串。完整 .NET Framework 的资源写入器定义

> **NOTE** *保存包含 Unicode 字符的文本文件时，必须使用正确的编码保存文件。要选择 UTF8 编码，请使用“另存为”对话框。*

你可以使用资源文件生成器（`Resgen.exe`）实用程序从`Wrox.ProCSharp.Localization.MyResources.txt`创建资源文件。键入以下行

```
resgen Wrox.ProCSharp.Localization.MyResources.txt
```

创建文件`Wrox.ProCSharp.Localization.MyResources.resources`。生成的资源文件可以作为外部文件添加到程序集中，也可以嵌入到 DLL 或 EXE 中。`Resgen`还支持创建基于 XML 的`.resX`资源文件。使用`Resgen`本身构建 XML 文件的一种简便方法是：

```
resgen Wrox.ProCSharp.Localization.MyResources.txt
  Wrox.ProCSharp.Localization.MyResources.resX
```

此命令创建 XML 资源文件`Wrox.ProCSharp.LocalizationMyResources.resX`。`Resgen`支持强类型资源。强类型资源由访问资源的类表示。你可以使用`Resgen`实用程序的`/str`选项创建该类：
