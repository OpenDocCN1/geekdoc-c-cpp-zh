
- c. CUPS 管理 > 存在 (CUPS Administration > Presence)
- d. CUPS 管理 > 应用 (CUPS Administration > Application)

### 基础主题

### 描述 CUCM 的 GUI 和 CLI

通过 HTTPS 访问 CUCM 的 Web 界面是可能的（命令行则使用 Secure Shell [SSH]）。共有六个独立的界面：

- Cisco 统一通信管理器管理 (`https://<node_ip>/cmadmin`)
- Cisco 统一服务性 (`https://<node_ip>/ccmservice`)
- 灾难恢复系统 (`https://<node_ip>/drf`)
- Cisco 统一操作系统管理 (`https://<node_ip>/cmplatform`)
- Cisco 统一报告 (`https://<node_ip>/cucreports`)
- 命令行界面 (CLI)

除了 CLI 之外，每个界面都可以通过其自己的 URL 访问。

每个界面（CLI 除外）都可以可以通过其自己的 URL 访问，也可以通过页面右上角的导航下拉菜单并点击旁边的 Go 按钮来访问。

安装时定义的平台管理帐户和密码用于访问灾难恢复和操作系统管理页面。同样，在安装期间定义的应用程序帐户和密码用于访问 CM 管理、服务性和统一报告界面。可以创建额外的账户并分配管理权限，以便它们也能访问这些界面。

在安装期间，定义了一个额外的密码作为安全密码。此密码需要连接到发布器数据库（用于订阅服务器或其他使用发布器数据库的统一通信应用）。

## Cisco 统一通信管理器管理界面

CM 管理界面（如图 8-1 所示）包含以下内容的九个菜单（对每个菜单可以执行的任务进行了简要描述；这绝不是详尽列表，还有许多未列出的任务）：

- 系统菜单：包括配置 CM 组、存在组、设备移动组、设备池、区域、位置、企业和业务参数、可生存远程电话系统 (SRST) 等其他内容的配置任务。
- 呼叫路由菜单：包括定义呼叫路由系统、呼叫寻路 (Call Hunting)、控制类 (Class of Control)、对讲机 (Intercom) 以及如呼叫停留 (Call Park)、呼叫接听 (Call Pickup) 等功能。
- 媒体资源菜单：在此菜单中，可以定义如等待等待音乐 (MOH)、公告器 (annunciator)、媒体终端点和转码器，并管理 hold-misc 文件。
- 高级功能菜单：在此菜单下，配置语音信箱集成、媒体引擎配置、跨集群扩展移动和 VPN 功能。

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_250_0.png)

### 图 8-1 CUCM 管理界面

- 设备菜单：配置网关、分机、IP 电话等设置。
- 应用菜单：访问语音信箱。
- 用户菜单：创建并修改平台帐户。
- 批量菜单：在集群中对服务器（例如，IP 电话）进行操作。
- 帮助菜单：提供帮助。

安装时定义的平台管理帐户和密码用于访问灾难恢复和操作系统管理页面。同样，在安装期间定义的应用程序帐户和密码用于访问 CM 管理、服务性和统一报告界面。可以创建额外的账户并分配管理权限，以便它们也能访问这些界面。

在安装期间，定义了一个额外的密码作为安全密码。此密码需要连接到发布器数据库（用于订阅服务器或其他使用发布器数据库的统一通信应用）。

### 统一服务性界面

C 统一服务性界面（如图 8-2 所示）提供了五个菜单，每个菜单都可以执行：

- 告警菜单：访问告警并监控性能。
- 跟踪菜单：跟踪数据并排除问题。

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_251_0.png)

- 图 8-2 统一服务性界面
- SNMP 菜单：访问 SNMP 和连接性。
- 帮助菜单：提供帮助。

什么是功能服务和网络服务的区别？功能服务可以根据服务器进行激活（例如，CUCM、TFTP 和 DNS）。网络服务可以被停用，但可以启动、停止和重启。

## 统一操作系统管理界面

Cisco 统一操作系统管理界面（如图 8-3 所示）允许管理员监控并与 Linux 操作系统交互。在此可以执行的操作包括：

- 监控硬件（CPU、磁盘）
- 检查和升级软件版本
- 修改 IP 地址
- 管理网络时间协议 (NTP) 服务器地址
- 管理安全性，包括 IPSec 和数字证书
- 创建 TAC 协助帐户
- Ping 其他设备

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_252_0.png)

- 图 8-3 统一操作系统管理界面

### 灾难恢复系统

灾难恢复系统 (DRS) 提供备份（带有调度程序）和恢复能力。访问此界面使用安装时定义的平台帐户（OS 管理界面）。可以为其他人创建额外的帐户。

备份可以写入本地 DLT 磁带或 SFTP 服务器。提供了调度程序用于自动备份，也可以选择立即启动备份。可以执行单个服务器或全集群备份。

