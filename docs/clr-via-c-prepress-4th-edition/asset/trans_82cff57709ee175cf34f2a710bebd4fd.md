
元数据表。例如，实现标记 0x26000001 引用 File 表的第一行。对于大多数表，行从 1 开始编号，而不是从 0 开始。对于 TypeDef 表，行实际上从 2 开始。

任何使用 MultiFileLibrary.dll 程序集类型的客户端代码都必须使用 `/r[eference]:MultiFileLibrary.dll` 编译器开关来生成。此开关告诉编译器在搜索外部类型时，加载 MultiFileLibrary.dll 程序集及其 FileDef 表中列出的所有文件。编译器要求该程序集的所有文件都已安装且可访问。如果你删除了 RUT.netmodule 文件，C# 编译器将产生以下错误：“fatal error CS0009: 无法打开元数据文件 'C:\MultiFileLibrary.dll'——导入程序集 'C:\MultiFileLibrary.dll' 的模块 'RUT.netmodule' 时出错——系统找不到指定的文件”。这意味着，要生成新的程序集，所引用程序集的所有文件都必须存在。

当客户端代码执行时，它会调用方法。首次调用某个方法时，CLR 会检测该方法作为参数、返回类型或局部变量引用的类型。然后，CLR 尝试加载包含清单的所引用程序集文件。如果要访问的类型位于此文件中，CLR 会执行其内部簿记，从而允许使用该类型。如果清单指示所引用的类型位于其他文件中，CLR 会尝试加载必要的文件，执行其内部簿记，并允许访问该类型。仅当调用某个方法，而该方法引用未加载程序集中的类型时，CLR 才会加载程序集文件。这意味着，要运行应用程序，并不需要所引用程序集的所有文件都存在。

### 使用 Visual Studio IDE 向项目添加程序集

如果你使用 Visual Studio IDE 生成项目，则必须将要引用的任何程序集添加到项目中。为此，请打开解决方案资源管理器，右键单击要添加引用的项目，然后选择“添加引用”菜单项。这将显示图 2-2 所示的“引用管理器”对话框。

```text
csc /t:module FUT.cs
al /out:MultiFileLibrary.dll /t:library FUT.netmodule RUT.netmodule
```

图 2-3 显示了创建这些语句后生成的文件。

![](img/3f2c86949cdef7e2f9e27c37c607b28e_55_0.png)

**图 2-3** 一个由三个托管模块（其中一个包含清单）组成的多文件程序集。

在此示例中，创建了两个独立的模块：RUT.netmodule 和 FUT.netmodule。这两个模块都不是程序集，因为它们不包含清单元数据表。然后生成第三个文件：MultiFileLibrary.dll，这是一个小型 DLL PE 文件（由于使用了 /t[target]:library 开关），其中不包含 IL 代码，但具有清单元数据表，指示 RUT.netmodule 和 FUT.netmodule 是程序集的一部分。生成的程序集由三个文件组成：MultiFileLibrary.dll、RUT.netmodule 和 FUT.netmodule。程序集链接器无法将多个文件合并为单个文件。

AL.exe 实用工具还可以通过使用 /t[target]:exe、/t[target]:winexe 或 /t[target]:appcontainerexe 命令行开关，生成 CUI、GUI 和 Windows 商店应用 PE 文件。但这非常不寻常，因为这意味着你会有一个 EXE PE 文件，其中只包含刚好足够的 IL 代码，用来调用另一个模块中的方法。在调用 AL.exe 时，可以通过添加 /main 命令行开关，指定模块中的哪个方法应作为入口点。以下示例演示如何使用 /main 命令行开关调用程序集链接器 AL.exe：

```text
csc /t:module /r:MultiFileLibrary.dll Program.cs
al /out:Program.exe /t:exe /main:Program.Main Program.netmodule
```

