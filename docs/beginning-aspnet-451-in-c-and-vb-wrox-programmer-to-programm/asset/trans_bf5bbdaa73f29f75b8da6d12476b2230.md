

在名为 c:\BeASPNET\site 的文件夹中。注意这个文件夹名称，因为它在整本书中都会用到。如果你决定使用不同的文件夹，请确保在书中看到该文件夹名称时使用你的位置。确保不要使用特殊字符，如井号 (#) 或在文件夹名称中插入空格，否则在开发网站时会出现问题。最后，确保不要在 Windows 文档文件夹 c:\Users\UserName\Documents\ 下创建此文件夹，因为当除你自己之外的其他账户访问你的网站时，后续会出现问题。

## TRY IT OUT Creating New ASP.NET 4.5.1 Website

- 1. 首先使用文件资源管理器（旧版 Windows 中为 Windows 资源管理器）在驱动器的根目录下创建一个名为 BeASPNET 的文件夹。在该文件夹内，再创建另一个名为 site 的文件夹。你应该得到一个文件夹 c:\BeASPNET\site。如果你按照本书“Introduction”步骤中的说明解压了本书的源代码，你已经拥有 BeASPNET 文件夹，其中包含 Source 和 Resources 文件夹。你仍需要创建 site 文件夹。如果你想同时跟随 VB.NET 和 C#，请创建两个文件夹 BeASPNETVB 和 BeASPNETCS，并使用两个 Visual Studio 实例。
- 2. 启动 Visual Studio 并选择 File -> New Web Project 或 New -> Web Site，具体取决于你的 VS 版本。
- 3. 在屏幕顶部的目标框架下拉列表中，选择 .NET Framework 4.5.1。
- 4. 在左侧的 Installed Templates 区域中，在 Visual Basic 和 Visual C# 之间进行选择。本书中的所有示例都同时以两种编程语言展示，因此你可以选择自己喜欢的一种。
- 5. 在中间区域选择 ASP.NET Empty Web Site。
- 6. 在 Web Location 下拉列表中，确保选择了 File System。其他两个选项（HTTP 和 FTP）分别可让你打开在 IIS 上运行的站点（在本地机器或使用所谓的 Microsoft FrontPage Extensions 的远程服务器上）以及从 FTP 服务器打开站点。
- 7. 单击位置文本旁边的 Browse 按钮，浏览到 C:\BeASPNET\site（你在本次练习第一步中创建的文件夹），然后单击 Open。
- 8. 单击 OK，VS 将为你创建新的站点。

> COMMON MISTAKES 不要错误地使用 File New Project 模板创建一个新的 Web Application Project，因为该项目与本书中的练习不兼容。

## Creating Websites with Visual Studio | 39

![](img/9e033e3b9560597824f8b22941d6d8bb_76_0.png)

FIGURE 2-2

## How It Works

一旦你单击 OK，VS 就会为 web 创建一个全新的、空的网站。此新网站仅包含配置文件（称为 `web.config` 和 `Web.debug`）。在 Solution Explorer 中，你的网站现在看起来像图 2-3（我们展开了 `web.config` 文件）。如果你看不到顶层的 Solution Explorer，请在 VS 中选择 Tools -> Options，并在 Projects and Solutions 类别中选择 Always Solution。

由于基于 Empty Web Site 模板的网站只是一个 VS 查看的简单 Windows 文件夹，因此磁盘上的实际文件夹包含相同的文件。没有使用额外的文件来创建站点，如图 2-4 所示，其中显示了文件资源管理器中 C:\BegASPNET\ 下的文件夹。

![](img/9e033e3b9560597824f8b22941d6d8bb_76_1.png)

FIGURE 2-3

![](img/9e033e3b9560597824f8b22941d6d8bb_76_2.png)

FIGURE 2-4

如果你看不到 web 文件的 .config 扩展名，不用担心。你将在后面的练习中了解如何查看文件扩展名。

随着你阅读本书的进展，你会向站点添加新的文件和文件夹。这些额外文件和文件夹会显示在 Solution Explorer 中，也会出现在 Windows 文件夹 C:\BegASPNET\Site 中。

在 Web Site Project 模板上打开网站与创建新网站非常相似。在下一节中，你将快速了解如何在 VS 中打开现有站点。

## Opening Existing Websites

与创建新站点一样，在 VS 中打开现有站点也会给你一些关于网站源位置的选项。你可以选择从本地文件系统打开站点，从本地 IIS 服务器打开，从 FTP 远程服务器打开，使用 Microsoft FrontPage Server Extensions 从远程站点打开，或从 Microsoft 的 Team Foundation Server 等中央源代码控制系统打开。图 2-5 显示了 VS 中的 Open Web 对话框。

![](img/9e033e3b9560597824f8b22941d6d8bb_77_0.png)

FIGURE 2-5

要打开此对话框，请在 VS 中选择 File Open Web Site（不要错误地选择 File Open Web Projects）。书中的所有示例都假设你始终从本地文件系统打开 Planet Wrox 网站，使用 File System，即窗口左侧列中的第一个按钮。然后在右窗格中，定位你的网站（本例中为 C:\BegASPNET\Site）并单击 Open 按钮。

你在上一个 Try Out 中创建的站点是一个非常基础的站点。为了使其更有用，你需要向其中添加文件。你可以使用的多种文件类型以及它们如何添加到站点是接下来的讨论主题。

## WORKING WITH FILES IN YOUR WEBSITE

ASP.NET Web Forms 至少包含一个 Web Form（扩展名为 .aspx 的文件），通常包含大量文件。VS 中有许多不同的文件类型可供使用，提供不同的功能。在下一节中，你将看到在 VS 中使用的最重要文件类型。此外，你还将学习几种将这些文件添加到站点的方法。

## The Many File Types of an ASP.NET Website

为了让你了解 ASP.NET 中可以使用哪些不同文件，图 2-6 显示了可让你向站点添加新文件的对话框（通过在 Solution Explorer 中右键单击你的网站并选择 Add+ Add New Item，或通过主菜单选择 Add+ Add New Item）。

![](img/9e033e3b9560597824f8b22941d6d8bb_78_0.png)

FIGURE 2-6

为了更轻松地找到所需的文件类型，你可以使用对话框右上角的搜索框。只需输入你正在查找的类型的前几个字母并按 Enter。VS 会将文件列表过滤为与你的搜索词匹配的结果。

可以添加到站点的文件可以分为几个不同的类别。最重要的文件——即本书示例中反复使用的文件——接下来会进行讨论。

## Web Files

Web 文件特定于 Web 应用程序，可以直接由浏览器请求，或用于构建在浏览器中请求的部分网页。下表列出了你在 ASP.NET Web Forms 网站中通常使用的各种 Web 文件及其扩展名，并描述了每个文件的使用方式。

| FILE TYPE | EXTENSION | DESCRIPTION |
|---|---|---|
| Web Form | .aspx | 任何 ASP.NET Web Forms 网站的核心；代表用户在其浏览器中查看的页面。 |
| Master Page | .master | 使你能够定义网站的全局结构和外观。你将在第 6 章看到其用法。 |
| Web User Control | .ascx | 包含可在站点多个页面中重复使用的页面片段。第 8 章完全致力于用户控件。 |
| HTML Page | .html | 可用于在网站中显示静态 HTML。 |
| Style Sheet | .css | 包含可让你设置网站样式和格式的 CSS 代码。你将在第 3 章了解更多关于 CSS 的内容。 |
| Web Configuration File | .config | 包含在整个站点中使用的全局配置信息。你将在本章后面看到如何使用 Web.config |
| Site Map | .sitemap | 以 XML 格式包含站点中文件的层次结构表示。站点地图用于导航，并在第 7 章中讨论。 |
| JavaScript File | .js | 包含可在客户端浏览器中执行的 JavaScript。 |
| Skin File | .skin | 包含网站中控件的设计信息。皮肤在第 6 章中讨论。 |

下一个 Try It 练习将向你展示如何向站点添加新的母版页，该母版页在整本书中使用。

## TRY IT OUT Adding Files to Your Site

- 1. 如果尚未打开，请通过选择 File � Open Web Site 打开你之前创建的 Planet Wrox 网站。确保你是从文件打开站点，定位包含你的站点的文件夹（C:\BEASPNET\site），然后单击 Open 按钮。
- 2. 在 Solution Explorer 中，右键单击你的站点并选择 Add ⇩ New Folder。

> COMMON MISTAKES 确保你单击的是实际的站点，而不是 Web.config 文件或顶部的 Solution 节点（见图 2-3），否则你将得不到正确的菜单项。

