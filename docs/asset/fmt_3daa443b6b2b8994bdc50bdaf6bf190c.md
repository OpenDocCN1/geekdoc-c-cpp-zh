
```xml
<property name="NOTIFY" />
<permission name="READ" />
<permission name="WRITE" />
<descriptor name="Client Descriptor Configuration Descriptor" uuid="00002902-0000-1000-8000-00805f9b34fb" value="00" enabled="true">
  <permission name="READ" />
  <permission name="WRITE" />
</descriptor>
</characteristic>
<characteristic name="Local Time Information" uuid="00002A0F-0000-1000-8000-00805f9b34fb" value="00" enabled="true">
  <property name="READ" />
  <property name="WRITE" />
  <permission name="READ" />
  <permission name="WRITE" />
</characteristic>
<characteristic name="Reference Time Information" uuid="00002A14-0000-1000-8000-00805f9b34fb" value="00" enabled="true">
  <property name="READ" />
  <permission name="READ" />
</characteristic>
</service>
</server-configuration>
```

## 属性操作 (Attribute Operations)

共有六种属性操作。它们分别是命令 `Commands`、请求 `Requests`、通知 `Notifications`、响应 `Responses`、指示 `Indications` 和确认 `Confirmations`。

- 命令由客户端发送到服务器，且不需要响应。
- 请求由客户端发送到服务器，并且需要响应。
  * 请求有两种类型：信息查询请求 `Find Information Request` 和读取请求 `Read Request`。
- 响应由服务器响应请求而发送。
- 如果客户端对某个感兴趣的特征启用了通知，则服务器将通知发送给客户端，告知客户端特定特征的值已更改。
  * 通知不需要客户端回复响应来确认已收到。
- 指示由服务器发送给客户端；它们与通知类似，但需要客户端发回确认，以通知服务器指示已成功接收。

通知和指示通过客户端特征配置描述符 `CCCD` 属性暴露。向此属性值写入“1”可以启用通知，写入“2”可以启用指示，写入“0”则同时禁用通知和指示。

确认数据包是客户端发送到服务器的封包，用于告知服务器客户端已成功收到了指示。

## 请求 – 流控制、读取属性和写入属性

请求在顺序上是串行执行的，因为在发送新请求之前，需要服务器的响应。指示也有类似的要求；在收到服务器对上一个指示的确认之前，不能发送新的指示。

然而，请求和指示在顺序要求方面是互斥的。因此，服务器可以在响应较早的请求之前先发送一个指示。

命令和通知不需要任何流控制；它们可以在任何时间发送。因此，可能会因为缓冲区和处理限制等问题导致命令或通知丢失。这意味着命令和通知不能被认为是可靠的。如果可靠性是考虑因素，应使用请求和指示代替命令和通知。

属性读取本质上是请求，因为它们需要响应。读取有多种可能的类型。这包括读取请求，它给出了句柄 `handle` 和指示读取起始位置的偏移量 `offset`，因此只返回指定特征的一部分。

对属性的写入可以以写入请求或写入命令的形式发出。写入命令不需要服务器的响应，而写入请求则需要服务器确认属性已写入。

此外还有队列写入 `queued writes`，它可用于提供涉及多次写入的原子操作。队列写入涉及准备写入请求，这些请求将包含一个偏移量，用于指定发送的值应写入属性值中的哪个位置。这些发送的值也被称为就绪值 `prepared values`，当需要写入单个消息无法容纳的值时可以使用它们。就绪值存储在服务器端的缓冲区中，而不是直接写入属性。一旦发送了所有就绪值，就会使用写入请求请求服务器执行或取消就绪值的写入。服务器必须响应以确认发送服务器的完整值已写入。

## 蓝牙 5

蓝牙 5 为 BLE 增加了许多额外功能。这些 `2M PHY` 指定了如何实现比之前版本快一倍的速率、`Coded PHY` 使其能够扩展之前版本的范围，并实现数百米外设备间的 BLE 通信。蓝牙 5 还支持扩展广告，利用辅助广播信道使设备能够广播比主广播信道允许更多的数据。在扩展广告的情况下，在主广播信道上的广告数据包提供了发现在辅助广播信道上的卸载广告所需的信息。蓝牙 5 还支持周期广播模式，两个或多个设备以无连接的方式进行通信。

在周期广播模式下，外设设备发送同步信息和其他广告数据，允许另一个设备与外设设备同步，并以固定的间隔接收外设设备的扩展广告。

## BLE 安全

BLE 安全由架构中的安全管理器 `SM` 层处理。

安全管理器定义了两个设备之间生成和交换密钥的协议和算法，并涉及配对 `pairing`、绑定 `bonding`、认证 `authentication`、加密 `encryption`，最后是消息完整性 `message integrity`。

这些步骤如图 7-8 所示的序列图所示。

# 第 7 章 开发 ZePHYR BLE 应用

