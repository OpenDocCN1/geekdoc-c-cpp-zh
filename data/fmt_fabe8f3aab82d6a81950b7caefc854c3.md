
本附录中列出的一些选项旁边带有加号 (`+`) 或减号 (`-`)。加号表示应启用该选项，而减号表示不应启用该选项。例如，以下命令表示应启用文档：

```
vbc.exe MyModule.vb /reference:Microsoft.VisualBasic.dll /doc+
```

而以下命令则表示不应启用文档：

```
vbc.exe MyModule.vb /reference:Microsoft.VisualBasic.dll /doc-
```

## 编译器选项

本节全面介绍 Visual Basic 编译器可用的选项。要查看完整列表，请键入以下命令：

```
vbc.exe /?
```

## 输出文件

以下各节将解释输出文件。

### `/doc[+|-]`

默认情况下，编译器在编译时不会生成 XML 文档文件。Visual Basic 的此功能使开发人员能够在代码中添加结构化注释，然后可以将其转换为便于查看的 XML 文档（配合样式表使用）。包含 `/doc` 选项会使编译器创建此文档。如果要生成此 XML 文档文件，请按如下方式构造命令：

```
vbc.exe MyModule.vb /doc
```

您还可以按如下方式指定 XML 文件的名称：

```
vbc.exe MyModule.vb /doc:MyModuleXmlFile.xml
```

### `/out`

使用 `/out` 选项可以更改编译生成文件的名称和扩展名。默认情况下，它采用包含 Main 过程的文件名，或 DLL 中第一个源代码文件的名称。如果您想自行修改而不是使用默认名称，可以使用类似于以下内容的命令：

```
vbc.exe MyModule.vb /out:MyReallyCoolModule.exe
```

### `/target`

此设置允许您指定编译过程的确切输出内容。有四个选项：EXE、DLL、模块或 Windows 程序：

- `/target:exe` — 生成可执行的控制台应用程序。如果未指定 `/target` 选项，则这是默认设置。
- `/target:library` — 生成动态链接库（也称为 DLL）
- `/target:module` — 生成模块
- `/target:winexe` — 生成 Windows 程序

您还可以使用简短形式，只需使用 `/t:exe`、`/t:library`、`/t:module` 或 `/t:winexe`。

## 输入文件

以下各节将解释输入文件。

### /addmodule

此选项在 Visual Studio 中不可用，但在使用 Visual Basic 编译器时可以使用。使用 `/addmodule` 可以将 `.netmodule` 文件添加到编译器的输出结果中。在以下示例中，`MyOtherModule.netmodule` 是一个文件名。您可以附加一个或多个模块文件。模块文件与程序集并不完全相同，因为它们是专门使用 `/target:module` 选项编译的，该选项会创建一个适合作为其他编译的一部分包含在内的 netmodule 文件。使用 `/addmodule` 的示例如下所示：

```
vbc.exe MyModule.vb /addmodule:MyOtherModule.netmodule
```

### /link

这使您可以引用指定互操作程序集中的元数据。由于 .NET 4 支持无主互操作程序集 (PIA) 功能，您需要在编译时链接相应的互操作程序集。使用此选项可在编译期间将 PIA 元数据链接到程序集中，这样部署时就无需相关的互操作程序集。它可以缩写为 `/l`。

```
vbc.exe MyModule.vb /l:COMponent.dll
```

### /recurse

`/recurse` 选项告诉编译器编译指定目录中的所有指定文件。同时还会包含所指定目录的所有子目录。以下是使用 `/recurse` 的一个示例：

```
vbc.exe /target:library /out:MyComponent.dll /recurse:MyApplication\Classes\*.vb
```

此命令获取 `MyApplication/Classes` 目录及其子目录中的所有 `.vb` 文件，并创建一个名为 `MyComponent.dll` 的 DLL。

### /reference

`/reference` 选项允许您在编译过程中引用其他程序集。用法如下：

