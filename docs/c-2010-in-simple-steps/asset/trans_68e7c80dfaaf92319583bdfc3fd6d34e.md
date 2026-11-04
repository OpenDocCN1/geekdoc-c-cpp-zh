
控件。DataGrid 控件的 `RowBackground` 属性被赋值为 Khaki，而 `AlternatingRowBackground` 属性被赋值为 Beige，这意味着 DataGrid 中每隔一行的背景色为米色。

我们在应用程序中创建的 DataGrid 不会显示任何数据。

5 将清单 7.14 中突出显示的代码添加到 MainWindow.xaml.cs 文件中，以编程方式向 DataGrid 填充数据：

## 清单 7.14：显示用于填充 DataGrid 控件的代码

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Imaging;
using System.Windows.Navigation;
using System.Windows.Shapes;
namespace DataGridDemo
{
    /// <summary>
    /// Interaction logic for MainWindow.xaml
    /// </summary>
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();
            dataGrid1.Items.Add(new Student() { ID="ST01", Name = "John", Age = 14});
            dataGrid1.Items.Add(new Student() { ID="ST02", Name = "Andrew", Age = 11});
            dataGrid1.Items.Add(new Student() { ID="ST03", Name = "Katie", Age = 16});
            DataGridTextColumn col1 = new DataGridTextColumn();
            col1.Binding = new Binding("ID");
            DataGridTextColumn col2 = new DataGridTextColumn();
            col2.Binding = new Binding("Name");
            DataGridTextColumn col3 = new DataGridTextColumn();
            col3.Binding = new Binding("Age");
            dataGrid1.Columns.Add(col1);
            dataGrid1.Columns.Add(col2);
            dataGrid1.Columns.Add(col3);
            col1.Header = "Student_ID";
            col2.Header = "Name of Student";
            col3.Header = "Age of Student";
        }
        public class Student
        {
            private string name;
            private int age;
            private string id;
            public string Name
            {
                get;
                set;
            }
        }
