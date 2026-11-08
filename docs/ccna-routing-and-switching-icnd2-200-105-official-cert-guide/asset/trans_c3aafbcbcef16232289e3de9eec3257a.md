

```text
ipv6 eigrp 1
!
interface serial 0/0/0
 description link to R3
 ipv6 address 2001:db8:1:6::2/64
 ipv6 eigrp 1
!
interface serial 0/0/1
 description link to R1
 ipv6 address 2001:db8:1:5::2/64
 ipv6 eigrp 1
!
interface serial 0/1/0
 description link to R4
 ipv6 address 2001:db8:1:8::2/64
 ipv6 eigrp 1
```

> **注意** IOS 允许使用 EIGRP 配置模式下的 shutdown 和 no shutdown 命令来禁用然后重新启用 EIGRP for IPv6 路由进程。虽然较新版本的 IOS 默认启用，但请注意，较旧版本的 IOS 默认处于禁用状态，需要先在 EIGRP 配置模式下配置 no shutdown 命令，EIGRP for IPv6 才能正常工作。

## 其他 EIGRP for IPv6 配置设置

示例24-1和24-2展示了 EIGRP for IPv6 配置的基础。接下来的几页将讨论与 EIGRP for IPv4 相比的一些配置选项。

### 设置带宽和延迟以影响 EIGRP for IPv6 路由选择

默认情况下，EIGRP for IPv6 在计算每条路由的度量时，使用与 EIGRP for IPv4 完全相同的设置。需要特别说明的是，这些设置并非相似或仅仅使用相同的命令语法，而是完全相同。EIGRP for IPv6 使用与 EIGRP for IPv4 完全相同的设置，具体来说就是使用 bandwidth 和 delay 接口子命令配置的接口带宽和延迟设置。更改这些值会同时影响 EIGRP for IPv4 和 EIGRP for IPv6 的度量计算。

EIGRP for IPv6 还使用与 EIGRP for IPv4 完全相同的公式来计算路由的度量。因此，在某些条件下，路由器到某个 IPv4 子网的 EIGRP for IPv4 度量，与同一路由器到同一位置 IPv6 子网的 EIGRP for IPv6 路由度量将会相同。

例如，在图24-3中，所有路由器都是双栈路由器，网络中所有接口上都启用了 EIGRP for IPv4 和 EIGRP for IPv6。子网 10.1.33.0/24 位于右上角，与 IPv6 子网33（2001:DB8:1:33::/64）位于同一位置。R1 的 EIGRP for IPv4 和 EIGRP for IPv6 进程将根据相同的接口带宽和延迟设置集合，为这些路由计算出完全相同的度量。

![](img/79473ea15699e01619d2aa789f5bd43b_706_0.png)

**图24-3** *IPv4子网33和IPv6子网33在R4上的相同位置*

示例24-3显示了图24-3中R1上各子网的IPv4和IPv6路由。请注意，所有情况下突出显示的度量都是2,684,416。

**示例24-3** *使用EIGRP for IPv4和EIGRP for IPv6时IPv4与IPv6路由的相同度量*

```text
R1# show ip route | section 10.1.33.0
D    10.1.33.0/24 [90/2684416] via 10.1.5.2, 00:02:23, Serial0/0/0
                      [90/2684416] via 10.1.4.3, 00:02:23, Serial0/0/1

R1# show ipv6 route | section 2001:DB8:1:33::/64
D   2001:DB8:1:33::/64 [90/2684416]
     via FE80::FF:FE00:1, Serial0/1/0
     via FE80::FF:FE00:2, Serial0/1/0
```

请注意，两条命令都在R1上列出了子网33的两条等成本路由，但输出格式略有不同。show ip route 命令将目标子网与第一条路由的转发信息放在同一行；而 show ipv6 route 命令将目标前缀放在第一行，每条路由的转发信息分别位于第二行和第三行。

### EIGRP 负载均衡

EIGRP for IPv6 和 EIGRP for IPv4 在等成本和非等成本负载均衡上使用完全相同的概念和完全相同的配置命令语法。不过，EIGRP for IPv6 有自己的配置设置，通过 EIGRP for IPv6 配置模式下的 maximum-paths 和 variance 命令进行配置。EIGRP for IPv4 则在 EIGRP for IPv4 配置模式下使用这两个相同的命令进行单独设置。

