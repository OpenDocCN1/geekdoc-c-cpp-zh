
注意：此处应根据逻辑将 Inherits 更改为 `$relnamespace$$_safeitemename`（此处原文示例显示为 Temporary，但描述意图是替换）。*更正：根据上下文逻辑，此处应替换为占位符。*

(由于提供的文本在末处中断，此处翻译至此处结束)

# 第 6 章 创建外观一致的网站

该功能基于你使用“添加新建项”（Add New Item）对话框创建的模板，它将 `$urlfoldername$` 替换为文件夹名称（如果是添加到网站根目录的文件，则留空），并将 `$safeitemname$` 替换为页面的实际名称。在练习中，你使用 `TestPage.aspx` 作为页面的新名称，因此你在代码后台中生成了一个名为 `_TestPage` 的类，该类继承自全局的 `BasePage`。下划线 `_` 在两个两个占位符之间是硬编码的，实际上只有当你从此模板将 Web 表单添加到子文件夹时才真正需要。然而，一个有效的类标识符可以安全地将其留在网站的文件夹中。如果你添加了子文件夹（例如 `Demos` 文件夹），类将带有文件夹名称的前缀，因此你会得到一个类 `$urlfoldername$` 和 `$safeitemname$`，你还可以使用一些其他占位符。可以在 `mdn.microsoft.com` 的 MSDN 网站上搜索 `$safeitemname` 来查找其他参数。

如果你需要对导出的模板进行更改，可以重新执行整个导出过程，或者手动编辑 zip 包中的文件。

有了这个导出的模板，你现在有一种非常快速的方法为网站添加继承自 `BasePage` 类的页面。你不再需要手动更改基文件的代码后台或页面的标记。

除了主页（master pages）和当前的 `BasePage` 类外，你还有更多选项来创建外观一致的网站。其中一个就是主题（themes）。

# 主题（THEMES）

到目前为止，你已经看到了如何创建主页来定义网站中页面的全局外观和感受。你还看到了如何通过使用中心基页来自定义页面的行为。然而，你有更多方法来影响网站的外观和感受：主题和皮肤（skins）。皮肤将在本章稍后部分处理，因为它们是主题的可选部分，需要先讨论主题。

主题是定义页面外观的文件集合。主题通常包含皮肤文件、CSS 文件和图像。你在网站根目录的特殊 `App.Themes` 文件夹中定义主题。在该文件夹内，你创建一个或多个子文件夹来定义实际的主题。在每个子文件夹内部，你可以有多个组成主题的文件。图 6-12 显示了定义了两个主题：单色（Monochrome）和深灰（DarkGrey）的网站解决方案资源管理器。

当主题激活时，主题文件夹中每个 CSS 文件的链接会自动添加到你页面的 `<head>` 部分。你稍后会看到它是如何工作的。主题文件夹中的图像可以在 CSS 文件中引用。你可以使用它们来更改网站的共同元素，例如背景图像，或用于项目列表或导航列表的图像。

![](img/9e033e3b9560597824f8b22941d6d8bb_253_0.png)

图 6-12

要创建一个主题，你需要执行以下操作：

- 如果网站中尚不存在，请创建一个特殊的 `App_Themes` 文件夹。
- 对于你想要创建的每个主题，创建一个以主题命名的子文件夹，例如图 6-12 中的 `Monochrome` 或 `DarkGrey`。
- （可选）创建一个或多个作为主题一部分的 CSS 文件。虽然以主题命命名 CSS 文件有助于识别正确的文件，但这并非强制要求。你添加到主题文件夹的任何 CSS 文件都会在运行时自动添加到页面中。
- （可选）向主题文件夹中添加一个或多个图像。如前所述，CSS 文件应使用相对路径引用这些图像。
- （可选）向主题文件夹中添加一个或多个皮肤文件。皮肤允许你为特定控件定义单独属性（如 `ForeColor` 和 `CssClass`），这些属性会在运行时应用。

遵循这些步骤后，你就可以配置你的网站或单个页面了。

## 主题类型（Different Types of Themes）

ASP.NET 页面有两个属性可以启用主题：`Theme` 属性和 `StyleSheetTheme` 属性。它们都使用 `App_Themes` 文件夹中定义的主题。尽管它们看起来非常相似，但它们在页面生命周期中的应用时间不同。你可以在标记中设置 `StyleSheetTheme` 来看到这种区别。例如，在页面标记中设置 `Theme` 属性：

```asp
@Page Language="VB" AutoEventWireup="false" CodeFile="Default.aspx.vb"
Inherits="Default" Theme
%>
<asp:Button ID="Button" runat="server" Text="Click" />
```