public int Age
{
    get;
    set;
}
public string ID
{
    get;
    set;
}
}
}
```

在清单 7.14 中，一个名为 Student 的类被添加到 DataGridDemo 应用程序的 MainWindow.xaml 文件中。

Student 类包含三个私有数据成员：id、name 和 age。同时定义了三个属性 ID、Name 和 Age，用于赋值和检索 Student 类中定义的 id、name 和 age 数据成员的值。在分部类 MainWindow 的构造函数内部，通过以下代码行将 Student 类的 ID、Name 和 Age 属性的值添加到 DataGrid 控件 dataGrid1 的 Items 集合中：

```
dataGrid1.Items.Add(new Student() { ID="ST01", Name = "John", Age = 14});
dataGrid1.Items.Add(new Student() { ID="ST02", Name = "Andrew", Age = 11});
dataGrid1.Items.Add(new Student() { ID="ST03", Name = "Katie", Age = 16});
```

为了在 dataGrid1 控件中显示 ID、Name 和 Age 属性的值，创建了三个列 col1、col2 和 col3，并分别将它们绑定到 ID、Name 和 Age 属性，使用以下代码行：

```
DataGridTextColumn col1 = new DataGridTextColumn();
col1.Binding = new Binding("ID");
DataGridTextColumn col2 = new DataGridTextColumn();
col2.Binding = new Binding("Name");
DataGridTextColumn col3 = new DataGridTextColumn();
col3.Binding = new Binding("Age");
```

请注意，DataGridTextColumn 是一个用于在 DataGrid 控件中显示文本内容的类。然后通过以下代码行将 col1、col2 和 col3 列添加到 dataGrid1 控件中：

```
dataGrid1.Columns.Add(col1);
dataGrid1.Columns.Add(col2);
dataGrid1.Columns.Add(col3);
```

通过以下代码行设置 col1、col2 和 col3 列的标题，以清楚标识 dataGrid1 控件中每列显示的数据：

```
col1.Header = "Student_ID";
col2.Header = "Name of Student";
col3.Header = "Age of Student";
```

按 F5 键运行 DataGridDemo 应用程序。输出结果如图 C#7.30 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_252_0.png)

图 C#7.30

在图 C#7.30 中，数据在 Student_ID、Name of Student 和 Age of Student 列下显示在 DataGrid 控件中。接下来，让我们讨论 Calendar 控件。

## 使用 Calendar 控件

Calendar 控件是 WPF 最新版本中引入的一个新控件。它是一个可视化日历，用户可以在其中选择特定日期。每当在 Calendar 控件上选择某个日期时，都会在所选日期上触发一个事件。Calendar 控件位于 System.Windows.Controls 命名空间中，该命名空间位于 PresentationFramework 程序集中。Calendar 控件继承自 Control 类。表 7.12 列出了 Calendar 控件的一些重要属性：

表 7.12：Calendar 控件的显著属性

| 属性 | 说明 |
|---|---|
| BlackOutDates | 检索在 Calendar 控件中标记为不可选择的日期集合 |
| DisplayDate | 检索或设置要在 Calendar 控件中显示的日期 |
| DisplayDateEnd | 检索或设置 Calendar 控件中可用的日期范围的最后一天 |
| DisplayDateStart | 检索或设置 Calendar 控件中可用的第一天 |
| DisplayMode | 检索或设置指示 Calendar 控件显示月、年还是十年的值 |
| FirstDayOfWeek | 检索或设置在 Calendar 控件中被视为一周开始日的日期 |
| SelectedDate | 检索或设置 Calendar 控件中当前选定的日期 |
| SelectedDates | 检索 Calendar 控件中选定日期的集合 |
| SelectionMode | 检索或设置指示 Calendar 控件允许何种选择类型的值 |

让我们创建一个名为 CalendarDemo 的独立 WPF 应用程序来演示 Calendar 控件的使用。为此，请执行以下步骤：

- 1. 重复本章“使用 Grid 控件”一节中创建 GridDemo 应用程序时执行的步骤 1 到 3。
- 2. 在“名称”文本框中输入名称 CalendarDemo，并在“位置”组合框中为应用程序指定合适的位置。
- 3. 单击“确定”按钮。CalendarDemo 应用程序即创建完成。
- 4. 将清单 7.15 中突出显示的代码添加到 MainWindow.xaml 文件中：

### 清单 7.15：使用 Calendar 控件

```xml
<Window x:Class="CalendarDemo.MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Title="CalendarDemo" Height="300" Width="300">
<Grid>
    <Calendar Name="calendar1" Height="170" Width="185" Margin="10,10,0,0" HorizontalAlignment="Left" VerticalAlignment="Top"/>
</Grid>
</Window>
```

在清单 7.15 中，将一个 Calendar 控件添加到 Grid 控件中。设置了 Calendar 控件的 Width 和 Height 属性，而 Name 属性用于唯一标识该 Calendar 控件：

5 按 F5 键运行 CalendarDemo 应用程序。输出结果如图 C#7.31 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_253_0.png)

图 C#7.31

在图 C#7.31 中，您会看到 Calendar 控件中默认选中了一个日期。这是当前日期或今天的日期。您可以更改 Calendar 控件的 DisplayDate 属性，以显示您喜欢的任何日期。

Calendar 控件的 DisplayMode 属性指定 Calendar 的显示格式，可以是月、年或十年。

6 将清单 7.15 中的代码替换为清单 7.16 中突出显示的代码：

### 清单 7.16：显示要添加到 MainWindow.xaml 文件中的代码

```xml
<Window x:Class="CalendarDemo.MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Title="CalendarDemo" Height="300" Width="300">
<Grid>
    <Calendar Name="calendar1" Height="170" Width="185" Margin="10,10,0,0" DisplayMode="Year" HorizontalAlignment="Left" VerticalAlignment="Top"/>
</Grid>
</Window>
```

7 再次按 F5 键运行 CalendarDemo 应用程序。输出结果如图 C#7.32 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_253_1.png)

图 C#7.32

8 同样，将清单 7.16 中显示的代码替换为清单 7.17 中突出显示的代码，以限制您想要在 Calendar 控件中显示的日期：

### 清单 7.17：显示用于限制 Calendar 控件中显示日期的代码

```xml
<Window x:Class="CalendarDemo.MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
```

