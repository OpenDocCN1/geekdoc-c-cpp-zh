

## /baseaddress

使用 /target:library 选项创建 DLL 时，可以指定 DLL 的基地址。默认情况下，编译器会为您完成此操作，但如果您希望自行指定，也可以这样做。要实现此目的，您可以使用类似以下内容：

```
vbc.exe MyClass.vb /target:library /baseaddress:0x11110000
```

所有基地址均指定为十六进制数字。

## /bugreport

/bugreport 选项会创建一个文件，其中包含编译过程的完整报告。此文件包含您的代码以及计算机操作系统和编译器本身的版本信息。使用此选项的方式如下：

```
vbc.exe MyModule.vb /bugreport:bugsy.txt
```

## /codepage

默认情况下，编译器期望所有文件都使用 ANSI、Unicode 或 UTF-8 代码页。使用编译器的 /codepage 选项，您可以指定编译器实际应使用的代码页。将其设置为默认值之一的示例如下所示：

```
vbc.exe MyClass.vb /codepage:1252
```

1252 用于美式英语和大多数欧洲语言，尽管将其设置为日文假名也同样简单：

```
vbc.exe MyClass.vb /codepage:932
```

## /delaysign[+-:]

此编译器选项需要与 /key 或 /keycontainer 选项结合使用，后者处理程序集的签名。当与 /delaysign 选项一起使用时，编译器会为数字签名创建空间以供以后对程序集进行签名，而不是在此时实际签名程序集。您可以使用以下方式使用此选项：

```
vbc.exe MyModule.vb /key:myKey1.sn /delaysign
```

## /errorreport

此选项定义如何处理内部编译器错误。可能的设置有 prompt、send、none 或默认的 queue。Prompt 会提示用户是否允许将错误发送给 Microsoft。Send 会自动将错误发送给 Microsoft，而 None 仅在文本文件中报告错误。

## /filealign

大多数开发人员通常不使用 /filealign 设置，它使您可以指定输出文件中节或连续内存块的对齐方式。它使用以下结构：

```
vbc.exe MyModule.vb /filealign:2048
```

分配的数字是生成文件的字节大小，有效值包括 512、1024、2048、4096、8192 和 16384。

## /keycontainer

此命令会导致编译器创建可共享组件并将公钥放入组件的程序集清单中，同时使用私钥对程序集进行签名。按如下方式使用此选项：

```
vbc.exe MyModule.vb /keycontainer:myKey1
```

如果您的密钥容器名称包含空格，则必须将值用引号括起来，如下所示：

```
vbc.exe MyModule.vb /keycontainer:"my Key1"
```

## /keyfile

与 /keycontainer 选项类似，/key 选项会导致编译器将公钥放入组件的程序集清单中，同时使用私钥对程序集进行签名。按如下方式使用：

```
vbc.exe MyModule.vb /key:myKey1.sn
```

如果您的密钥名称包含空格，则必须将值用引号括起来，如下所示：

```
vbc.exe MyModule.vb /key:"my Key1.sn"
```

## /libpath

在使用 /reference 编译器选项引用其他程序集时，您并不总是拥有这些被引用程序集与正在编译的对象相同的位置。您可以使用 /libpath 选项指定被引用程序集的位置，如下例所示：

```
vbc.exe MyModule.vb /reference:MyAssembly.dll /libpath:c:\Reuters\bin
```

如果您希望编译器在多个位置搜索被引用的 DLL，则可以使用 /libpath 选项指定多个位置，用分号分隔位置：

```
vbc.exe MyModule.vb /reference:MyAssembly.dll /libpath:c:\Reuters\bin, c:\
```

这条命令意味着编译器将在 C:\Reuters\bin 目录和位于 C:\ 的根目录中查找 MyAssembly.dll。

## /main

使用 /main 或 /m 选项，您可以将编译器指向包含 Sub Main 过程的类或模块。按如下方式使用：

```
vbc.exe MyClass.vb /main:MyClass.vb
```

## /moduleassemblyname

此选项指定模块将成为其一部分的程序集的名称。

## /netcf

此选项无法从 Visual Studio 本身执行，但您可以使用此标志从 Visual Basic 命令行编译器使用。使用 /netcf 会导致编译器构建您的应用程序，使结果针对 .NET Compact Framework，而不是完整的 .NET Framework 本身。要实现此目的，请使用以下结构：

```
vbc.exe MyModule.vb /netcf
```

## /nostdlib

默认情况下，Visual Basic 编译器在编译过程中使用标准库（System.dll）和 vbc.rsp 资源文件。使用 /nostdlib 选项可告诉编译器在编译过程中不使用此文件，如下所示：

