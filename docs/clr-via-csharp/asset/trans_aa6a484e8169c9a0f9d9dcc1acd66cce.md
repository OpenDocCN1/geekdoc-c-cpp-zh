
公钥的大小使其难以使用。为了让开发人员（以及最终用户）更方便，创建了 *公钥标记*。公钥标记是公钥的 64 位哈希。`SN.exe` 的 `-tp` 开关会在其输出末尾显示与完整公钥对应的公钥标记。

既然你已经知道如何创建公钥/私钥对，创建强命名程序集就很简单了。编译程序集时，使用 `/keyfile:<file>` 编译器开关：

```text
csc /keyfile:MyCompany.snk Program.cs
```

当 C# 编译器看到此开关时，编译器会打开指定的文件（MyCompany.snk），用私钥对程序集签名，并将公钥嵌入清单中。请注意，你只对包含清单的程序集文件进行签名；程序集的其他文件无法显式签名。

如果你使用的是 Visual Studio，可以通过显示项目属性、单击“签名”选项卡、选中“对程序集签名”复选框，然后从“选择强名称密钥文件”组合框中选择 `<New...>` 选项来创建新的公钥/私钥文件。

下面解释对文件进行签名的含义：当你生成强命名程序集时，程序集的 FileDef 清单元数据表会包含组成该程序集的所有文件的列表。当每个文件的名称被添加到清单中时，会计算文件内容的哈希值，并且该哈希值会与文件名一起存储在 FileDef 表中。你可以使用 `AL.exe` 的 `/algid` 开关覆盖默认使用的哈希算法，或者在程序集的某个源代码文件中应用程序集级的 `System.Reflection.AssemblyAlgorithmIdAttribute` 自定义特性。默认情况下，使用 SHA-1 算法，这对于几乎所有应用程序来说都应该足够了。

在生成包含清单的 PE 文件之后，会对该 PE 文件的全部内容（除了任何 Authenticode 签名、程序集的强名称数据以及 PE 头校验和）进行哈希计算，如图 3-1 所示。这里使用的哈希算法始终是 SHA-1，且无法覆盖。此哈希值会用发布者的私钥签名，生成的 RSA 数字签名会存储在 PE 文件内的一个保留节中（不包含在哈希中）。PE 文件的 CLR 头会被更新，以反映数字签名嵌入在文件中的位置。

```text
AssemblyRef #1 (23000001)
---------------------------------------
Token: 0x23000001
Public Key or Token: b7 7a 5c 56 19 34 e0 89
Name: mscorlib
Version: 4.0.0.0
Major Version: 0x00000004
Minor Version: 0x00000000
Build Number: 0x00000000
Revision Number: 0x00000000
Locale: <null>
HashValue Blob:
Flags: [none] (00000000)
```

由此可以看出，JeffTypes.dll 引用了一个类型，该类型包含在匹配以下属性的程序集中：

> "MSCorLib, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"

不幸的是，ILDasm.exe 使用了 *区域设置* 这一术语，而实际上它应该使用 *区域性*。

如果你查看 JeffTypes.dll 的 AssemblyDef 元数据表，会看到以下内容：

```text
Assembly
---------------------------------------
Token: 0x20000001
Name : JeffTypes
PublicKey :
Hash Algorithm : 0x00008004
Version: 3.0.0.0
Major Version: 0x00000003
Minor Version: 0x00000000
Build Number: 0x00000000
Revision Number: 0x00000000
Locale: <null>
Flags : [none] (00000000)
```

这等价于以下内容：

> "JeffTypes, Version=3.0.0.0, Culture=neutral, PublicKeyToken=null"

在这一行中，没有指定公钥标记，因为第 2 章中的 JeffTypes.dll 程序集并未使用公钥/私钥对签名，因此它是一个弱命名程序集。如果我曾使用 SN.exe 创建密钥文件，并使用 **/keyfile** 编译器开关进行编译，那么生成的程序集就会被签名。如果我随后使用 ILDasm.exe 查看新程序集的元数据，AssemblyDef 条目中 PublicKey 字段之后会出现字节，并且该程序集将是强命名程序集。顺便说一句，AssemblyDef 条目始终存储完整的公钥，而不是公钥标记。完整的公钥是确保文件未被篡改所必需的。本章后面我会解释强命名程序集的防篡改能力。

