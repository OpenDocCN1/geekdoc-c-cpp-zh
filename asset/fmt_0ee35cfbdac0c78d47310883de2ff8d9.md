
当 `dll` 被加载时，它的执行将从此方法开始。你可以区分此方法被加载的原因。这些如下：

- `DLL_PROCESS_ATTACH` 方法通知应用程序刚刚加载了 `dll`
- `DLL_PROCESS_DETACH` 方法通知应用程序刚刚卸载了 `dll`
- `DLL_THREAD_ATTACH` 方法通知加载该 `dll` 的应用程序创建了一个新线程
- `DLL_THREAD_DETACH` 方法通知线程正在退出，可以进行一些清理工作

我们将所有的操作都放在 `DLL_PROCESS_ATTACH` 内部完成。在我们的主应用程序中，我们创建了用于应用程序和 `dll` 之间通信所需的内存映射，我们稍后会解释它。在 `dll` 内部，我们首先使用 `OpenFileMapping` API 打开文件映射。如果映射已打开，我们将句柄（handle）写入 `hLibrary` 属性中。在我们完成工作后，我们需要这个句柄从目标进程中卸载库。接下来，我们调用 `ChangWindowTitle` 方法。此函数尝试使用 `FindMainWindow` 查找主窗口句柄。如果找到了句柄，我们可以修改窗口标题。

`FindWindow` 方法使用 `EnumWindows` API 枚举所有顶层窗口。用户必须提供一个指向用户定义函数（称为回调）的指针作为传递给 `EnumWindows` 的参数。操作系统会为每个属于系统的窗口句柄调用此回调函数。我们可以利用此功能查询拥有该线程（进程）的窗口句柄。我们可以通过 `GetWindowThreadProcessId` 实现这一点。

如果我们发现了一个属于目标进程的窗口，我们还应该检查它是否为主窗口。对于此部分任务，我们使用 `IsMainWnd` 方法。该方法调用 `GetWindow` 并将 `GW_OWNER` 作为第二个参数，如果返回的值为 0（零），它将使用 `IsVisible` API 查询窗口的可见性，以确保如果可见，它就是目标进程的主应用程序窗口。`ChangeWindowTitle` 返回后，我们打开一个事件，用它来通知应用程序任务已完成，我们可以卸载库。我们使用 `SetEvent` API 将事件设置为信号量状态（signaled state）。

# 第 8 章

现在，让我们来解释主应用程序。`RemoteLoadLibrary` 方法被用于在目标进程内部创建一个远程线程。首先，我们需要获取 `LoadLibrary` API 的地址（本示例使用了 `LoadLibraryA` 多字节版本）。此 API 将用作远程线程的起点，并将指定的 `dll` 名称作为参数进行加载。在此过程中，我们将指定的 `dll` 加载到目标进程并在其中执行我们的操作。在获取 `LoadLibrary` 的地址后，我们必须使用 `VirtualAlloc` API 在目标进程中分配虚拟内存，以便在其中写入 `dll` 名称。请注意，在当前进程中指定字符数组的地址在目标进程中是没用的。

我们将 `dll` 写入目标进程，映射在目标进程内有效的字符地址。在分配了虚拟内存后，我们使用 `WriteProcessMemory` API 执行该操作。如果操作成功，我们使用 `CreateRemoteThread` API 创建远程线程。我们必须提供具有正确权限的目标进程句柄。我们没有关注句柄权限，因为我们的应用程序创建了目标进程，创建返回的句柄包含了我们可能需要的所有线程。

在无法创建目标进程的情况下，我们必须打开一个已有的进程，并将 `PROCESS ALL` 访问标志作为 `OpenProcess` API 的第一个参数。只有带有此类权限返回的句柄才能用于 `CreateRemoteThread` API。在成功创建远程线程后，我们使用 `WaitForSingleObject` API 等待线程创建并返回。`RemoteFreeLibrary` 方法用于启动一个远程线程任务，该任务将运行 `FreeLibrary` 并传递 `dll` 作为参数。这样，远程线程将通过传递的句柄卸载指定的 `dll`。

