
```
<@ OutputCache Duration="ofseconds"
Location=Any | Client | Downstream | Server | None |
ServerCache
Shared=false
VaryByControl=classname
VaryByCustom="browser | customing"
VaryByHeader="headers"
VaryByParam="parametername"
VaryContentEncoding="encodings"
CacheProfile="cache profile name = "-"
nostrue=false
SqlDependency=database/table name pair | Commandnotification"
ProviderName="ProviderName" %>
```

### @ Reference 指令

`Reference` 指令动态链接用户控件。

The `@ Reference` 指令的语法如下：

```
<@ Reference path=".aspx"
VirtualPath="path"
```

### @ WebHandler 指令

`WebHandler` 指令指定了 `.ashx` 文件的属性和编译选项。

The `@ WebHandler` 指令的语法如下：

```
<@ WebHandler attribute="value"
```

# 第 10 章：介绍 ASP.NET 4.5 和 Web Forms

## 解决方案

## 创建新的站点

在本章的深度介绍部分，我们提到可以在本地计算机或网络计算机上创建新的站点。

### 使用文件系统 (File System)

在创建文件系统站点时，文件存储在本地计算机或网络计算机上。为了做到这一点，请执行以下步骤：

1. 点击 `文件→新建→站点`。
2. 选择 `ASP.NET` 空站点模板，并在 `Web` 站点位置下拉列表中选择 `文件系统`。
3. 在 `Location` 框中输入要创建 `Web` 点的路径，或点击 `Browse` 按钮选择位置。
4. 选择存储 `Web` 点的文件夹。
5. 点击 `Open` 按钮返回 `Web` 站点对话框。

## 解决方案

创建站点后，你需要为站点添加一个 `Default` 页面：

6. 在资源管理器中右键点击 `Web` 名称，选择 `添加→新建项...`。打开 `添加新建项` 对话框。
7. 在中间面板中选择 `Web Form` 选项，并在 `Name` 框中提供 `Web` 表单名称（在此例中为 `Default`），点击 `添加`。

`Default` 页面已添加并在源中打开。

# 第 10 章：介绍 ASP.NET 4.5 和 Web Forms

- 4. 点击 `Local IIS` 选项卡。在树视图中，打开你想要创建新网站的 `IIS` 站点节点，这通常是 `Default Web Site`（默认网站）。现在，你可以选择要创建本地 `IIS` 站点的文件夹，或者你可以创建一个新站点。
- 5. 点击 `New Web Application`（新建 `Web` 应用程序）并为文件夹提供名称。在此情况下，可以使用 `LocalIISWebsite`，或者通过点击 `Create New Virtual Directory`（创建新虚拟目录）图标为该网站创建一个新的虚拟目录。在 `New Virtual Directory` 框中，输入网站的别名，然后输入或选择文件所在的文件夹。如果文件夹不存在，系统将提示你创建一个。
- 6. 点击 `Open`（打开）按钮返回到 `New Web Site`（新建网站）对话框。选择语言为 `Visual C#` 并点击 `OK`。这会在本地 `IIS` 中创建一个网站。

最初，你可以在远程计算机上创建 `Remote IIS` 网站。要执行此操作，请执行以下步骤：

- 1. 点击 `FILE→New→Web Site` 菜单项。出现 `New Web Site` 对话框，如图 10.21 所示。
- 2. 从左窗格选择 `Installed→Visual C#` 选项，然后从中间面板选择 `ASP.NET Empty Web Site`。
- 3. 在 `Web site` 下拉列表中选择 `HTTP`，然后在 `ASP location` 框中输入你想创建网站的路径，或点击 `Browse`（浏览）按钮。出现 `Choose Location` 对话框，如图 10.23 所示。

![](img/17af790174c480761404624aeed9b30b_485_0.png)

> 图 10.23：选中了远程站点的 Choose Location 对话框

- 4. 点击 `Remote Site` 选项卡并指定网站的位置，如图 10.23 所示。点击 `OK` 按钮返回到 `New Web Site` 对话框。
- 5. 点击 `OK` 按钮。这会在远程计算机上创建一个网站。

## 使用基于 FTP 的位置

我们知道 `Visual Studio` 可用于打开和编辑 `FTP` 服务器上的网站。要执行此操作，使用 `Visual Studio`，首先连接到任何你具有读取或写入权限的 `FTP` 服务器。然后在 `FTP` 服务器上创建或编辑网页。在这里我们学习如何创建一个名为 `FTPWebsite` 的基于 `FTP` 的网站。要执行此操作，请执行以下步骤：

- 1. 点击 `FILE→New→Web Site` 菜单项。出现 `New Web Site` 对话框，如图 10.24 所示：

