
键 **firstBrush** 和 **secondBrush** 已定义。这两个资源用于设置三个按钮（**button1、button2 和 button3**）的 **Background** 属性。**StaticResource** 标记扩展用于将 **Background** 属性设置为这些资源的值。

- **5** *按 F5 键运行 StaticResourcesDemo 应用程序。输出如 **图 C#-7.37** 所示。*

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_258_0.png)

**图 C#-7.37**

在 **图 C#-7.37** 中，显示了三个按钮 **button1、button2 和 button3**，它们的 **Background** 属性是使用 **StaticResource** 标记扩展设置的。

现在我们来学习动态资源。

## 使用动态资源

使用 **DynamicResource** 标记扩展时，该资源称为动态资源。与静态资源相比，动态资源提供了更大的灵活性，并且适用于希望将属性值的赋值推迟到运行时的情况，例如，当希望通过用户设置或系统设置在运行时更改资源的值时。

与在加载时查找的静态资源不同，动态资源仅在使用时（运行时）才进行查找。使用动态资源时，会为请求的资源创建一个表达式。该表达式直到运行时才会求值。当在运行时使用动态资源时，会在设置属性的元素资源中查找所请求资源的键。如果未找到该键，则会在父元素及其资源字典中逐级向上查找，直到根元素。如果仍未找到该键，则依次查找应用程序、主题和系统资源。

让我们创建一个名为 **DynamicResourcesDemo** 的独立 WPF 应用程序，以演示动态资源的使用。为此，请执行以下步骤：

- 1. *重复步骤 1 到 3*，与本章 *使用 Grid 控件* 一节中前面创建 **GridDemo** 应用程序时相同。
- 2. *在* **Name** *文本框中输入名称* **DynamicResourcesDemo**，*并在* **Location** *组合框中为该应用程序指定合适的位置。*
- 3. *单击* **OK** *按钮。* **DynamicResourcesDemo** *应用程序即被创建。*
- 4. *将清单 7.21 中给出的突出显示的代码添加到* **MainWindow.xaml** *文件中。*

### 清单 7.21：在 XAML 中使用动态资源

```xml
<Window x:Class="DynamicResourcesDemo.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="Demo-DynamicResources" Height="300" Width="300">
    <Window.Resources>
        <SolidColorBrush x:Key="firstBrush" Color="Lavender"/>
        <SolidColorBrush x:Key="secondBrush" Color="PowderBlue"/>
        <SolidColorBrush x:Key="thirdBrush" Color="Violet"/>
    </Window.Resources>
    <Grid Name="grid1" Background="{StaticResource firstBrush}">
<Button Name="button1" Height="100" Width="150" Margin="0,0,0,75" Content="Dynamic Button" BorderBrush="Black" BorderThickness="5" Background="{DynamicResource grid1.Background}"/>
<Button Name="button2" Height="25" Margin="0,185,100,0" Width="75" Content="Color1" Click="button2_Click" />
<Button Name="button3" Height="25" Margin="100,185,0,0" Width="75" Content="Color2" Click="button3_Click" />
</Grid>
</Window>
```

在清单 7.21 中，可以看到 Window 控件有三个 SolidColorBrush 资源，其键分别为 firstBrush、secondBrush 和 thirdBrush。firstBrush 资源在 grid1 控件的 **Background** 属性中作为静态资源引用。然后，grid1 控件的 **Background** 属性在 button1 控件中用作动态资源。这意味着每当 grid1 控件的背景发生变化时，button1 控件的背景也会随之变化。

- 5 在设计视图中双击 **Color1** 按钮，在 MainWindow.xaml.cs 文件中添加该按钮的 Click 事件处理程序。

- 6 现在，在 MainWindow 类中为 button2_Click 事件处理程序添加以下代码片段：

```
private void button2_Click(object sender, RoutedEventArgs e)
{
    grid1.Background = (Brush)this.FindResource("secondBrush");
}
```

在前面的代码片段中，在 button2_Click 事件处理程序中，通过使用 FindResource() 方法将 grid1 控件的背景设置为 secondBrush 资源的值。

- 7 切换到 MainWindow.xaml 文件，并在设计视图中双击 **Color2** 按钮，在 MainWindow.xaml.cs 文件中添加该按钮的 Click 事件处理程序。

- 8 在 MainWindow 类中为 button3_Click 事件处理程序添加以下代码片段：

```
private void button3_Click(object sender, RoutedEventArgs e)
{
    grid1.Background = (Brush)this.FindResource("thirdBrush");
}
```

在前面的代码片段中，在 button3_Click 事件处理程序中将 grid1 控件的背景设置为 thirdBrush 资源的值。

- 9 按 F5 键运行 DynamicResourcesDemo 应用程序。输出如 **图 C#-7.38** 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_259_0.png)

图 C#-7.38

- 10 在 Demo-DynamicResources 窗口中单击 **Color1** 按钮，如 **图 C#-7.39** 所示：

2 在 Name 文本框中输入名称 StylesDemo，并在 Location 组合框中为该应用程序指定合适的位置。