`Theme` 属性在页面生命周期中较晚应用，而 `StyleSheetTheme` 属性则较早。通过设置 `StyleSheetTheme` 属性，你稍后会看到效果。

# 选择 Theme 还是 StyleSheetTheme（Choosing Between Theme and StyleSheetTheme）

在 `Theme` 和 `StyleSheetTheme` 属性之间进行选择，取决于你希望何时应用设置。如果你希望通过 `Theme` 属性为控件提供默认值，请使用它，因为 `Theme` 属性可以覆盖你对控件的自定义。如果你希望通过 `StyleSheetTheme` 属性来执行控件的设置，请使用它。

## 应用主题（Applying Themes）

要为网站应用主题，你有三种选择：在页面指令中设置、在 `web.config` 文件中设置，以及通过代码设置。

- 在页面级别设置主题。要应用主题，只需在页面指令中设置 `Theme` 或 `StyleSheetTheme` 属性：

```asp
@Page Language="VB" AutoEventWireup="false" CodeFile="Default.aspx.vb"
Inherits="Default" Theme="DarkGray" %>
```

一旦你输入 `Theme`，VS 就会弹出你在 `App_Themes` 文件夹中找到的所有主题。图 6-13 显示了这一点。

- 在网站级别设置主题。要为整个网站强制主题，在 `web.config` 文件的 `<system.web>` 元素中添加 `theme` 或 `StyleSheetTheme` 属性：

```xml
<pages theme="DarkGray" StyleSheetTheme="DarkGray">
```

确保你按照所示方式输入这些属性，因为配置文件中的 XML 是大小敏感的。你在这里设置的属性随后将应用于页面类的 `Theme` 和 `StyleSheetTheme` 属性。

- 通过代码设置主题。设置主题的第三种也是方法是通过代码。在稍后的练习中查看它是如何工作的。

## 为你的网站创建新主题（Creating a New Theme for Your Website）

在练习中，你创建了两个主题：单色和深灰。对于每个主题，添加 CSS 布局，它会自动应用到站点。配置应用程序使用一个主题并切换以查看差异。

1. 添加特殊的 `App_Themes` 文件夹以创建你的主题。要执行此操作，右键点击解决方案管理器中的网站并选择添加 -> ASP.NET 主题。这不会创建 `App_Themes` 文件夹，但会立即为默认主题 `Theme1` 创建子文件夹。使用 `Monochrome` 作为新名称。你的解决方案资源管理器现在显示如图 6-14。

![](img/9e033e3b9560597824f8b22941d6d8bb_255_1.png)

图 6-14

2. 从 `Styles` 文件夹中移动 `Styles` 文件夹。你可以将其拖入新文件夹，或者使用 `Ctrl+X` 剪切文件，点击 `Monochrome` 文件夹，然后按 `Ctrl+V` 再次粘贴。你可以留下空的 `Styles` 文件夹，因为以后还会再次使用它。

3. 为了让你的 CSS 来源更加清晰，请将文件名从 `Styles.css` 重命名为 `Monochrome.css`。你可以通过选中文件并按 `F2` 或右键点击它并选择“重命名”来重命名。

4. 因为主布局现在将由主题控制，你不再需要在主页的 `<head>` 部分中使用旧 CSS 的 `<link>` 元素，因此可以将其删除。为此，打开主页，切换到标记视图（Markup View），并从代码中删除以下高亮行：

```html
<head runat="server">
<title></title>
<asp:ContentPlaceHolder id="head" runat="server">
</asp:ContentPlaceHolder>
<link href="../Styles.css" rel="stylesheet" type="text/css" />
```

5. 下一步是将主题应用到 Web 环境。从站点打开 Web 文件并直接在 `<system.web>` 元素内部编辑，创建一个带有 `theme` 属性的 `<pages>` 元素，指向 `Monochrome` 主题。由于 `web.config` 文件在 IntelliSense 中不支持主题支持，你需要手动输入名称。

```xml
<system.web>
<pages theme="Monochrome" />
```

6. 要测试主题，保存所有更改，然后在浏览器中请求 `Default.aspx`。网站的设计应该与预期的完全一致。

> **常见错误**：如果你收到关于无效页面标题的错误，请返回 Visual Studio 并将 `@ Default.aspx` 的 `Title` 属性更改为“Welcome to Planet Wrox.”。如果你的设计看起来不符合预期，请在浏览器中按 `Ctrl+F5` 或 `Ctrl+R`。这将强制强制刷新，意味着你获得的是文件的最新版本，而不是页面的缓存副本。

现在，不再从主页链接 CSS 文件，而是通过 `Web.config` 文件中设置的主题包含在页面源代码中。要查看其工作原理，请在浏览器中打开页面的 HTML 源代码。在顶部你将看到以下代码（我调整了布局以提高可读性）：