![](img/17af790174c480761404624aeed9b30b_486_0.png)

图 10.24：使用 `FTP` 创建网站

- 2. 从中间面板选择 `ASP.NET Empty Web Site` 模板。在 `Web location` 下拉列表中选择 `FTP`，然后在 `location` 组合框中输入你想创建网站的路径，或通过点击 `Browse` 按钮选择位置。出现 `Choose Location` 对话框，如图 10.25 所示：

![](img/17af790174c480761404624aeed9b30b_486_1.png)

图 10.25：选中了 `FTP Site` 选项的 `Location` 对话框

- 3. 点击 `FTP Site` 选项卡。现在输入服务器名称、端口号和目录，如图 10.25 所示，并点击 `Open` 按钮返回 `Web Site` 对话框。
- 4. 选择语言为 `Visual C#` 并点击 `OK` 按钮创建基于 `FTP` 的网站。

## 设置 Web Form 的标题

你可以通过 `HTML` 头部 `Title` 属性为 `Web Form` 设置标题。默认情况下，当 `Web Form` 显示时，你会在浏览器标题栏看到 `Title`。你可以使用 `Title` 属性为 `Web Form` 指定一个标题。

> 要显示网页，网页必须包含一个带有 `runat="server"` 属性的 `<head>` 元素。

让我们使用应用程序 `FileSystemWebsite` 为其 `Default` 页显示标题。要执行此操作，在 `Default` 页的 `<title>` 标签中添加一个值，如代码 10.4 所示。

代码 10.4：设置 `Web Form` 的标题

```aspx
@Page Language="C#" AutoEventWireup="true" Inherits="_Default" %>
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
  <head>
    <title runat="server">Welcome Page</title>
  </head>
  <body>
    <form id="form1" runat="server">
      <div></div>
    </form>
  </body>
</html>
```

你现在可以通过按 `F5` 键运行应用程序。结果如图 10.26 所示：

![](img/17af790174c480761404624aeed9b30b_487_0.png)

图 10.26：`Default Web Form` 的标题

在下一节，你将学习如何为 `Web Form` 添加背景颜色。

## 为 Web Form 添加背景颜色

- 1. 在 `Design View`（设计视图）中选择 `Web Form`。然后点击工具栏上的 `Background Color`（背景颜色）按钮。出现 `More Colors` 对话框，如图 10.27 所示。

![](img/17af790174c480761404624aeed9b30b_488_0.png)

代码 10.5：添加 `Web Form` 的背景颜色

```aspx
@Page Language="C#" AutoEventWireup="true" CodeFile="default.aspx.cs" Inherits="Default" %>
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
  <head>
    <meta charset="server">
    <title>Welcome Page</title>
  </head>
  <body style="background-color:#CCCFFF">
    <form id="form1" runat="server">
      <div></div>
    </form>
  </body>
</html>
```

- 3. 按 `F5` 运行网站，通过更改页面颜色显示输出，如图 10.28 所示：

![](img/17af790174c480761404624aeed9b30b_488_1.png)

在下一节，你将学习为 `Web Form` 添加背景图片。

## 为 Web Form 添加背景图片

你也可以为应用程序的 `Default` 页添加背景图片。我们使用 `FileSystemWebsite` 应用程序学习如何向 `Default` 页添加背景图片。要执行此操作，请执行以下步骤：

- 1. 为应用程序添加图片。

> 注意：向应用程序添加图片，只需复制图片文件，在 `Solution Explorer` 中右键点击项目名称并从上下文菜单选择 `Paste`（粘贴）。

- 2. 在网页源代码中添加高亮的代码。选定的背景图片被添加到 `Default` 页，如代码 10.6 所示。

代码 10.6：为 `Web Form` 添加背景图片

- 3. 按 `F5` 运行控件，显示输出，如图 10.29 所示：

![](img/17af790174c480761404624aeed9b30b_489_0.png)

接下来你将学习向 `Web Form` 添加控件。

如果 `Web Form` 不包含任何控件，它将是不完整的。通常，几乎所有的 `Web Form` 都附加了控件。在本节中，你将学习如何向 `Web Form` 添加控件并探索控件的各种属性。我们采用 `FileSystemWebsite` 应用程序相同的示例，向其 `Default` 页添加控件。要执行此操作，从 `Toolbox`（工具箱）中拖放三个 `Label` 控件、两个 `TextBox` 控件和一个 `Button` 控件到 `Default` 页上，并设置它们的文本，如图 10.30 所示。

显示默认页的设计视图，如图 10.30 所示：

![](img/17af790174c480761404624aeed9b30b_490_0.png)

图 10.30：`Default` 页的设计视图

## 隐藏和显示控件

