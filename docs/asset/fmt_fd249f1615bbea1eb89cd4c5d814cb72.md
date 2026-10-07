
![](img/aaf6096fc6b4485534c737801bdbc4fd_165_0.png)

图 6-19：我的工作已更新

![](img/aaf6096fc6b4485534c737801bdbc4fd_165_1.png)

图 6-20：任务板中的任务自动更新

# 使用“我的工作”保持任务进度

除了创建“架”之外，Visual Studio 还会将你打开的窗口、工具窗口的位置和断点等作为属性存储起来。该工作项也会被自动更新，将其放回“待办（To Do）”，以便你的团队知道你不再正在处理该任务。

接下来，你按照要求进行代码审查并发送你的注释。

注意：欲查看 Visual Studio Ultimate 2012 或 Visual Studio Premium 2012 中代码审查过程的逐步指南，请参第 7 章。

一旦完成了该活动，你就可以回到上次的地方继续工作。确保你的“挂起（Suspended）”部分包含你上次工作的内容，如图 6-23 所示，这在万一你忘记时非常有用。选择挂起的工作并按下“恢复（Resume）”。

这将快速撤出更改，恢复你打开的文件，打开工具并恢复你的断点。

请注意，即使你觉得已经准备好恢复工作，但采取了许多人的做法，只是回到桌前开始做其他事情，也可以选择挂起的工作并将其与 Server 2012 中的当前工作合并，以支持在架上进行合并（得益于 Team Foundation Server 的更改和所有改进）。

当任务完成后，你可以直接在“我的工作”页面上点击“提交（Check In）”。它将带你进入“待处理更改（Pending Changes）”页面以审查你的更改、输入注释并提交。注意，如果你在解析工作项时关联了该工作项，那么当你执行提交时，该工作项将自动移动到下一个状态，在你的情况下是“已完成（Done）”。

工作项会在任务板中更新，并在更改集与你与更改关联的工作项之间创建一个链接。这一切通过使用“我的页面（My Page）”简单轻松地完成。

注意：“我的工作”页面非常实用，你可能会发现自己经常去那里。从 Visual Studio 任何地方快速进入“我的工作”页面的快捷键是 `Ctrl+0,M`。欲查看 Team Explorer 快捷键的完整列表，请访问 http://aka.ms/TEKeys。

![](img/aaf6096fc6b4485534c737801bdbc4fd_167_0.png)

图 6-23：恢复工作

# ECLIPSE 中的 TEAM FOUNDATION 版本控制

到目前为止，本章主要关注 Visual Studio 内部的体验。然而，Team Foundation 适用于各种环境，而不只是 Visual Studio 2012，也支持旧版本。

当你开始为你的任务进行更改时，版本控制更改的状态将显示在“我的工作”页面，并带有一个“查看更改”链接，带你进入待处理更改以获取更多信息，如图 6-21 所示。

这时，Julia 走到你的办公桌前，请你快速查看她刚刚发送的代码审查，因为她需要尽快提交。你想暂停当前的工作，以便先完成代码审查，然后再回来处理任务。只需点击“我的工作”页面上的“挂起（Suspend）”按钮即可。

当你点击“挂起”按钮时，它将创建一个新的“架（shelf）”来存放你在版本控制中的更改。默认情况下，“架”的标题将是你添加到“进行中”部分的第一个工作项的标题，你可以在按下“挂起”按钮之前编辑名称，如图 6-22 所示。

除了创建“架”之外，Visual Studio 还会将你打开的窗口、工具窗口的位置和断点等作为属性存储起来。该工作项也会被自动更新，将其放回“待办（To Do）”，以便你的团队知道你不再正在处理该任务。

接下来，你按照要求进行代码审查并发送你的注释。

注意：欲查看 Visual Studio Ultimate 2012 或 Visual Studio Premium 2012 中代码审查过程的逐步指南，请参阅第 7 章。

