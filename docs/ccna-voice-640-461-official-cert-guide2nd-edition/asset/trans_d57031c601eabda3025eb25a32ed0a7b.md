

-   隐私设置
-   服务订阅
-   拨号名称

存在默认设备配置（Default Device Profile），允许针对特定 IP 电话类型没有用户设备配置的用户使用 EM（扩展移动性）登录。

## 在 CUCM 中启用 EM

启用 EM 涉及多个步骤，根据系统中的电话和用户数量，某些步骤可能需要重复多次。基本步骤如下：

1. 激活 Cisco EM 服务。
2. 配置 EM 服务参数。
3. 添加 EM 服务。
4. 为正在使用的每种电话型号创建默认设备配置。
5. 创建设备配置并将其订阅到 EM 服务。
6. 创建终端用户并与设备配置关联。
7. 为电话启用 EM 并让电话订阅到 EM 服务。

后续章节将更详细地描述这些步骤。

### 步骤 1：激活 EM 服务

- 1.1 在 Serviceability（服务性）Web页面中，导航至 Tools（工具） > Service Activation（服务激活）。
- 1.2 选择 Cisco Extension Mobility，然后点击 Save（保存）。

### 步骤 2：配置 EM 服务参数

- 2.1 在 CM Administration（CM 管理）Web页面中，导航至 System（系统） > Service Parameters（服务参数）。从 Server 下拉列表中选择您想要配置的服务器，然后在 Service 下拉列表中选择 Cisco Extension Mobility Service。

- 2.2 向下滚动到 Clusterwide Parameters（集群范围参数）部分。在此，您可以选择在最大登录时间过期后强制强制 EM 登录，以及该计时器的时长。这里您还可以如前所述，设置多次登录的行为（不允许多次登录、允许多次登录或自动注销）。此处的额外设置包括：启用字母数字用户 ID（或仅使用数字）、选择在电话上记住并显示最后一次登录的 User ID 为字母数字格式（或不显示），以及在注销时是否清除最后登录用户的呼叫列表。

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_322_0.png)

### 步骤 3：添加 EM 服务

- 3.1 导航至 Device（设备） > Device Settings（设备设置） > Phone Services（电话服务）。
- 3.2 点击 New（新建）。
- 3.3 如果需要，为 EM 服务提供名称和描述。
- 3.4 在 Service URL 字段中输入（或从外部源复制粘贴）以下 URL：
http://IP_address_of_Publisher:8080/emapp/EMAppContext?device=#DEVICENAME#.
- 3.5 您也可以选择添加 Secure Service URL（安全服务 URL）；如果两者都已配置且 IP 电话支持 HTTPS，将优先使用安全 URL。
- 3.6 确保勾选 Enable（启用）复选框。
- 3.7 您也可以选择选择 Enterprise Subscription（企业订阅）复选框。这将自动订阅所有支持服务订阅的 EM 服务；管理员不需要手动为每个设备添加该服务。

图 11-1 显示服务配置页面。

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_323_0.png)

图 11-1 Extension Mobility 服务配置

### 步骤 4：创建默认设备配置

- 4.1 在 CM Administration Web页面中，导航至 Device（设备） > Device Settings（设备设置） > Default Device Profile（默认设备配置）。
- 4.2 点击 Add New（新建）。
- 4.3 选择 Product Type（产品类型，即电话型号）和 Device Protocol（设备协议）。

可用设置取决于所选电话型号和协议。您可以选择 Phone Button 和 Soft Templates（电话按钮和软模板），但无法配置 DN（目录号码）或其他特定的电话按钮设置。图 11-2 显示默认设备配置页面。

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_324_0.png)

图 11-2 默认设备配置配置

### 步骤 5a：创建设备配置

- 5.1 导航至 Device（设备） > Device Settings（设备设置） > Device Profile（设备配置）。
- 5.2 点击 Add New（新建）。
- 5.3 为特定用户的电话选择型号和协议。
- 5.4 为配置输入一个名称。
- 5.5 配置用户特定设置，包括 DN、按钮自定义和其他参数。

图 11-3 显示设备配置配置页面。

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_325_0.png)

### 11-3 设备配置页面

### 步骤 5b：将设备配置订阅到 EM 服务

- 5b.1 在 Device Profile 页面，从 Links 下拉列表中选择 Subscribe/Unsubscribe Services（订阅/取消订阅服务）并点击 Go。
- 5b.2 选择步骤 3 中添加的 EM 服务并点击 Next（下一步）。
- 5b.3 输入 EM 服务的显示名称，如果低分辨率显示电话需要，还输入 ASCII 版本。
- 5b.4 点击 Subscribe（订阅），然后点击 Save（保存）。

**注意：** 如果在步骤 3 中勾选了 Enterprise subscription 复选框，则不需要执行步骤 5b。

图 11-4 释了此过程。

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_326_0.png)

图 11-4 将设备配置订阅到 EM 服务

注意：您必须将设备配置和 IP 电话都订阅到 EM 服务。如果不这样做，用户登录后将无法访问 EM 服务且无法注销。

### 步骤 6：将用户与设备配置关联