| 发起者 | 响应者 |
|---|---|
| | 已建立连接 |
| （可选）安全请求 | |
| 配对请求 | 阶段 1 |
| 配对响应 | |
| 安全连接的传统配对 | 阶段 2 |
| 使用第 2 阶段生成的密钥建立加密连接 | |
| 密钥分配 | |
| 密钥分配 | 阶段 3 |
| 密钥分配 | |

图 7-8 BLE 安全序列图

根据上述原理图，配对 `pairing` 是阶段 1 和阶段 2 的结合，而绑定 `bonding` 则由阶段 3 表示。配对是一种临时安全措施，它不会跨连接持久存在，并且每当两个设备重新连接并希望加密它们之间的连接时，都需要启动并完成配对。为了将加密扩展到后续连接，两个设备之间必须进行绑定。

326

# 构建和测试外设与中心 BLE 应用

构建和测试 BLE 应用至少需要设置一个包含多个运行 BLE 节点的小型 BLE 网络，例如运行一个 BLE 外设应用、一个 BLE 中心应用，可能还有一个 BLE 通信扫描和协议分析应用。这里介绍的示例涉及使用 Nordic Semiconductor nRF 设备，结合了 `nRF52840 DK`、`nRF52840` 适配器 `dongle`、手机以及 `nRF Connect` 蓝牙低功耗应用。另一种方法是使用 `Renode` 模拟 BLE 网络和 BLE 应用。

# nRF52840 适配器及其用途

`nRF52840` 适配器基于 Nordic Semiconductor `nRF52840` 芯片的小型、低成本 USB 适配器，具有几个 I/O 外设，包括一个按钮、两个 LED 和 15 个 GPIO 引。作为一个适配器，它可以启用 `nRF Connect PC` 应用，例如蓝牙低功耗应用、 `nRF` 云网关应用和 RSSI 查看器应用。它可以用于开发自定义应用并运行 `nRF Connect SDK` 提供的示例应用以及 BLE 示例程序。适配器还可以被编程作为 BLE 嗅探器工作。

# 第 7 章 开发 ZePHYR BLE 应用

## nRF Connect 蓝牙低功耗应用

`nRF Connect` 应用可以被认为是桌面版 `nRF` 应用的单一枢纽。如图 7-9 所示，这些应用包括蓝牙低功耗应用、功率分析仪 `Power Profiler`、编程器 `Programmer` 和 RSSI 查看器。

![](img/d625a3dc80e999570aa2c88dcc398b17_341_0.png)

**图 7-9.** nRF Connect for Desktop

328

**注意** 随着 `nRF Connect` 更新到更高版本，此处显示的截图可能与实际观察到的不同。

蓝牙低功耗应用有两种工作模式。它可以作为 BLE 中心设备运行，用于发现广告设备；也可以作为 BLE 外设运行，用于发布广告、允许连接并暴露 GATT 服务器。GATT 服务器可以使用 SIG 采纳的服务和特征进行自定义，甚至可以使用自定义的服务和特征。

## 设置 nRF52840 适配器以供 nRF Connect for Desktop nRF BLE 应用使用

为了在 `nRF BLE` 应用中使用 `nRF52840` 适配器，需要对其进行相应的固件编程。所需的步骤是：将适配器插入 PC USB 端口，启动 `nRF Connect for Desktop` 蓝牙低功耗应用，然后对发现的设备点击 `SELECT DEVICE`，然后进行编程。

![](img/d625a3dc80e999570aa2c88dcc398b17_343_0.png)

**图 7-10. 启动 nRF Connect for Desktop 蓝牙低功耗应用**

![](img/d625a3dc80e999570aa2c88dcc398b17_343_1.png)

**图 7-11. 选择发现的设备**

330

## 确认

设备必须编程，你要继续吗？

**图 7-12. 确认选择发现的设备**

在设备编程完成后，将如图 7-13 所示显示设备详情。

![](img/d625a3dc80e999570aa2c88dcc398b17_344_0.png)

**图 7-13. 显示已编程设备的详情**

一旦适配器编程完成，就可以作为 BLE 中心设备或 BLE 外设使用。

## 在 BLE 中心模式下使用适配器

在此模式下，该应用可用于发现相邻设备、连接到广告设备，并通过对特征的读、写、通知 `notifications` 以及指示 `indications` 与已连接的外设 GATT 服务器进行交互。扫描外设涉及点击 `Start` 按钮来扫描设备。一旦建立连接，就可以浏览 GATT 服务器暴露的不同服务和特征。

![](img/d625a3dc80e999570aa2c88dcc398b17_345_0.png)

**图 7-14. 显示已编程设备的详情**

点击连接选项将提供额外信息。

## BLE 连接图

连接图显示了已建立的连接，并用于对其进行检查。

![](img/d625a3dc80e999570aa2c88dcc398b17_346_0.png)

**图 7-15. BLE 连接图**

