
这使得该应用程序能够从 AppContainer 应用程序下方关闭句柄。即使没有恶意意图，原始启动程序可能会退出，从而清理其句柄并销毁 AppContainer 特有的对象目录。为了避免这种情况，AppContainer 令牌具有能够存储句柄数组的能力，这些句柄保证在使用它们的任何应用程序的生命周期内存在。这些句柄最初在创建 AppContainer 令牌时传递（通过 `NtCreateLowListBox`），并被复制为内核句柄。

与 AppContainer 令牌类似，还使用了一个特殊的 `SEP_CACHED_HANDLES_ENTRY` 结构，该结构基于存储在该用户登录会话中的哈希表。（有关登录会话的更多信息，请参阅本章的“登录”章节。）该结构包含一个在创建 AppContainer 令牌期间复制的内核句柄数组。这些句柄将在令牌销毁时（因为应用程序退出）或用户注销时（这将导致登录会话拆除）被关闭。

## 实验：查看令牌存储的句柄

要查看令牌存储的句柄，请按照以下步骤操作：

- 1. 运行计算器并启动本地内核调试。
- 2. 搜索计算器进程：

```
ikd>!process 0 1 calculator.exe
PROCESS fffff82c9d1080
SessionId: 1 Cid: 4bd8 Peb: d40bcb00 ParentId: 03a4
DeepFreeze
Base: 5ffca000 ObjectTable: fffff90ad9fa2800 HandleCount:
<Data Not Accessible>
Image: Calculator.exe
Vadroot fffff82cd2c9b6a0 Vads 168 Clone 0 Private 2938, Modified 3332.
Locked 0.
DeviceMap fffff90ad2cd2f0
Token fffff90ad513060
ElapsedTime 1 Day 08:01:47.018
UserTime 00:00:00.015
KernelTime 00:00:00.031
QuotaUsage[PagedPool] 465880
QuotaUsage[NonPagedPool] 23288
Working Sets (now,min,max) (7434, 50, 345) (29736KB, 200KB, 13800KB)
PeakWorkingSetSize 11097
VirtualSize 303 Mb
PeakVirtualSize 314 Mb
PageFaultCount 21281
MemoryPriority BACKGROUND
BasePriority 8
CommitCharge 4925
Job fffff828cd4914060
```

- 3. 使用 `dt` 命令转储令牌。（如果低 3 或 4 位不为零，请降低降低掩码）。

```
nkd> dt ntl_token fffff950adb31060
+0000 TokenSource : :TOKEN_SOURCE
+0010 TokenId : :LUID
+0018 AuthenticationId : :LUID
+0020 ParentTokenId : :LUID

+00c8 TokenFlags : 0x4a00
+00cc TokenInUse : 0x1
+00d4 IntegrityLevel : 1
+00d4 MandatoryPolicy : 1
+00d8 LogonSession : 0ffff950a'b4bb35c0_SEP_LOGON_SESSION_REFERENCES
+00e0 OriginatingLogonSession : :LUID
+00e8 SIdHash : :SID_AND_ATTRIBUTES
+01f8 RetainedSIdHash : :SID_AND_ATTRIBUTES
+0308 SecurityAttributes : 0ffff950a'e4f5f7f0_AUTHZBASED_SECURITY_nnATTRIBUTES_INFORMATION
+0310 Package : 0ffff950a'e0e0d6d0 Void
+0318 Capabilities : 0ffff950a'e8efb8c0_SID_AND_ATTRIBUTES
+0320 CapabilityCount : 1
+0328 CapabilitiesHash : :SID_AND_ATTRIBUTES
+0438 LowboxNumberEntry : 0ffff950a'b3fd5d50_SEP_LOWBOX_NUMBER_ENTRY
+0440 LowboxHandlesEntry : 0ffff950a'e6f91d90_SEP_LOWBOX_HANDLES_ENTRY
+0448 PClaimAttributes : (null)
```

- 4. 转储 `LowboxHandlesEntry` 成员：

```
kd> dt ntl_sep_lowbox_handles_entry 0ffff950a'e6f91d90
+0000 HashEntry : :RTL_DYNAMIC_HASH_ENTRY
+0018 ReferenceCount : On10
+0020 PackageSize : 0ffff950a'e6f9208 Void
+0028 HandleCount : 6
+0030 Handles : 0ffff950a'e9d18490 -> 0xffffff800023cc Void
```

- 5. 有六个句柄。让我们转储它们的值：

```
kd> dq fffff950ae9d18490 6
ffff950a'e9d18490 fffffffff0023cc fffffffff01e80
ffff950a'e9d18a0 fffffffff004214 fffffffff0042c
ffff950a'e9d18b0 fffffffff002c fffffffff01834
```

- 6. 你可以看到这些句柄是内核句柄——以 `0xffffffxx` 开头。现在你可以使用 `!handle` 命令查看单个句柄。这里有两个示例：

