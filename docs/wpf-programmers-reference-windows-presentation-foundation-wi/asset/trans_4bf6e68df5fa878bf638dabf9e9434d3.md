
为了在 XAML 文件与后台代码（code-behind）之间实现分离，程序使用了一组独立的程序来执行实际工作。事件处理程序捕获控件事件并调用这些程序。

以下代码展示了“蓝色皮肤”如何在表单顶部侧定义其红色开关皮肤：

```xml
<Grid
  xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
  xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
  Tag="Blue">

  <!-- 省略大量代码 -->

  <Ellipse Name="Skin" Width="10" Height="10"
           Canvas.Left="70" Canvas.Top="13"
           Cursor="Cross" Tooltip="Change Skin"
           Fill="HotPink" Stroke={StaticResource brRedStroke}
           StrokeThickness="2" Tag="Red.xaml" />

  <!-- 省略大量代码 -->
</Grid>
```

代码片段以 `Grid` 控件作为根元素。（可以使用其他控件作为文件的根元素，但使用 `Grid` 非常方便，因为 Visual Studio WPF 窗口设计器知道当根元素为 `Grid` 时如何显示皮肤。）根元素的 `Tag` 属性被设置为它的名称，在本例中为 `Blue`。

显示的代码省略了所有其他控件，只保留了名称 `ellSkin` 和它的 `Tag` `Red.xaml`。`Tag` 属性用于在点击圆形时查找要加载哪个 XAML 文件。

暂忽略这是如何由其事件处理程序控制的，以下代码显示了控件执行的事件处理程序。由于此事件由该控件和红色皮肤的“切换皮肤”多边形（左上角的三角形）共享，因此它命名为 `pSkin.MouseDown`。

```csharp
private void MouseDown(object sender, MouseEventArgs e)
{
  FrameworkElement element = (FrameworkElement)sender;
  LoadSkin(element.Tag.ToString());
}
```

这段代码获取触发事件的元素（可以是蓝色皮肤的 `Ellipse` 或红色皮肤的 `Polygon`），读取该元素的 `Tag` 属性以查看要加载哪个 XAML 文件，并将文件名传递给函数 `LoadSkin`。

`LoadSkin` 函数使用以下代码加载 XAML 皮肤文件。为了节省空间，代码仅展示了部分控制控件到其事件处理程序的语句。

```csharp
// 加载皮肤文件并绑定事件处理程序。
private void LoadSkin(string skin_file)
{
    // 加载控件。
    FrameworkElement element =
        (FrameworkElement)Application.LoadComponent(
            new Uri(skin_file, UriKind.Relative));
    this.Content = element;

    // 绑定事件处理程序。
    Button btn;
    Polygon pgn;
    Rectangle rect;
    Grid grd;
    Ellipse ell;

    switch (element.ToString())
    {
        case "Red":
            btn = (Button)element.FindName("btnRepairDisk");
            btn.Click += new RoutedEventHandler(btnRepairDisk_Click);

            // 省略其他控件的代码
            break;
        case "Blue":
            // 省略大量代码

            // 使用与 rectMove 相同的事件处理程序。
            ell = (Ellipse)element.FindName("ellMove");
            ell.MouseDown += new System.Windows.Input.MouseEventHandler(
                rectMove_MouseDown);

            grd = (Grid)element.FindName("grdExit");
            grd.MouseDown += new System.Windows.Input.MouseEventHandler(
                grdExit_MouseDown);
            break;
    }
}
```

皮肤接口（SkinInterfaces）

代码首先使用 WPF 组件方法加载所需的 XAML 皮肤文件。它将窗口的主内容设置为来自文件的根元素，以便显示控件。

接下来，代码检查新加载元素的 `Tag` 属性，以查看它现在显示的是红色皮肤还是蓝色皮肤。根据加载了哪种皮肤，代码会在皮肤中寻找特定的控件并连接它们的的事件处理程序。