```text
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

如你所见，你可以调用 GACUtil.exe，指定 /i 开关将程序集安装到 GAC 中，也可以使用 GACUtil.exe 的 /u 开关从 GAC 中卸载程序集。请注意，永远不能将弱命名程序集放入 GAC。如果将弱命名程序集的文件名传递给 GACUtil.exe，它会显示以下错误消息：“将程序集添加到缓存失败：尝试安装没有强名称的程序集。”

> **注意** 默认情况下，只有属于 Windows 管理员组的用户才能操作 GAC。如果调用该实用工具的用户不是此组的成员，GACUtil.exe 将无法安装或卸载程序集。

使用 GACUtil.exe 的 /i 开关对开发人员测试非常方便。然而，如果你在生产环境中使用 GACUtil.exe 部署程序集，建议除了指定 /i 或 /u 开关来安装或卸载程序集之外，还使用 GACUtil.exe 的 /r 开关。/r 开关会将程序集与 Windows 安装和卸载引擎集成。基本上，它会告诉系统哪个应用程序需要该程序集，然后将应用程序和程序集绑定在一起。

> **注意** 如果强命名程序集打包在 cabinet（.cab）文件中或以某种方式压缩，则必须先将该程序集文件解压缩到临时文件，然后才能使用 GACUtil.exe 将程序集文件安装到 GAC 中。一旦程序集文件安装完成，就可以删除临时文件。

GACUtil.exe 工具不会随最终用户 .NET Framework 可再发行包一起提供。如果你的应用程序包含一些想要部署到 GAC 中的程序集，则应使用 Windows Installer (MSI)，因为 MSI 是唯一保证存在于最终用户计算机上并且能够将程序集安装到 GAC 中的工具。

> **重要** 将程序集文件全局部署到 GAC 是对程序集进行注册的一种形式，尽管实际的 Windows 注册表不会受到任何影响。将程序集安装到 GAC 会破坏简单应用程序安装、备份、还原、移动和卸载的目标。因此，建议避免全局部署，并尽可能使用私有部署。

在 GAC 中“注册”程序集的目的是什么？假设有两家公司各自生成一个 OurLibrary 程序集，该程序集由一个文件组成：OurLibrary.dll。显然，这两个文件不能放在同一目录中，因为后安装的文件会覆盖先安装的文件，这肯定会导致某个应用程序无法正常工作。当你将程序集安装到 GAC 中时，会在 C:\Windows\Assembly 目录下创建专用子目录，并将程序集文件复制到其中一个子目录中。

通常没有人会检查 GAC 的子目录，因此 GAC 的结构对你来说并不重要。只要工具和 CLR 知道该结构，一切就都没问题。

## 生成引用强命名程序集的程序集

每当你生成一个程序集时，该程序集都会引用其他强命名程序集。这是真的，因为 System.Object 定义在 MSCorLib.dll 中，而该文件是强命名的。然而，程序集很可能会引用由 Microsoft、第三方或你自己的组织发布的其他强命名程序集中的类型。在第 2 章中，我展示了如何使用 CSC.exe 的 /reference 编译器开关来指定要引用的程序集文件名。如果文件名是完整路径，CSC.exe 会加载指定的文件，并使用其元数据信息来生成程序集。如第 2 章所述，如果指定的文件名不带路径，CSC.exe 会尝试按以下目录顺序（按此处列出的顺序）查找程序集：

- 1. 工作目录。
- 2. 包含 CSC.exe 文件本身的目录。此目录还包含 CLR DLL。
- 3. 使用 /lib 编译器开关指定的任何目录。
- 4. 使用 LIB 环境变量指定的任何目录。

因此，如果你要生成一个引用 Microsoft 的 System.Drawing.dll 的程序集，可以在调用 CSC.exe 时指定 /reference:System.Drawing.dll 开关。编译器将检查前面列出的目录，并在包含 CSC.exe 文件本身的目录中找到 System.Drawing.dll 文件；该目录与包含编译器所绑定 CLR 版本的 DLL 的目录相同。尽管这是编译时找到程序集的目录，但它并不是运行时加载程序集所在的目录。

