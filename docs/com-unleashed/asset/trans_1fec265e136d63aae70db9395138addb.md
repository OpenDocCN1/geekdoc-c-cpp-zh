
隧道 TCP 协议在每个 COM+ 连接开始时引入一种特殊握手，使其能够穿过大多数防火墙和代理。此握手（由 CIS 透明处理）之后，线路协议就是基于 TCP 的 COM。除了本章后面列出的注意事项外，这意味着：

- 该协议对客户端和服务器都是透明的。客户端代码和服务器代码都不需要修改即可使用 CIS。
- 所有基于 TCP 的 COM+ 协议服务都可用——包括 COM+ 安全性和生命周期管理（即“ping”）服务。

## 隧道 TCP 协议的限制

隧道 TCP 协议受以下限制：

- 它要求在承载可由 CIS 访问的 COM+ 对象的服务器端计算机上安装 Internet Information Server 4.0 或更高版本，因为部分 CIS 功能是使用 ISAPI 筛选器实现的。
- 由于隧道 TCP 在初始握手后由非 HTTP 流量组成，CIS 要求代理服务器和防火墙允许通过为 HTTP 打开的端口传输此类流量。

> **注意**
>
> 由于这些限制，实际上，CIS 不支持回调。例如，这意味着应用程序无法使用连接点或建议接收器机制执行通知。但是，如果 CIS 客户端可以充当 CIS 服务器并按本章后面所述进行配置，则没有任何因素会阻止客户端接收 COM+ 调用——包括回调。

## 隧道 TCP 协议概述

如果客户端配置指示应将发往服务器的 HTTP 流量通过代理路由，则客户端 COM+ 运行时环境会与该代理建立 TCP/Internet 协议 (IP) 连接。然后，它向代理发送 HTTP CONNECT 方法，请求连接到服务器主机上的端口 80。图 14.1 显示了隧道 TCP 流程的示意图。

代理与服务器主机建立 TCP/IP 连接。这假定代理已配置为在客户端所连接的端口上启用 HTTP CONNECT 方法。代理上的此端口配置有时被称为“启用 SSL 隧道”。

**图 14.1**  
*隧道 TCP 流程。*

![](img/112c2326f49d26b8d59aa054e14c5747_383_0.png)

如果客户端配置不使用代理，则 COM+ 运行时环境会与服务器主机上的端口 80 建立 TCP/IP 连接。此步骤之后，无论客户端是否使用代理，客户端都已连接到服务器主机上的端口 80（可能由代理中介）。客户端现在向服务器发送 RPC_CONNECT 命令，请求连接到服务器主机上的 DCOM 服务器。

响应 RPC_CONNECT，服务器 RPC 运行时环境（部分由 ISAPI 筛选器/扩展对实现）建立到 COM+ 服务器的本地连接。

客户端和服务器现已建立经中介的 TCP/IP 连接，并进行基于 TCP 的 COM+ 对话。

## 配置隧道 TCP 协议

表 14.1 中列出的操作系统支持隧道 TCP 协议。安装说明在相应的操作系统或 Service Pack 发行说明中提供。

**表 14.1** 隧道 TCP 的操作系统支持

| 操作系统 | 客户端 | 服务器（需要 IIS 4.0 或更高版本） |
|---|---|---|
| 带 DCOM95 1.2 的 Windows 95 | 是 | 否 |
| 带 DCOM98 1.3 的 Windows 98 | 是 | 否 |
| 带 SP4 的 Windows NT 4.0 Workstation | 是 | 否 |
| 带 SP4 的 Windows NT 4.0 Server | 是 | 是 |
| Windows 2000 Workstation | 是 | 否 |
| Windows 2000 Server | 是 | 是 |

### Windows 95 和 Windows 98 的客户端配置

CIS 要求在 Windows 95 计算机上安装 DCOM95 1.2 或更高版本。DCOM95 1.2 可从 Microsoft COM 主页 www.microsoft.com/com/default.asp 下载。必须安装 DCOM，以便 Windows 95 计算机能够参与分布式应用程序。默认情况下，不具备所需的 RPC 功能。

在 Windows 98 上，必须安装 DCOM98 1.3 或更高版本。DCOM98 1.3 随 Windows 98 OSR1 提供，也可以从 Microsoft COM 主页下载。与 Windows 95 一样，必须安装 DCOM，以便具备 RPC 功能。

> **注意**
>
> 可以从 http://www.microsoft.com/com/resources/downloads.asp 下载 DCOM95 和 DCOM98。

还需要安装另一个程序：DCOM98 配置实用程序。尽管名称如此，Windows 95 和 Windows 98 都使用同一实用程序。运行此程序时，它会将 CISCNFG 程序解压到计算机的 Windows\System 目录中。

要启用 CIS 客户端支持，请在命令行中使用以下参数运行 CISCNFG 实用程序（见图 14.2）：

```
CISCNFG tcp_http
```

