
0:00:~peb

PE at `00000000d4c90100`

InheritedSpace: No

ReadImageFileOptions: No

BeingDebugged: Yes

ImageBaseAddress: `0007ffe80b6000`

Ldr: `0007ffe85d25a0`

Ldr.Initialized: Yes

Ldr.InitializationOrderList: `0000022815d230` `0000022815d40`

Ldr.InOrderList: `0000022815dee4` `0000022815d30`

Ldr.InMemoryOrderList: `0000022815def0` `0000022815d20` Timestamp

`7ff720b6000` `57899a` Jul 16 15:04:02 2016 `C:\Windows\System32\`

notepad.exe `7ffe85480000` `582582f` Nov 11 10:59:43 2016 `C:\WINDOWS\System32\`

ntll.dll `7ffe84b0000` `5789a29` Jul 16 05:21:26 2016 `C:\WINDOWS\System32\`

kernel2.dll `7ffe823c0000` `582858e6` Nov 11 11:01:26 2016 `C:\WINDOWS\System32\`

```
- 2. Ldr 行上的地址指向 `PEB_LDR` 结构。注意 WinDbg 向你显示了三个列表的地址，并转储了初始化列表。

- 3. 你可以通过遍历模块列表并转储格式化为 `LDR_DATA_TABLE_ENTRY` 结构的数据来分析每个模块。但是，而不是对每个条目执行此操作，WinDbg 可以通过 `!list` 扩展和以下语法完成部分工作：
```

```
!list -x "dt ntdll!LDR_DATA_TABLE_ENTRY" @$peb->Ldr->InLoadModuleList

+0x00 InOrderLinks : :LIST_ENTRY [00000028'152d10 00007fe'85d3b0 ]

+0x10 MemoryOrderLinks : :LIST_ENTRY [00000028'152d20 00007fe'85dc0 ]

