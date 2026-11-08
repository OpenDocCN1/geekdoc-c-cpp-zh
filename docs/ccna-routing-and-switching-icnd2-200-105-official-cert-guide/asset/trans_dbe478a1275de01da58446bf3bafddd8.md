
首先，连接到 ISP 的物理接口（本例中为 G0/1）没有 IP 地址，也不会学习 IP 地址，并且在使用 PPPoE 期间不需要 IP 地址。是的，IP 流量将通过该物理接口进出 ISP，但不是通过在物理接口（本例中为 G0/1）上启用 IP 来实现的。（相反，第 3 层逻辑应用于拨号器接口，然后由拨号器接口使用物理接口。）因此，物理接口需要 **no ip address** 命令来确保那里不存在地址。

其次，拨号器接口充当 PPPoE 的主要第 3 层接口。拨号器接口将在 **show ip route** 命令的输出中列为出站接口，并且拨号器接口可以在定义静态路由的命令中被引用。实际上，如果本例中的客户路由器想要使用默认路由将数据包转发到 Internet，它可以配置为 **ip route 0.0.0.0 0.0.0.0 dialer 2**。该命令不会引用物理以太网接口。

拨号器接口确实需要一个 IP 地址。为了动态学习地址，PPPoE 使用 PPP 的 IPCP 而不是 DHCP。要实现这一点，客户路由器（R1）使用 **ip address negotiated** 命令，这是 IOS 命令，意思是“使用 PPP IPCP 协商地址”。请注意，如果客户想要使用静态 IP 地址，也许是由 ISP 分配的地址，以便 GRE 配置稳定，则可以使用通常的 **ip address address mask** 接口子命令来配置该地址。

最后，作为一个重要的日常维护项，将 IP 数据包的最大传输单元（MTU）设置为 1492，如 **mtu 1492** 接口子命令所示。通常，IP MTU 默认为 1500。PPPoE 增加了另一个 8 字节的报头，使 IP 数据包的空间减少了 8 字节，因此将 IP MTU 减小到 1492 可以防止路由器进行不必要的分片工作。

## PPPoE 配置摘要

本节在单个示例的上下文中介绍了配置 PPPoE 的命令。以下配置清单总结了该配置，以便于复习和研究。

![](img/79473ea15699e01619d2aa789f5bd43b_473_0.png)

- **步骤 1.** 配置第 1 层细节。
  - **步骤 1A.** 配置拨号器接口：
    - **I.** 使用 **interface dialer** *编号* 命令创建拨号器接口；选择一个本地路由器上尚未被其他拨号器接口使用的编号。
    - **II.** 使用 **dialer-pool** *编号* 接口子命令引用一个可用于 PPPoE 的以太网系列接口池。
  - **步骤 1B.** 配置物理接口：
    - **I.** 使用 **pppoe-client dial-pool-number** *编号* 接口子命令将该接口添加到拨号器接口上配置的同一池编号。
- **步骤 2.** 配置第 2 层细节。
  - **步骤 2A.** 在拨号器接口上配置 PPP：
    - **I.** 使用 **encapsulation ppp** 接口子命令在拨号器接口上启用 PPP。
    - **II.** 使用 `ppp chap hostname name` 接口子命令定义用于向 ISP 认证的用户名。
    - **III.** 使用 `ppp chap password password` 接口子命令定义用于向 ISP 认证的密码。
  - **步骤 2B.** 在以太网接口上配置 PPPoE：
    - **I.** 使用 `pppoe enable` 接口子命令启用 PPPoE。（当配置了 `pppoe-client` 接口子命令时，IOS 会自动添加此命令。）
- **步骤 3.** 配置第 3 层细节。
  - **步骤 3A.** 在拨号器接口上配置 IP：
    - **I.** 使用 `ip address negotiated` 接口子命令告诉拨号器接口使用 PPP 的 IPCP 来学习要使用的 IP 地址。
    - **II.** 使用 `mtu 1492` 接口子命令将默认值 1500 更改为允许 PPPoE 使用的 8 个额外报头字节。
  - **步骤 3B.** 在以太网接口上禁用 IP：
    - **I.** 使用 `no ip address` 接口子命令在物理接口上禁用 IP 路由，并从接口中移除 IPv4 地址。