例如，如果红色皮肤可见，代码将使用 `FindName` 定位 `btnRepairDisk` 按钮，并将 `btnRepairDisk_Click` 事件处理程序添加到其 `Click` 事件中。

之前的代码省略了绝大多数连接到事件处理程序的控件代码。然而，它确实展示了代码如何找到 `ellSkin`（“切换皮肤”圆形）并将其 `pgnSkin_MouseDown` 添加到其 `MouseDown` 事件中。

此处未显示用于绑定控件的代码。

程序的最后一部分在窗口的构造函数中，如下代码所示。在窗口初始化后，代码调用 `LoadSkin` 以从红色皮肤开始。

```csharp
public Window()
{
    this.InitializeComponent();

    // 在此点下方插入对象创建时所需的代码。

    // 从红色皮肤开始。
    LoadSkin("Red.xaml");
}
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_338_0.png)

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_338_1.png)

这就完成了程序的生命周期。当程序启动时，它调用 `LoadSkin` 加载红色皮肤。`LoadSkin` 加载控件并绑定它们的事件处理程序。特别是，它为 `pgnSkin` “切换皮肤”控件的 `MouseDown` 事件挂载了事件处理程序。当你点击多边形时，`pgnSkin_MouseDown` 事件执行并调用 `LoadSkin` 重新开始该过程。

[/content]

皮肤接口（SkinInterfaces）

代码首先使用 WPF 组件方法加载所需的 XAML 皮肤文件。它将窗口的主内容设置为来自文件的根元素，以便显示控件。

接下来，代码检查新加载元素的 `Tag` 属性，以查看它现在显示的是红色皮肤还是蓝色皮肤。根据加载了哪种皮肤，代码会在皮肤中寻找特定的控件并连接它们的事件处理程序。

例如，如果红色皮肤可见，代码将使用 `FindName` 定位 `btnRepairDisk` 按钮，并将 `btnRepairDisk_Click` 事件处理程序添加到其 `Click` 事件中。

之前的代码省略了绝大多数连接到事件处理程序的控件代码。然而，它确实展示了代码如何找到 `ellSkin`（“切换皮肤”圆形）并将其 `pgnSkin_MouseDown` 添加到其 `MouseDown` 事件中。

此处未显示用于绑定控件的代码。

程序的最后一部分在窗口的构造函数中，如下代码所示。在窗口初始化后，代码调用 `LoadSkin` 以从红色皮肤开始。

```csharp
public Window()
{
    this.InitializeComponent();

    // 在此点下方插入对象创建时所需的代码。

    // 从红色皮肤开始。
    LoadSkin("Red.xaml");
}
```
（注：由于用户提供的待翻译文本包含重复段落，根据指令“一定不要重复输出原文”的原则，此处译文应仅翻译一次内容。以下为重新整理的最终译文：）

---

**抱歉，上述回复在处理重复时出现了逻辑混乱。以下是针对您提供文本的正确唯一译文：**

[content]
为了在 XAML 文件与后台代码之间实现分离，程序使用了一组独立的程序来执行实际工作。事件处理程序捕获控件事件并调用这些程序。

以下代码展示了“蓝色皮肤”如何在表单顶部侧定义其红色开关皮肤：

```xml
<Grid
  xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
  xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
  Tag="Blue">

  <!-- 省略大量代码 -->

  <Ellipse Name="Skin" Width="10" Height="10"
           Canvas.Left="70" Canvas.Top="13"
           Cursor="Cross" Tooltip="Change Skin"
           Fill="HotPink" Stroke={StaticResource brRedStroke}
           StrokeThickness="2" Tag="Red.xaml" />

  <!-- 省略大量代码 -->
