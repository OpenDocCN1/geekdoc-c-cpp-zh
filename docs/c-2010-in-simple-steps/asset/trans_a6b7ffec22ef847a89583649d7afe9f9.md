
9. 按 F5 键再次运行 CalendarDemo 应用程序。输出出现（Fig.C#7.33）。

10. 如图 C#7.33 所示，点击 Calendar 控件上的 Apr 选项：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_254_0.png)

Fig.C#7.33

点击 Apr 选项后的输出出现，如图 C#7.34 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_254_1.png)

Fig.C#7.34

在图 C#7.34 中，我们将 Calendar 控件中显示的日期数量限制为三个：28、29 和 30。

## 使用 DatePicker 控件

与 Calendar 控件类似，WPF 的 DatePicker 控件也允许用户选择日期。位于 System.Windows.Controls 命名空间中，DatePicker 控件继承 DatePicker 类。

表 7.13 列出了 DatePicker 类值得注意的属性：

### 表 7.13：DatePicker 类的注目属性

| 属性 | 描述 |
|---|---|
| BlackOutDates | 检索或分配一个在 DatePicker 控件中标记为不可选择的日期集合 |
| DisplayDate | 检索或设置在 DatePicker 控件中显示的日期 |
| DisplayDateEnd | 检索或设置在 DatePicker 控件中显示的最后日期 |
| DisplayDateStart | 检索或设置在 DatePicker 控件中显示的第一个日期 |
| FirstDayOfWeek | 检索或设置在 DatePicker 控件中被视为一周开始的日期 |
| SelectedDate | 检索或设置 DatePicker 控件中当前选择的日期 |
| SelectedDateFormat | 检索或设置用于在 DatePicker 控件中显示所选日期的格式 |
| SelectionMode | 检索或设置指示 DatePicker 控件中允许何种日期选择的值。SelectionMode 属性的默认值是 SingleDate，这意味着只能选择一个日期。 |

让我们创建一个名为 DatePickerDemo 的独立 WPF 应用程序来展示 DatePicker 控件的使用。为此，请执行以下步骤：

1. 在本章的 *使用 Grid 控件* 部分创建 GridDemo 应用程序时，重复之前执行的步骤 1 到 3。
2. 在 Name 文本框中输入名称 DatePickerDemo，并在 Location 下拉组合框中指定应用程序的适当位置。
3. 点击 OK 按钮。DatePickerDemo 应用程序已创建。
4. 在 MainWindow.xaml 文件中添加清单 7.18 中给出的突出显示的代码：

### 清单 7.18：显示添加 DatePicker 控件的代码

```xml
<Window x:Class="DatePickerDemo.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="DatePickerDemo" Height="300" Width="300">
    <Grid>
        <DatePicker Height="25" HorizontalAlignment="Left" Margin="10,10,0,0" Name="datePicker1" VerticalAlignment="Top" Width="115"/>
    </Grid>
</Window>
```

在清单 7.18 中，一个 DatePicker 控件被添加到 Grid 控件中。DatePicker 控件的 Width 和 Height 属性被设置，而 Name 属性用于唯一标识 DatePicker 控件。

5. 在 MainWindow.xaml.cs 文件中添加清单 7.19 中给出的突出显示的代码：

### 清单 7.19：为 DatePicker 控件添加代码

```csharp
namespace DatePickerDemo
{
    /// <summary>
    /// Interaction logic for MainWindow.xaml
    /// </summary>
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();
            datePicker1.SelectedDate = new DateTime(2010, 5, 1);
            datePicker1.DisplayDateStart = new DateTime(2010, 5, 1);
            datePicker1.DisplayDateEnd = new DateTime(2010, 5, 31);
            datePicker1.FirstDayOfWeek = DayOfWeek.Monday;
        }
    }
}
```

如清单 7.19 所示，DatePicker 控件的 DisplayDate 属性被设置为 2010 年 5 月 1 日。由于 DisplayDateEnd 属性，DatePicker 控件上显示的最后日期是 2010 年 5 月 31 日。此外，使用控件的 FirstDayOfWeek 属性将星期一指定为一周的第一天。

6. 按 F5 键运行 DatePickerDemo 应用程序。输出出现（Fig.C#7.35）。

7. 如图 C#7.35 所示，点击 DatePicker 控件上显示的日期右侧的向下箭头：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_256_0.png)

Fig.C#7.35

点击下拉箭头的输出显示在图 C#7.36 中：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_256_1.png)