3 单击 OK 按钮。StylesDemo 应用程序即被创建。

4 将清单 7.22 中给出的突出显示的代码添加到 MainWindow.xaml 文件中：

### 清单 7.22：将样式用作资源

```xml
<Window x:Class="StylesDemo.MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Title="Demo-Styles" Height="200" Width="300">
<Grid>
<Grid.Resources>
<Style x:Key="myButtonStyle">
<Setter Property="Button.Background" Value="Black"/>
<Setter Property="Button.Foreground" Value="White"/>
</Style>
</Grid.Resources>
<Button Name="button1" Style="{StaticResource myButtonStyle}" Margin="10,10,140,85"/>
<Button Name="button2" Style="{StaticResource myButtonStyle}" Margin="140,85,10,10"/>
</Grid>
</Window>
```

在清单 7.22 中，Grid 控件的 Resource 属性有一个键为 myButtonStyle 的 Style 元素。该 Style 元素有两个 Setter 元素，分别指定网格中按钮的 **Background** 和 **Foreground** 属性的值。然后，该 Style 元素在 button1 和 button2 控件的 Style 属性中作为静态资源引用。这意味着网格中的两个按钮具有相同的样式。

- 5 按 F5 键运行 StylesDemo 应用程序。输出如 **图 C#-7.41** 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_261_0.png)

图 C#-7.41

至此，本章结束。现在我们来回顾本章讨论的要点。

## 小结

在本章中，您学习了：

- WPF 4.0 的体系结构
- WPF 4.0 中的增强功能
- 不同类型的 WPF 4.0 应用程序
- WPF 4.0 设计器
- XAML 在 WPF 中的使用
- 在 WPF 应用程序中使用常用控件和新控件
- 在 WPF 应用程序中使用资源和样式

## 第 8 章

## ADO.NET 与数据绑定

**本章内容：**

- 探索 ADO.NET
- Windows Forms 中的数据绑定类型
- WPF 中的数据绑定

商业世界正在迅速发展，存储数据的需求也在迅速增长。如您所知，数据是事实的集合，通常以表的形式存储在数据库中。数据库是表的集合，用于在计算机中系统地存储大量数据（信息）。这些存储的信息可以在需要时从数据库中快速高效地访问。用于关联多个表中数据的数据库称为关系数据库。一些常用的关系数据库包括 SQL Server（其中 SQL 代表结构化查询语言服务器）、Oracle 和 Microsoft Access。

直接从数据库检索和操作数据需要具备基本 SQL 命令的知识。不熟悉 SQL 命令的人将无法使用数据库中存储的数据。因此，大多数业务应用程序都提供用户友好的界面，帮助从数据库中检索数据，而无需编写 SQL 命令。Microsoft ActiveX Data Objects.NET（ADO.NET）是 .NET 应用程序使用的一种模型，您可以使用它直接与数据库通信，以检索和操作数据。

本章向您介绍 ADO.NET。您还将学习数据绑定的概念，以及 Windows Forms 和 Windows Presentation Foundation（WPF）中不同类型的数据绑定。

我们先简要探讨 ADO.NET。

## 探索 ADO.NET

ADO.NET 是 .NET 应用程序使用的主要数据访问技术。ADO.NET 使用断开式数据体系结构，这意味着您处理的数据只是数据库中数据的副本。Microsoft 出于多种原因选择了断开式数据体系结构。在传统的客户端/服务器应用程序中，您连接到数据库，并且需要在应用程序运行期间保持此连接。然而，维护这样的连接需要大量服务器资源。因此，当您迁移到 Internet 时，应遵循断开式数据体系结构，而不是与服务器保持直接且连续的连接，以减少服务器负载。

现在我们来讨论 ADO.NET 4.0 实体框架中的改进以及构成 ADO.NET 的组件。

## ADO.NET 4.0 实体框架中的改进

借助 ADO.NET 实体框架，程序员可以通过针对概念应用程序模型编程来开发数据访问应用程序，而不是直接针对关系存储架构编程。这样做的主要目的是减少面向数据的应用程序通常所需的代码量和维护工作量。

ADO.NET 4.0 实体框架中引入的新功能和增强功能包括：

- **支持在概念数据模型中创建外键：** 使开发人员能够创建概念模型，其中数据库中的外键列对应于实体类型上的标量属性。映射到数据存储模型中单个字段的任何实体类型的属性称为标量属性。
- **引入用于 n 层应用程序开发的自我跟踪实体：** 指在处理 n 层应用程序时使用自我跟踪实体。这些自我跟踪实体通常可以记录对标量属性、复杂属性和导航属性的更改。

> **注意**
> n 层应用程序是指分布在分布式网络中三台或更多独立计算机上的应用程序。在术语 n 层中，n 指某个数字，例如 3 层。在 3 层应用程序中，用户界面位于用户的计算机上，业务逻辑存储在更加集中的计算机上，所需数据存储在数据库服务器或管理数据库的计算机上。

- **用于 n 层应用程序开发的新方法：** 指在 System.Data.Objects 命名空间中添加的新方法，以便更轻松地开发 n 层应用程序。