### 关于 PPPoE 实验室实验的简要旁白

对于本书中的大多数配置主题，您学到的信息足以进入实验室，配置几台路由器和交换机使该功能正常工作，然后使用 `show` 命令进行实验。但是，本章不解释 ISP 的 PPPoE 配置的细节，因为 PPPoE 考试主题指出它仅涉及客户端。而且客户路由器和 ISP 路由器上的配置并不相同。

但是，对于那些想要尝试重新创建本书本节中所示示例的人，请这样做。为了给您一个起点，请对 ISP 使用类似示例 15-10 的配置；这是来自标记为 R2 的路由器的相关配置的副本，该路由器在创建即将到来的示例时使用。然后使用一个实验，在两台路由器之间使用交叉以太网电缆，拓扑类似于图 15-24。

**示例 15-10** ISP 路由器配置示例

```text
ip local pool WOPool 10.1.3.2 10.1.3.254
bba-group pppoe WOGROUP
 virtual-template 1
!
username Fred password Barney
!
interface virtual-template 1
 ip address 10.1.3.1 255.255.255.0
 peer default ip address pool WOPool
 ppp authentication chap callin
!
```

- **步骤 3.** 如果 PPPoE 会话达到期望的 up 状态，IOS 会创建一个虚拟访问接口。这个动态创建的接口充当 PPPoE 接口。虚拟访问接口保存了大部分第 2 层 PPPoE 操作设置和计数器。
- **步骤 4.** 图中的三个接口是独立的，但它们紧密协作，并且在 PPPoE 的用途上被视为绑定在一起。各种 **show 命令** 可以识别这些绑定。

总结关于这些接口的概念，物理接口发送以太网帧；虚拟访问接口（作为 PPPoE 接口）利用物理接口发送 PPPoE 帧；而拨号器接口（作为第 3 层接口）发送数据包，依靠 PPPoE 接口封装数据包，然后将其发送出物理接口。

记住这些重要概念后，现在来看一些相关的 **show 命令**。本节其余部分假设使用图 15-24 所示的拓扑和示例 15-9 所示的配置。另请注意，图 15-15 重复了示例 15-9 中的配置，但根据 TCP/IP 层组织了命令。接下来的示例列出了 PPPoE 正常工作时获取的 **show 命令** 输出。

## 验证拨号器和虚拟访问接口绑定

对于 PPPoE，**show interfaces dialer** *编号* 命令的输出包含许多有趣的信息。特别是：

- 当 PPPoE 会话存在时，拨号器接口绑定到一个动态创建的虚拟访问接口。因此，**show interfaces dialer** 命令不仅列出一个接口的输出，而是两个接口：一组约 20 行输出用于拨号器接口，另一组用于它所绑定的虚拟访问接口。
- 两部分输出都列出了一些关于绑定到另一个接口的信息（拨号器绑定到虚拟访问，反之亦然）。
- 拨号器接口输出确认了拨号器接口的第 3 层重点（列出 IP 地址），但 PPP 的链路控制协议（LCP）处于关闭状态。
- 虚拟访问接口输出确认了该接口的第 2 层重点，PPP 的 LCP 处于打开状态，但没有 IP 地址。

示例 15-11 显示了从客户路由器 R1 获取的 **show interfaces dialer 2** 命令的输出。突出显示的行将在示例之后讨论。

**示例 15-11** 显示拨号器和虚拟访问接口

```text
R1# show interfaces dialer 2
Dialer2 is up, line protocol is up (spoofing)
  Hardware is Unknown
  Internet address is 10.1.3.2/32
  MTU 1492 bytes, BW 56 Kbit/sec, DLY 20000 usec,
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation PPP, LCP Closed, loopback not set
  Keepalive set (10 sec)
```
