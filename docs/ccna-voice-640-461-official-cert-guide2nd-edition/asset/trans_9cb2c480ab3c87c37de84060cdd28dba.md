
7. Ermeniglio 决定开始使用服务性报告（Serviceability Reports）存档。他启动了相应的服务，等到第二天打开了警报报告（Alerts Report）。他惊讶地发现报告显示昨天没有生成任何警报。可能是什么问题？

- a. 服务卡顿了，需要重启。
- b. 没有生成警报。
- c. 必须将显示报警阈值（Display Alert Threshold）设置为临界（Critical）或以下。
- d. Ermeniglio 必须使用 RTMT 查看警报。

8. Bob 说他想查看服务性存档（Serviceability Archives）中显示的警报详情。你应该怎么做？

- a. 打开 CUC 的 RTMT，进入警报中心（Alert Central），右键点击任何警报查看详情。
- b. 打开 RTMT，进入服务器（Server）选项卡并查找警报列表。
- c. 生成警报报告时勾选包含细节（Include Detail）复选框。
- d. 等30秒让 Bob 是真的，然后从 CUCM 服务器下载事件日志（Event Log）。

9. 上任 CUC 管理员最近辞职了。你被聘来接替她的。你想了解 CUC 服务器的维护状况如何。你如何发现哪些账户仍处于激活状态但未使用？

- a. 运行每周诊断报告（Weekly Diagnostics Report）。
- b. 运行安全报告（Security Report）。
- c. 运行未使用语音邮箱账户报告（Unused Voice Mail Accounts Report）。
- d. 运行用户锁定报告（User Lockout Report）。

10. 每周有几天，通常在早上 8:00 到上午 9:00 之间，用户抱怨 MWI（新消息指示灯）问题。有些人有新消息，但指示灯没亮；另一些人抱怨指示灯亮着，但没有新消息。你怀疑服务器没有发出 MWI 叫。你如何快速检查是否是这种情况？

- a. 运行端口模拟器（Port Simulator）工具并发送测试消息。
- b. 下午运行端口状态监控器（Port Status Monitor）。
- c. 周四早点来，尝试给一个用户留留言，看指示灯是否会亮。
- d. 运行端口活动报告（Port Activity Report）。

## 基础主题

## 生成和访问 Cisco Unity 报告

在 CUC 中生成和查看报告有两个主要接口：在 Cisco Unity Serviceability 的工具（Tools） > 报告（Reports）下，以及在 Cisco Unified Serviceability 的工具（Tools） > 服务性报告存档（Serviceability Reports Archive）下。

## Cisco Unity 服务性报告

Cisco Serviceability 提供了 19 份报告，帮助管理员监控和理解 CUC 应用程序的状态和行为。图 17-1 显示了 CUC 服务性报告页面，列出了所有 19 份报告。

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_471_0.png)

图 17-1 CUC 服务性报告页面

要访问这些报告，打开 CUC Serviceability 应用程序并导航到 Tools > Reports。报告列表包括：

- 电话接口失败日志报告（Phone Interface Failed Log Report）
- 用户报告（Users Report）
- 消息流量报告（Message Traffic Report）
- 端口活动报告（Port Activity Report）
- 邮箱存储报告（Mailbox Store Report）
- 拨号计划报告（Dial Plan Report）
- 拨号搜索范围报告（Dial Search Scope Report）
- 用户电话登录和 MWI（User Phone Login and MWI）
- 用户消息活动报告（User Message Activity Report）
- 分发列表报告（Distribution Lists Report）
- 用户锁定报告（User Lockout Report）
- 未使用的语音邮箱账户报告（Unused Voice Mail Accounts Report）
- 转移计费报告（Transfer Call Billing Report）
- 外呼计费报告（Outcall Billing Report）
- 外呼计费摘要报告（Outcall Billing Summary Report）
- 话处理流量报告（Call Handler Traffic Report）
- 系统配置报告（System Configuration Report）
- 按用户 SpeechView 活动报告（SpeechView Activity Report by User）
- SpeechView 活动摘要报告（SpeechView Acitivity Summary Report）

以运行用户报告（Users Report）为例。从 CUC 服务性报告页面，点击 Users Report。出现如图 17-2 所示的屏幕。

可以通过以下选择来自定义报告（如图 17-2 所示）：

