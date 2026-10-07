
```xml
<ItemGroup>
  <Reference Include="System" />
  <Reference Include="System.Data" />
  <Reference Include="System.Deployment" />
  <Reference Include="System.Xml" />
  <Reference Include="System.Core" />
  <Reference Include="System.Linq" />
  <Reference Include="System.Data.DataSetExtensions" />
</ItemGroup>
<ItemGroup>
  <Import Include="Microsoft.VisualBasic" />
  <Import Include="System" />
</ItemGroup>
<ItemGroup>
  <Compile Include="Module.vb" />
  <Compile Include="Project.AssemblyInfo.vb" />
  <Compile Include="Project.Application.Designer.vb" />
    <AutoGen>True</AutoGen>
    <DependentUpon>Application.myapp</DependentUpon>
  </Compile>
  <Compile Include="Project.Resources.Designer.vb" />
    <AutoGen>True</AutoGen>
    <DesignTime>True</DesignTime>
    <DependentUpon>Resources.resx</DependentUpon>
  </Compile>
  <Compile Include="Project.Settings.Designer.vb" />
    <AutoGen>True</AutoGen>
    <DependentUpon>Settings.settings</DependentUpon>
    <DesignTimeSharedInput>True</DesignTimeSharedInput>
  </Compile>
</ItemGroup>
<ItemGroup>
  <EmbeddedResource Include="Project.Resources.resx" />
    <Generator>VbMyResourcesFileGenerator</Generator>
    <LastOutput>Resources.Designer.vb</LastOutput>
    <CustomToolNamespace>My.Resources</CustomToolNamespace>
    <Subtype>Designer</Subtype>
  </EmbeddedResource>
</ItemGroup>
<ItemGroup>
  <None Include="Project.Application.myapp" />
    <Generator>ApplicationCodeGenerator</Generator>
    <LastOutput>Application.Designer.vb</LastOutput>
  </None>
  <None Include="Project.Settings.settings" />
    <Generator>SettingsSingleFileGenerator</Generator>
    <CustomToolNamespace>My</CustomToolNamespace>
    <LastOutput>Settings.Designer.vb</LastOutput>
  </None>
</ItemGroup>
<ItemGroup>
  <Import Project="$(MSBuildBuildPath)\Microsoft.VisualBasic.targets" />
  <!-- 若要修改构建，请将您的任务添加到下面的某个 target 中并取消注释 -->
   存在其他扩展点，请参见 Microsoft.Common.targets。
  <Target Name="BeforeBuild" />
</ItemGroup>
```

```xml
<Target Name="AfterBuild">
</Target>
</Project>
```

## Windows Foundation

虽然下一章重点关注其他工具，但值得提到的是 Windows Foundation `WF`。`WF` 是微软提供的一个编程框架，用于自动化构建。在构建自动化的早期，`WF` 是使用 `.NET` 实现的，并且能够处理许多版本控制系统，包括 Team Foundation Server。由于其关注 `.NET` 开发者，它可以使用 `NAnt` 或 `MSBuild` 脚本构建 `.NET` 项目并通知开发者。构建输出（包括单元测试结果、代码覆盖报告、API 文档等）可以通过 Web 访问。

虽然任何构建过程都可以由 CruiseControl 执行，但它通常用于 Ant 构建和 Java 项目。正如提到的，Team Foundation Server 作为版本控制库受到 CruiseControl 支持。然而，构建的数据和通知存储在 CruiseControl 系统中。

## CruiseControl

CruiseControl `https://cruisecontrol.sourceforge.net/` 是另一个使用 Java 实现的开源构建服务器。因此，它运行在包括 Windows 和 Linux 在许多平台上。CruiseControl 的核心是一个定期检查配置系统的循环，如果检测到更改，它将触发新的构建。一旦构建完成，就会发送有关状态的通知。

CruiseControl 的配置通过 `config.xml` 文件进行。由于其作为一个活跃且充满活力的源码项目已久，许多扩展被贡献给了 CruiseControl。许多不同的版本控制系统（包括 Team Foundation Server）都可以被 CruiseControl 查询，以及许多不同的通知方案（包括电子邮件、Web 控制台、即时消息甚至是 Windows 托盘系统）。构建输出（包括单元测试结果、代码覆盖报告、API 文档等）可以通过 Web 访问。

## CruiseControl.NET

CruiseControl.NET `https://ccnet.thoughtworks.com/` 是一个开源构建服务器，但正如其名称所示，它是使用 `.NET` 实现的。它基于基于原始版本的 CruiseControl，并且同样由相同的 ThoughtWorks 咨询公司开发。

CruiseControl.NET 的配置通常通过编辑名为 `ccnet.config` 的 XML 文件进行。它也能够处理许多版本控制系统，包括 Team Foundation Server。

## Hudson / Jenkins

Hudson 是另一个使用 Java 实现的开源构建服务器。Hudson 是该服务器的原始名称，但在主要社区维护者之间发生了一场激烈的歧后后

