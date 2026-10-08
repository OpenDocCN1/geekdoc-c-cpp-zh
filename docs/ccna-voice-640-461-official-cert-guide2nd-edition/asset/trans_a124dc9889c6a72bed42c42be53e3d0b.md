
示例 7-10 中的分页配置演示了多组分页系统的配置。Ephones 1 和 2 继续使用 ephone-dn 80 作为它们的专用分页组。Ephones 3 和 4 使用 ephone-dn 81。这次，第三个分页组允许你同时对多个分页组进行呼叫。这使得组织能够灵活地呼叫特定部门或整个公司。

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

通过示例 7-10 中的配置，拨打 DN 5555 会呼叫 ephones 1 和 2，拨打 DN 5556 会呼叫 ephones 3 和 4，拨打 DN 5557 则会呼叫所有 ephones。你不需要将任何 ephones 分配给 paging-dn 82，因为此 ephone-dn 代表了 paging-dns 80 和 81 的组合组。

**注意：** CME 允许你使用 paging group 命令列出最多十个分页号码。

如果你选择使用 CCP 配置分页，请导航到 Unified Communications（统一通信） > Telephony Features（电话功能） > Paging Numbers（分页号码）。点击 Create（创建）按钮允许你定义号码并关联电话，如图 7-18 所示。可以将此视为单组配置允许的操作。

CCP 也允许配置多组分页。通过导航到 Unified Communications > Telephony Features > Paging Groups（分页组），你可以创建与其它分页组关联的分页号码，而不是单独的分机机，如图 7-19 所示。

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_228_0.png)

图 7-18 在 CCP 中配置单组分页

## 配置下班时间呼叫拦截

在传统的电话领域，有许多记录在案显示，在非工作时间（即大多数或所有员工已下班后）发生了未经授权的呼叫。为了防止这种情况，你可以在 CME 上实施下班时间呼叫拦截。

下班时间呼叫拦截允许你定义指定为下班时间段的时间。然后你可以列出在该时间段内不允许的号码模式。如果用户在下班时间范围内拨打了符合所定义模式之一的电话，CME 将播放重拨音调并断开呼叫。

当然，每条规则都有例外。你可能希望让某些电话完全免于该策略，或者如果用户工作很晚并需要拨打 CME 通常会限制的业务电话，给他们一个绕过限制的“后门”。CME 下班时间呼叫拦截配置提供了这两种场景。你可以选择完全让某些 IP 电话免于下班限制，或为用户提供一个可以输入 IP 电话的 PIN。如果他们正确输入 PIN，CME 将将在可配置的时间内让 IP 电话免于下班策略。

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_229_0.png)

图 7-19 在 CCP 中配置多组分页

注意：某些模式可能在全天候拦截都有益。例如，美国的 1-900 号码通常代表高成本且信誉不佳的企业，这些企业通常被所有公司环境禁止。CME 还允许你使用下班时间系统创建一个 24/7 的非示例模式，该模式在任何时候都是禁止的。

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

 示例 7-11 定义的下班时间段为下午 5:00 到第二天上午 8:00，涵盖 25 日（圣诞节）和 1 日（元旦）。

在下班时间呼叫拦截限制的配置中，你将在电话服务配置模式下执行大部分工作。第 8 和 9 章讨论了你可以用于匹配的模式。

注意：你可能可能在示例 7-12 的上下文帮助中注意到，CME 允许你配置 32 个拦截模式索引。初始拦截模式 1 匹配并拦截长途电话；模式 2 匹配国际电话；模式 3 匹配 900 电话。

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

如果你需要比下班时间拦截更具灵活性的功能，你还可以使用 CME 的限制类别（COR）功能。

下班时间拦截配置的最后一步是允许策略的任何例外，如示例 7-13 所示。你可以根据 IP 电话添加例外，或通过使用一个或多个 PIN 号允许从任何 IP 电话按需访问拦截模式（使用 24 关键字定义的模式除外）。示例 7-13 配置电话 1 免于下班拦截策略。电话 2 和 3 配置了 PIN 号。

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
