
2. CME 在准备好接受 IP 注册之前需要的最少电话服务命令集是什么？（选择三个。）

- a. ip source-address
- b. no shutdown
- c. ephone
- d. ephone-dn
- e. max-ephones
- f. max-ephone-dn
- g. max-dn

3. 在全局配置模式下输入命令 `ephone-dn 2` 创建的是什么类型的 ephone-dn？

- a. 单线 (Single line)
- b. 双线 (Dual line)
- c. 四线 (Quad line)
- d. 八线 (Octo line)

4. 让 ephone-dn 能够响应四位分机号和十位 DID 码的最简单方法是什么？

- a. 创建分配给 dial-peer 的入站翻译模式（incoming translation patterns）。
- b. 使用分区（partitions）和路由搜索空间（calling search spaces）。
- c. 使用“number”命令分配辅助号码。
- d. 分配主叫转换掩码（calling party transformation mask）。

5. 你想将目录号 1000 (ephone-dn 5) 分配到 Cisco 7961 IP Phone (ephone 12) 的第三线按钮上。什么语法可以完成此任务？

- a. button 3:1000
- b. button 12:3:1000
- c. button 5:3:12
- d. button 3:5

6. 你想验证 CME 支持的 IP 的线路分配和注册状态。以下哪个显示提供了提供了信息？

- a. show run
- b. show ephone
- c. show voip ephone registration
- d. show voip registration

7. 在 CCP 允许你配置任何电话或分机之前，必须配置哪个组件？

- a. 动态路由协议
- b. 指向 CME 系统的静态路由
- c. 电话服务 (Telephony service)
- d. Unity express 语音信箱

8. 当你在路由器上配置更改时，CCP 会自动将更改保存到 flash。

- a. 正确 (True)
- b. 错误 (False)

9. 使用 CCP 添加用户账户时，以下哪个是必填字段？

- a. UserID
- b. 名 (First Name)
- c. 姓 (Last Name)
- d. 密码 (Password)

10. CCP 如何将电话和分机连接在一起？

- a. 通过导航到电话配置页，可以将分机分配给电话。
- b. 通过创建用户账户，可以将用户账户、电话和分机连接在一起。
- c. 你可以从分机配置页将分机分配给电话。
- d. 你必须使用命令行 ephone/ephone-dn 语法将电话和分机连接在一起。

# 基础主题

# 确保基础

第 3 章“理解 Cisco IP Phone 概念与注册”和第 4 章“熟悉 CME 管理”为运行中的 CME 系统奠定了关键的配置。在跳到 IP 电话的配置之前，对这些概念进行高层次回顾是明智的。

到为止讨论的所有概念几乎都关注 Cisco IP Phone 的启动过程。以下列表列出了 Cisco IP Phone 的启动过程，如图 5-1 所示：

- 1. 802.3af PoE 交换机在以太网线上传发送微小的直流电压，检测到未供电的 802.3af 设备，并为线路供电。
- 2. 交换机使用 Cisco 发现协议 (CDP) 向 Cisco IP Phone 发送语音 VLAN 信息。
- 3. IP 电话在它的语音 VLAN 上发送动态主机配置协议 (DHCP) 请求。DHCP 服务器回复 IP 地址信息，包括 DHCP  150，该选项将 IP 电话引向 TFTP 服务器。
- 4. IP 电话连接 TFTP 服务器并下载其配置文件和固件。
- 5. 根据配置文件列出的 IP 地址，IP 电话联系呼处理服务器（在此例中为 CME 路由器），该服务器支持 VoIP 功能。

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_113_0.png)

图 5-1 Cisco IP Phone 启动过程

**注意：** 图 5-1 将 DHCP 服务器、TFTP 服务器和 CME 路由器显示为三个独立的设备。为了节省资源，较小的网络通常会将这三个功能合并到一个设备中。在这种情况下，CME 路由器同时也充当网络的 DHCP 和 TFTP 服务器。

为了满足此启动过程的需求，我们在前两个章节的基础上增加了以下配置：

- 语音 VLAN
- DHCP 服务
- TFTP 服务

### 语音 VLAN

为了分离语音和数据流量，你必须为每个连接到 Cisco IP Phone 的端口配置语音 VLAN。在示例 5-1 中，语音 VLAN 为 100，数据 VLAN（用于连接到 IP 电话的 PC 设备）为 200。

### 示例 5-1 配置语音 VLAN

```
Switch#configure terminal
Switch(config)#interface fa0/1
Switch(config-if)#switchport mode access
Switch(config-if)#switchport vlan 100
Switch(config-if)#switchport access vlan 200
Switch(config-if)#spanning-tree portfast
```

### DHCP 服务

IP 电话接收其语音 VLAN 信息后，开始发送 DHCP 请求。示例 5-2 中的配置使 Cisco 路由器成为 DHCP 服务器。

### 示例 5-2 配置 DHCP 范围

```
ROUTER(config)#ip pool VOICE_SCOPE
ROUTER(config-pool)#network 192.168.1.0 255.255.255.0
ROUTER(config-pool)#default-router 192.168.1.1
ROUTER(config-pool)#dns-server 8.8.8.8
ROUTER(config-pool)#option 150 192.168.1.10
```

### TFTP 服务

IP 电话接收其语音 VLAN 信息后，开始发送 DHCP 请求。在 IP 电话的启动过程中，IP 电话连接 TFTP 服务器下载其固件。在此之前，你可能会想：“这个 TFTP 服务器在哪里？那个配置文件里有什么？”我很高兴你问这个问题。TFTP 服务器一如既往：简单的文件存储器，根据需要为未身份验证的客户端提供文件。虽然 Cisco 路由器具有在任何设备上作为 TFTP 服务器的能力，但通常由 Cisco 路由器（在 CME 中）或 CUCM 发布服务器处理 TFTP 服务器的角色。

除了交付 DHCP 标准信息（IP 地址、子网掩码、默认网关和 DNS）外，DHCP 服务器还交付电话选项 150，这为 IP 电话提供了 TFTP 服务器的 IP 地址。

如果你没有输入任何单独电话配置，发送到 IP 电话的唯一配置文件是 XMLDefault.cnf 文件。该文件包含连接到呼处理服务器（在本例中为 CME 路由器）的 IP 地址和端口号，以及 IP 电话应该使用的固件文件名。IP 电话获得配置文件后，它会下载必要的固件并联系 CME 路由器应用固件镜像。

> 注意：在 CME 4.0 及以后，可以在电话服务配置模式下使用命令 c-file location http://<TFTP 服务器 IP 地址> 将配置和固件存储在外部 TFTP 服务器上。这可以节省路由器上宝贵的 flash 空间。

为了将路由器的 flash 作为 TFTP 服务器，你必须使文件单独可用供 IP 电话下载。示例 5-3 说明了针对 7940/7960 IP 电话固件文件的此过程。