Fig.C#7.36

现在你已经了解了 WPF 中使用的一些常用控件，让我们继续学习 WPF 中的资源和样式。

## 使用资源和样式

考虑一种情况，你想在 WPF 应用程序中的多个元素上应用背景颜色。为此，你可以在这些元素上设置 Background 属性；然而，这可能相当繁琐。WPF 允许你通过资源简化并简化此类常用对象的使用。资源是指资源字典的一部分的对象、元素或值，可被应用程序的其他元素重用。资源字典是 ResourceDictionary 类的一个实例，指在元素上定义的资源集合。

虽然你可以为任何 UI 元素定义资源，但建议在根元素（如 Window 或 Page 元素）上定义资源。你为元素定义的资源也适用于该元素的所有子元素。例如，如果你为 Window 元素定义资源且其子元素为 Grid 元素，则 Window 元素的资源也适用于 Grid 元素。然而，如果你为 Grid 元素定义资源，则该资源仅适用于 Grid 元素的子元素。

### 提示

> 假设你有一个包含多个 Window 元素的独立 WPF 应用程序，并且你想将资源应用于所有 Window 元素。为此，你需要在应用程序的 App.xaml 文件中定义资源。

你可以通过使用元素的 Resources 属性在元素上定义资源。Resources 属性指的是该元素的资源字典。通过 Resources 属性，你可以在元素上定义任意多的资源。你在元素上定义的每个资源都必须有一个唯一的键，该键指的是在资源字典中唯一标识资源的字符串。唯一的键是通过使用 x:Key 属性分配给资源的。在定义资源后，你可以通过在任何 UI 元素中将资源引用为属性值来使用它们。在 WPF 中引用资源的语法如下：

```xml
<elementName propertyName="{markupExtension KeyName}">
    <!--content-->
</elementName>
```

前述语法中的各个参数可以简要描述如下：

- **elementName**: 指的是使用资源的元素的名称
- **propertyName**: 指的是其值取自资源的属性的名称
- **markupExtension**: 指的是资源的类型，可以是静态资源或动态资源
- **keyName**: 指的是资源的键名

根据用于引用资源的标记扩展，有两种类型的资源：静态和动态。让我们在以下各节中详细了解这两种资源类型。

## 使用静态资源

使用 StaticResource 标记扩展引用的资源称为静态资源。当资源在运行时保持静态时，即资源的值在被引用后不会改变，你可以将资源引用为静态资源。

静态资源的值在加载时确定。资源的键名会在应用程序中的所有资源（资源字典）中查找。键名首先在你要设置属性的元素的资源中查找。如果找不到键名，则在父元素及其资源中查找，直到根元素。如果在任何元素中都找不到键名，则在应用程序资源中查找键名。如果根本找不到静态资源，则会发生异常。

让我们创建一个名为 StaticResourcesDemo 的独立 WPF 应用程序来展示静态资源的使用。为此，请执行以下步骤：

1. 在本章的 *使用 Grid 控件* 部分创建 GridDemo 应用程序时，重复之前执行的步骤 1 到 3。
2. 在 **Name** 文本框中输入名称 **StaticResourcesDemo**，并在 **Location** 下拉组合框中指定应用程序的适当位置。
3. 点击 **OK** 按钮。StaticResourcesDemo 应用程序已创建。
4. 在 MainWindow.xaml 文件中添加清单 7.20 中给出的突出显示的代码。

### 清单 7.20：在 XAML 中使用静态资源

```xml
<Window x:Class="StaticResourcesDemo.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="Demo StaticResources" Height="200" Width="300">
    <Grid>
        <Grid.Resources>
            <SolidColorBrush x:Key="firstBrush" Color="BlanchedAlmond"/>
            <SolidColorBrush x:Key="secondBrush" Color="ForestGreen"/>
        </Grid.Resources>
        <Button Name="button1" Width="50" Height="100" Margin="0,0,200,0"
                Background="{StaticResource firstBrush}"/>
        <Button Name="button2" Width="50" Height="100" Margin="0,0,0,0"
                Background="{StaticResource secondBrush}"/>
        <Button Name="button3" Width="50" Height="100" Margin="200,0,0,0"
                Background="{StaticResource firstBrush}"/>
    </Grid>
</Window>
```

在清单 7.20 中，**Grid** 控件使用 **Resources** 属性来定义一组资源。两个 **SolidColorBrush** 资源（**SolidColorBrush** 元素用纯色填充给定区域）与