这里，第一行将 Program.cs 文件生成为 Program.netmodule 文件。第二行生成一个包含清单元数据表的小型 Program.exe PE 文件。此外，由于 /main:Program.Main 命令行开关，AL.exe 会发出一个名为 __EntryPoint 的小型全局函数。此函数 __EntryPoint 包含以下 IL 代码：

```
    .method privatescope static void __EntryPoint$PST06000001() cil managed
    {
      .entrypoint
      // Code size       8 (0x8)
      .maxstack  8
      IL_0000:  tail.
      IL_0002:  call       void [.module 'Program.netmodule']Program::Main()
      IL_0007:  ret
    } // end of method 'Global Functions'::__EntryPoint
```

如你所见，这段代码只是调用 Program.netmodule 文件中定义的 Program 类型所包含的 Main 方法。AL.exe 中的 /main 开关并不是很有用，因为你不太可能为某个应用程序创建程序集，而该应用程序的入口点却不在包含清单元数据表的 PE 文件中。我在这里提到这个开关，只是让你知道它的存在。

对于本书附带的代码，我创建了一个 Ch02-3-BuildMultiFileLibrary.bat 文件，它封装了生成多文件程序集所需的所有步骤。Visual Studio 中的 Ch02-4-AppUsingMultiFileLibrary 项目将此批处理文件作为生成前命令行步骤调用。你可以检查此项目，了解如何在 Visual Studio 中集成生成和引用多文件程序集。

### 向程序集添加资源文件

使用 AL.exe 创建程序集时，可以通过使用 /embed[resource] 开关将文件作为资源添加到程序集。此开关接受一个文件（任意文件），并将该文件的内容嵌入生成的 PE 文件中。清单的 ManifestResourceDef 表会更新，以反映这些资源的存在。

AL.exe 还支持 /link[resource] 开关，该开关也接受一个包含资源的文件。但是，/link[resource] 开关会更新清单的 ManifestResourceDef 和 FileDef 表，指示该资源存在，并标识程序集的哪个文件包含它。该资源文件不会嵌入程序集 PE 文件中；它保持独立，并且必须与其他程序集文件一起打包和部署。

与 AL.exe 类似，CSC.exe 也允许将资源合并到 C# 编译器生成的程序集中。C# 编译器的 /resource 开关会将指定的资源文件嵌入生成的程序集 PE 文件中，并更新 ManifestResourceDef 表。编译器的 /linkresource 开关会向 ManifestResourceDef 和 FileDef 清单表添加一个条目，以引用独立的资源文件。

关于资源的最后一点说明：可以将标准 Win32 资源嵌入程序集。使用 AL.exe 或 CSC.exe 时，通过 /win32res 开关指定 .res 文件的路径名，即可轻松完成此操作。此外，使用 AL.exe 或 CSC.exe 时，通过 /win32icon 开关指定 .ico 文件的路径名，即可快速轻松地将标准 Win32 图标资源嵌入程序集文件。在 Visual Studio 中，可以显示项目属性，然后单击“应用程序”选项卡，从而将资源文件添加到程序集。嵌入图标的典型原因是让 Windows 资源管理器能够为托管可执行文件显示图标。

**注意** 托管程序集文件中也包含 Win32 清单资源信息。默认情况下，C# 编译器会自动生成此清单信息，但你可以使用 /nowin32manifest 开关告诉它不要生成。C# 编译器生成的默认清单如下所示：

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
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

### 程序集版本资源信息

当 AL.exe 或 CSC.exe 生成 PE 文件程序集时，它还会将标准 Win32 版本资源嵌入到该 PE 文件中。用户可以通过查看文件属性来检查此资源。应用程序代码还可以在运行时通过调用 System.Diagnostics.FileVersionInfo 的静态 GetVersionInfo 方法，并以程序集路径名作为参数，来获取并检查此信息。图 2-4 显示了 Ch02-3-MultiFileLibrary.dll 属性对话框的“详细信息”选项卡。