让我们学习如何使用 `Visible` 属性在网页上隐藏和显示控件。我们使用 `FileSystemWeb` 应用程序作为示例，隐藏在页面首次加载时位于 `Default` 页底部的标签。要执行此操作，请执行以下步骤：

- 1. 在设计时选择 `Label` 控件，并在 `Properties`（属性）窗口中将 `Visible` 属性设为 `False`。在我们的案例，我们选中了 `Label3`。
- 2. 按 `F5` 键执行应用程序，将显示结果，如图 10.31 所示：

![](img/17af790174c480761404624aeed9b30b_490_1.png)

图 10.31：显示隐藏标签的页面

在图 10.30 中你可以看到网页底部的标签是可见的，但在图 10.31 中，它是隐藏的。现在，如果你想通过按钮显示隐藏的标签，双击该按钮（例如设计视图中的 `Welcome` 按钮），并在按钮的 `Click` 事件中添加以下代码：

```aspx
protected void button1_Click(object sender, EventArgs e)
{
    Label3.visible = true;
    Label3.Text = "welcome " + TextBox2.Text;
}
```

## 第 10 章：介绍 ASP.NET 4.5 和 Web Forms

3. 在文本框中输入名称和学号，然后点击 `Welcome`（欢迎）按钮。`Label` 控件将变为可见，并显示文本 `<UserName>`，如图 10.32 所示。

![](img/17af790174c480761404624aeed9b30b_491_0.png)

图 10.32：显示带有欢迎消息的可见 `Label`

当你不希望用户访问某个控件时，通常会禁用该控件。通常，我们会禁用具有自动生成用户 `ID` 的控件。让我们学习如何禁用包含用户学号的文本框。我们在 `Welcome` 按钮的 `Click` 事件中禁用该文本框。要这样做，请在 `Click` 事件中添加高亮的代码，如列表 10.7 所示：

列表 10.7：禁用和启用 `TextBox` 控件的代码

```csharp
protected void button1_Click(object sender, EventArgs e)
{
    Label3.Visible = true;
    Label3.Text = "Welcome " + TextBox2.Text;
    TextBox1.Enabled = false;
}
```

默认情况下，`Enabled` 属性会将文本框设为灰色，现在按 `F5` 键运行应用程序。随后会出现 `Welcome` 按钮和禁用的文本框，如图 10.33 所示：

![](img/17af790174c480761404624aeed9b30b_491_1.png)

图 10.33：显示禁用的文本框

现在，要启用此文本框，只需将其 `Enabled` 属性设置为 `true` 即可。

## 设置控件的标题和字体

你可以使用控件的 `Text` 属性设置任何控件的标题。该属性在设计时和运行时均可用。添加 `Web Form` 后，你可以在 `Properties`（属性）窗口的 `Text` 属性中置入相应的文本来设置其标题。

你可以使用 `Font` 属性更改控件的字体。要这样做，首先选择控件，然后在其 `Properties` 窗口中展开 `Font` 属性。最后，根据需要设置字体和大小，如图 10.34 所示：

![](img/17af790174c480761404624aeed9b30b_492_0.png)

图 10.34：使用属性窗口设置字体

与设置 `Text` 属性类似，我们为 `Default Web` 页面上的所有控件设置了 `Font` 属性。按 `F5` 键运行 `FileSystemWebsite` 应用程序，所有控件的字体如图 10.35 所示：

![](img/17af790174c480761404624aeed9b30b_492_1.png)

图 10.35：显示更改了字体的 `Web Form`

## 第 10 章：介绍 ASP.NET 4.5 和 Web Forms

### 设置控件的 Tab 顺序

假设你的鼠标无法工作，但你仍然想访问 `Web` 页面。该怎么做？当然，你可以使用键盘。通过 `TabIndex` 属性管理控件。`TabIndex` 属性是当前控件在 `Tab` 顺序中的索引，通常从 `0` 开始。当用户按下 `Tab` 键时，焦点将根据 `tab` 索引升序从一个控件移动到另一个控件。在本节中，我们将学习如何为 `Default` 属性上的所有控件设置 `tab` 顺序。要这样做，选择你想设置 `tab` 顺序的控件并打开其 `Properties` 窗口。现在，将控件的 `TabIndex` 属性设置为 `0`，依此类推。在这种情况下，将 `TextBox1` 的 `TabIndex` 设置为 `1`，`TextBox2` 设置为 `2`，最后 `Button` 设置为 `3`。通常，你会为 `Label` 控件设置 `tab` 键。列表 10：在 `Web` 页面中设置控件 `Tab` 顺序源代码

列表 10：在 `Web` 页面中设置控件 `Tab` 顺序
