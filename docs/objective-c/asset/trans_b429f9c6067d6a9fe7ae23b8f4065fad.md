

## 将源代码转换为编译代码，再将编译代码转换为可执行文件

创建好源代码之后，你需要让计算机将源代码转换为它可以执行的指令。这个过程的一部分被称为编译源代码。

编译源代码实际上涉及多个步骤。

第一步称为预处理。你可以将预处理步骤理解为计算机为编译你的代码做准备。在此步骤中，编译器会移除任何不会生成可执行代码的内容，例如注释等。它还会展开部分代码并重新排列某些指令，以便编译过程的第二步能够更高效。编译第一步的最终结果是源代码的一种中间状态。你通常不会看到或处理这种中间形式的代码，不过有一些编译器开关可以让你在出于任何原因想查看输出时，让编译在此阶段停止。一些使用高级技术的开发者有时会利用这些编译器开关，以便查看中间文件并确切了解编译器在做什么。在正常的应用程序开发中，你可能永远不需要这样做。

预处理之后，第二步是编译器真正将源代码转换为所谓的对象文件（object file）。对象文件的扩展名为 `.o`。编译源代码可能是一个相对漫长的过程，涉及许多不同的模块和许多不同的源代码文件。因此，如果某个模块及其所有依赖项都没有发生变化，而你可以避免重新构建该模块，那么在减少编译时间方面将是一个很大的优势。正因为如此，对象文件通常存储在构建目录的磁盘上。如果某个源代码文件自上次运行编译器以来没有更改，编译器就可以直接跳过对该源代码的重新编译，转而重用上次运行编译器时留下的对象文件。通常，你在日常使用中不需要查看这些文件。它们仅供编译器使用。

编译的最后一步涉及一个称为链接（linking）的过程。链接意味着将上一步生成的对象文件连接在一起，形成一个可执行文件。除了对象文件本身之外，库和框架也会被链接到可执行文件中。链接过程的最终结果就是你的实际应用程序可执行文件。对于命令行应用程序而言，这将是一个可以从命令行运行的单一二进制文件。对于桌面应用程序而言，这通常是一个所谓的应用程序包（application bundle），实际上是一个包含可执行文件以及运行应用程序所需的所有资源（如图形、声音等）的磁盘目录。你将在下一节中了解更多关于应用程序包的内容。

在 Xcode 中，编译你的应用程序只需点击“构建并运行”（Build and Run）按钮即可。如果你在示例项目上这样做，它会在控制台中启动应用程序并显示其输出。同时，Xcode 会切换到调试模式，并允许你对应用程序进行调试。调试是一个高级 IDE 主题；有关如何使用它进行调试的信息，请参阅 Xcode 文档。

编译过程的最终结果就是你的可执行文件。如果在任何时刻编译器在你的源代码中检测到错误，它会停止处理该文件并向你显示错误，以便你进行修正。遗憾的是，编译器相当挑剔。计算机在从文字中推断含义方面远不如我们。因此，编译器不会猜测你原本想输入什么，而是直接放弃并显示错误。这些错误可能简单到缺少分号、缺少空格、大小写错误，或任何数量的小问题。做好准备——当你走上程序员这条职业道路后，你每天都会遇到这样的错误，即使没有成千上万次，也会有数百次。即使是最优秀的程序员，也很少能写出第一次就能完美编译的代码。

## 探索应用程序包

在上一节中，我提到了“应用程序包”这个术语——即使你是一位经验丰富的程序员，这对你来说也可能是一个全新的术语。你可能想知道它是什么。应用程序包实际上更像是操作系统层面的构造，而不是 Objective-C 的构造。Objective-C 语言本身并不要求也不生成应用程序包。尽管如此，应用程序包在几乎所有可以使用 Objective-C 的平台上都是编程中重要且不可或缺的概念，因此，作为 Objective-C 程序员，理解它们对你来说是很重要的概念。

应用程序包就是磁盘上的一个目录，其中包含一组文件。在 Mac OS X 中，应用程序包用于将应用程序运行所需的全部文件分组在一起。这包括可执行文件、图形、声音文件和用户界面资源等项目。此外，在构建 Mac OS X 图形应用程序时，用户界面定义通常是在一个名为 Interface Builder 的应用程序中完成的。该应用程序也会生成称为 NIB 文件的包。NIB 文件通常具有 `.nib` 扩展名，并存储在应用程序包内部。

### 注意

