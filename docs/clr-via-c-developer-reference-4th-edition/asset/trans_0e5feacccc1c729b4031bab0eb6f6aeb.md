

ALexe 还支持一个 /link[resource] 开关，该开关也接受资源。然而，/link[resource] 开关会通过 `ManifestResourceDef` 和 `FileDef` 表更新清单文件，用以指示资源存在，并标识程序中的哪个文件包含该资源。资源文件并没有被嵌入到程序的 PE 文件中；它保持独立，并且必须与程序的其他程序文件一起打包并部署。

与 ALexe 类似，CSC.exe 也允许你通过 C# 编译器将资源组合到程序中。C# 编译器会将资源文件嵌入到生成的 PE 文件中，并更新 `ManifestResourceDef` 表。编译器的 /link[resource] 开关会在 `ManifestResourceDef` 和 `FileDef` 清单表中添加一个项，以引用独立的资源文件。

关于资源的最后一点说明：可以将 Win32 资源嵌入到程序中。你可以通过使用 ALexe 或 CSC.exe 的 /win32res 开关，并指定 .res 文件的路径来实现。此外，你还可以通过使用 ALexe 或 CSC.exe 的 /win32icon 开关，并指定 .ico 文件的路径，快速方便地将标准的 Win32 图标资源嵌入到程序中。在 Visual Studio 中，你可以通过显示项目的属性并点击“应用程序”（Application）选项卡来向程序添加资源。嵌入图标的典型目的是让 Windows 资源管理器为可执行文件找到图标。

![](img/0ce3b788d061e3d3095fa554b1a34adf_79_0.png)

托管程序集文件内部也包含了 Win32 清单资源信息。默认情况下，C# 编译器会自动生成这些信息，但你可以通过 /win32manifest 开关告诉它不要这样做。C# 编译器生成的默认清单如下所示：

```xml
<xml version="1.0" encoding="UTF-8" standalone="yes"?>
<assembly xmlns="urn:schemas-microsoft-com:asm.v1" manifestVersion="1.0">
  <assemblyIdentity version="1.0.0.0" name="MyApplication.app" />
  <trustInfo xmlns="urn:schemas-microsoft-com:asm.v2">
    <security>
      <requestedPrivileges xmlns="urn:schemas-microsoft-com:asm.v3">
        <requestedExecutionLevel level="asInvoker" uiAccess="false"/>
      </requestedPrivileges>
    </security>
  </trustInfo>
</assembly>
```

## 程序集版本资源信息

当 ALexe 或 CSC.exe 生成 PE 文件程序集时，它也会 PE 文件中嵌入一个标准的 Win32 资源版本。用户可以通过查看文件的属性来检查此资源。应用程序代码也可以在运行时调用 `System.Diagnostics.FileVersion` 的静态方法 `GetVersionInfo` 并将程序集路径作为参数，获取并检查此信息。图 2-4 显示了 Ch02-3-MultiLibrary.dll 属性框的详情。

## Ch02-3-MultiFileLibrary.dll 属性

| 属性 | 值 |
|---|---|
| 文件描述 (File description) | MultiFileLibrary.dll |
| 类型 (Type) | 应用程序扩展名 |
| 文件版本 (File version) | 1.0.0 |
| 产品名称 (Product name) | Winterlect (R) MultiFileLibrary's Type Lib... |
| 产品版本 (Product version) | 2.0.0 |
| 版权 (Copyright) | Copyright (c) Winterlect 2013 |
| 大小 (Size) | 5.00 KB |
| 修改日期 (Date modified) | 中立 |
| 法律商标 (Legal trademarks) | MultiFileLibrary is a registered trademark... |
| 原始文件名 (Original filename) | Ch02-3-MultiFileLibrary.dll |

图 2-4 Ch02-3-MultiFileLibrary.dll 属性对话框的“详细信息”选项卡。

构建程序集时，你应该通过在源代码中应用于程序集级别的自定义性性来设置版本资源字段。以下是生成图 2-4 中版本信息的代码样式。

```csharp
using System.Reflection;

// FileDescription 版本信息:
[assembly:AssemblyTitle("MultiFileLibrary.dll")];

// Comments 版本信息:
[assembly:AssemblyDescription("This assembly contains MultiFileLibrary's types")];

// CompanyName 版本信息:
[assembly:AssemblyCompany("Winterlect")];

// ProductName 版本信息:
[assembly:AssemblyProduct("Winterlect (R) MultiFileLibrary's Type Library")];

// LegalCopyright 版本信息:
[assembly:AssemblyCopyright("Copyright (c) Winterlect 2013")];

// LegalTrademarks 版本信息:
[assembly:AssemblyTrademark("MultiFileLibrary is a registered trademark of Winterlect")];

// AssemblyVersion 版本信息:
[assembly:AssemblyVersion("3.0.0.0")];

// FILEVERSION/FileVersion 版本信息:
[assembly:AssemblyFileVersion("1.0.0.0")];

// PRODUCTVERSION/ProductVersion 版本信息:
[assembly:AssemblyInformationalVersion("2.0.0.0")];

// 设置语言 字段（稍后在“文化”部分中讨论）
[assembly:AssemblyCulture("")];
```

> 重要：遗憾的是，Windows 资源管理器属性对话框缺少了某些属性的条目。特别是，如果能显示 AssemblyVersion 属性的值将就太棒了，因为 CLR 在加载程序集时会使用此值，我们将在第 3 章中讨论。

表 2-4 显示了版本资源字段及其对应的自定义属性。如果你使用 Alexe 构建你的程序集，可以使用命令行开关来设置这些信息，而不是使用自定义属性。

表 2-4 的第二列显示了与每个版本对应的 Alex 命令行开关。

| 版本字段 | Alex 开关 | 自定义属性 |
|---|---|---|
| FILEVERSION | /fileversion | AssemblyFileVersion |
| PRODUCTVERSION | /productversion | AssemblyInformationalVersion |

