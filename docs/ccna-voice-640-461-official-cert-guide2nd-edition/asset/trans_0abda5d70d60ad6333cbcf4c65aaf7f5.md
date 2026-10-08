
图 13-16 显示了 LDAP 目录配置页。

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_400_0.png)

图 13-16 LDAP 目录配置页

## CUC 用户批量管理导入

使用批量管理工具（Bulk Administration Tool）导入用户是创建多个账户的一种快速方便的方法，前提是所需的用户可以格式化为 CSV 文件。要导入用户，请按照以下步骤操作：

1. 导航到 工具 > 批量管理工具 (Bulk Administration Tool)。
2. 在选择操作 (Select Operation)下，选择创建 (Create)。（注意，你也可以选择更新 (Update)、删除 (Delete) 或导出 (Export)。）
3. 在选择对象类型 (Select Object Type)下，选择带邮箱箱的用户 (Users With Mailbox)。
4. 在创建用户账户时覆盖 CSV 字段 (Override CSV Fields When Creating User Accounts)下，选择用户模板：是 (User Template Yes)并选择所需的模板 (Template)。
5. 在选择文件 (Select File)下，浏览并包含用户导入信息的 .csv 文件。
6. 指定一个失败文件名 (Failed Filename)。
7. 点击提交 (Submit)。

**注意：** .csv 的格式对于导入成功至关重要。获取格式正确的文件最简单的方法是对单个用户执行 BAT 导出（BAT Export）。生成的 .csv 文件将包含正确创建导入文件所需的所有信息。

选择你想要移动的用户，选择要将其移动到的数据库，并点击**移动已选邮箱箱 (Move Selected Mailboxes)**。

## 第 13 章与 Cisco Unity Connection 373 的语音信箱集成

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_402_0.png)

图 13-18 编辑邮箱箱存储页

## 消息老化策略

默认的消息老化策略（Message Aging Policy）会在 15 天后删除已删除项目（Deleted Items）文件夹中的项目。要修改此策略，请导航到消息存储 (Message Storage) > 消息老化策略 (Message Aging Policy)，然后选择默认系统策略 (Default System Policy)。（注意，如果你需要，可以创建自定义的老化策略。）你可以通过取消勾选启用 (Enabled) 复选框来禁用该策略；默认是启用的。你还可以选择修改以下内容：

- 在根据最后修改时间的消息老化规则（Message Aging Rules Based on When the Message Was Last Modified）下，选择是否将新消息移动到保存 (Saved) 文件夹，将保存的消息移动到已删除项目文件夹，以及每个规则的天数。
- 在根据消息创建时间的安全消息老化规则（Secure Message Aging Rules Based on When the Message Was Created）标题下，你可以选择永久删除安全消息或删除达到特定时长的所有安全消息。

图 13-19 显示了默认系统策略的消息老化页。

## 邮箱配额

在部署早期设置邮箱大小限制是一个好主意。要开始，请导航到消息存储 (Message Storage) > 邮箱配额 (Mailbox Quotas)。在这里，你可以更改全局邮箱配额（System-Wide Mailbox Quotas），包括警告（Warning）、软限制（Soft）和发送/接收（Send/Receive）阈值。这些配额可以在用户模板中或按用户单独进行覆盖。

图 13-20 显示了全局邮箱配额页。

## CCNA 语音 640-461 官方认证指南

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_403_0.png)

图 13-19 消息老化策略

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_403_1.png)

图 13-20 全局邮箱配额页

## 考试准备任务

## 复习所有关键主题

回顾章节中最重要的主题，这些主题在页外边角用关键主题图标标记。表 13-3 描述了这些关键主题，并标识了它们所在的页码。

表 13-3 Cisco Unity Connection 语音信箱集成关键主题

| 关键主题元素 | 描述 | 页码 |
| :--- | :--- | :--- |
| 段落 | 使用 SCCP CUC 与 CUCM 集成 | 347 |
| 段落 | 话路路由 | 350 |
| 关键概念框 | CUC 中的 CoS | 353 |
| 段落 | 分机和呼叫转移选项 | 355 |
| 段落 | 用户创建选项 | 356 |
| 段落 | 配置 CUC 端用户 | 365 |
| 段落 | 在 CUC 中导入端用户 | 367 |
| 段落 | 从 LDAP 导入用户 | 368 |
| 段落 | CUC 用户批量管理导入 | 371 |

## 关键术语定义

定义本章的以下关键术语，并在词表中检查你的答案：集成 (integration)、呼叫处理程序 (call handler)、服务类别 (CoS)、XML 扩展分号 (AXL)、话路路由规则 (call routing rules)。

本章包含以下主题：

- 描述 Cisco 统一存在功能（Cisco Unified Presence Features）：本节讨论了 Cisco 统一个人通信器（Unified Personal Communicator）及其功能、工作模式和协议利用。还回顾了 Cisco 统一通信管理器 IP 服务和 IP 电话消息程序的基本功能。
- 描述 Cisco 统一存在架构（Cisco Unified Presence Architecture）：本节识别了与 CUPS 集成其他统一通信应用和功能相关的协议和交互。描述了桌面模式和软电话模式下的 Cisco 统一个人通信器呼叫流程，以及法规合规性和服务质量（QoS）考量。
- 启用 Cisco 统一存在（Enabling Cisco Unified Presence）：本节回顾了配置端用户所需的步骤，使其能够在桌面电话控制模式或软电话模式下使用 Cisco 统一个人通信器。

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_405_0.png)

## 启用 Cisco 统一存在支持

Cisco 统一存在服务器 (CUPS) 扩展了统一管理器的原生功能，提供了多种通信方法和状态。本章简要描述了 CUPS 的部署考量。

启用 Cisco 统一存在：本节回顾了配置端用户所需的步骤，使其能够在桌面电话控制模式或软电话模式下使用 Cisco 统一个人通信器。

Cisco 统一存在（Cisco Unified Presence）

Cisco 统一存在服务器 (CUPS) 扩展了统一管理器的原生功能，提供了多种通信方法和状态。本章简要描述了 CUPS 的部署考量。

启用 Cisco 统一存在：本节回顾了配置端用户所需的步骤，使其能够在桌面电话控制模式或软电话模式下使用 Cisco 统一个人通信器。