在连接图中，悬停在连接图标上将显示连接间隔 `connection interval`、从机延迟 `slave latency`、监控超时 `supervision timeout`、绑定状态和配对状态。

![](img/d625a3dc80e999570aa2c88dcc398b17_347_0.png)

**图 7-16. 连接详情**

点击连接图标会弹出用于更改连接参数、启动配对和断开连接的菜单。

![](img/d625a3dc80e999570aa2c88dcc398b17_347_1.png)

**图 7-17. 修改连接属性**

点击与关联的服务将打开子菜单，可以在其中执行读写操作。

![](img/d625a3dc80e999570aa2c88dcc398b17_348_0.png)

**图 7-18. 读取按钮状态**

![](img/d625a3dc80e999570aa2c88dcc398b17_348_1.png)

**图 7-19. 写入按钮状态**

## 在 BLE 外设模式下使用适配器

当在外设模式下运行时，适配器被设置为作为外设工作。在此模式下运行应用时，可以设置和配置仿真 GATT 服务器暴露的不同参数、服务和特征。这是通过运行服务器设置来实现，可以通过导航到 `Server Setup` 选项卡来访问。

![](img/d625a3dc80e999570aa2c88dcc398b17_350_0.png)

### 图 7-21. 配置设备名称

一旦完成服务的配置/自定义，可以通过点击 `Apply to device` 按钮应用，然后在 `Connection Map` 选项卡中，点击 `nRF5x` dongle 列表旁齿轮按钮并点击 `Start advertising`，如图 7-22 所示。

# 第 7 章 开发 ZEPHYR BLE 应用

![](img/d625a3dc80e999570aa2c88dcc398b17_351_0.png)

图 7-22. 显示开始广播的广播菜单

一旦 dongle 开始广播，将显示无线图标。此时，可以使用手机运行的 Nordic RF Connect 或 LightBlue Explorer 等 BLE 客户端模拟器应用来检查设备是否正在广播且工作正常。

![](img/d625a3dc80e999570aa2c88dcc398b17_351_1.png)

图 7-23. 适配器广播

## 使用电源模式仿真设置仿真电池服务

可以通过导航到 `Server Setup` 选项卡并从列出的服务列表中选择要创建的服务，例如电池服务，来设置基于 dongle 的仿真作为外围设备，暴露 GATT 服务器暴露的各种服务和特征。

![](img/d625a3dc80e999570aa2c88dcc398b17_352_0.png)

图 7-24. 配置 dongle 仿真电池服务

然后，可以通过从特征列表中选择并点击某个特征来创建一个特征，例如图 7-25 所示的电量水平。

# 第 7 章 开发 ZEPHYR BLE 应用

![](img/d625a3dc80e999570aa2c88dcc398b17_353_0.png)

**图 7-25.** 选择电量水平特征

然后可以设置该特征的属性，例如其初始值以及读、写、通知和指示行为。

![](img/d625a3dc80e999570aa2c88dcc398b17_353_1.png)

**图 7-26.** 为电量水平特征设置属性

# 第 7 章 开发 ZEPHYR 应用

如果如本例所示设置了 Notify 和 Indication，则需要通过点击 `New Characteristic` 为电量水平创建一个 `Client Characteristic Configuration Descriptor`，然后点击新创建的特征并选择 `Client Characteristic Configuration Descriptor`。这如图 7-27 所示。

![](img/d625a3dc80e999570aa2c88dcc398b17_354_0.png)

图 7-27. 配置客户端特征

然后可以通过点击 `Apply to device` 按钮将配置应用到设备上。如果这涉及重写现有配置，则会显示请求确认重置设备的对话框。

![](img/d625a3dc80e999570aa2c88dcc398b17_354_1.png)

图 7-28. 确认客户端特征配置

最后一步是导航到 `Connection Map`，点击 `nRF5x` dongle 列表旁齿轮按钮，然后点击 `Start advertising`。

# 第 7 章 开发 ZEPHYR BLE 应用

要测试外围设备需要一个中心设备。一种方法是使用手机，例如如 LightBlue 等 iPhone 应用。当该应用启动时，它将扫描并显示附近的外围设备列表。选择 dongle 将建立连接，并通过查询所选外围设备的服务来发现电池服务。

![](img/d625a3dc80e999570aa2c88dcc398b17_355_0.png)

**图 7-29.** LightBlue 应用选择附近的外围设备

点击 `Battery Level` 将显示通过已建立连接与服务交互的详细信息和选项。在 `Connection Map` 选项卡中点击 `Battery Service` 将弹出一个与外围设备交互的对话框。

## Zephyr 和 nRF Connect SDK 提供的 BLE 应用开发

Zephyr BLE API 集合既庞大又全面。这里将仅介绍启动 BLE 开发最核心的 API。核心且基础的 Zephyr API 包括 `ATT`、`GAP`、`UUID`、`SDP` 以及逻辑控制和适配协议 `L2CAP`。
