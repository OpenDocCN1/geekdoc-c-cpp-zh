

请注意，资源文件中已定义了一些服务器控件属性。例如，Button服务器控件的Text和ToolTip属性已暴露在资源文件中，Visual Studio本地化工具根据您在控件中放置的内容提取了默认的Text属性值。仔细查看该文件中的Button服务器控件构造，您会看到Text和ToolTip属性的名称前都有一个定义性的`Button1Resource1`值。这正是前面展示的Button服务器控件所使用的键。

在以下aspx源代码中，`meta:resourcekey`属性被添加到按钮控件上。此处的引用指向`Button1Resource1`。资源文件中使用该键的所有属性（例如Text和ToolTip属性）都会在运行时应用到该Button服务器控件。

```aspx
<asp:Button ID="Button1" runat="server" Text="Submit Name"
    meta:resourcekey="Button1Resource1" />
```

> *代码片段摘自ProVB_Localization\Default.aspx*

## 添加另一种语言的资源文件

上一节创建的`Default.aspx.resx`文件被应用程序用作默认（或固定区域性）资源文件。此资源文件没有分配特定的区域性。如果某个请求无法确定区域性，则将使用该资源文件。要为处理另一种语言的`Default.aspx`页面添加另一个资源文件，请将`Default.aspx.resx`文件复制并粘贴到相同的`App_LocalResources`文件夹中，然后重命名新复制的文件。如果使用`Default.aspx.fi-FI.resx`，请将以下键设置为所示的值，以创建芬兰语资源文件：

```text
Button1Resource1.Text     Lähetä Nimi
Label1Resource1.Text      Mikä sinun nimesi on?
PageResource1.Title       Näytesivu
```

创建此文件后，请再执行一步：在两个资源文件中使用键`Label2Answer`创建自定义资源。`Default.aspx.resx`文件应包含以下新键：

```text
Label2Answer              Hello
```

现在您可以按如下方式将键`Label2Answer`添加到`Default.aspx.fi-FI.resx`文件中：

```text
Label2Answer              Hei
```

您现在已经有了针对特定控件的资源，以及以后可以通过编程方式访问的资源。

## 完成Default.aspx页面的构建

完成`Default.aspx`页面时，您需要添加一个`Button1_Click`事件，以便当最终用户在文本框中输入姓名并单击Submit按钮时，`Label2`服务器控件提供从本地资源文件中提取的问候语。所有工作完成后，默认页面应具有与以下代码匹配的代码隐藏元素：

```vb
Partial Class _Default
    Inherits System.Web.UI.Page

    Protected Sub Button1_Click(ByVal sender As Object,
            ByVal e As System.EventArgs) Handles Button1.Click
        Label2.Text = GetLocalResourceObject("Label2Answer") &
            " " & TextBox1.Text
    End Sub
End Class
```

> *代码片段摘自ProVB_Localization\Default.aspx.vb*

除了通过在页面上的服务器控件中使用`meta:resourcekey`属性来提取本地资源以访问暴露的属性之外，您还可以通过使用GetLocalResourceObject来访问本地资源文件中包含的任何属性值。使用GetLocalResourceObject时，只需将键名称作为参数传入，如下所示：

```
GetLocalResourceObject("Label2Answer")
```

在Default.aspx页面上的代码就绪且资源文件完成之后，您可以运行该页面，在文本框中输入姓名，然后点击Submit Name按钮获取响应，如图27-13所示。

幕后发生了什么使得该页面以此方式构建？首先，只有两个资源文件可用：`Default.aspx.resx`和`Default.aspx.fi-FI.resx`。其中`Default.aspx.resx`是固定区域性资源文件，而`Default.aspx.fi-FI.resx`是针对特定区域性（fi-FI）的资源文件。由于请求Default.aspx页面的浏览器首选区域性为en-US，ASP.NET找到了Default.aspx页面的本地资源。接着，ASP.NET检查是否存在针对en-US特定区域性的Default.aspx页面版本。由于没有针对en-US区域性特定页面，ASP.NET便检查是否存在针对en（中性区域性）的特定页面。在找不到针对en中性区域性的页面后，ASP.NET只能使用固定区域性资源文件`Default.aspx.resx`，从而生成如图27-13所示的页面。

