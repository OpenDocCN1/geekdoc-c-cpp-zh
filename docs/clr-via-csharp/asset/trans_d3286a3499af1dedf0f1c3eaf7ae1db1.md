
若要监视 CLR 的垃圾回收器，请选择“.NET CLR Memory”性能对象。然后从实例列表框中选择特定应用程序。最后，选择你感兴趣监视的计数器集合，单击“添加”，再单击“确定”。此时，系统监视器将绘制所选实时统计信息的图表。要了解某个特定计数器的说明，请选择所需计数器，然后选中“显示描述”复选框。

另一个监视应用程序对象分配的好工具是 CLR Profiler。该工具提供调用分析、堆快照和内存使用时间线。它甚至还有一个 API，可用于从测试代码中启动和停止分析，并将注释注入日志中。此外，该工具的源代码是可用的，因此你可以根据自己的需要修改该工具。获取此工具的最佳方式是在网络上搜索 *CLR Profiler*。这个工具非常宝贵，我强烈推荐它。

最后，你应了解如何使用 SOS 调试扩展（SOS.dll）。当调试内存问题和其他 CLR 问题时，它通常能提供很大帮助。对于与内存相关的操作，SOS 调试扩展允许你查看进程内为托管堆分配了多少内存，显示终结队列中所有已注册终结的对象，显示每个 AppDomain 或整个进程的 GCHandle 表中的条目，显示堆中使对象保持活跃的根，等等。

## CLR 宿主

.NET Framework 运行在 Microsoft Windows 之上。这意味着必须使用 Windows 可以交互的技术来构建 .NET Framework。首先，所有托管模块和程序集文件必须使用 Windows 可移植可执行（PE）文件格式，并且必须是 Windows 可执行（EXE）文件或 DLL。

在开发 CLR 时，Microsoft 将其实现为包含在 DLL 中的 COM 服务器；也就是说，Microsoft 为 CLR 定义了标准 COM 接口，并为该接口和 COM 服务器分配了 GUID。安装 .NET Framework 时，表示 CLR 的 COM 服务器会像任何其他 COM 服务器一样在 Windows 注册表中注册。如果你希望了解有关此主题的更多信息，请参阅 .NET Framework SDK 自带的 MetaHost.h C++ 头文件。此头文件定义了 GUID 和非托管 ICLRMetaHost 接口定义。

任何 Windows 应用程序都可以宿主 CLR。但是，你不应通过调用 CoCreateInstance 来创建 CLR COM 服务器的实例；相反，非托管宿主应调用在 MetaHost.h 中声明的 CLRCreateInstance 函数。CLRCreateInstance 函数在 MSCorEE.dll 文件中实现，该文件通常位于 C:\Windows\System32 目录中。这个 DLL 被亲切地称为 shim（填充层），其工作是确定要创建的 CLR 版本；shim DLL 本身不包含 CLR COM 服务器。

一台机器可以安装多个版本的 CLR，但只有一个版本的 MSCorEE.dll 文件（即 shim）。¹ 机器上安装的 MSCorEE.dll 版本是与机器上安装的最新版 CLR 一同发布的版本。因此，该版本的 MSCorEE.dll 知道如何找到可能已安装的任何旧版 CLR。

实际的 CLR 代码包含在一个文件中，该文件的名称随 CLR 版本的不同而改变。对于 1.0、1.1 和 2.0 版本，CLR 代码位于名为 MSCorWks.dll 的文件中；对于 4.0 版本，CLR 代码位于名为 Clr.dll 的文件中。由于一台机器上可以安装多个版本的 CLR，因此这些文件按如下方式安装到不同的目录。²

- 版本 1.0 位于 C:\Windows\Microsoft.NET\Framework\v1.0.3705
- 版本 1.1 位于 C:\Windows\Microsoft.NET\Framework\v1.1.4322
- 版本 2.0 位于 C:\Windows\Microsoft.NET\Framework\v2.0.50727
- 版本 4.0 位于 C:\Windows\Microsoft.NET\Framework\v4.0.21006

¹ 如果你使用的是 64 位 Windows 版本，实际上会安装两个版本的 MSCorEE.dll 文件。一个是 32 位 x86 版本，位于 C:\Windows\SysWOW64 目录中。另一个是 64 位 x64 或 IA64 版本（取决于计算机的 CPU 架构），位于 C:\Windows\System32 目录中。

² 请注意，.NET Framework 3.0 和 3.5 版本随附了 CLR 2.0 版本。我没有显示 .NET Framework 3.0 和 3.5 版本的目录，因为 CLR DLL 是从 v2.0.50727 目录加载的。

`CLRCreateInstance` 函数可以返回 `ICLRMetaHost` 接口。宿主应用程序可以调用此接口的 `GetRuntime` 函数，指定宿主希望创建的 CLR 版本。然后，shim 会将所需版本的 CLR 加载到宿主进程中。

