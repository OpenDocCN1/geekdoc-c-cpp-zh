
CCP 也可以配置对讲机功能。要执行此操作，请导航到 `Unified Communications > Telephony Features > Intercom` 并点击 `Create` 按钮。图 7-16 所示的配置窗口允许您选择要分配对讲机功能的用户和快速拨号按钮。

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_224_0.png)

图 7-16 在 CCP 中配置对讲机

当您点击 `Deliver` 按钮后，CCP 应用以下语法：

```
ephone-dn 5
number A101
intercom A100 label "Assistant"
exit
ephone-dn 6
number A100
intercom A101 label "Manager"
exit
```

示例 7-10 中的分页配置演示了多组分页系统的配置。`Ephones` 1 和 2 继续使用 `ephone-dn 80` 作为它们的专用分页组。`Ephones` 3 和 4 使用 `ephone-dn 81`。这次，第三个分页组允许你同时对多个分页组进行呼叫。这使得组织能够灵活地呼叫特定部门或整个公司。

## 示例 7-10 配置多组分页

```
CME_Voice(config)# ephone-dn 80
CME_Voice(config-ephone-dn)# number 5555
CME_Voice(config-ephone-dn)# paging
CME_Voice(config-ephone-dn)# exit
CME_Voice(config)# ephone-dn 81
CME_Voice(config-ephone-dn)# number 5556
CME_Voice(config-ephone-dn)# paging
CME_Voice(config-ephone-dn)# exit
CME_Voice(config)# ephone-dn 82
CME_Voice(config-ephone-dn)# paging group 80,81
CME_Voice(config-ephone-dn)# exit
CME_Voice(config)# ephone 1
CME_Voice(config-ephone)# paging-dn 80
CME_Voice(config-ephone)# exit
CME_Voice(config)# ephone 2
CME_Voice(config-ephone)# paging-dn 80
CME_Voice(config-ephone)# exit
CME_Voice(config)# ephone 3
CME_Voice(config-ephone)# paging-dn 81
CME_Voice(config-ephone)# exit
CME_Voice(config)# ephone 4
CME_Voice(config-ephone)# paging-dn 81
```

通过示例 7-10 中的配置，拨打 DN `5555` 会呼叫 `ephones` 1 和 2，拨打 DN `5556` 会呼叫 `ephones` 3 和 4，拨打 DN `5557` 则会呼叫所有 `ephones`。你不需要将任何 `ephones` 分配给 `paging-dn 82`，因为此 `ephone-dn` 代表了 `paging-dns` 80 和 81 的组合组。

**注意：** `CME` 允许你使用 `paging group` 命令列出最多十个分页号码。

如果你选择使用 CCP 配置分页，请导航到 `Unified Communications` > `Telephony Features` > `Paging Numbers`。点击 `Create` 按钮允许你定义号码并关联电话，如图 7-18 所示。可以将此视为单组配置允许的操作。

CCP 也允许配置多组分页。通过导航到 `Unified Communications > Telephony Features > Paging Groups`，你可以创建与其它分页组关联的分页号码，而不是单独的分机机，如图 7-19 所示。

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_228_0.png)

图 7-18 在 CCP 中配置单组分页

## 配置下班时间呼叫拦截

在传统的电话领域，有许多记录在案显示，在非工作时间即大多数或所有员工已下班后发生了未经授权的呼叫。为了防止这种情况，你可以在 `CME` 上实施下班时间呼叫拦截。

下班时间呼叫拦截允许你定义指定为下班时间段的时间。然后你可以列出在该时间段内不允许的号码模式。如果用户在下班时间范围内拨打了符合所定义模式之一的电话，`CME` 将播放重拨音调并断开呼叫。

当然，每条规则都有例外。你可能希望让某些电话完全免于该策略，或者如果用户工作很晚并需要拨打 `CME` 通常会限制的业务电话，给他们一个绕过限制的“后门”。`CME` 下班时间呼叫拦截配置提供了这两种场景。你可以选择完全让某些 IP 电话免于下班限制，或为用户提供一个可以输入 IP 电话的 PIN。如果他们正确输入 PIN，`CME` 将将在可配置的时间内让 IP 电话免于下班策略。

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_229_0.png)

图 7-19 在 CCP 中配置多组分页

注意：某些模式可能在全天候拦截都有益。例如，美国的 1-900 号码通常代表高成本且信誉不佳的企业，这些企业通常被所有公司环境禁止。`CME` 还允许你使用下班时间系统创建一个 24/7 的非示例模式，该模式在任何时候都是禁止的。

