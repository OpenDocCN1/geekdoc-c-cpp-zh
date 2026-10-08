

最后，你可以使用示例 6-4 所示的语法为连接到 FXS 端口的设备配置主叫显示信息。

## 示例 6-4 配置 FXS 端口主叫显示信息

```
CME_Voice(config)# voice-port 0/0/0
CME_Voice(config-voiceport)# station-id name 3rd Floor Fax
CME_Voice(config-voiceport)# station-id number 5551000
```

此配置允许系统中的其他设备在 FXS 端口连接设备向其拨号时，接收主叫名称和信息。

## 外线端口 (FXO Ports)

如图 6-2 所示，FXO 端口作为接入公共交换电话网络（PSTN）局端（CO）或私有分支交换（PBX）系统的中继。

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_140_0.png)

## 图 6-2 FXO 端口连接

FXO 端口使用的许多命令与 FXS 端口相同，例如环路起始信号或地线起始信号，以及用于设置主叫显示信息的 `station-id`。有两个额外的命令值得注意：

- dial-type
- ring number

`dial-type <dtmf|pulse>` 命令允许你选择使用双音多频（DTMF）拨号或脉冲拨号。然而世界上某些地区仍需要使用脉冲拨号（以及拨号电话）。如果你在这些地区之一安装语音网络，此命令用于：

`ring number <number>` 命令允许你指定路由器在接听 FXO 端口的入叫电话时应通过的响铃次数。默认情况下，此设置为一个响铃，导致路由器立即接听入叫。在某些情况下，路由器的 FXO 端口可能连接到其他设备的环路（例如在家庭办公环境中），用户希望其他设备在路由器接听并处理线路之前有机会先行。在这种情况下，你可以将 `ring number` 设置为较高的值。

## 配置数字语音端口

Cisco 以语音和 WAN 接口卡（VWIC）的形式为路由器提供了数字 T1 和 E1 端口。这些卡片为你提供了配置数据连接或语音连接的灵活性。与模拟接口不同，你必须在数字接口正常工作之前对其进行配置，因为路由器不知道你将使用的网络类型。如第1章“传统语音与统一语音”所述，存在两种网络配置：T1/E1 关联信令（CAS）或 T1/E1 通道信令（CCS），通常称为 ISDN 主接口 [PRI]。你所连接的网络类型决定了你用于配置 VWIC 卡的命令：用于 T1/E1 CAS 连接的 `ds-group` 或用于 T1/E1 CCS 连接的 `pri-group`。

示例 6-5 展示了如何配置 T1 CAS 接口的所有 24 个通道以连接 PSTN 运营商。

## 示例 6-5 配置 T1 CAS PSTN 接口

```
CME Voice# show controllers t1
T1 1/0 is down.
Application type is Channelized T1
cableLength is longgain36 db
Transmitter is sending remote alarm.
Receiver has loss of signal.
alarmtrigger is not set
Soaking time: 3, Clearance time: 10
AIS State:Clear LOS State:Clear LOF State:Clear
Version info Firmware: 20585620, FPGA: 20, spm_count = 0
Framing is SF, Line Code is AMI, Clock Source is Line.
Current port master clock:local osc on this network module
Data in current interval (215 seconds elapsed)
@ Line Code Violations, @ Code Violations
@ Slip Secs, @ Fr Secs, @ Err Secs, @ Degraded Mins
@ Errored Secs, @ Bursty Err Secs, @ Severely Err Secs, 215 Unavail Secs
CME_Voice# configure terminal
Enter configuration commands, one per line. End with CNTL/Z.
CME_Voice(config)# controller t1 1/0
CME_Voice(config-controller)# framing ?
esf Extended Superframe
CME_Voice(config-controller)# framing esf
CME_Voice(config-controller)# linecode ?
```

```
ami AMI encoding
b8zs B8ZS encoding
CME_Voice(config-controller)# linecode b8zs
CME_Voice(config-controller)# clock source ?
free-running Free Running Clock
internal Internal Clock
line Recovered Clock
```

```
CME_Voice(config-controller)# clock source line
CME_Voice(config-controller)# ds0-group ?
<0-23> Group Number
CME_Voice(config-controller)# ds0-group 1
timeslots List of timeslots in the ds0-group
CME_Voice(config-controller)# ds0-group 1 timeslots ?
<1-24> List of T1 timeslots
CME_Voice(config-controller)# ds0-group 1 timeslots 1-24 ?
type Specify the type of signaling
<cr>
```

```
CME_Voice(config-controller)# ds0-group 1 timeslots 1-24 type
CME_Voice(config-controller)# ds0-group 1 timeslots 1-24 type
&m-delay-start
&m-fgd
&m-immediate-start
&m-radio
&m-wink-start
&m-type
&m-none
CME_Voice(config-controller)# ds0-group 1 timeslots 1-24 type
```
CME_Voice(config-controller)# ds0-group 1 timeslots 1-24 type
CME_Voice(config-controller)# show port summary
PORT TYPE STATUS
=====================
| IN | OUT | STATUS |
|---|---|---|
| 01 | | down |
| 02 | | down |
| 03 | | down |
| 04 | | down |
| 05 | | down |
| 06 | | down |
| 07 | | down |
| 08 | | down |
| 09 | | down |
| 10 | | down |
| 11 | | down |
| 12 | | down |
| 13 | | down |
| 14 | | down |
| 15 | | down |
| 16 | | down |
| 17 | | down |
| 18 | | down |
| 19 | | down |
| 20 | | down |
| 21 | | down |
| 22 | | down |
| 23 | | down |
| 24 | | down |

