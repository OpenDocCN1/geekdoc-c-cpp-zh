

显然，这大大节省了时间，因为你无需在 Riak 网站上搜索 CorrugatedIron 或其任何依赖项的下载。一切已就绪，你可以专注于开发。当需要将 CorrugatedIron 升级到下一版本时，你也可以使用 NuGet 自动更新整个解决方案中所有依赖于它的包。

## 生成包

NuGet 还允许你创建包。你可能希望创建包以发布到官方 NuGet 包库供其他开发人员使用，或者你可能希望托管自己的包源以管理第一方依赖项。图 2-19 展示了 NuGet 包资源管理器，它可用于创建你自己的包。在此包中，我将 CorrugatedIron 配置为一个依赖项，因此它还将隐式依赖 Newtonsoft.Json 和 protobuf-net。我添加了一个专门针对 .NET Framework 4.5.1 的库程序集，以及一个将在引用程序集中创建于 My folder/NewFile.txt 下的文本文件。甚至还有一个 Windows PowerShell 脚本被指示在安装期间运行。得益于 Windows PowerShell 的灵活性，这实际上几乎可以用于做任何事情。

![](img/65c1bad7a6b3cffae8cbb79664f0708b_97_0.png)

图 2-19 NuGet 包资源管理器使得构建你自己的包变得非常容易。

每个包都有一个 XML 文件，其中详细说明了安装窗口中显示的元数据。清单 2-21 展示了该文件的部分语法。

### 清单 2-21 包 XML 定义，包括元数据。

单击此处查看代码图像

```
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
  <metadata>
    <id>MyTestPackage</id>
    <version>1.0.0</version>
    <authors>Gary McLean Hall</authors>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>My package description.</description>
    <dependencies>
        <dependency id="CorrugatedIron" version="1.0.1" />
    </dependencies>
  </metadata>
</package>
```

NuGet 在提高生产力和组织性方面是如此有益，以至于如果没有针对某个特定库的包，回到手动管理第三方依赖项会令人痛苦。事实上，NuGet 不仅适用于第三方依赖项。当解决方案变得足够大时，建议将解决方案按层切分为多个部分。然后可以使用 NuGet 将每一层的程序集打包，供上层使用。这使解决方案保持较小且易于处理。

## Chocolatey

描述 Chocolatey 的最佳方式是说它是一个包管理工具，就像 NuGet 一样，但它的包是应用程序和工具，而不是程序集。有一定 Linux 知识的开发人员会发现 Chocolatey 就像 apt-get——Debian 和 Ubuntu 的包管理器。同样，包管理的许多好处在这里也适用：简化的安装、依赖管理和易用性。

以下 Windows PowerShell 脚本可用于下载和安装 Chocolatey。

单击此处查看代码图像

```
@powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%systemdrive%\chocolatey\bin
```

安装 Chocolatey 后，你可以使用命令行搜索和安装各种应用程序和工具。安装过程应该已经更新了命令行路径，使其包含 chocolatey.exe 应用程序。与 Git 非常相似，Chocolatey 有诸如 list 和 install 之类的子命令，但这些子命令也有可用作快捷方式的同义词：分别为 clist 和 cinst。清单 2-22 展示了一个示例 Chocolatey 会话，该会话查找 FTP 客户端 FileZilla 的包名称，然后安装它。

### 清单 2-22 首先搜索包含所需应用程序的包，然后安装它。

单击此处查看代码图像

```
C:\dev> clist filezilla
ferventcoder.chocolatey.utilities 1.0.20130622
filezilla 3.7.1
filezilla.commandline 3.7.1
filezilla.server 0.9.41.20120523
jivkok.tools 1.1.0.2
kareemsultan.developer.toolkit 1.4
UAdevelopers.utils 1.9
C:\dev> cinst filezilla
Chocolatey (v0.9.8.20) is installing filezilla and
dependencies. By installing you accept
the license for filezilla and each dependency you are
installing.
...
  This finished installing 'filezilla' and dependencies - if
errors not shown in console,
none detected. Check log for errors if unsure.
```

只要 Chocolatey 没有报告错误，所请求的包现在就安装好了。请注意，Chocolatey 应该已经修改了你的系统 PATH，以便可以从命令行执行任何新的二进制文件，但它并不总是如此。通过 Chocolatey 可以获得大量包，它所提供的便利性是使用它的一个令人信服的理由。

## 分层

到目前为止，本章主要从程序集级别讨论依赖管理。这是组织应用程序的自然第一步，因为所有类和接口都包含在程序集中，而它们如何相互引用是一个常见问题。如果组织得当，你的程序集将只包含与单一组相关功能相关的类和接口。然而，从整体来看，你如何确保程序集的分组也被正确组织？

两个或更多相互关联的程序集组成正在开发的软件系统的组件。这些组件以同样良好定义和结构化的方式交互，同样重要（如果不是更重要的话）。如图 2-20 所示，组件不是部署的物理工件（如程序集动态链接库 (DLL)），而是共享相似主题的程序集的逻辑分组。

![](img/65c1bad7a6b3cffae8cbb79664f0708b_99_0.png)

图 2-20 通过将相关程序集分组在一起，你可以定义逻辑组件。

图中包含三个程序集：Views、Controllers 和 ViewModels。每个程序集包含两个服务不同目的且可能需要不同依赖项的类。尽管类和程序集是 .NET Framework 提供的构造，但将一切分组在一起的用户界面包是逻辑上的。这三个程序集可能位于解决方案中一个名为 UserInterfaces 的文件夹中，但没有什么能阻止你添加一个不属于该层的另一个项目来污染这一层。除了你自己的谨慎之外，没有什么能阻止。

在依赖管理中，组件与较低层次的其他编程构造并无不同。与方法、类和程序集一样，你可以将层视为本章前面展示的依赖图中的另一个节点。因此，同样的规则适用：保持有向图无环，并确保单一职责。

*分层*是一种架构模式，它鼓励你将软件组件视为相互构建以形成完整应用程序的功能水平层。组件一层一层地叠放，依赖方向必须始终向下。也就是说，应用程序的底层没有依赖²，每一层向上都依赖于其正下方的层。栈顶是用户界面。如果应用程序是服务层，则顶层将是客户端用来与系统交互的 API。

> ² 这并不完全正确：很可能存在一些依赖，但因为它是底层，没有其他第一方代码可依赖，所以这些依赖很可能是第三方的、基础架构性的依赖。

## 常见模式

对于任何项目，都有几种常见的分层模式可供选择。这里介绍的每一种都应作为指南，根据你所在环境的具体要求和限制进行调整。各种分层模式之间的区别因素只是所使用的层*数量*。本节首先介绍一个仅由两层组成的简单架构，然后在中间插入第三层，最后推广到任意数量的层。

所需层数与解决方案的复杂性相关；解决方案的复杂性又与问题的复杂性相关。因此，问题越复杂，你可能越倾向于投资于多层架构。在这种情况下，复杂性由许多因素衡量：项目的时间限制、其需要的长期性、需求可能变化的频率，以及开发团队对模式和实践的重视程度，仅举几例。

因为本书是关于适应需求变化，我提倡*先做最简单可行的事情*，并且*仅在需要时*才重构为更复杂的东西。这对项目有积极影响。首先，它允许你尽快交付一些东西。在软件开发中，应尽早并频繁地寻求反馈。如果客户对完美的想法与开发团队对完美的想法不同，试图交付完美的解决方案是没有意义的。开发多层解决方案比简单的两层解决方案花费更长时间，从而延迟了那至关重要的反馈循环。