在应用程序进程内部，首先必须设置编译后的 `dll` 的路径。这很重要，因为目标进程中的远程线程将尝试从给定路径加载 `dll`。该路径必须是绝对路径才能成功加载。接下来，我们创建一个文件映射，用于与 `dll` 通信。这非常重要，因为当我们想要卸载库时，必须为 `FreeLibrary` API 提供 `dll` 的句柄。目标进程内部加载的 `dll` 句柄只有在加载成功后已知。这就是为什么在 `dll` 附加后，我们从目标进程写入文件映射。我们创建一个事件，`dll` 将用它信号主应用程序它已写入文件映射，且可以卸载 `dll`。然后，我们使用 `CreateProcess` API 启动计算器。如果创建了进程，我们在 `WaitSingleObject` API 中指定等待 0.5 秒来等待初始化。然后我们尝试创建一个远程线程并等待一个事件对象。在事件设置为信号量状态后，我们可以使用 `RemoteFreeLibrary` 卸载库并关闭所有使用的句柄。

# 另见...

我们该去向何方？很好，我们在这里讨论了关于并发的许多细节。正如我们多次所说的，实践是最好的老师。所以，准备好吧！

## 附录

在本附录中，我们将涵盖以下主题：

- 安装 MySQL Connector/C
- 安装 WinDK 开发工具包
- 设置 Visual Studio 项目
- 使用调试

## 安装 MySQL Connector/C

为了使用 MySQL Connector/C，你需要执行以下操作：

1. 打开浏览器并导航到 `http://dev.mysql.com/downloads/connector/c`

| | | |
|---|---|---|
| Windows (x86, 32-bit), MSI Installer | 6.1.3 | 21.0M [下载] |
| (mysql-connector-c-6.1.3-win32.msi) | | MD5: 509e83de22f3f982ea955f33577e4 |
| Windows (x86, 64-bit), MSI Installer | 6.1.3 | 22.0M [下载] |
| (mysql-connector-c-6.1.3-win64.msi) | | MD5: 122aade6c8d0a77d9401c177477f1 |
| Windows (x86, 32-bit), ZIP Archive | 6.1.3 | 24.0M [下载] |
| (mysql-connector-c-6.1.3-win32.zip) | | MD5: 56c3f5a35d1b0118f95700e55775d0 |
| Windows (x86, 64-bit), ZIP Archive | 6.1.3 | 26.0M [下载] |
| (mysql-connector-c-6.1.3-win64.zip) | | MD5: 61f4e54472f538f99cf44561d3a47f93 |

2. 根据你的架构和项目配置，下载 `mysql-connector-c-6.1.3-win32.msi` 或 `mysql-connector-c-6.1.3-win64.msi` 文件，然后如截图所示开始安装：

## 附录

6. 在配置属性（Configuration Properties）下，展开链接器（Linker）节点。打开**附加依赖（Additional Dependencies）**旁边的组合框并输入 `C:\Program Files\MySQL\MySQL Connector C 6.1.lib\libmysql.lib`，如下截图所示：

![](img/412b0f5bbb36adcce2ddd2d5b7416516_398_0.png)

7. 使用 Windows 文件资源管理器，导航到 `C:\Program Files\MySQL\MySQL Connector C 6.1.lib`。将 `mysql.dll` 文件复制到 `C:\Windows\System32`。

现在，你可以编译并运行 **MultithreadedDBTest** 项目或任何使用 MySQL Connector/C 的项目。

## 安装 WinDK – 驱动程序开发包

为了使用 Windows 驱动程序包（WDK），你需要执行以下操作：

- 1. 打开浏览器并访问 `http://msdn.microsoft.com/en-us/library/windows/hardware/hh852365.aspx`。由于我们使用的是 Visual Studio 2013，你需要下载 WDK 8.1 或使用以下地址：
  `http://go.microsoft.com/fwlink/link/p?LinkId=393659`。以下是 WDK 下载页的截图：

![](img/412b0f5bbb36adcce2ddd2d5b7416516_399_0.png)

- 2. 点击“下一步”并选择你是否愿意参与客户体验改进计划，然后接受许可协议以开始安装。你会看到如下所示的窗口：

![](img/412b0f5bbb36adcce2ddd2d5b7416516_399_1.png)

- 3. 等待安装完成并关闭向导。

![](img/412b0f5bbb36adcce2ddd2d5b7416516_400_0.png)

现在，Windows Driver程序包已成功安装。

## 设置用于驱动程序编译的 Visual Studio 项目