下班时间呼叫拦截有三个主要的配置步骤：

- 步骤 1. 定义公司认为的非工作日期和或小时。
- 步骤 2. 指定在步骤 1 指定的时间内想要拦截的模式。
- 步骤 3. 如果需要，创建策略的例外。

你将在电话服务配置模式下执行大部分下班时间呼叫拦截限制的配置。示例 7-11 展示了下班时间段。

## 示例 7-11 配置下班时间范围和日期

```
CME_Voice(config)# telephony-service
CME_Voice(config-telephony)# after-hours
block define after-hours block pattern
date define month and day
day define day in week
CME_Voice(config-telephony)# after-hours day ?nDAY day of week (Mon, Tue, Wed, etc)
CME_Voice(config-telephony)# after-hours day ?nhh:mm Time to start (hh:mm)
CME_Voice(config-telephony)# after-hours day mon 17:00 ?
hh:mm Time to start (hh:mm)
CME_Voice(config-telephony)# after-hours day mon 17:00 8:00
CME_Voice(config-telephony)# after-hours day tue 17:00 8:00
CME_Voice(config-telephony)# after-hours day wed 17:00 8:00
CME_Voice(config-telephony)# after-hours day thu 17:00 8:00
CME_Voice(config-telephony)# after-hours day fri 17:00 8:00
CME_Voice(config-telephony)# after-hours date ?nMonth (Jan, Feb, etc)
CME_Voice(config-telephony)# after-hours date <1-31> day of month
CME_Voice(config-telephony)# after-hours date 25 ?nhh:mm Time to start (hh:mm)
CME_Voice(config-telephony)# after-hours date 25 00:00
CME_Voice(config-telephony)# after-hours date 1 ?nhh:mm Time to start (hh:mm)
CME_Voice(config-telephony)# after-hours date 1 00:00
CME_Voice(config-telephony)# after-hours date jan 00:00
```

示例 7-11 定义的下班时间段为下午 5:00 到第二天上午 8:00，涵盖 25 日圣诞节和 1 日元旦。

在下班时间呼叫拦截限制的配置中，你将在电话服务配置模式下执行大部分工作。第 8 和 9 章讨论了你可以用于匹配的模式。

注意：你可能可能在示例 7-12 的上下文帮助中注意到，`CME` 允许你配置 32 个拦截模式索引。初始拦截模式 1 匹配并拦截长途电话；模式 2 匹配国际电话；模式 3 匹配 900 电话。

## 示例 7-12 配置拦截拦截模式

```
CME_Voice(config)# telephony-service
CME_Voice(config-telephony)# after-hours block ?nblock pattern
CME_Voice(config-telephony)# after-hours block pattern <1-32> index of patterns
CME_Voice(config-telephony)# after-hours block pattern ?nWORD string for hour pattern
CME_Voice(config-telephony)# after-hours block pattern 1 91...
CME_Voice(config-telephony)# after-hours block pattern 2 98...
CME_Voice(config-telephony)# after-hours block pattern 3 9100...
```

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_230_0.png)

如果你需要比下班时间拦截更具灵活性的功能，你还可以使用 `CME` 的限制类别 `COR` 功能。

下班时间拦截配置的最后一步是允许策略的任何例外，如示例 7-13 所示。你可以根据 IP 电话添加例外，或通过使用一个或多个 PIN 号允许从任何 IP 电话按需访问拦截模式使用 24 关键字定义的模式除外。示例 7-13 配置电话 1 免于下班拦截策略。电话 2 和 3 配置了 PIN 号。

## 示例 7-13 配置下班例外

```
CME_Voice(config)# phone 1
CME_Voice(config-phone)# after-hours exempt
CME_Voice(config-phone)# exit
CME_Voice(config)# phone 2
CME_Voice(config-phone)# pin 7
  WORD A sequence of digits representing personal identification
CME_Voice(config-phone)# phone 1234
CME_Voice(config-phone)# exit
CME_Voice(config)# phone 3
CME_Voice(config-phone)# pin 4321
CME_Voice(config-phone)# exit
```

注意：PIN 码可以是四到八位数字之间的任意数字。

