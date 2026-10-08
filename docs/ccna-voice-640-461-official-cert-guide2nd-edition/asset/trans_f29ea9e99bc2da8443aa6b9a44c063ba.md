

5. Beru 阿姨想找出她的团队中谁通话时间最长。应该运行哪份 CAR 报告？

- a. Bills > Department（账单 > 部门）
- b. Bills > Individual（账单 > 个人）
- c. Top N > By Duration（前 N > 按时长）
- d. Top N > By Charge（前 N > 按费用）

6. Greg 是 CAR Reports 用户。他可以运行 Top N > By Charge 报告吗？

- a. 不能
- b. 可以

7. Janice 很 upset，因为她委托的自定义 IP电话服务没有被许多用户采用。哪份 CAR 报告可以确定有多少电话订阅了她的服务？

- a. Cisco IP Phone Services (with the custom service selected）（Cisco IP电话服务（选择自定义服务））
- b. Top N > Service Subscriptions（前 N > 服务订阅）
- c. Cisco Unified Communications Manager Assistant > Manager Call Usage（Cisco 通信管理器助手 > 管理通话使用情况）
- d. Top N > Number of Calls（前 N > 通话次数）

8. 你是 CMC 管理员。几个月前，管理层要求你实施 Client Matters（客户事项）来跟踪员工的个人通话。对于使用 CMC 分配个人通话的通话列表，你可以提供哪份报告？

- a. Traffic > Summary（流量 > 摘要）
- b. Traffic > Summary By Extension（流量 > 分扩展摘要）
- c. Forced Authorization Code / Client Matter Code > Client Matter Code（强制授权码/客户事项代码 > 客户事项代码）
- d. Forced Authorization Code / Client Matter Code > Authorization Level（强制授权码/客户事项代码 > 授权级别）

9. Luke 当 CMC 管理员已有两年。他正尝试使用 RTMT 查看新 CUC 服务器的系统摘要信息。他抱怨菜单不可见。Luke 应该做什么来让 CMC 菜单可见？

- a. 在 Edit > Preferences（编辑 > 选项）下，勾选 CUC System Menu（CUC 系统菜单）。
- b. 在 PC 上安装 Linux 版本的 RTMT。
- c. 从 CUC 服务器下载并安装 RTMT。
- d. Luke 必须成为标准 RTMT 管理员组的成员。

10. 灾难恢复系统有两种哪些存储选项？

- a. Local disk file and TFTP（本地磁盘文件和 TFTP）
- b. Local disk file and FTP（本地磁盘文件和 FTP）
- c. Local tape drive and FTP（本地磁带驱动和 FTP）
- d. Local tape drive and local disk file（本地磁带驱动和本地磁盘文件）
- e. Local tape drive and SFTP（本地磁带驱动和 SFTP）

# 基础主题

## 描述如何为连接性和语音质量问题提供用户支持

排查 CUCM 等复杂应用的故障具有挑战性。CCNA Voice (ICOMM) 的范围要求我们保持相对简单，因此绝不应视为全面的 CUCM 故障排除手册。在本章中，你将学习如何排查基本的 IP 电话注册问题，并查看 CUCM 系统强大的报告功能，通过这些功能你可以监控部署中服务器的健康状况。

请注意，关于故障排除方法的下述章节将在第 9 章“使用 CME 管理端点和用户”中重复出现。在这里再次出现是因为它很重要，并且便于你在阅读本章时进行查阅。

# 故障排除

在排除故障时，采用一致且系统化的方法可以节省时间并帮助防止错误导致情况恶化。此处描述的步骤序列被 Cisco 最佳实践支持作为有效故障排除的模型，图 16-1 所示了故障排除顺序。

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_447_0.png)

图 16-1 故障排除方法

图 16-1 所示的步骤如下：

- 1. **定义问题：** 分析问题并创建一个清晰的问题描述。定义症状和可能的原因。将当前状况与基准“正常”状况进行比较。

- 2. **收集事实：** 收集并使用命令输出和用户陈述。排除可能的原因以减少潜在问题的数量。询问：问题何时发生？问题开始之前发生了什么变化？是间歇性的还是持续性的？是否有任何错误信息？是否有人遇到了这个问题？