- 6.1 导航至 User Management（用户管理） > End User（终端用户）。
- 6.2 选择要创建配置的用户，或者在必要时创建一个新用户（参见第 9 章“管理终端和终端用户”）。
- 6.3 在用户配置中，选择应与之关联的设备配置。如果分配了多个，用户在登录 EM 后必须选择其中一个。默认配置会将选定的配置放在列表顶部。

图 11-5 释了将终端用户与设备配置关联。

![](img/e4ad7862dc47b4e5de0cde3b427.png)

图 11-5 将终端用户关联到设备配置

### 步骤 7a：为电话启用 EM

- 7a.1 导航至 Device（设备） > Phone（电话），选择您要配置 EM 的电话。
- 7a.2 在 Extension Mobility 部分，勾选 Enable（启用）框。
- 7a.3 在 Log Profile 下拉列表中选择特定的设备配置或当前配置的设备（推荐）。

注意：Log Profile 是登录电话时应用到电话的配置。此配置通常包含紧急、分机和有时本地呼叫功能。

图 11-6 显示了用于 EM 的电话配置。

### 步骤 7b：将电话订阅到 EM 服务

- 7b.1 在电话配置中，从 Related Links（相关链接）下拉列表中选择 Subscribe/Unsubscribe Services（订阅/取消订阅服务），打开 Subscribed Phone Services 窗口（如果在 EM 服务页面中勾选了 Enterprise Subscription 复选框，则无需此操作）。
- 7b.2 在 Select Service 下拉列表中选择 EM 服务。
- 7b.3 输入希望在 IP 电话上显示的服务名称。

![](img/e4ad7862dc47b4e5de0cde3b4550ad328.png)

图 11-6 为电话配置 EM

您应该能够进入任何订阅了 EM 服务且配置了该类型设备配置的电话并登录。

图 11-7 释了将 EM 服务到电话。

![](img/e4ad7862dc47b4e5de0cde3b4550ad329.png)

图 11-7 将电话订阅到 EM 服务

## 描述 CUCM 中的电话功能

CUCM 支持广泛的电话功能。本节回顾了一些广泛使用的功能，包括多种 Call Coverage（呼叫覆盖）、Intercom（分机）和 Presence（状态）。

### Call Coverage（呼叫覆盖）

Call Coverage 是一个通用术语，指的是用于确保在意外情况下接听电话的功能和机制。CUCM 支持以下 Call Coverage 功能：

- Call Forward（呼叫转移）
- Shared Lines（共享线路）
- Call Pickup（摘号）
- Call Hunting（呼叫寻路）

### Call Forward（呼叫转移）

CUCM 可配置多种 Call Forward 选项：

- Call Forward All (CFA)：CFA 将所有通话转移到用户或管理员在电话本身或 CUCM 管理页面上指定的号码，而无需响铃原始拨号号码。启用 CFA 时，将使用 Call Forward Search Space（呼叫转移搜索空间）并忽略线路/设备搜索空间。因此，在使用 Custom Partitions（自定义分区）和 Search Spaces 的系统中，应配置 Call Forward Search Spaces 以避免呼叫失败。

注意：如果勾选了 Voice Mail（语音箱）复选框，CUCM 将忽略转移设置和 Search Space 字段中的目标，并将通话转移到配置的 Voice Mail Profile 中的 Voice Mail Pilot 号。

### Shared Lines（共享线路）

如果两个或多个 IP 电话的线路配置了相同的 DN，拨打该 DN 会导致两个电话响铃。第一个接听的电话通话；第二个电话在不调用 Barge（插会）功能的情况下无法接听通话。如果第一个电话挂起通话，第二个电话可以接听挂起的通话。

### Barge and Privacy（插会与隐私）

如果两个电话配置了共享线路，且其中一个电话正在使用该线路，第二个电话可以使用 Barge 功能强制与第一个电话建立三方会议。会议在第一个电话的内置会议桥接上进行（对于不支持内置桥接的 IP 电话型号，可以配置外部会议桥接）。当第二个电话插会通话时，所有参与方都会听到蜂鸣声（默认）。如果插会失败（通常是缺少会议资源），插会电话将显示错误消息。

可以配置 Privacy（隐私）软键，启用后可防止插会正在进行的通话。Barge 和 Privacy 功能都可以在整个集群范围内以及单个电话配置页面上启用或禁用。

### Call Pickup（摘号）

DN 可以是 Call Pickup Group（摘号组）的成员，这仅仅是一个编号分配。可以使用这些摘号组分配配置三种类型的 Call Pickup：

- Call Pickup（摘号）：如果多个 DN 具有相同的组号，且其中一个正在响铃，同一摘号组内具有 DN 的另一个电话可以调用 Call Pickup 软键，通话将立即转接到该电话
- Group Call Pickup（组摘号）：如果两个 DN 属于不同的 Call Pickup Groups 且其中一个正在响铃，另一个电话可以调用 GPicup（组摘号）软键，拨打响铃 DN 的组号，通话将立即转接到该电话。该功能的一种变体 Directed Call Pickup（定向摘号）允许用户输入正在响铃的特定 DN 来接听该特定通话，而不是组内开始响铃的第一个通话。

