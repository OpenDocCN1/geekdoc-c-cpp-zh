

- 消息已发送：CUC 为每条消息添加了时间戳。
- 发送者 ANI：CUC 为外部叫者的消息添加 ANI。
- 消息时长：CUC 播每条消息的长度。

图 13-10 显示了回放设置的部分。

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_393_0.png)

图 13-10 用户模板：回放设置

# 通知设备

消息通知不应与 MWI（视觉信箱指示）混淆；通知是指 CUC 给用户拨打电话或发送电子邮件，告知其其有新消息。CUC 默认支持通过传真机、工作电话、家用电话、手机以及 SMTP 进行通知。可以添加额外的通知设备。

对于每个设备，根据需要执行以下操作：

- 启用：勾选此框以允许 CUC 向此设备发送通知。
- 显示名称：根据需要修改名称。
- 首次通知事件之前的延迟：设置 CUC 在使用此设备发送通知之前等待新消息的分钟数。
- 通知重复间隔：CUC 重新发送通知的频率。
- 通知我：勾选复选框允许 CUC 对所有消息、语音消息、传真消息、日历安排、日历会议进行通知，对于每种类型，仅发送紧急消息。

- 传真机/电话设置：设置 CUC 应拨打的电话号码。修改设置以编辑数字、等待时间等，以确保通话正确完成。所有这些设置都应应用于单个用户账户，而不是模板。

# 配置 CUC 端用户

向 CUC 添加用户可以手动完成（一次一个）、通过从 CUCM 或 LDAP 导入，或通过使用批量管理工具 (BAT) 完成。在每种情况下，目标都是为每个用户提供单独的信息，以完成之前配置的不同用户模板所提供的公共信息。

在接下来的章节中，为了与 Cisco 的相关性，省略了一些可能的配置步骤。

# 手动流程

要手动创建新用户，导航到 *Users > Users* 并创建用户。选择适当的 *User Type*（通常是带有信箱的用户）并选择或输入以下内容：

1. 从“基于模板”下拉菜单中，选择适用于此用户的适当用户模板以提供公共配置。

2. 添加 *Alias*（必须是唯一的）、*First Name*（名）、*Last Name*（姓）和 *Display Name*（显示名称）。

3. 如果在使用多个，请选择适当的 Mailbox Store（信箱存储）。

4. 添加用户的 *Extension*（分机号），这通常是与其 IP 电话关联的主 DN。

5. 点击 Save。

图 13-11 显示了用户配置基础页面的部分。

# 备用分机和名称

为用户提供备用分机（Alternate Extension），允许他们从主分机以外的号码拨入 CUC，并在不通过开场欢迎的情况下访问其信箱。以下步骤概述了备用分机的配置：

1. 在用户配置页面中
2. 从下拉菜单设置 *Type of Phone*（工作、家庭、手机）。
3. 提供 *Display Name*（显示名称）。
4. 设置正确的 *Phone Number*（电话号码）。这是电话在 CUC 中显示的呼叫 ID (ANI) 号码；通常，这是完整的 PSTN 号，但请注意 CUCM 可能会在发送到 CUC 之前剥离或修改数字。

图 13-12 显示了备用分机页面。

5. 从 *Edit menu*（编辑菜单）中选择 Alternate Names（备用名称）。

# 366 CCNA Voice 640-461 官方认证指南

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_395_0.png)

图 13-11 用户配置基础

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_395_1.png)

图 13-12 用户配置：备用分机

备用名称（Alternate Name）允许管理员定义昵称、常用名称或音标拼写，允许呼叫者通过用户页面主配置中以外的名称搜索用户。例如，如果 Jedediah 是名字条目，但呼叫者因为那是他的昵称而搜索 J.D.，管理员可以添加 J.D. 的备用名称，如果使用了语音识别，甚至可以添加 Jaydee。

# 私有列表

管理员可以代表用户添加私有列表 (Private DLs)，或者用户可以从他们的个人通信助手 (PCA) 网页中添加。（注意，管理员界面也会以用户身份登录打开 PCA）。每个列表（最多可以创建 99 个）都需要唯一的名称，并可以包含最多 99 个成员。这些最大值在 CoS 中受到限制。

图 13-13 显示了私有列表的 PCA 视图。

img/e4ad7862dc47b4e5de0cde3b4550ad65_396_0.png)

图 13-13 PCA：私有列表

# 将端用户导入 CUC