```
vbc.exe MyModule.vb /reference:MyAssembly.dll
```

您也可以仅使用 `/r` 来简化命令选项：

```
vbc.exe MyModule.vb /r:MyAssembly.dll
```

您可以通过逗号分隔来引用多个程序集：

```
vbc.exe MyModule.vb /reference:MyAssembly.dll, MyOtherAssembly.dll
```

## 资源

以下各节将详细说明编译器中的资源。

### /linkresource

`/linkresource` 选项不是将资源直接嵌入生成的输出文件中（例如使用 `/resource` 选项时那样），而是使您能够在输出文件与其所需的资源之间建立连接。您可以按以下方式使用此选项：

```
vbc.exe MyModule.vb /linkresource:MyResourceFile.res
```

你可以指定程序集清单中的资源文件是公共的还是私有的。默认情况下，资源文件被引用为公共资源。以下是一个使用示例：

```
vbc.exe MyModule.vb /linkresource:MyResourceFile.res,private
```

你可以将 `/linkresource` 选项简写为 `/linkres`。

## /resource

`/resource` 选项允许你引用托管资源对象。引用的资源随后会被嵌入到程序集中。你可以通过以下方式进行操作：

```
vbc.exe MyModule.vb /resource:MyResourceFile.res
```

与 `/linkresource` 选项类似，你可以指定对资源的引用是公共的还是私有的。操作方式如下（默认为公共）：

```
vbc.exe MyModule.vb /resource:MyResourceFile.res,private
```

你可以将 `/resource` 选项简写为 `/res`。

## /win32icon

使用此选项可将 `.ico` 文件（即应用程序图标的图像）嵌入生成的文件中，如下例所示：

```
vbc.exe MyModule.vb /win32icon:MyIcon.ico
```

## /win32resource

此选项允许你将 Win32 资源文件嵌入生成的文件中。用法如下例所示：

```
vbc.exe MyModule.vb /win32resource:MyResourceFile.res
```

## 代码生成

以下各节介绍可用于代码生成的选项。

## /debug[+/-]

默认情况下，Visual Basic 编译器生成的对象不会包含附加的调试信息。使用 `/debug` 选项可使编译器将此信息放入生成的输出文件中。此外，你可以选择调试完整（默认）或仅生成 PDB 文件。此选项的用法如下所示：

```
vbc.exe MyModule.vb /debug
vbc.exe MyModule.vb /debug:full
vbc.exe MyModule.vb /debug:pdbonly
```

## /optimize[+/-]

如果你打开项目的属性页（在 Visual Studio 解决方案资源管理器中右键单击项目即可找到），你会看到编译设置页面。在此页面中，你可以进行各种编译优化。为了避免命令行编译器忽略这些设置，请在编译指令中设置 `/optimize` 标志：

```
vbc.exe MyModule.vb /optimize
```

默认情况下，优化是关闭的。

## /removeintchecks[+/-]

默认情况下，Visual Basic 编译器会检查所有整数计算是否可能出错。可能的错误包括除以零或溢出情况。使用 `/removeintchecks` 选项可使编译器不在所编译文件的代码中查找这类错误。你可以按如下方式使用此选项：

```
vbc.exe MyModule.vb /removeintchecks
```

## 错误和警告

## /nowarn

`/nowarn` 选项实际上会禁止编译器发出任何警告。此选项有几种用法。第一种是直接使用不带任何关联值的 `/nowarn`：

```
vbc.exe MyModule.vb /nowarn
```

除了禁止编译器可能发出的所有警告之外，你还可以指定希望编译器抑制的确切警告，如下所示：

```
vbc.exe MyModule.vb /nowarn:42016
```

在这种情况下，你是在告诉编译器在遇到 42016 错误（隐式转换警告错误）时不要发出任何警告。如果要插入多个警告代码，请用逗号分隔警告代码，如下所示：

