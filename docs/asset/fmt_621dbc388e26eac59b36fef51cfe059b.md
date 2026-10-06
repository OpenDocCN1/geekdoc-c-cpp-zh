
随着 Wi-Fi 标准的演进，开发出了多种关键认证方案。从最安全到最安全的认证方案顺序为 WEP、WPA、WPA2，然后是 WPA3 [2]。

在发现早期协议存在漏洞后，开发了更新的协议。事实证明等效网络隐私（WEP）存在许多缺陷，不应再继续使用。目前有许多现成的工具可以破解 WEP 加密。出于这个原因，Wi-Fi 联盟在 2004 年正式废弃了 WEP Wi-Fi 加密标准。

WPA 于 2003 年发布，作为 WPA2 的过渡阶段，WPA2 则于 2004 年发布。

WPA3 是针对 WPA2 中发现的漏洞而开发的，于 2018 年发布。

WPA3 添加的功能包括：

- 通过防止暴力破解字典攻击提供防暴力保护
- 公共网络隐私
- 针对物联网（IoT）的安全支持
- 通过支持 192 位加密提供更强的加密

现代 WPA3 路由器支持 WPA2/WPA3 过渡模式，因为并非所有连接接入点的设备都支持 WPA2。这是一种特殊的混合模式，同时使用 WPA3-Personal（后文将详细介绍）和 WPA2-Personal，允许不支持 WPA3 的旧设备连接到路由器。

WPA2 容易受到密钥重装攻击（KRACK），黑客可以利用该攻击拦截并操纵安全连接过程中新加密密钥的生成。然而，这是一种相对复杂的攻击，因此在无法使用 WPA3 的情况下，WPA2 可以提供实用的安全级别。

## 第 12 章 ZEPHYR RTOS WI-FI 应用

WPA3 要求所有连接都使用保护管理帧（PMF），这提供了额外的安全性。WPA3 可以使用 128 位 AES，但对于 WPA3 企业级连接，需要 192 位 AES。

WPA3 有三个版本：

- WPA3-Personal
- WPA3-Enterprise
- Wi-Fi 增强开放（Enhanced Open）

Wi-Fi 增强开放旨在为“开放式”网络上的用户提供 Wi-Fi 加密。无线路由器使用密钥对网络流量进行加密。在 WPA3-Personal 的情况下，该密钥根据路由器上设置的 Wi-Fi 密码计算。出于安全考虑，使用难以猜测的强密码至关重要。

### WPA3 SAE 密钥交换协议

SAE（等价身份认证）是一种密钥交换协议，它消除了加密密钥的重用，并提供了“前向安全性”。前向安全性防止攻击者即使知道 WPA3 密码，也无法解密之前记录的互联网连接。SAE 还使用点对点连接来建立交换，可以防止中间人拦截攻击。

### Wi-Fi 如何使用分配给它的频谱

Wi-Fi 可以使用 2.4 GHz ISM（工业科学医学）频段和 5 GHz 频段。2.4 GHz 频段非常拥挤，因为其带宽较窄，也被 BLE 和 Zigbee 等协议使用。相比之下，5 GHz 频段拥挤程度得多。尽管从理论上 Wi-Fi 应该完全迁移到 5 GHz 频谱，但在实践中，短期内不太可能发生，因为有许多工作在 2.4 GHz 的 Wi-Fi 设备。

Wi-Fi 一直不断演进，以提供更快的数据速率、更好的安全性和更低的功耗。标准既有 IEEE 名称，也有 Wi-Fi 联盟名称。例如，`802.11ac` 也称为 Wi-Fi 5。

Wi-Fi 的演进总结在以下要点中 [3]