执行用户导入是在 CUC 中创建用户账户最快最简单的方法之一。通过使用完全配置的用户模板，创建用户的工作将更快更准确。取决于实现情况，如果用户账户与另一个系统同步，可能会产生额外收益，从而减少与用户维护相关的管理任务的重复。

> 关键主题

# 从 CUCM 导入用户

使用完全配置的用户模板，创建用户的工作将更快更准确。取决于实现情况，如果用户账户与另一个系统同步，可能会产生额外收益，从而减少与用户维护相关的管理任务的重复。

> 关键主题

# 从 CUCM 导入用户

如果 CUCM 已经有了完全填充的用户数据库，执行以下操作以同步：

1. 在 Unified Service 界面下，导航到 Tools。
2. 选择 Service 并点击 Save。
3. 在 CUC 管理界面下，导航到 Telephony。
4. 选择要导入的 CUCM 服务器。
5. 在 Edit 菜单下点击 AXL。
6. 在 AXL 设置的页面下，输入 CUC 用于读取和导入 LDAP 数据库的帐户和密码。
7. 点击 Save。
8. 在 AXL 部分，添加 New。
9. 输入 IP 地址和端口：CUC 使用的端口（支持 8443）。
10. 点击 Test 按钮进行测试。
11. 在 Status 部分完成 AXL 集成。

图 13-14 显示了 AXL 状态。

现在 AXL 正常工作，我们可以按照以下步骤使用它来导入用户：

1. 在 CUC 管理界面下，导航到 Users > Import。
2. 从下拉菜单中选择适当的用户模板。
3. 点击 Find。
4. 选择要导入的用户(s)，然后点击 Selected。

> 注意：CUCM 用户必须有主分机号。

# 从 LDAP 导入用户

LDAP 是一个基于标准的用户、密码和系统。CUC 可以从许多厂商的实现中导入用户。要启用同步，请执行以下步骤：

1. 在 Unified Serviceability 界面下，导航到 Services。
2. 选择 DirSync 服务并点击 Save。
3. 在 CUC 管理界面下，导航到 System Settings。
4. 勾选 Enable LDAP。
5. 从下拉菜单选择 LDAP Server Type。
6. 在 LDAP Attribute for User ID 中，选择映射到 CUC 别的 LDAP 属性。该属性必须包含唯一数据。
7. 导航到 LDAP > Directory Configuration。
8. 输入 LDAP Configuration Name。如果配置了多个 Search Base，建议使用标识正在导入用户的名称。
9. 输入 LDAP Distinguished Name 和 LDAP Password：这是 CUC 用于读取和导入 LDAP 数据库的帐户和密码。
10. 输入 LDAP User Search Base：此条目定义了 CUC 开始读取 LDAP 数据库的点。大多数 LDAP 设计是层次树形结构；CUC 从 User Search Base 指定的点开始搜索，并可以读取树的所有分支。它无法从该点向上移动，无法跨越其他分支。CUC 只能与单个 LDAP 数据库集成。

11. 在 LDAP Directory Synchronization 中，如果您不想让 CUC 执行定期同步，请选择 Perform Once。刷新更新当前用户信息；它不会导入同步以来创建任何新用户。必须执行新的 User Import 来在 CUC 中创建这些用户。
12. 要让 CUC 按定期计划同步，请按需要设置 Perform a Re-sync Every。
13. 要配置 LDAP 属性与 CUC 用户属性之间的映射，在 User Fields To Be Synchronized 部分设置所需值。根据所选 LDAP 类型/厂商，列出的字段会有不同。

# 备用分机

为用户提供备用分机（Alternate Extension），允许他们从主分机以外的号码拨入 CUC，并在不通过开场欢迎的情况下访问其信箱。以下步骤概述了备用分机的配置：

1. 在用户配置页面中
2. 从下拉菜单设置 *Type of Phone*（工作、家庭、手机）。
3. 提供 *Display Name*（显示名称）。
4. 设置正确的 *Phone Number*（电话号码）。这是电话在 CUC 中显示的呼叫 ID (ANI) 号码；通常，这是完整的 PSTN 号，但请注意 CUCM 可能会在发送到 CUC 之前剥离或修改数字。

图 13-12 显示了备用分机页面。

5. 从 *Edit menu*（编辑菜单）中选择 Alternate Names（备用名称）。

# 366 CCNA Voice 640-461 官方认证指南

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_395_0.png)

