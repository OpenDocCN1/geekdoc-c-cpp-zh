
- 源和目标协议端口（例如 Telnet 或 SNMP）
- ICMP 类型（例如 echo、echo-reply 或 host-unreachable）
- 现有服务对象组

| Command | Description |
| --- | --- |
| `Router(config)#object-group service svr_grp_id` | 创建服务对象组。 |
| `Router(config-service-group)#description description-text` | 在服务对象配置模式下，定义服务对象的具体信息。 |
| `Router(config-service-group)#protocol {protocol-number \| protocol} {tcp \| udp \| tcp-udp {source {{eq \| lt \| gt} port \| range port1 port2}} \| {{eq \| lt \| gt} port \| range port1 port2}} \| icmp icmp-type` | **注意：** 选项是可选的。 |

以下是 `object-group service` 选项的命令语法分解：

| Command | Description |
| --- | --- |
| `Router(config-network-group)# description description-text` | 添加最多 200 个字符的描述。 |
| `Router(config-service-group)#protocol {protocol-number \| protocol}` | 标识 IP 协议编号或名称。 |
| `Router(config-service-group)#tcp \| udp \| tcp-udp {source {{eq \| lt \| gt} port \| range port1 port2}} \| {{eq \| lt \| gt} port \| range port1 port2}}` | 指定 TCP、UDP 或两者的参数。 |
| `Router(config-service-group)#icmp icmp-type` | 指定 ICMP 类型的十进制编号或名称。 |
| `Router(config-service-group)#group-object nested-object-group-name` | 指定要包含在当前（父）对象组中的嵌套（子）对象组。 |

**提示：** 要获取配置选项帮助，请使用问号（?）字符。

**注意：** 标准 ACL 中不支持对象组，也不支持与 IPsec 一起使用，但可在扩展 ACL 中用于服务质量（QoS）匹配条件、Cisco IOS 防火墙功能、动态主机配置协议（DHCP）、组播流量以及许多其他使用扩展 ACL 的功能。

**注意：** 不能删除正在 ACL 中使用的对象组。

### 在扩展 ACL 中使用对象组

对象组可用于大多数扩展 ACL 操作。在 IPv4 ACL 上，通过包含 `object-group` 命令并在其后跟上相应对象组名称来应用对象组：

| Command | Description |
| --- | --- |
| `R1(config)#object-group service SERVER-APPS` | 创建一个名为 SERVER-APPS 的服务对象组。 |
| `R1(config-service-group)#tcp www` | 指定 HTTP 流量。 |
| `R1(config-service-group)#tcp smtp` | 指定电子邮件流量。 |
| `R1(config-service-group)#exit` | 返回全局配置模式。 |

创建一个扩展 ACL，将所有已定义对象合并到一个 ACE 中：

| Command | Description |
| --- | --- |
| `R1(config)#ip access-list extended ACL-IN` | 定义名为 ACL-IN 的扩展 ACL。 |
| `R1(config-ext-nacl)#permit object-group SERVER-APPS object-group OUTSIDE-HOSTS object-group SERVERS` | 允许从外部主机到内部服务器的 HTTP 和 SMTP 流量。 |
| `R1(config-ext-nacl)#exit` | 返回全局配置模式。 |

将扩展 ACL 应用到外部接口：

| Command | Description |
| --- | --- |
| `R1(config)#interface serial 0/0` | 进入串行接口的接口配置模式。 |
| `R1(config-if)#ip access-group ACL-IN in` | 在外部接口上应用入站 ACL。 |

> **注意：** 要验证对象组，请使用 `show ip access-list` 或 `show object-group` 命令。

## 使用 CCP 在 ACL 中配置对象组示例

要在 ACL 规则中使用对象组，首先创建一个网络对象组或服务对象组。

要配置网络组对象，请选择 **配置 > 路由器 > ACL > 对象组 > 网络对象组**。

这将打开如图 11-6 所示的“网络对象组”界面。

![](img/0d9540c65a85f4cb1c32cee46038d8ab_164_0.png)

**图 11-6** 网络对象组摘要界面

在此界面中，可以创建、编辑或删除网络对象组。

要添加新的网络对象，请单击 **创建**。

这将打开如图 11-7 所示的“创建网络对象组”窗口。在此窗口中，指定网络对象组名称、描述，并添加网络对象成员。

**提示：** 使用“成员类型”下拉框显示对象的标识方式。