</Grid>
```

代码片段以 `Grid` 控件作为根元素。（可以使用其他控件作为文件的根元素，但使用 `Grid` 非常方便，因为 Visual Studio WPF 窗口设计器知道当根元素为 `Grid` 时如何显示皮肤。）根元素的 `Tag` 属性被设置为它的名称，在本例中为 `Blue`。

显示的代码省略了所有其他控件，只保留了名称 `ellSkin` 和它的 `Tag` `Red.xaml`。`Tag` 属性用于在点击圆形时查找要加载哪个 XAML 文件。

暂忽略这是如何由其事件处理程序控制的，以下代码显示了控件执行的事件处理程序。由于此事件由该控件和红色皮肤的“切换皮肤”多边形（左上角的三角形）共享，因此它命名为 `pSkin.MouseDown`。

```csharp
private void MouseDown(object sender, MouseEventArgs e)
{
  FrameworkElement element = (FrameworkElement)sender;
  LoadSkin(element.Tag.ToString());
}
```

这段代码获取触发事件的元素（可以是蓝色皮肤的 `Ellipse` 或红色皮肤的 `Polygon`），读取该元素的 `Tag` 属性以查看要加载哪个 XAML 文件，并将文件名传递给函数 `LoadSkin`。

`LoadSkin` 函数使用以下代码加载 XAML 皮肤文件。为了节省空间，代码仅展示了部分控制控件到其事件处理程序的语句。

```csharp
// 加载皮肤文件并绑定事件处理程序。
private void LoadSkin(string skin_file)
{
    // 加载控件。
    FrameworkElement element =
        (FrameworkElement)Application.LoadComponent(
            new Uri(skin_file, UriKind.Relative));
    this.Content = element;

    // 绑定事件处理程序。
    Button btn;
    Polygon pgn;
    Rectangle rect;
    Grid grd;
    Ellipse ell;

    switch (element.ToString())
    {
        case "Red":
            btn = (Button)element.FindName("btnRepairDisk");
            btn.Click += new RoutedEventHandler(btnRepairDisk_Click);

            // 省略其他控件的代码
            break;
        case "Blue":
            // 省略大量代码

            // 使用与 rectMove 相同的事件处理程序。
            ell = (Ellipse)element.FindName("ellMove");
            ell.MouseDown += new System.Windows.Input.MouseEventHandler(
                rectMove_MouseDown);

            grd = (Grid)element.FindName("grdExit");
            grd.MouseDown += new System.Windows.Input.MouseEventHandler(
                grdExit_MouseDown);
            break;
    }
}
```

皮肤接口（SkinInterfaces）

代码首先使用 WPF 组件方法加载所需的 XAML 皮肤文件。它将窗口的主内容设置为来自文件的根元素，以便显示控件。

接下来，代码检查新加载元素的 `Tag` 属性，以查看它现在显示的是红色皮肤还是蓝色皮肤。根据加载了哪种皮肤，代码会在皮肤中寻找特定的控件并连接它们的的事件处理程序。

例如，如果红色皮肤可见，代码将使用 `FindName` 定位 `btnRepairDisk` 按钮，并将 `btnRepairDisk_Click` 事件处理程序添加到其 `Click` 事件中。

之前的代码省略了绝大多数连接到事件处理程序的控件代码。然而，它确实展示了代码如何找到 `ellSkin`（“切换皮肤”圆形）并将其 `pgnSkin_MouseDown` 添加到其 `MouseDown` 事件中。

此处未显示用于绑定控件的代码。

程序的最后一部分在窗口的构造函数中，如下代码所示。在窗口初始化后，代码调用 `LoadSkin` 以从红色皮肤开始。

```csharp
public Window()
{
    this.InitializeComponent();

    // 在此点下方插入对象创建时所需的代码。

    // 从红色皮肤开始。
    LoadSkin("Red.xaml");
}
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_338_0.png)

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_338_1.png)

这就完成了程序的生命周期。当程序启动时，它调用 `LoadSkin` 加载红色皮肤。`LoadSkin` 加载控件并绑定它们的事件处理程序。特别是，它为 `pgnSkin` “切换皮肤”控件的 `MouseDown` 事件挂载了事件处理程序。当你点击多边形时，`pgnSkin_MouseDown` 事件执行并调用 `LoadSkin` 重新开始该过程。