- 3. **考虑可能性：** 根据步骤 2 收集的事实，识别出一份可能原因短名单。这可能是一个快速的、几乎直觉的过程，也可能需要研究和讨论。

- 4. **制定行动计划：** 从步骤 3 列表中最可能的原因开始，制定一个纠正问题的行动计划。计划应每次只修改一个变量，以便于评估一次更改的效果。

- 5. **实施行动计划：** 执行步骤 4 中确定的命令或做出更改。不要临时发挥：如果出现新的信息或主想法，你可能需要重新从步骤 3 开始。确保每一步所采取的行动都不会让问题恶化——如果导致了，请撤销。尽量减少更改对生产流程的影响，特别是限制安全漏洞的持续时间，例如临时移除访问列表以查看其状态。

- 6. **观察结果：** 问题解决了吗？

- 7a. 未解决：** 如果问题未解决，撤销步骤 5 中实施的更改并返回步骤 4。

- 7b. 已解决：** 如果问题已解决，记录解决方案、根本原因以及对系统进行的更改。

- 8. 你已完成。

像这样的列表（你需要背诵）需要一个好的记忆法。这里有一个可以给你参考：定义、收集、考虑、创建、实施、观察：“**Dogs Gobble Cookies, Cats Interact.**（狗吞掉饼干，猫在互动）”。

# 排排除 IP 电话注册问题

IP 电话注册过程具有欺骗性的复杂性，几个离散区域可能会导致问题——而且，如果一个步骤失败，后续步骤也会失败。在这种情况下，你可以使用分而治之的方法：快速检查哪些步骤已成功，然后从第一个故障点开始排排除故障。IP 电话注册问题可以根据以下故障点进行分类：

- 本地到 IP 电话
- VLAN 或交换机不匹配
- DHCP 问题
- TFTP 问题
- CUCM 注册问题

让我们检查电话未注册的场景。在这种情况下，电话应该通过 DHCP 使用。接下来的每个点描述了可能发生问题的地方。最佳实践规定我们按顺序执行以下故障排除程序：

- 本地到 IP 电话：电话本身可以显示当前配置和设置，这可以快速指示哪个部分失败了。按下 Settings 按钮，从显示列表中选择 Network Configuration。滚动到 IP Configuration，验证电话是否获得了 IP 地址、子网掩码、默认网关以及 TFTP 服务器地址。如果条目缺失或错误，验证电话是否配置为使用 DHCP（检查 Enabled 是否为 Yes）。如果都正确，请进入下一步。

- VLAN 或交换机不匹配：验证交换机已正确配置以支持 IP电话。交换机应定义语音 VLAN，如果电话连接了 PC，则有一个单独的 VLAN（参见第3章“理解IP电话概念和注册”）。验证 VLAN 号正确。如果交换机配置正确，请继续。

- DHCP 问题：验证 DHCP 服务器正在运行且没有耗尽 IP 地址。确保 DHCP 范围（子网或池）正确，相对于 IP 地址范围、子网掩码、默认网关以及选项 150（TFTP 服务器 IP 地址）。在 IP电话上，导航到 Settings > Network Configuration。验证 DHCP Server 条目列出了正确的 DHCP 服务器 IP。检查是否已分配 IP 地址，如果是，检查是否在正确范围内。验证 TFTP Server 1 地址条目正确。

> 注意：如果 DHCP 服务器位于电话的远程子网，本地路由器默认阻止 DHCP 广播。在本地路由器上使用 ip-helper<ip address> 命令允许将 DHCP 请求转发到 DHCP 服务器 IP。

- TFTP 问题：启动时，电话向 TFTP 服务器（通过 DHCP 获取的地址）查询其配置文件。它请求的文件名是 SEP<mac>.cnf.xml。如果电话已成功添加到 CUCM 或 Cisco Communication Express (CME) 应用，文件将存在并下载到电话。如果电话之前未添加到应用程序，文件将不存在。电话随后会请求名为 XMLDe-cnf.xml 的文件。此默认文件始终可用。如果电话没有获取其配置文件，验证电话在 Network Configuration 列表中具有正确的 TFTP 地址。验证该 IP 服务器上的 TFTP 服务正在运行。你可以通过按下 Settings > Status Messages 来检查电话上 TFTP 进程的状态：

