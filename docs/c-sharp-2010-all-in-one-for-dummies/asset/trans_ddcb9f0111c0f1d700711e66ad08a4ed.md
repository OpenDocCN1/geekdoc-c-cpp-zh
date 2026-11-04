
应用程序。应用范围的资源可供项目中定义的所有 Windows 和用户控件使用。请按照以下步骤操作：

- 1. **在 `mscorlib.dll` 程序集中添加 System 命名空间。**
  这里是 `String` 类所在的位置。

- 2. **为此，将以下命名空间添加到 `App.xaml` 根元素：**
  `xmlns:sys="clr-namespace:System;assembly=mscorlib"`
  `String` 类现在可在整个 `App.xaml` 文档中使用。

- 3. **在 `Application.Resources` 标签之间创建资源，添加以下 `String` 元素：**
  `<sys:String x:Key="Purpose">Hello WPF World!</sys:String>`
  该元素实例化一个类型为 `String` 的对象，初始化为值 Hello WPF World!，并以键 Purpose 为键。此资源现在可在整个 `MyFirstWPFApplication` 应用程序中通过请求资源“Purpose”来使用。

### 列表 1-2：已更新的 App.xaml，其中定义了资源和 System 命名空间

```xml
<Application x:Class="MyFirstWPFApplication.App"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:sys="clr-namespace:System;assembly=mscorlib"
    StartupUri="MainWindow.xaml">
    <Application.Resources>
        <sys:String x:Key="Purpose">Hello WPF World!</sys:String>
    </Application.Resources>
</Application>
```

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_575_0.png)

你可能会注意到 `Application.Resource` 标签看起来有点奇怪。`Application.Resources` 并不会像大多数 XAML 元素那样定义一个类。它实际上是将值赋给其包含的 Application 对象的 Resources 属性。

这种类型的标签称为 *属性元素*，它是一个表示对象属性或属性的 XML 元素。当将复杂对象分配给无法以简单字符串值表示的对象的属性时，会使用属性元素。属性元素必须包含在父元素的标签内——在本例中，在 Application 标签内。

## 让应用程序执行某些操作

如果按原样运行应用程序，除了显示一个空窗口外不会发生太多事情。空窗口是在 `MainWindow.xaml` 中定义的那个窗口。

App.xaml 是 WPF 应用程序的入口点。在 App.xaml 中，StartupUri 值定义了应用程序启动时显示的窗口。在本例中，StartupUri 的值是 MainWindow.xaml。

让我们在 MainWindow.xaml 中添加一个标签，以显示我们在 Resources 中定义的 String 的用途。只需按照以下步骤操作：

- 1. 打开 MainWindow.xaml。
- 2. 在 Grid 标签之间，通过添加以下 XAML 标记定义一个具有单行单列的网格：
- 3. 在 Grid.RowDefinitions 属性实体正下方，使用以下 XAML 创建一个标签：

```
<Grid.ColumnDefinitions>
<ColumnDefinition></ColumnDefinition>
</Grid.ColumnDefinitions>
<Grid.RowDefinitions>
<RowDefinition></RowDefinition>
</Grid.RowDefinitions>
```

每个列和行均由 Grid 中包含的 ColumnDefinition 和 RowDefinition 元素定义，分别为 ColumnDefinitions 和 Grid.RowDefinitions 属性。如果要添加更多列，只需向 Grid.ColumnDefinitions 属性实体添加另一个 ColumnDefinition 元素即可。添加行的操作相同：向 Grid.RowDefinitions 属性实体添加额外的 RowDefinition 元素。

```
<Label x:Name="lblPurpose" Content="{StaticResource Purpose}" FontSize="25" Grid.Row="0" Grid.Column="0" />
```

此标记使用变量 lblPurpose 实例化一个可供代码隐藏文件 (MainWindow.xaml.cs) 访问的 WPF Label 对象。Content 属性包含要在标签中显示的文本；在本例中，我们将使用前一节中定义的应用程序资源，通过其键值 Purpose 检索它。标签文本以 25 单位的字体大小呈现，并应位于网格的第一行第一列中。

WOW！这一行 XAML 真的包含了很多内容！让我们回顾一下其中发生的一些事情：

