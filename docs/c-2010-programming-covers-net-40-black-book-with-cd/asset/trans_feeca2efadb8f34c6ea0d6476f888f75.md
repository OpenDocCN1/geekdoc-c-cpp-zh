
![](img/e073a4882197be4ab61103cbe0bcb394_896_0.png)

您还可以使用DataTemplate、HierarchicalDataTemplate和Style标签来定制TreeView控件的外观。此外，您还可以在TreeView控件内部放置其他控件，例如TextBlock和Button控件。TreeView控件是TreeView类的一个实例，位于System.Windows.Controls命名空间中的System.Windows.Controls.dll程序集中。TreeView类的类层次结构如下所示：

```
System.Object
  System.Windows.DependencyObject
    System.Windows.UIElement
      System.Windows.FrameworkElement
        System.Windows.Controls.Control
          System.Windows.Controls.ItemsControl
            System.Windows.Controls.TreeView
```

表17.17列出了TreeView类中值得注意的属性：

| 属性 | 描述 |
|---|---|
| ItemContainerGenerator | 检索TreeView控件中各项与其父元素之间的映射。 |
| ItemContainerStyle | 检索或分配应用于TreeView控件中为每个项生成的父元素的样式。 |
| Items | 检索用于生成TreeView控件内容的集合。 |
| ItemTemplate | 检索或设置用于显示TreeView控件中每个项的DataTemplate。 |
| SelectedItem | 检索TreeView控件中选中的项。 |

接下来，让我们讨论如何在ASP.NET Web应用程序中托管Silverlight内容。

## Silverlight 与 ASP.NET

Silverlight可以轻松地渗透到使用现有Web技术（如ASP.NET）构建的Web应用程序中。对于ASP.NET应用程序，Silverlight提供了一致的应用程序模型来实现应用程序的逻辑，并提供一组丰富且交互性强的控件来设计应用程序的UI。将Silverlight与ASP.NET网站融合，不仅通过让网站更具动态性来改善其外观，还通过让网站更具交互性来增强其行为。

您可以使用某些ASP.NET服务器控件在任何ASP.NET网站上托管Silverlight内容。请注意，托管在ASP.NET网站中的Silverlight内容使用XAML作为UI，而ASP.NET内容的其余部分则使用标准HTML作为UI。您可以通过使用Visual Studio 2010模板创建Silverlight应用程序，并使用ASP.NET Web应用程序来托管它，从而在ASP.NET Web应用程序中托管Silverlight内容。

现在，让我们通过执行以下步骤创建一个Silverlight 3.0应用程序，并使用一个网站来托管该Silverlight内容：

+   1. 打开Visual Studio 2010窗口，选择“文件”→“新建”→“项目”，系统将显示“新建项目”对话框。
+   2. 从“已安装的模板”窗格中选择Visual C#。
+   3. 从“已安装的模板”窗格中选择Silverlight，并从“新建项目”对话框中间窗格中选择“Silverlight应用程序”选项（图17.19）。
+   4. 在“名称”文本框和“位置”组合框中分别为Silverlight应用程序输入适当的名称和位置。在我们的示例中，我们将Silverlight应用程序命名为SilverlightWithASP，并将位置输入为D:\Books\Black Book\C# 2010\Chapter 17\PracticeApplications（图17.19）。
+   5. 单击“确定”按钮，如图17.19所示：

![](img/e073a4882197be4ab61103cbe0bcb394_897_0.png)

## 图17.19：创建Silverlight 3.0应用程序

“新建项目”对话框关闭，并出现“新建Silverlight应用程序”对话框（图17.20）。

+   6. 选中“在新的网站中托管Silverlight应用程序”复选框，以指定您的Silverlight应用程序SilverlightWithASP的主机（图17.20）。
+   7. 在“新Web项目名称”文本框中输入托管Silverlight内容所需的新ASP.NET应用程序的名称。在我们的示例中，我们保留了默认名称SilverlightWithASP.Web（图17.20）。
+   8. 从标记为“新Web项目类型”的下拉列表中选择“ASP.NET Web应用程序项目”（图17.20）。
+   9. 从标记为“Silverlight版本”的下拉列表中选择“Silverlight 3”选项（图17.20）。
+   10. 单击“确定”按钮，如图17.20所示：

![](img/e073a4882197be4ab61103cbe0bcb394_898_0.png)

## 图17.20：为Silverlight 3.0应用程序指定主机

这将创建一个Silverlight应用程序SilverlightWithASP，以及一个用于托管Silverlight内容的ASP.NET Web应用程序SilverlightWithASP.Web，如图17.21所示：

