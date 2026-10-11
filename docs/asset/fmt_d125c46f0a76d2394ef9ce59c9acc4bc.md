
| IN | OUT | STATUS |
|---|---|---|
| 01 |  | down |
| 02 |  | down |
| 03 |  | down |
| 04 |  | down |
| 05 |  | down |
| 06 |  | down |
| 07 |  | down |
| 08 |  | down |
| 09 |  | down |
| 10 |  | down |
| 11 |  | down |
| 12 |  | down |
| 13 |  | down |
| 14 |  | down |
| 15 |  | down |
| 16 |  | down |
| 17 |  | down |
| 18 |  | down |
| 19 |  | down |
| 20 |  | down |
| 21 |  | down |
| 22 |  | down |
| 23 |  | down |
| 24 |  | down |

## PBX 系统

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_144_0.png)

**图 6-3** 使用单个 T1 接口配置多个连接

**注意：** 图 6-3 所示的解复用设备允许您将 T1 接口拆分为具有特定通道分配的多个接口。

注意，`ds0-group` 命令还允许您设置信令类型。这使您能够连接到许多不同的网络类型。PSTN 运营商通常通过 T1 CAS 连接使用 FXO 回路起始信令（这可能取决于您所在的位置和服务提供商）。PBX 系统通常支持多种耳麦话风（E&M）信令类型之一。

在输入 `ds0-group` 命令后，路由器会自动为您配置的每个时隙创建一个语音端口，如示例 6-5 中的 `show voice port summary` 输出所示。端口被列为 1/0，其中代表物理接口，而额外的 1 代表 DS0 组号。请记住此端口标识符，因为您需要它来配置拨号对。列出的每个端口代表 T1 接口上的不同通道。

用于 CCS (ISDN PRI) PSTN 连接的数字 T1/E1 接口使用与示例 6-6 类似的语法配置，示例 6-6 展示了将 VWIC 接口的所有 24 个时隙作为 PRI PSTN 连接的配置。

## **示例 6-6** 配置 T1 CCS PSTN 接口

```
CME-Voice(config)# isdn switch-type ?
primary-4ess      Lucent ESS switch type for the U.S.
primary-5ess      Lucent 5ESS switch type for the U.S.
primary-dms100  Northern Telecom DMS-100 switch type for the U.S.
primary-dnpss DPSSS switch type for Europe
primary-net      NETS switch type for UK, Europe, Asia and Australia
```

```
primary-ni National ISDN Switch type for the U.S.
primary-ntt NTT switch type for Japan
primary-qsig QSIG switch type
primary-ts04 TS04 switch-type-primary for Australia (obsolete)
CME_Voice(config)# isdn switch-type primary-5ess
CME_Voice(config)# controller t 1/0
CME_Voice(config)# pri-group?
fas_d Specify the operation of the D-channel timeslot.
service Specify the service type
timeslots List of timeslots in the pri-group
<cr>
CME_Voice(config-controller)# pri-group timeslots?
<1-24> List of timeslots which comprise the pri-group

CME_Voice(config-controller)# pri-group timeslots 1-24?
fas_d Specify the operation of the D-channel timeslot.
service Specify the service type
CME_Voice(config-controller)# pri-group timeslots 1-24
CME_Voice(config-controller)*Z
CME_Voice# show voice port summary
```

| PORT CH SIG-TYPE ADMIN OPER STATUS EC |
|---|---|---|---|---|---|---|---|
| 1/0:23 | 01 | isdn-voice | up | dorm | none | y |
| 1/0:23 | 02 | isdn-voice | up | dorm | none | y |
| 1/0:23 | 03 | isdn-voice | up | dorm | none | y |
| 1/0:23 | 04 | isdn-voice | up | dorm | none | y |
| 1/0:23 | 05 | isdn-voice | up | dorm | none | y |
| 1/0:23 | 06 | isdn-voice | up | dorm | none | y |
| 1/0:23 | 07 | isdn-voice | up | dorm | none | y |
| 1/0:23 | 08 | isdn-voice | up | dorm | none | y |
| 1/0:23 | 09 | isdn-voice | up | dorm | none | y |
| 1/0:23 | 10 | isdn-voice | up | dorm | none | y |
| 1/0:23 | 11 | isdn-voice | up | dorm | none | y |
| 1/0:23 | 12 | isdn-voice | up | dorm | none | y |
| 1/0:23 | 13 | isdn-voice | up | dorm | none | y |
| 1/0:23 | 14 | isdn-voice | up | dorm | none | y |
| 1/0:23 | 15 | isdn-voice | up | dorm | none | y |
| 1/0:23 | 16 | isdn-voice | up | dorm | none | y |
| 1/0:23 | 17 | isdn-voice | up | dorm | none | y |
| 1/0:23 | 18 | isdn-voice | up | dorm | none | y |
| 1/0:23 | 19 | isdn-voice | up | dorm | none | y |
| 1/0:23 | 20 | isdn-voice | up | dorm | none | y |
| 1/0:23 | 21 | isdn-voice | up | dorm | none | y |
| 1/0:23 | 22 | isdn-voice | up | dorm | none | y |
| 1/0:23 | 23 | isdn-voice | up | dorm | none | y |

