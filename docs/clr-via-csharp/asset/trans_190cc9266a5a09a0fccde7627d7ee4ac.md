

每当CLR尝试定位程序集文件时，它总是首先在应用程序的目录中查找，如果在那里找不到文件，它就会在AuxFiles子目录中查找。你可以为probing元素的`privatePath`属性指定多个以分号分隔的路径。每个路径都被视为相对于应用程序基目录的路径。你不能指定标识应用程序基目录之外的目录的绝对路径或相对路径。其理念是，应用程序可以控制其目录及其子目录，但无法控制其他目录。

## 探测程序集文件

当CLR需要定位程序集时，它会扫描几个子目录。以下是针对非特定区域性的程序集进行目录探测的顺序（其中`firstPrivatePath`和`secondPrivatePath`是通过配置文件的`privatePath`属性指定的）：

```
AppDir\AsmName.dll
AppDir\AsmName\AsmName.dll
AppDir\FirstPrivatePath\AsmName.dll
AppDir\FirstPrivatePath\AsmName\AsmName.dll
AppDir\secondPrivatePath\AsmName.dll
AppDir\secondPrivatePath\AsmName\AsmName.dll
...
```

在此示例中，如果JeffTypes程序集文件被部署到名为JeffTypes的子目录中，则不需要任何配置文件，因为CLR会自动扫描名称与正在搜索的程序集名称相匹配的子目录。

如果在上述任何子目录中都找不到该程序集，CLR会从头再来，使用.exe扩展名代替.dll扩展名。如果仍然找不到该程序集，则会抛出`FileNotFoundException`。

对于附属程序集，遵循类似的规则，不同之处在于该程序集预计位于应用程序基目录下名称与区域性匹配的子目录中。例如，如果AsmName.dll具有“en-US”区域性，则会探测以下目录：

```
C:\AppDir\en-US\AsmName.dll
C:\AppDir\en-US\AsmName\AsmName.dll
C:\AppDir\FirstPrivatePath\en-US\AsmName.dll
C:\AppDir\FirstPrivatePath\en-US\AsmName\AsmName.dll
C:\AppDir\secondPrivatePath\en-US\AsmName.dll
C:\AppDir\secondPrivatePath\en-US\AsmName\AsmName.dll

C:\AppDir\en-US\AsmName.exe
C:\AppDir\en-US\AsmName\AsmName.exe
C:\AppDir\FirstPrivatePath\en-US\AsmName.exe
C:\AppDir\FirstPrivatePath\en-US\AsmName\AsmName.exe
C:\AppDir\secondPrivatePath\en-US\AsmName.exe
C:\AppDir\secondPrivatePath\en-US\AsmName\AsmName.exe
```

Machine.config文件中的设置表示影响计算机上运行的所有应用程序的默认设置。管理员可以通过修改单个Machine.config文件来创建计算机范围的策略。但是，管理员和用户应避免修改此文件，因为它包含许多与各种内容相关的设置，使得浏览起来更加困难。此外，你可能希望应用程序的设置能够备份和还原，而将应用程序的设置保存在特定于应用程序的配置文件中可以实现这一点。

# 第3章

# 共享程序集和强命名程序集

- **本章内容：**
  - 两种程序集，两种部署方式 ..... 66
  - 为程序集赋予强名称 ..... 67
  - 全局程序集缓存 ..... 73
  - 生成引用强命名程序集的程序集 ..... 75
  - 强命名程序集具有防篡改能力 ..... 76
  - 延迟签名 ..... 77
  - 私有部署强命名程序集 ..... 80
  - 运行时如何解析类型引用 ..... 81
  - 高级管理控制（配置） ..... 84

在第2章“生成、打包、部署和管理应用程序与类型”中，我讨论了生成、打包和部署程序集所需的步骤。我重点关注了所谓的*私有部署*，即将程序集放置在应用程序的基目录（或其子目录）中供应用程序单独使用。私有部署程序集使公司能够对程序集的命名、版本和行为进行高度控制。

在本章中，我将重点讨论创建可供多个应用程序访问的程序集。Microsoft .NET Framework附带的程序集就是全局部署程序集的一个极佳示例，因为所有托管应用程序都使用Microsoft在.NET Framework类库（FCL）中定义的类型。

正如我在第2章中提到的，Microsoft Windows以不稳定而闻名。这种声誉的主要原因是应用程序是使用其他人实现的代码来构建和测试的。毕竟，当你为Windows编写应用程序时，你的应用程序正在调用由Microsoft开发人员编写的代码。此外，大量公司会制作控件，供应用程序开发人员将其整合到自己的应用程序中。实际上，.NET Framework鼓励这种做法，而且随着时间的推移，出现了许多控件供应商。

随着时间推移，Microsoft开发人员和控件开发人员会修改他们的代码：修复错误、修补安全漏洞、添加功能等等。最终，新代码会进入用户的计算机。用户先前安装并运行良好的应用程序不再使用与构建和测试应用程序时相同的代码。结果，应用程序的行为不再可预测，这导致了Windows的不稳定性。

文件版本管理是一个非常难以解决的问题。事实上，我断言，如果你采用一个被其他代码文件使用的文件，并且只改变文件中的一个位——将0改为1或将1改为0——绝对无法保证在更改前使用该文件的代码在使用新版本文件时仍能正常工作。这个说法成立的原因之一是，许多应用程序会有意或无意地利用bug。如果文件的后继版本修复了某个bug，应用程序就无法再按预期运行。

所以问题来了：如何在修复bug和向文件添加新功能的同时，保证不会破坏某些应用程序？我对这个问题进行了很多思考，并得出一个结论：这是不可能的。但显然，这个答案并不令人满意。文件会带有bug发布，公司也总是希望提供新功能。必须有一种方式分发新文件，并希望应用程序能够正常运行。如果应用程序不能正常运行，还必须有一种简单的方法将应用程序恢复到其上次已知的良好状态。

在本章中，我将解释.NET Framework为处理版本问题而提供的基础设施。让我提醒你：我接下来要描述的内容相当复杂。我将讨论内置在公共语言运行时（CLR）中的许多算法、规则和策略。我还会提到应用程序开发人员必须使用的许多工具和实用程序。这些东西很复杂，因为正如我提到的，版本问题难以应对和解决。

## 两种程序集，两种部署方式

CLR支持两种程序集：*弱命名程序集*和*强命名程序集*。

> **重要提示** 顺便说一下，你在任何.NET Framework文档中都找不到*弱命名程序集*这个术语。为什么？因为这是我杜撰的。事实上，文档中没有术语来标识弱命名程序集。我决定创造这个术语，以便在讨论程序集时不会对我所指的程序集类型产生任何歧义。

弱命名程序集和强命名程序集在结构上是相同的——也就是说，它们使用我们在第1章“CLR的执行模型”和第2章中考察过的相同的可移植可执行（PE）文件格式、PE32(+)头、CLR头、元数据、清单表以及中间语言（IL）。并且你使用相同的工具，例如C#编译器和AL.exe，来构建这两种程序集。弱命名与强命名程序集之间的真正区别在于

