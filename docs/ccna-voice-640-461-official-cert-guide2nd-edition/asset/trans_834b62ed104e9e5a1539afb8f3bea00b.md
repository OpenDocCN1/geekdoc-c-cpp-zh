

# CCNA Voice 640-461 官方认证指南

destination-pattern 9...... 命令（用于七位拨号），路由器在将通话发送到 PSTN 之前会自动剥离显式定义的数字 9。

在示例 6-10 中，在将通话发送到 PBX 系统之前剥离数字 2 并不是预期的行为。因此，`no digit-strip` 命令可以防止这种自动数字剥离过程。

**注意：**自动数字剥离功能适用于 POTS 拨号（dial peers）。VoIP 拨号（在后续节中讨论）不会自动剥离数字。

## 配置 VoIP 拨号

如图 6-7 所示的场景中，POTS 拨号为旧留语音设备提供连接。然而，CME_A 和 ROUTER_B 被一个 IP WAN 连接隔开，旧留语音设备必须跨越该连接来实现端到端通信。

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_153_0.png)

**图 6-7** 拨号配置场景

为了实现这种连接，你必须使用 VoIP 拨号，因为通话正在跨基于 IP 网络。示例 6-11 在 CME_A 和 ROUTER_B 设备上配置了必要的 VoIP 拨号。

## 示例 6-11 配置 VoIP 拨号

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
| g729r8 | G729 8000 bps |
| ilbc | ilBC 13330 or 15200 bps |

```
CME_A(config-dial-peer)# codec g711ulaw

ROUTER_B(config-dial-peer)# destination-pattern 110.
ROUTER_B(config-dial-peer)# session target ipv4:10.1.1.1
ROUTER_B(config-dial-peer)# codec g711ulaw
```

POTS 和 VoIP 拨号配置的主要区别在于使用了 `session target` 命令而不是 `port` 命令。当你使用 `session target` 命令后使用上下文敏感帮助时，路由器简单地回复 `WORD`。这意味着你在命令后输入的任何内容都是自由格式的。你使用 `ipv4:sip address>` 语法来输入远程 IP 地址，如示例 6-11 所示。该命令还允许你将通话定向到 DNS 名称（使用 `dns<name>` 语法）或各种通话管理服务器，例如 H.323 网关或会话启动协议（SIP）代理服务器。

在设置 `session target` 后，你可以可选地使用 `codec destination` 来选择路由器在向此目的地拨号时应使用的编码器。

> 注意：如果两个路由器之间的编码器值不匹配，通话将失败并返回重拨音（快速忙音信号）。这通常被称为编码器不匹配（codec mismatch）。VoIP 拨号的默认编码器值为 G.729。

最后，注意 ROUTER_B 上的拨号 1100 使用 `destination-pattern 110` 命令，将所有以数字 110 开头的通话重定向到 CME 路由器。如果没有这个通配符，你需要在 ROUTER_B 上创建两个拨号：一个用于 110。

## 通配符 (Wildcards)

正如你在上一节中看到的，通配符 `.` 匹配单个数字。

