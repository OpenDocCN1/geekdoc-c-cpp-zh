

## 使用 Visual Studio IDE 将程序集添加到项目

如果你使用 Visual Studio IDE 构建项目，就必须将想要引用的所有程序集添加到项目中。为此，请打开“解决方案资源管理器”，右键单击要添加引用的项目，然后选择“添加引用”菜单项。此时会出现“引用管理器”对话框，如图 2-2 所示。

![](img/857bdf6cef9e242b53a37f88df9a1287_76_0.png)

图 2-2 Visual Studio 中的“引用管理器”对话框。

若要让项目引用某个程序集，请从列表中选择所需的程序集。如果所需程序集不在列表中，请单击“浏览”按钮，定位到所需程序集（包含清单的文件）以添加程序集引用。“解决方案”选项允许当前项目引用同一解决方案中另一个项目创建的程序集。“引用管理器”对话框中的“COM”选项允许通过 Visual Studio 自动生成的托管代理类，在托管源代码中访问非托管 COM 服务器。“浏览”选项允许你选择最近添加到另一个项目中的程序集。

若要使自己的程序集出现在“引用管理器”对话框中，请按照 http://msdn.microsoft.com/en-us/library/wkze6zky(v=vs.110).aspx 上的说明操作。

### 使用程序集链接器

除了使用 C# 编译器，你也可以使用程序集链接器工具 AL.exe 来创建程序集。如果你希望创建一个由不同编译器生成的模块组成的程序集（当你的编译器不支持与 C# 的 /addmodule 开关等效的功能时），或者只是还不确定程序集在生成时的打包需求，那么程序集链接器会很有用。你也可以使用 AL.exe 来构建仅含资源的程序集，这类程序集称为附属程序集，通常用于本地化。本章稍后会讨论附属程序集。

AL.exe 工具可以生成一个 EXE 或 DLL PE 文件，该文件只包含描述其他模块中类型的清单。为了理解 AL.exe 的工作方式，我们来改变 MultiFileLibrary.dll 程序集的构建方式。

```
csc /t:module RUT.cs
csc /t:module FUT.cs
al /out: MultiFileLibrary.dll /t:library FUT.netmodule RUT.netmodule
```

图 2-3 显示了执行这些语句后生成的文件。

![](img/857bdf6cef9e242b53a37f88df9a1287_77_0.png)

图 2-3 由三个托管模块组成的多文件程序集，其中一个模块带有清单。

在此示例中，创建了两个独立的模块：RUT.netmodule 和 FUT.netmodule。这两个模块都不是程序集，因为它们不包含清单元数据表。然后生成第三个文件：MultiFileLibrary.dll，它是一个小的 DLL PE 文件（因为使用了 /t[arget]:library 开关），不包含 IL 代码，但包含清单元数据表，表明 RUT.netmodule 和 FUT.netmodule 属于该程序集。生成的程序集由三个文件组成：MultiFileLibrary.dll，

![](img/857bdf6cef9e242b53a37f88df9a1287_80_0.png)

图 2-4 Ch02-3-MultiFileLibrary.dll 属性对话框的“详细信息”选项卡。

在构建程序集时，应使用在源代码中程序集级别应用的自定义特性来设置版本资源字段。下面就是生成图 2-4 中版本信息的代码。

```csharp
using System.Reflection;

// FileDescription version information:
[assembly: AssemblyTitle("MultiFileLibrary.dll")]

// Comments version information:
[assembly: AssemblyDescription("This assembly contains MultiFileLibrary's types")]

// CompanyName version information:
[assembly: AssemblyCompany("Wintellect")]

// ProductName version information:
[assembly: AssemblyProduct("Wintellect (R) MultiFileLibrary's Type Library")]

// LegalCopyright version information:
[assembly: AssemblyCopyright("Copyright (c) Wintellect 2013")]

// LegalTrademarks version information:
[assembly: AssemblyTrademark("MultiFileLibrary is a registered trademark of Wintellect")]

// AssemblyVersion version information:
[assembly: AssemblyVersion("3.0.0.0")]
```