一旦完成了该活动，你就可以回到上次的地方继续工作。确保你的“挂起（Suspended）”部分包含你上次工作的内容，如图 6-23 所示，这在万一你忘记时非常有用。选择挂起的工作并按下“恢复（Resume）”。

这将快速撤出更改，恢复你打开的文件，打开工具并恢复你的断点。

请注意，即使你觉得已经准备好恢复工作，但采取了许多人的做法，只是回到桌前开始做其他事情，也可以选择挂起的工作并将其与 Server 2012 中的当前工作合并，以支持在架上合并（得益于 Team Foundation Server 的更改和所有改进）。

当任务完成后，你可以直接在“我的工作”页面上点击“提交（Check In）”。它将带你进入“待处理更改（Pending Changes）”页面以审查你的更改、输入注释并提交。注意，如果你在解析工作项时关联了该工作项，那么当你执行提交时，该工作项将自动移动到下一个状态，在你的情况下是“已完成（Done）”。

工作项会在任务板中更新，并在更改集与你与更改关联的工作项之间创建一个链接。这一切通过使用“我的页面（My Page）”简单轻松地完成。

注意：“我的工作”页面非常实用，你可能会发现自己经常去那里。从 Visual Studio 任何地方快速进入“我的工作”页面的快捷键是 `Ctrl+0,M`。欲查看 Team Explorer 快捷键的完整列表，请访问 http://aka.ms/TEKeys。

# 第 6 章 使用 Team Foundation 版本控制

![](img/aaf6096fc6b4485534c737801bdbc4fd_169_0.png)

**6-24:** 在 Eclipse 中工作

## 备用安装方法

在 Eclipse 中安装 Team Explorer Everywhere 的推荐方法是通过 Eclipse 市场或或之前提供的 Eclipse 更新站点。然而，你也可以从微软下载中心或 MSDN 下载 Team Explorer Everywhere 的更新站点存档。

之前的安装方法将引导你进入 Team Explorer Everywhere 的最新发布版本。如果你想运行 Team Explorer Everywhere 的最新预发布版本，可以使用以下 Eclipse 更新站点：http://dl.microsoft.com/eclipse/tfs/preview。

继续完成向导的其余步骤并接受许可条款。一旦点击“完成”（Finish），Team Foundation Server 插件将会被安装，系统会提示你重启 Eclipse（你应该这样做）。

这会在 Eclipse 中添加 Team Explorer 视图以及一个 Team Foundation 探索视图，你可以使用它连接并处理 Team Foundation 资源。

## 在 Team Foundation Server 中共享 Eclipse 项目

现在你已经安装了 Team Foundation Server 集成，下一步你想做的是将你的 Eclipse 项目添加到 Team Foundation Server 中，以便与团队的其他成员共享。此操作类似于 Visual Studio 中的“将解决方案添加到源代码控制”功能。

然而，在 Eclipse 中，版本控制提供程序通过在 Eclipse 中右键点击并选择“共享项目”（Share Project）来提供此功能。这将显示一个版本控制仓库类型列表。如图 6-25 所示，Team Foundation Server 地址将出现在列表中。

![](img/aaf6096fc6b4485534c737801bdbc4fd_170_0.png)

图 6-25：显示为仓库类型的 Team Foundation Server

选择 Team Foundation Server。在下一个屏幕上，系统将提示你选择你的 Team Foundation Server。如果你还没有设置过现有的 Team Foundation Server 连接，系统将提示你输入 Team Foundation Server 实例的名称或完全限定 URL。

请注意，如果你的 Team Foundation Server 实例未安装在 `http://server_name:8080/tfs`，那么你可能需要使用完全限定 URL（即 `https://fabrikam.tfpreview.com`）而不是主机名与开发团队共享你的 Team Foundation Server 地址，以确保使用正确的连接设置。

一旦选了服务器，系统将要求你选择要共享 Eclipse 项目的项目集和团队项目，如图 6-26 所示。

