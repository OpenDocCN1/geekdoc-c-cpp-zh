
为了保护 .cab 文件，尤其是在可通过 Internet 访问的站点上，建议使用标准 HTTP 加密和身份验证方案保护下载页面所在的虚拟目录。

## 3. 使用存储卡

在许多情况下，应用程序需要与 SQLCE 数据库或其他软件一起部署。因此，通过 Internet 或安全连接部署此类应用程序可能既耗时又庞大。出于这些原因，应用程序也可以部署在内存存储卡（例如 Compact Flash 卡）上；然而，Pocket PC 设备并不要求用户在将存储卡插入设备后执行 .cab 文件，而是包含 Autorun 功能。借助此功能，当存储卡插入设备时，Pocket PC 会在映射到设备处理器类型的文件夹中查找名为 Autorun.exe 的可执行文件。例如，如果处理器类型为 ARM，它将在存储卡上查找文件 \Storage Card\ARM\Autorun.exe。找到后，该可执行文件会被复制到 \Windows 文件夹，并使用安装参数执行。同样，当从设备中取出卡时，会使用卸载参数启动同一个可执行文件。

## 4. 使用文件共享

与通过网站部署一样，.cab 文件可以放在网络 (LAN) 共享上，并从设备上的文件资源管理器访问，既可以通过 802.11 无线访问，也可以在使用 ActiveSync 3.5 及更高版本安全连接时访问。并且，与通过 Web 部署一样，可以保护该共享，用户必须输入有效凭据才能访问文件。同样，此选项使用户无需为了安装软件而始终安全地持有设备。

### 28.5.2.2 设置自动部署

- Compact Framework 应用程序与使用桌面 Framework 编写的应用程序一样，可以编写为自动更新。自动更新是指应用程序定期或在每次调用时检查文件共享或网站，以获取其程序集的较新版本，并动态下载它们。此技术对于使用私有程序集的应用程序尤其有效，因为应用程序可以划分为各种功能，每个功能都存放在单独的程序集中，因此可以独立更新。创建自动更新应用程序的明显好处是，它减轻了用户保持应用程序最新的负担。

### 28.5.2.3 在设备上部署应用程序

可通过以下任一方式选择在设备上部署，即：

- 在 Visual Studio .NET 工具栏上，从“部署设备”组合框中选择“Pocket PC Device”。
- 在“项目属性”对话框的“设备”页中，从“部署设备”组合框中选择“Pocket PC Device”。
- 在“属性”窗口中，将项目的“Deployment Device”属性设置为“Pocket PC Device”。

### 28.5.2.4 在设备上部署应用程序的要求

- 使用 Visual Studio .NET 构建的应用程序要求目标设备上驻留 .NET Compact Framework。此外，如果应用程序使用 SQL Server CE，则需要安装 SQL Server CE 组件。
- 安装例程会处理所有这些要求。它可能需要包含多个 CAB 文件：一个用于应用程序，第二个用于 .NET Compact Framework，以及 SQL Server CE 的 CAB 文件。

### 28.5.2.5 为 .NET Compact Framework 应用程序创建桌面安装程序

- 如果应用程序安装将从桌面 PC 通过对接底座在设备上执行，则安装过程会变得稍微复杂一些。在这种情况下，需要两个安装程序：一个用于桌面 PC，一个用于设备。设备安装程序就是 CAB 文件。桌面安装程序是一个可执行文件，它承担两项功能。首先，它将 CAB 文件复制到桌面 PC 上。其次，它启动 Application Manager (CeAppMgr.exe)。然后，Application Manager 接管，将 CAB 文件复制到设备，并随后启动安装过程。
- Application Manager 负责在设备上添加和删除应用程序，以及从发起安装的 PC 上删除应用程序文件。可使用 .INI 文件向 Application Manager 提供安装说明。
- 可以为任何允许将 CAB 文件复制到 PC 并随后启动 Application Manager 的应用程序创建桌面安装程序。**InstallShield** 和 **Wise** 两家公司提供具备此功能的商业级安装开发包。**Spb Software House** 提供一款名为 EZSetup 的免费安装产品。虽然此应用程序不如 InstallShield 和 Wise 的产品稳健，但对于大多数安装场景而言运行良好。
- 应注意，在编写自己的桌面安装程序时，必须找到 Application Manager 在安装 PC 上的位置。Application Manager 的完整名称和路径存储在注册表值 `HKLM\\Software\\Microsoft\\Windows\\CurrentVersion\\App Paths\\CEAppMgr.exe` 中。

## 28.6 .NET Compact Framework - 网络

对于使用 .NET 开发通过网络通信的应用程序，联网所需的类属于 System.Net 命名空间。它包含用于处理 Internet 通信的类，其对象支持代理服务器、IP 地址、DNS 名称解析、网络数据流，以及用于处理可插拔协议（如超文本传输协议 (HTTP)）的特定类。

### 28.6.1 System.Net 命名空间

| 名称 | 对象类型 | 描述 |
|---|---|---|
| AuthenticationManager | 类 | 管理身份验证模型 |
| Authorization | 类 | 处理发往服务器的授权消息 |
| Dns | 类 | 处理域名解析 |
| EndPoint | 类 | 用于标识网络地址的抽象类 |
| GlobalProxySelection | 类 | 处理 HTTP 请求的默认代理 |
| HttpContinueDelegate | 委托 | 用于 HTTP 请求的回调 |
| HttpStatusCode | 枚举 | 用于 HTTP 请求的状态代码 |
| HttpVersion | 类 | 处理 HTTP 请求支持的版本号 |
| HttpWebRequest | 类 | 处理 HTTP 请求 |
| HttpWebResponse | 类 | 处理 HTTP 请求的响应 |
| IAuthenticationModule | 接口 | 用于 Web 身份验证的接口 |
| ICertificatePolicy | 接口 | 验证服务器证书的接口 |
| ICredentials | 接口 | 用于处理 Web 客户端身份验证的接口 |
| IPAddress | 类 | 处理 IP 寻址 |
| IPEndPoint | 类 | 处理 IP 地址和端口号 |
| IPHostEntry | 类 | 处理 Internet 主机地址信息 |
| IrDAEndPoint | 类 | 处理与另一台设备的红外连接 |
| IWebProxy | 接口 | 用于处理代理请求的接口 |
| IWebRequestCreate | 接口 | 用于处理新 WebRequest 实例的接口 |
| NetworkCredential | 类 | 处理网络用户名和密码 |
| ProtocolViolationException | 类 | 网络协议错误发生时使用的异常 |
| ServicePoint | 类 | 处理 HTTP 的连接管理 |
| ServicePointManager | 类 | 处理 ServicePoint 类的集合 |
| SocketAddress | 类 | 存储来自 EndPoint 类的信息 |
| WebException | 类 | 访问网络发生错误时使用的异常 |
| WebExceptionStatus | 枚举 | 与 WebException 类一起使用的状态代码 |
| WebHeaderCollection | 类 | 处理网络请求或响应的协议标头 |
| WebProxy | 类 | 处理 HTTP 代理设置 |
| WebRequest | 类 | 处理对 URI 的请求 |
| WebResponse | 类 | 处理对 URI 的响应 |

### 28.6.2 TCP/IP 地址

设备使用 IPv4 地址来指定其唯一的主机和子网地址，Pocket 设备同样使用该地址在 TCP/IP 网络上通信。在 Compact Framework 中管理 Internet 地址所需的所有方法和属性都由 System.Net.IPAddress 类处理。