| 版本资源 | AL.exe 开关 | 自定义特性/注释 |
| --- | --- | --- |
| InternalName | /out | 设置为指定的输出文件名（不含扩展名）。 |
| LegalCopyright | /copyright | System.Reflection.AssemblyCopyrightAttribute。 |
| LegalTrademarks | /trademark | System.Reflection.AssemblyTrademarkAttribute。 |
| OriginalFilename | /out | 设置为输出文件名（不含路径）。 |
| PrivateBuild | （无） | 始终为空。 |
| ProductName | /product | System.Reflection.AssemblyProductAttribute。 |
| ProductVersion | /productversion | System.Reflection.AssemblyInformationalVersionAttribute。 |
| SpecialBuild | （无） | 始终为空。 |

> **重要说明** 在 Visual Studio 中创建新的 C# 项目时，系统会自动在 Properties 文件夹中为你生成一个 AssemblyInfo.cs 文件。这个文件包含本节描述的所有程序集版本特性，以及我将在第 3 章介绍的一些附加特性。你只需打开 AssemblyInfo.cs 文件，修改程序集特定的信息即可。Visual Studio 还提供了一个对话框，可用于编辑此文件中的程序集版本信息。要查看此对话框，请在“解决方案资源管理器”中双击项目的 Properties 项，然后在“应用程序”选项卡上单击“程序集信息”；你将看到如图 2-5 所示的对话框。

![](img/857bdf6cef9e242b53a37f88df9a1287_82_0.png)

图 2-5 Visual Studio 的“程序集信息”对话框。

- **AssemblyVersion** 此版本号存储在 AssemblyDef 清单元数据表中。CLR 在绑定到强命名程序集（第 3 章讨论）时会使用此版本号。这个编号极为重要，用于唯一标识程序集。开始开发程序集时，应设置主版本号、次版本号、内部版本号和修订号，并且在准备好开始处理下一个可部署版本之前不应更改这些编号。当程序集 A 引用强命名程序集 B 时，程序集 B 的版本会嵌入到程序集 A 的 AssemblyRef 表项中。这样，当 CLR 需要加载程序集 B 时，它确切地知道程序集 A 是针对哪个版本生成和测试的。也可以通过绑定重定向（第 3 章讨论）让 CLR 加载不同版本。

### 区域性

与版本号一样，区域性也是程序集标识的一部分。例如，可以有一个专门用于德语的程序集，一个用于瑞士德语的程序集，一个用于美国英语的程序集，等等。区域性通过包含主标记和次标记的字符串来标识（如 RFC 1766 所述）。表 2-6 显示了一些示例。

**表 2-6** 程序集区域性标记示例

| 主标记 | 次标记 | 区域性 |
| --- | --- | --- |
| de | （无） | 德语 |
| de | AT | 奥地利德语 |
| de | CH | 瑞士德语 |
| en | （无） | 英语 |
| en | GB | 英式英语 |
| en | US | 美式英语 |

一般来说，如果要创建包含代码的程序集，不应为它指定区域性。这是因为代码通常不会内建任何区域性特定的假设。未指定区域性的程序集称为*区域性中立*。

如果你在设计一个包含区域性特定资源的应用程序，Microsoft 强烈建议你创建一个程序集，其中包含你的代码和应用程序的默认（或回退）资源。构建此程序集时，请不要指定区域性。其他程序集在创建和操作它公开暴露的类型时会引用这个程序集。

然后，你可以创建一个或多个独立的程序集，这些程序集只包含区域性特定的资源——完全不含代码。标有区域性的程序集称为*附属程序集*。对于这些附属程序集，请指定一个能准确反映程序集中所放置资源区域性的区域性。你应该为打算支持的每种区域性创建一个附属程序集。

