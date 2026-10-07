
# 第 16 章构建自动化概述

## Ant 与 Make

Ant 与 Make 有许多相似之处。构建文件由一个包含多个目标的项目组成。每个目标定义了系列要执行的任务和一组依赖项。Ant 是声明式的自动依赖管理。例如，一个简单的 Java Hello World 示例可以使用以下 `build.xml` 来编译它 Ant：

```xml
<?xml version="1.0" encoding="utf-8"?>
<project name="helloworld" basdir="." default="package">

  <target name="compile">
		<mkdir dir="${basedir}/bin" />
```

```xml
<javac srcdir="${basedir}/src
  destdir="${basedir}/bin"
  debug="on"
  includeRuntime="false"/>
</target>

<target name="jar">
  <jar destfile="${basedir}/helloworld.jar"
  basedir="${basedir}/bin" />
</target>

<target name="clean">
  <delete file="helloworld.jar" />
  <delete dir="${basedir}/bin" />
</target>

<target name="package" depends="compile,jar">
  <!-- 标准 XML 格式的注释 -->
</target>

</project>
```

Ant 中的任务是通过实现特定接口的编译 Java 代码来实现的。除了 Ant 附带的大量任务外，开源社区还提供了许多可用任务。Java 相关工具的制造商会提供 Ant 任务，以便在 Ant 中方便地与他们的工具协作。

Ant 脚本可能会变得复杂，而且 Ant 脚本中使用的 XML 非常冗长；脚本可能会迅速变得巨大且复杂。因此，对于复杂的系统，可以将 `build.xml` 文件拆分为更具模块化的文件。

Ant 在 Java 社区中非常常见，以至于大多数现代 IDE 都自带了一个版本的 Ant，允许在开发环境内部执行构建，并提供帮助编写 Ant 的工具。

## Apache Maven

Maven 是一个用 Java 编写的开源项目管理和构建自动化工具。Maven 的核心概念是项目对象模型 `pom.xml`，它描述了正在构建的项目。Maven 在功能上类似于 Make，并派生自 Ant，但它具有一些新颖的概念，定义了一个独特的新类构建工具，使得 Maven 在书中书中讨论价值。

Make 和 Ant 允许编写完全自由的脚本，并且你的源文件可以位于任何地方。Maven 则采取了一个不合理的假设，即你正在进行构建，并对构建过程中文件应该所在的位置使用了约约定。它将“约约定优于配置”`Convention over Configuration` 的软件设计范式应用于构建。这种范式的主要优势是它能帮助你熟悉 Maven 项目，因为它们都遵循某些模式来完成构建（缺点是失去了灵活性）。

Maven 与受 Make 启发的构建工具之间的另一个区别是，它将将依赖管理提升到了新的高度。Make 和 Ant 处理被构建项目内部的依赖，而 Maven 可以管理对外部库的依赖（这在许多 Java 项目中特别常见）。如果你的代码依赖于某个版本的库，那么 Maven 将从项目仓库下载该库并存储在本地，供构建使用。这有助于构建的可移植性，因为它意味着你只需要安装 Java 和 Maven。构建过程应该处理好运行构建所需的所有内容。

> 有关 Maven 的更多信息，请请访问 `http://maven.apache.org/`。

## NAnt

NAnt `http://nant.sourceforge.net/` 的灵感来自 Apache Ant，但用 .NET 编写并用于构建 .NET 项目。与 Ant 类似，它也是一个开源项目，最初发布于 2001 年。有趣的是，根据 NAnt 的 FAQ，Nant 的名字来源于该工具是“不是 Ant”`Not Ant`，从其缩写中提取出 Ant，意思是 Nant 是“不是另一个工具”`Not Another Tool`。但实际上，Nant 是执行构建自动化的新方法，在早期的 .NET 1.0 和 1.1 项目中非常有用。

语法上与 Ant 非常相似，NAnt 文件以 `.build` 后缀存储。每个文件由一个包含许多任务的项目组成。每个 `target` 目标定义了若干要执行的任务和一组依赖关系。它有用于执行 .NET 活动的任务，例如使用 `<exec />` 来执行 C# 命令行编译器工具。

NAnt 文件的主要问题是 Visual Studio 并不理解这种编写方式，而且对 Visual Studio 解决方案文件 `.sln` 和项目的更改也必须在 NAnt 文件中进行；否则自动化构建脚本将无法识别这些依赖关系。要使用 `.sln` 文件或 `.vbproj` / `.csproj` 文件执行构建，你必须在构建服务器上安装 Visual Studio，并使用 `deven` 任务从命令行驱动 Visual Studio，而大多数人都会避免这样做。

## MSBuild

MSBuild 是 Visual Studio 自 2005 版本以来一直使用的构建系统。然而，MSBuild 平台是 .NET Framework 的一部分安装的，你可以从命令行使用 `MSBuild.exe` 构建项目，而无需使用 Visual Studio IDE。

Visual Studio 保持 MSBuild 文件的更新。事实上，对于 Visual Studio 开发者来说广为人知的 `.csproj` 和 `.vbproj` 文件简单来说就是 MSBuild 脚本。

MSBuild 受到如 Ant 或 NAnt 等基于 XML 的构建自动化系统的深度影响，同时也受到其前身 Make 影响。MSBuild 文件通常以 `.proj` 扩展结尾（例如 `TFSBuild.proj`, `MyProject.vbproj`, `MyCSharpProject.csproj`）。MSBuild 文件遵循一种新模式，并在项目内部包含许多属性和 `target`。每个 `target` 包含许多任务。

