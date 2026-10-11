
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

### 示例 6-12 配置北美 PSTN 拨计划

```
VOICE_RTR(config) dial-peer 90 pots
VOICE_RTR(config-dial-peer) description Service Dialing
VOICE_RTR(config-dial-peer) destination-pattern [469]11
VOICE_RTR(config-dial-peer) forward-digits 3
VOICE_RTR(config-dial-peer) port 1/0:1
VOICE_RTR(config-dial-peer) exit
VOICE_RTR(config) dial-peer 91 pots
VOICE_RTR(config-dial-peer) description 10-Digit Dialing
VOICE_RTR(config-dial-peer) destination-pattern [2-9]..2-9]......
VOICE_RTR(config-dial-peer) port 1/0:1
VOICE_RTR(config-dial-peer) exit
VOICE_RTR(config) dial-peer 92 pots
VOICE_RTR(config-dial-peer) description 11-Digit Dialing
VOICE_RTR(config-dial-peer) destination-pattern 9[2-9]..2-9]......
VOICE_RTR(config-dial-peer) forward-digits 11
VOICE_RTR(config-dial-peer) port 1/0:1
VOICE_RTR(config-dial-peer) exit
VOICE_RTR(config) dial-peer 93 pots
VOICE_RTR(config-dial-peer) description International Dialing
VOICE_RTR(config-dial-peer) destination-pattern 9011T
VOICE_RTR(config-dial-peer) prefix 011
VOICE_RTR(config-dial-peer) port 1/0:1
VOICE_RTR(config-dial-peer) exit
```

该语法中的两个命令用于处理 POTS 的自动数字剥离功能：`dial forward-digits <numbers>` 和 `prefix <number>`。`forward-digits <number>` 命令允许你指定想要转发的右对齐数字个数。注意示例 6-12 中的第一个拨号 90。对于目标模式为 `[469]11`，路由器在发送通话之前会自动剥离模式中的 9 和两个 2。通过使用 `forward-digits 3` 命令，路由器会转发右对齐的数字（411、611 或 911），并且仅剥离 9。

`prefix <number>` 命令在路由通话之前向拨号的号码添加指定的数字。这对于 示例 6-12 中的 dial peer 93 很有用。因为国际号码的长度可能是可变的，因此无法确定 `forward-digits` 命令应该输入什么值。通过使用 `prefix 011` 命令，利用 POTS 的自动数字剥离功能，dial peers 会从模式中剥离显式定义的 9011 数字，然后前缀会在原位置加回 011。

## 私有线自动振铃 (PLAR)

尽管与 dial peer 配置没有直接直接关系，但私有线自动振铃（PLAR）极度依赖现有的 dial peers 来连接通话。配置了 PLAR 能力的端口一旦检测到摘机信号（off-hook signal），就会自动拨打号码。PLAR 配置最明显的用途是电梯或停车场等地点的紧急电话。示例 6-13 显示了 x1101（如图 6-8 所示）作为一个 PLAR 扩展分，只要用户一拿起听筒，它就会立即拨打 x1102。

| | |

|---|---|

| FXS 0/0/0 | x1101 |

| FXS 0/0/1 | CME_A (x1102) |

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_158_0.png)

### 图 6-8 PLAR 配置

### 示例 6-13 FXS PLAR 配置

```
CME_A(config)# voice-port 0/0/0
CME_A(config-voiceport)# connection ?nplar  Private Line Auto Rewinding
tie-line A tie line
trunk      A Straight Tie Line
CME_A(config-voiceport)# connection plar ?nWORD A string of digits including wild cards
tied dedicated tie to this number
CME_A(config-voiceport)# connection plar 1102
```

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_158_1.png)

FXS 语音端口 0/0/0 现在被硬编码为在用户拿起听筒后立即拨打号码 1102。

PLAR 在各种情况下也很有用。一种常见场景是如图 6-9 所示的 FXO 连接。

| | |

|---|---|

| 接线员 | 1500 |

| FXO 2/0/0 | CME_A |

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_158_2.png)

### 图 6-9 FXO 连接

## 路由器数字处理

数字间隔超时时间。你也可以通过一些高级的数字处理技术来实现这一目标，你将在后续章节中学习这些技术。

### 匹配入站和出站拨号对 (Dial Peers)

当路由器接收到语音电话时，它必须以某种方式匹配拨号对（dial peer），路由器才能处理该通话。虽然这听起来像是一个简单的陈述，但实际上要在入站和出站方向实现这一目标，需要制定大量的策略。以图 6-10 所示场景为例，它扩展了本节关于拨号对的呼叫路段场景。

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_161_0.png)

图 6-10 入站和出站拨号对

除了呼叫路段，图 6-10 还展示了拨号对配置，用于完成从 x1101 到 x2510 及其反的端到端通话。现在，匹配出站拨号对很容易：获取拨号数字，并将其与你在路由器上配置的拨号对下的目标模式进行比较，以找到最具体的匹配。例如，如果 x1101 拨打 x2510，路由器会查找其拨号对并发现有一个 VoIP 拨号对直接将通话匹配到 IP 地址 10.1.1.2。当 ROUTER B 接收到同时，它意识到拨号数字匹配 POTS 拨号对 2510，这导致路由器调用 T1 接口以访问 PBX 系统。这一过程解释了路由器如何匹配出站拨号对（在图 6-10 中显示为呼叫路段 2 和呼叫路段 4），但路由器是如何匹配入站拨号对的？路由器通过以下方法匹配入站拨号对：

- 1. 使用 `call-number` 拨号对配置命令匹配拨号号码 (DNIS)。

- 2. 使用 `answer-address` 拨号对配置命令匹配主叫 ID (ANI)。
