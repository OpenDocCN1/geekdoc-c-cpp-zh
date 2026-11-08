
## 642-436：配置 IP-to-IP 网关以提供呼叫准入控制

- CAC 可以作为本地、基于测量或基于资源的技术来实现。
- 使用本地 CAC 时，网关会评估所有连接，以确定它是否能处理另一个连接。
- 使用基于测量的 CAC 时，数据包会被发送到 WAN 上，目的是测量连接。测量连接后，可以相应地配置 CAC。
- 使用基于资源的 CAC 时，你利用网守来确保管理呼叫限制，从而整体提供 QoS。RSVP 用于基于资源的 CAC。
- max-conn 命令用于 dial-peer 配置模式中，以限制给定 WAN 链路上允许的连接数。

## 642-436：验证 IP-to-IP 网关实施

- show call active voice 和 show call history voice 命令用于查看当前和过去的 VoIP 呼叫信息。
- show dial-peer voice 命令将用于验证编解码器透明性或媒体流（flow-through 和 flow-around）的正确配置。
- debug cch323 all 和 debug ccsip all 命令分别用于查看有关 H.323 和 SIP 进程的详细信息。
- debug voip ipipgw 命令用于查看有关入站和出站呼叫腿处理的信息。

## 自测

以下问题将帮助你衡量对本章所呈现材料的理解。请仔细阅读所有选项，因为可能有多个正确答案。请为每个问题选择所有正确答案。

### 642-436：描述 IP-to-IP 网关的特性和功能

- 1. Cisco UBE 网关的主要目的是什么？
  - A. 连接两个不同的物理层网络
  - B. 在以太网和令牌环网络之间提供桥接
  - C. 连接两个不同的 VoIP 网络
  - D. 连接两个不同的目录服务网络

- 2. 为了将 Cisco ISR 实现为 UBE 网关，必须在其上安装什么？
  - A. 正确的 IOS 版本和特性集
  - B. IPIPGW 软件模块
  - C. IPIPGW 接口模块
  - D. SDM

- 3. UBE 网关支持以下哪些 DTMF 信令方法？（选择所有适用项。）
  - A. SS7
  - B. H.245
  - C. SIP Notify
  - D. KPML

- 4. Cisco UBE 上的 QoS 支持哪两种方法？
  - A. IP 优先级
  - B. DSCP 标记
  - C. TCC 标记
  - D. 六西格玛

### 642-436：配置网守以支持 IP-to-IP 网关

- 5. 为了使网守能够使用 Cisco UBE，必须配置和实现什么？
  - A. 正确的 sRTP 参数
  - B. 正确的 cRTP 参数
  - C. IPX 接口
  - D. via-zones

### 642-436：配置 IP-to-IP 网关以提供地址隐藏

- 6. 在 Cisco UBE 网关上，使用什么命令来隐藏 IP 地址？
  - A. address-hiding
  - B. address hiding
  - C. hide ip
  - D. hide-ip

- 7. 使用 Cisco UBE 网关时，IP 地址隐藏有什么好处？
  - A. 更难以入侵网络。
  - B. 更容易监控网络流量。
  - C. 确保 UBE 是唯一的信令和媒体入口点。
  - D. 确保 CME 是唯一的信令和媒体入口点。

### 642-436：配置 IP-to-IP 网关以提供协议和媒体互通

- 8. 在 Cisco UBE 网关上，使用什么命令来实现 SIP-to-SIP？
  - A. allowed-connections sip
  - B. allowed-connections sip to sip
  - C. allowed-connections sip-to-sip
  - D. allowed-connections sip only

- 9. 你希望 RTP 媒体从一部电话经过 UBE 传到另一部电话，而不进行终止和重新发起。在 dial-peer 配置模式下应输入什么命令？
  - A. media flow-through
  - B. media passthrough
  - C. media flow-around
  - D. RTP passthrough

### 642-436：配置 IP-to-IP 网关以提供呼叫准入控制

- 10. 在 dial-peer 配置模式下，使用什么命令来限制可同时通过该拨号对等体的连接数？
  - A. limit-conn
  - B. max-conn
  - C. upper-conn
  - D. conn-limit

- 11. 哪种 CAC 会向 WAN 发送数据包以确定 WAN 链路的质量，并据此实施 CAC？
  - A. 本地 CAC
  - B. 基于测量的 CAC
  - C. 基于资源的 CAC
  - D. 网守 CAC

- 12. 使用基于资源的 CAC 必须配置哪两个组件？
  - A. H.323 网守
  - B. SIP 代理
  - C. RSVP
  - D. DiffServ

### 642-436：验证 IP-to-IP 网关实施

- 13. 使用什么命令查看网关上的拨号对等体？
  - A. show dial-peer voice
  - B. show running-config
  - C. show active voice
  - D. show call history voice