以下是一个 MSBuild 脚本的示例，你可以通过 Visual Studio 命令提示符使用 `msbuild helloworld.proj` 命令来执行它：

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003"
  DefaultTargets="SayHello">

  <PropertyGroup>
    <!-- 定义要问候的名字 -->
    <Name>World</Name>
  </PropertyGroup>

  <Target Name="SayHello">
    <Message Text="Hello $(Name)!" />
  </Target>

</Project>
```

然而，MSBuild 也有一些显著的例外。除了 `PropertyGroup` 中简单的属性（可以被视为键值对），`Items` 是一个值的列表，这在编程术语中可以类似于数组或枚举。一个 `Item` 还关联有相关的元数据。当你创建一个 `Item` 时，它实际上是一个实现了 `ITask` 接口的 .NET 对象。每个 `Item` 有一组预定义的元数据，但你也可以作为 `Item` 的子节点添加自己的属性。

MSBuild 使用与 Ant 或 Nano 等工具的另一个区别在于，Visual Studio 和 Team Foundation 使用许多目标 用于构建过程。这些目标存储在带有 `targets` 扩展的 MSBuild 脚本中。它们通常存储在 `%ProgramFiles%/MSBuild` 或个人机器的 .NET Framework 中。Visual Studio 创建的实际脚本通常连接相关的 `targets` 文件，并提供许多属性来自定义 `targets` 文件中定义的构建行为。通过这种方式，MSBuild 与 Maven 有细微的相似之处，因为都呈现了典型的构建模式，由项目对其进行自定义。

在 MSBuild 脚本中，从上到下读取文件，最后定义属性或 `target` 的将胜出（与 Ant 不同，第一个定义的地方为胜者）。这种行为意味着你在 MSBuild 脚本 `targets` 文件中编写的任何内容都会覆盖导入模板中的行为。

微软提供的标准模板包含许多 `targets` 文件，这些文件在标准模板中以 `Before` 或 `After` 命名调用，被设计为在之前或之后运行你自定义逻辑的钩点。一个经典的例子是 `BeforeBuild` 和 `AfterBuild`。良好的做法是只覆盖被设计为可覆盖的 `target`，或者覆盖用于控制构建过程的属性。导入的 `targets` 文件通常是广为人知的，如果你想进一步了解它们的作用，可以阅读它们。

以下是由 Visual Studio 2011 生成的简单 `.vbproj` 文件，用于一个简单的 Hello World 风格应用程序。希望你现在能识别并理解文件中的许多元素。注意它不包含任何 Targets——这些都在导入的 Microsoft

`.VisualBasic.target.files` 包含了 Visual Basic 编译器的实际布局。`.vbproj` 文件包含属性和项目组 `ItemGroups`，这些内容配置了 `.target` 的行为：

```xml
<?xml version="1.0" encoding="utf-8"?>
<ProjectTools Version="4.0" DefaultTargets="Build"
  xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <PropertyGroup>
    <Configuration Condition="$(Configuration)" == 'Debug'</Configuration>
    <Platform Condition="$(Platform)" == 'x86'</Platform>
    <ProductVersion></ProductVersion>
    <SchemaVersion></SchemaVersion>
    <ProjectGuid>D3961BC-0340-4462-A7A3-85C66F37176</ProjectGuid>
    <OutputType>Exe</OutputType>
    <StartupObject>HelloWorld</StartupObject>
    <Namespace>HelloWorld</Namespace>
    <FileAlignment>51</FileAlignment>
    <Type>Console</Type>
    <TargetFrameworkVersion>v4.5</TargetFrameworkVersion>
  </PropertyGroup>
  <PropertyGroup Condition="$(Configuration) | '$(Platform)" == 'Debug|x86'>
    <PlatformTarget>x86</PlatformTarget>
    <DebugSymbols>true</DebugSymbols>
    <DebugType>full</DebugType>
    <DefineDebug>true</DefineDebug>
    <DefineTrace>true</DefineTrace>
    <OutputPath>Path</OutputPath>
    <DocumentationFile>HelloWorld.xml</DocumentationFile>
    <NoWarn>42016,42019,42017,42018,42019,42032,42036,42020,42021,42022</NoWarn>
  </PropertyGroup>
  <PropertyGroup Condition="$(Configuration) | '$(Platform)" == 'Release|x86'>
    <PlatformTarget>x86</PlatformTarget>
    <DebugType>none</DebugType>
    <DefineDebug>false</DefineDebug>
    <DefineTrace>true</DefineTrace>
    <Optimize>true</Optimize>
    <OutputPath>Release</OutputPath>
    <DocumentationFile>HelloWorld.xml</DocumentationFile>
    <NoWarn>42016,42019,42017,42018,42019,42032,42036,42020,42021,42022</NoWarn>
  </PropertyGroup>
  <PropertyGroup>
    <OptionExplicit>On</OptionExplicit>
  </PropertyGroup>
  <PropertyGroup>
    <OptionCompare>Binary</OptionCompare>
  </PropertyGroup>
  <PropertyGroup>
    <OptionStrict>Off</OptionStrict>
  </PropertyGroup>
  <PropertyGroup>
    <OptionInfer>On</OptionInfer>
  </PropertyGroup>
```