- IEEE 802.11 是原始的 2.4 GHz Wi-Fi 标准，于 1997 年引入，开启了 Wi-Fi 的开发，这是最广泛使用的无线网络协议之一。
- IEEE 802.11b（或 Wi-Fi 1）于 1999 年引入，使用直接序列扩频/互补码键控（DSSS/CCK），以应对来自微波炉、无绳电话和婴儿监监视器等其他设备的干扰。它的室内范围约为 38 米，室外范围约为 140 米。
- IEEE 802.11a（或 Wi-Fi 2）于 1999 年引入，作为 IEEE 802.11b 的继者。它使用 OFDM（正交频分复用）调制提供更高的数据速率，并支持 5 GHz 操作。
- IEEE 802.11g（或 Wi-Fi 3）于 2003 年引入，在与 IEEE 802.11b 相同的 2.4 GHz 频段内通过各种 OFDM 增强提供了高达 54 Mbit/s 的更快数据速率。它在大众市场中非常受欢迎，因为 2.4 GHz 设备比 5 GHz 设备便宜。
- IEEE 802.11n（或 Wi-Fi 4）于 2009 年引入，作为一种支持 2.4 GHz 和 5 GHz 频段的标准，数据速率高达 600 Mbit/s。
- IEEE 802.11ac（或 Wi-Fi 5）于 2013 年引入，以启用多输入多输出（MIMO）技术，支持高达 3.5 Gbit/s 的速率。
- IEEE 802.11ax（或 Wi-Fi 6）于 2021 年发布，解决了 Wi-Fi 使用问题，支持高达 9.6 Gbit/s 的速率。

### Wi-Fi 帧与 802.11 数据包结构 - 概述

Wi-Fi 帧主要有三种：

- 管理帧
- 控制帧
- 数据帧

管理帧用于发现 AP（接入点）并加入 BSS（基本服务集）。它们包括信标（Beacon）、探测请求和响应、认证和去认证、关联和去关联。

控制帧用于确认成功传输并保留介质。常见的控制帧类型包括 ACK、发送请求（RTS）和清除发送（CTS）。

数据帧包含实际数据，是唯一从无线转发到有线的包。数据帧类型包括数据和空帧。

Wi-Fi 层头部比相应的以太层头部更复杂。它提供了信道、数据速率和信号强度等信息。

- 信道（频率）必要的，因为无线局域网可能支持 3 到 25 个不同的信道。
- 关于正在使用的数据速率的信息。
- 信号强度 – 以 dBm 表示。它是对预期信号质量的衡量。

### 接入点

接入点可以被认为是连接客户端（移动站）与网络上其他设备的桥梁。在移动站通过 AP 发送流量之前，它必须建立关联以进入适当连接状态 [4]。

### 发现接入点

扫描附近的接入点可以使用被动或主动方法。

在主动方法中，搜索设备轮流调到支持的每个信道，发送探测请求帧，并等待 20-40 毫秒收集该信道 AP 的探测响应帧，然后进入下一个信道。

在被动扫描中，搜索设备轮流调到每个信道并等待一个典型的信标间隔（约 100 毫秒）以收集信标。被动扫描比主动扫描慢。

### 认证与关联

三个 802.11 连接状态如下：

- 未认证未关联
- 已认证但尚未关联
- 已认证并关联

为了进行桥接，移动站必须处于已认证且关联的状态。认证涉及移动站和 AP 交换一系列 802.11 管理帧。

交换序列如示意图所示：

![](img/d625a3dc80e999570aa2c88dcc398b17_593_0.png)

图 12-1 认证与关联序列图

+ 1. 移动站发送探测请求（probe requests）以发现周附近的 802.11 网络。探测请求通告了移动站支持的数据速率和 802.11ac 标准。由于探测请求是从移动站发送到 BSSID 为 ff:ff:ff:ff:ff:ff（接入点无线网卡的 48 位 MAC 地址）的目标层 2 地址，因此所有接收到该请求的 AP 都会做出响应。

2. 接收到探测请求的 AP 会检查移动站是否至少有一个共同支持的数据速率。如果是这种情况，则会发送探测响应（probe response），通告 SSID（无线网络名称）、支持的数据速率、如果所需的加密类型，以及 AP 的其他 802.11set。

移动站从收到的探测响应中选择兼容的网络。兼容性可能需要考虑加密类型。当发现可连接的网络后，移动站将尝试与兼容的 AP 进行底层 802.11 认证。初始的 802.11 认证使用开放的认证帧，并且几乎总是会成功。

3. 移动站向 AP 发送底层 802.11 认证帧，将认证设置为开放（open），并将序列设置为 0x0001。

4. AP 接收到认证帧，并向移动站响应一个设置为开放的认证帧，指示序列为 0x0002。

如果 AP 接收到未认证移动站发送的除认证或探测请求以外的任何帧，它将响应去认证帧（deauthentication frame），将移动站置于未认证且未关联的状态。该站必须从底层认证步骤重新开始关联过程。此时，移动站已通过认证但尚未关联。