为了获得 Windows 驱动程序包的功能（如编译器和库），你需要设置 Visual Studio 项目属性。要执行此操作，请执行以下步骤：

- 1. 如果你遵循了第 2 章“线程概念（Thread Concept）——示例：在内核中实现线程”的说明，请打开解决方案 KernelThread。在解决方案管理器中，右键点击 DriverApp 并选择“属性”。在“常规”选项卡下，选择“目标扩展（Target Extension）”并点击“编辑”。将 `.exe` 重命名为 `.sys`。点击“应用”，如下截图所示：

![](img/412b0f5bbb36adcce2ddd2d5b7416516_401_0.png)

- 2. 展开 C++ 节点，并在“常规”下选择**附加目录（Additional Directories）**。点击**编辑**并输入以下路径：`C:\Program Files (x86)\Windows Kits\8.1\Include.km`。点击“确定”然后点击“应用”。

![](img/412b0f5bbb36adcce2ddd2d5b7416516_401_1.png)

- 3. 现在，在 C++ 下移除所有“预处理器（Preprocessor）”，并在“预处理器定义（Preprocessor Definitions）”下选择“编辑”。删除所有行，如果激活了 Win32 配置，则输入 `_x86_`；如果激活了 x64 配置，则输入 `_AMD64_`，如下：

![](img/412b0f5bbb36adcce2ddd2d5b7416516_402_0.png)

- 4. 点击确定并应用。现在，在“代码生成（Code Generation）”下，选择“启用 C++ 异常”并删除所有文本留空。点击“应用”。在“基本运行时检查（Basic Runtimes Check）”下，选择“默认”然后点击“应用”。在“安全检查（Security Check）”下，选择“禁用安全检查 (/GS-)”并点击“应用”。

![](img/412b0f5bbb36adcce2ddd2d5b7416516_403_0.png)

- 5. 现在，在“高级（advanced）下，选择“调用约定（calling convention）”并如下选择 `_stdcall (/Gz)` ：

![](img/412b0f5bbb36adcce2ddd2d5b7416516_403_1.png)

- 6. 现在，展开链接器节点，并在“常规”下，选择“启用增量链接（Enable Incremental Linking）”并选择“否 (INCREMENTAL:NO)”。现在，在“输入”下，选择“附加依赖 (x86)”并点击“编辑”。输入以下行：`C:\Program Files (x86) Windows Kits\8.1\Lib\winkm\x64\ntoskrnl.lib` 和 `C:\Program Files (x86) Windows Kits\8.1\Lib\winkm\x64\hal.lib`。注意根据你的解决方案配置将 x64 改为 x86：

![](img/412b0f5bbb36adcce2ddd2d5b7416516_404_0.png)

- 7. 点击确定并选择应用。现在，展开“清单文件（Manifest File）”节点并选择“生成清单（Generate Manifest）”。从下拉列表中选择“否 (/MANIFEST:NO)”。点击“应用”。现在，展开“系统（System）”节点并选择“子系统（SubSystem）”。从下拉列表中选择“原生 (/SUBSYSTEM:NATIVE)”。选择“驱动程序（Driver）”并在下拉列表中选择“驱动程序 (Driver)”。点击“应用”。

![](img/412b0f5bbb36adcce2ddd2d5b7416516_405_0.png)

- 8. 最后，选择**高级（Advanced）**节点并选择**入口（Entry Point）**。插入文本 `DriverEntry`。在**基地址（Base Address）**下插入文本 `x0`。然后选择**随机基地址（Randomize Base Address）**并删除所有文本留空。选择**数据执行防护（Data Execution Prevention）**并删除所有文本留空。选择“导入库（Import Library）”插入文本 `ntoskrnl.lib`。

![](img/412b0f5bbb36adcce2ddd2d5b7416516_405_1.png)

现在，你可以编译并运行 DriverApp。注意，如果你使用的是 64 位操作系统，在修改“高级启动选项”之前，无法启动未数字签名的驱动程序；Vista 及更高版本的 Windows 支持 F8 高级启动选项，即“禁用签名强制（Disable Driver Signature Enforcement）”，这将禁用当前会话内核驱动程序的加载时签名强制。此设置在重启系统后失效（来自 MSDN）。更多信息请访问 `http://microsoft.com/en-us/library/windows/hardware/ff57565(v=vs.85).aspx`。