例如，假设在一个双栈网络中，路由器同时使用 EIGRP for IPv4 和 EIGRP for IPv6。网络工程师很可能会为这两种路由协议选择相同的 variance 和 maximum-paths 设置。但是，为了说明差异，假设工程师选择了不同的设置，如下所示：

- EIGRP for IPv4：最多 2 条路由，非等成本路由的 variance 为 3
- EIGRP for IPv6：最多 5 条路由，非等成本路由的 variance 为 4

示例24-4演示了如何为这两个不同的路由进程进行不同的设置。但请注意，这些命令恰好使用了完全相同的语法。

**示例24-4** *为每个路由进程设置负载均衡参数*

```text
R1# configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
! First, configure the settings for IPv4
R1(config)# router eigrp 10
R1(config-router)# maximum-paths 2
R1(config-router)# variance 3
! Next, configure similar settings for IPv6
R1(config)# ipv6 router eigrp 11
R1(config-rtr)# maximum-paths 5
R1(config-rtr)# variance 4
R1(config-rtr)# ^Z
R1#
```

### EIGRP 计时器

EIGRP for IPv6 和 EIGRP for IPv4 在 Hello 和保持计时器上使用与 EIGRP for IPv4 完全相同的概念。为了允许为每个路由进程设置不同的值，IOS 在 EIGRP for IPv6 和 EIGRP for IPv4 命令上提供了略微不同的语法，其中 EIGRP for IPv6 命令使用关键字 ipv6 而不是 ip。除此之外，EIGRP for IPv6 的语法与 EIGRP for IPv4 版本的命令相同。

示例24-5展示了同时更改 EIGRP for IPv4 和 EIGRP for IPv6 的 Hello 计时器的示例，目的只是为了并排展示不同的命令。对于 EIGRP for IPv4，Hello 计时器设置为 6 秒；对于 EIGRP for IPv6，设置为 7 秒。

**示例24-5** *设置 EIGRP for IPv4 和 EIGRP for IPv6 的 Hello 计时器*

```text
R1# configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
R1(config)# interface gigabitethernet0/1
R1(config-if)# ip hello-interval eigrp 10 6
R1(config-if)# ipv6 hello-interval eigrp 11 7
R1(config-if)# ^Z
R1#
```

这里计时器值的选择是任意的，只是为了清楚说明哪条命令对应哪个路由协议。在实际网络中，EIGRP for IPv4 和 EIGRP for IPv6 的这些设置很可能采用相同的值。

## EIGRP for IPv6 验证与故障排除

就本书讨论的深度而言，EIGRP for IPv4 和 EIGRP for IPv6 的行为几乎完全相同。前面，表24-2并排列出了配置命令，以展示它们的相似之处。本章的第二个主要部分现在讨论 EIGRP for IPv6 的验证与故障排除，EIGRP for IPv6 与其老前辈 EIGRP for IPv4 之间还有更多相似之处。

EIGRP for IPv6 和 EIGRP for IPv4 之间存在如此多的相似之处，以至于你大可以认为它们的工作原理相同，只有少数差异，如下列表所述：

![](img/79473ea15699e01619d2aa789f5bd43b_708_0.png)

- EIGRP for IPv6 通告 IPv6 前缀，而 EIGRP for IPv4 通告 IPv4 子网。
- EIGRP for IPv6 的 show 命令使用关键字 ipv6，位置与 EIGRP for IPv4 的 show 命令使用关键字 ip 的位置相同。
- EIGRP for IPv6 使用相同的检查清单来决定是否成为邻居，不同之处在于，只要 IPv6 地址位于不同子网，EIGRP for IPv6 路由器也有可能成为邻居。（EIGRP for IPv4 邻居必须位于同一 IPv4 子网。）
- EIGRP for IPv6 没有自治系统的概念（而 EIGRP for IPv4 有）。

可以看到，这里提到的差异列表很短。通过本章剩余部分的大量 show 命令输出示例，这些相似之处将变得更加清晰。首先，图24-4回顾了本章讨论的 EIGRP for IPv6 show 命令。请注意，图中所有命令都使用与 EIGRP for IPv4 对应命令相同的语法，只是将 ip 改为了 ipv6。

![](img/79473ea15699e01619d2aa789f5bd43b_708_1.png)

**图24-4** *EIGRP for IPv6 验证命令参考*

与前一章的流程类似，本章的第二个主要部分按照 EIGRP for IPv6 启动进程时的相同一般顺序进行讨论。本节首先检查 EIGRP for IPv6 接口，然后是邻居、拓扑，最后是 IPv6 路由。

