
`C:\AppDir\en-US\AsName.dll`

`C:\AppDir\firstPrivatePath\en-US\AsName.dll`

`C:\AppDir\firstPrivatePath\en-US\AsName.dll`

`C:\AppDir\secondPrivatePath\en-US\AsName.dll`

`C:\AppDir\secondPrivatePath\en-US\AsName.dll`

`C:\AppDir\en-US\AsName.exe`

`C:\AppDir\en-US\AsName.exe`

`C:\AppDir\firstPrivatePath\en-US\AsName.exe`

`C:\AppDir\secondPrivatePath\en-US\AsName.exe`

`C:\AppDir\secondPrivatePath\en-US\AsName.exe`

## 第 2 章 构建、打包、部署和管理应用程序与类型 63

`C:\AppDir\en\AsmName.dll`

`C:\AppDir\en\AsmName.dll`

`C:\AppDir\firstPrivatePath\en\AsmName.dll`

`C:\AppDir\firstPrivatePath\en\AsmName.dll`

`C:\AppDir\secondPrivatePath\en\AsmName.dll`

`C:\AppDir\secondPrivatePath\en\AsmName.dll`

`C:\AppDir\en\AsmName.exe`

`C:\AppDir\en\AsmName.exe`

`C:\AppDir\firstPrivatePath\en\AsmName.exe`

`C:\AppDir\firstPrivatePath\en\AsmName.exe`

`C:\AppDir\secondPrivatePath\en\AsmName.exe`

`C:\AppDir\secondPrivatePath\en\AsmName.exe`

如你所见，CLR 会探测具有 `.exe` 或 `.dll` 扩展名的文件。由于探测这些文件可能非常耗时（尤其是当通过网络进行探测时），在 XML 配置文件中，你可以指定一个或多个 `culture` 元素，以限制 CLR 在查找卫星程序集时执行的探测。

此 XML 配置文件的名称和位置取决于应用程序的类型：

- 可执行应用程序 `EXEs`：配置文件必须位于应用程序的基目录中，且其名称必须是 EXE 文件名加上 `config` 后。
- Microsoft ASP.Net Web Form 应用程序：文件必须位于 Web 应用程序的虚拟根目录中，且始终命名为 `Web.config`。此外，子目录也可以包含自己的 `Web.config` 文件，且配置设置会被继承。例如，位于 http://Wintlect.com/Training 的 Web 应用程序将使用虚拟根目录及其 Training 子目录中 `Web.config` 文件中的设置。

正如本节开头提到的，配置设置适用于特定的应用程序和机器。当你安装 .NET Framework 时，它会创建一个 `Machine.config` 文件。对于机器上安装的每个版本的 CLR，都有一个 `Machine.config` 文件。

`Machine.config` 文件位于以下目录：

```
%SystemRoot%\Microsoft.NET\Framework\version\CONFIG
```

当然，`%SystemRoot%` 代表你的 Windows 目录（通常是 `C:\WINDOWS`），`version` 是标识特定 .NET Framework 版本的数字（类似于 `v4.0.####`）。

## 第一部分 | CLR 基础知识

`Machine.config` 文件中的设置代表影响机器上运行的所有应用程序的默认设置。管理员可以通过修改唯一的 `Machine.config` 文件来创建全局范围策略。然而，管理员和用户应避免修改此文件，因为它包含了与许多事项相关的设置，使其变得难以导航。此外，你还希望应用程序的设置得到备份。

## 第 3 章 共享程序集与强命名程序集

- 本章内容：
- 两种程序集，两种部署方式 ...... 66
- 为程序集命名.............................................. 67
- 全局程序集缓存 `GAC`................................ 75
- 强命名程序集具有防篡改性 .............. 76
- 私有部署程序集........................................... 80
- 运行时如何解析程序集.................. 81
- 高级配置（程序集）.................... 84

正如本节开头提到的，配置设置适用于特定的应用程序和机器。当你安装 .NET Framework 时，它会创建一个 `Machine.config` 文件。对于机器上安装的每个版本的 CLR，都有一个 `Machine.config` 文件。

`Machine.config` 文件位于以下目录：

```
%SystemRoot%\Microsoft.NET\Framework\version\CONFIG
```

当然，`%SystemRoot%` 代表你的 Windows 目录（通常是 `C:\WINDOWS`），`version` 是标识特定 .NET Framework 版本的数字（类似于 `v4.0.####`）。