# 使用 DebugView 

为了显示驱动程序的输出，你需要使用 DebugView 。

- 1. 打开浏览器访问 `http://technet.microsoft.com/en-us/internals/bb964.aspx`。下载 DebugView ZIP 文件并解压到文件夹。运行 DebugView 程序，从菜单选择“捕获（Capture）”。勾选“内核（Kernel)”或按 Ctrl + K。

![](img/412b0f5bbb36adcce2ddd2d5b7416516_406_0.png)

- 2. 现在，运行驱动程序，将在 DebugView 窗口中看到输出。

# 设置用于驱动程序的 Visual Studio 项目

为了获得 Windows 驱动程序包的功能（如编译器和库），你需要设置 Visual Studio 项目属性。要执行此操作，请执行以下步骤：

- 1. 如果你遵循了第 2 章“线程概念——示例：在内核中实现线程”的说明，请打开解决方案 KernelThread。在解决方案管理器中，右键点击 DriverApp 并选择“属性”。在“常规”选项卡下，选择“目标扩展（Target Extension）”并点击“编辑”。将 `.exe` 重命名为 `.sys`。点击“应用”，如下截图所示：

![](img/412b0f5bbb36adcce2ddd2d5b7416516_407_0.png)

- 2. 展开 C++ 节点，并在“常规”下选择**附加目录（Additional Directories）**。点击**编辑**并输入以下路径：`C:\Program Files (x86)\Windows Kits\8.1\Include.km`。点击**确定**然后点击**应用**。

![](img/412b0f5bbb36adcce2ddd2d5b7416516_407_1.png)

- 3. 现在，在 C++ 下移除所有“预处理器（Preprocessor）”，并在“预处理器定义（Preprocessor Definitions）”下选择“编辑”。删除所有行，如果激活了 Win32 配置，则输入 `_x86_`；如果激活了 x64 配置，则输入 `_AMD64_`，如下：

![](img/412b0f5bbb36adcce2ddd2d5b7416516_408_0.png)

- 4. 点击确定并应用。现在，在“代码生成（Code Generation）”下，选择“启用 C++ 异常”并删除所有文本留空。点击“应用”。在“基本运行时检查（Basic Runtimes Check）”下，选择“默认”然后点击“应用”。在“安全检查（Security Check）”下，选择“禁用安全检查 (/GS-)”并点击“应用”。

![](img/412b0f5bbb36adcce2ddd2d5b7416516_409_0.png)

- 5. 现在，在“高级（advanced）下，选择“调用约定（calling convention）”并如下选择 `_stdcall (/Gz)` ：

![](img/412b0f5bbb36adcce2ddd2d5b7416516_409_1.png)

- 6. 现在，展开链接器节点，并在“常规”下，选择“启用增量链接（Enable Incremental Linking）”并选择“否 (INCREMENTAL:NO)”。现在，在“输入”下，选择“附加依赖 (x86)”并点击“编辑”。输入以下行：`C:\Program Files (x86) Windows Kits\8.1\Lib\winkm\x64\ntoskrnl.lib` 和 `C:\Program Files (x86) Windows Kits\8.1\Lib\winkm\x64\hal.lib`。注意根据你的解决方案配置将 x64 改为 x86：

![](img/412b0f5bbb36adcce2ddd2d5b7416516_410_0.png)

- 7. 点击确定并选择应用。现在，展开“清单文件（Manifest File）”节点并选择“生成清单（Generate Manifest）”。从下拉列表中选择“否 (/MANIFEST:NO)”。点击“应用”。现在，展开“系统（System）”节点并选择“子系统（SubSystem）”。从下拉列表中选择“原生 (/SUBSYSTEM:NATIVE)”。选择“驱动程序（Driver）”并在下拉列表中选择“驱动程序 (Driver)”。点击“应用”。

- 8. 最后，选择**高级（Advanced）**节点并选择**入口（Entry Point）**。插入文本 `DriverEntry`。在**基地址（Base Address）**下插入文本 `x0`。然后选择**随机基地址（Randomize Base Address）**并删除所有文本留空。然后选择**数据执行防护（Data Execution Prevention）**并删除所有文本留空。选择“导入库（Import Library）”插入文本 `ntoskrnl.lib`。