NIB 代表 NeXTstep Interface Builder，是从 NeXT 时代遗留下来的。最近，格式从二进制变为 XML，文件扩展名也从 `.nib` 改成了 `.xib`。在编译期间，XIB 文件仍然会被编译成 NIB 文件，因此当你查看应用程序包时，你会看到 `.nib` 而不是 `.xib`。

清单 1.3 显示了一个典型的应用程序包目录结构。在这个例子中，它是 Xcode 应用程序包的部分列表。

### 应用程序包的内容

```
Xcode.app
`-- Contents
|--- CodeResources -> _CodeSignature/CodeResources
|--- Info.plist
|--- Library
|   `-- QuickLook
|       `-- SourceCode.qlgenerator
|           `-- Contents
|           |--- CodeResources -> _CodeSignature/CodeResources
|           |--- Info.plist
|           |--- MacOS
|           |   `-- SourceCode
|           |--- _CodeSignature
|           |   `-- CodeResources
|           `-- version.plist
|   `-- Spotlight
|       |--- SourceCode.mdimporter
|       |   `-- Contents
|       |   |--- CodeResources -> _CodeSignature/CodeResources
|       |   |--- Info.plist
|       |   |--- MacOS
|       |   |   `-- SourceCode
|       |   |--- _CodeSignature
|       |   |   `-- CodeResources
|       |   `-- version.plist
|       `-- uuid.mdimporter
|           `-- Contents
|           |--- CodeResources -> _CodeSignature/CodeResources
|           |--- Info.plist
|           |--- MacOS
|           |   `-- uuid
|           |--- Resources
|           |   |--- English.lproj
|           |   |   |--- InfoPlist.strings
|           |   |   `-- schema.strings
|           |   |--- Japanese.lproj
|           |   |   |--- InfoPlist.strings
|           |   |   `-- schema.strings
|           |   `-- schema.xml
|           |--- _CodeSignature
|           |   `-- CodeResources
|           `-- version.plist
|--- MacOS
|   `-- Xcode
|--- PkgInfo
|--- PlugIns
```

清单 1.3（续）

```
|   |-- BuildSettingsPanes.xcplugin
|   |   `-- Contents
|   |       |-- CodeResources -> _CodeSignature/CodeResources
|   |       |-- Info.plist
|   |       |-- MacOS
|   |       |   `-- BuildSettingsPanes
|   |       |-- Resources
|   |           |-- Built-in Build Settings Panes.pbsettingspanespec
|   |
|   |-- Resources
|   |   |-- AskUserForNewFileDialog
|   |   |-- CreateDiskImage.workflow
|   |   |   `-- Contents
|   |   |       `-- document.wflow
|   |   |-- DevCDVersion.plist
|   |   |-- Document-Cert.icons
|   |-- _CodeSignature
|   |   `-- CodeResources
|   `-- version.plist
```

请注意，`Contents/MacOS` 目录包含 Xcode 可执行文件。这个可执行文件与你制作命令行应用程序时生成的可执行文件是一样的。区别在于，它被打包在应用程序包中，并且包含从该包中加载资源的代码。此应用程序中其他一些有趣的目录包括 `PlugIns` 目录，其中也包含包。`Spotlight` 目录也包含以 `SourceCode.mdimporter` 和 `uuid.mdimporter` 目录形式存在的包。Foundation 框架（我们将在本书第二部分介绍）包含让你能够读取应用程序包的方法，并允许访问这类嵌入式包。

此时你需要知道的重要事情是，当你为 Mac OS X、iPhone 或 iPad 创建图形应用程序时，Xcode 会为你的应用程序创建一个应用程序包。将来，如果你需要在应用程序中包含分组隔离的资源组，你可能会希望自己创建一个应用程序包。Xcode 也正好为你提供了这样的能力。不过，目前你不需要担心这一点。

## 使用构建设置

Xcode 中有两个位置可以配置项目的构建设置。第一个也是主要的位置是项目信息窗口，你可以通过选择“项目 ▷ 编辑项目设置”（Project ▷ Edit Project Settings）来访问它。在本节中，我将详细介绍这些窗口，因为这些信息既有用又有指导意义。由于这部分内容在书中的位置，你可能无法理解我将要讨论的许多内容。我建议你先略读这一节，等完成第 2 章之后再回来阅读。项目设置窗口的第一个面板（如图 1.9 所示）显示了项目的一般设置。其中大部分你不需要更改，但通过“配置根目录和 SCM”（Configure Roots and SCM）按钮配置源代码管理这一项除外。