- x:Name：此属性为 XAML 标签创建的对象分配一个变量名。这使你能够从代码隐藏文件中访问该对象。在本例中，被实例化的标签对象的变量名为 lblPurpose。
- Content：分配给此属性的值可以是任何类型。默认情况下，你可以为其分配字符串值，它将像你认为的标准标签那样呈现。在 WPF 的现实中，Content 可以由任何内容组成：字符串、图像、用户控件的实例、文本框等等。更多信息，请参阅本迷你书的第 2 章。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_576_0.png)

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_576_1.png)

- **FontSize：** 标签字体的大小。需要注意的是，大小不是以磅表示的；它以设备无关单位表示。WPF 摆脱了像素和磅的概念，采用了通用的尺寸策略。将设备无关单位视为比率而非像素。例如，如果标签的包含元素为 100 单位乘 100 单位，则标签将以其大小的 ½ 呈现。

- **Grid.Row：** 标识要呈现标签的网格行。网格行集合是基于零的，这意味着第一行为第 0 行，第二行为第 1 行，以此类推。你还应注意，Label 类不包含名为 Grid 的属性。你在这里看到的是附加属性的概念。附加属性是一种相对于祖先控件的属性为当前控件分配上下文的方式。在本例中，我们将标签分配为在其包含的网格的第一行（行索引 0）中显示。还请注意，标签位于 Grid 标签内；这就是如何定位祖先 Grid 元素的方式。

- **Grid.Column：** 与 Grid.Row 类似，此附加属性标识要呈现标签的网格列。Grid.Row 和 Grid.Column 两个属性共同标识标签所在的单元格。在本例中，我们将标签分配为在其包含的网格的第一列中呈现。网格列集合也是基于零的。

继续运行你的应用程序，你现在将在窗口上的标签中看到 Hello World 显示。恭喜你，你刚刚创建了你的第一个 WPF 应用程序！

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_577_0.png)

完整解决方案可在 www.csharpfordummies.net 的章节下载中获得。

## XAML 能做的，C# 做得更好！

使用 XAML 实现的任何内容都可以用 C# 实现。这在反向情况下不成立；不是 C# 中能做的一切都可以在 XAML 中完成。C# 是执行使用过程式代码无法在 XAML 中表达的业务逻辑任务的明显选择。让我们创建一个与我们刚刚创建的相同的 WPF 应用程序，这次使用 C# 实现其功能。你需要做的就是：

- 1. **通过选择 文件 ⇨ 新建项目 来创建一个新项目。**
- 2. **在 Visual C# 下，选择 Windows。**
- 3. **选择 WPF 应用程序。**
- 4. **将应用程序命名为 MyFirstCodeOnlyWPFApplication。**
- 5. **单击 确定。**

Visual Studio 创建解决方案和项目结构。

- 6. **打开 App.xaml.cs。**
- 7. **重写 OnStartup 方法**，通过向 App 类添加以下代码来包含 Purpose 应用程序资源的创建：

```
protected override void OnStartup(StartupEventArgs e)
{
    // create and add the Purpose application resource
    string purpose = "Hello WPF World, in C#";
    this.Resources.Add("Purpose", purpose);

    base.OnStartup(e);
}
```

- 8. **打开 MainWindow.xaml，并通过添加以下属性为 Grid 元素命名：**

```
x:Name="gridLayout"
```

- 9. **打开 MainWindow.xaml.cs，并在默认构造函数中，在 InitializeComponent 方法调用之后，添加以下代码：**

```
// define grid column and row
this.gridLayout.ColumnDefinitions.Add(new ColumnDefinition());
this.gridLayout.RowDefinitions.Add(new RowDefinition());

// obtain label content from the application resource, Purpose
string purpose = this.TryFindResource("Purpose") as string;
Label lblPurpose = new Label();
lblPurpose.Content = purpose;
lblPurpose.FontSize = 25;

// add label to the grid
this.gridLayout.Children.Add(lblPurpose);

// assign attached property values
Grid.SetColumn(lblPurpose, 0);
Grid.SetRow(lblPurpose, 0);
```

运行应用程序并观察结果产品与本章前面“深入！创建你的第一个 WPF 应用程序”一节中获得的产品相似。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_578_0.png)

完整解决方案可在 www.csharpfordummies.net 网站的章节下载中获得。