某些 802.11 功能允许移动站对多个 AP 进行底层认证，这可以加快在 AP 之间移动时的关联过程。尽管移动站可能对多个 AP 经过了 802.11 认证，但它同一时间只能与单个 AP 主动关联并传输数据。

+ 5. 一旦移动站确定了想要关联的 AP，它将向该 AP 发送关联请求（association request）。关联请求包含了所需的所选加密类型和其他兼容的 802.11 功能。

一旦 AP 接收到来自已认证但尚未关联的移动站的帧，它将响应去关联帧（disassociation frame），将移动站置于已认证但未关联的状态。

+ 6. 如果关联请求中的元素与 AP 的功能匹配，则 AP 将为移动站创建一个关联 ID（Association ID），并响应关联响应成功消息，授予移动站网络访问权限。

+ 7. 现在移动站已成功与 AP 关联，可以开始数据传输。

如果无线网络需要 WPA/WPA2/WPA3 或 802.1X 认证，则在 802.11 关联完成后完成动态密钥和认证之前，移动站将无法发送数据。

## Zephyr RTOS 与 Wi-Fi 应用开发

Zephyr RTOS 框架包含了对 Wi-Fi 的支持，通常通过支持各种扩展板（shields）和开发板来实现。Arduino 兼容扩展板的示例包括 Inventek e-WIFI Shield、Adafruit WINC1500 WiFi Shield 以及基于 ESP32 处理器的 MikroElektronika WIFI 和 BLE Shield。Zephyr 还支持各种带有片上 ESP32 Wi-Fi 的 ESP32 板，例如 Olimex ESP32 EVB。

由于本书广泛使用了 Nordic Semiconductor nRF 板，本章使用的主板将是 nRF7002 DK，它集成了 Nordic 的 nRF7002 作为 Wi-Fi 6 协处理器 IC [8, 9]。nRF7002 DK 使用 nRF5340 多协议系统级芯片（SoC）作为 nRF7002 的主处理器。nRF7002 DK 是一种为了低功耗设计的 Wi-Fi 6 协处理器，支持 2.4 GHz 和 5 GHz，以及 802.11a/b/g/ac/ax。

### nRF7002 DK – 概述

![](img/d625a3dc80e999570aa2c88dcc398b17_597.png)

图 12-2 nRF7002 DK 顶视图

由于 nRF7002 DK 结合了 nRF5340 系统级芯片（SoC）和 nRF7002 Wi-Fi 协处理器，它提供了以下功能：

- 低功耗蓝牙 (BLE)
- 近场通信 (NFC)
- 其他协议
- 目标唤醒时间 (TWT)
- WPA3 支持
- 正交频分多接入 (OFDMA)
- Wi-Fi 6 功能
- 波束成形 (Beamforming)
- 下行和上行

### Wi-Fi 扫描示例

示例可以在 nRF SDK 的 `nrf\samples\scan` 中。这是一个展示如何实现本地 Wi-Fi 热点的应用程序。示例代码了如何在 2.4 GHz 和 5 GHz 波段进行扫描，即：

- 默认扫描
- 主动扫描
- 被动扫描
- 2.4 GHz 主动扫描
- 2.4 GHz 被动扫描
- 5 GHz 主动扫描
- 5 GHz 被动扫描
- 仅扫描 2.4 GHz 非重叠通道
- 仅扫描 5 GHz DFS 信道

### Zephyr 网络管理 – 概述

网络管理 API [5] 的目的是允许应用程序和网络层代码调用特定例程，并接收协议栈中任何级别的网络事件通知。

由于 Zephyr 应用是单体式的且类似于操作系统本身，只有需要的例程会被编译到应用程序中，特定的网络管理代码通过使用 `NET_MGMT_REGISTER_REQUEST` 宏定义并注册处理器来提供。用于收集接收和发送数据包信息的函数原型和宏定义在 `zephyr/subsys/net/ip` 文件夹下的 `net_private.h` 头文件中。

### 请求定义的网络管理程序

网络管理请求的形式为 `net_mgmt(mgmt_request, ...)`。

`mgmt_request` 参数是一个位掩码，指示目标栈层，以及是否隐含了 net_if 对象以及正在请求特定的管理程序。可用的程序请求取决于实现方式。

#### 监听网络事件

接收网络事件通知的步骤是注册回调函数，并指定过滤器以选择感兴趣的事件，以便调用该回调。

