
标签；在这种情况下，你使用前一节中定义的应用程序资源，通过其键值 Purpose 来检索它。标签文本以 25 单位的字体大小渲染，并应位于网格的第一行第一列。

WOW！这一行 XAML 真的很有分量！以下是其中发生的一些事情：

- **x:Name：** 此属性为 XAML 标签创建的对象分配一个变量名。这使你能够从代码后置文件中访问该对象。在本例中，被实例化的标签对象的变量名为 `lblPurpose`。
- **Content：** 分配给此属性的值可以是任何类型。默认情况下，你可以为其分配一个 `string` 值，它将像你认为的标准标签那样渲染。在 WPF 的现实中，`Content` 可以由任何内容组成：字符串、图像、用户控件的实例、文本框等等。更多信息请参阅本迷你书的第 2 章。
- **FontSize：** 标签字体的大小。需要注意的是，大小不是以磅表示的；它以设备无关单位表示。WPF 摆脱了像素和磅的概念，采用了通用的尺寸策略。将设备无关单位视为比率而非像素。例如，如果标签的包含元素为 100 单位 x 100 单位，则标签将以其大小的 ½ 渲染。
- **Grid.Row：** 标识要渲染标签的网格行。网格行集合是基于零的，这意味着第一行是第 0 行，第二行是第 1 行，依此类推。你还应注意 Label 类不包含名为 Grid 的属性。这里看到的是附加属性的概念。附加属性是一种相对于祖先控件的属性为当前控件分配上下文的方式。在本例中，你将标签分配为出现在其包含网格的第一行（行索引 0）。还请注意标签位于 `Grid` 标签内；这就是如何定位祖先 `Grid` 元素的方式。
- **Grid.Column：** 类似于 `Grid.Row`，此附加属性标识要渲染标签的网格列。`Grid.Row` 与 `Grid.Column` 一起标识标签所在的单元格。在本例中，你将标签分配为在其包含网格的第一列中渲染。网格列集合也是基于零的。

继续运行你的应用程序。你现在会在窗口上的标签中看到 Hello World。恭喜，你刚刚创建了你的第一个 WPF 应用程序！

完整解决方案可在 http://csharpfordummies.net 的章节下载中获得。

![](img/80ff26f06fc9ab951e1cd4257b867366_599_0.png)

![](img/80ff26f06fc9ab951e1cd4257b867366_599_1.png)

## 无论 XAML 能做什么，C# 做得更好！

任何你可以用 XAML 实现的功能都可以用 C# 实现。这在反向情况下不成立；不是所有你可以用 C# 完成的事情都能在 XAML 中完成。C# 是执行使用过程式代码且无法在 XAML 中表达的业务逻辑任务的明显选择。在以下步骤中，你将创建一个与前一节中创建的相同的 WPF 应用程序，这次使用 C# 来实现其功能：

1. 通过选择 文件 ▸ 新建项目 创建一个新项目。
2. 在 Visual C# 下，选择 Windows。
3. 选择 WPF 应用程序。
4. 将应用程序命名为 MyFirstCodeOnlyWPFApplication。
5. 单击 确定。
6. 打开 App.xaml.cs。
7. 通过向 App 类添加以下代码来重写 OnStartup 方法以包含 Purpose 应用程序资源的创建：

```csharp
protected override void OnStartup(StartupEventArgs e)
{
    //create and add the Purpose application resource
    string purpose = "Hello WPF World. in C#";
    this.Resources.Add("Purpose", purpose);

    base.OnStartup(e);
}
```

8. 打开 MainWindow.xaml 并通过添加以下属性为 Grid 元素命名：

```xml
x:Name="gridLayout"
```

9. 打开 MainWindow.xaml.cs，并在默认构造函数中，在 InitializeComponent 方法调用之后，添加以下代码：

