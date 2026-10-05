
要创建此层次结构，应从根作业（root job）开始向作业添加进程。以下是创建此层次结构的步骤set：

- 1. 将进程 P1 添加到作业 1。
2. 将进程 P1 添加到作业 2。这创建了第一次嵌套。
3. 将进程 P2 添加到作业 1。
4. 将进程 P2 添加到作业 3。这创建了第二次嵌套。
5. 将进程 P3 添加到作业 2。
6. 将进程 P4 添加到作业 1。

# 实验：查看作业对象（job object）

你可以使用性能监控（Performance Monitor）工具查看作业对象。（查找作业对象（Job Object）和对象详情（Object Details）类别）。你可以使用内核调试器 `!job` 或 `dt nt!_exe` 命令查看未命名作业。

要查看一个进程是否与某个作业关联，可以使用内核调试器 `!process` 命令或进程管理器（Process Explorer）。按照以下步骤创建并查看未命名作业：

- 1. 从命令提示符开始，使用 `run` 命令创建一个运行命令提示符（cmd.exe）的进程。例如，输入 `runas /user:<domain>\<username> cmd`。

- 2. 系统会提示你输入密码。输入密码后将出现命令提示符窗口。执行 `run` 命令的 Windows 服务会创建一个未命名作业来包含所有进程（以便在注销时终止这些进程）。

- 3. 运行进程管理器，使用“选项”（Options）菜单，选择“选择颜色”（Choose Colors），并勾选“作业”（Jobs）项。注意，Cmd.exe 进程及其子进程 Host.exe 进程作为作业的一部分被突出显示，如下：

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_196_0.png)

- 4. 双击 Cmd.exe 或 Host.Exe 打开其属性对话框。然后点击“作业”（Job）选项卡，查看该进程所所属作业的信息：

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_197_0.png)

- 5. 从命令提示符运行 Notepad.exe。

- 6. 打开记事本的进程并查看“作业”选项卡。Notepad 运行在同一个作业下。这是因为 cmd.exe 没有使用 `CREATE_BREAKAWAY_FROM_JOB` 创建标志。在嵌套作业的情况下，“作业”选项卡会显示该直接作业中的进程，而这些进程属于所有子作业中的进程。

- 7. 在实时系统上运行内核调试器，并使用 `lprocess` 命令找到 notepad.exe 并显示其基本信息：

```
1kd> !process 0 1 notepad.exe
PROCESS Fffe001ecaf280
SessionID: 1 Cid: 3078 Peb: 7ff41b3000 ParentId: 05dc
DirBase: 4878b3000 ObjectTable: fffe0015b89fd80 HandleCount: 188.
Image: notepad.exe
```
- - BasePriority 8
CommitCharge 671
Job fffe00189aec460

- 8. 注意作业指针，它是非零的。对于某些作业，使用 `ljob` 命令：

```
1kd> !job fffe00189aec460
Job at fffe00189aec460
Basic Accounting Information
TotalUserTime: 0x0
TotalKernelTime: 0x0
TotalCycleTime: 0x0
ThisPeriodTotalUserTime: 0x0
ThisPeriodTotalKernelTime: 0x0
PageFaultCount: 0x0
TotalProcesses: 0x3
ActiveProcesses: 0x3
```
FreezeCount: 0
BackgroundCount: 0
TotalTerminatedProcesses: 0x0
PeakJobMemoryUsed: 0x10db
PeakProcessMemoryUsed: 0xa56
Job Flags
Limit Information (LimitFlags: 0x0)
Limit Information (EffectiveLimitFlags: 0x0)

```

- 9. 注意 `ActiveProcesses` 成员被设置为 3（cmd, conhost, exe 和 notepad.exe）。你可以在作业命令后使用标志 2 来查看属于该作业的进程列表：

```
1kd-> !job ffffe00189aec460 2
```

分配给此作业的进程：
PROCESS ffff8188d84dd780
SessionId: 1 Cid: 5720 Peb: 43ebdb6000 ParentId: 13cc
DirBase: 75a183000 ObjectTable: fffebe0dc4e3a040 HandleCount:
<Data Not Accessible>
Image: cmd.exe

```
PROCESS ffff8188ea077540
SessionId: 1 Cid: 30ec Peb: dd7f17c00 ParentId: 5720
DirBase: 75a183000 ObjectTable: fffebe0dbaf79040 HandleCount:
<Data Not Accessible>
Image: conhost.exe

```
PROCESS ffff001eafc2080
SessionId: 1 Cid: 3078 Peb: 7f4113b000 ParentId: 05dc
DirBase: 4878b3000 ObjectTable: fffc015b69fd80 HandleCount: 188.
Image: notepad.exe
```

- 10. 你还可以使用 `dt` 命令显示作业对象，并查看关于作业的附加字段、其成员级以及在发生嵌套时与其他作业的关系（父作业、兄弟作业和根作业）：

```
1kd-> dt job ffffe00189aec460
+0000 Event : _KEVENT
+0018 Job : _LIST_ENTRY [xffff001'8d93e5f0]
+0028 ObjectDetails : _OBJECT_000000000000000000000000000000000000000000000000000000000
+0080 LimitFlags : 0x0
+0088 EffectiveLimitFlags : 0x0
+00a0 Resource : _RESOURCE
+00a8 WaitCount : 0
+00b0 HandleCount : 0
+00b8 ObjectType : 0
+00c0 ProcessCount : 0
+00c8 ThreadCount : 0
+00d0 ActiveProcesses : 0
+00d8 TotalProcesses : 0
+00e0 FreezeCount : 0
+00e8 BackgroundCount : 0
+00f0 TotalTerminatedProcesses : 0
+00f8 PeakJobMemoryUsed : 0
+0100 PeakProcessMemoryUsed : 0
+0110 JobFlags : 0
```
