
对文件进行签名的含义如下：生成强命名程序集时，程序集的 FileDef 清单元数据表会包含组成该程序集的所有文件的列表。当每个文件的名称被添加到清单中时，会计算文件内容的哈希，并将该哈希值连同文件名一起存储在 FileDef 表中。可以使用 AL.exe 的 `/algid` 开关覆盖默认哈希算法，也可以在程序集的某个源代码文件中应用程序集级 `System.Reflection.AssemblyAlgorithmIdAttribute` 自定义特性。默认情况下，使用 SHA-1 算法。

生成包含清单的 PE 文件后，对 PE 文件的全部内容（除任何 Authenticode 签名、程序集的强名称数据和 PE 头校验和之外）进行哈希，如图 3-1 所示。该哈希值使用发布者的私钥签名，生成的 RSA 数字签名存储在 PE 文件内的保留节中（不包含在哈希中）。PE 文件的 CLR 头会更新，以反映数字签名嵌入文件中的位置。

![](img/857bdf6cef9e242b53a37f88df9a1287_95_0.png)

**图 3-1** 对程序集进行签名。

发布者的公钥也会嵌入此 PE 文件的 AssemblyDef 清单元数据表中。文件名、程序集版本、区域性和公钥的组合赋予该程序集强名称，保证其唯一。除非两家公司彼此共享该密钥对，否则它们不可能各自生成一个名为 *OurLibrary* 且使用相同公钥/私钥的程序集。

此时，程序集及其所有文件已准备好打包和分发。

如第 2 章所述，编译源代码时，编译器会检测代码引用的类型和成员。必须向编译器指定所引用的程序集。对于 C# 编译器，使用 `/reference` 编译器开关。编译器的一项工作是在生成的托管模块中生成 AssemblyRef 元数据表。AssemblyRef 元数据表中的每个条目指示所引用程序集的名称（不含路径和扩展名）、版本号、区域性和公钥信息。

这等效于以下内容。

> "SomeClassLibrary, Version=3.0.0.0, Culture=neutral, PublicKeyToken=null"

在这一行中，未指定公钥标记，因为该 DLL 程序集未使用公钥/私钥对签名，因此它是弱命名程序集。如果我使用 SN.exe 创建密钥文件，并使用 /keyfile 编译器开关编译，则生成的程序集就会已签名。如果我随后使用 ILDasm.exe 查看新程序集的元数据，AssemblyDef 条目会在 Public Key 字段后出现字节，并且该程序集将是强命名的。顺便说一句，AssemblyDef 条目始终存储完整公钥，而不是公钥标记。完整公钥对于确保文件未被篡改是必要的。本章后面我将解释强命名程序集的防篡改能力。

## 全局程序集缓存

既然知道了如何创建强命名程序集，现在该学习如何部署该程序集，以及 CLR 如何使用这些信息定位并加载程序集。

如果多个应用程序要访问某个程序集，就必须将该程序集放到一个众所周知的目录中，并且当检测到对该程序集的引用时，CLR 必须知道自动查看此目录。这个众所周知的位置称为全局程序集缓存 (GAC)。GAC 的确切位置是实现细节，可能随 .NET Framework 的不同版本而变化。不过，通常可以在以下目录中找到它：

```text
%SystemRoot%\Microsoft.NET\Assembly
```

GAC 目录是有结构的。它包含许多子目录，并使用一种算法生成这些子目录的名称。绝不要手动将程序集文件复制到 GAC 中；而应使用工具完成此任务。这些工具了解 GAC 的内部结构以及如何生成正确的子目录名。

在开发和测试期间，可以使用最常见的工具将强命名程序集安装到 GAC 中，即 GACUtil.exe。不带任何命令行参数运行此工具会显示以下用法。