### 统一报告界面

统一报告界面提供了访问系统报告的简化方法。这些报告从日志中收集信息并格式化为简单、实用的报告。数据从集群（发布者和订阅者）收集，提供摘要信息并突出可能影响运行的异常。该界面还会警告特定报告可能会影响服务器运行并花费过多的时间。

**注意：** CLI 是一个强大的接口。按回车键会立即提交命令，系统极少要求你确认操作意图。这意味着 CLI 将完全按照你的指令执行操作，包括可能对服务器的运行产生负面影响。。在使用 CLI 之前，请审阅《CLI 管理指南》并确保你输入的命令准确无误。

### CUCM 中的用户管理：角色和组

CUCM 应用定义了一种一致且简单的方法，用于向用户分配（并限制）管理权限。用户被分配到组；组被分配角色；角色定义了应用程序的权限。接下来的章节将提供该结构的详细信息。

### 角色

角色定义了对应用程序中资源的一组权限。资源可以是 CUCM 管理页面、报告工具或 CUCM 网页中的某部分内容。为每个资源分配的权限可以是以下其中之一：

- **无访问权限（No Access）：** 角色拒绝访问资源；例如，网页将加载，但取而代之的是错误。
- **读取（Read）：** 角色允许显示资源但不可进行编辑：例如，网页可以加载，但无法修改任何字段或设置。不会出现添加、插入、删除或更新等按钮。
- **更新（Update）：** 角色允许对资源进行完全访问，包括编辑和修改（以及适用的删除）。

其他应用程序（例如，Cisco Unified Serviceability 或 Cisco Extension Mobility）定义了与应用程序相关且特定的访问权限。

- CUCM 管理
- CUCM 服务管理
- Cisco 计算机电话接口 (CTI)
- CUCM 管理 XML (AXL) 数据库
- Cisco Extension Mobility
- CUCM 用户

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_254_0.png)

图 8-4 显示“查找和列出角色”页面。

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_255_0.png)

**图 8-4** CUCM 中的角色列表。

## 组

CUCM 应用默认定义了 24 个标准组。这些组与或多个标准角色关联，通过 CUCM 管理页面为各种应用程序提供不同层级的权限。大多数组默认都有成员；当在 CUCM 中创建或关联用户时，这些账户可能会添加到一个或多个组中。用户账户通过成为组的成员来继承角色所定义的权限。

通过角色，这些场景下的管理需求很可能通过使用标准组和角色关联来得到满足。如果情况并非如此，可以创建自定义组并与标准角色或自定义角色关联，以精确满足管理需求。

由于用户可以是多个组的成员，并因此继承多个层级的权限，理解冲突角色权限的影响至关重要。考虑以下场景：

Bob 是组 A 和组 B 的成员。组 A 与角色 X 关联，该角色为应用程序资源提供更新权限。组 B 与角色 Z 关联，该角色为同一资源提供读取权限。问题是：Bob 对该资源的有效权限是什么？

答案由“重叠用户组和角色的企业参数有效访问权限”决定。默认设置为“最大”（Maximum），意味着默认情况下，Bob 拥有更新权限。该参数可以更改为“最小”（Minimum），将 Bob 的有效权限改为“读取”。

**注意：** 如所述所述更改企业参数会影响除标准 CCM 超用户组以外的所有组（这是最高权限组，其唯一的默认成员是安装在 [例如, CCMAdministrator] 的 CUCM 应用管理员）。

有趣的是，“最大”权限的默认设置与大多数网络应用程序和操作系统的默认设置相反。只要管理员意识到该设置的影响和重要性，无论选择哪种，这都不算问题。

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_256_0.png)

## 图 8-5 CUCM 中的用户组列表

## 描述 CUC GUI 和 CLI

CUC 提供了以下六种管理接口：

- Cisco Unity Connection 管理 (`https://<ip-address>/cuadmin`)
- Cisco Unified Serviceability (`https://<ip-address>/ccmservice`)
- Cisco Unity Connection 服务管理 (`https://<ip-address>/cuservice`)
- Cisco 统一统合操作系统管理 (Cisco Unified Operating System Administration)(`https://<ip-address>/cmplatform`)
- 灾难恢复系统 (Disaster Recovery System)(`https://<ip-address>/drf`)
- 命令行界面 (Command-Line Interface)

### Cisco Unity Connection 管理

CUC 管理界面使用类似于 Windows 资源器的树结构，使查找并导航到所需页面变得简单。主菜单项在以下章节中描述；更详细的信息见第 13 章“与 Cisco Unity Connection 集成语音邮件”。