在配置 CCS 连接时，第一步是设置 ISDN 交换机类型以匹配您的本地服务提供商使用的交换机类型。示例 6-6 将设置为 primary-sessions。在配置交换机类型后，路由器允许您输入 `pri-group` 命令。这与 `dso-group` 命令的作用完全相同，它允许您为配合 PSTN 运营商配置特定数量的时隙。该命令不允许您选择信令类型，因为路由器假定使用 ISDN PRI 信令。

**注意：** 此示例假设您有足够的数字信号处理器 (DSP) 资源来支持完整的 PRI 连接。如果您的路由器没有足够的 DSP，配置可能会失败。

注意：请记住，这一切背后的引擎是 CME 路由器中的 DSP 资源。这些“得力干”将模拟音频转换为数字（VoIP 数据包），反之亦然。如果 CME 路由器没有任何 DSP 资源，这种转换将是不可能的。

## 配置 POTS 拨号伙伴 (Dial Peers)

如前所述，您可以使用 POTS 拨号伙伴为从传统电话世界连接到 VoIP 网络的任何设备定义可性信息。这包括连接到 FXO、FXS、E&M 以及数字 BRI/T1/E1 接口的设备。

提示：如果您连接到没有 IP 地址的设备（例如模拟电话、传真机、PBX 或 PSTN），它就是一个 POTS 拨号伙伴。

图 6-6 中的网络演示了 POTS 拨号伙伴的配置。

### 图 6-6 拨号伙伴配置场景

配置从 CME_A 路由器开始。要创建 POTS 拨号伙伴，您可以在全局配置模式下使用语法 `dial-peer voice <tag>`。`tag` 值可以是您想要的任何数字（1 到 2,147,483,647），只要它在路由器上是唯一的即可。尽管此 `tag` 对您分配给设备的可用性信息没有影响，但许多管理员有一个共同做法，即将拨号伙伴 `tag` 与设备的电话号码关联。示例 6-7 解释了图 6-6 中所示连接到 CME_A 路由器 FXS 端口的模拟电话的分扩展。

### 示例 6-7 为 FXS 端口配置 POTS 拨号伙伴

```
CME_A(config)# dial-peer voice ?
<1-2147483647> Voice dial-peer tag
CME_A(config)# dial-peer voice 1101 ?
mmoip Multi Media Over IP
npots Telephony
```

```
vofr Voice over Frame Relay
voip Voice over IP
cME_A(config)# dial-peer voice 1101 pots
cME_A(config-dial-peer)# destination-pattern ?
WORD A sequence of digits - 代表前缀或完整电话号码
cME_A(config-dial-peer)# destination-pattern 1101
cME_A(config-dial-peer)# port 0/0/0
cME_A(config-dial-peer)# exit
cME_A(config-dial-peer)# dial-peer voice 1102 pots
cME_A(config-dial-peer)# destination-pattern 1102
cME_A(config-dial-peer)# port 0/0/1
```

创建拨号伙伴后，您可以使用 `destination-pattern` 和 `port` 命令将电话号码分配给连接的设备。输入此配置后，您可以在连接到 CME A 路由器的电话之间拨打。在拨打任何电话之前，最好始终验证拨号伙伴配置。

> **提示：** 创建拨号伙伴后，在进入配置模式时不再需要指定拨号伙伴的类型。例如，要创建一个 `tag` 为 50 的 VoIP 拨号伙伴，您输入 `dial-peer voice 50 voip`。如果以后想返回配置模式，只需输入 `dial-peer voice 50`。如果您想更改拨号伙伴类型（VoIP 或 POTS），则必须删除该拨号伙伴（`no dial-peer voice 50`）并重新创建。

`show dial-peer voice` 命令（不带 `summary` 关键字）会显示路由器上的所有拨号伙伴，但每个拨号伙伴都会占用一页输出。虽然这些信息有时很有用，但示例 6-8 所示的摘要视图通常更容易理解。注意输出底部的拨号伙伴 `tag` 1101 和 1102，它们被显示为具有正确拨号目的地模式和端口分配的 POTS 拨号伙伴。其他拨号伙伴（`tag` 为 20005–20014）是 CME 路由器为第 5 章“使用 CME 管理端点和用户”中配置的 ephone-dns 创建的拨号伙伴。