![](img/112c2326f49d26b8d59aa054e14c5747_384_0.png)

**图 14.2**  
*CISCNFG 实用程序。*

CISCNFG 配置 DCOM 使用的协议，并可与以下参数一起使用：

- tcp（仅基于 TCP 的 DCOM）
- http（仅隧道 TCP）
- tcp_http（先尝试基于 TCP 的 DCOM，然后尝试隧道 TCP）

通常应使用 tcp_http，因为它同时选择 tcp 和 http。运行 CISCNFG 后，必须重新启动系统。

> **注意**
>
> 如果依赖 DCOM98 功能，有两种选择：随应用程序重新分发更新的系统文件 (DCOM98)，或引导用户访问 DCOM98 Web 版本。如果应用程序将从 Web 下载，建议引导用户访问 Web 版本，因为 DCOM98 相当大，许多用户可能已经拥有它。

### Windows NT 4.0 SP4 和 Windows 2000 的客户端配置

Windows NT 4.0 Service Pack 4 和 Windows 2000 包含 CIS 支持。

要启用 CIS，需要将隧道 TCP 协议添加到 DCOM 协议列表。可以通过执行以下步骤运行 DCOMCNFG 来修改协议列表：

- 1. 选择“默认协议”选项卡。
- 2. 使用“添加”按钮添加隧道 TCP/IP。
- 3. 重新启动系统以使此更改生效。

> **注意**
>
> 如果配置了多个协议，将尝试按它们在协议列表中出现的顺序使用它们。

### 客户端计算机代理配置

假设客户端位于代理服务器之后。如果是这样，需要确保客户端计算机已正确配置为使用代理服务器访问 Web。要将客户端配置为使用代理服务器，请打开 Internet 属性对话框的“连接”选项卡（如图 14.3 所示），或从 Internet Explorer 转到 Internet 选项。也可以通过注册表项进行设置，如后面“影响 CIS 的注册表项”一节所述。请注意，使用 HTTP 的其他应用程序（最值得注意的是 Microsoft Internet Explorer）会与 RPC 运行时环境共享此配置。

无论操作系统如何，都必须为代理服务器之后的所有客户端计算机设置代理配置。

![](img/112c2326f49d26b8d59aa054e14c5747_386_0.png)

**图 14.3**  
*HTTP 代理配置*

### Windows NT Server 4.0 上的服务器配置

CIS 要求在 Windows NT Server 4.0 计算机上安装 Service Pack 4。CIS 还要求 Internet Information Server 4.0（包括 Internet 服务管理器）正在运行。IIS 4.0 是 Windows NT 4.0 Option Pack 的一部分。

> **警告**
>
> 不应在运行 Microsoft Proxy Server 的计算机上安装 CIS。CIS 与 Microsoft Proxy Server 端口配置冲突。

在 Inetpub 目录下创建 RPC 子目录。例如，在命令提示符下，键入以下内容：

```
md c:\inetpub\rpc
```

在以下说明中，此目录将称为 `%inetpub%\rpc`。

将 rpcproxy.dll 从 Windows 系统目录复制到 `%inetpub%\rpc`。例如，在命令提示符下，键入以下内容：

```
copy %windir%\system32\rpcproxy.dll c:\inetpub\rpc
```

为创建的目录创建虚拟根。为此，请执行以下操作：

- 1. 从“开始”菜单中，选择“程序”，指向 Windows NT 4.0 Option Pack、Microsoft Internet Information Server，然后单击 Internet 服务管理器。
- 2. 在控制台树（左窗格）中，选择 `Console Root/IIS/<machine name>/Default Web Site`。
- 3. 右键单击“默认 Web 站点”，单击“新建”，然后单击“虚拟目录”。在“新建虚拟目录向导”中，输入以下内容：
  - 用于访问虚拟目录的别名：`RPC`
  - 物理路径：`%inetpub%\rpc`
  - 权限：`Execute Access`

不要关闭 Internet 服务管理器。将默认 Web 站点的连接超时更改为 5 分钟。为此：

- 1. 在控制台树（左窗格）中，选择 `Console Root/IIS/<machine name>/Default Web Site`。
- 2. 右键单击“默认 Web 站点”，然后单击“属性”。
- 3. 在“默认 Web 站点属性”对话框中，选择“Web 站点”选项卡。
- 4. 将连接超时更改为 300。
- 5. 单击“确定”。不要关闭 Internet 服务管理器。
- 6. 安装 RPC 代理 ISAPI 筛选器。在控制台树（左窗格）中选择 `Console Root/IIS/<machine name>`，右键单击计算机名称，单击“属性”，选择“主 WWW 服务属性”的“编辑”，选择“ISAPI 筛选器”选项卡，选择“添加”，然后输入以下内容：
  - 筛选器名称：`Rpcproxy`
  - 可执行文件：`%inetpub%\rpc\rpcproxy.dll`

