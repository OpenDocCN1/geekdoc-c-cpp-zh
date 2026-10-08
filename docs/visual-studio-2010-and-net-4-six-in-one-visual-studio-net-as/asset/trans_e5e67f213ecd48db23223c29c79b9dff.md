

# XAML

为了充分理解 XAML 与 Silverlight 之间的关系，一个示例应用程序将最有帮助。

> Visual Studio 2010 允许你创建开箱用的 Silverlight 3 和 Silverlight 4 。然而，它仅提供 Silverlight 3 支持。要启用 Silverlight 4 开发，你必须从 http://www.silverlight.net/getstarted 下载并安装“Silverlight 4 Tools for Visual Studio 2010”。如果你计划在自己的计算机上按照示例操作，建议现在进行安装。

# Silverlight Hello World 应用程序

让我们启动 Visual Studio 2010 并创建第一个 Silverlight 应用程序。在图 8-1 所示的新建项目对话框中，选择 Silverlight Application。（你可以使用右上角的的新模板搜索功能来快速找到它。）

![](img/b5597c749e848b27b0d305153ae16106_345_0.png)

图 8-1：在 Visual Studio 2010 中创建新的 Silverlight 项目

在提供了解决方案的名称和目录（暂命名为 HelloWorld）后，Visual Studio 会询问你是否想要“在新网站中托管 Silverlight 应用程序”。保持勾选框选中，并确保 Silverlight 版本为 Silverlight 4。现在

项目创建后，查看解决方案管理器（Solution Explorer）。应该有一个新的解决方案，包含两个项目。第一个是 Silverlight 项目，包含 .xaml 文件（以及对应的 .cs 文件）。第二个项目是你通过向导创建的托管网站。它包含了 HelloWorldTestPage.aspx 和 HelloWorldTestPage.html 页面、一个 JavaScript 库、一个 Web.config 以及一个 ClientBin 目录。通过生成，你现在会看到 ClientBin 文件夹中有一个项目：HelloWorld.xap 文件，这是在浏览器中下载并运行的实际 Silverlight 应用程序。图 8-2 显示了你的 Silverlight 解决方案中文件是如何布局的。

你还可以看到，在创建解决方案后，Visual Studio 打开了 MainPage 进行编辑，如图 8-3 所示。就像 ASP.NET 的拆分视图一样，你应该看到一个分屏界面，上方是空的 Silverlight 屏幕，下方是 XAML 代码。如果你没有看到分屏，请点击编辑窗口底部的小水平线。

![](img/b5597c749e848b27b0d305153ae16106_346_0.png)

图 8-2：Silverlight 解决方案的文件结构

![](img/b5597c749e848b27b0d305153ae16106_346_1.png)

图 8-3：Visual Studio 2010 工作空间

那么，什么是 XAML 代码？如果你熟悉 XML，你一眼就能看出 XAML 基本上就是 XML。作为一种基本方法，你可以将 XAML 为将 CLR 对象树序列化为 XML 的方式。XAML 具有一些额外的语法，有助于数据绑定和其他 UI 相关的任务。

就像在 HTML 中一样，在 Silverlight 中，XAML 主要用于描述应用程序的 UI。让我们查看代码 8-1 所示的 MainPage.xaml 文件的内容。

# 代码 8-1：MainPage.xaml

```
<UserControl x:Class="HelloWorld.MainPage"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:mc="http://schemas.microsoft.xmlformats.org/markup-compatibility/2006"
c:Ignorable="d"
d:DesignHeight="300" d:DesignWidth="400">

  <Grid x:Name="LayoutRoot" Background="White">

  </Grid>
</UserControl>
```

与任何 XML 文件一样，你有一个根元素。在这种情况下，这是一个 UserControl，定义了类型和命名空间，其中 xmlns:d 是一个设计命名空间，供 Expression Blend 和 Visual Studio 等工具用于设计设计属性。这些属性在应用程序运行时不起任何作用，但为 UserControl 提供了 d:DesignHeight 和 d:DesignWidth 属性。为 UserControl 使用设计宽度和高度以便在视觉设计器中查看。

在 UserControl 内部，MainPage.xaml 有一个 Grid。Grid 是一个布局控件。它的任务是在行和列中排列并显示其子元素。Grid 的名称为 LayoutRoot，并具有白色背景。

通过在 Grid 中插入一个 TextBlock 来更改 XAML。现在 MainPage.xaml 应该如代码 8-2 所示所示。

# 代码 8-2：带有 Hello TextBlock 的 MainPage.xaml

```
<UserControl x:Class="HelloWorld.MainPage"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:mc="http://schemas.microsoft.xmlformats.org/markup-compatibility/2006"
c:Ignorable="d"
d:DesignHeight="300" d:DesignWidth="400">

  <Grid x:Name="LayoutRoot" Background="White">
    <TextBlock Text="Hello World" HorizontalAlignment="Center" VerticalAlignment="Center" />
  </Grid>
</UserControl>
```

