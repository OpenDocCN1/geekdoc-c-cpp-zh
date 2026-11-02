

该能力是网络能力，而不是与 Internet 相关的能力。

**注意** 如果将要使用文件选择器（见第 11 章）让用户浏览本地网络，则不需要 *专用网络* 能力。只有当你需要直接以编程方式连接这些资源时，才需要该能力。

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_160_0.png)

**图 4-1** 清单中的其他网络能力。

### 侧边栏：Localhost 环回

无论清单中声明了哪些能力，Windows 商店应用都会阻止本地环回，即使用 http://localhost URI。安装了开发人员许可证的计算机属于例外，正如本章“后台传输”一节中的“侧边栏：使用 Localhost”所述（我们将在那里的示例中使用它）。此例外仅用于简化开发期间在同一台计算机上调试应用和服务的过程。你可以在 Visual Studio 中通过“项目 > 属性页”对话框中的“调试 > 允许本地网络环回”来禁用此许可，这样可以帮助你以普通用户所体验的方式测试应用。

## 网络信息（网络对象清单）

无论涉及哪种网络，关于该网络的一切信息都可以通过 `Connectivity.NetworkInformation` 对象获取。除了稍后将在“连接事件”中讨论的单个 `networkstatuschanged` 事件外，该对象的接口由一些方法组成，用于在其他对象中检索更具体的详细信息。

以下是 `NetworkInformation` 中的方法清单，以及通过这些方法获取的对象内容。你可以通过“网络信息”示例中标注的场景来练习这些最常见的 API：

- `getInternetConnectionProfile`（场景 1）为当前活动的 Internet 连接返回一个 `ConnectionProfile` 对象。如果有多个连接，此方法会返回最有可能用于 Internet 流量的首选配置文件。
- `getConnectionProfiles`（场景 3）返回一个 `ConnectionProfile` 对象向量，每个连接一个对象，其中包括 `getInternetConnectionProfile` 所返回的活动 Internet 连接。还包括你过去建立过且选择了“自动连接”的任何无线连接。（这样，该示例会显示一些你最近连接过的位置细节。）有关 `ConnectionProfile` 的更多信息，请参阅下一节。
- `findConnectionProfilesAsync`（场景 6）给定一个 `ConnectionProfileFilter` 对象，返回一个与筛选条件匹配的 `ConnectionProfile` 对象向量。这有助于你查找适用于特定应用场景的可用网络，例如查找 Wi-Fi 连接或具有特定费用策略的连接。
- `getHostNames` 返回一个 `HostName` 对象向量（见下方注释），每个连接一个对象，提供各种名称字符串（`displayName`、`canonicalName` 和 `rawName`）、名称类型（来自 `HostNameType`，取值为 `domainName`、`ipv4`、`ipv6` 和 `bluetooth`）以及一个包含 IPv4 和 IPv6 主机的 `prefixLength` 和 `networkAdapter` 属性的 `ipInformation` 属性（类型为 `IPInformation`）。（后者是一个 `NetworkAdapter` 对象，包含各种底层详细信息。）`HostName` 类用于各种网络 API，以标识服务器或其他端点。
- `getLanIdentifiers`（场景 4）返回一个 `LanIdentifier` 对象向量，每个对象包含一个 `infrastructureId`（包含类型和值的 `LanIdentifierData`）、一个 `networkAdapterId`（一个 GUID）和一个 `portId`（`LanIdentifierData`）。
- `getProxyConfigurationAsync` 为给定 URI 和当前用户返回一个 `ProxyConfiguration` 对象。该对象的属性为 `canConnectDirectly`（一个 Boolean）和 `proxyUris`（配置的 `Windows.Foundation.Uri` 对象向量）。
- `getSortedEndpointPairs` 根据 `HostNameSortOptions` 对 `EndpointPair` 对象数组进行排序。一个 `EndpointPair` 包含本地和远程端点的主机和服务名称，通常在设置套接字等特定连接时获取。两种排序选项是 `none` 和 `optimizeForLongConnections`，它们会根据应用建立的是短时连接还是长时连接来改变连接行为。有关详细信息，请参阅 `EndpointPair` 和 `HostNameSortOptions` 的文档。

