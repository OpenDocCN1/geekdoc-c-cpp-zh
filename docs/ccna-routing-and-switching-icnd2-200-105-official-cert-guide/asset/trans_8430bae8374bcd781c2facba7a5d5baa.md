
首先，介绍 HSRP 规则。当一台路由器（称为本地路由器）具有启用了 HSRP 的接口，并且该接口启动时，路由器会发送 HSRP 消息，协商它应成为活动路由器还是备用路由器。当它发送这些消息时，如果它……

![](img/79473ea15699e01619d2aa789f5bd43b_612_0.png)

- **步骤 1。** ……发现子网中没有其他 HSRP 路由器，则本地路由器成为活动路由器。
- **步骤 2。** ……发现一个现有的 HSRP 路由器，并且两者当前正在协商决定谁应成为 HSRP 活动路由器，则路由器进行协商，具有最高 HSRP 优先级的路由器成为 HSRP 活动路由器。
- **步骤 3。** ……发现子网中有一个现有的 HSRP 路由器，并且该路由器已经充当活动路由器：
  - **A.** 如果配置为不抢占（默认；**no standby preempt**），则本地路由器成为备用路由器，即使它具有更好（更高）的优先级。
  - **B.** 如果配置了抢占（**standby preempt**），则本地路由器会将其优先级与活动路由器进行比较；如果本地路由器优先级更好（更高），则本地路由器接管（抢占）现有活动路由器，成为新的 HSRP 活动路由器。

列表中的步骤 1 和步骤 2 相当明显，但步骤 3A 和 3B 值得再仔细看看。例如，本章到目前为止的示例显示，R1 的 G0/0 优先级为 110，而 R2 的 G0/0 优先级为 100。示例 20-3 中的 show 命令显示 R1 当前是 HSRP 活动路由器。同一示例还列出了 R1 和 R2 的一行，确认“preemption disabled”（抢占已禁用），这是默认设置。

为了展示对步骤 3A 逻辑的测试，示例 20-4 展示了一个过程：R1 的 G0/0 接口被禁用，然后再次启用，但在此之前让路由器 R2 有足够时间接管并成为活动路由器。也就是说，R1 恢复启动，但 R2 已经是组 1 的 HSRP 活动路由器。该示例底部列出了来自 R2 的 show standby brief 命令的输出，确认 R2 成为 HSRP 活动路由器，R1 成为备用路由器（10.1.1.9），证明在这种情况下 R1 不会抢占 R2。

### **示例 20-4** *展示不抢占如何在 R1 恢复后使 R1 保持为备用路由器*

```text
! First, R1's G0/0 is disabled and enabled; the ending log message shows a standby
! state.

R1# configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
R1(config)# interface gigabitEthernet 0/0
R1(config-if)# shutdown
*Mar  8 18:10:29.242: %HSRP-5-STATE: GigabitEthernet0/0 Grp 1 state Active ->
  Init
*Mar  8 18:10:31.205: %LINK-5-CHANGED: Interface GigabitEthernet0/0, changed state to
  administratively down
*Mar  8 18:10:32.205: %LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet
  0/0, changed state to down
R1(config-if)#
R1(config-if)# no shutdown
R1(config-if)# ^Z
R1#
*Mar 8 18:11:08.355: %HSRP-5-STATECHANGE: GigabitEthernet0/0 Grp 1 state Speak ->
  Standby
! Now from R2, note R2 is active, and 10.1.1.9 (R1) is standby
R2# show standby brief

                 P indicates configured to preempt.

Interface   Grp  Pri  P  State   Active       Standby      Virtual IP
Gi0/1       1    100     Active  local        10.1.1.9     10.1.1.1
```

如果在前一个场景中为 R1 配置了抢占，那么当 R1 的接口恢复启动时，R1 就会从 R2 那里接管。示例 20-5 正是展示了这一点。在收集示例 20-5 的输出之前，网络已被恢复到与示例 20-4 开始时相同的初始状态：R1 为活动路由器，R2 为备用路由器。在示例 20-5 中，R1 的接口被关闭，然后使用 standby 1 preempt 命令配置抢占，从而启用抢占。接着，在再次启用接口后，R1 接管成为 HSRP 活动路由器，如该示例底部来自 R2 的 show standby brief 命令输出所示。该输出现在显示本地路由器的状态为 Standby（备用），活动路由器为 10.1.1.9（R1）。

### **示例 20-5** *展示抢占如何在恢复后使 R1 接管成为活动路由器*

```text
! First, R1’s G0/0 is disabled and enabled; the ending log message shows a standby
! state.
R1# configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
R1(config)# interface gigabitEthernet 0/0
R1(config-if)# shutdown
*Mar 8 18:10:29.242: %HSRP-5-STATECHANGE: GigabitEthernet0/0 Grp 1 state Active ->
  Standby
*Mar 8 18:10:31.205: %LINK-5-CHANGED: Interface GigabitEthernet0/0, changed state to
  administratively down
*Mar 8 18:10:32.205: %LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEther
  net0/0, changed state to down
R1(config-if)# standby 1 preempt
R1(config-if)# no shutdown
R1(config-if)# ^Z
R1#
*Mar 8 18:19:14.355: %HSRP-5-STATECHANGE: GigabitEthernet0/0 Grp 1 state Listen ->
  Active
! Now from R2, note it is active, and 10.1.1.9 (R1) is standby

*Mar 8 18:18:55.948: %HSRP-5-STATECHANGE: GigabitEthernet0/0 Grp 1 state Standby ->
  Active
*Mar 8 18:19:14.528: %HSRP-5-STATECHANGE: GigabitEthernet0/0 Grp 1 state Active ->
  Speak
*Mar 8 18:19:26.298: %HSRP-5-STATECHANGE: GigabitEthernet0/0 Grp 1 state Speak ->
  Standby
```

