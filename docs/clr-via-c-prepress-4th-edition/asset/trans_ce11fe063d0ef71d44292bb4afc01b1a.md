
在开发和测试期间，将强命名程序集安装到 GAC 中最常用的工具是 GACUtil.exe。不带任何命令行参数运行该工具时，会显示以下用法：

```text
Microsoft (R) .NET Global Assembly Cache Utility. Version 4.0.30319.17929
Copyright (c) Microsoft Corporation.  All rights reserved.

Usage: Gacutil <command> [ <options> ]
Commands:
 /i <assembly_path> [ /r <...> ] [ /f ]
    Installs an assembly to the global assembly cache.

 /il <assembly_path_list_file> [ /r <...> ] [ /f ]
    Installs one or more assemblies to the global assembly cache.

 /u <assembly_display_name> [ /r <...> ]
    Uninstalls an assembly from the global assembly cache.

 /ul <assembly_display_name_list_file> [ /r <...> ]
    Uninstalls one or more assemblies from the global assembly cache.

 /l [ <assembly_name> ]
    List the global assembly cache filtered by <assembly_name>

 /lr [ <assembly_name> ]
    List the global assembly cache with all traced references.

 /cdl
    Deletes the contents of the download cache

 /ldl
    Lists the contents of the download cache

 /?
    Displays a detailed help screen

Options:
 /r <reference scheme> <reference id> <description>
    Specifies a traced reference to install (/i, /il) or uninstall (/u, /ul).

 /f
    Forces reinstall of an assembly.

 /nologo
    Suppresses display of the logo banner

 /silent
    Suppresses display of all output
```

如你所见，可以调用 GACUtil.exe，指定 /i 开关将程序集安装到 GAC；也可以使用 GACUtil.exe /u 开关从 GAC 卸载程序集。注意，你永远不能将弱命名程序集放入 GAC。如果将弱命名程序集的文件名传递给 GACUtil.exe，它会显示以下错误消息：“向缓存添加程序集失败：尝试安装没有强名称的程序集。”

**注意** 默认情况下，只有属于 Windows Administrators 组的用户才能操作 GAC。如果调用该工具的用户不是此组的成员，GACUtil.exe 将无法安装或卸载程序集。

使用 GACUtil.exe 的 /i 开关对开发人员测试非常方便。但是，如果使用 GACUtil.exe 在生产环境中部署程序集，建议除了指定 /i 或 /u 开关来安装或卸载程序集之外，还要使用 GACUtil.exe 的 /r 开关。/r 开关会将程序集与 Windows 安装和卸载服务集成。基本上，它告诉系统哪个应用程序需要该程序集，然后将应用程序和程序集绑定在一起。

**注意** 如果强命名程序集打包在 Cabinet（.cab）文件中或以某种方式压缩，则必须先将该程序集的文件解压到临时文件，然后才能使用 GACUtil.exe 将程序集的文件安装到 GAC。程序集的文件安装完成后，可以删除临时文件。

GACUtil.exe 工具不随最终用户 .NET Framework 可再发行组件包提供。如果你的应用程序包含一些要部署到 GAC 的程序集，则应使用 Windows Installer (MSI)，因为 MSI 是唯一保证存在于最终用户计算机上并且能够将程序集安装到 GAC 的工具。

**重要** 将程序集文件全局部署到 GAC 是注册程序集的一种形式，尽管实际的 Windows 注册表不会受到任何影响。将程序集安装到 GAC 会破坏简单应用程序安装、备份、还原、移动和卸载的目标。因此，建议尽可能避免全局部署，而使用私有部署。

在 GAC 中“注册”程序集的目的是什么？假设有两家公司各自生成一个 OurLibrary 程序集，该程序集由一个文件组成：OurLibrary.dll。显然，这两个文件不能放在同一目录中，因为最后安装的文件会覆盖先安装的文件，这必然破坏某些应用程序。当你将程序集安装到 GAC 时，会在 %SystemRoot%\Microsoft.NET\Assembly 目录下创建专用子目录，并且程序集文件会被复制到其中一个子目录中。

通常，没有人会检查 GAC 的子目录，因此 GAC 的结构实际上不应该对你重要。只要工具和 CLR 知道该结构，一切就都没问题。

## 生成引用强命名程序集的程序集

每当生成程序集时，该程序集都会引用其他强命名程序集。这是真的，因为 System.Object 定义在 MSCorLib.dll 中，而 MSCorLib.dll 是强命名的。但是，程序集很可能引用由 Microsoft、第三方或你自己的组织发布的其他强命名程序集中的类型。在第 2 章中，我向你展示了如何使用 CSC.exe 的 /reference 编译器开关来指定要引用的程序集文件名。如果文件名是完整路径，CSC.exe 会加载指定的文件，并使用其元数据信息生成程序集。如第 2 章所述，如果指定的文件名没有路径，CSC.exe 会尝试按以下目录顺序查找程序集（按此处列出的顺序）：

