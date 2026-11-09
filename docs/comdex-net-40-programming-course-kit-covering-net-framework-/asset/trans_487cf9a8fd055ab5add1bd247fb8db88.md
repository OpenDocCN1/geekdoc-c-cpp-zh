

```vb
End Property
Public Property Age() As Integer
    Get
        Return m_Age
    End Get
    Set(ByVal value As Integer)
        m_Age = value
    End Set
End Property
End Class
```

代码清单 5.12 中突出显示的代码显示了 Student 类的定义。在类定义中，我们定义了三个变量 m_ID、m_Name 和 m_Age，它们分别对应三个属性 ID、Name 和 Age。我们还为这些属性中的每一个定义了 Get 和 Set 过程。当从属性中检索数据时，会调用该属性的 Get 过程；当向属性分配数据时，会调用该属性的 Set 过程。

- 10. 在设计视图中选择 Window 控件，然后在属性窗口中选择事件选项卡，以显示该控件的事件（图 VB-5.42）。
- 11. 选择 Loaded 事件，并双击该事件前面的组合框内部，以在代码编辑器中创建该事件的事件处理程序，如图 VB-5.42 所示。

![](img/9862a98a1a2d3bb14334137965a1ec60_215_0.png)

图 VB-5.42

- 12. 将突出显示的代码片段（如代码清单 5.13 所示）添加到代码编辑器中：

**代码清单 5.13：显示 Window 控件的 Loaded 事件处理程序的代码**

```vb
Private Sub Window_Loaded(ByVal sender As System.Object, ByVal e As System.Windows.RoutedEventArgs) Handles MyBase.Loaded
dataGrid1.Items.Add(New Student With {.ID = "ST01", .Name = "John", .Age = 14})
dataGrid1.Items.Add(New Student With {.ID = "ST02", .Name = "Andrew", .Age = 11})
dataGrid1.Items.Add(New Student With {.ID = "ST03", .Name = "Katie", .Age = 12})
Dim col1 As DataGridTextColumn = New DataGridTextColumn()
col1.Binding = New Binding("ID")
Dim col2 As DataGridTextColumn = New DataGridTextColumn()
col2.Binding = New Binding("Name")
Dim col3 As DataGridTextColumn = New DataGridTextColumn()
col3.Binding = New Binding("Age")
dataGrid1.Columns.Add(col1)
dataGrid1.Columns.Add(col2)
dataGrid1.Columns.Add(col3)
col1.Header = "Student ID"
col2.Header = "Name of Student"
col3.Header = "Age"
End Sub
```

代码清单 5.13 显示了 Window 控件的 Loaded 事件处理程序的代码。在突出显示的行中，我们首先通过调用 Items 集合对象的 Add 方法，向 DataGrid 控件 dataGrid1 的 Items 集合添加三个项。添加到 Items 集合的项是我们在代码清单 5.12 中创建的 Student 类的对象。之后，我们通过创建 DataGridTextColumn 类的对象来创建三个列，并通过设置列对象的 **Binding** 属性将这些列绑定到 ID、Name 和 Age 属性。接着，我们将这些列添加到 dataGrid1 的 **Columns** 集合中。最后，我们为三个列指定列标题。

- 13. **按**键盘上的 F5 键运行应用程序。应用程序的输出出现，如图 VB-5.43 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_216_0.png)

如图 VB-5.43 所示，**DataGrid** 控件的数据显示在**学生 ID、学生姓名**和**学生年龄**列下。现在让我们讨论 **Calendar** 控件。

### 使用 Calendar 控件

**Calendar** 控件是 WPF 4.0 中引入的另一个新 WPF 控件。它是一个可视化日历，用户可以在其中选择特定日期。每当在 **Calendar** 控件中选择一个日期时，就会为所选日期触发一个事件。**Calendar** 控件是 **Calendar** 类的实例，该类位于 **System.Windows.Controls** 命名空间中。表 5.12 列出了 **Calendar** 类的值得注意的属性：

**表 5.12：Calendar 类的值得注意的属性**

| 属性 | 描述 |
|---|---|
| BlackoutDates | 检索在 Calendar 控件中标记为不可选择的日期集合 |
| DisplayDate | 检索或设置要在 Calendar 控件中显示的日期 |
| DisplayDateEnd | 检索或设置 Calendar 控件中可用日期范围的最后日期 |
| DisplayDateStart | 检索或设置 Calendar 控件中可用的第一个日期 |
| DisplayMode | 检索或设置一个值，该值指示 Calendar 控件显示月份、年份还是十年 |
| FirstDayOfWeek | 检索或设置 Calendar 控件中视为一周开始的那一天 |
| SelectedDate | 检索或设置 Calendar 控件中当前选定的日期 |
| SelectedDates | 检索 Calendar 控件中选定日期的集合 |
| SelectionMode | 检索或设置一个值，该值指示 Calendar 控件中允许哪种选择 |