```
vbc.exe MyModule.vb /nowarn:42016, 42024
```

你可以在 MSDN 文档中搜索“在 Visual Basic 中配置警告”来查找可用警告列表。

## /warnaserror[+-]

除了发现和报告错误之外，编译器还可能遇到仅被视为警告的情况。即使遇到警告，编译过程仍会继续。在编译过程中使用 `/warnaserror` 选项会使编译器将所有警告视为错误。按如下所示使用此选项：

```
vbc.exe MyModule.vb /warnaserror
```

你可能不希望每个警告都导致抛出错误，而只希望某些特定警告。对于这些情况，你可以指定需要注意的警告 ID 号，如下所示：

```
vbc.exe MyModule.vb /warnaserror:42016
```

你也可以通过用逗号分隔警告 ID 号来检查多个警告：

```
vbc.exe MyModule.vb /warnaserror:42016, 42024
```

## 语言

以下各节详细介绍 Visual Basic 语言特定的选项。

## /define

`/define` 选项允许你为编译过程定义条件编译器常量。这很像在代码中使用 `#Const` 指令。以下是一个示例：

```
vbc.exe MyModule.vb /define:Version="4.11"
```

此选项可以简写为 `/d`。你也可以为多个常量设置定义，如下所示：

```
vbc.exe MyModule.vb /d:Version="4.11",DebugMode=False
```

对于多个常量，只需用逗号分隔各常量即可。

## /imports

`/imports` 是一个常用的编译器选项，它允许你在编译过程中导入命名空间：

```
vbc.exe MyModule.vb /imports:System
```

用逗号分隔多个命名空间来添加它们：

```
vbc.exe MyModule.vb /imports:System, System.Data
```

## /langversion

此选项允许你指定语言版本。该版本基于 Visual Basic 版本，而不是 .NET 版本。例如，.NET 4 附带 Visual Basic 10。

```
vbc.exe MyModule.vb /langversion:10
```

## /optionexplicit[+:-]

使用 `/optionexplicit` 始终是个好主意，它会让编译器检查代码中是否有变量在声明之前就被使用（是的，这种情况是可能的，而且是非常糟糕的做法）。使用此设置后，当发现变量在声明之前就被使用时，编译器会抛出错误。默认情况下，编译器不会使用 `/optionexplicit` 选项检查代码。请按以下示例使用此选项：

```
vbc.exe MyModule.vb /optionexplicit
```

## /optionstrict[+:-]

在编译过程中使用 `/optionstrict` 选项也是一个好主意。使用此选项会使编译器检查你是否在代码中进行了任何不正确的类型转换。允许扩大类型转换，但当你开始执行缩小类型转换时，使用此选项将导致编译器抛出错误。默认情况下，编译器不会检查类型转换中的这类错误。请按如下方式使用此选项：

```
vbc.exe MyModule.vb /optionstrict
```

## /optioncompare

默认情况下，Visual Basic 编译器使用二进制比较来比较字符串。如果你希望字符串比较使用文本比较，请使用以下构造：

```
vbc.exe MyModule.vb /optioncompare:text
```

## /optioninfer[+:-]

这是 .NET Framework 3.5 版编译器新增的选项，用于指定允许对变量进行类型推断。请按以下示例使用此选项：

```
vbc.exe MyModule.vb /optioninfer
```

## /rootnamespace

使用此选项指定用于编译的命名空间：

```
vbc.exe MyClass.vb /rootnamespace:Reuters
```

## 其他功能

本附录的其余部分介绍了编译器中其他一些非常有用的功能。

## /?

当你手边没有这本书可供参考时，可以使用 `/?` 选项从 Visual Basic 编译器获取选项列表，如下所示：

```
vbc.exe /?
```

这将在命令窗口中显示完整的选项列表及其定义。

## /help

`/help` 选项与 `/?` 选项相同。这两个选项都会产生相同的结果：一个可用于编译器的选项列表。