+0x20 InitializationOrderLinks : :LIST_ENTRY [00000000'0000000 ]

+0x30 Base : 00007ff7f20b600 Void

+0x38 EntryPoint : 00007ff7f028b70 Void

+0x40 SizeOfImage : 0x410000

+0x48 FullDllName : :UNICODE_STRING "C:\Windows\System32\notepad.exe"

+0x58 BaseName : :UNICODE_STRING "notepad.exe"

+0x68 Flags : [4] "???"

+0x68 Flags : 0xacc
```

- 4. 你应该看到每个模块的条目：
尽管此节涵盖了 `ntll.dll` 中的用户态加载器，但请注意内核对驱动程序和依赖 DLL 使用类似的加载器结构，名为 `KLDR_DATA_TABLE_ENTRY`。同样，内核态加载器有自己的条目数据库，可以通过 `PsActiveModuleList` 直接访问。你可以使用前面实验所示的 `!list` 命令，将命令末尾的指针替换为 `PsActiveModuleList`：`!list !KLDR_DATA_TABLE_ENTRY !PsActiveModuleList`。

这种格式的列表可以让你进一步了解加载器，例如 `Flags` 字段包含了它本身无法显示的信息。由于内核和用户态加载器都使用此结构，标志的含义并不总是相同的（某些也存在内核结构中）。

### 表 3-10 加载数据表标志

| 标志 | 含义 |
| --- | --- |
| Packaged Binary (0x1) | 该模块封装应用程序的一部分（只能在 AppX 包的主模块上设置）。 |
| Marked for Removal (0x2) | 一旦引用（例如来自执行的工作线程）丢失，该模块将被卸载。 |
| Image DLL (0x4) | 该模块是镜像 DLL（而不是 DLL 或可执行文件）。 |
| Load Notifications (0x8) | 注册的回调通知了此镜像。 |
| Telemetry Entry Process (0x10) | 该镜像的遥测数据已处理。 |
| Process Static (0x20) | 该模块是主二进制文件的静态导入。 |
| In Legacy Lists (0x40) | 该镜像条目位于加载器的双链列表中。 |
| In Indexes (0x80) | 该镜像条目位于加载器的红黑树中。 |
| Shim DLL (0x100) | 该镜像条目代表 shim 引擎/应用程序数据库的一部分。 |
| In Exception Table (0x200) | 该模块的 pdata 异常处理器已捕获在加载器的插入表中。 |
| Load In Progress (0x800) | 该模块正在加载。 |
| Load Config Processed (0x1000) | 已找到并处理了该模块的加载配置目录。 |
| Entry Processed (0x2000) | 加载器已完成对该模块的处理。 |
| Protect Delay Load (0x4000) | 该文件的控制流保护功能尊重了延迟加载 IAT 的保护。更多信息请见第 7 章。 |
| Process Attach Attached (0x20000) | DLL_PROCESS_ATTACH 通知已发送给 DLL。 |
| Process Attach Failed (0x40000) | DLL 的 DllMain 运行时处理 DLL_PROCESS_ATTACH 通知失败。 |
| Don't Call for Threads (0x80000) | 不向此 DLL 发送 DLL_THREAD_ATTACH/DETACH 通知。可以通过 DThread.libraryCalls 设置。 |
| COR Deferred Validate (0x100000) | Common Object Runtime (COR) 将后验证此 .NET 镜像。 |
| COR Image Application (0x200000) | 该模块是一个 AppX 应用程序。 |
| Don't Relocate (0x400000) | 此镜像不应重定位或随机化。 |
| COR IL (0x800000) | 这是一个仅 . . 中间语言 (IL) 的库，不包含原生汇编代码。 |
| Compat Database Processed (0x4000000) | shim 引擎已处理此 DLL。 |

# 导入解析

现在我们已经解释了加载器跟踪进程加载的所有模块的方式，可以继续分析加载器执行的启动初始化任务。在此步骤中，加载器将执行以下操作：

- 1. 加载进程可执行镜像中导入表中引用的 DLL。

- 2. 通过检查模块数据库来检查 DLL 是否已经加载。如果它不在列表中，加载器将打开 DLL 并将其映射到内存中。

- 3. 在映射操作期间，加载器首先查找尝试尝试加载此 DLL 的各种路径，并检查该 DLL 是否为已知 DLL（这意味着系统在启动时已加载了它，并提供了一个全局内存映射文件以供访问）。此外，根据标准查找算法，还可能发生某些依赖关系，这可能是通过使用本地文件（强制加载器使用本地路径）或通过清单文件（manifest file）实现的，后者可以指定重定向的 DLL 以确保使用特定版本。

- 4. 在磁盘上找到并映射 DLL 后，加载器检查内核是否已将其加载在某处——这被称为重定位（relocation）。如果加载器检测到重定位，它将解析 DLL 中的重定位信息并执行所需的操作。如果没有重定位信息：则 DLL 加载失败。

- 5. 加载器为该 DLL 创建加载器数据表条目并将其插入数据库。

- 6. DLL 映射完成后，对该 DLL 重复此过程以解析其导入表及其所有依赖项。

- 7. 每个 DLL 加载后，加载器会解析 IAT 以查找正在导入的特定函数。这通常通过名称进行，也可以通过序数（一个索引数字）。对于每个名称，加载器会解析所导入 DLL 的导出表并尝试创建匹配。如果没有找到匹配项，则中止操作。

- 8. 镜像的导入表也可以被绑定（bound）。这意味着在链接时，开发人员已经分配了指向外部 DLL 中导入函数的静态地址。这消除了对每个名称进行查找的需要，但它假设应用程序将使用的 DLL 将位于相同的地址。由于 Windows 使用了地址随机化（有关 ASLR 的更多信息请参见第 5 章），这对于系统应用程序和库来说通常并非如此。

- 9. 导入 DLL 的导出表可以使用转发条目（forwarder entry），这意味着该函数在另一个 DLL 中实现。这本质上必须被视为导入或依赖项，因此在解析导出表后，由转发器引用的每个 DLL 也会被加载，加载器返回步骤 1。

在所有导入的 DLL（及其依赖项或导入项）都加载后，所有所需的导入函数都已查找并找到，所有转发器也已加载且处理完成：应用程序在编译时定义的其各个 DLL 的所有依赖项现在都已满足。在执行期间，延迟依赖项（称为延迟加载）以及运行时操作（如调用 `LoadLibrary`）可以调用加载器并重复执行相同的任务。但注意，如果这些步骤在启动期间完成，其中的失败将导致应用程序加载错误。例如，尝试运行一个在当前操作系统版本中不存在的函数的应用程序可能会导致与图 3-12 所示类似的消息。

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_186_0.png)

**3-12** 当 DLL 中不存在所需的（导入）函数时显示的对话框。

## 导入后处理初始化 (Post-import process initialization)

加载所需的依赖项后，必须执行若干初始化任务以完全完成应用程序。在此阶段，加载器将执行以下操作：

- 1. 这些步骤从 `LdrIniState` 设置为 2 开始，这意味着导入项已加载。

- 2. 使用如 Winbg 等调试器时，将命中初始调试器断点。在之前的实验中，这就是你必须输入 `g` 来继续执行的地方。

- 3. 检查是否为 Windows 子系统应用程序，如果是，`BaseThreadInUiThunk` 函数应该已经在早期的进程初始化步骤中被捕获。此时，会调用它并检查执行成功。同样，现在调用 `TermSrvGetWindowsDirectory` 函数（在支持终端服务的系统上，它应该在更早被捕获），该函数会重置 System 和 Windows 目录路径。

- 4. 使用分布图，递归遍历所有依赖项以及所有镜像静态导入的初始化器。这一步会为每个 DLL 调用 `D11Main` 例程，这可能包括在运行时加载新的 DLL，以及处理每个 DLL 的 TLS 初始化器。这是加载应用程序过程中可能失败的最后步骤之一。如果所有加载的 DLL 在完成 `D11Main` 例程后没有返回成功代码，加载器将中止应用程序。

- 5. 如果镜像具有任何 TLS，则调用其 TLS 初始化器。

- 6. 如果模块正在为了应用程序兼容性进行垫片（shimmed）处理，则运行初始化后的 shim 引擎回调。

- 7. 运行在 PEB 中注册的关联子系统 DLL 初始化后例程。对于 Windows 应用程序，这执行了例如终端服务的检查检查。

- 8. 此时，会触发一个 ETW 事件指示进程已成功加载。

- 9. 如果存在最小栈计数，则触摸线程栈以强制将提交的页调入页文件。

- 10. 将 `LdrInstanceState` 设置为 3，这意味着初始化完成。将 PEB 的 `ProcessInitializing` 字段置为 0。然后，更新 `LdrProcessInitialized` 变量。

## SwitchBack

随着 Windows 新版本的发布修复了诸如 API 函数中的竞态条件和错误的参数验证检查等 Bug，无论变化多么微小，每次更改都会创建一个应用程序兼容性风险。Windows 在加载器中使用了一种名为 SwitchBack 的技术，它允许软件开发人员在其执行文件的清单（manifest）中嵌入其目标 Windows 版本的 GUID。

例如，如果一个开发者想要利用 Windows 10 为特定 API 添加的改进，她会在清单中包含 Windows 10 的 GUID；而如果开发者有一个依赖于 Windows 7 特定行为的遗留应用程序，她会在清单中放入 Windows 7 的 GUID。

SwitchBack 解析此信息并将其与 SwitchBack 兼容的 DLL（在 `.sb_data` 节）中的嵌入信息相关联，以决定模块应该调用受影响 API 的哪个版本。由于 SwitchBack 在加载模块级别上工作，它允许进程同时让旧版和当前版本的 DLL 调用同一个 API，但观察到不同的结果。

## SwitchBack GUIDs

Windows 定义了代表从 Windows Vista 开始每个版本的兼容性设置的 GUID：

- (`e2011457-1546-43c5-a5fe-008deee3df30`) 用于 Windows Vista
- (`3513b89a-5d96-4fbd-822d-a2402f9a3`) 用于 Windows 7
- (`4aa2f8e3-53b9-4441-ba9c-d6d4aa6e3`) 用于 Windows 8
- (`e80f7a12-bfb3-4f88-b9a5-4fd50a1a59`) 用于 Windows 10

这些 GUID 必须存在于应用程序文件的 `<SupportedOS>` 元素下（如果清单未包含 GUID，则默认选择 Vista 兼容模式）。使用任务管理器可以查看是否有任何应用程序运行在特定的 OS 模式。图 3-13 显示了在 Windows Vista 和 Windows 7 模式下的应用程序示例。

```xml
<compatibility xmlns="urn:schemas-microsoft.com:v1">
  <supportedOS Id="e2011457-1546-43c5-a5fe-008deee3df30" />
  <supportedOS Id="3513b89a-5d96-4fbd-822d-a2402f9a3" />
  <supportedOS Id="4aa2f8e3-53b9-4441-ba9c-d6d4aa6e3" />
  <supportedOS Id="e80f7a12-bfb3-4f88-b9a5-4fd50a1a59" />
</compatibility>
```