执行以下步骤，在 WPF 独立应用程序中使用 **Calendar** 控件：

- 1. **启动** Visual Studio 2010。
- 2. **选择**菜单栏中的“文件”→“新建”→“项目”。将打开**新建项目**对话框。
- 3. 在**新建项目**对话框左窗格的**已安装模板**部分中**选择** Visual Basic→Windows。
- 4. 在中间窗格中**选择** **WPF 应用程序**模板以创建 WPF 独立应用程序。
- 5. 在**名称**文本框中输入应用程序名称 **MyCalendar**（也可在 CD 上获取），并在**位置**组合框中输入应用程序的适当位置。
- 6. **单击** **确定**按钮关闭**新建项目**对话框并创建 **MyCalendar** 应用程序。
- 7. 用代码清单 5.14 中给出的代码替换 **MainWindow.xaml** 文件 XAML 视图中的默认代码：

**代码清单 5.14：显示 MainWindow.xaml 文件的代码**

```xml
<Window x:Class="MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="MyCalendar Application" Height="300" Width="300">
    <Grid>
        <Calendar Name="calendar1" Height="170" Width="185" Margin="10,10,0,0"
                  HorizontalAlignment="Left" VerticalAlignment="Top" />
        <Button Content="Show Dates in Year Mode" Height="23"
                HorizontalAlignment="Left" Margin="12,180,0,0" Name="Button1"
                VerticalAlignment="Top" Width="156" />
        <Button Content="Limit Dates Displayed" Height="23"
                HorizontalAlignment="Left" Margin="12,222,0,0" Name="Button2"
                VerticalAlignment="Top" Width="133" />
    </Grid>
</Window>
```

在代码清单 5.14 中，**Window** 元素的 **Title** 属性设置为 **MyCalendar 应用程序**。这意味着文本 **MyCalendar 应用程序** 会显示在窗口的标题栏上。之后，我们向 **Grid** 控件添加了一个 **Calendar** 控件和两个 **Button** 控件。第一个和第二个 **Button** 控件的 **Content** 属性分别设置为 **以年份模式显示日期** 和 **限制显示的日期**。

- 8. *双击* **MainWindow.xaml** 文件设计视图中的 **以年份模式显示日期** 按钮。**以年份模式显示日期** 按钮的 Click 事件的事件处理程序会自动添加到 **MainWindow.xaml.vb** 文件中。

- 9. 在 **以年份模式显示日期** 按钮的 Click 事件的事件处理程序中添加以下突出显示的代码片段：

```vb
Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.Windows.RoutedEventArgs) Handles Button1.Click
    calendar1.DisplayMode = CalendarMode.Year
End Sub
```

在前面的代码片段中，**Button1_Click** 是第一个 Button 控件 **Button1**（或 **以年份模式显示日期** 按钮）的 Click 事件的事件处理程序。在运行时单击 **以年份模式显示日期** 按钮时，将执行此事件处理程序。在突出显示的行中，我们将 **Calendar** 控件 calendar1 的 **DisplayMode** 属性设置为 **CalendarMode.Year**。这使 Calendar 控件中的日期以年份模式显示。

- 10. *切换到 MainWindow.xaml 文件。*

- 11. *双击* **MainWindow.xaml** 文件设计视图中的 **限制显示的日期** 按钮。**限制显示的日期** 按钮的 Click 事件的事件处理程序会自动添加到 **MainWindow.xaml.vb** 文件中。

- 12. 在 **限制显示的日期** 按钮的 Click 事件的事件处理程序中添加以下突出显示的代码片段：

```vb
Private Sub Button2_Click(ByVal sender As System.Object, ByVal e As System.Windows.RoutedEventArgs) Handles Button2.Click
    calendar1.DisplayDateStart = Convert.ToDateTime("09/15/2010")
    calendar1.DisplayDateEnd = Convert.ToDateTime("09/30/2010")
End Sub
```

在前面的代码片段中，**Button2_Click** 是第二个 Button 控件 **Button2**（或 **限制显示的日期** 按钮）的 Click 事件的事件处理程序。在运行时单击 **限制显示的日期** 按钮时，将执行此事件处理程序。在突出显示的行中，我们设置了 **Calendar** 控件的 **DisplayDateStart** 和 **DisplayDateEnd** 属性，以限制 Calendar 控件中显示的日期。**DisplayDateStart** 属性指的是 Calendar 控件中显示的第一个日期，**DisplayDateEnd** 属性指的是 Calendar 控件中显示的最后一个日期。