## /noconfig

默认情况下，Visual Basic 编译器在编译过程中使用 `vbc.rsp` 资源文件。使用 `/noconfig` 选项可告知编译器在编译过程中不要使用此文件，如下所示：

```
vbc.exe MyClass.vb /noconfig
```

## /nologo

此选项使编译器在执行编译时不生成前面示例中显示的编译器信息集。这实际上只在以下情况下有用：你在应用程序中调用编译器、将生成的结果显示给最终用户，并且不希望这些信息显示在结果集中。

## /quiet

与其他一些编译器选项一样，`/quiet` 选项只适用于命令行编译器；在使用 Visual Studio 编译应用程序时不可用。`/quiet` 选项会从通常生成的错误文本输出中移除部分错误通知。通常，当编译器遇到阻止进一步编译的错误时，错误通知会包含文件中出错的那一行代码。所显示的代码行在出错的确切代码下方有一条波浪线。使用 `/quiet` 选项后，编译器只显示通知行，而不在输出中显示代码行。在某些情况下，这可能是可取的。

## /verbose

添加此命令会使编译器输出其正在执行的操作的完整列表，包括正在加载的程序集以及在编译过程中收到的错误。用法如下：

```
vbc.exe MyModule.vb /reference:Microsoft.VisualBasic.dll /verbose
```

这将产生类似下面的结果（由于输出结果相当长，这里做了缩写）：

```
Adding assembly reference 'C:\WINDOWS\Microsoft.NET\Framework\v4.0.*\System.Data.dll'
```

此外：

```
Adding import 'System'
Adding import 'Microsoft.VisualBasic'
Adding file 'C:\MyModule.vb'
Adding assembly reference 'C:\WINDOWS\Microsoft.NET\Framework\v4.0.*\Microsoft.VisualBasic.dll'
Compiling...
```

然后编译器开始加载程序集……

```
Loading C:\WINDOWS\Microsoft.NET\Framework\v4.0.*\mscorlib.dll.
Loading C:\WINDOWS\Microsoft.NET\Framework\v4.0.*\Microsoft.VisualBasic.dll.
```

……直到完成：

```
Building 17d14f5c-a337-4978-8281-53493378c1071.vb.
Building C:\CoolStuff\MyModule.vb.
Compilation successful
```

## 高级功能

以下各节讨论可用的优化和其他高级功能。

## /baseaddress

使用 `/target:library` 选项创建 DLL 时，可以指定 DLL 的基地址。默认情况下，编译器会为您完成此操作，但如果您希望自行指定，也可以这样做。要实现此目的，您可以使用类似以下内容：

```
vbc.exe MyClass.vb /target:library /baseaddress:0x11110000
```

所有基地址均指定为十六进制数字。

## /bugreport

`/bugreport` 选项会创建一个文件，其中包含编译过程的完整报告。此文件包含您的代码以及计算机操作系统和编译器本身的版本信息。使用此选项的方式如下：

```
vbc.exe MyModule.vb /bugreport:bugsy.txt
```

## /codepage

默认情况下，编译器期望所有文件都使用 ANSI、Unicode 或 UTF-8 代码页。使用编译器的 `/codepage` 选项，您可以指定编译器实际应使用的代码页。将其设置为默认值之一的示例如下所示：

```
vbc.exe MyClass.vb /codepage:1252
```

1252 用于美式英语和大多数欧洲语言，尽管将其设置为日文假名也同样简单：

```
vbc.exe MyClass.vb /codepage:932
```

## /delaysign[+-:]

此编译器选项需要与 `/key` 或 `/keycontainer` 选项结合使用，后者处理程序集的签名。当与 `/delaysign` 选项一起使用时，编译器会为数字签名创建空间以供以后对程序集进行签名，而不是在此时实际签名程序集。您可以使用以下方式使用此选项：