现在，你可以编译并运行 DriverApp。注意，如果你使用的是 64 位操作系统，在修改“高级启动选项”之前，无法启动未数字签名的驱动程序；Vista 及更高版本的 Windows 支持 F8 高级启动选项，即“禁用签名强制（Disable Driver Signature Enforcement）”，这将禁用当前会话内核驱动程序的加载时签名强制。此设置在重启系统后失效（来自 MSDN）。

# D

- 公用语言运行时 (`CLR`) 234
- 编译后的应用程序 (`*.exe`) 234
- `ComplexXAdd` 函数 16
- 复合操作场景 312
- 并发
  - 守护任务 216
- 数据库管理系统 (`DBMS`) 88
- 数据竞态场景 310
- 死锁
  - 关于 260
  - 避免 260
- `DebugView`
  - 安装 392
  - 使用 392
- `DestroyWindow` API 33
- 析构函数 (`dtor`) 42
- 哲学家就问题
  - 解决 66-74
- 调度器 (`dispatcher`)
  - 关于 175, 176, 343
  - 定制 355-366
  - 工作 366-370
- `dValue` 11
- 动态绑定 28
- 动态库 (`*.dll`) 14
- 动态优先级 169, 170
  - 正性问题 310
  - 活跃性问题 310
- 构造函数 (`ctor`) 42
- `ContinueWith` 方法 291
- 正确性问题
  - 关于 310
  - 发生实例 314
- `Count` 方法 42
- `cout` 对象 12
- `CParameters` 类 352
- C++ 程序
  - `#include <iostream>` 头文件 11
  - 创建 11-14
  - 示例 13
- C++ 项目
  - 创建 9, 10
- CPU 多任务系统 46
- `Create` 方法 120
- `CreateNamedPipe` API
  - 引用，URL 165
- `CreateProcess` 函数
  - 关于 49
  - 在 MDN 上，URL 47
- `CreateThread` API
  - 非 MDN，URL 81
- `CreateWindow` API 32
- 临界区域 56
- 临界区 (`critical section`)
  - 关于 56, 139, 206
  - 使用 206-215
- `CSchwefelMT` 类
  - 创建 325-327
  - 工作 328
- `CShapePair` 生类
  - 工作 337-340
- `Cthread` 类 120
- `ThreadPool` 类 353
- `CWorker` 类, `CPerson` 22

# E

- `EAP`
  - 关于 269
  - 优势 275
  - 缺点 275
  - 示例 275, 276
  - 程序，创建 269-275
  - 工作 275
- `Elapsed(TCHAR*)` 方法 323
- `Elapsed(void)` 方法 323
- `Evaluate` 方法 328
- `Evaluate(void*)` 方法 323
- 事件 (`event`)
  - 使用 197-206
  - 事件的异步模式 (`EAP`)。参见 `EAP`
  - 事件驱动系统 141
- 事件处理程序 (`event handler`)
  - 关于 29
  - 针对 Windows 29
- 事件对象 136-138
- 事件同步对象 197
- 最终问题解决功能 343
- 事件等待句柄 (`event wait handles`)
  - 信号 263-268
- `ExitProcess` 函数 50

# F

- 斐那契序列 339
- 文件映射 64
- `FindMainWindow` 方法 378
- `Find` 方法 42
- 先进先出 (`FIFO`) 34
- 前台线程
  - 区分，与后台线程
  - 线程 243-247
- 傅里叶集 175
- 全线程 293

# G

- 垃圾回收器 (`GC`) 242
- `new` 运算符 242
- `GetAsyncState` 方法 321
- `GetFirst` 方法 42
- `GetHandle` 方法 121
- `Getid` 方法 121
- `GetLast` 方法 42
- `GetMessage` API 32
- `GetNext` 方法 42
- `GetUserData` 方法 121
- `GET_X_LPARAM` 宏 147
- `GET_Y_LPARAM` 宏 147
- 图形用户界面 (`GUI`) 9
- `GWLP_USERDATA` 宏 155

# H

- 半栅（`volatile` 内存对象） 293
- 硬件抽象层 (`HAL`) 234
- `Head` 方法 42
- `hprev` 参数 30
- `hThis` 参数 30
- `hhThread` 属性 367
- 超线程技术 (`Hyper-Threading Technology`) 338

# I

