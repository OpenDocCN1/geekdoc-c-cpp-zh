
底部显示了启用了 H.450.3 支持的通话。当通话到达加利福尼亚州时，CME 发送基于 H.450.3 的重定向消息，而不是接受通话并将其转发到佛罗里达。VoIP 流量直接从德克萨州的 x1001 传输到佛罗里达，而不是通过加州到达那儿。

在电话服务配置模式下输入呼叫转移模式 `<pattern>`，可以告诉 CME 哪些号码应该开始支持 H.450.3。输入模式 15，即是告诉 CME：“我希望所有以 15 开头的四位数字都支持 H.450.3。”因此，所有拨向 15XX 的通话都将支持 H.450.3。

**注意：** 关于 H.450.3 标准还有更多内容要说。还有更多配置应该实施以完全支持 H.450.3。这旨在作为标准的“预览”，在 CCNP 语音认证中会深入探讨。

如果你倾向于使用 CCP 进行转发修改，可以在扩展（Extensions）选项卡下（Unified Communications > Phones, and Extensions）找到设置，如图 7-9 所示。![](img/ead7862dc47b4e5de0cde3450ad65_212.png)

**图7-9** 使用 CCP 配置转发

转移通话是语音网络中的另一个常用功能。要转移通话，在通话活动期间按下 Transfer 软键。（注意：这里的 Transferring 是拼写错误：Transfer 是正确的。）当你听到拨号音时，可以拨通想要转移的电话号码。取决于 CME 路由器上配置的转移方法。有两种转移方法：![](img/ead7862dc47b4e5de0cde3450ad65_213.png)

- **咨询（Consult）**：咨询转移允许你在转移通话之前与对方通话。在你拨通想要转移的号码后，等待对方接听并与其通话。再次按下 Transfer 软键将转移通话，让你退出对话。咨询转移需要第二线路（或双线配置）。但是 CME 中默认的转移模式是咨询。
- **盲转（Blind）**：盲转在你拨通号码后立即转移通话（你不需要再次按下 Transfer 软键）。盲转可以在单线配置下工作。要配置使用的转移方法，请参见示例 7-4。

 示例 7-4 全局配置 CME 转移方法

```
CME_Voice(config)# telephony-service
CME_Voice(config-telephony)# transfer-system
full-blind      不使用咨询使用 H.450.2 或 SIP 标准转移通话
full-consult   如果可用线路，则使用咨询进行通话转移，如果没有则回退到盲转。这是大多数系统推荐的方法。另见 'voice service voip' 下的 'supplementary-service' 命令和 dial-peer。
local-consult  如果可用线路，则使用本地咨询进行通话转移，如果没有则回退到目标。使用 Cisco 私有方法。
```

```
CME_Voice(config-telephony)# transfer-system full-consult
```

从上下文相关帮助可以看出，有三种转移方法可用：盲转、咨询和本地咨询。本节开头介绍了这些转移方法。盲转和咨询转移方法使用行业标准的 H.450.2 转移方法。就像呼叫转移一样，你不希望每次转移时都产生环路并导致潜在的 QoS 问题。在转移通话时使用 H.450.2 标准，CME 路由器会完全断开转移电话的通话，并目标电话拨起新通话。

本地咨询方法使用 Cisco 私有转移方法，如果有多个线路或双线配置，它将执行咨询，但如果只有单线，则将恢复盲转。Cisco 私有方法与 H.450 标准类似。唯一的问题是，如果你网络中没有 Cisco IP 电话系统，这种转移方法会导致环路。

**注意：** 你还可以通过 ephone-dn 配置模式使用 `transfer-mode<blind/consult>` 语法为每个 ephone-dn 独立配置转移模式。这种方式配置转移模式使用标准并覆盖全局设置。

默认情况下，Cisco 路由器限制转移到非本地管理的设备。这通常是一个好的策略，因为到公司之外可能会导致话费欺诈。例如，用户可以将外部呼叫者转移到国际号码，导致话费由组织而非外部呼叫者支付。如果你允许向本地管理设备之外进行转移，可以使用电话服务模式下的 `transfer-pattern<pattern>` 命令，其中 pattern 代表你允许转移的号码。示例 7-5 配置了 Cisco Unified CME，允许转移到 5XXX 扩展和本地数字 PSTN 号。

## 示例 7-5 配置 CME 转移模式允许外部转移

![](img/ead7862dc47b4e5de0cde34550ad65_214_0.png)

```
CME_Voice(config)#telephony
CME_Voice(config-telephony)#transfer-pattern ?n  允许的非本地呼叫转移的数字字符串模式

CME_Voice(config-telephony)#transfer-pattern 5...
CME_Voice(config-telephony)#transfer-pattern 9....................

```

Cisco CCP 也允许配置转移模式。这些位于 Unified Communications > Advanced Telephony Settings 下。图 7-10 所示的简单配置允许你只需点击 Add 按钮并将手动配置的转移模式直接添加到 CCP 界面中。

## 配置呼叫留守（Call Park）

通常，当你将通话挂起时，你只能从放置通话的原始电话恢复通话。共享线路系统通过规则允许你从具有相同共享线路分配的任何电话恢复通话。呼叫留守功能进一步允许从组织内的任何电话恢复通话。留守停留在扩展号而不是特定线路。任何拨通留守号码的 IP 电话都可以恢复通话。

留守系统通过查找配置中未分配给 IP 电话并专门指定为留守槽的空闲 dns 来工作。你可以允许 CME 随机留守通话，也可以允许用户选择留守通话的扩展号。这些场景适用于不同的环境。随机留守扩展号可能适用于带有语音广播系统的仓库环境。当有来电时，接线员可以通过扬声器宣布：“Larry，你有一个 5913 的电话”，这时 Larry 可以去电话并拨通扩展号来接听通话。

![](img/ead7862dc47b4e5de0cde34550ad65_215_0.png)

**图7-10** 使用 CCP 配置转移模式

选择扩展适用于每个部门对应已知扩展号码的电子超级市场。例如，软件可以是扩展 301，摄像头可以是扩展 302，以此此类推。然后，接线员可以将多个通话留守同一个留守号码（这需要多个 ephone-dn 分配相同的扩展号）。当服务部门恢复通话时，CME 会按照请求顺序分发。

你可以通过简单添加为留守目的设计的 ephone-dn 来配置呼叫留守。示例 7-6 创建了两个用于留守的 ephone-dn。

```
CME_Voice(config)# ephone-dn 50
CME_Voice(config-ephone-dn)\# number 3001
CME_Voice(config-ephone-dn)\# name Maintenance
CME_Voice(config-ephone-dn)\# park-slot
```
