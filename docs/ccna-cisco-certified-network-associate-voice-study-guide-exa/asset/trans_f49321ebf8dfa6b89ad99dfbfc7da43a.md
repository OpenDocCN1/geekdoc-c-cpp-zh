

6. ☑ **A 正确。** `dspfarm profile 5 transcode` 命令是正确的。该命令中的正确顺序是 `dspfarm profile`，后跟配置文件 ID，然后是配置文件类型，可以是 conference、mtp 或 transcode。

   ☒ **B、C 和 D 不正确。** 命令 `dspfarm profile transcode 5` 的配置文件 ID 和配置文件类型顺序错误。Cisco IOS 中不存在 `create dspfarm` 命令。

7. ☑ **A 正确。** `maximum sessions 5` 命令是正确的。此命令应在 dspfarm-profile 配置模式下输入。

   ☒ **B、C 和 D 不正确。** 命令 `session 5`、`max-sessions 5` 和 `maximum dsp actions 5` 不是有效的 IOS 命令。

8. ☑ **D 正确。** flex 模式同时允许中等和高复杂度编解码器，因此命令 `codec complexity flex` 是正确的。

   ☒ **A、B 和 C 不正确。** 这三个命令完全无效。应改用 `codec complexity flex` 命令。

9. ☑ **A 正确。** `dsp services dspfarm` 命令将 DSP 资源分配或分配给 DSP farm。该命令应在 voice-card 配置模式下输入。

   ☒ **B、C 和 D 不正确。** 这三个命令无效。

10. ☑ **A 正确。** 如果语音卡是语音卡 1，正确的命令是 `voice-card 1`。该命令始终是 `voice-card` 后跟卡号。这个简短命令将路由器置于指定语音卡的 voice-card 配置模式。

    ☒ **B、C 和 D 不正确。** 这三个命令无效。

## 实验答案

配置 DSP farm 的三个基本步骤是：配置编解码器复杂度、将 DSP 资源分配给 DSP farm，以及配置 DSP farm 配置文件。例如，要使用 DSP 资源进行转码，应使用图 11-5 中的命令。

现在 DSP 资源已配置，你可以使用 `show voice dsp` 命令查看 DSP 资源的信息，如图 11-6 所示，其中使用了 detail 选项。

你还可以使用 `show running-config` 命令查看 DSP 配置文件，配置如图 11-7 所示。

**图 11-7**

在运行配置中查看 DSP 配置文件配置

```
voice-port 0/0/0
voice-port 0/0/1

dspfarm profile 1 transcode
 codec g711alaw
 codec g729ar8
 codec g729abr8
 maximum sessions 4
 associate application SCCP

gatekeeper
 shutdown
```

![](img/ee67e6cd30f16bc39d653f87870eabb5_350_0.png)

## 12 Communications Manager Express

### 认证目标

| 目标 | 主题 | 活动 |
|---|---|---|
| 12.01 | 640-460：使用 CLI 实施 Cisco Unified Communications Manager Express 以支持端点 | ✓ 两分钟演练<br>问答自测 |

> 消息灵通的人知道通过电线传输语音是不可能的。
> 即使可能，也没有实际价值。
> ——《波士顿邮报》，1865 年

在电话技术的早期，一位活生生的接线员会坐在房间里，等待客户在家中或大楼里拿起电话听筒，以便接线员将线缆插入正确的插孔位置来完成呼叫。这位接线员就是人工呼叫管理器，负责管理呼叫的建立。一旦呼叫建立，主叫方和被叫方就可以直接通信，但需要接线员来建立呼叫。Cisco Unified Communications Manager Express（以前称为 CallManager Express）扮演的就是这位传统接线员的角色。在本章中，你将了解 Communications Manager Express 的功能和特性，以及如何在 Cisco 集成服务路由器（ISR）上实施该软件。

### 认证目标 12.01

**640-460：使用 CLI 实施 Cisco Unified Communications Manager Express 以支持端点**

在小型网络中，不太可能需要完整的 Unified Communications Manager。Cisco 提供了一种替代解决方案，称为 Cisco Unified Communications Manager Express，简称 CME，可满足小型 VoIP 网络和分支机构的需求。在本节中，你将了解 CME 的特性、实施过程，以及使用 CME CLI 配置各种语音功能所需的配置命令。

### Communications Manager Express (CME) 简介