| 通配符 | 描述 |
| :--- | :--- |
| . | 匹配单个数字 |
| * | 匹配零个或多个任意字符 |
| ? | 匹配单个任意字符的字符 |
| [set] | 匹配集合中的任意一个字符 |
| [range] | 匹配范围内的任意一个字符 |
| [^set] | 匹配不在集合中的任意一个字符 |
| [set]* | 匹配集合后跟多个任意字符 |
| [set]? | 匹配集合后的单个任意字符 |
| [set]. | 匹配集合后的单个数字 |
| [set1][set2] | 匹配两个集合中的任意一个字符 |
| [set1]* | 匹配第一个集合，后跟多个任意字符 |
| [set1]? | 匹配第一个集合，后跟单个任意字符 |
| [set1]. | 匹配第一个集合，后跟单个数字 |
| [set1][set2]* | 匹配两个集合，后跟多个任意字符 |
| [set1][set2]? | 匹配两个集合，后跟单个任意字符 |
| [set1][set2]. | 匹配两个集合，后跟单个数字 |
| [set1][set2][set3]* | 匹配三个集合，后跟多个任意字符 |
| [set1][set2][set3]? | 匹配三个集合，后跟单个任意字符 |
| [set1][set2][set3]. | 匹配三个集合，后跟单个数字 |
| [set1][set2][set3][set4]* | 匹配四个集合，后跟多个任意字符 |
| [set1][set2][set3][set4]? | 匹配四个集合，后跟单个任意字符 |
| [set1][set2][set3][set4]. | 匹配四个集合，后跟单个数字 |
| [set1][set2][set3][set4][set5]* | 匹配五个集合，后跟多个任意字符 |
| [set1][set2][set3][set4][set5]? | 匹配五个集合，后跟单个任意字符 |
| [set1][set2][set3][set4][set5]. | 匹配五个集合，后跟单个数字 |
| [set1][set2][set3][set4][set5][set6]* | 匹配六个集合，后跟多个任意字符 |
| [set1][set2][set3][set4][set5][set6]? | 匹配六个集合，后跟单个任意字符 |
| [set1][set2][set3][set4][set5][set6]. | 匹配六个集合，后跟单个数字 |
| [set1][set2][set3][set4][set5][set6][set7]* | 匹配七个集合，后跟多个任意字符 |
| [set1][set2][set3][set4][set5][set6][set7]? | 匹配七个集合，后跟单个任意字符 |
| [set1][set2][set3][set4][set5][set6][set7]. | 匹配七个集合，后跟单个数字 |
| [set1][set2][set3][set4][set5][set6][set7][set8]* | 匹配八个集合，后跟多个任意字符 |
| [set1][set2][set3][set4][set5][set6][set7][set8]? | 匹配八个集合，后跟单个任意字符 |
| [set1][set2][set3][set4][set5][set6][set7][set8]. | 匹配八个集合，后跟单个数字 |
| [set1][set2][set3][set4][set5][set6][set7][set8][set9]* | 匹配九个集合，后跟多个任意字符 |
| [set1][set2][set3][set4][set5][set6][set7][set8][set9]? | 匹配九个集合，后跟单个任意字符 |
| [set1][set2][set3][set4][set5][set6][set7][set8][set9]. | 匹配九个集合，后跟单个数字 |

这些通配符通常用于创建 PSTN 的拨号计划。最初，对于 PSTN 最符合逻辑的选择似乎是 9T（外线后跟跟任意数字）。问题在于 Cisco 设计 T 通配符是为了匹配 0-32 位的字符串。当用户拨打外部号码，例如 1408551212 时，配置了 T 通配符的路由器将静止并等待输入更多数字。默认情况下，路由器会等待 10 秒，这就是数字计时（interdigit timer）。虽然你可以通过按下井键 (#) 强制路由器立即处理通话，但这并不是你希望让所有用户学习的。使用非 T 通配符创建 PSTN 拨号计划并不困难，只要你考虑可访问的 PSTN 号码。表 6-5 提供了一个你可以使用的示例 PSTN 拨号计划。

| 模式 | 描述 |
| :--- | :--- |
| [2-9]...... | 用于七位拨号区 |
| [2-9].[2-9]...... | 用于 10 位拨号区 |
| 1[2-9].[2-9]...... | 用于 11 位长途拨号 |
| [469]11 | 用于服务热线，例如 411、611 和 911 |
| 011T | 用于国际拨号 |

注意：虽然你可以手动创建不使用 T 符号的国际拨号计划，但这可能变得非常繁琐。示例 6-12 展示了在路由器上配置北美 PSTN 拨号计划。在此示例中，T1 CAS 端口 1/0:1 连接到 PSTN，内部用户必须拨打 9 以访问外部 PSTN。