- **用户（Users）：** 提供对本地用户数据库的访问权限，用于创建或编辑用户。此处还列出了用户导入和同步菜单选项。
- **服务类别（Class of Service）：** 定义用户可用的功能，包括许可功能和高级功能，并可以应用其他用户交互限制。服务类别是控制用户与 CUC 交互的一种灵活且强大的方法，特别是对于许可功能。创建的服务类别数量没有限制，因此可以构建多样化且特定的服务类别来覆盖任何组合需求。
- **模板（Templates）：** 提供了一种为用户、联系人或通话处理器（Call Handlers）定义通用设置的方法。在创建这三种类型对象的新对象时，选择合适的模板可以应用所有除每个对象特定的信息以外的所有信息，使过程更快速、更准确。
- **联系人（Contacts）：** 系统联系人是一个关联了邮箱箱的用于与 CUC 交互的账户。也许某位顾问在客户办公室工作并每天与客户团队互动，但在其公司办公室的系统上有一个邮箱箱。系统联系人可以为 CUC 用户提供一个发送消息的目录，消息将中继到顾问公司办公室的邮箱箱。
- **分配列表（Distribution Lists）：** 允许将一条消息投递给多个用户。分配列表可以根据需要创建。服务类别设置可以防止用户使用系统分配列表。
- **通话管理（Call Management）：** 定义通话处理器。通话处理器是 CUC 的功能结构，可以配置为接听电话、播放问候语、路由通话和接收留言。特殊的通话处理器包括*目录处理器（Directory Handlers）*，它允许呼叫者搜索目录并向所选用户拨打电话或留言留言；以及*访谈处理器（Interview Handlers）*，它通过通过播放一系列录制消息与呼叫者进行交互。
- **消息存储（Message Storage）：** 允许设置邮箱箱配额，强制限制邮箱箱大小。
- **网络（Networking）：** 在数字网络或 VPIM 环境中配置多个 CUC 系统。
- **拨号计划（Dial-Plan）：** 提供创建分区（Partitions）和搜索空间（Search Spaces）以控制可见性和访问。这对于向用户隐藏部分 CUC 功能非常有用。
- **系统设置（System Settings）：** 系统设置子菜单提供全局配置。此处总结了部分子菜单：
  - **许可（Licenses）：** 跟踪并显示系统可用的许可。许可与服务器网卡的 MAC 地址绑定。
  - **假期计划（Holiday Schedules）：** 三个系统计划（所有时间、工作日和语音识别计划）可以修改但不能删除；可以添加新计划以自定义系统。
  - **外部服务（External Services）：** CUC 可以配置为访问 Microsoft Exchange 持有的日历和联系人信息。这些信息随后可以整合到个人通话路由中。同样，网络中有 Cisco Unified MeetingPlace，CUC 可以从服务器提取会议信息，以便用户从通讯助手或电话查看并加入会议。
  - **LDAP：** 子菜单允许配置 LDAP 同步（用户导入）和 LDAP 验证（密码验证重定向到 LDAP）。
  - **SMTP：** CUC 可以通过电子邮件通知用户新消息；子菜单配置内置 SMTP 服务器的细节。
  - **高级（Advanced）：** 在高级子菜单下有多个配置子菜单，包括 SMPP 入口，通过该入口可以配置 CUC 向手机发送短消息点/短信通知。
- **电话集成（Telephony Integrations）：** 列出并配置与 CUC 集成的电话系统、端口组和端口。
- **工具（Tools）：** 包括批量管理接口（Bulk Administration Interface）和任务管理（自动化维护和故障排除）系统。

图 8-6 显示 CUC 的主页。

## Cisco Unity Connection 服务管理

CUC Unified Serviceability 应用与 CUCM 中同名的应用程序相似。CUC 提供了另一个名为 Cisco Unity Connection Serviceability 的应用程序，尽管名称相似，但功能非常不同。CUC Serviceability 主要是一个故障排除工具，具有定义告警、跟踪和日志的工具，以及针对 CUC 特有功能服务的控制（激活/禁用、启动/停止/重启）。如果使用了主备备冗余集群对，此处提供了管理集群的工具。这里还有一个报告接口。

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_259_0.png)

### 图 8-6 CUC 管理主页

#### 描述 Cisco Unified Presence Server 的 GUI 和 CLI

Cisco Unified Presence Server (CUPS) 提供了五个管理接口：

- [Cisco Unified Presence Administration](https://<ip-address>/cupadmin)
- [Cisco Unified Serviceability](https://<ip-address>/cmservice)
- [Cisco Unified Operating System Administration](https://<ip-address>/cmplatform)
- [Disaster Recovery System](https://<ip-address>/drf)
- 命令行界面 (CLI)

与其他 CUCM 和 CUC 类似，在平台管理员（Platform Administrator）中定义的账户默认是唯一可以登录 OS  way界面、DRS 和 CLI 接口的账户。应用程序管理（Application Administration）账户默认是唯一可以登录 CUPS 管理和统一可用性（Unified Serviceability）接口的账户。可以根据需要创建额外的应用程序和平台管理账户。

## Cisco Unified Presence Administration 界面

CUPS 管理菜单包含以下内容：
