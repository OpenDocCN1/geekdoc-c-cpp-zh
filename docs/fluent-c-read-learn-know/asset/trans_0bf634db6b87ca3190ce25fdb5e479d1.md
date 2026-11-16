

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_515_0.png)

## XAML 基础

让我们通过将 XAML 标记与你已经熟悉的 C# 进行比较，来开始对 XAML 的考察。以下代码片段生成相同的窗口：

```xml
<Window x:Class="MainWindow" Title="My Window" Name="MyWindow">
  <Grid Name="LayoutRoot">
    <!-- The button is inside the grid -->
    <Button Name="FirstButton" Height="74" Width="229">
      Click Me, Please
    </Button>
  </Grid>
</Window>
```

```csharp
Window MyWindow = new MainWindow();
MyWindow.Title = "My Window";
Grid LayoutRoot = new Grid();
MyWindow.Content = LayoutRoot;
// The button is inside the grid
Button FirstButton = new Button();
FirstButton.Height = 74;
FirstButton.Width = 229;
FirstButton.Content = "Click Me, Please";
LayoutRoot.Children.Add(FirstButton);
```

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_515_1.png)

### 戴上你的思考帽

如果 C# 能做 XAML 能做的一切，并且还能做更多，你能想到在应用程序开发过程中同时使用这两种语言有什么好处吗？

### 你做得怎么样？

你想到一些理由了吗？你被它们说服了吗？以下是一些你可能没有想到的理由列表：

### XAML 通常更简洁

如果你比较上一页的代码片段，你会发现 XAML 版本的窗口要少冗长得多。（但并非总是如此。）

### XAML 是声明式的

“声明式”不一定意味着更好，但通常更容易理解（和编写）。想象一下说“我想在那面墙上装一个电源插座”和实际布线之间的区别。

### XAML 清晰地表达了 WPF 组合模式

正如我们在探索逻辑树和可视化树时将看到的那样，WPF 界面是组合而成的。事物不会凭空漂浮：一个字符串包含在按钮中，按钮包含在网格中，网格包含在窗口中。XAML 的层级结构使其比过程式代码清晰得多，清晰得多。

### XAML 支持工具化

微软的人们谈到 XAML 是“可工具化的”。他们的意思是，因为 XAML 是普通的旧 XML，它可以被任何应用程序轻松解析和操作。一个很好的例子是微软的 Expression Blend，这是一款面向设计师而非开发人员的设计和原型工具（也就是说，它会让习惯使用 Adobe Photoshop 的人感到熟悉）。

### XAML 支持独立的工作流程

程序员作为一类人，并不以其图形设计技能著称；那是另一门职业。但一旦你有用于设计图形和实现行为的独立工具，就可以轻而易举地让不同的人执行他们受过训练的任务。让图形设计师设计，程序员编程，难道不合理吗？XAML 使这变得容易。而且，由于许多图形设计师熟悉另一种基于 XML 的语言 HTML，其中许多人发现直接在 XAML 中工作相当舒适。

### 语法基础

如果你熟悉 XML 或 HTML，XAML 的语法对你来说已经很熟悉，但它对基本 XML 添加了一些扩展，并使用了一些特殊词汇。如果你不熟悉 XML，不用担心。它真的，真的很简单。

### 对象元素

C# 的基本单位是语句。XAML 的基本单位是对象元素。就像在 C# 中你可以编写单行或多行语句一样，你可以编写单行和多行对象元素声明：

此语法用于不包含任何其他元素的元素。它大致相当于单行 C# 语句。

```xml
<Button />
```

此语法用于在对象中嵌套其他元素时。它大致相当于由大括号括起来的 C# 语句块。

```xml
<Button>
  <Element />...
</Button>
```

### 属性和特性

在 C# 中，你使用类似 Object.Property = value 的语法为对象的属性赋值。在 XAML 中，你有两种选择。你可以将属性设置为在开始标记中声明的特性，也可以将属性定义为单独的嵌套元素：

这是特性语法 特性包含在引号中，多个特性由空格分隔。

```xml
<Button Height="74" Width="229" />
```

这称为属性元素语法。对于某些复杂属性，它比特性语法更容易编写和理解。

```xml
<Button Width="229">
  <Button.Height>74</Button.Height>
</Button>
```