该项目以及 Hudson 商标的持有者——创建了一个该项目的社区分支，并名为 Jenkins。近年来，它们已成为 CruiseControl 的流行替代方案，这主要是是因为它提供了一个易于使用的基于 Web 的界面来配置新构建，而不是手动编辑 XML 文件。

虽然 Hudson / Jenkins 能够构建许多项目（Ant 甚至 `MSBuild`），但它在处理构建以及跟踪 Maven 项目构建之间的依赖关系方面具有一些特殊功能，这正是它在本书中值得被特别提出的原因。

Hudson 能够与许多版本控制工具配合，包括 Team Foundation Server。然而，与所有外部构建系统一样，这些构建的数据存储在 Hudson 系统内部，尽管它确实拥有一些实用的构建能力。

## Team Foundation Server

构建自动化对于提高软件开发质量至关重要，因此自 2005 年最初发布以来，Team Foundation Server 就包含了构建自动化功能。在内部，该功能被称为“Big Build”，但人们将 Team Foundation Server 的构建自动化组件称为 Team Build 或 Team Foundation Server。

`MSBuild` 首次于 2005 年随 Visual Studio 出发，而 2005 年 Team Foundation Build 的原始形态是紧密围绕 `MSBuild` 构建的。构建通过位于 Team Foundation Server 版本控制中 `$/Project/TeamTypes/TypeName` 文件夹下的 MSBuild 脚本 `TFSBuild.proj` 定义。

当触发构建时，`TFSBuild.proj` 会下载到服务器并执行。结果会被发布回服务器，更重要的是，构建指标会馈送到强大的 Team Foundation Server 数据仓库中。构建会自动与 Team Foundation Server 的项目跟踪进行关联。

然而，在 2005 年的原始版本中，Team Foundation Build 的功能非常有限。没有用于触发构建的构建进程——它们必须手动触发，或者用户必须配置其作业来定期触发构建，或者监听提交并触发持续构建。

幸运的是，2008 年的 Team Foundation Server 版本在构建能力上取得了巨大的改进。事实上，Team Foundation Build 可能是从 Team Foundation Server 2005 升级的最主要原因。在 2008 年，你拥有了通过多种触发器之一来触发构建的能力，包括计划构建和持续集成构建。

2010 年的发布版对 Team Foundation Server 的构建有了更多的改进。其中最大的一点是从完全基于 `MSBuild` 的解决方案转变为使用 `WF` 作为编排引擎的解决方案。这具有几个重要优势，包括能够轻松在 Visual Studio 用户界面中显示有关构建的常用构建配置属性，以及将构建分布到多个服务器（或构建代理）的能力。

虽然你在 Team Foundation Server 的版本控制和工作跟踪功能中获得了非常丰富的集成，但重要的是，Team Foundation Server 的构建自动化功能只能与 Team Foundation Server 版本控制配合使用。虽然对于本书的读者来说这不是一个问题，但在计划迁移到 Team Foundation Server 时这是一个重要的考虑因素。只有在源代码进入 Team Foundation Server 后，开启其自动化功能才有意义。

## 采用构建自动化

希望你现在已经说服构建自动化是你想要做的事情。采用构建自动化作为一种实践如何？

第一步是确保你有一个可以运行的完整构建并打包待部署产品的命令。如果使用 Visual Studio，这很容易，大多数 Visual Studio 项目类型都可以使用 `MSBuild` 轻松构建。但如果你有用 Java 或软件语言开发的组件，那么你需要做一些工作，使用最合适的脚本语言（如 Ant 或 Maven）来组合你的构建脚本。

接下来，你应该确保每个人都知道如何构建该项目，并且所有开发者都能从他们的机器上运行它。

一旦构建变得简单，下一步就是定期运行构建，以确保你始终有一个整洁的基础。如果你的构建包含资源，请努力实现持续集成风格的构建，并确保你有一种快速（且理想的）通知方法，在构建损坏时告知开发者。简单的电子邮件通知足够了且至少可以这样做，但如果你愿意，也可以更具创意。

## BRIAN THE BUILD BUNNY

> 让团队关注构建状态的一些方法比其他方法更具想象力。鼓励团队关注当前构建状态的一种流行方法是创建创意且引人注目的构建状态机制。虽然墙显示器和指示灯是向……传达信息的好方法……

本章内容经过了刻意的泛化处理，因为无论你选择何种技术或平台，构建自动化都是至关重要的。然而，Team Foundation Server（TFS）在构建自动化方面具有一些创新特性。

第 17 节详细描述了如何在 Team Foundation Server 内部创建自动化构建。它描述了 Team Foundation Server 提供的所有功能，并重点介绍了 2011 版本中的新特性。你将学习到 Team Foundation Build 系统的架构以及如何处理构建。最后，将详细检查构建过程，描述其功能和工作原理。