```csharp
//define grid column and row
this.gridLayout.ColumnDefinitions.Add(new ColumnDefinition());
this.gridLayout.RowDefinitions.Add(new RowDefinition());

//obtain label content from the application resource, Purpose
string purpose = this.TryFindResource("Purpose") as string;
Label lblPurpose = new Label();
lblPurpose.Content = purpose;
lblPurpose.FontSize = 25;

//add label to the grid
this.gridLayout.Children.Add(lblPurpose);

//assign attached property values
Grid.SetColumn(lblPurpose, 0);
Grid.SetRow(lblPurpose, 0);
```

运行应用程序并观察结果产品与本章前面“深入！创建你的第一个 WPF 应用程序”一节中获得的产品相似。

![](img/80ff26f06fc9ab951e1cd4257b867366_601_0.png)

完整解决方案可在 http://csharpfordummies.net 网站的章节下载中获得。

## 第 2 章：了解 WPF 的基础知识

### 本章内容

- 布局应用程序
- 使用布局面板
- 使用网格
- 实现仅显示、输入和基于列表的控件

正如第 1 章所述，WPF 不仅带来了 Windows 应用程序外观和感觉的巨大转变，也改变了开发方式。从工具箱拖放控件到窗体上的日子早已一去不复返。即使在 WPF 中仍然可以拖放，你会发现直接在 XAML 中工作会更好、更开心。

曾经困难的事情现在相对简单。例如，在传统的 Windows 应用程序中，当用户更改窗体大小时，控件通常挤在角落，显示大片空白画布。唯一的解决办法是大量自定义代码或昂贵的第三方控件。WPF 将网页中的流式布局概念带入了 Windows 世界。

在 WinForms 的 GDI/GDI+ 世界中，修改控件样式或构建复杂外观是一项艰巨的任务。WPF 完全重新定义了控件范式，赋予你作为开发者的自由，让控件执行难以想象的任务——包括在按钮表面播放视频。然而，请记住，仅因为你可以做某事并不意味着你应该做！

在本章中，我们将使用 WPF 的布局过程来控制应用程序的布局，并向你介绍各种 WPF 控件。

### 使用 WPF 布局你的应用程序

传统的 Windows 窗体开发采用绝对值。控件的位置和大小在设计时决定，并基于开发人员机器的分辨率。当应用程序部署给用户时，在开发人员机器上看起来很棒的窗体现在可能看起来非常不同（并且可能完全无法使用），这是由于硬件分辨率差异造成的。

WPF 不依赖屏幕分辨率，而是以基于 *系统 DPI* 的设备无关单位（DIU）来测量 UI 元素。这使得在许多不同的硬件配置之间保持一致的外观成为可能。

WPF 布局基于 *相对* 值，并在运行时进行调整。当你将控件放置在布局容器中（参见下一节）时，渲染引擎仅将高度和宽度视为“建议”值。位置是相对于其他控件或容器的定义的。实际渲染是一个两步过程，首先测量所有控件（并查询它们的首选尺寸），然后相应地排列它们。如果控件会说话，对话可能如下：

布局引擎：“控件，你想要多少空间？”

*<这是测量阶段>*

控件：“我希望高度为 50 DIU，宽度为 100 DIU，并且在包含的 Grid 单元格中有 3 DIU 的边距。”

*布局引擎询问所有其他控件和布局容器。*

布局引擎：“抱歉，高度你只能有 40 DIU，但我可以满足你的其他请求。”

*<这是排列阶段>*

### 新技术，新术语

似乎每次微软推出新技术，我们都必须学习一套全新的术语。WPF 也不例外！变化的根源是我们所称的 Windows 窗体（WinForms）中的窗体和控件。以下是一些新术语：

- WinForms 中的 *Form* 在 WPF 中称为 *Window*。
- 放置在 WinForms Form 上的任何东西称为 *control*，而放置在 WPF Window 上的项目则称为 *UIElements*。
- *Panels* 是用于布局的 WPF UIElements。
- WPF 中的 *Control* 是一个可以接收焦点并响应用户事件的 UIElement。
- WPF 中的 *Content* 控件只能包含单个项目，该项目本身可以是其他 UIElements。
- WPF Window 类是一个专门的 Content 控件。