请注意，你可以组合使用属性元素语法和特性语法。

### 内容属性

你是否注意到在 Button 属性元素示例中，我们必须将 Height 属性指定为 Button.Height？

当我们使用特性语法时，我们只需要指定属性名称。

```xml
<Button Width="229">
  <Button.Height>74</Button.Height>
</Button>
```

属性元素语法需要对象名称和属性名称。

像这样重复对象名称，可以清楚地表明你引用的是属性，而不是名为“Height”的其他元素。但是每个 WPF 元素都可以定义一个名为内容属性的单个属性，该属性可以简单地放置在对象的开始标记和结束标记之间。对于 Button，内容属性是显示在 Button 内部的内容，通常是一个字符串：

```xml
<Button>
  Click Me, Please
</Button>
```

内容属性不需要用标记括起来（虽然你可以），并且某些元素（如 WPF Button）甚至可以直接解释字符串，而无需将其放在引号中。

使用内容属性的棘手之处在于知道它是什么意思。从技术上讲，内容属性是控件模板的 ContentPresenter 将显示的任何对象。（我们将在第 21 章中检查控件模板。）但通常很直观，就像 Button 一样。我的意思是，除了显示“Click Me, Please”，你还期望控件对它做什么呢？

### 戴上你的思考帽

是时候动手实践一下了。你能将下面的 C# 代码片段翻译成 XAML，并将 XAML 代码翻译成 C# 吗？[不用担心所有元素是什么。我们将在后面的章节中检查它们。]

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_519_0.png)

```csharp
Window MainWindow = new MainWindow();
MainWindow.Title = "Sample";
MainWindow.Height = 300;
MainWindow.Width = 500;

DockPanel LayoutRoot = new DockPanel();

Menu MainMenu = new Menu();
MenuItem FileMenu = new MenuItem();
FileMenu.Header = "File";

MainMenu.AddChild(FileMenu);
LayoutRoot.Children.Add(MainMenu);
MainWindow.Content = LayoutRoot;
```

> 请注意，你在 Menu 上调用 AddChild()，但在 LayoutRoot 上调用 Add()。当我们在下一章中检查 WPF 控件时，你就会明白为什么。

```xml
<Window x:Class="MainWindow" Height="Auto" Width="Auto">
  <Grid Name="LayoutRoot">
    <Button Height="50" Width="75">
      Cancel
    </Button>
  </Grid>
</Window>
```

### 你做得怎么样？

请记住，在 C# 和 XAML 中都有不同的方式来表达相同的事物，所以如果你的代码与我的略有不同，请不要担心，只要语法正确即可。

```csharp
Window MainWindow = new MainWindow();
MainWindow.Title = "Sample";
MainWindow.Height = 300;
MainWindow.Width = 500;
DockPanel LayoutRoot = new DockPanel();
Menu MainMenu = new Menu();
MenuItem FileMenu = new MenuItem();
FileMenu.Header = "File";
MainMenu.AddChild(FileMenu);
LayoutRoot.Children.Add(MainMenu);
MainWindow.Content = LayoutRoot;
```

```xml
<Window x:Class="MainWindow" Title="Sample" Height="300" Width="500">
  <DockPanel Name="LayoutRoot">
    <Menu Name="MainMenu">
      <MenuItem Name="FileMenu" Header="File" />
    </Menu>
  </DockPanel>
</Window>
```

这个有点棘手。你做对了吗？你不需要显式地将 MenuItem 添加到 Menu 中，因为这在 XAML 的结构中是隐式的。

你在为这里的变量命名时遇到问题了吗？与 C# 变量不同，XAML 元素不需要名称，除非你打算在代码中引用它们，但使用 name 特性给它们一个名称是个好主意。

```csharp
MainWindow myWindow = new MainWindow();
Grid LayoutRoot = new Grid();
Button myButton = new Button();
myButton.Height = 50;
myButton.Width = 75;
LayoutRoot.Children.Add(myButton);
myWindow.Content = LayoutRoot;
```

```xml
<Window x:Class="MainWindow" Height="Auto" Width="Auto">
  <Grid Name="LayoutRoot">
    <Button Height="50" Width="75">
      Cancel
    </Button>
  </Grid>
</Window>
```