```html
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<title>Welcome to Planet Wrox</title>
<script src="Scripts/modernizr-2.7.1.js"></script>
<link href="App.Themes/Monochrome/Monochrome.css" type="css" rel="stylesheet" />
</head>
<body>
```

注意，来自 `Monochrome` 文件夹的样式表链接已注入到页面的 `<head>` 中。ASP.NET 运行时会对它包含在当前活动文件夹中的每个 CSS 文件（按字母顺序排序）执行此操作，因此请确保保留你的主题文件夹，以避免浏览器包含并下载不必要的文件。还要注意 `<link>` 是如何紧跟在 `<head>` 标签之后添加的。这确保了该文件会在你添加的所有其他文件（例如通过主页）之后包含。这与 `StyleSheet` 属性的方式不同。这种类型的主题允许其设置被覆盖，它从文件顶部导入，为紧随其后的其他 CSS 文件更改页面的视觉效果留了空间。

7. 返回 Visual Studio 并在设计视图（Design View）中打开主页。注意所有设计都消失了，现在遵循页面布局。遗憾的是，VS 没有显示你使用 `theme` 属性的主题。但是，你可以通过设置 `StyleSheetTheme` 属性来克服这一点。打开 `Web.config` 文件，找到你之前创建的 `<pages>` 元素，并添加以下属性：

```xml
<pages theme="Monochrome" StyleSheetTheme="Monochrome" />
```

8. 保存 `Web.config` 的更改，重新打开主页并切换到设计视图。你会发现 VS 现在为你的页面应用了正确的信息。

9. 为站点添加另一个主题，在 `App_Themes` 下创建一个新文件夹并命名为 `DarkGrey`。现在，打开你解压随书下载的代码的文件夹。如果你遵循了书中的说明，你的文件夹位于 `C:\ASPNET\Resources`。如果你没有这些文件，可以在 `www.wrox.com/go/aspnet-451` 获取。打开第 06 章和主题文件夹，将文件资源管理器中的 `DarkGrey` 文件夹拖入 VS 中的 `DarkGrey` 主题文件夹。如果拖放不起用，请在文件资源管理器中使用 `Ctrl+C` 复制文件，然后在 VS 中使用 `Ctrl+V` 将文件粘贴到项目。。你的解决方案资源管理器现在应该显示图 6-15。

你将在稍后的条目中添加 CSS 文件引用的图像。

10. 再次打开 `Web.config` 文件，将`<pages>` 元素中的其他 `Monochrome` 更改为 `DarkGrey`。再次保存更改并按 `Ctrl+F5`。你看到的将不是蓝色的 `Monochrome`，而是应用了 `DarkGrey` 主题的网站，如图 6-16 所示。如果你没有看到占位符、主内容和侧边栏并排，请确保你的浏览器足够宽以显示所有内容。

![](img/9e033e3)

## 第 6 章创建外观一致的网站

![](img/9e033e3)

## 图 6-15

![](img/9e033e3)

## 图 6-16

![](img/9e033e3)

## 工作原理

不再从主页链接 CSS 文件，而是通过 `Web.config` 文件中设置的主题包含在页面源代码中。要查看其工作原理，请在浏览器中打开页面的 HTML 源代码。在顶部你将看到以下代码（我调整了布局以提高可读性）：

```html
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<title>Welcome to Planet Wrox</title>
<script src="Scripts/modernizr-2.7.1.js"></script>
<link href="App.Themes/Monochrome/Monochrome.css" type="css" rel="stylesheet" />
</head>
<body>
```

注意，来自 `Monochrome` 文件夹的样式表链接已注入到页面的 `<head>` 中。ASP.NET 运行时会对它包含在当前活动文件夹中的每个 CSS 文件（按字母顺序排序）执行此操作，因此请确保保留你的主题文件夹，以避免浏览器包含并下载不必要的文件。还要注意 `<link>` 是如何紧跟在 `<head>` 标签之后添加的。这确保了文件会在你添加的所有其他文件（例如通过主页）之后包含。这与 `StyleSheet` 属性的方式不同。这种类型的主题允许其设置被覆盖，它从文件顶部导入，为紧随其后的其他 CSS 文件更改页面的视觉效果留了空间。

7. 返回 Visual Studio 并在设计视图（Design View）中打开主页。注意所有设计都消失了，现在遵循页面布局。遗憾的是，VS 没有显示你使用 `theme` 属性的主题。但是，你可以通过设置 `StyleSheetTheme` 属性来克服这一点。打开 `Web.config` 文件，找到你之前创建的 `<pages>` 元素，并添加以下属性：

```xml
<pages theme="Monochrome" StyleSheetTheme="Monochrome" />
```