![](img/e073a4882197be4ab61103cbe0bcb394_898_1.png)

## 图17.21：在解决方案资源管理器中显示Silverlight应用程序SilverlightWithASP的文件

如图17.21所示，Silverlight应用程序中创建了两个项目。一个项目SilverlightWithASP用于Silverlight内容本身，另一个项目SilverlightWithASP.Web是托管Silverlight内容的ASP.NET Web应用程序。Silverlight应用程序SilverlightWithASP包含App.xaml和App.xaml.cs文件，用于处理Silverlight应用程序的整体设置；以及MainPage.xaml和MainPage.xaml.cs文件，用于处理Silverlight应用程序的UI。

ASP.NET网站项目为整个Silverlight应用程序SilverlightWithASP创建了两个测试页面。这两个测试页面（一个是.aspx，另一个是.html）都用于托管Silverlight应用程序。测试页面的名称与Silverlight应用程序相同，并带有文本TestPage后缀（图17.21）。请注意，.aspx和.html测试页面在默认情况下都会创建。.html测试页面中包含的代码与托管在单个HTML页面中的Silverlight应用程序的TestPage.html文件大致相同，也就是说，.html测试页面包含用于创建和初始化Silverlight内容的代码。.aspx测试页面包含.html测试页面的等效ASP.NET代码。当用户运行该应用程序时，首先出现的页面就是这个.aspx测试页面。Web应用程序还包括web.config文件，这是一个用于存储网站配置的XML文件。

## Silverlight 中的数据绑定

简单来说，数据绑定是指数据提供程序与包含数据绑定控件（如DataGrid）的UI之间的连接。UI被称为目标，数据提供程序被称为源。这种数据绑定的划分有助于维护应用程序并提高应用程序的性能。性能之所以提高，是因为这种数据绑定划分减少了对服务器的往返调用。Silverlight是.NET Framework 4.0的一部分，您可以在其中实现数据绑定。让我们来了解Silverlight中数据绑定的各个方面。

### Silverlight 中数据绑定的类型

在Silverlight应用程序中，您可以将数据绑定为以下几种类型：

+   - **OneTime** – 设置目标，然后绑定完成。当您显示很少或从不更改的数据时，可以使用OneTime绑定。
+   - **OneWay** – 设置目标，并在源更改时保持目标最新。当您显示不允许更改的数据时，可以使用OneWay绑定。
+   - **TwoWay** – 设置目标，并在源更改时保持目标最新。当您更改目标或应用程序中有其他更改导致源发生变化时，它也会使源保持最新。

您可以使用一个简单的示例来理解Silverlight中的数据绑定类型。假设您负责构建一个在线书店。如果您正在显示有关一本书的信息，您可能会对书名和作者使用OneTime绑定，因为它们永远不会更改。对于书的价格，您会使用OneWay绑定，因为用户无法更改它。对于手头的书的数量，您会选择TwoWay绑定，因为它可能会发生变化。

### 绑定对象

Silverlight中的绑定对象是目标与源之间的通用连接器。该绑定对象负责从源检索目标所需的数据。Silverlight中的绑定对象表示对象的属性值与控件的属性值之间的绑定。例如，您可以将TextBox控件的Text属性绑定到Customers表的FirstName列。类似地，您可以将另一个TextBox控件的Text属性绑定到Customers表的LastName列。当您运行应用程序时，绑定对象将确保在相应的TextBox控件中检索到正确的数据。数据绑定的这一特性在Silverlight应用程序中非常有用。在前一节解释的示例中，您实际上是在使用绑定对象绑定TextBox控件的Text属性。

### 数据上下文

数据上下文是在运行时从源中选择正确的数据并将其发送到目标的过程。例如，当您将目标与源绑定时，您只需指定目标将显示的数据种类。您指定特定的文本框将显示客户的姓名。您不指定要显示哪个客户姓名。您只需将TextBox与Customers表绑定。这就是数据上下文发挥作用的地方。数据上下文是在运行时显示的特定客户。简单来说，您可以将数据上下文视为可以绑定到目标的数据源。当容器控件中有多个控件且所有控件都使用相同的绑定源时，数据上下文非常有用。每个FrameworkElement对象都有一个数据上下文。

在创建绑定时，必须将FrameworkElement对象的依赖项属性分配给绑定。这是绑定操作的基本目标。您可以通过元素的DataContext属性设置绑定的源。数据上下文还允许其元素从父容器继承有关数据源的信息。