# 17

## 使用 Team Foundation Build

本章包含哪些内容？

- 了解由 Team Foundation Server 提供的构建自动化功能
- 理解 Team Foundation 构建架构
- 安装构建计数器（build controller）和构建代理（build agent）
- 与构建进行交互操作
- 理解构建过程
- 编辑构建过程参数
- 使用 Team Foundation Server 同时构建 .NET 和 Java 项目

本章介绍了 Team Foundation Server 的构建自动化能力、核心概念以及如何安装构建服务器功能。你将学习如何根据标准的构建过程模板创建你自己的构建，以及如何使用这些模板来管理它们。

> 注意：有关自定义标准构建过程的信息，请参阅第 18 节。

### TEAM FOUNDATION BUILD 介绍

Team Foundation Server 的构建自动化能力自 Team Foundation Server 2005 初始发布以来经历了最显著的变化。最初，构建功能扩展了 `MSBuild`，以实现与 Team Foundation 版本控制和项目跟踪集成的基础级构建自动化。

在 2008 版本中，构建系统作为一套完全的就级构建系统，拥有了自己的独立地位。该版本在 Team Foundation Server 中引入了新的一等公民概念，例如构建定义（build definition）和构建代理（build agent），并且内置了灵活的触发器功能。然而，构建过程仍然依赖于 `MSBuild`。

2010 版本在构建自动化领域引入了更多功能。最大的变化是引入了 Windows Workflow 4.0 作为构建编排机制。解决方案的实际编译仍然由专门的构建语言处理（例如用于 .NET 解决方案的 `MSBuild`，以及用于基于 Java 项目的 Ant 或 Maven）。然而，过程的其他部分由使用 Windows Workflow 4.0 的构建过程模板管理。

> 注意：有关这些构建语言的更多信息，请参阅第 16 节。

2010 版本中的其他显著特性还包括门禁检查（gated check-in）支持、私有构建、构建通知、通用构建自定义属性、与 Symbol 和 Source 服务器的集成、增强的构建删除能力以及名为构建计数器（build controller）的新概念。

对于运行本地部署 Team Foundation Server 的客户，Team Foundation Build 的 2012 版本是对现有功能的精炼。其中一个显著特性是能够通过配置同时构建多个检查项，来提高门禁检查的效率。

对于 2012 版本，开发团队投入了大量精力重写构建计数器和代理与 Team Foundation Server 通信的方式。在之前的版本中，是 Team Foundation Server 主动连接构建服务器以建立连接并启动构建。当构建服务器位于防火墙后或其他路由时，这就成了一个问题。

随着 Team Foundation Service 的引入，产品需要允许客户在使用托管服务的同时运行自己的构建服务器。这使得构建服务器通信转向基于轮询（polling-based）的消息架构。本质上，Team Foundation Server 为每个构建维护一个消息队列，构建通过持续轮询来保持同步。

### TEAM FOUNDATION BUILD 架构

图 17-1 显示了 Team Foundation Build 架构中关键的几个逻辑组件。

构建由构建定义（build definition）定义，它详细描述了构建，包括应该构建什么、如何构建以及何时构建。关于构建定义以及如何创建和管理定义的更多信息将在本章后部分提供。

![](img/aaf6096fc6b4485534c737801bdbc4fd_428_0.png)

构建定义属于 Team Foundation 中的一个团队项目。当应用程序确定需要执行该构建定义的构建时，它会向*构建计数器*（build controller）队列发送构建请求消息。

随后，构建计数器下载为构建定义的基于 Windows Workflow 的构建过程模板并执行它。默认情况下，这将导致构建在计数器代理池中的下一个可用*构建代理*（build agent）上运行。

构建代理是执行构建的实际机器。每个构建代理都有一个构建计数器作为父节点，但一个计数器可以拥有多个用于构建的构建代理。每个构建计数器必须分配给单个项目集。

构建代理执行构建定义过程模板中描述的构建主体部分——包括使用 `MSBuild` 执行实际的编译和测试步骤。

一旦构建代理成功执行构建，默认构建过程模板会将构建结果（如网站、可执行文件、程序集等）归档到基于 Windows 的文件共享中作为输出位置（drop location）。它还会将任何符号发布到*符号服务器*（symbol server）（如果已配置）。

所有关于构建的信息（例如构建号、状态以及特定构建的进度）都称为*构建详情*（build details）。请注意，构建计数器和构建代理进程由*构建服务*托管。构建计数器和构建代理可以运行在同一台机器上，但在生产配置中，建议不要与应用程序层位于同一台机器。

### 设置 TEAM FOUNDATION BUILD 服务

本节详细介绍了如何设置构建服务以启用构建自动化。这对于管理 Foundation Server 实例的用户非常有用。如果你已经为你的项目集准备了构建计数器，你可能希望跳过此节，直接进入“与构建交互”部分以了解如何创建和管理构建定义。
