

## 密码套件选项

下表比较了较弱的选项和较强的选项：

| 参数 | 最弱 | 最强 |
|---|---|---|
| 加密算法 | 数据加密标准（DES） | 高级加密标准（AES） |
| 哈希算法 | 消息摘要算法5（MD5） | 安全哈希算法2（SHA-2） |
| 认证方法 | 预共享密钥（PSK） | Rivest、Shamir、Adleman（RSA）签名 |
| 密钥交换 | Diffie-Hellman（DH）组1 | DH 组5 |
| IKE SA 生命周期 | 86,400 秒 | < 86,400 秒 |

## 配置 IOS 站点到站点 VPN

要使用 IOS 命令行界面（CLI）配置站点到站点 VPN，请完成以下步骤：

1. 创建 IKE 策略并配置所需的第 1 阶段参数。
2. 指定 PSK 并标识对等体地址（或主机名）。
3. 创建第 2 阶段所需的 IPsec 策略。
4. 创建加密映射并配置加密映射的具体信息。
5. 使用扩展 ACL 标识感兴趣流量。
6. 将加密映射应用到接口。
7. 验证隧道。

> **注意：** 其中一些步骤可以按不同顺序完成。

创建 IKE 策略。

```
Router(config)#crypto isakmp policy priority

定义 IKE 策略，以指定在 IKE 协商期间用于创建 IKE SA 的参数。

*priority* 唯一标识 IKE 策略并为该策略分配优先级。使用 1 到 10,000 之间的整数，其中 1 为最高优先级，10,000 为最低优先级。
```

> **注意：** 您可以配置多个 IKE 策略。当 IKE 协商开始时，它会尝试在两端对等体上找到共同的策略，从远程对等体上指定的最高优先级策略开始。

> **注意：** 使用 `show crypto isakmp policy` 命令验证 IKE 设置。

可配置的 IKE 参数包括以下内容：

- 认证（默认 = RSA 签名）
- 加密（默认 = 56 位 DES）
- 哈希（默认 = SHA-1）
- DH 组（默认 = 768 位 DH）
- IKE SA 生命周期（默认 = 86400 秒 [1 天]）

配置 IKE 策略第 1 阶段参数：

| 命令 | 描述 |
|---|---|
| `Router(config-isakmp)# authentication {pre-share \| rsa-encr \| rsa-sig}` | 设置 IKE 策略的认证方法。 |
| `Router(config-isakmp)#encryption {des \| 3des \| aes \| aes-bit}` | 设置 IKE 策略的加密算法。<br>**注意：** 加密选项可能因 IOS 映像而异。 |
| `Router(config-isakmp)#hash {md5 \| sha}` | 设置 IKE 策略的哈希算法。 |
| `Router(config-isakmp)#group {1 \| 2 \| 5}` | 设置用于 IKE 策略的 DH 组。 |
| `Router(config-isakmp)#lifetime seconds` | 配置 IKE SA 在过期之前可以存在的最大时间。时间值范围为 60 到 86400 秒（1 分钟到 24 小时）。 |

> **注意：** 如果未配置某个参数，则将使用该参数的默认值。

> **注意：** 对转换集的更改不会应用到现有 SA，而是在后续协商中用于建立新的 SA。要更快地强制应用设置，请使用 `clear crypto sa` 命令清除全部或部分 SA 数据库。

> **注意：** 使用 `show crypto ipsec transform-set` 命令验证 IPsec 设置。

创建加密映射的具体信息：

| 命令 | 描述 |
|---|---|
| `Router(config)#crypto map map-name sequence-number ipsec-isakmp` | 定义站点到站点 IPsec VPN 加密映射设置。 |

> **注意：** 还有其他选项可用，但本章的重点是 IPsec 和 ISAKMP 加密映射定义。

可配置的站点到站点 VPN 加密映射参数包括以下内容：

- 标识远程对等体。
- 标识要使用的转换集。
- 标识感兴趣流量。

> **注意：** 可以配置其他选项，但这些是站点到站点 VPN 的典型选项。

配置加密映射的具体信息：