关于表中的细节，请务必查看版本 1 和版本 2 的 MAC 地址。Cisco 为 HSRPv1 保留前缀 0000.0C07.AC，为 HSRPv2 保留前缀 0000.0C9F.F。HSRPv1 每个接口最多可有 256 个 HSRP 组，因此使用最后两个十六进制数字来标识 HSRP 组。例如，使用版本 1 的 HSRP 组 1 将使用以十六进制 01 结尾的虚拟 MAC 地址。同样，由于 HSRPv2 每个接口支持 4096 个组，MAC 地址保留三个十六进制数字来标识组。使用版本 2 的 HSRP 组 1 将使用以十六进制 001 结尾的虚拟 MAC 地址。

## HSRP 故障排除

HSRP 故障排除遵循本书中一些熟悉的主题，涉及你应准备执行的活动类型。首先，你需要掌握配置细节，以便知道配置何时正确或错误。作为其中的一部分，你需要准备好根据除 show running-config 命令之外的 show 命令来推断配置；你需要能够尽可能根据其他 show 命令反向推导出配置。

此外，你应当清楚同一 HSRP 组中的路由器上哪些 HSRP 配置设置需要匹配。而且，了解在发生某些常见配置错误时 show 命令输出会是什么样子，总是有帮助的。

### 检查 HSRP 配置

首先，关于确定配置的问题，再花点时间思考 show standby 命令的输出，但现在要以重建配置为目标。为此，示例 20-6 重复了本章贯穿使用的运行示例中路由器 R1 的配置。它还重复了示例 20-3 中相同的 show standby 命令输出。在这个新示例中，show 命令输出中突出显示的注释列出了输出所基于的匹配配置命令。

### **示例 20-6** *在 show standby 命令输出中查找 HSRP 配置*

```text
! First, the configuration of the HSRP group:
interface GigabitEthernet0/0
 ip address 10.1.1.9 255.255.255.0
 standby version 2
 standby 1 ip 10.1.1.1
 standby 1 priority 110
 standby 1 name HSRP-group-for-book

! Next, the show standby command output
R1# show standby
GigabitEthernet0/0 - Group 1 (version 2)                    ! standby version 2
  State is Active
    6 state changes, last state change 00:12:53
  Virtual IP address is 10.1.1.1                         ! standby 1 ip 10.1.1.1
  Active virtual MAC address is 0000.0c9f.f001
    Local virtual MAC address is 0000.0c9f.f001 (v2 default)
  Hello time 3 sec, hold time 10 sec
    Next hello sent in 1.696 secs
Preemption disabled                                      ! no standby 1 preempt
    {default}
Active router is local
Standby router is 10.1.1.129, priority 100 (expires in 8.096 sec)
Priority 110 (configured 110)                            ! standby 1 priority 110
Group name is "HSRP-group-for-book" (cfgd)             ! standby 1 name HSRP-group-for-book
```

如果你仔细阅读 **show** 命令输出最右侧的注释（以 ! 开头的注释），就可以在脑海中将 **show** 命令输出同一行上的概念与示例顶部的四条 standby 配置命令联系起来。

接下来，要使 HSRP 正常工作，某些 HSRP 参数必须匹配。例如，如果两台路由器本应位于同一个 HSRP 组中，但配置了两个不同的 HSRP 版本，它们将无法理解彼此的消息，会忽略彼此，并各自独立运行。以下列表详细列出了需要检查的一些重要事项，以确保配置应能正常工作：

- 路由器必须配置相同的 HSRP 版本（standby version {1 | 2}）。
- 路由器必须配置相同的 HSRP 组号（standby number ...）。
- 路由器必须配置相同的虚拟 IP 地址（standby number ip address）。
- 虚拟 IP 地址必须 (a) 与接口 IP 地址位于同一子网，并且 (b) 未被该子网中的任何其他设备使用（包括其他 HSRP 路由器）（standby number ip address）。
- 在连接的二层网络中，路由器或三层交换机上的接口必须位于同一 VLAN 中。
- 不应有 ACL 过滤两台路由器之间的 HSRP 消息。（HSRP 使用 UDP 端口 1985；版本 1 发送到组播地址 224.0.0.2，而版本 2 发送到 224.0.0.102。）

### HSRP 配置错误的症状

IOS 无法检测出与上一列表中良好配置建议不同的若干配置错误。因此，想一想良好的配置会是什么样，然后想象故意错误配置单个项目。会出现什么症状？表 20-4 列出了四种此类故意配置错误。每一种都假设只犯了一个错误。在表之后，本章会逐一仔细研究。

**表 20-4 — HSRP 配置错误场景及预期结果**

| 参考编号 | 场景 | 两台路由器都成为活动路由器？ | 检测到地址重复？ | VIP 是否随活动路由器变化？ |
|---|---|---|---|---|
| 1 | HSRP 版本不匹配 | 是 | 是 | 不适用 |
| 2 | HSRP 组号不匹配 | 是 | 是 | 不适用 |
| 3 | ACL 阻止 HSRP 数据包 | 是 | 否 | 不适用 |
| 4 | 路由器配置了不同的 VIP | 否 | 不适用 | 是 |