如果您现在将IE语言首选项设置为fi-FI并重新运行Default.aspx页面，您将看到该页面的芬兰语版本，如图27-14所示。

![](img/d99870e80390742f93963da7be0b2e61_922_0.png)

图27-13

![](img/d99870e80390742f93963da7be0b2e61_922_1.png)

图27-14

在这种情况下，由于已将IE语言首选项设置为fi-FI，您看到的是该区域性版本的页面，而不是前面显示的固定区域性页面。ASP.NET通过使用`Default.aspx.fi-FI.resx`资源文件找到了此特定区域性。

您可以看到，所有已翻译并放入资源文件中的控件属性都会被ASP.NET自动使用，包括IE标题栏中显示的页面标题。

## 中性区域性通常更受青睐

在处理本示例中的资源文件时，请注意其中一个资源是针对*特定区域性*的。`Default.aspx.fi-FI.resx`文件针对的是特定区域性——芬兰境内使用的芬兰语。另一种选择是使此文件不针对特定区域性，而是针对中性区域性。要做到这一点，只需将文件命名为`Default.aspx.fi.resx`。在这种情况下，差异不大，因为没有其他国家使用芬兰语；但是对于德语、西班牙语或法语等在多国使用的语言来说，这样做就很有意义了。

例如，如果您要制作`Default.aspx`页面的西班牙语版本，您完全可以将其构建为针对特定区域性，例如`Default.aspx.es-MX.resx`。这种构造针对的是墨西哥使用的西班牙语。有了此文件后，如果某个用户以es-MX语言设置请求`Default.aspx`页面，该用户将获得此资源文件的内容。如果请求者的设置为es-ES，他或她将不会获得`Default.aspx.es-MX.resx`资源文件，而是获得固定区域性资源文件`Default.aspx.resx`。如果您只打算为站点或任何页面提供单一翻译，请将资源文件构建为中性区域性，而非特定区域性。

如果您拥有资源文件`Default.aspx.es.resx`，那么无论最终用户的首选设置是es-MX、es-ES还是甚至es-AR，该用户都会获得相应的西班牙语中性区域性版本页面。

## 全局资源

除了仅使用与ASP.NET应用程序中特定页面相关的本地资源之外，您还可以选择创建可跨多个页面使用的*全局资源*。若要创建可在整个应用程序中使用的资源文件，请在Visual Studio的解决方案资源管理器中右键单击解决方案，然后选择“添加新项”。在“添加新项”对话框中，选择“资源文件”。Visual Studio会提示您将此文件放入名为`App_GlobalResources`的新文件夹中。您会看到此文件已存在于示例代码下载中。同样，您的第一个资源文件是固定区域性资源文件。添加一个键为`LabelText`的字符串资源，并为此键分配一个较长的字符串值。代码下载中使用了字符串“Non-Variant Format Label Text”。接下来，在现有页面的底部添加第三个标签控件`Label3`。

既然固定区域性资源文件已完成，下一步是添加另一个资源文件，但这次将其命名为`Resource.es.resx`。同样，对于此资源文件，请使用字符串键`LabelText`，并将前面文本的西班牙语翻译粘贴进去。

全局资源文件的意义在于能够在整个应用程序中访问这些资源。您可以通过多种方式访问放置在这些文件中的值。一种方式是将值直接用于任何服务器控件声明中。例如，您可以按如下方式将下面的隐私声明放在Label服务器控件中：

```aspx
<asp:Label ID="Label3" runat="server"
    Text='<%$ Resources: Resource, LabelText %>'></asp:Label>
```

> *代码片段摘自ProVB_Localization\Default.aspx*