- 1. 工作目录。
- 2. 包含 CSC.exe 文件本身的目录。此目录还包含 CLR DLL。
- 3. 使用 /lib 编译器开关指定的任何目录。
- 4. 使用 LIB 环境变量指定的任何目录。

因此，如果要生成引用 Microsoft 的 System.Drawing.dll 的程序集，可以在调用 CSC.exe 时指定 /reference:System.Drawing.dll 开关。编译器将检查前面显示的目录，并在包含 CSC.exe 文件本身的目录中找到 System.Drawing.dll 文件，该目录与包含编译器所绑定 CLR 版本的 DLL 的目录相同。尽管这是编译时找到程序集的目录，但这并不是运行时加载程序集的目录。

你看，安装 .NET Framework 时，实际上会安装 Microsoft 程序集文件的两份副本。一组安装到编译器/CLR 目录，另一组安装到 GAC 子目录。编译器/CLR 目录中的文件存在是为了让你可以轻松生成程序集，而 GAC 中的副本存在是为了在运行时加载它们。

CSC.exe 不在 GAC 中查找被引用程序集的原因是，你必须知道程序集文件的路径，而 GAC 的结构没有文档记录。另一种方案是，CSC.exe 可以允许你指定一个仍然很长但稍微好看一点的字符串，例如“System.Drawing, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a”。这两种解决方案都被认为比在用户硬盘上安装两次程序集文件更糟。

此外，编译器/CLR 目录中的程序集与机器无关。也就是说，这些程序集只包含元数据。由于生成时不需要 IL 代码，此目录不必包含程序集的 x86、x64 和 ARM 版本。GAC 中的程序集包含元数据和 IL 代码，因为只有在运行时才需要代码。而且，由于代码可以针对特定 CPU 架构进行微调，GAC 允许程序集的多个副本驻留在其中；每个副本位于针对每种 CPU 架构的不同子目录下。

## 强命名程序集是防篡改的

使用私钥对程序集进行签名，并将签名和公钥嵌入程序集，使 CLR 能够验证程序集未被修改或损坏。当程序集安装到 GAC 时，系统会对包含清单的文件内容进行哈希，并将哈希值与嵌入 PE 文件中的 RSA 数字签名值进行比较（在用公钥验证签名之后）。如果值相同，则文件内容未被篡改。此外，系统还会对程序集其他文件的内容进行哈希，并将哈希值与清单文件 FileDef 表中存储的哈希值进行比较。如果任何哈希值不匹配，则至少有一个程序集文件已被篡改，程序集将无法安装到 GAC。

当应用程序需要绑定到程序集时，CLR 使用被引用程序集的属性（名称、版本、区域性和公钥）在 GAC 中定位程序集。如果找到被引用的程序集，则返回包含它的子目录，并加载包含清单的文件。以这种方式找到程序集可以向调用方保证：运行时加载的程序集与编译代码时所依据的程序集来自同一发布者。这种保证之所以可行，是因为引用程序集的 AssemblyRef 表中的公钥标记与被引用程序集的 AssemblyDef 表中的公钥相对应。如果被引用的程序集不在 GAC 中，CLR 会先查找应用程序的基目录，然后查找应用程序配置文件中标识的任何私有路径；接着，如果应用程序是使用 MSI 安装的，CLR 会要求 MSI 定位程序集。如果在这些位置中的任何一处都找不到该程序集，绑定就会失败，并引发 `System.IO.FileNotFoundException`。

当从 GAC 以外的位置（通过应用程序的基目录或通过配置文件中的 codeBase 元素）加载强命名程序集文件时，CLR 会在加载程序集时比较哈希值。换句话说，每次应用程序执行并加载程序集时，都会对文件进行哈希。这种性能损失是为了确保程序集内容未被篡改而付出的代价。当 CLR 在运行时检测到哈希值不匹配时，会引发 `System.IO.FileLoadException`。

**注意** 当强命名程序集安装到 GAC 中时，系统会确保包含清单的文件未被篡改。此检查只在安装时发生一次。此外，为了提高性能，如果强命名程序集是完全受信任的，并且正在加载到完全受信任的 AppDomain 中，CLR 不会检查该程序集是否被篡改。另一方面，当从 GAC 以外的目录加载强命名程序集时，CLR 会验证程序集的清单文件，以确保文件内容未被篡改，因此每次加载该文件时都会造成额外的性能损失。