完成后，单击 **确定**。

![](img/0d9540c65a85f4cb1c32cee46038d8ab_167_0.png)

**图 11-11** 添加规则对话框

单击 **添加** 打开“添加扩展规则条目”窗口，将 **OUTSIDE-HOSTS** 网络对象组标识为源，将 **SERVER** 网络对象组标识为目标，并为协议和服务选择 **SERVER-APPS** 服务对象组。

单击 **确定** 返回“添加规则”对话框，然后单击 **关联** 打开“与接口关联”窗口。选择外部串行接口并单击 **确定**。查看规则，完成后单击 **确定**。

CCP 显示 CLI 配置命令。单击 **下发** 以提交配置更改。

修改后的“访问规则”信息界面会显示新创建的规则，如图 11-12 所示。

![](img/0d9540c65a85f4cb1c32cee46038d8ab_167_1.png)

**图 11-12** 修改后的访问规则界面

## IPv6 中的 ACL

IPv6 中的数据包过滤与 IPv4 中的数据包过滤类似。防止两种协议栈之间常见攻击（例如侦察和欺骗攻击）的策略通常从尝试匹配恶意流量的 ACL 开始。

### 使用 ACL 缓解 IPv6 攻击

IPv6 ACL 可以帮助缓解以下威胁（以及其他威胁）：

- 报头扩展威胁，例如基于路由报头（RH）的放大攻击
- 基于 ICMPv6 误用和滥用的威胁
- 基于组播 IPv6 地址的侦察
- 利用隧道解决方案的威胁，例如 IPv6 迁移环境中使用的隧道解决方案

**注意：** 某些威胁需要使用两种协议栈的组合方法，特别是那些利用双栈环境的威胁。

### IPv6 ACL 的隐式条目

每个 IPv6 ACL 都会隐式追加三行：两个允许条目用于启用 IPv6 邻居发现（ND），以及实现默认拒绝策略的传统规则：

```text
permit icmp any any nd-na
permit icmp any any nd-ns
deny ipv6 any any
```

**警告：** 可能希望通过显式配置 `deny ipv6 any any log` ACE 来记录所有被隐式拒绝的数据包。一个常见错误是忘记两个隐式 ND ACE，从而导致 ND 问题。解决方案是按正确顺序在 ACL 末尾显式添加所有三个隐式行。

### 使用 IPv6 ACL 进行过滤

| Command | Description |
| --- | --- |
| `Router(config)#ipv6 access-list access-list-name` | 定义 IPv6 ACL，并进入 IPv6 访问列表配置模式。IPv6 ACL 名称不能包含空格或引号，也不能以数字开头。 |
| `Router(config-ipv6-acl)#permit protocol {source-ipv6-prefix /nn \| any \| host source-ipv6-address \| auth} {operator [port-number]} {destination-ipv6-prefix /nn \| any \| host destination-ipv6-address \| auth} {operator [port-number]} {dest-option-type {doh-number \| doh-type}} [dscp value] {flow-label value} [fragments] [log] [log-input] [mobility] [mobility-type [mh-number \| mh-type]] [reflect name [timeout value]] [routing] {routing-type [routing-number]} {sequence value} [time-range name]` | 指定 IPv6 ACL 的允许条件。 |
| `Router(config-ipv6-acl)#deny protocol {source-ipv6-prefix /nn \| any \| host source-ipv6-address \| auth} {operator [port-number]} {destination-ipv6-prefix /nn \| any \| host destination-ipv6-address \| auth} {operator [port-number]} {dest-option-type {doh-number \| doh-type}} [dscp value] {flow-label value} [fragments] [log] [log-input] [mobility] [mobility-type [mh-number \| mh-type]] [routing] {routing-type [routing-number]} {sequence value} [time-range name] [undetermined-transport]` | 指定 IPv6 ACL 的拒绝条件。 |
| `Router(config)#interface type number` | 指定接口类型和编号，并进入接口配置模式。 |
| `Router(config-if)#ipv6 traffic-filter access-list-name {in \| out}` | 将指定的 IPv6 访问列表应用到接口。 |
| `Router(config)#line vty 0 4` | 进入 line vty 模式。 |
| `Router(config-line)#ipv6 access-class access-list-name {in \| out}` | 应用 IPv6 ACL 以指定谁可以访问 vty 线路。 |

**注意：** 有关 IPv6 ACL 参数的更多信息，请参阅 Cisco.com。

