

```
CME_Voice(config-ephone-dn)# exit
CME_Voice(config-ephone-dn)# ephone-dn 51
CME_Voice(config-ephone-dn)# number 3002
CME_Voice(config-ephone-dn)# name Sales
CME_Voice(config-ephone-dn)# park-slot =
reserved-for Reserve this park slot for the exclusive use of the phone with the
extension indicated by the transfer extension number
timeout Set call park timeout
<cr>
CME_Voice(config-ephone-dn)# park-slot ? =
<0-65535> Specify the park timeout (seconds) before the call is returned to the
number it was
CME_Voice(config-ephone-dn)# park-slot timeout 60 ?
limit Set call park timeout count limit
CME_Voice(config-ephone-dn)# park-slot timeout 60 limit =
<1-65535> Specify the number of park timeout cycles before the call is
disconnected
CME_Voice(config-ephone-dn)# park-slot timeout 60 10 ?
notify Define additional extension number to notify for park timeout
recall recall transfer back to originator phone after timeout
transfer Transfer to originator or specified destination after timeout
exceeded
<cr>
CME_Voice(config-ephone-dn)# park-slot timeout 60 10 recall =
alternate Transfer to alternate target if original target is busy
retry Set call/transfer retry interval if target is in use
<cr>
ME_Voice(config-ephone-dn)# park-slot timeout 60 10 recall
```

请查看示例 7-6 中 ephone-dn 50 的配置。指定呼叫留守分号只需在 ephone-dn 配置模式下使用 `park-slot` 命令即可简单。

**注意：** 在计划配置呼叫留守时，请记住每个留守通话插槽都会消耗一个 ephone-dn 插槽（无论单线还是双线配置）。您可能需要增加 CME 部署所支持的 ephone-dns (max-dn) 数量。

示例 7-6 还显示，当您指定特定的呼叫留守 ephone-dns 时，有许多选项可用。表 7-2 解释了您可以在哪里使用这些选项。

## **表 7-2** 与 park slot 命令配合使用的选项

| 命令 | 功能 |
| :--- | :--- |
| reserved-for <dn> | 允许您为输入的目录号码 (DN) 预留呼叫留守插槽。其他无法无法该呼叫留守插槽。 |
| timeout <seconds> | 指定 CME 在通知留守通话的电话该通话仍被留守之前等待的秒数。要进行通知，CME 会让电话响一秒钟并在 LCD 屏幕上显示消息。 |
| limit <count> | 限制留守通话可以达到的超时间隔次数。达到此限制后，留守通话将被断开。顺便提一下，建议将此值设大。客户在长时间等待后被断开通常会感到困扰。 |
| notify <dn> | 当留守通话达到超时时，除了留守通话的电话外，还会通知另一个 DN。 |
| only | 与先前的 notify 语法配合使用；指示 CME 仅响 notify 命令指定的 DN，而不是响原始电话。 |
| recall | 在留守通话达到超时期后，使通话返回（转移回）留守的原始电话。 |
| transfer <dn> | 在留守通话达到超时期后，使通话转移到指定的 DN。 |
| alternate <dn> | 如果 transfer 命令中指定的 DN 忙，则允许转移到备用目标。 |
| retry <seconds> | 设置 CME 再次尝试转移留守通话之前的时间。 |

配置呼叫留守选项具有很大的灵活性。在您指定至少一个 phone-dn 用于呼叫留守（通过使用 `park-slot` 命令）后，Park 软键会在活动通话的 IP 电话上出现。

> **注意：** 如果您配置了初始指定的 ephone-dn 呼叫留守软键出现在活动通话中，必须重启或重置 IP 电话。您可以通过电话服务配置模式下使用 `restart` 或 `reset` 命令来实现。

要留守通话，只需在活动通话期间按 Park 软键即可。CME 会为执行留守操作的电话找到一个留守插槽，如图 7-11 所示。

当用户留守通话时，CME 会分配第一个可用的留守插槽。有时，您可能想指定哪个留守插槽接收通话，例如公司每个部门都分配了唯一的呼叫留守号码的情况。在这种情况下，您可以直接（使用 Transfer 软键）将通话转移到您想要的留守插槽。

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_218_0.png)

图 7-11 留守通话后的 IP 电话

**注意：** 如果你想使用每个部门都有自己的呼叫留守插槽的系统，为每个部门分配多个指定用于呼叫留守的 ephone-dns 将很有益。否则，每个部门只能留守一个通话。

您可以通过三种方式接听留守通话：

- 直接拨入留守插槽。例如，拿起电话筒并拨打 3001 可接听留守在 3001 的任何通话。
- 按 PickUp 软键并拨打您想接听的留留留号码。
- 从留守通话的电话上，按 PickUp 软键后跟星号 (*)，将最近留守的通话召回电话。

使用 CCG 配置呼叫留守功能在很大程度上自动化了过程。首先，导航到呼叫留守配置窗口（Unified Communications > Telephony Features > Call Park）。到达后，您可以点击 Create 按钮打开创建呼叫留守条目的配置窗口。输入名称会在 IOS 中为呼叫留守条目创建一个描述标签。CCG 为您提供了选择插槽数量（呼叫留守号码）以及插槽起始号码的选项。例如，应用图 7-12 所示的配置将创建从 1300 到 1309 的十个留守插槽。

# 190 CCNA Voice 640-461 认证指南

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_219_0.png)

**图 7-12** 使用 CCP 配置呼叫留守

此外，呼叫留守配置窗口的 Advanced 标签页如图 7-13 所示）提供了许多选项（如表 7-2 所示）来修改呼叫留守功能。

## 配置 Call Pickup

Michael 在 Widget Things, Inc. 的销售部门工作。作为小组的最新成员，他值晚班，从早上 10:30 到晚上 7:30。晚上 6 点，最后一位同事离开了，Michael 独自处理所有通话。不幸的是，Widget Things 的客户有其他销售人员的直接联系方式，因此 Michael 一个典型的晚上是接听来自销售电话的电话。这就是 Call Pickup 有帮助的地方。

Call park 允许您从本地电话接听另一个响铃电话。这是通过在电话响铃时按下软键实现的。通话会自动转移到本地电话，您可以接听。当然，公司很大，可能同时有很多电话响铃，因此 call park 为您提供了将电话分组的机会。您在 CME 配置中为每个组分配一个号码，如图 7-14 所示。

根据软键，用户可以接听所在小组的其他响铃电话，或输入其他组号码接听该组的响铃电话。

# 第 7 章 配置 CME 语音功能 191

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_220_0.png)

图 7-13 从 CCP 可的高级呼叫留守

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_220_1.png)

图 7-14 设计 Call Pickup 小组

call pickup 的配置非常简单：只需设计电话组并将 ephone-dns 分配给组。示例 7-7 将 ephone-dn 1、2 和 3 分配给 SALES 组，将 ephone-dn 4、5 分配给 ACCOUNTING 组，如图 7-14 所示。

# 示例 7-7 配置 Call Pickup

```
CME_Voice(config)# ephone-dn 1
CME_Voice(config-ephone-dn)# pickup-group 5509
CME_Voice(config-ephone-dn)# ephone-dn 2
CME_Voice(config-ephone-dn)# pickup-group 5509
CME_Voice(config-ephone-dn)# ephone-dn 3
```

