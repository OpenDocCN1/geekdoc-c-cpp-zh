

## 线程挂起

线程可以通过 `SuspendThread` 和 `ResumeThread` API 函数显式地被挂起和恢复。每个线程都有一个挂起计数（suspend count），在挂起时加1，在恢复时减1。如果计数为 0，则该线程可以执行；否则，它将不会执行。

挂起的工作原理是通过向线程队列一个内核 APC（异步过程调用）来实现。当线程切换到执行时，会先执行该 APC。这使得线程处于等待状态，直到线程最终恢复时触发事件信号，其退出等待状态。

如果线程在挂起请求到来时处于等待状态，那么这种挂起机制有一个明显的缺点，因为这意味着线程需要被唤醒仅仅是为了再次被挂起。这（如果线程的内核栈被交换出）可能会导致内核栈缺页。Windows 8.1 和 Server 2012 R2 了一种名为“轻量级挂起”（Lightweight Suspend）的机制，允许在不使用 APC 机制的情况下挂起处于等待状态的线程，而是直接操作内存中的线程对象并将其标记为挂起。

## （深度）冻结

冻结是一种机制，进程进入一种挂起状态，该状态无法通过在线程上调用 `ResumeThread` 来改变。这在系统需要挂起 UWP 应用时非常有用。这通常发生在 Windows 应用进入后台时——例如，另一个应用进入了前台，或者该应用处于挂起模式。在这种情况下，系统会给应用程序大约五秒的时间运行，通常用于保存应用程序状态。保存状态非常重要，因为如果内存资源不足，Windows 应用可能会在不通知的情况下被杀死。如果应用被杀死，状态可以在下次启动时重新加载，用户会觉得应用从未消失。冻结进程意味着以某种方式挂起所有线程，使得 `ResumeThread` 无法唤醒它们。`KTHREAD` 结构中的一个标志位指示线程是否被冻结。要使一个线程能够执行，其挂起计数必须为 0 且 `Frozen` 标志位必须置零。

深度冻结增加了另一个限制：进程中新创建的线程无法启动得那么快。例如，如果使用 `CreateThread` 调用在深度冻结的进程中创建一个新线程，该线程将在实际启动之前被冻结。这是冻结功能的典型用法。

进程和线程冻结功能没有直接暴露给用户态。它由进程状态管理器（PSM）服务内部使用，该服务负责向内核发出释放和解冻（取消冻结）请求。

你也可以使用作业（jobs）来冻结进程。冻结和解冻作业的能力没有公开文档说明，但可以使用标准的 `SetInformationJob` 系统调用来实现。这通常用于 Windows 应用，因为所有 Windows 应用都包含在作业中。此类作业可能包含单个进程（Windows 应用本身），但也可以包含与同一 Windows 应用程序相关的后台任务托管进程，这样就可以一次性完成对该作业下所有进程的冻结或解冻。（Windows 应用请参阅第 2 部分的第 8 章。）

## 实验：深度冻结

在这个实验中，你将通过调试虚拟机来观察深度冻结的发生。

- 1. 以管理员权限打开 WinDbg 并挂载到正在运行 Windows 10 的虚拟机上。
- 2. 按 `Ctrl+Break` 进入虚拟机的调试模式。
- 3. 当深度冻结开始时，使用显示被冻结进程的命令设置断点：
```
bp nt!PsFreezeProcess "process -1 0; g"
```
- 4. 输入 `g`（go）命令或按 F5。你应该能看到许多深度冻结的发生。
- 5. 从任务栏启动 UI，然后关闭 UI。大约 5 秒后，你将看到如下内容：
```
PROCESS 8F518500 SessionId: 2 Cid: 12c8 Peb: 03945000 ParentCid: 02ac
DirBase: 054007e0 Object: b0a8a040 HandleCount: 988.
Image: SearchUi.exe
```
- 6. 现在退出调试器并显示该进程的更多信息：
```
kd> !process 8F518500 1
PROCESS 8F518500 SessionId: 2 Cid: 12c8 Peb: 03945000 ParentCid: 02ac
DeepFreeze
DirBase: 054007e0 Object: b0a8a040 HandleCount: 988.
Image: SearchUi.exe
VadRoot 9c1fffd8 Vads 405 Clone 0 Priority 7682. Modified 2024. Locked 0nDeviceDevice a12509c0
Token b0a65bd0
ElapsedTime 04:02:33.518
UserTime 00:00:06.937
KernelTime 00:00:00.703
QuotaPoolUsage[PagedPool] 562688
QuotaPoolUsage[NonPagedPool] 34392
Working Sets (now,min,max) (20470, 50, 345) (81880KB, 200KB, 13880KB)
PeakWorkingSetSize 25878
VirtualSize 367 Mb
PeakVirtualSize 400 Mb
PageFaultCount 307764
MemoryPriority BACKGROUND
BasePriority 8
CommitCharge 8908
Job 
```
- 7. 退出调试器查看作业，注意作业是否处于冻结状态。使用作业命令查看更多信息：
```
kd> !job
```
- 8. 停止深度冻结，然后启动 UI 观察其解冻过程。

