
此处使用 application/atom+xml，因此采用了 AtomPub 格式。如果将 Accept 头改为 application/json，则会得到如下响应：

```json
{
  "d" : {
    "EntitySets" : [
      "Categories", "CustomerDemographics", "Customers", "Employees",
      "Order_Details", "Orders", "Products", "Region", "Shippers",
      "Suppliers", "Territories"
    ]
  }
}
```

上述代码的格式正是 ASP.NET AJAX 页面所需的格式。

## 构建 ASP.NET Web 包

将 Web 应用程序部署到服务器的最简单方法之一，是使用 Visual Studio 2010 新增的内置发布功能。在幕后，这一新功能使用 Microsoft 的 Web 部署工具（也称为 MSDeploy），这意味着，如果你想要将应用程序部署到服务器，该服务器上必须安装 MSDeploy，应用程序的部署才能实际生效。

创建并传递的包实际上是一个物理文件——一个 .zip 文件。此 .zip 文件包含将 Web 应用程序及其所有设置重新部署到新环境所需的一切。除 .zip 文件外，它还包含一个清单文件和一个命令文件，用于在主机上启动包的安装。

部署此应用程序的第一种方式是使用 Visual Studio 2010 中新增的“一键发布”功能。为此，请在 Visual Studio 解决方案资源管理器中右键单击项目，然后从提供的菜单中选择“发布”选项。随后将出现“发布 Web”对话框，如下图所示。

![](img/7954dcc7dd1d929d072aec8e9531b6cc_68_0.png)

由于许多开发人员会不断将 Web 应用程序部署到测试、暂存和生产环境中，因此可以让你将部署选项存储在一个配置文件中，以便反复使用。另请注意，上图的对话框中，此部署的生成配置设置为 Release。此设置来自你在选择“发布”选项之前，在 Visual Studio 2010 工具栏中所做的设置。

“发布 Web”对话框包含下表中定义的以下选项。

| 设置 | 说明 |
|---|---|
| 配置文件名称 | 已保存配置文件的名称。这让你能够将设置作为默认值，用于重复部署。 |
| 生成配置 | 指定生成编译将在“调试”还是“发布”模式下进行。你可以先在 Visual Studio 的工具栏中设置此选项。 |
| 发布方法 | 你要用于部署的方法。可能的选项包括 MSDeploy 发布、FTP、文件系统和 FPSE。 |
| 服务 URL | 指定主机服务器上 MSDeploy 的位置。此 URL 指向实际具有 MSDeploy 功能的 IIS 处理程序，其构造方式类似于 http://myhostserver:8172/MsDeploy.axd。 |
| 站点/应用程序 | 指定应用程序将部署到的位置。你可以在此指定站点以及放置应用程序的虚拟目录。例如 MyDomain.com/MyApplication。 |
| 在目标上标记为 IIS 应用程序 | 如果选择此选项，IIS 会将“站点/应用程序”文本框中定义的终结点视为应用程序根目录。 |
| 不删除目标上的多余文件 | 如果未选择此选项，“一键发布”选项将首先删除主机服务器位置上的所有内容，然后再应用文件和设置。 |
| 允许不受信任的证书 | 如果选择此选项，你将信任自行发布的证书，或与目标 URL 不匹配的证书。 |
| 用户名 | 用于 IIS 连接的用户名。 |
| 密码 | 用于 IIS 连接的密码。 |
| 保存密码 | 指定 Visual Studio 发布功能是否将密码保存到配置文件中。 |

除了使用 MSDeploy 选项外，你会发现通过新的“发布 Web”对话框提供的其他选项更加简单。下图显示了所提供的其他三个部署选项的设置。

![](img/7954dcc7dd1d929d072aec8e9531b6cc_70_0.png)

在此图中，你可以看到使用 FTP、文件系统或 FrontPage 服务器扩展进行部署的一些标准设置。

Visual Studio 2010 现在所支持的 MSDeploy 功能的有趣之处在于，除了连接到远程 MSDeploy 处理程序并实时运行部署之外，你还可以创建一个可以随时运行的 MSDeploy 包。

Visual Studio 2010 现在包含创建这些包的功能，然后可以通过电子邮件或其他方式将这些包提供给其他人，让他们在自己的系统上运行。若要创建 Web 部署包，请在 Visual Studio 解决方案资源管理器中右键单击项目，然后从提供的菜单中选择“创建包”选项。

当你选择“创建包”选项时，包创建的进度会显示在 Visual Studio 状态栏中。在收到“发布成功”的通知后，你可以在应用程序的 obj 文件夹中找到整个包，例如

```
C:\Users\Evjen\Documents\Visual Studio 2010\
Projects\MyWebApplication\MyWebApplication\obj\Release\Package
```

该文件夹中包含构成包的所有文件。下图展示了这些文件。

![](img/7954dcc7dd1d929d072aec8e9531b6cc_71_0.png)

所有这些文件共同构成包，可用于部署过程。

- `MyWebApplication.deploy.cmd` 文件是供你的基础设施团队在主机（装有 MSDeploy）上运行，以安装应用程序及应用程序所需的所有设置的文件。
- 其他文件 `MyWebApplication.SetParameters.xml` 和 `MyWebApplication.SourceManifest.xml` 用于定义安装过程中使用的设置。
- 最后一个文件 `MyWebApplication.zip` 包含应用程序的内容。

使用此包，向另一个团队传递应用程序所需的安装变得很容易。一个很好的例子是，如果你要部署到 Web 场，因为需要进行多次部署，并且你希望所有这些部署保持一致。从这一个包运行安装可确保这种一致性。

包系统的另一个优点是，它允许你保存以前的部署，如果需要回头验证部署，可以轻松地获取已保存的包。它还使部署过程中的回滚变得容易。

![](img/7954dcc7dd1d929d072aec8e9531b6cc_72_0.png)

![](img/7954dcc7dd1d929d072aec8e9531b6cc_72_1.png)

## WPF

## 程序员参考

使用 C# 2010 和 .NET 4 的 Windows® Presentation Foundation

## WPF

## 程序员参考

## Windows Presentation Foundation
使用 C# 2010 和 .NET 4

## 代码隐藏文件

每当向项目添加窗口时，Expression Blend 或 Visual Studio 都会添加相应的代码隐藏文件。该文件的名称与 XAML 文件相同，但额外扩展名为 cs（用于 C#）或 vb（用于 Visual Basic）。例如，当你在 C# 中创建新的 WPF 项目时，项目将初始窗口包含在 Window1.xaml 文件中，并包含相应的代码隐藏文件 Window1.xaml.cs。

如果你使用的是 Visual Studio，则可以编辑代码隐藏文件，并充分利用 Visual Studio 强大的代码编辑功能，例如关键字突出显示和 IntelliSense。

## 示例代码

源代码可在本书网站 www.wrox.com 上下载，其中包含几个示例应用程序，它们都实现相同的功能，但使用不同的技术将代码隐藏附加到用户界面。

此图展示了一个程序的运行情况。你可以拖动滚动条或在文本框中输入值，以设置右侧所显示颜色的红色、绿色和蓝色分量。如果单击“应用”按钮，程序会将窗口的背景色设置为与当前样本匹配。

![](img/7954dcc7dd1d929d072aec8e9531b6cc_73_0.png)

你可以下载本节中的代码。请访问 WROX.COM 并搜索 ISBN 9780470477229
