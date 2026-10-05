

# 本地安全策略

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_776_0.png)

**图 7-33** Appocker 和 SRP 策略共存在同一个二进制文件（AppIdSvc.dll）中，该文件运行在 SvHost 进程内。

AppID 请求注册表更改以监控该键值下的更改，这些更改由组策略对象（GPO）或“本地安全策略” MMC 插入程序中的 Appocker UI 界面写入。当检测到更改时，AppID 服务会触发用户任务（AppIDPolicyConverter.exe），然后将其将其翻译为二进制格式的 ACES 和 SDDL 字符串，这些字符串将由用户态和内核态的 AppID 以及 AppL 组件进行审计。该任务将翻译后的规则存储在 HKLM\SYSTEM\CurrentControlSet\Control\Srp\Gp 下。此键仅允许系统（System）和管理员（Administrators）写入，对于经过验证的用户是只读的。用户态和内核态的 AppID 组件都会从注册表中读取翻译后的规则。该服务还会监控本地计算机信任证书存储区，并调用用户态（AppCertStoreCheck.exe）每天重新验证一次证书，并在证书存储发生任何更改时重新验证。AppID 内核态驱动程序（%SystemRoot%\System32\driversAppID.sys）通过 APPID_POLICY_ 由 AppID 服务通知规则更改。

管理员可以使用事件查看器查看系统事件日志，跟踪哪些应用程序被允许或拒绝（在配置好 Appocker 并启动服务后）。见图 7-34。

# 事件查看器

| 级别 | 日期和时间 | 源 | 事件 ID | 类别 |
|---|---|---|---|---|
| 信息 | 12/12/2016 12:26:19 | AppLock | 8002 | 无 |
| 信息 | 12/12/2016 12:26:03 | AppLock | 8001 | 无 |
| 信息 | 12/12/2016 12:26:38 | AppLock | 8001 | 无 |

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_777_0.png)

图 7-34 事件查看器 AppLock 允许和拒绝访问各种应用程序。事件 ID 8004 表示拒绝；8002 表示允许。

AppID、AppLock 和 SRP 的实现方式有些模糊，并违反了严格的分层设计，各种逻辑组件共存在同一个可执行文件中，且命名并不如所愿的那样一致：

AppID 服务以 `LocalService` 身份运行，以便它可以访问系统上的受信任根证书存储区。这使得它能够执行证书验证。AppID 服务负责以下工作：

- 验证发布者证书
- 将新证书添加到缓存中
- 检测 AppLock 规则更新并通知 AppID 驱动程序

AppID 驱动程序执行大部分 AppLock 功能，并依赖 AppID 服务的通信（通过 `DevIcToControl1` 请求），因此设备对象受 ACL 保护，仅授予 `NT Service\AppIDsvc`、`LOCAL SERVICE` 和 `BUILTIN\Administrators` 组访问权限。因此，驱动程序可能会被恶意软件伪造。

当驱动程序首次加载时，它通过调用 `PsSetCreateProcessNotifyRoutineEx` 触发进程创建回调。当调用通知路由时，它会传递一个 `PPS_CREATE_NOTIFY_INFO` 结构（描述正在创建的进程）。然后它收集标识可执行映像的 AppID 属性并将其写入进程令牌中。随后，它检查未公开的 `SeSprAccessCheck`，该函数会写入进程令牌和条件 ACE AppLock 规则，并确定是否允许进程运行。如果不允许进程运行，驱动程序会在 `PPS_CREATE_NOTIFY_INFO` 结构的 `Status` 字段写入 `STATUS_ACCESS_DISABLED_BY_POLICY_OTHER`，导致进程创建被取消（以及进程的最终完成状态）。

为了执行 DLL 限制，镜像加载器在每次向进程加载 DLL 时，都会向 AppID 驱动程序发送 `DeviceIoControl` 请求。然后驱动程序会根据 AppLocker 的条件 ACE 检查 DLL 的身份，就像检查可执行文件一样。

> 注意：对每个 DLL 加载都执行这些检查是非常耗时的，用户可能会察觉到。因此，DLL 规则通常是禁用的，必须通过“本地安全策略”插入程序中 AppLocker 属性页的“高级”选项卡显式启用。

脚本引擎和 MSI 安装程序已过修改，以便在每次打开文件时都调用用户态 SRP API，以检查该文件是否允许打开。用户态 SRP API 调用 AuthZ API 来执行条件 ACE 检查。

# 软件限制策略

Windows 包含一种名为“软件限制策略”（SRP）的用户态机制，允许管理员控制映像和脚本在系统上的执行方式。如图 7-35 所示，本地安全策略编辑器中的“软件限制策略”节点是机器代码执行策略的管理界面，尽管使用域策略也可以实现针对特定用户的策略。

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_778_0.png)

图 7-35 软件限制策略配置。

“软件限制策略”节点下显示了几个全局策略设置：

- **强制**：此策略配置是否将限制应用于库（例如 DLL）。
- **指定的文件类型**：此策略规定哪些扩展名被视为可执行文件。
- **信任的发布者**：此策略控制哪些发布者是受信任的。

在配置特定脚本的策略时，管理员可以通过路径、哈希值或数字证书间接让系统识别并阻止执行。

SRP 的强制执行发生在各种组件中，这些组件被视为包含执行代码。以下是某些组件：

- `Kernel32.dll` 中的系统调用强制执行。
- `Ntdll`` 中的 DLL 加载强制执行。
- Windows 命令行提示符强制执行批处理。
- Windows 脚本主机（`cscript.exe`、`wscript.exe` 和 `scrobj.dll`）强制执行。
- PowerShell 宿主（`PowerShell.exe`）。

这些每个组件都通过读取注册表 `HKLM\Software\Policies\Safer` 中的 `Enabled` 值来决定是否启用强制执行。如果匹配，默认策略（设置为 1 时）将决定是否允许执行。

软件限制策略是防止未经授权的代码和脚本的强大工具，但前提是应用得当。除非默认策略设置为禁止，否则用户可以对映像进行微调，导致哈希值无法识别，或将其复制到其他位置。

# 实验：观察软件限制策略的执行

你可以通过观察尝试执行禁用映像时的注册表访问来间接查看 SRP 的执行。

1. 运行 `secpol.msc` 打开本地安全策略编辑器并导航到“软件限制策略”。
2. 如果没有定义策略，从右键菜单中选择“新建策略”。
3. 为 `%SystemRoot%\System32\Notepad.exe` 创建基于路径的禁止规则（“其他规则”节点）。
4. 运行 Process Monitor 并为 `Safer` 设置路径过滤器。
5. 打开命令行提示符并在提示符中运行 Notepad。

运行 Notepad 的操作应该导致一个提示无法执行该程序的消息，并且 Process Monitor 应显示命令行提示符（cmd.exe）正在查询本地策略。