```text
Microsoft (R) .NET Global Assembly Cache Utility.  Version 4.0.30319.17929
Copyright (c) Microsoft Corporation.  All rights reserved.

Usage: Gacutil <command> [ <options> ]
Commands:
  /i <assembly_path> [ /r <...> ] [ /f ]
      Installs an assembly to the global assembly cache.

  /il <assembly_path_list_file> [ /r <...> ] [ /f ]
      Installs one or more assemblies to the global assembly cache.

  /u <assembly_display_name> [/r <...>]
      Uninstalls an assembly from the global assembly cache.

  /ul <assembly_display_name_list_file> [/r <...>]
      Uninstalls one or more assemblies from the global assembly cache.

  /l [<assembly_name>]
      List the global assembly cache filtered by <assembly_name>

  /r [<assembly_name>]
      List the global assembly cache with all traced references.

  /cdl
      Deletes the contents of the download cache

  /dl
      Lists the contents of the download cache

  /?
      Displays a detailed help screen

Options:
  /r <reference_scheme> <reference_id> <description>
      Specifies a traced reference to install (/i, /il) or uninstall (/u, /ul).

  /f
      Forces reinstall of an assembly.

  /nologo
      Suppresses display of the logo banner

  /silent
      Suppresses display of all output
```

如你所见，可以调用 GACUtil.exe，指定 /i 开关将程序集安装到 GAC，还可以使用 GACUtil.exe 的 /u 开关从 GAC 卸载程序集。注意，绝不能将弱命名程序集放入 GAC。如果将弱命名程序集的文件名传递给 GACUtil.exe，它会显示以下错误消息：向缓存添加程序集失败：尝试安装没有强名称的程序集。

> **注意** 默认情况下，只有属于 Windows Administrators 组的用户才能操作 GAC。如果调用该实用程序执行操作的用户不是此组的成员，GACUtil.exe 将无法安装或卸载程序集。

使用 GACUtil.exe 的 /i 开关对开发人员测试非常方便。但是，如果在生产环境中使用 GACUtil.exe 部署程序集，建议除了指定 /i 或 /u 开关来安装或卸载程序集外，还使用 GACUtil.exe 的 /r 开关。/r 开关将程序集与 Windows 安装和卸载引擎集成。基本上，它告诉系统哪个应用程序需要该程序集，然后将应用程序和程序集关联在一起。

> 注意 如果强命名程序集打包在 cabinet (.cab) 文件中或以某种方式压缩，则必须先将其文件解压缩到临时文件，然后才能使用 GACUtil.exe 将程序集的文件安装到 GAC 中。程序集文件安装完成后，可以删除临时文件。

GACUtil.exe 工具不随最终用户 .NET Framework 可再发行组件包一起提供。如果应用程序包含要部署到 GAC 中的某些程序集，则应使用 Windows Installer (MSI)，因为 MSI 是唯一保证存在于最终用户计算机上且能够将程序集安装到 GAC 中的工具。

> 重要 将程序集文件全局部署到 GAC 是注册程序集的一种形式，尽管实际 Windows 注册表不会受到任何影响。将程序集安装到 GAC 会破坏简单应用程序安装、备份、还原、移动和卸载的目标。因此建议尽可能避免全局部署并使用私有部署。

在 GAC 中“注册”程序集的目的是什么？假设两家公司各自生成一个由一个文件组成的 OurLibrary 程序集：OurLibrary.dll。显然，这两个文件不能放在同一目录中，因为后安装的文件会覆盖先安装的文件，必然破坏某些应用程序。将程序集安装到 GAC 时，会在 %SystemRoot%\Microsoft.NET\Assembly 目录下创建专用子目录，并将程序集文件复制到其中一个子目录中。

通常没人会检查 GAC 的子目录，因此 GAC 的结构对你来说并不重要。只要工具和 CLR 知道该结构，就一切正常。

## 构建引用强命名程序集的程序集

无论何时构建程序集，该程序集都会引用其他强命名程序集。这是因为 System.Object 定义在 MSCorLib.dll 中，而该文件是强命名的。然而，程序集很可能引用由 Microsoft、第三方或你自己的组织发布的其他强命名程序集中的类型。在第 2 章中，我展示了如何使用 CSC.exe 的 `/reference` 编译器开关指定要引用的程序集文件名。如果文件名是完整路径，CSC.exe 会加载指定的文件并使用其元数据信息构建程序集。如第 2 章所述，如果指定的文件名不带路径，CSC.exe 会尝试按以下目录（按此处列出的顺序）查找程序集：

- 1. 工作目录。
- 2. 包含 CSC.exe 文件本身的目录。此目录还包含 CLR DLL。