然后，在向导的后续页面中，系统将提示你选择项目使用哪个 Team Foundation Server 工作空间。请注意，你可能希望在机器上使用多个 Team Foundation Server 工作空间，以保持你的 Eclipse 工作空间分开，或者将你的 Eclipse 和 Visual Studio 工作空间分开。然而，单个工作空间可以被同一机器上的 Visual Studio 和 Eclipse 安全地共享。事实上，作为 2012 发布版本本地工作空间范围的一部分，人们投入了大量工作来确保 Eclipse 插件和 Visual Studio 中的 Team Explorer 能够通过服务器连接和工作空间设置进行通信并共享数据。

如果你从未连接过 Team Foundation 项目集，系统将为你创建一个新的私有工作空间。选择你需要的工作空间（或添加一个新的并选择它）并点击“下一步”。

![](img/aaf6096fc6b4485534c737801bdbc4fd_171_0.png)

**图 6-26：**关于 Team Foundation Server 的详情

你将看到如图 6-27 所示的页面，该页面询问你将项目放置在版本控制仓库中的位置。如果你认为未来想使用 Team Foundation Server 的分支功能，请将项目放入 `Main` 文件夹中。

共享向导的最后一页将确认共享详情，允许你在点击“完成”之前检查详情。请注意，插件将自动创建任何所需的工作文件夹映射。

一旦共享完成，包管理器（Package Explorer）中的项目资源将被检测到，表明它们处于 Team Foundation 版本控制之下；但在你勾选要共享的文件之前，它们在服务器上不可供他人使用。

你可以通过右键点击项目并选择“签入”（Check In）来检查你正在共享的文件。（注意：此片段中引用了图 6-27 但未显示）。

## 在 Team Foundation Server 中导入 Eclipse 项目

如果你从未连接过 Team Foundation 项目集，系统将为你创建一个新的私有工作空间。选择你需要的工作空间（或添加一个新的并选择它）并点击“下一步”。

![](img/aaf6096fc6b4485534c737801bdbc4fd_171_0.png)

**图 6-26：**关于 Team Foundation Server 的详情

跨平台 Windows 客户端在大多数版本中都广泛兼容支持的支持相同的命令和参数，从而允许使用命令行接口重用脚本并进行集成。然而，它们源于不同的命令行接口实现。Windows 版本使用 `.NET` 编写，而跨平台实现使用 `Java` 编写。因此，它们之间存在一些细微差异，但大多数功能是完全相同的。

## 获取帮助

如前所述，您可以使用 `tf help` 命令来查看可用命令列表。要查看单个命令的语法，请输入 `help [command]`，其中 `command` 是您想要查看详细信息的命令名称。

> 注意：访问在线 MSDN 文档 http://aka.ms/tfclc 获取更多关于使用 `tf` 命令行的相关信息。

## 使用命令行

以下示例展示了使用命令行的一种非常基础的方法，以演示其工作原理。假设您从未连接到 Team Foundation Server，在开始之前，第一件事是在您的本地计算机上创建一个工作空间：

```
tf workspace -new -collection:http://servername:8080/tfs/defaultCollection -login:users$DOMAIN Password MyWorkspace
```

在此示例中，`MyWorkspace` 是您的工作空间名称，`http://servername:8080/tfs/defaultCollection` 是您的团队项目集合的 URL。您在命令中传递了凭据。如果您在 Windows 上没有提供任何凭据，或者您在非 Windows 平台上使用 Kerberos，您将使用已验证用户的凭据进行连接。如果您尝试从非 Windows 系统连接到 `tfpreview.com` 托管 TFS 实例，则您需要在用户配置文件中启用基本身份验证并使用这些凭据。一旦创建了工作空间，除非另有说明，否则凭据将缓存在用户的配置文件中。

接下来，您创建一个工作文件夹：

```
tf work -map -workspace:MyWorkspace $/TeamProject/Main/Path.
```

这里是在 `MyWorkspace` 中在服务器路径 `$/TeamProject/Main/Path` 和当前目录 (`.`) 之间创建一个工作文件夹。

现在，您想要下载代码：

```
tf get
```

