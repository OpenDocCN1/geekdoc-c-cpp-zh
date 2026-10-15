
您的应用程序可以使用 .NET 3.0、.NET 3.5 或 .NET 4。为了在编译器层面充分利用此目标框架功能，您需要确保库引用与您打算支持的框架目标相匹配。如果引用了 WPF 之类的库，却试图支持 .NET 2.0，那是行不通的。

<supportedRuntime> 元素适用于 .NET Framework 1.1 及更高版本。如果打算使用 .NET Framework 1.0，则应使用 <requiredRuntime> 元素。

<supportedRuntime> 元素包含两个可能的属性：version 和 safemode。这两个属性都是可选的。version 属性允许您指定应用程序要运行所针对的特定版本，而 safemode 则指定是否应在注册表中搜索特定的框架版本。safemode 属性采用布尔值，默认值为 false，表示不检查框架版本。

最后请注意，为了利用此设置，您需要针对这些不同的 .NET 版本测试您的应用程序。

## 编译的简单步骤

为了以最简单的方式展示 Visual Basic 编译器的工作原理，我们可以先看看如何编译单个类文件：

- 1. 创建一个名为 MyModule.vb 的模块文件。我们会让此模块保持简单，因为本示例旨在向您展示如何使用 vbc.exe 编译器编译这些项：

```
Module Module1
    Sub Main()
        Console.WriteLine("Howdy there")
        Console.ReadLine()
    End Sub
End Module
```

- 2. 文件就位后，就可以使用 Visual Basic 编译器了。如果您的计算机上装有 Visual Studio，则可以打开 Visual Studio 命令提示符（位于“开始 ▸ 所有程序 ▸ Microsoft Visual Studio 2010 ▸ Visual Studio 工具 ▸ Visual Studio 命令提示符(2010)”）。打开后，只需导航到文件所在位置，然后对文件运行编译器（稍后演示）。

- 3. 在大多数情况下，您可能会在没有安装 Visual Studio 的计算机上使用 Visual Basic 编译器。在这种情况下，一种选择是将 vbc.exe、vbc.exe.config 和 vbc.rsp 文件复制并粘贴到您要编译的类文件所在的文件夹中。然后，您可以通过从“开始”菜单中选择“运行”并在文本框中输入 cmd 来打开命令提示符。另一种选择是将编译器添加到 path 本身。为此，请在命令提示符下输入以下内容：

```
path %path%;C:\WINDOWS\Microsoft.NET\Framework\v4.0.*
Now you can work with the compilation normally, and the vbc.exe compiler will be found upon compilation. Yet another option is to work from the Windows folder, using an explicit reference to the file to be compiled. However, this option is frowned upon, as you are likely to start creating project-specific files within your .NET Framework folder hierarchy.
```

- 4. 命令提示符打开后，导航到包含需要编译的类文件的文件夹。在此位置，于命令提示符下输入以下命令：

```
vbc.exe MyModule.vb
```

使用 Visual Basic 编译器可以通过多种方式编译项，但这是编译此模块的最简单方式。此命令会编译该 .vb 文件，以便您的应用程序可以使用它。运行上述命令会产生以下结果：

```
C:\CoolStuff>vbc.exe MyModule.vb
Microsoft (R) Visual Basic Compiler version 10.0.*
Copyright (c) Microsoft Corporation.  All rights reserved.
```

此操作实际上做了什么？在本例中，它在 `MyModule.vb` 文件所在的同一目录中为您创建了一个 `.exe` 文件。查看该目录，您会发现 `MyModule.exe` 已准备好运行。

Visual Basic 编译器有许多选项，可让您指定编译器在编译过程中执行哪些操作。稍后将定义这些标志，但您可以通过使用正斜杠，后跟选项名称以及分配给该选项的设置，来指定其他设置。例如，如果要在编译时添加对 `Microsoft.VisualBasic.dll` 的引用，可以按如下方式构建编译器命令：

```
vbc.exe MyModule.vb /reference:Microsoft.VisualBasic.dll
```

本附录中列出的一些选项旁边带有加号 (+) 或减号 (-)。加号表示应启用该选项，而减号表示不应启用该选项。例如，以下命令表示应启用文档：

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

您还可以使用简短形式，只需使用 /t:exe、/t:library、/t:module 或 /t:winexe。

## 输入文件

以下各节将解释输入文件。

### /addmodule

此选项在 Visual Studio 中不可用，但在使用 Visual Basic 编译器时可以使用。使用 /addmodule 可以将 .netmodule 文件添加到编译器的输出结果中。在以下示例中，MyOtherModule.netmodule 是一个文件名。您可以附加一个或多个模块文件。模块文件与程序集并不完全相同，因为它们是专门使用 /target:module 选项编译的，该选项会创建一个适合作为其他编译的一部分包含在内的 netmodule 文件。使用 /addmodule 的示例如下所示：

```
vbc.exe MyModule.vb /addmodule:MyOtherModule.netmodule
```

### /link

这使您可以引用指定互操作程序集中的元数据。由于 .NET 4 支持无主互操作程序集 (PIA) 功能，您需要在编译时链接相应的互操作程序集。使用此选项可在编译期间将 PIA 元数据链接到程序集中，这样部署时就无需相关的互操作程序集。它可以缩写为 /l。

```
vbc.exe MyModule.vb /l:COMponent.dll
```

### /recurse

/recurse 选项告诉编译器编译指定目录中的所有指定文件。同时还会包含所指定目录的所有子目录。以下是使用 /recurse 的一个示例：

```
vbc.exe /target:library /out:MyComponent.dll /recurse:MyApplication\Classes\*.vb
```

此命令获取 MyApplication/Classes 目录及其子目录中的所有 .vb 文件，并创建一个名为 MyComponent.dll 的 DLL。

### /reference

/reference 选项允许您在编译过程中引用其他程序集。用法如下：

```
vbc.exe MyModule.vb /reference:MyAssembly.dll
```

您也可以仅使用 /r 来简化命令选项：

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

/linkresource 选项不是将资源直接嵌入生成的输出文件中（例如使用 /resource 选项时那样），而是使您能够在输出文件与其所需的资源之间建立连接。您可以按以下方式使用此选项：

```
vbc.exe MyModule.vb /linkresource:MyResourceFile.res
```