Cisco 的 CME 运行在集成服务路由器（ISR）上，例如 2600、3600、2800 和 3800 系列设备。不需要专用服务器，因为 CME 软件运行在路由器的内存和处理器中。支持的手机数量取决于所使用的 ISR。表 12-1 列出了各种 ISR 型号以及在运行 CME 版本 4.3（现代 VoIP 网络中非常流行的版本）时这些型号支持的手机数量。

**表 12-1** ISR 与最大电话支持数

| ISR 型号 | 最大支持电话数 |
|---|---|
| UC500 系列 | 48 |
| 1861 | 8 |
| 2801 | 25 |
| 2811 | 35 |
| 2821 | 50 |
| 3825 | 175 |
| 3845 | 250 |

> 请记住，CME 软件运行在 ISR 上，而不是运行在专用的特殊服务器上。还要记住，不同的 ISR 型号支持不同数量的电话。

除了支持的手机数量之外，了解支持哪些手机也很重要。CME 版本 4.3 支持以下任意手机：

- SIP 3911
- 7906G
- 7911G
- 7920/7921G
- 7931G
- 7940G/7941G/7941G-GE/7942G/7945G
- 7960G/7961G/7961G-GE/7962G/7965G
- 7970G/7971G-GE/7975G
- 7985G 视频电话
- 7936/7937 会议站

> **注意** 新的 CME 版本 8 在 Cisco 3945E ISR 上最多支持 450 部电话；但是，当前的 CCNA Voice 和 CVOICE 考试不太可能考到该版本。

CME 可以充当电话/呼叫管理器、中继管理器，以及到 Cisco Unity 和 Cisco Unity Express 等语音邮件解决方案的连接器。根据 Cisco 的 CME 4.3 数据表，CME 4.3 支持以下电话功能：

- 每个系统最多 250 部电话
- 每部电话最多 34 个线路外观
- 使用 Cisco Unified IP Phone Expansion Module 7914 的接线员控制台功能
- 快速转接：盲转或咨询转
- 忙灯
- 静音振铃选项
- 外呼自动线路选择
- 忙时、无应答和全部呼叫转移（内部或外部）
- 呼叫全部转移限制控制
- 请勿打扰（DND）
- 设置 DND 时的功能振铃
- IP 电话显示 DND 状态
- 在 SIP 电话上加载拨号计划模式
- 将呼叫直接转至语音邮件
- 自定义软键
- 按线路启用和禁用呼叫等待通知
- 带叠加目录号码的呼叫等待
- 呼叫等待振铃
- 每个按钮双路或 8 路呼叫线路外观
- 非工作时间长途限制覆盖
- 使用耳机的自动应答
- 欧洲日期格式
- 跨模拟 PSTN 中继的拍叉传递
- 空闲 URL：定期在 IP 电话上推送消息或图形
- 末位号码重拨
- 实时录制到 Cisco Unity Express 邮箱
- 本地名称目录查询
- 摘机拨号
- 通过 IP 电话进行配置更改的站点快速拨号
- 10,000 个号码的系统快速拨号
- 静音和功能振铃选项
- 基于 SIP 的线路侧订阅，提供电话状态的基本呈现
- 转至语音邮件软键
- 在共享线路上进行有隐私的呼叫强插
- 使用软键或功能访问码访问功能
- 远程远程工作者 IP 电话支持
- 动态加入或离开寻线组
- 在 SCCP 模式下使用 Cisco ATA 186 模拟电话适配器或 Cisco VG224 模拟电话网关支持模拟电话
- 在外汇局（FXS）端口或使用 H.323、SCCP 或 SIP 的 ATA 上支持传真机
- Cisco Unified IP 显示电话上的 XML 应用服务
- 使用 Cisco Unified Video Advantage 或 Cisco Unified IP Phone 7985G 视频端点进行站点到站点的带语音视频
- 单站点内的分机移动性
- 宽带音频（G.722）和 iLBC（Internet 低比特率编解码器）

由于 CME 运行在用作通往其他网络网关的 ISR 路由器上，因此还支持以下中继功能：

- 模拟外汇局（FXO）环路启动和接地启动
- 耳和口（E&M）
- 基本速率接口（BRI）和主速率接口（PRI）支持（NI2、4ESS、5ESS、EuroISDN、DMS100 和 DMS250），并且 Cisco IOS 软件目前还支持其他几种交换机类型
- 主叫 ID 名称和号码