- `ICount` 11
- 不一致同步场景 311
- 继承 (`Inheritance`)
  - 关于 19
  - 示例，复 20-22
  - 工作 22
- `Initialize` 方法 40
- `Insert` 方法 42
- 安装
  - MySQL Connector/C 381-384
  - WinDK 384-386
- `IntelliSense` 引擎 9
- 进程间通信。参见
- `Interrupt` 方法 281
- `int _main(int argc, char *argv[])` `argc` 参数 12
- `int_main(void)` 原型 12
- `IPC`
  - 关于 55, 230
  - 示例 55-59
  - 工作 63-65
- `IPCDemo` 64
- `IPC` 问题
  - 哲学家就问题，解决。65-67
- `IPCWorker` 63

# J

- Java 环境 (`JRE`) 235
- `Join` 方法 121

# K

- 内核 (`kernel`)
  - 线程，实现 99-104

# L

- `LABEL_TEXT` 宏 146
- 后进先出 (`LIFO`) 34
- 线性链表
  - 使用 35-41
- 线性列表 34
- 监听线程
  - 创建 230
- 列表视图 (`list view`) 121, 310, 314
- 活跃性问题 291
- `LoadLibrary` API 379
- 锁 (`lock`)
  - 实现 254-260
- `Lock` 类 254
- `LockName` 方法 352
- 互斥锁 (`mutex`)
  - 关于 67, 134, 177
  - 使用 177-187
- MySQL Connector/C
  - 实现 381-384
- MySQL 数据库
  - 使用，用于线程 81-88

# M

- 主函数
  - 原型 12
  - 主线程 8, 105
- 托管代码
  - 优势 234
  - 缺点 235
- `ManualEventSlim` 268
- `ManifestEvent` 类 234, 235
- `MemoryBarrier` 291
- 消息 141
- 消息传递 (`message passing`)
  - 演示 142-147
- 消息传递接口 (`MPI`) 141, 142
- 消息队列
  - 关于 147
  - 实现 148-155
- Microsoft.NET
  - 框架 234
- `Monitor` 对象
  - `Monitor::Pulse` 方法 294
  - `Monitor::Wait` 方法 294
  - `MonitorWait` 方法 294
  - 信号 294-299
- MSDN 参考 9
- MSI
  - 多任务 46
  - 多线程 8

# N

- 命名空间 (`namespaces`) 12
- 非阻塞同步 291-293

# O

- 对象管理器 (`Object Manager`) 111
- 面向对象 (`OOP`)
  - 关于 17
  - 示例，复 17
  - 继承 19
  - 工作 19
- OpenMP (多处理器) 关于 332
- `OpenThread` 函数 49
- `OVERLAPPED` 对象 166
- 覆盖功能 24

# P

- 并行应用
  - 设计 310-316
- 并行方法
  - 转换 324-331
- 并行性
  - 添加到代码 323, 324
  - 并行编程 309
- `PCB`
  - 关于 51, 52
- `Peek` API 161
- 性能因素 332-336
- 协作性多任务与抢占式多任务 110
- 信号
  - 终止 281-286
  - 中断 281-286
  - 安全取消 281-290
  - 信号 `Monitor::Wait` pulse 294-299
  - 信号 `Monitor::Wait` 方法 294
- 哲学家应用 74
- 客户端 (`client`) 161
- 管道对象
  - 关于 216
  - 用于进程通信 161-266
- 管道服务器 161
- `PLDATAobject` 155
- 多态 24
- `PostAction` 委托 307
- `PostMessage` API 142
- `PostQueue` API 33
- 主线程 8
- 进程与线程优先级 170-176
- 进程控制块。`PCB`
  - 关于 46
  - 实现 52-54
- 进程模型
  - 阻塞状态 50
  - 事件 47
  - 创建 48-51
  - 运行状态 50
- 生产者-消费者问题 98
- 程序
  - 创建，Schweifel 函数计算 317-322
- 编程范式
  - 声明式 10
  - 函数式 10
  - 命令式 10
  - 面向对象
  - 伪并行 8, 168
- 纯虚函数 27

# Q

- 量 177
- 伪并行概念 8
- 队列 34

# R

- 竞态条件 56
- `Rand` 函数 16
- 就绪进程 50
- 就绪线程 176
- 释放栅栏 293
- `ReleaseThread` 方法 353
- `RemoteLibrary` 方法 379
- 远程线程
  - 关于 371
  - 使用 371-375
  - 工作 377-399