### 示例 6-8 验证拨号伙伴

```
cME_A# show dial-peer voice summary
dial-peer hunt 0
```

| TAG | TYPE | MIN | OPER | PREFIX | DEST-PATTERN | FER | THRU | SESS-TARGET | STAT | PORT |
|---|---|---|---|---|---|---|---|---|---|---|
| 20005 | pots | up | up | 1500$ |  | 0 |  | 50/0/20 |
| 20006 | pots | up | up | 1501$ |  | 0 |  | 50/0/21 |
| 20007 | pots | up | up | 1502$ |  | 0 |  | 50/0/22 |
| 20008 | pots | up | up | 1503$ |  | 0 |  | 50/0/23 |
| 20009 | pots | up | up | 1504$ |  | 0 |  | 50/0/24 |
| 20010 | pots | up | up | 1505$ |  | 0 |  | 50/0/25 |
| 20011 | pots | up | up | 1506$ |  | 0 |  | 50/0/26 |
| 20012 | pots | up | up | 1507$ |  | 0 |  | 50/0/27 |
| 20013 | pots | up | up | 1508$ |  | 0 |  | 50/0/28 |
| 20014 | pots | up | up | 1509$ |  | 0 |  | 50/0/29 |
| 1101 |  |  |  |  | 1101 |  | up |  | 0/0/0 |
| 1102 | pots | up | up | 1102 |  | up |  | 0/0/1 |

您可以通过在设备之间拨打电话来测试配置。这是一本书，您实际上不会听到电话铃响，因此示例 6-9 显示了一个实用的调试命令，您可以使用它查看连接到 FXS 端口的电话拨号数字。

### 示例 6-9 使用 debug dialpeer 分析数字处理

*(注：原始文本中存在大量 OCR 重复和错误，已根据要求进行逻辑处理。)*

## CCNA Voice 640-461 官方认证指南

`destination-pattern 9......` 命令（用于七位拨号），路由器在将通话发送到 PSTN 之前会自动剥离显式定义的数字 9。

在示例 6-10 中，在将通话发送到 PBX 系统之前剥离数字 2 并不是预期的行为。因此，`no digit-strip` 命令可以防止这种自动数字剥离过程。

**注意：**自动数字剥离功能适用于 POTS 拨号（dial peers）。VoIP 拨号（在后续节中讨论）不会自动剥离数字。

## 配置 VoIP 拨号

如图 6-7 所示的场景中，POTS 拨号为旧留语音设备提供连接。然而，CME_A 和 ROUTER_B 被一个 IP WAN 连接隔开，旧留语音设备必须跨越该连接来实现端到端通信。

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_153_0.png)

**图 6-7** 拨号配置场景

为了实现这种连接，你必须使用 VoIP 拨号，因为通话正在跨基于 IP 网络。示例 6-11 在 CME_A 和 ROUTER_B 设备上配置了必要的 VoIP 拨号。

### 示例 6-11 配置 VoIP 拨号

```
CME_A(config)# dial-peer voice 2000 voip
CME_A(config-dial-peer)# destination-pattern 2...
CME_A(config-dial-peer)# session target ?  WORD 一个指定会话目标的字符串
CME_A(config-dial-peer)# session target ipv4:10.1.1.2
CME_A(config-dial-peer)# codec ?  clear-channel Clear Channel 64000 bps (无语音功能：仅数据传输)
g711alaw      G.711 A Law 64000 bps
g711ulaw      G.711 U Law 64000 bps
g722-48      G722-48K 64000 bps - 仅支持 H.320<->H.323通话
```

| g722-56 | G722-56K 64000 bps - 仅支持 H.320<->H.323通话 |
| g722-64 | G722-64K 64000 bps - 仅支持 H.320->H.323通话 |
| g723ar53 disabled | G723.1 ANNEX-A 5300 bps (包含内置 vad，无法 | |
| g723ar63 disabled | G723.1 ANNEX-A 6300 bps (包含内置 vad，无法 | |
| g723s53 | G723.1 5300 bps |
| g723r63 | G723.1 6300 bps |
| g726r16 | G726 16000 bps |
| g726r24 | G726 24000 bps |
| g726r32 | G726 32000 bps |
| g728 | G728 16000 bps |
| g729b8 disabled | G729 ANNEX-B 8000 bps (包含内置 vad，无法 | |
