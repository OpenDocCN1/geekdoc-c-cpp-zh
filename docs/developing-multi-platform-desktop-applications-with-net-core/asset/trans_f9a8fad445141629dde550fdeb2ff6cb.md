

## 9.1 .NET CORE CLI 本地工具

在 .NET Core 应用程序开发中，依赖项由 NuGet 包管理，与经典 .NET 框架相比，这提供了一种更好的方式来保持依赖项的最新状态。

这种架构为您开发的应用程序所使用的依赖项提供了一致性和可维护性。这是 .NET Core 框架的关键基础；每种专用功能都必须通过特定的 NuGet 包进行集成。

您可以使用 dotnet CLI 的 restore 命令在项目中解决包的更新问题。

如果您在 .NET Core 3.0 中尝试过本地工具，例如运行“dotnet tool restore”或“dotnet tool install”，请删除本地工具缓存文件夹。否则，本地工具在任何较新版本中都将无法工作。该文件夹位于：

### 在 macOS 和 Linux 上：

```
@user>rm -r $HOME/.dotnet/toolResolverCache
```

### 在 Windows 上：

```
C:>rmdir /s
%USERPROFILE%\.dotnet\toolResolverCache
```

本地工具依赖于当前项目目录（dotnet 文件夹）中名为“dotnet-tools.json”的清单文件。此清单文件定义工具是否可用。您可以随代码分发清单文件，以确保任何使用您代码的人都可以恢复和使用相同的工具。

## 9.2 .NET CORE CLI 生成选项

"dotnet CLI" 是允许开发者管理 .NET Core 3 源代码和资源的工具。各种命令使能够执行特定任务（例如“dotnet run”，用于执行程序）。这些命令中的每一个都定义了自己的参数集。

可使用多个 dotnet 命令来构建您的项目，您可以根据预期的结果类型选择其中一种。这些命令是用于显式构建 dotnet 项目的“build”以及将项目（及其依赖项）打包到可部署文件夹中的“publish”。

以下是 dotnet CLI 工具默认提供的基本命令预览（最常用）：

- new: 基于指定模板创建新项、项目或元素。
- restore: 恢复项目的依赖项。
- build: 创建项目的 CLR 映像。
- run: 执行项目。
- publish: 将项目的 CLR 映像打包以供部署。
- test: 执行单元测试。
- pack: 将项目打包为 NuGet 包。
- clean: 擦除项目的程序集映像。
- help: 显示指定命令的详细文档。
- store: 将程序集记录到运行时包存储中。

所有这些命令都非常有趣，但我们将考虑最常用的命令。我们将深入回顾其中两个命令：build 和 publish。

### 9.2.1 dotnet build

"build" 命令生成项目及其所有依赖项的 .NET Core 程序集。该命令还执行依赖项的“隐式”恢复。

您可以直接从命令行编译和构建 .NET Core 3 项目，如下所示（您必须位于包含 .csproj 文件的文件夹中）。

```
C:>dotnet build
```

当然，您可以定义更复杂的构建命令行指令，如下所示。

```
C:>dotnet build -r win-x64 --configuration Release
```

以下是前一条命令行指令中最常用选项的说明。

- -c (或 --configuration): 定义构建所使用的配置，默认值为 "Debug"（如有需要请指定 "Release"）
- -o (或 --output): 定义 build 命令生成的程序集的目标文件夹。
- -r (或 --runtime): 指定目标运行时（请参阅 RID 参考）

### 9.2.2 dotnet publish

"publish" 命令生成项目及其所有依赖项的 .NET Core 程序集。"publish" 命令也会触发构建。它实际上与“build”命令的结果几乎相同，但提供了一些额外功能。

您可以直接从命令行“发布” .NET Core 3 项目，如下所示。

```
C:>dotnet publish
```

您可以定义更复杂的“发布”命令，如下所示。

```
C:>dotnet publish -c Release -r win-x64 --self-contained /p:PublishSingleFile=true
```

以下是前一条命令行指令中最常用选项的说明。

- -c (或 --configuration): 定义发布所使用的配置。
- -o (或 --output): 将应用程序发布到指定文件夹中。
- -r (或 --runtime): 为给定运行时发布应用程序。
- --self-contained: 随 .NET Core 运行时一起发布应用程序（在这种情况下，运行应用程序的目标计算机上不再需要 dotnet core）

这只是“dotnet”命令行可用的所有选项和命令的快速预览。有关选项和开关的完整详尽参考，您可以阅读以下参考链接中的 Microsoft 文档。

https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet/
https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-build
https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-publish

这两个命令都使用 .csproj 文件来构建项目（添加到命令行参数中）。

## 9.3 CSPROJ 文件结构

.NET Core 3 使用新的 .csproj 文件格式（替换 .NET Core 2 的 project.json），供 MSBuild 用于项目构建过程。

借助这种新的 .csproj 文件格式，Microsoft 完成了出色的简化工作（比以前简洁得多），同时也为其添加了功能（例如指定在构建时生成 NuGet 包）。

.csproj 文件由 MSBuild 可解释的 XML 文件组成，它构成了引导构建过程的脚本（dotnet CLI 也是如此）。

.csproj 文件由 MSBuild 用于编译、构建和链接您的项目。它提供许多功能选项：

- 单个 exe 打包。
- NuGet 包创建。
- 多框架目标。
- 条件引用。
- 条件编译。

以下是 .csproj 文件的简单示例：

```
<Project Sdk="Microsoft.NET.Sdk">
<PropertyGroup>
<TargetFramework>netcoreapp3.0</TargetFramework>
</PropertyGroup>
<ItemGroup>
<PackageReference Include="Microsoft.Extensions.Configuration" />
</ItemGroup>
</Project>
```

(csproj 图 1)

".csproj" 文件包含两个部分；这些部分是主节点 <Project> 的子节点（请参阅 csproj 图 1）：

- <PropertyGroup>: 此部分包含与项目相关的一组属性；这些属性由 MSBuild 用于生成可执行文件（MSIL 或本机）。

您还可以添加有关构建执行环境或所选选项（在代码中）的条件属性。

- <TargetFramework>: 指定应用程序使用的框架，这是 .csproj 文件的必填项。您可以指定多个框架（逗号分隔）。

- <OutputType>: 指定可执行文件输出类型

- <AssemblyName>: 这是程序集名称。

- <OutputPath>: 这是构建的输出文件将被复制到的路径。

- <Optimization>: 指定是否要使用优化（true/false）。
- <ItemGroup>: 此部分包含用户定义的 Item 元素。
- <PackageReferences>: 允许您根据目标框架和版本号选择引用的包（可选）。

对于上述呈现的属性，您可以使用通配符（?, *, **）以实现对版本号、文件名等的更大匹配 ...
"?" 匹配单个字符。
"*" 匹配字符串或空字符串。
"**" 匹配部分路径。

- 条件包引用
- .csproj 文件语法允许您使用条件来包含包引用（根据框架版本、配置、平台 ...）。

以下是此类 .csproj 功能的演示片段。

```
<PropertyGroup>
    <Apple>True</Apple>
    <Banana>False</Banana>
    <Pear>False</Pear>
</PropertyGroup>

<Target Name="GetFruit">
    <ItemGroup>
        <AllFruits Include="Apple" Condition="'$(Apple)'=='true'" />
        <AllFruits Include="Banana" Condition="'$(Banana)'=='true'" />
    </ItemGroup>
</Target>
```