- `RemoveAll` 方法 353
- `RemoveThread` 方法 353, 368
- 请求处理 166
- `RequestThread` 方法 353, 168
- `ResetEvent` 138
- `Resume` 方法 121
- 运行进程 50
- 运行线程 176

# S

- 调度器 (`Scheduler`) 46, 51
- 操作系统调度 98
- Schweifel 函数 317
- 信号量 (`semaphore`)
  - 关于 135, 136, 187
  - 使用 187-196
- `SendMessage` API 155
- 顺序式编程方法
- 终止状态 176
- 重要性 310
- `Thread::Abort` 方法 281
- `SetEvent` API 161
- 线程执行
- `SetUserData` 方法 121
- 单线程单元 (`STA`) 242
- .NET 线程
  - `Sleep` 方法 247, 248
  - 关于 235-242
- 套字 216
- 并行任务，执行 235
- 栈 24
  - 工作 237-242
- 待备状态 176
- `Thread::interrupt` 方法 281
- `StartAddress` 方法 241, 328
- `Thread::Join` 方法 247
- `STATE_ALIVE` 宏 120
- 线程消息队列
- `STATE_BLOCKED` 宏 120
  - 使用 156-161
- `STATE_CONTINUOUS` 宏 120
- 线程模型
- `STATE_READY` 宏 120
  - 实现 75-80
- `STATE_RUNNING` 宏 120
- 线程对象属性
- `static_SYNC` 宏 120
- 基础优先级 169
- 静态库 (`*lib`) 314
- 动态优先级 169
- `ScheduleAction` 方法 352
- 线程池
- 结构化编程方法
  - 关于 342
  - 关于 14
  - 调度器，定制 354-366
- `Suspend` 方法 121
  - 使用 343-350
- 同步 188
- 工作 352, 353
- .NET 同步机制
- `ThreadPool` 类 236
  - 添加 47
  - 工作 253
  - 使用 MySQL 数据库演示 81-88
- Win32 同步对象
  - 在内核中实现 99-104
- 临界区 133
  - 在用户空间实现 89-98
- 事件 133
  - 无锁实现
- 互斥锁 133
- 同步 121-127
- 同步线程
  - 管理 112-121
  - 使用 127-132
- 终止 168
- `szCmdLine` 参数 300
- 时间控制 168

# T

- `Task` 类
  - 进程 107-109
  - 视图 290
- 线程安全
  - 关于 261
- `Task::Wait` 方法 247
- 在 .NET 263
- `TCHAR* Object(void)` 方法 323
- `Thread::Sleep` 方法 247
- `T_ENDTASK` 消息
- `ThreadStart` 方法 81
- 时间控制，线程
  - 优先级 168
- 同步 168

由 `[stormrg]` 上传

# T_MESSAGE 信息
定义 161
- 传输方法 352
- 转换状态 176
- 编译单元 (`TU`) 模型 9
- 类型的 NqueryInformationProcess-函数 54
- 等待状态 176
- `Wait`方法 247
- `WhoAml` 方法
- 覆盖 24
- Win32
- 同步对象 133
- 线程对象 111
- Win32 API `CreateThread` 105
- Win32 线程对象 111
- WinDDK
- 安装 384-386
- Windows 应用程序
- 创建 29-34
- Windows 调度对象 176, 341
- Windows 驱动开发包, Sei, WinDDK
- Windows NT HAL 234
- Windows 同步对象
- 临界区 206
- 信号量 177
- Windows 虚拟内存管理器
- 机制 341
- `WM_ENDTASK` 消息 154
- `WM_USER` 消息 154
- `WndProc` 29
- 工作窃取特性 236

# U

- 非托管代码
- 关于 234
- 对比非托管代码 234
- `UpdateWindow` 函数 32
- 用户空间
- 线程，在 89-98 中实现
- 使用命令 12

# V

- Visual Studio 项目
- 为驱动编译进行设置 386-392
- 为 OpenMP 编译进行设置 393-395
- `void_main(int argc, TCHAR* argv[])` 原型 12
- `void_main(void)` 原型 12
- `volatile` 关键字 293

# W

- `WaitAll` 方法 353
- 等待链遍历 (`WCT`) 369
- `WaitForInputDialog` 函数 50