- 14. 使用什么命令查看网关上的当前语音连接？
  - A. show call active voice
  - B. show call history voice
  - C. show dial-peer voice
  - D. show interfaces

- 15. 什么调试命令会显示 SIP 事件和错误？
  - A. debug voip ipgw
  - B. debug h323 all
  - C. debug ccsip all
  - D. debug sip all

## 实验题

你想在 Cisco 2801 ISR 上验证 Cisco UBE 的正确配置。你特别希望看到以下信息：

- 允许连接的 H.323-to-SIP 网关设置
- 当前语音连接
- SIP 和 H.323 的错误信息
- 呼叫的媒体流配置

对于每组信息，你将执行什么命令？

## 自测答案

### 642-436：描述 IP-to-IP 网关的特性和功能

- 1. ☑ C 正确。UBE 网关的主要目的是连接两个不同的 VoIP 网络，这些网络可能使用相同或不同的信令协议。
  
  ☒ A、B 和 D 不正确。虽然网关可用于连接任何其他三类网络或服务，但 Cisco UBE 网关不用于这些目的。

- 2. ☑ A 正确。Cisco ISR 必须具有正确的特性集，这要求特定版本（或更高版本）的 IOS 包含该特性集。
  
  ☒ B、C 和 D 不正确。无需添加任何软件或硬件模块，也不需要 Security Device Manager (SDM)。

- 3. ☑ B、C 和 D 正确。你可以使用 H.245、SIP Notify 或 KPML 通过 UBE 网关传输 DTMF 信号。
  
  ☒ A 不正确。作为边界控制器功能的一部分，UBE 网关不直接支持 SS7 信令。

- 4. ☑ A 和 B 正确。Cisco UBE 上的 QoS 同时支持 IP 优先级和 DSCP 标记。
  
  ☒ C 和 D 不正确。TCC 标记不是 Cisco 路由器支持的 QoS 方法。六西格玛是一种管理和流程方法，与 QoS 无关。

### 642-436：配置网守以支持 IP-to-IP 网关

- 5. ☑ D 正确。网守使用 via-zones 来判断何时路由到 UBE，以及何时可以在内部处理 VoIP 呼叫。
  
  ☒ A、B 和 C 不正确。与 Cisco UBE 网关相关，sRTP 和 cRTP 不是网守配置的必需参数。IPX 接口不用于 VoIP 网络。

### 642-436：配置 IP-to-IP 网关以提供地址隐藏

- 6. ☑ A 正确。简单的 address-hiding 命令用于隐藏 IP 地址。
  
  ☒ B、C 和 D 不正确。Address hiding、hide ip 和 hide-ip 是无效命令。它们在 Cisco IOS 路由器上或 Cisco UBE 网关内不起任何作用。

- 7. ☑ C 正确。地址隐藏确保在所有场景中，UBE 是唯一的信令和媒体入口或出口点。
  
  ☒ A、B 和 D 不正确。地址隐藏不会使入侵网络变得更困难，也不会使监控网络流量变得更容易。此外，UBE 是网络中信令和媒体进出的唯一点，而不是 CME。

### 642-436：配置 IP-to-IP 网关以提供协议和媒体互通

- 8. ☑ B 正确。SIP-to-SIP 实现的正确命令是 allowed-connections sip to sip 命令。
  
  ☒ A、C 和 D 不正确。你不能仅指示 allowed-connections sip 就实现 SIP-to-SIP。在 allowed-connections 命令的 sip to sip 子句中，不应包含连字符。allowed-connections 命令不存在 sip only 这样的选项。

- 9. ☑ C 正确。应使用 media flow-around 命令。该命令表示媒体（RTP 流）不应由 UBE 终止和重新发起。
  
  ☒ A、B 和 D 不正确。media flow-through 命令表示 UBE 应终止并重新发起 RTP 媒体流。media passthrough 和 RTP passthrough 命令不是有效的 IOS 命令。

### 642-436：配置 IP-to-IP 网关以提供呼叫准入控制

- 10. ☑ B 正确。max-conn 命令用于限制可同时通过拨号对等体的连接数。例如，max-conn 12 会将拨号对等体限制为 12 个并发连接。
  
  ☒ A、C 和 D 不正确。limit-conn、upper-conn 和 conn-limit 是 dial-peer 配置模式中的无效 IOS 命令。

- 11. ☑ B 正确。基于测量的 CAC 向 WAN 发送数据包，以测量 WAN 的性能。然后根据结果动态配置 CAC。
  
  ☒ A、C 和 D 不正确。本地 CAC 使用简单的连接限制，或受限于字面输入源（例如单条 POTS 线路）。基于资源的 CAC 使用网守和 RSVP。网守 CAC 不是 Cisco 术语。

- 12. ☑ A 和 C 正确。基于资源的 CAC 需要网守以及端点和网关上的 RSVP 协议支持。
  
  ☒ B 和 D 不正确。不需要 SIP 代理，也不使用 DiffServ。