`Machine.config` 文件中的设置代表影响机器上运行的所有应用程序的默认设置。管理员可以通过修改唯一的 `Machine.config` 文件来创建全局范围策略。然而，管理员和用户应避免修改此文件，因为它包含了与许多事项相关的设置，使其变得难以导航。此外，你还希望应用程序的设置得到备份。

正如本节开头提到的，配置设置适用于特定的应用程序和机器。当你安装 .NET Framework 时，它会创建一个 `Machine.config` 文件。对于机器上安装的每个版本的 CLR，都有一个 `Machine.config` 文件。

在第 2 章“构建、打包、部署和管理应用程序与类型”中，我关注的是哪些程序集可以部署。在本章中，我将解释 .NET Framework 用于处理版本控制的基础设施。预警一下：我即将描述的内容非常复杂。我将介绍许多内置在公共语言运行时 `CLR` 中的算法、规则和策略。我还会提到许多开发者必须使用的工具和实用程序。这些之所以复杂，是因为正如我提到的，版本问题很难处理和解决。

`CLR` 支持两种程序集：弱命名程序集和强命名程序集。

> 重要 顺便说一下，你不会任何 .NET Framework 文档中找到“弱命名程序集”这个术语。为什么？因为这是我发明的。事实上，文档中没有术语来标识弱命名程序集。我决定创造这个术语，以便我在讨论程序集类型时不会产生歧义。弱命名和强命名程序集之间的真实区别在于

# 第3章 共享程序集与强命名程序集 67

强命名程序集是指使用发布者的公钥/私钥对签名的程序集，该密钥对可以唯一标识程序的发布者。该密钥对允许程序集被唯一标识和保护，并允许将其部署在用户机器或互联网上的任何地方。这种识别程序集的能力允许 `CLR` 在应用程序尝试绑定强命名程序集时，执行某些已知的安全策略。本章专门解释什么是命名程序集以及 `CLR` 对它们应用哪些策略。

程序集可以通过两种方式部署：私有或全局。私有部署的程序集是部署在程序集根目录或其子目录下的程序集。弱命名程序集可以进行私有部署。我在第2章中讨论过私有部署的程序集。全局部署的程序集部署在某些已知位置，`CLR` 在搜索程序集时会查找这些位置。强命名程序集可以私有或全局部署。我将在本章中解释如何创建和部署强命名程序集。表 3-1 总结了程序集及其部署方式。

## 表 3-1 弱命名和强命名程序集的部署方式

| 程序集类型 | 可以私有部署 | 可以全局部署 |
|---|---|---|
| 弱命名 | 是 | 否 |
| 强命名 | 是 | 是 |

> 注意：强烈建议你对所有程序集进行命名。事实上，`CLR` 的未来版本可能要求所有程序集都必须是强命名的，且创建弱命名程序集的能力将被弃用。弱命名程序集是一个问题，因为可能存在多个同名但不同的程序集。另一方面，为程序集指定强名称可以唯一标识该程序集。如果 `CLR` 能够唯一标识它，就可以对版本控制或向后兼容应用更多策略。微软的计划是确保未来的 `CLR` 版本通过这些策略使版本控制变得更简单。事实上，消除创建弱命名程序集的能力会让 `CLR` 的版本控制更加简单。

## 为程序集指定强名称

如果有多个应用程序需要访问某个程序集，该程序集必须放在已知目录中，并且检测到对该程序集的引用时，`CLR` 必须知道在该目录查找。然而，我们面临一个问题：两个（或多个）公司可能会产生相同文件的程序集。如果这两个程序集都被复制到同一个已知目录中，后一个将胜出，所有使用旧程序集的应用程序都将无法按预期运行。（这正是今天 Windows 中存在 DLL 的原因，共享 DLL 都被复制到 System32 目录：）

## 第一部分 CLR 基础

显然，仅仅通过文件名来区分程序集是不够的。`CLR` 需要支持某种机制允许程序集被唯一标识。这就是“强命名程序集”术语的含义。一个强命名程序集由四个唯一标识该程序集的属性组成：名称（不带扩展名）、版本号、文化 `Culture` 和公钥。由于公钥是很大的数字，我们经常使用从公钥派生出的短哈希值。这个哈希称为公钥令牌 `Public Key Token`。以下程序集标识字符串（有时称为程序集显示名称）标识了不同的程序集：

```
"MyTypes,Version=1.0.8123.0, Culture=neutral, PublicKeyToken=b7a55c561934e089"
"MyTypes,Version=1.0.8123.0, Culture="en-US", PublicKeyToken=b7a55c561934e089"
"MyTypes,Version=2.0.1234.0, Culture=neutral, PublicKeyToken=b7a55c561934e089"
"MyTypes,Version=1.0.8123.0, Culture=neutral, PublicKeyToken=b03f5f7f11d503a3"
```

