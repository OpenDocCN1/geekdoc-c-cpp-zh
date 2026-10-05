
5. 选择进程映像（Process Image）并勾选完整性级别（Integrity Level）复选框。对话框应类似于此处所示：

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_645_0.png)

6. Process Explorer 显示系统中进程的完整性级别。对于 AppContainer（MicrosoftEdge.Edge）进程，我们应该在提升权限的命令提示符看到记事本（Notepad）进程。还要注意，系统和进程运行在更高的完整性级别：System。

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_645_1.png)

## 第 7 章 安全 629

每个进程都有一个完整性级别，它表示在令牌（token）中并根据以下规则传播：

- 进程通常继承其父进程的完整性级别（这意味着提升权限的命令将产生其他提升权限的进程）。
- 如果子进程所属的可执行映像文件对象具有完整性级别，且父进程的完整性级别为中等或更高，则子进程将继承两者中较低的一个。
- 父进程可以创建一个显式完整性低于其自身的子进程。要实现这一点，它使用 `DuplicateToken` 复制其自身的访问令牌，使用 `SetTokenInformation` 将新令牌中的完整性级别更改所需的级别，然后使用该新令牌调用 `CreateProcessAsUser`。

表 7-3 列出了与进程关联的完整性级别，但哪些对象的完整性级别存储在它们的安全描述符（security descriptor）中，这种结构被称为强制标签（mandatory label）。

为了支持从之前的 Windows 版本进行迁移（其注册表项和文件不包含完整性级别信息），并为了方便应用程序开发人员工作，所有对象都有一个隐式的完整性级别，以避免手动指定。这种隐式完整性级别为中等（medium），这意味着对象上的强制策略（稍后描述）将对以低于中等的完整性级别访问该对象的令牌（tokens）进行执行。

当进程创建对象而未指定完整性级别时，系统会检查令牌中的完整性级别。对于级别为中等或更高的令牌，对象的隐式完整性级别保持为中等。然而，当令牌包含低于中等的完整性级别时，对象将以与令牌中级别匹配的显式完整性级别创建。

由高或系统完整性级别进程创建的对象本身具有中等完整性级别，用户可以禁用它并继承创建者的完整性级别，这允许禁用了 UAC 的管理员操作。如果完整性级别禁用了 UAC 随后将其启用可能会失败，因为管理员将无法修改任何在高完整性级别创建的注册表设置或文件。对象也可以具有由系统或对象创建者设置的显式完整性级别。例如，内核在创建进程、线程和作业时赋予它们显式完整性级别。为这些对象分配完整性级别的目的是防止同一用户但完整性级别较低的进程访问这些对象并修改其内容或行为（例如 DLL 注入或代码修改）。

除了该完整性级别外，对象还有强制策略，它定义了根据完整性级别划分的实际保护级别。可能的可能的类型，如表 7-4 所示。完整性级别和强制策略存储在同一个 ACE（访问控制项）中。

# 表 7-4 对象强制策略

| 策略 | 存在于，由 | 描述 |
| :--- | :--- | :--- |
| No-Write-Up（禁止向上写） | 所有对象上隐式存在 | 用于限制来自较低完整性级别进程对对象的写入访问权限。 |
| No-Read-Up（禁止向上读） | 仅存在进程对象上 | 用于限制来自较低完整性级别进程对对象的读取访问权限。在进程对象上的特定用途是通过阻止外部进程读取地址空间的读取来防止信息泄露。 |
| No-Execute-Up（禁止向上执行） | 仅存在实现 COM 类的二进制文件上 | 用于限制来自较低完整性级别进程对对象的执行访问权限。在 COM 类上的特定用途是限制 COM 类的启动激活（launchactivation）。 |

# 实验：查看对象的完整性级别

你可以使用 Sysinternals 的 AccessChk 工具显示系统上对象（如文件、进程和注册表项）的完整性级别。这里有一个展示 Windows 中 LocalLow 目录目的的实验：

- 在命令提示符窗口中浏览到 `C:\Users\<UserName>`，其中 `<username>` 是你的名字。
- 尝试对 AppData 文件夹运行 AccessChk，如下：
  `C:\Users\<UserName> accesschk -v appdata`
- 注意输出中 Local 和 LocalLow 子文件夹之间的差异，在此显示：
  `C:\Users\<UserName>AppData\Local`
  Medium Mandatory Level (Default) [No-Write-Up]
  `[...]`
  `C:\Users\<UserName>AppData\LocalLow`
  Low Mandatory Level [No-Write-Up]
  `[...]`
  `C:\Users\<UserName>AppData\Roaming`
  Medium Mandatory Level (Default) [No-Write-Up]
  `[...]`
- 注意到 LocalLow 目录的完整性设置为 Low（低），而 Local 和 Roaming 目录的完整性级别为 Medium（默认）。默认意味着系统正在使用隐式完整性级别。
- 向 AccessChk 传递 `-e` 标志以便显示显式完整性级别。如果你再次对 AppData 文件夹运行该工具，你会发现只显示了 LocalLow 的信息。

`-o`（对象）、`-k`（注册表项）和 `-p`（进程）标志允许你指定文件或目录以外的内容。

# 令牌 (Tokens)

SRM 使用名为令牌（token）的对象来标识进程或线程的安全上下文。安全上下文包含了帐户、组和关联的权限。令牌还包括会话 ID、完整性级别以及 UAC 状态（我们稍后会描述权限）。

在登录过程中（稍后描述），Lsass 会创建一个表示登录用户的初始令牌。它决定了登录用户是否为强大组成员或拥有强大权限。检查的组包括：

- Built-In Administrators
- Certificate Administrators
- Domain Administrators
- Enterprise Administrators
- Policy Administrators
- Schema Administrators
- Domain Controllers
- Enterprise Read-Only Domain Controllers
- Read-Only Domain Controllers
- Account Operators
- Backup Operators
- Cryptographic Operators
- Network Configuration Operators
- Print Operators
- System Operators
- RAS Servers
- Power Users
- Pre-Windows2000

如果存在这些组或权限，Lsass 会为用户创建一个受限令牌（也称为过滤管理员令牌），并为两者创建一个登录会话。检查的权限：

- SeBackupPrivilege
- SeCreateTokenPrivilege
- SeDebugPrivilege
- SeImpersonatePrivilege
- SeLabelPrivilege
- SeLoadDriverPrivilege
- SeRestorePrivilege
- SeTakeOwnershipPrivilege
- SeTcbPrivilege

这些权限将在本章后的“权限”部分详细介绍。

由于子进程默认继承创建者的令牌副本，因此会话中的所有进程都运行在相同的令牌下。你也可以通过 Windows LogonUser 生成令牌。通过将令牌传递给 `CreateProcessAsUser` 函数，你可以创建一个在通过 LogonUser 登录的安全上下文内运行的进程。`CreateProcessWithLogon` 函数将这些合并到一个调用中，这就是 Runas 命令通过备用令牌启动进程的方式。