```
vbc.exe MyClass.vb /nostdlib
```

## /platform

/platform 选项使您可以指定编译应针对的平台。可能的选择包括以下内容：

- /platform:x86 — 将程序编译为 x86 系统
- /platform:x64 — 将程序编译为 64 位系统

```
# is specified.
# Reference the common Framework libraries
/r:Accessibility.dll
/r:Microsoft.Vsa.dll
/r:System.Configuration.Install.dll
/r:System.Data.dll
/r:System.Design.dll
/r:System.DirectoryServices.dll
/r:System.dll
/r:System.Drawing.Design.dll
/r:System.Drawing.dll
/r:System.EnterpriseServices.dll
/r:System.Management.dll
/r:System.Messaging.dll
/r:System.Runtime.Remoting.dll
/r:System.Runtime.Serialization.Formatters.Soap.dll
/r:System.Security.dll
/r:System.ServiceProcess.dll
/r:System.Web.dll
/r:System.Web.Mobile.dll
/r:System.Web.RegularExpressions.dll
/r:System.Web.Services.dll
/r:System.Windows.Forms.dll
/r:System.XML.dll

/r:System.Workflow.Activities.dll
/r:System.Workflow.ComponentModel.dll
/r:System.Workflow.Runtime.dll
/r:System.Runtime.Serialization.dll
/r:System.ServiceModel.dll

/r:System.Core.dll
/r:System.Xml.Linq.dll
/r:System.Data.Linq.dll
/r:System.Data.DataSetExtensions.dll
/r:System.Web.Extensions.dll
/r:System.Web.Extensions.Design.dll
/r:System.ServiceModel.Web.dll

# Import System and Microsoft.VisualBasic
/imports:System
/imports:Microsoft.VisualBasic
/imports:System.Linq
/imports:System.Xml.Linq
```

这些命令反映了使用此命令行编译器编译的每个项目所进行的引用和导入。请随意按您选择的修改此文件。如果您想添加自己的引用，只需将它们添加到列表并保存文件。从那时起，您进行的每次编译都将包含新的引用。如果您对使用 Visual Basic 命令行编译器更加熟悉，您会发现使用 .rsp 文件具有很大的威力——甚至是默认的 Visual Basic 文件。

## Visual Basic Power Packs 工具

本附录介绍了 Visual Basic Power Packs 工具。这些工具最初是一组离周期发布的软件包，重点是帮助维护传统 VB6 应用程序的开发人员开始过渡到 Visual Basic .NET。原始 Power Packs 的主要部分已作为 Visual Studio 中的功能集成。此外，除了 Power Packs，本章还介绍了一种供 VB6 用户使用的第二种工具，即 VB6 Interop Toolkit。这些工具包含一组功能，旨在帮助拥有多年 Visual Basic 经验的开发人员在 Visual Basic .NET 中复制在 VB6 中轻松完成的任务和行为。

本附录简要介绍了目前可用的两个安装包。这些包最初针对 Visual Studio 2005 发布，并已更新为 Visual Studio 2010。此外，Visual Basic Power Packs 3.0 包中用于打印的元素已完全集成到 Visual Studio 2008 SP1 中，并继续随 Visual Studio 2010 一起提供。

本附录重点关注三个领域：

- Power Packs 背景，包括目标和安装
- Interop Forms Toolkit 2.1
- Visual Basic Power Packs 3.0

这些工具可作为免费下载提供；然而，由于 Express 版本的许可限制，Visual Basic Express 和其他 Express 版本不支持任何加载项。因此，要利用 Interop Forms Toolkit，您需要 Visual Studio Standard 或更高版本的许可版本。您为何要利用 Power Packs 的问题，最好通过了解 Power Packs 所解决的问题来回答。这些不仅仅是为了技术而技术：它们解决了传统 VB 开发人员今天面临的非常现实的问题。

## VISUAL BASIC POWER PACKS

Visual Basic Power Packs 由 Microsoft 的 Visual Basic 开发团队引入，旨在在 Visual Studio 的主要版本之间为 Visual Basic 开发人员引入新功能和能力。主要重点是帮助 Visual Basic 6.0 开发人员，他们已实施了无法一蹴而就迁移到 .NET 的解决方案。存在两个问题：

- 无论你喜欢与否，原本随 .NET 1.0 一起发布的迁移向导并不能满足迁移实际应用程序的开发人员的需求。
- 一旦他们在 .NET 中工作，典型开发人员在某些任务上面临挑战，这些任务在 Visual Basic 6.0 下很容易，但在 Visual Basic .NET 中却并非如此。