然后您可以编辑文件（使用您选择的任何文本编辑器——在本例中是 `vi`，但在 Windows 上您可能会选择 `Notepad`）。请注意，由于在 Team Foundation Server 2012 中默认使用本地工作空间（Local Workspaces），您不需要显式地检出（check out）文件：

```
vi myfile.txt
```

## Team Foundation 版本控制 Power Tools 和第三方实用 | 139

然后，您想要检查待处理更改的状态，以确保您想要进行的编辑列表是正确的：

```
tf status
```

`status` 命令将执行全磁盘扫描并自动挂起（pend）您所做的任何更改。如果您创建或删除了任何文件，这些文件将显示为候选文件，允许您使用 `tf add` 或 `tf delete` 命令显式地添加或删除它们。接下来，您可以检查 `MyWorkspace` 中的更改：

```
tf checkin -comment="Making changes from the command line"
```

您的更改现在已经签入，并创建了一个更改集（changeset）。您可以通过执行 `Get` 操作来下载刚刚通过命令行提交的更改，从而从任何其他版本控制客户端中查看这些更改。

## TEAM FOUNDATION VERSION CONTROL POWER TOOLS AND THIRD-PARTYILITIES

Team Foundation Server 提供的功能非常丰富，通过基于 `.NET` 的 Team Foundation Server API 和第三方工具创建的扩展可以以更易于使用的方式暴露功能。要列举所有工具都来不完，以下章节详细介绍了每个 Team Foundation Server 用户都应该拥有的某些极具价值的工具。

## Microsoft Studio Team Foundation Server Power Tools

Team Foundation Server Power Tools 由微软的 Team Foundation Server 团队自行创建，提供了许多优秀功能，这些功能在发布时尚未准备好进入最终版本，或者没有考虑到大多数用户。最初在 Power Tools 中交付的许多功能（如 Annotate、folder diff、rollback 等）首先在 Power Tools 中出现，稍后才作为完整产品推出。

> 注意：可以从 http://aka.ms/ftpt 免费获取 Power Tools。

主要的 Power Tools 将扩展安装到 Visual Studio 中，并在 Windows 上提供一个新的命令行客户端。Power Tools 包含以下控制领域特别受关注的内容：

- Windows Shell 扩展——这是一个类似于 TortoiseSVN 的 Windows 资源管理器和常用文件对话框扩展，允许您在不运行 Visual Studio 或命令行的情况下，从 Windows 执行基本的源控制操作。

- 命令行（tf 工具)—`tf help` 显示可用命令列表，包括 `tf online`，它将您的本地文件夹与服务器认为的您工作空间中的内容进行比较。它还可以帮助您在离线状态下使用服务器工作空间（Server Workspace）并在 Visual Studio 之外更改文件挂起添加、编辑、删除等。

另一个实用的命令是 `tftft scorch`，它将确保您的本地工作文件夹与应拥有的服务器完全匹配——任何额外文件将被删除，而任何修改的文件将被重新下载并替换。

## Team Foundation Server MSSCCI

MSSCCI 提供程序允许 Team Foundation Server 版本控制集成到支持旧版 MSSCCI API 的产品中，该 API 最初为 VSS 设计，但后来被许多 IDE 开发者采用。MSSCCI 提供程序由微软负责 Team Foundation Server 的团队开发。

> 注意：可以从 http://aka.ms/tftgr 免费下载 MSSCCI 提供程序。

由于该提供程序是在原始开发者可能创建 API 很久之后才创建的，而且它是针对一个与 IDE 开发者测试过的系统完全不同的版本控制系统，效果因人而异——许多人在各种环境中使用它。然而，MSSCCI 的下载页面显示针对以下环境进行了测试：

- Visual Studio .NET 2003

- Visual C++ 6 SP6

- Visual Basic 6 SP6

- Visual FoxPro 9 SP2

- Microsoft Access 2007

- SQL Server Management Studio

- Enterprise Architect 7.5

- PowerBuilder 11.5

- Microsoft embedded VC++ 4.0

## 配置版本控制
