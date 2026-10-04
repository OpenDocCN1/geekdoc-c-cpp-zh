
- 位于一个名为 `c:\BeASPNET\site` 的文件夹中。请记住此文件夹名称，因为它整本书都会用到它。如果你决定使用不同的文件夹，请在书中每次看到此文件夹名称时，务必使用你自己的路径。确保不要在文件夹名称中使用像井号 (#) 这样的特殊字符或插入空格，否则在开发网站时会遇到麻烦。最后，确保不要在 `c:\Users\UserName\Documents\` 的 Windows 文档文件夹下创建此文件夹，因为以后当你以外的账户访问你的网站时，你会遇到问题。

# 尝试一下：创建一个新的 ASP.NET 4.5.1 网站

- 1. 首先，使用文件管理器（旧版本 Windows 中的 Windows 资源管理器）在驱动器根目录下创建一个名为 `BeASPNET` 的文件夹。在文件夹内部再次创建一个名为 `site` 的文件夹。你最终应该得到一个文件夹 `c:\BeASPNET\site`。如果你遵循了本书“引言”步骤的说明并解压了本书的源码，你已经有了 `BeASPNET` 文件夹，其中又包含 `Source` 和 `Resources` 文件夹。不过你仍然需要创建 `site` 文件夹。如果你想同时参考 VB.NET 和 C#，可以创建两个文件夹：`BeASPNETVB` 和 `BeASPNETCS`，并使用两个 Visual Studio 实例。
- 2. 启动 Visual Studio，根据你的 VS 版本点击 `File -> New Web Project` 或 `New -> Web Site`。
- 3. 在屏幕顶部的目标框架（target framework）下拉列表中，选择 `.NET Framework 4.5.1`。
- 4. 在左侧的安装模板（Installed Templates）区域，在 Visual Basic 和 Visual C# 之间进行选择。书中所有的示例都以这两种编程语言展示，因此你可以选择你最喜欢的一种。
- 5. 在中间区域选择 `ASP.NET Empty Web Site`。
- 6. 在“Web 位置”（Web Location）下拉列表中，确保选择了 `File System`（文件系统）。另外两个选项（HTTP 和 FTP）分别允许你打开运行在 IIS 上的网站（在本地机器上或使用所谓的 Microsoft FrontPage 扩展的远程服务器上）以及从 FTP 服务器打开网站。
- 7. 点击位置文本旁边的“浏览”（Browse）按钮，浏览到 `C:\BeASPNET\site`（你在练习第一步中创建的文件夹），并点击“打开”（Open）。
- 8. 点击“确定”，VS 将为你创建新网站。

> 常见错误：不要误用 `File New Project` 模板创建新的 Web Application 项目，因为该项目与书中的练习题不兼容。

# 使用 Visual Studio 创建网站 | 39

![](img/9e033e3b9560597824f8b22941d6d8bb_76_0.png)

图 2-2

## 工作原理

一旦你点击确定，VS 就会为 Web 创建一个新的空白网站。这个新网站除了配置文件（称为 `web.config` 和 `Web.debug`）之外一无一物。在解决方案管理器（Solution Explorer）中，你的网站现在看起来如图 2-3 所示（我们展开了 `web.config` 文件）。如果你没有看到顶部的解决方案，请在 VS 中选择 `Tools -> Options`，并在 `Projects and Solutions` 类别中选择 `Always Solution`。

由于基于“Empty Web Site”模板的网站是 VS 查找的简单 Windows 文件夹，磁盘上的实际文件夹包含相同的文件。没有使用额外的文件来创建网站，如图 2-4 所示，该图显示文件资源管理器显示 `C:\BeASPNET\` 下的文件夹。

![](img/9e033e3b9560597824f8b22941d6d8bb_76_1.png)

图 2-3

![](img/9e033e3b9560597824f8b22941d6d8bb_76_2.png)

图 2-4

如果你没有看到 `.config` 扩展文件，请担心。你将在练习中看到如何查看文件扩展名。随着学习的进行，你会向网站添加新的文件和文件夹。这些额外的文件出现在解决方案管理器中，也会出现在 `c:\BeASPNET\site` 文件夹中。

在 Web Site 模板上打开网站与创建新网站非常相似。在下一节中，你将获得在 VS 中打开现有网站的快速概述。

# 打开现有网站

与创建新网站一样，在 VS 中打开现有网站会提供关于网站位置的几个选项。你可以选择从文件系统、本地 IIS 服务器、使用 FTP 的远程服务器、使用 Microsoft FrontPage 扩展的远程网站或如 Microsoft Team Foundation Server 的中央版本控制系统打开网站。图 2-5 显示了 VS 中的 Open 对话框。

![](img/9e033e3b9560597824f8b22941d6d8bb_77_0.png)

图 2-5

进入此对话框，在 VS 中选择 `File Open Web Site`（不要误选为 `Open Web Projects`）。书中的所有示例都假设你始终从文件系统（File System，它是窗口左列的第一个按钮）打开网站。然后在右窗中找到你的网站（`C:\BeASPNET\site`）并点击“打开”。