第一个字符串标识一个名为 `MyTypes.exe` 或 `MyTypes.dll` 的程序集文件（无法从程序集标识字符串确定文件扩展名）。生产该程序集的公司正在创建该程序的 1.0.8123.0 版本，且程序集中没有内容对任何特定文化敏感，`Culture` 被设置为 `neutral`（中性）。或者，任何公司都可以生成一个标记为版本 1.0.8123.0 和中性文化的 `MyTypes.dll`（或 `MyTypes.exe`）程序集文件。

必须有一种方法将该公司的程序集与具有相同属性的其他程序集区分开。由于几个原因，微软可以使用标准的公钥/私钥加密技术，而不是任何其他唯一标识技术（如 GUID、URL 或 URN）。具体而言，加密技术提供了一种方法，在程序集安装到机器时检查其完整性，并且还允许按发布者授予权限。我将在本章稍晚时候讨论这些技术。因此，想要标记其程序集的公司必须创建一个公钥/私钥对。不应该有两个公司拥有相同的公钥/私钥对，这种区分允许两家公司创建相同名称、版本和文化的程序集而不会引起任何冲突。

> 注意：`System.Reflection.AssemblyName` 类是一个辅助类，可以让你更方便地构建程序集并获取程序集名称的各个部分。该类提供了几个公共实例属性，如 `CultureInfo`、`FullName`、`KeyPair` 和 `Version`。该类还提供了几个公共实例方法，如 `GetPublicKey`、`GetPublicKeyToken`、`SetPublicKey`。

在第2章中，展示了如何命名程序集以及如何应用版本和文化。弱命名程序集可以包含版本和文化元数据；然而，`CLR` 在探测程序集时，总是忽略版本号而仅使用文化。由于弱命名程序集是私有部署的，`CLR` 在应用程序基目录查找程序集文件（`.dll` 或 `.exe`）时，仅使用可扩展标记语言 `XML` 配置文件的 `probing` 属性。强命名程序集具有名称、版本和文化。此外，强命名程序集使用发布者的私钥进行签名。

创建强命名程序集的第一步是使用随 .NET Framework 和 Visual Studio 附带 `SN.exe` 工具获取密钥。该工具提供了许多命令行开关。注意，所有 `SN.exe` 的命令行开关都是大小敏感的。要生成公钥/私钥对，请如下运行 `SN.exe`：

```
SN -k MyCompany.snk
```

此行告诉 `SN.exe` 创建一个名为 `MyCompany.snk` 的文件。该文件将以二进制格式持久化公私钥。公钥数值很大。如果你想在创建包含公钥和私钥的文件后再次使用 `SN.exe` 工具查看实际公钥。要这样做，你必须使用 `-p` 参数执行 `SN.exe` 创建一个仅包含公钥的文件（`MyCompany.PublicKey`）：

```
SN -p MyCompany.snk MyCompany.PublicKey
```

然后，你调用 `SN.exe`，并将包含公钥的文件传递给 `-tp` 开关：

当我执行它时，得到以下输出：

```
Microsoft (R) .NET Framework Name Utility Version 4.0.20928.1
Copyright (c) Microsoft Corporation. All rights reserved.
Public key is
002400004800000094000000020000002400000010000001000100314311009f6d21b702111
850e453b2b9d6a8c02e0b7b40f753d67ab302047fc786397b6692915afbd84614a6f29401
22b33ac0b8c8c9ba80885d2f5b72653d696424d07f7164639d18651a48446231732cac83c626a550
69f21a125bc03193261176dd629eaeec90d36853d3febc7b81fc8b7817936a567cad608ae672b6
1f08be00
```

公钥令牌为 `3db32f3c8b842c9a`

`SN.exe` 工具没有提供任何方法让你显示私钥。

公钥的大小使得它们处理起来非常困难。为了给开发者（以及最终用户）方便，创建了公钥令牌 `public key tokens`。公钥令牌是公钥的 64 位哈希值。`SN.exe -tp` 命令会在输出的末尾显示与该公钥对应的公钥。

现在你已经知道如何创建公钥/私钥对，创建强名称程序集就变得简单了。当你编译程序集时，使用 `/keyfile:<file>` 编译器开关：

```bash
csc /keyfile:MyCompany.snk Program.cs
```