运行此报告针对（Run This Report For:）：

- 选择类别（Select Class）：
    - 用户（User）
    - 分发列表（Distribution List）
    - 服务类别（COS）

- 用户（User）：
    - 所有用户（All Users）
    - 选择的用户（Selected Users）

文件格式（File Format）：

- 网页页（Web Page）
- 逗号分隔文件（Comma-Delimited File）
- PDF 文件（PDF File）

## CCNA 语音 640-461 官方认证指南

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_473_0.png)

**图 17-2** 用户报告配置页面

## 排序顺序（Sort Order）：

- 姓（Last Name）
- 名（First Name）
- 分机号（Extension）
- COS

自定义选择后，点击生成报告（Generate Report）。

图 17-3 显示了用户报告的示例输出。

用户报告包含以下信息，如图 17-3 所示：

- 姓、名和别名（Last Name, First Name, and Alias）
- 地位置（Location）
- 主邮局服务器（Home Mail Server）
- 计费 ID、CoS 和分机号（Billing ID, CoS, and Extension）
- 账户锁定状态（Account Lockout Status）
- 个人转移规则启用/禁用状态（Personal Call Transfer Rules Enabled/Disabled Status）

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_474_0.png)

图 17-3 示例输出：用户报告

CUC 服务性报告列表中的其他报告提供了对 CUC 服务器当前状态、配置和利用的见解。

## Cisco Unified Serviceability: 服务性报告存档

CUC 包含一个内置报告系统用于监控服务器健康和性能。这些报告通过 Unified Serviceability Web 访问（不要与 CUC Serviceability 应用程序混淆）。要访问这些报告，必须先激活服务性报告器（Serviceability Reporter）。

服务性报告器从日志收集数据并填充服务性存档（Serviceability Archive），该存档存储报告信息并使其每日可用。它是基于日志收集数据的，由于它是 CPU 密集型服务，因此激活它可能会影响性能。在 Unified Serviceability 中，导航到 Tools > Reports 查看以下项：

- 启用审计日志（Enable Audit Log）：取消勾选此框将停止记录过程。默认设置为启用。

## 关键主题（Key Topic）

- 审计日志允许的最大次数（Maximum Entries Allowed in Audit Log）：限制审计日志条目。超过定义数值时，将覆盖旧条目。范围在 1 到 100,000 之间。默认为 100,000。
- 启用安全日志（Enable Security Log）：取消勾选此框将停止记录过程。
- 安全日志允许的最大次数（Maximum Entries Allowed in Security Log）：限制安全日志条目。超过定义数值时，将覆盖旧条目。范围在 1 到 100,000 之间。默认为 100,000。
- 数据周期间隔分钟（Minutes Between Data Cycles）：控制收集数据的频率。默认为 30。
- 数据保留天数（Days to Keep Data）：决定在报告数据库中保留多少天的历史数据。默认为 90 天。注意，如果报告指定的时间范围超过 90 天，报告仍受此设置值的限制。
- 禁用报告收获的数据库大小百分比（Reports Database Size... After Which Reports Harvest Is Disabled）：设置报告数据库可占用的磁盘空间百分比。达到该值时，停止 CUC 报告收获服务，防止数据库增长。默认值为 80%。
- 输出最大记录数（Maximum Records in Output）：限制报告中显示的记录数。范围从 5,000 到 30,000；默认为 25,000。某些报告由于其大小有自己的限制（例如，用户消息活动限制为 25,000）。
- 显示进度指示器的最小记录数（Minimum Records Needed to Display Progress Indicator）：此值决定在生成报告之前是否弹出消息并在生成时显示进度条。其目的是警告用户所选报告很大，可能会影响服务器性能。范围在 1 到 10,000 之间。默认为 2,500。

图 17-4 显示了报告配置页面。

## 分析 Cisco Unity 连接报告

在 Unified Serviceability Web 应用程序中，导航到 Tools > Serviceability Reports Archive。点击您想要查看报告的月份，然后点击特定日期。图 17-5 显示了服务性报告存档列表页面。

有两个可查看的服务性存档报告（假设已过去足够的时间提供供收集的数据）。

警报报告（Alerts Report）显示：

- 集群中按严重程度划分的警报数量
- 每个服务器的警报数量
- 集群中的前十大警报
