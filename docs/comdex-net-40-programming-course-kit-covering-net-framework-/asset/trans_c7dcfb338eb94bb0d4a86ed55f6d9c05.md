
- 13. **按键盘上的 F5 键**运行应用程序。应用程序的输出如图 VB-5.44 所示。

图 VB-5.44 中的 **Calendar** 控件显示当前年份当前月份的日历。默认情况下，**Calendar** 控件以月模式显示日期，在此模式下，日历一次只显示一个月的日期。但是，您可以更改 **Calendar** 控件的显示模式，使日历一次显示一年的所有月份。

- 14. 单击 **按年模式显示日期** 按钮以按年模式显示日期（图 VB-5.44）。

日历显示当前年份的所有月份，并将当前月份突出显示（图 VB-5.45）。

- 15. 单击日历中的当前月份，以像之前一样显示当前月份的所有日期（图 VB-5.45）。

![](img/9862a98a1a2d3bb14334137965a1ec60_218_0.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_218_1.png)

- 16. 单击 **限制显示的日期** 按钮以限制日历中显示的日期（图 VB-5.46）。

日历仅显示指定范围内的日期（图 VB-5.47）。

![](img/9862a98a1a2d3bb14334137965a1ec60_218_2.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_218_3.png)

现在我们来了解 DatePicker 控件。

## 使用 DatePicker 控件

DatePicker 控件是 WPF 4.0 中引入的新 WPF 控件。与 **Calendar** 控件类似，**DatePicker** 控件也允许您选择日期。但是，这两个控件之间的区别在于：Calendar 控件仅由一个可从中选择日期的日历组成，而 DatePicker 控件是组合框和日历的组合。**DatePicker** 控件是 **DatePicker** 类的实例，该类定义在 **System.Windows.Controls** 命名空间中。表 5.13 列出了 **DatePicker** 类值得注意的属性：

**表 5.13：DatePicker 类值得注意的属性**

| 属性 | 描述 |
|---|---|
| **BlackoutDates** | 检索或分配在 DatePicker 控件中标记为不可选择的日期集合 |
| **DisplayDate** | 检索或设置要在 DatePicker 控件中显示的日期 |
| **DisplayDateEnd** | 检索或设置要在 DatePicker 控件中显示的最后一个日期 |
| **DisplayDateStart** | 检索或设置要在 DatePicker 控件中显示的第一个日期 |
| **FirstDayOfWeek** | 检索或设置 DatePicker 控件中被视为一周开始的那一天 |
| **SelectedDate** | 检索或设置 DatePicker 控件中当前选定的日期 |
| **SelectedDateFormat** | 检索或设置用于在 DatePicker 控件中显示所选日期的格式 |
| **SelectionMode** | 检索或设置一个值，该值指示 DatePicker 控件中允许何种日期选择。SelectionMode 属性的默认值为 SingleDate，这意味着只能选择一个日期。 |

执行以下步骤，在 WPF 独立应用程序中使用 DatePicker 控件：

- 1. *启动* Visual Studio 2010。
- 2. 从菜单栏中*选择* **文件→新建→项目**。将打开新建项目对话框。
- 3. 在 **新建项目** 对话框的左窗格中，从 **已安装的模板** 部分*选择* **Visual Basic→Windows**。
- 4. 在中间窗格中*选择* **WPF 应用程序** 模板以创建 WPF 独立应用程序。
- 5. 在 **名称** 文本框中*输入*应用程序名称 **MyDatePicker**（也位于 CD 上），并在 **位置** 组合框中输入应用程序的适当位置。
- 6. *单击* **确定** 按钮关闭 **新建项目** 对话框并创建 **MyDatePicker** 应用程序。
- 7. 用代码清单 5.15 中给出的代码*替换* **MainWindow.xaml** 文件的 XAML 视图中的默认代码：

**代码清单 5.15：显示 MainWindow.xaml 文件的代码**

```xml
<Window x:Class="MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="MyDatePicker Application" Height="250" Width="250">
    <Grid>
        <DatePicker Height="25" HorizontalAlignment="Left" Margin="10,10,0,0"
                    Name="DatePicker1" VerticalAlignment="Top" Width="115"/>
    </Grid>
</Window>
```

在代码清单 5.15 中，Window 元素的 **Title** 属性设置为 **MyDatePicker Application**。这意味着文本 **MyDatePicker Application** 会出现在窗口的标题栏上。之后，我们向 Grid 控件添加了一个 **DatePicker** 控件。

- 8. 按键盘上的 **F5** 键运行应用程序。应用程序的输出如图 VB-5.48 所示。
- 9. 单击 DatePicker 控件右侧显示的图标（图 VB-5.48）。**DatePicker** 控件显示当前年份当前月份的日历（图 VB-5.49）。
- 10. 从日历中选择一个日期（图 VB-5.49）。所选日期显示在 **DatePicker** 控件的文本框中（图 VB-5.50）。

![](img/9862a98a1a2d3bb14334137965a1ec60_219_0.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_219_1.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_219_2.png)

您已经了解了 WPF 中使用的一些常见控件。接下来，我们继续学习如何在 WPF 中使用资源和样式。

## 使用资源和样式

考虑这样一种情况：您想要在 WPF 应用程序中的多个控件上应用相同的背景色。您可以设置所有这些控件的 **Background** 属性；但是，这可能相当繁琐且耗时。因此，为了简化此类常见属性的使用，您可以在 WPF 应用程序中将它们指定为资源。资源是指可由应用程序中的多个控件或元素使用的对象、元素或值。

您可以为任何控件或元素定义资源；但是，建议在根元素（如 **Window** 或 **Page** 元素）上定义资源。为某个元素定义的资源也适用于该元素的所有子元素。例如，如果您为以 **Grid** 元素作为子元素的 **Window** 元素定义资源，那么 **Window** 元素的资源也适用于 **Grid** 元素。此外，如果您为 **Grid** 元素定义资源，那么该资源也适用于其子元素。

![](img/9862a98a1a2d3bb14334137965a1ec60_220_0.png)

> **假设您有一个包含多个窗口的 WPF 独立应用程序，并且希望将某个资源应用于所有窗口，那么您需要在应用程序的 Application.xaml 文件中定义该资源。**

您可以使用元素的 **Resources** 属性在元素上定义资源。**Resources** 属性指的是资源字典，它是在特定控件或元素上定义的资源的集合。使用 **Resources** 属性，您可以在一个元素上定义任意数量的资源。您在元素上定义的每个资源都必须具有唯一键，该键是一个字符串，用于在资源字典中唯一标识该资源。唯一键通过 **x:Key** 属性分配给资源。在元素上定义资源的基本语法如下：

```xml
<elementName>
    <elementName.Resources>
        <resourceName x:Key="keyName" />
    </elementName.Resources>
</elementName>
```

在前面的语法中：

- **elementName**：指定义资源的元素名称
- **elementName.Resources**：指该元素的 **Resources** 属性
- **resourceName**：指所定义资源的名称
- **x:Key**：指资源的 **x:Key** 属性
- **keyName**：指资源的唯一键名

定义资源后，您可以通过将其引用为其他元素的属性值来使用它。定义资源后引用该资源的语法如下：

```xml
<elementName propertyName="{markupExtension keyName}">
    <content>...
</elementName>
```

在前面的语法中：

- **elementName**：指使用该资源的元素名称
- **propertyName**：指从资源中获取值的属性名称
- **markupExtension**：指标记扩展的名称
- **keyName**：指资源的键名

根据用于引用资源的标记扩展，资源有两种类型——静态资源和动态资源。