| 命令 | 描述 |
|---|---|
| `Router(config-crypto-map)# description description` | 向加密映射添加描述。 |
| `Router(config-crypto-map)#set peer peer-ip` | 指定 IPsec 对等体。**注意：** 您可以使用多个单独的命令标识多个对等体。 |
| `Router(config-crypto-map)#set transform-set transform-name1 [transform-name2 ... transform-name6]` | 指定哪些转换集可用于该加密映射条目。**注意：** 您可以在一条命令中最多指定六个转换集。 |
| `Router(config-crypto-map)#match address crypto-acl` | 将扩展访问列表分配给加密映射条目，IPsec 将使用该列表来确定哪些流量应受加密保护，哪些流量不需要加密保护。**注意：** 访问列表允许的流量将受到保护。访问列表拒绝的流量在相应加密映射条目的上下文中将不受保护。 |

使用扩展访问控制列表（ACL）标识感兴趣流量。ACL 标识源流量何时到达目标网络时应启用 VPN 隧道。扩展 ACL 可以是编号的或命名的。

> **注意：** 对等体之间的扩展 ACL 应该是互逆的（例如，在对等体 A 上，源 A 到目标 B；在对等体 B 上，源 B 到目标 A）。

将加密映射应用到接口：

| 命令 | 描述 |
|---|---|
| `Router(config)#interface type number` | 指定接口类型和编号。 |
| `Router(config-if)#crypto map crypto-map-name` | 将先前定义的加密映射集应用到接口。 |

## 验证 VPN 隧道

要验证站点到站点 VPN 配置，请使用以下命令。

要验证 IKE 第 1 阶段状态，请使用以下命令：

| 命令 | 描述 |
|---|---|
| `Router#show crypto isakmp policy` | 显示已配置的 IKE 策略。 |
| `Router#show crypto isakmp sa (active)` | 显示 IKE 第 1 阶段 SA 的状态。 |

> **注意：** `show crypto isakmp sa` 命令显示第 1 阶段的状态和状况。对于已建立的第 1 阶段隧道，状态 QM_IDLE 被视为正常。

要验证 IKE 第 2 阶段状态，请使用以下命令：

| 命令 | 描述 |
|---|---|
| `Router#show crypto ipsec transform-set` | 显示已配置的 IPsec 转换集。 |
| `Router#show crypto map` | 显示已配置的加密映射。 |
| `Router#show crypto ipsec sa` | 显示已建立的 IPsec 隧道。 |

要测试隧道，请完成以下步骤：

1. 使用 `clear crypto sa` 命令清除 IPsec SA。
2. 发出 `show crypto ipsec sa` 命令以验证计数器已清除。
3. 使用扩展 ping 创建感兴趣流量，例如 `ping destination-network-ip source source-network-ip`。
4. 发出 `show crypto ipsec sa` 命令以验证计数器已增加。

## 使用 IOS 配置站点到站点 IPsec VPN 示例

此示例在 R1 和 R3 之间建立站点到站点 VPN，保护两个 LAN 网段之间传输的流量。需要使用强密码套件，使用 PSK、AES 128 位和 SHA。

![](img/0d9540c65a85f4cb1c32cee46038d8ab_249_0.png)

图 17-1  站点到站点 IPsec VPN 示例的网络拓扑

创建 IKE 策略 1 并配置所需的第 1 阶段参数：

| 命令 | 描述 |
|---|---|
| `R1(config)#crypto isakmp policy 1` | 定义 IKE 策略设置。 |
| `R1(config-isakmp)#authentication pre-share` | 设置 IKE 策略的认证方法。 |
| `R1(config-isakmp)#encr aes 128` | 设置 IKE 策略的加密算法。 |
| `R1(config-isakmp)#hash sha` | 设置 IKE 策略的哈希算法。 |
| `R1(config-isakmp)#group 5` | 设置用于 IKE 策略的 DH 组。 |
| `R1(config-isakmp)#lifetime 86400` | 将 IKE SA 过期计时器设置为 24 小时。 |
| `R1(config-isakmp)#exit` | 返回到全局配置模式。 |

指定 PSK 并标识对等体地址（或主机名）：

```
R1(config)#crypto isakmp key cisco123 address 209.165.202.129    为 R3 对等体设置 PSK。
```