示例 7-13 中的最后一行是 PIN 码正常运行的关键。在默认情况下，所有支持 `CME` 的 Cisco IP 电话在 LCD 屏幕上都有一个 `Login` 软键。在从电话服务配置模式输入登录命令之前，该软键处于变暗状态且不可用。该命令随后的超时值代表电话自动撤销已输入的 PIN 码之前的空闲时间。清除时间值 `clear-time-value` 是最后输入的 PIN 码失效的绝对时间。在示例 7-13 的情况下，PIN 将在晚上 11:00 清除，无论是在何时输入的。它并不会阻止用户在晚上 11:00 之后再次输入 PIN 码重新登录。

注意：登录命令的默认超时时间为 60 分钟。此外，在登录命令生效之前，您需要重启或重置所有电话。

CCP 为配置下班拦截提供了一个直观的界面。当导航到 `Unified Communications > Telephony Features > After-Hour Toolbar` 时，CCP 会弹出一个窗口，允许您定义想要拦截的特定模式如图 7-20 所示。您可以通过点击 `After-Hour Toolbar` 配置窗口底部的 `Weekly Schedule`、`Holiday Schedule` 或 `Override` `Softkey Login` 窗格来创建计划和 PIN 码覆盖。

## 配置 CDR 和话费统计

“谁打了电话？”可能出于许多原因。也许是因为由于您的业务发生紧急情况，整个警察和消防部门都来到了您的公司大门。也许管理层正在审查最近的长途电话单，发现了一个拨往 Aruba 的时长四小时的国际电话。无论原因如何，只要您配置了 `CME` 路由器以支持它们，就可以通过查看存档的通话详细记录 `CDR` 找到答案。

`CDR` 包含了关于网络中接入、离开及 IP 电话通话的宝贵信息。这些记录包含了查找谁拨了电话以及通话时长所需的所有信息。`CME` 路由器可以将 `CDR` 日志到路由器的缓冲内存 `RAM`、syslog 服务器或两者都要。将 `CDR` 存储在路由器的 RAM 中比什么都没有好，但并不可有效。如果 `CME` 路由器掉电，所有 `CDR` 将丢失。同样，路由器的 RAM 存储空间有限，并不是一个有效的解决方案。从文件中查看 `CDR` 既晦涩又难以理解。示例 7-14 展示了您用于启用将 `CDR` 日志记录到路由器缓冲内存的语法。

示例 7-14 将 CDR 日志配置到缓冲内存

```
CME_Voice(config)# logging buffered 512000
CME_Voice(config)# dial-control-mib =
  max-size      指定拨号控制历史表的最大大小
retain-timer 指定拨号控制历史表条条目的计时器
CME(config#) dial-control-mib retain-timer =
<0.3591> 删除条目的时间（以分钟计）
CME(config#) dial-control-mib retain-timer 10080
CME(config#) dial-control-mib max-size =
<0.1200> 拨号控制历史表中的条目数量
CME(config#) dial-control-mib max-size 700
```

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_233_0.png)

**图 7-20** 使用 CCP 配置下班限制

示例 7-14 为 CDR 缓冲日志指定了以下参数：

- 512,000 字节内存专门用于路由器的日志功能。
- CDR 保留 10,080 分钟 7 天。
- CME 路由器在内存中最多保留 700 条 CDR。

要查看 CME 记录的 CDR，请使用 `logging` 命令，如示例 7-15 所示。

**示例 7-15** show logging 命令输出

```
CME Voice# show logging
Syslog logging: enabled (12 messages dropped, 1 messages rate-limited,
      0 flushes, 0 overflows, xml disabled, filtering disabled)
```

Console logging: level debugging, 168 messages logged, xml disabled, filtered disabled.

<...output omitted>

Log Buffer (512000 bytes):

* Jun 18 01:57:48.987: %SYS-S-5-CONFIG_1: Configured from console by Jeremy on vty0 (172.30.3.8)

* Jun 18 01:57:48.640: %VOIPAA-5-VOIP_CALL_HISTORY: CallLegType 1, ConnectionId B7142F7B3C10I1DD00EEB6A0B061E9, SetupTime *18:57:17.970 ARIONA Tue Jun 17 2008, PeerAddress 153, PeerSubAddress , DisconnectCause 1, DisconnectText unassigned number (1), ConnectTime *18:57:48.640 ARIONA Tue Jun 17 2008 DisconnectTime *18:57:48.640 ARIONA Tue Jun 17 2008, ChargedUnits 0, InfoType 2, TransmitPackets 0, TransmitBytes 0, ReceivePackets 0, ReceiveBytes