可以通过调用 `net_mgmt_add_event_callback()` 函数注册回调函数，并通过调用 `net_mgmt_del_event_callback()` 函数注销注册。`net_mgmt_init_event_callback()` 函数可用于正确初始化相应的 `struct net_mgmt_event_callback` 数据结构。

当事件与回调关联的事件集中的某项匹配时，回调函数将带有实际事件代码被调用。由于set过滤可能会向回调函数传递假正例，因此回调函数有责任检查事件代码（作为参数传递）是否对应于它将处理的某个特定网络事件。

为了从多个层接收事件，需要注册多个监听器，为每个被监听的层各注册一个。在这一前提下，回调处理函数可以在不同层的事件之间共享。

#### 定义网络管理程序

通过定义句处理程序并将其注册到相关的 `mgmt_request` 代码中，可以提供特定于自定义栈实现的管理程序。

管理请求代码根据目标层定义在相关位置，或者，如果目标是 L2 层，则还取决于所使用的技术。例如，IP 层管理请求代码可以在 `include/zephyr/net/net_event.h` 头文件中找到。在 L2 技术（例如以太网）的情况下，这些代码可以在 `include/zephyr/net/ethernet.h` 中找到。

#### 网络事件

通过调用 `net_mgmt_event_notify()` 函数并提供相应的网络事件代码作为参数，可以发出特定网络事件信号。

### 从 nRF Connect SDK 仓库构建 Wi-Fi 扫描示例

传递给 West 的 nRF7002 DK 构建目标是“nrf7002dk_nrf5340_cpuapp”构建目标。可以使用多种命令行选项来指定要构建的扫描应用程序类型。

- 构建仅获取设备扫描结果

  `west build -b nrf7002dk_nrf5340_cpuapp`

- 构建仅获取原始（Raw）扫描结果

  `west build -b nrf7002dk_nrf5340_cpuapp -- -DCONFIG_WIFI_MGMT_RAW_SCAN_RESULTS=y -DCONFIG_WIFI_MGMT_RAW_SCAN_RESULTS_ONLY=y`

- 构建同时获取原始和设备扫描结果

  `west build -b nrf7002dk_nrf5340_cpuapp -- -DCONFIG_WIFI_MGMT_RAW_SCAN_RESULTS=y`

### nRF Connect SDK 仓库扫描示例的结构化概述

通过学习单函数 `main.c` 中扫描应用程序代码，可以探索 Wi-Fi 标准的各个方面、主动和被动 Wi-Fi 扫描，以及 Zephyr 网络管理 API。

正如预期的那样，文件开头有各种 `#includes` 和 `#define`，并有一个 `LOG_MODULE_REGISTER` 调用，以便输出扫描结果。正如预期的那样，包含的许多头文件来自 `zephyr/net` 文件夹。此外还有一个根据构建过程中的各种定义来指定 `WIFI_SHELL_MGMT_EVENTS` 的条件。

```c
#include <zephyr/logging/log.h>
LOG_MODULE_REGISTER(scan, CONFIG_LOG_DEFAULT_LEVEL);
#include <zephyr/kernel.h>
#if defined(CLOCK_FEATURE_HFCLK_DIVIDE_PRESENT) || NRF_CLOCK_HAS_HFCLK192M
#include <nrfx_clock.h>
#endif
#include <stdio.h>
#include <stdlib.h>
#include <zephyr/shell/shell.h>
#include <zephyr/sys/printk.h>
#include <zephyr/init.h>
#include <zephyr/net/net_if.h>
#include <zephyr/net/wifi_mgmt.h>
#include <zephyr/net/wifi_utils.h>
#include <zephyr/net/net_event.h>
#include <zephyr/net/ethernet.h>
#include <zephyr/net/ethernet.
```

```c
#include <zephyr/net/ethernet.h>
#include "net_private.h"
#define WIFI_SHELL_MODULE "wifi"
#ifdef CONFIG_WIFI_MGMT_RAW_ONLY
#define WIFI_SHELL_MGMT_EVENTS (NET_EVENT_WIFI_SCAN_RESULT |
    NET_EVENT_WIFI_SCAN_DONE)
#else
#define WIFI_SHELL_MGMT_EVENTS (NET_EVENT_WIFI_SCAN_RESULT |
    NET_EVENT_WIFI_SCAN_DONE |
    NET_EVENT_WIFI_SCAN_RESULT)
#endif
#define SCAN_TIMEOUT_MS 10000
```

全局变量是 `scan_params` 类型的数组，根据扫描类型初始化，如下所示：