**什么是向量？** **向量**是一种 WinRT 类型，通常用于管理列表或集合。它有 `append`、`removeAt` 和 `clear` 等方法，可用于管理列表。`getAt` 和 `getMany` 等其他方法允许检索项，向量还像数组一样支持 `[ ]` 运算符。有关详细信息，请参阅第 6 章“数据绑定、模板和集合”中的“Windows.Foundation.Collections 类型”。在最简单的用法中，你可以通过 `[ ]` 运算符把向量当作 JavaScript 数组来使用。

## ConnectionProfile 对象

在 `NetworkInformation` 对象可提供的所有信息中，对应用最重要的信息位于 `ConnectionProfile` 中，最常见的是由 `getInternetConnectionProfile` 返回的配置文件，因为应用的 Internet 流量将通过该连接流动。该配置文件包含你为决定如何使用网络而需要的所有信息，尤其有助于成本感知。当网络状态发生变化时，这也是你通常会检查的对象。“网络信息”示例的场景 1 和 3 会检索并显示其中的大部分详细信息。

每个配置文件都有一个 `profileName` 属性（一个字符串），例如“Ethernet”或无线接入点的 SSID；一个 `serviceProviderGuid` 属性（网络运营商 ID）；以及一个 `getNetworkNames` 方法，用于返回端点的友好名称向量。`networkAdapter` 属性包含一个用于底层详细信息的 `NetworkAdapter` 对象，如果你需要的话；`networkSecuritySettings` 属性包含一个描述身份验证和加密类型的 `NetworkSecuritySettings` 对象。

更常见且更有趣的是 `getNetworkConnectivityLevel` 方法，它返回 `NetworkConnectivityLevel` 枚举中的一个值：none（无连接）、localAccess（当你想获得良好连接时最不想看到的级别！）、constrainedInternetAccess（强制门户连接，通常需要进一步提供凭据，在酒店、机场等场所经常遇到），以及 internetAccess（你几乎总是想要达到的状态）。连接级别通常是应用逻辑中的一个因素，也是你在网络状态变化时通常会关注的内容。与此相关的是 `getDomainConnectivityLevel`，它提供 `DomainConnectivityLevel` 值：none（没有域控制器）、unauthenticated（用户尚未由域控制器进行身份验证）和 authenticated。

若要检查连接是否位于 Wi-Fi 上，请检查 `isWlanConnectionProfile` 标志；如果为 true，则可以查看 `wlanConnectionProfileDetails` 属性以获取更多详细信息，例如 SSID。另一方面，如果你使用的是移动连接，`isWwanConnectionProfile` 标志将为 true，此时 `wwanConnectionProfileDetails` 属性会告知你该连接的数据服务类型和注册状态。如果你想显示其中任一连接的信号强度，`getSignalBars` 方法会返回一个从 0 到 5 的值。

连接在其生命周期中的上下波动可以通过 `getConnectivityIntervalsAsync` 获取，它会生成一个 `ConnectivityInterval` 对象向量。每个对象都描述该网络何时连接以及保持了多长时间。

要跟踪连接上的入站和出站流量，`getNetworkUsageAsync` 方法会返回一个 `NetworkUsage` 对象，该对象在给定时间段和 `NetworkUsageStates`（漫游或共享）下包含 `bytesReceived`、`bytesSent` 和 `connectionDuration` 属性。类似地，`getConnectionCost` 和 `getDataPlanStatus` 提供应用了解正在发生多少网络流量以及可能让用户花费多少所需的信息。我们稍后在“成本感知”中会回到这一点，包括如何在任务管理器中查看按应用统计的使用量。