```
kd> !handle fffff8001e80
PROCESS fffff28cd71b360
Session: 1 Id: 2c74 Peb: 3df2f00 ParentId: 2324
DirBase: 80bb8500 ObjectTable: ffff50addab7c0 HandleCount: <Data Not Accessible>
Image: windbg.exe

kd> !handle fffff80002c
PROCESS fffff28cd7b1360
SessionId: 1 Id: 27c4 Peb: 3dffb00 ParentId: 2324
DirBase: 80bb8500 ObjectTable: ffff50add7c0 HandleCount: <Data Not Accessible>
Image: windbg.exe
```

| Hash Address | Type | Name |
| --- | --- | --- |
| 23 | fffff82cb66e950 | ALPC Port |
| 376512899CCA5DE2085347 | SymbolicLink | Sessions\1\AppContainerNamedObjects\S-1-15-46627634-3793614953-270083692-180164423-2247275065-108783335-24683617 |将对象限制到特定命名空间的能力是进行沙箱访问的重要工具。本文编写时的 Windows 10 更新包含了一个名为 BNO isolation 的额外令牌能力（其中 BNO 指 BaseNamedObjects）。通过 `SEP_CACHE_HANDLES_ENTRY` 结构，TOKEN 结构中添加了一个新字段 `BnoIsolationHandlesEntry`，其类型设置为 `SepCachedNoIsolation` 而不是 `SepCachedLowbox`。要使用此功能，必须使用特殊的进程属性（详情请参见第 3 章），该属性包含隔离前缀和句柄列表。此时，使用了 Lowbox 机制，而不是 AppContainer SID 对象目录，使用了属性中指定的目录。

## 代理程序 (Brokers)

AppContainer 进程除了隐式授予的能力外，几乎没有权限；某些操作无法由 AppContainer 执行，需要帮助（这些操作对于 store 中的用户来说是不可见的，且难以管理）。某些示例包括使用常用的打开对话框选择文件或打印对话框；对于这些和其他操作，Windows 提供了称为代理的辅助进程，由系统进程 `RuntimeBroker.exe` 管理。

AppContainer 要求这些任何一个进程通过安全的 ALPC 通道与 Runtime Broker 通信，由 Runtime Broker 初始化请求的代理进程。示例包括 `%SystemRoot%\PrintDialog\PrintDialog.exe` 和 `%SystemRoot%\System32\PickerHost.exe`。

## 实验：代理程序

以下步骤显示了代理进程是如何启动和终止的：

- 1. 点击开始按钮，输入“照片”，并选择“照片”运行内置的 Windows 10 照片应用程序。
- 2. 打开进程管理器，切换到照片进程，并找到代理进程。
- 3. 在照片应用中，选择一个文件，右键点击菜单并选择打印。对话框应该打开。 ```
kd> !handle fffff8001e80
PROCESS fffff28cd71b360
Session: 1 Id: 2c74 Peb: 3df2f00 ParentId: 2324
DirBase: 80bb8500 ObjectTable: ffff50addab7c0 HandleCount: <Data Not Accessible>
Image: windbg.exe

- 4. 点击打印对话框。

第 7 章 安全

## 登录

交互式登录通过以下方式发生：

- 登录进程（Winlogon.exe）
- 用户界面进程（LogonUI.exe）
- Lsass.exe
- 一个或多个身份验证包

身份验证包是执行身份验证检查的 DLL。Kerberos 是用于域交互式登录的 Windows 身份验证包。MSV1_0 是用于本地计算机交互式登录且无法访问域控制器的 Windows 身份验证包。

Winlogon 是一个管理安全相关交互的可信进程。它协调登录，在登录时启动用户的第一个进程，并处理注销。它管理各种与安全相关的操作，包括启动 Winlogon 输入密码、更改密码以及锁定和解锁工作站。Winlogon 必须确保与安全的操作对任何活动进程不可见。例如，Winlogon 保证了不可信的进程在这些操作期间无法控制桌面，从而获取密码。

Winlogon 依赖于安装在系统上的凭据提供者来验证用户的帐户名或密码。凭据提供者是位于 DLL 内部的对象。默认提供者是 `authui`、`SmartCredentialProvider.dll` 和 `FaceCredentialProvider.dll`，分别支持密码、智能卡 PIN 和脸识别认证。允许安装其他凭据提供可以让 Windows 使用不同的用户识别方法。例如，第三方可以提供使用指纹识别设备的凭据提供者来识别用户并从加密数据库中提取密码。

为了防止凭据提供者中的 Bug导致 Winlogon 进程崩溃（由于 Winlogon 被视为关键系统进程，这会导致系统崩溃），将使用一个独立的进程 `LogonUI.exe` 来实际加载凭据提供者并向用户显示 Windows 登录界面。该进程在 Winlogon 需要向用户呈现用户界面时按需启动，并在操作完成后退出。它还允许 Winlogon 在因任何原因崩溃时重启一个新的登录 进程。

Winlogon 是唯一拦截键盘登录请求的进程。这些请求是通过 Win32k.sys 发送的 RPC 消息发送的。Winlogon 立即启动 LogonUI 应用程序以