图 13-11 用户配置基础

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_395_1.png)

图 13-12 用户配置：备用分机

备用名称（Alternate Name）允许管理员定义昵称、常用名称或音标拼写，允许呼叫者通过用户页面主配置中以外的名称搜索用户。例如，如果 Jedediah 是名字条目，但呼叫者因为那是他的昵称而搜索 J.D.，管理员可以添加 J.D. 的备用名称，如果使用了语音识别，甚至可以添加 Jaydee。

# 私有列表

管理员可以代表用户添加私有列表 (Private DLs)，或者用户可以从他们的个人通信助手 (PCA) 网页中添加。（注意，管理员界面也会以用户身份登录打开 PCA）。每个列表（最多可以创建 99 个）都需要唯一的名称，并可以包含最多 99 个成员。这些最大值在 CoS 中受到限制。

图 13-13 显示了私有列表的 PCA 视图。

img/e4ad7862dc47b4e5de0cde3b4550ad65_396_0.png)

图 13-13 PCA：私有列表

# 将端用户导入 CUC

执行用户导入是在 CUC 中创建用户账户最快最简单的方法之一。通过使用完全配置的用户模板，创建用户的工作将更快更准确。取决于实现情况，如果用户账户与另一个系统同步，可能会产生额外收益，从而减少与用户维护相关的管理任务的重复。

> 关键主题

# 从 CUCM 导入用户

如果 CUCM 已经有了完全填充的用户数据库，执行以下操作以同步：

1. 在 Unified Service 界面下，导航到 Tools。
2. 选择 Service 并点击 Save。
3. 在 CUC 管理界面下，导航到 Telephony。
4. 选择要导入的 CUCM 服务器。
5. 在 Edit 菜单下点击 AXL。
6. 在 AXL 设置的页面下，输入 CUC 用于读取和导入 LDAP 数据库的帐户和密码。
7. 点击 Save。
8. 在 AXL 部分，添加 New。
9. 输入 IP 地址和端口：CUC 使用的端口（支持 8443）。
10. 点击 Test 按钮进行测试。
11. 在 Status 部分完成 AXL 集成。

图 13-14 显示了 AXL 状态。

现在 AXL 正常工作，我们可以按照以下步骤使用它来导入用户：

1. 在 CUC 管理界面下，导航到 Users > Import。
2. 从下拉菜单中选择适当的用户模板。
3. 点击 Find。
4. 选择要导入的用户(s)，然后点击 Selected。

> 注意：CUCM 用户必须有主分机号。

# 从 LDAP 导入用户

LDAP 是一个基于标准的用户、密码和系统。CUC 可以从许多厂商的实现中导入用户。要启用同步，请执行以下步骤：

1. 在 Unified Serviceability 界面下，导航到 Services。
2. 选择 DirSync 服务并点击 Save。
3. 在 CUC 管理界面下，导航到 System Settings。
4. 勾选 Enable LDAP。
5. 从下拉菜单选择 LDAP Server Type。
6. 在 LDAP Attribute for User ID 中，选择映射到 CUC 别的 LDAP 属性。该属性必须包含唯一数据。
7. 导航到 LDAP > Directory Configuration。
8. 输入 LDAP Configuration Name。如果配置了多个 Search Base，建议使用标识正在导入用户的名称。
9. 输入 LDAP Distinguished Name 和 LDAP Password：这是 CUC 用于读取和导入 LDAP 数据库的帐户和密码。
10. 输入 LDAP User Search Base：此条目定义了 CUC 开始读取 LDAP 数据库的点。大多数 LDAP 设计是层次树形结构；CUC 从 User Search Base 指定的点开始搜索，并可以读取树的所有分支。它无法从该点向上移动，无法跨越其他分支。CUC 只能与单个 LDAP 数据库集成。

11. 在 LDAP Directory Synchronization 中，如果您不想让 CUC 执行定期同步，请选择 Perform Once。刷新更新当前用户信息；它不会导入同步以来创建任何新用户。必须执行新的 User Import 来在 CUC 中创建这些用户。
12. 要让 CUC 按定期计划同步，请按需要设置 Perform a Re-sync Every。
13. 要配置 LDAP 属性与 CUC 用户属性之间的映射，在 User Fields To Be Synchronized 部分设置所需值。根据所选 LDAP 类型/厂商，列出的字段会有不同。

# 第 13 章：语音信箱集成