默认情况下，当托管可执行文件启动时，shim 会检查可执行文件并提取指示应用程序生成和测试所用 CLR 版本的信息。但是，应用程序可以通过在其 XML 配置文件（将在第 2 章“构建、打包、部署和管理应用程序与类型”和第 3 章“共享程序集和强命名程序集”中介绍）中放置 `requiredRuntime` 和 `supportedRuntime` 条目来覆盖此默认行为。

`GetRuntime` 函数返回指向非托管 `ICLRRuntimeInfo` 接口的指针，通过 `GetInterface` 方法可以获取 `ICLRRuntimeHost` 接口。宿主应用程序可以调用此接口定义的方法来：

- 设置宿主管理器。告诉 CLR 宿主希望参与与内存分配、线程调度/同步、程序集加载等相关的决策。宿主还可以声明希望接收垃圾回收开始和停止的通知，以及某些操作超时的通知。
- 获取 CLR 管理器。告诉 CLR 阻止使用某些类/成员。此外，宿主可以指定哪些代码可以或不可以被调试，以及在发生特殊事件（如 AppDomain 卸载、CLR 停止或堆栈溢出异常）时应调用宿主中的哪些方法。
- 初始化并启动 CLR。
- 加载程序集并执行其中的代码。
- 停止 CLR，从而防止任何更多托管代码在 Windows 进程中运行。

宿主 CLR 有用的原因有很多。宿主允许任何应用程序提供 CLR 功能和可编程性支持，并且至少部分用托管代码编写。任何宿主运行时的应用程序都会为试图扩展该应用程序的开发人员带来许多好处。以下是其中的一些好处：

- 可以使用任何编程语言进行编程。
- 代码通过实时（JIT）编译来提高速度（而不是解释执行）。
- 代码使用垃圾回收来避免内存泄漏和损坏。
- 代码在安全沙箱中运行。
- 宿主无需担心提供丰富的开发环境。宿主可以利用现有技术：语言、编译器、编辑器、调试器、探查器等。

如果你对在宿主方案中使用 CLR 感兴趣，我强烈推荐你阅读 Steven Pressman 的佳作 *自定义 Microsoft .NET Framework 公共语言运行时*（Microsoft Press，2005），尽管该书重点是 CLR 4.0 之前的版本。

> **注意** 当然，Windows 进程根本不需要加载 CLR。仅当你想在进程中执行托管代码时，才需要加载它。在 .NET Framework 4.0 之前，CLR 只允许自身的一个实例驻留在 Windows 进程中。也就是说，一个进程可以包含无 CLR、CLR v1.0、CLR v1.1 或 CLR v2.0。每个进程只允许一个 CLR 版本是一个巨大的限制。例如，Microsoft Office Outlook 无法加载两个针对不同版本的 .NET Framework 生成和测试的加载项。
>
> 然而，借助 .NET Framework 4.0，Microsoft 现在支持在单个 Windows 进程中加载 v2.0 和 v4.0，允许为 .NET Framework 2.0 和 4.0 版本编写的组件并行运行，而不会出现任何兼容性问题。这是一个很棒的新功能，它使 .NET Framework 组件能够比以往在更多方案中可靠地使用。你可以使用 ClrVer.exe 工具查看任何给定进程中加载了哪些 CLR 版本。
>
> 一旦 CLR 被加载到 Windows 进程中，就永远无法卸载；在 **ICLRRuntimeInfo** 接口上调用 **AddRef** 和 **Release** 方法没有效果。从进程中卸载 CLR 的唯一方法是终止进程，从而使 Windows 清理进程所使用的所有资源。

## AppDomain（应用程序域）

当 CLR COM 服务器初始化时，它会创建一个 *AppDomain*。AppDomain 是一组程序集的逻辑容器。CLR 初始化时创建的第一个 AppDomain 被称为 *默认 AppDomain*；该 AppDomain 只有在 Windows 进程终止时才会被销毁。

除了默认 AppDomain 之外，使用非托管 COM 接口方法或托管类型方法的宿主可以指示 CLR 创建额外的 AppDomain。AppDomain 的全部目的是提供隔离。以下是 AppDomain 提供的具体功能：

- **一个 AppDomain 中的代码创建的对象不能直接被另一个 AppDomain 中的代码访问** 当 AppDomain 中的代码创建对象时，该对象由该 AppDomain“拥有”。换句话说，不允许对象活过构造它的 AppDomain 的生存期。其他 AppDomain 中的代码只能使用按引用封送或按值封送语义来访问另一个 AppDomain 的对象。这强制执行了清晰的分离和边界，因为一个 AppDomain 中的代码不能直接引用不同 AppDomain 中的代码创建的对象。这种隔离允许 AppDomain 很容易地从进程中卸载，而不会影响在其他 AppDomain 中运行的代码。
