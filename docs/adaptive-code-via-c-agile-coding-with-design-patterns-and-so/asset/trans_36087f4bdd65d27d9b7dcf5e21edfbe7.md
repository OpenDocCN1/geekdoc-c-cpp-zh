

## 解决依赖项

了解如何安排项目及其依赖关系，在调试程序集之间的依赖关系时并无帮助。有时程序集在运行时不可用，此时有必要找出原因。

## 程序集

公共语言运行时（CLR），即 .NET Framework 用于执行代码指令的虚拟机，与其他任何软件产品一样，已被编程为在托管应用程序时以可预测和逻辑的方式运行。对程序集如何被解析以及解析错误如何修复的理论和实践有良好的基础是非常有用的。当你需要追踪查找程序集的问题时，少量知识就能走得很远。

## 解析过程

程序集解析过程是 CLR 的一个重要方面。它涵盖了从向程序集或项目添加引用到应用程序运行并加载该程序集之间的差距。涉及多个步骤，只需一个概述即可，当过程中出现问题时，你可以推断出问题的可能原因。

图 2-15 以流程图的形式展示了程序集解析过程。该流程图处于高层次，不包括每个细节，但足以显示过程中的主要项目。过程如下：

- CLR 使用即时（JIT）模型来解析程序集。如本章前面已证明，应用程序中包含的引用在启动应用程序时不会被解析，而是在你首次使用该程序集的功能时才解析—— literally just in time。
- 每个程序集都有一个标识，它由名称、版本、区域性以及公钥令牌组成。绑定重定向等功能可以更改此标识，因此确定它并不像看起来那么简单。
- 当程序集的标识已确定后，CLR 能够确定它是否已在当前应用程序执行期间之前尝试解析此依赖项，如以下从 Visual Studio 项目文件摘取的代码段所示。
- 提出此问题会导致 CLR 根据答案分支。如果已尝试解析此程序集，则该过程要么已成功，要么已失败。如果成功，CLR 可以使用已加载的程序集并提前退出。如果不成功，CLR 知道无需继续尝试解析此程序集，因为它会失败。
- 或者，如果这是首次尝试解析程序集，CLR 首先检查全局程序集缓存（GAC）。GAC 是一个机器范围的程序集存储库，允许同一应用程序中执行同一程序集的多个版本。如果在 GAC 中找到程序集，则解析过程成功，并且发现的程序集被加载。因此你现在知道，因为 GAC 会首先被搜索，

```
<reference include="MyAssembly, Version=2.1.0.0, Culture=neutral,
    PublicKeyToken=17fac983cbea459c" />
```

GAC 中存在适用的程序集将优先于文件系统上的程序集。

- 如果在 GAC 中找不到程序集，CLR 开始探测多个目录以查找它。搜索的目录取决于 app.config 设置。如果 app.config 中有 codeBase 元素，则会检查该位置——如果未找到程序集，则不会随后检查其他位置。但是，默认情况下会搜索应用程序的根目录，通常是与入口点或 Web 应用程序相关的 /bin 文件夹。如果在那里找不到程序集，则解析过程失败，CLR 会抛出异常。通常，这会导致应用程序终止。

![](img/65c1bad7a6b3cffae8cbb79664f0708b_84_0.png)

图 2-15 程序集解析过程的简要概述。

## Fusion 日志

这是调试 CLR 在运行时绑定到程序集失败尝试的非常有用的工具。与尝试在 Visual Studio 调试器中逐步执行应用程序相比，最好打开 Fusion 并阅读生成的日志文件。

要启用 Fusion，你必须编辑 Windows 注册表，如以下代码所示。

```
HKLM\Software\Microsoft\Fusion\ForceLog 1
HKLM\Software\Microsoft\Fusion\LogPath C:\FusionLogs
```

ForceLog 值是一个 DWORD，而 LogPath 是一个字符串。你可以将 LogPath 设置为你选择的任何路径。失败绑定的示例显示在列表 2-12 中。

### 列表 2-12 Fusion 对绑定程序集失败尝试的示例输出。

```
*** Assembly Binder Log Entry (6/21/2013 @ 1:50:14 PM) ***

The operation failed.
Bind result: hr = 0x80070002. The system cannot find the file specified.

Assembly manager loaded
from: C:\Windows\Microsoft.NET\Framework64\v4.0.30319\clr.dll
Running under executable C:\Program Files\1UPIndustries\Bins\v1.1.0.242\Bins.exe
--- A detailed error log follows.

==== Pre-bind state information ====
LOG: User = DEV\gmclean
LOG: DisplayName = TaskbarDockUI.Xtensions.Bins.resources, Version=1.0.0.0, Culture=en-US, PublicKeyToken=null (Fully-specified)
LOG: Appbase = file:///C:/Program Files/1UPIndustries/Bins/v1.1.0.242/
LOG: Initial PrivatePath = NULL
LOG: Dynamic Base = NULL
LOG: Cache Base = NULL
LOG: AppName = Bins.exe
Calling assembly : TaskbarDockUI.Xtensions.Bins, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null.
====
LOG: This bind starts in default load context.
LOG: No application configuration file found.
LOG: Using host configuration file:
LOG: Using machine configuration file from C:\Windows\Microsoft.NET\Framework64\v4.0.30319\config\machine.config.
LOG: Policy not being applied to reference at this time (private, custom, partial, or location-based assembly bind).
LOG: Attempting download of new URL file:///C:/Program Files/1UPIndustries/Bins/v1.1.0.242/en-US/TaskbarDockUI.Xtensions.Bins.resources.DLL.
LOG: Attempting download of new URL file:///C:/Program Files/1UPIndustries/
Bins/v1.1.0.242/en-US/TaskbarDockUI.Xtensions.Bins.resources/
TaskbarDockUI.Xtensions.Bins.resources.DLL.
LOG: Attempting download of new URL file:///C:/Program Files/1UPIndustries/Bins/
v1.1.0.242/en-US/TaskbarDockUI.Xtensions.Bins.resources.EXE.
LOG: Attempting download of new URL file:///C:/Program Files/1UPIndustries/
Bins/v1.1.0.242/en-US/TaskbarDockUI.Xtensions.Bins.resources/
TaskbarDockUI.Xtensions.Bins.resources.EXE.
LOG: All probing URLs attempted and failed.
```

在编辑注册表后，所有托管应用程序对程序集的解析尝试，无论成功与否，都会写入日志。这显然会产生大量日志文件，这可能很有用，但也可能开始成为大海捞针的问题。

幸运的是，Fusion 有一个 UI 应用程序，如图 2-16 所示，它使找到应用程序的正确文件变得稍微容易一些，而无需在文件系统中搜索。

![](img/65c1bad7a6b3cffae8cbb79664f0708b_86_0.png)

图 2-16 Fusion 具有用于查找应用程序日志文件的用户界面。

并非所有依赖项都需要程序集引用。一种替代方案是将服务代码部署为托管服务。这需要进程间或网络间通信，但它最大限度地减少了客户端和服务器之间所需的程序集引用，正如下一节所考察的那样。

## 服务

与程序集相比，客户端与托管服务的耦合可以松得多，这是有益的，但也需要付出代价。根据应用程序的要求，客户端可能对服务的位置了解很多或很少。此外，你可以改变服务的实现方式，使其要求非常少。对于这些选项中的每一个，都需要考虑不同的权衡。

