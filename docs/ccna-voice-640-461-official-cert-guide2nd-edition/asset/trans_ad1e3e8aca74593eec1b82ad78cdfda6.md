
必须激活会议桥（在大多数 IP 电话型号上可用）。隐私功能会从所有共享线路的电话中移除通话信息，并阻止其他共享线路插入其通话。以下步骤描述了如何配置插入（Barge）。

- 1. 在 CM 管理中，导航到 System > Service Parameters（服务参数）。从 Server 下拉菜单中选择您要配置的服务器。
2. 从 Service 下拉菜单中选择 Cisco CallManager 服务。
3. 滚动到 Clusterwise Parameters (Device-Phone) 部分。找到 Built-in Bridge On（内置桥接开启）。
4. 将 Privacy Setting（隐私设置）设置为 True（默认值）。

**注意：** 根据需要，可以在设备池（Device Pool）或单个电话上覆盖 Built-in Bridge、Privacy 和 Single Button 设置。

- 5. 滚动到 Clusterwise Parameters (Feature-Join Across Lines And Single Barge Feature Set) 并设置 Single Barge/CBarge Policy（单线插入/CBarge 策略）。您的选项有 Off、Barge、CBarge。此设置允许按下共享线路按钮在线路正在使用时触发对该线路的插入（而不是使用软键）。将值设置为 Barge 将使用目标电话上的内置桥，而将其设置为 CBarge 则强制插入操作使用外部会议资源。图 11-10 显示了配置 Barge 的 Clusterwise Parameters。

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_335_0.png)

**注意：** 使用插入软键方法需要您配置软键模板，以为参与插入操作的电话包含 Barge 软键。使用单按钮插入方法则不需要。
如果需要 CBarge，则必须配置外部会议资源并供电话使用。

## 配置呼叫接听（Call Pickup）

要配置呼叫接听，您必须创建 Call Pickup Groups（呼叫接听组）并将其应用于必须互相接听通话的 DN。按照以下步骤操作：

- 1. 在 CM 管理中，导航到 Call Routing > Call Pickup Groups。
2. 点击 Add New（新建）。
3. 输入名称和唯一号码。（该号码不能包含通配符）。
4. 选择一个 Partition（分区；通常与 DN 分区相同；但是，如果需要，选择不同的 Partition 允许管理员通过修改电话的 CSS 来限制对接听组的访问）。

可以预先配置相关的 Call Pickup Groups，以便在需要时使用 Other Group Pickup（其他组接听）功能（前所述）；此选项仅在接听组的初始配置期间可用。图 11-11 显示了 Call Pickup Group 配置页面。

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_336_0.png)

**图 11-11** 呼接听组配置

要使用接听功能，必须在电话上添加软键。以下步骤概述了修改和添加软键模板以启用呼叫接听的过程：

- 1. 要配置软键模板，导航到 Device > Device Settings > Softkey Template。
- 2. 选择、添加或复制软键模板。
- 3. 从 Related Tasks（相关任务）下拉菜单中选择 Configure Softkey Layout（配置软键布局）。
- 4. 根据需要添加 Pickup、Group Pickup 或 Other Group Pickup 软键。这些键可以在 Off Hook（摘机）或 On Hook（挂机）通话中选择。
- 5. 保存。
- 6. 根据需要将修改后的软键模板应用到电话或 Device Profiles（设备配置文件）。

图 11-12 显示了配置了 On Hook 通话状态选项的软键配置页面。

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_337_0.png)

## 图 11-12 为插入配置软键模板

要使用接听功能，个别 DN 必须与我们配置的 Call Pickup Groups 关联。DN 使用 Pickup 功能接听对方的通话；如果它们的 Call Pickup Groups 已预先关联，具有不同接听组的 DN 可以 Group Pickup 或 Other Group。图 11-13 阐了 DN 与 Call Pickup Group 的关联。

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_338_0.png)

图 11-13 DN 与呼叫接听组的关联

## 配置呼叫寄存（Call Park）和定向呼叫（Directed Call）

Call Park 功能允许用户将通话寄存在 DN 处，Directed Call（定向呼叫）也类似。要配置 Call Park，请按照以下步骤操作：

- 1. 在 CM 管理中，导航到 Call Routing > Call Park。
2. 点击 Add New。
3. 输入名称。
4. 选择一个 Partition。
5. 设置 Parked Timeout（寄存超时，通话在重定向之前保持寄存状态的秒数）。
6. 指定 Park Prefix（寄存前缀，用于取回寄存通话的代码）。
7. 点击 Save。

Directed Call 允许在特定 DN 可用将通话转发到那里。要配置 Directed Call，请按照以下步骤操作：

- 1. （参考 Call Park 的类似配置步骤）。

图 11-14 显示了 Call Park 配置。

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_339_0.png)

要配置 Directed Call，请按照以下步骤操作：

- 1. 在 CM 管理中，导航到 Call Routing > Directed Call。
2. 点击 Add New。
3. 输入名称。
4. 选择一个 Partition。
5. 设置 Directed Call Timeout（定向呼叫超时，等待接收者接主的秒数）。
6. 指定 Directed Call Prefix（定向呼叫前缀，取回定向呼叫的代码）。
7. 点击 Save。

图 11-15 显示了 Directed Call 配置。

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_340.png)

## 配置呼叫寻（Call Hunting）

要配置 Call Hunting，DN 组与指定寻呼行为的 Line Groups 关联；Line Groups 与 Hunt Lists 关联，Hunt Pilot 作为拨号数字。要配置 Call Hunting，请按照以下步骤操作：

创建 Line Groups

- 1. 在 CM 管理中，导航到 Call Routing > Line Group。
2. 添加 DN 并与电话关联。
3. 输入 Line Group 名称。
4. 指定 RNA Timeout（无应超时，Line Group 中每个 DN 响铃的秒数）。
5. 选择 Distribution Algorithm（分配算法）：
    - Top Down（自上而下）：每次新通话从列表顶部的 DN 开始。
    - Circular（循环）：每次新通话从上一次通话使用的下一个下一个 DN 开始。
    - Broadcast（广播）：Line Group 中所有 DN 同时响铃。
    - Long Idle Time（长时间空闲）：处于 Hook 状态最长的 DN 响铃。
6. 为每个通话状态选择 Hunt 选项（无应、空忙和不可用）。Hunt 选项决定通话何时以及何时从当前 Line Group 移动到 Hunt List 中的下一个 Line Group。
7. 向 Line Group 添加 DN。
8. 点击 Save。图 11-16 显示了 Line Group 配置。

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_341_0.png)

创建 Hunt Lists

- 1. 在 CM 管理中，导航到 Call Routing > Hunt List。
2. 点击 Add New。
3. 指定一个名称。
4. 设置 CUCM Group 以提供 CUCM 冗余。
5. 点击 Save。
6. 将 line groups 添加到 Hunt List。Hunt List 始终自上而下处理，因此 Line Groups 的顺序非常重要。
7. 点击 Save。

创建 Hunt Pilot

- 1. 在 CM 管理中，导航到 Call Routing > Hunt Pilot。
2. 点击 Add New。