![](img/412b0f5bbb36adcce2ddd2d5b7416516_419_0.png)

# 感谢购买
C++ 多线程编程实战

# 关于 Packt 出版社

Packt 宣布“packed”，于 2004 年 4 月出版了第一本书《精通 phpMyAdmin 进行高效 MySQL 管理》，此后继续专注于出版针对特定技术和解决方案的高度聚焦书籍。

我们的书籍和出版物分享了您的同行 IT 专业人士在适应和定制今日系统、应用程序和框架方面的经验。我们基于解决方案的书籍为您提供了定制正在使用的软件和技术的知识和力量，以完成工作。Packt 的书籍比您过去看到的 IT 书籍更具体，不那么泛泛。我们独特的业务模式使我们能够为您提供更具针对性的信息，让您获得更多需要的内容，减少不需要的内容。

Packt 是一家现代、独特的出版公司，专注于为开发者、管理员和新手等社区生产高质量、前沿书籍。欲了解更多信息，请访问我们的网站：`www.packtpub.com`。

# 关于 Packt 开源

2010 年，Packt 启动了两个新品牌：Packt Open Source 和 Packt Enterprise，以继续其专业化重点。本书是 Packt Open Source 品牌的一部分，该品牌出版围绕开源许可构建的软件书籍，并为从高级开发人员到 Web 设计师的群体提供信息。开源品牌还运行 Packt 的开源版税计划，通过该计划，Packt 会为书籍内容涉及的每个开源项目支付版税。

# 为 Packt 写作

我们欢迎任何对撰书感兴趣的人士咨询。书籍提议请发送至 `author@packtpack.com`。如果您的书籍想法仍处于早期阶段，并希望在编写正式书籍提议之前进行讨论，请联系我们；我们的一位委托编辑将与您联系。

我们并不寻找已出版的作者；如果您拥有强大的技术技能但没有写作经验，我们丰富的编辑可以帮助您发展写作生涯，或者仅仅为您的专业知识获得额外的奖励。

# 开源社区经验挑战

# Java 7 并发编程实战

ISBN: 978-1-84968-788-1 平装本: 364 页

超过 60 多个简单但极其有效的配谱，帮助您使用 Java 7 精通多线程应用开发

- 1. 掌握 Java 7 为并发编程提供的所有功能。
- 2. 在本书和电子书中掌握线程管理、Fork/Join 框架、并发类以及更多。
- 3. 一本实用的实战指南，包含了实现最重要 Java 并发任务的配谱。

![](img/412b0f5bbb36adcce2ddd2d5b7416516_420_0.png)

# C# 5.0 多线程编程实战

ISBN: 978-1-84969-764-4 平装本: 268 页

超过 70 个配谱，帮助您快速高效地学习 C# 5.0 异步和并行编程

- 1. 深入研究 .NET 线程基础并使用 Task 库进行异步编程。
- 2. 有效扩展您的应用程序。
- 3. 掌握 C# 5.0 异步操作支持。

![](img/412b0f5bbb36adcce2ddd2d5b7416516_420_1.png)

请访问 `www.PacktPub.com` 了解其他

# 开源

# 使用 Code::Blocks 进行 C++ 应用程序开发

ISBN: 978-1-78328-341-5 平装本: 128 页

通过本简简洁的实操指南，快速高效地使用 Code::Blocks 开发高级应用程序

- 为 C++ 开发成功安装并配置 Code::Blocks。
- 使用 Code::Blocks 进行快速应用程序开发。
- 使用高级 C++ 特性，包括代码调试和 GUI 工具。

![](img/412b0f5bbb36adcce2ddd2d5b7416516_421_0.png)

# Boost C++ 应用程序开发实战

ISBN: 978-1-84951-488-0 平装本: 348 页

超过 80 个实用的基于任务方案，使用 Boost 库创建应用程序

- 探索如何编写一次程序并用于 Linux、Windows、Mac OS 和 Android 操作系统。
- 包含了 Boost 库开发者提供的关于多线程、元编程和泛型编程的所有使用方案。
- 利用 Boost 和 C++ 的真实力量，在任何项目中打下坚实基础。

![](img/412b0f5bbb36adcce2ddd2d5b7416516_421_1.png)

请访问 `www.PacktPub.com` 了解我们最新的
