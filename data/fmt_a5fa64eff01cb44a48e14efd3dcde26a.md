
```
Warning Form submission failed. (User: K2DEMO\administrator, Form
Name:TipsTicks, IP:, Request:
http://2kdemo.local/_layouts/Postback.FormServer.aspx, Form ID:
urn:schemas-microsoft-com:infopath:TipsTicks--myXSD-2008-09-
T20-24-31, Type: DataAdapterException,Exception Message: The remote
server returned an error: (500) Internal Error.
System.Web.Services-->System.SoapException: The process cannot be started
oproject due to the following reason: 24408 K2:K2DEMO\administrator from
192.168.1.103:7 does not have rights to Start Process
TipsTicks\TipsIPProcProcess1
```

## 附录 A：K2 blackpearl 技巧与窍

2. 如果错误并非特定的 Forms Services 问题，如果可能，可以临时将表单库配置为使用 InfoPath 客户端而非 Web 浏览器，以获取更有意义的错误信息。与使用 Forms Services 时得到的“通用”错误不同，你将获得一个包含底层异常详细信息的对话框，如图 A-40 所示。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_905_0.png)

在此示例中，如果你向右滚动，将看到之前看到的在 SharePoint 日志中记录的相同的异常消息。

这种技术的优势在于，它不需要试图翻阅 SharePoint 日志来寻找异常。

## 自定义表单与 SharePoint 工作流集成

作者 Chris Geiger，K2 项目经理

我针对我们的 SharePoint 集成问过很多问题，但没有哪个问题的频率高于关于我们 SharePoint 集成工作流中表单的问题。在构建此类流程时，你可以选择使用几种不同类型的表单，自动生成 ASP.NET 页面。人们通常希望自定义这些页面的外观和感觉，超出向导中提供的预期。遗憾的是，这比你想象的要简单得多。

在运行 SharePoint 工作流集成向导时，确保你使用 ASP.NET 作为表单技术，并生成新的 ASP.NET 页面作为表单位置。对于过程的其余部分，按常常运行向导。构建流程后，转到文件系统中保存项目的地方。你会看到一个新目录，默认名为 `CSwebsiteWI`。在该目录中，你将看到 K2 blackpearl 为你生成的页面。你可以使用 Visual Studio 甚至 SharePoint Designer 打开这些文件中的每一个。一旦在你选择的编辑器中打开，你就可以添加图形、更改外观和感觉、添加其他字段、使用 K2 API 或几乎任何你需要的操作。太棒了，不是吗？

## 索引

### A

会计 (`accounting`)。参见审计 (`auditing`)

操作菜单 (`Action Menu`)

SharePoint K2 Web Designer，508

工作列表 (`Worklist`)，705

操作策略 (`action policies`), 事件总线 (`Event Bus`)，750

操作 (`actions`)

- 映射到 InfoPath，379–381
- 作为流程的构建块，27–28
- 在 InfoPath 中配置，360–362
- 内容基准，225
- 与事件分离，248
- 完成并更新 (`Finish and Update`)，288
- 获取在流程实例中执行的操作和用户列表，860–861
- 映射到元组 (`tuples`)，223
- 多插槽和，233
- 流程实例和，541
- 设置用户操作，224–226
- InfoPath 客户端事件向导的任务字段 (`Task field`)，357–359
- 任务项 (`task items`)，548
- 工作列表项 (`worklist items`)，704–706

高级的 (`advanced`),

- 概述，782
- 权限和，786–788
- 当操作和结果没有一对一匹配时，783

活动目录 (`Active Directory`)

- 与之集成，74–75
- Kerberos 要求和，79

活动目录安全 (`Active Directory security`)，610–614

- ADUM 设置，610–612
- 配置对多个域的支持，612–614
- 概述，610

活动目录 SmartObject (`Active Directory SmartObject`)

- 创建活动目录 SmartObjects，131–133
- `GetDetails` 方法，133–140
- `GetManagerDetails` 方法，140–141
- `GetUserInfoGroup` 方法，141–144

活动目录用户管理器 (`Active Directory User manager (ADUM)`)

- 配置对多个域的支持，612–614
- 安全设置，610–612

活动目录用户和组 (`Active Directory Users and Groups`)

- 角色和，260
- 用户浏览器 (`User Browser and)`，253

基于活动目录的身份认证 (`Active Directory-based authentication`)，593

活动 (`activities`)

- 添加到工作流，262–265
- 分配，271–273
- 编写 AS.NET 表单活动，411–414
- 通过重复 XML 元素确定用户，828–830
- 升级 (`escalations and)`，240
- 获取/设置 XML 字段的辅助类，866–867
- 连接工作流活动的线条，273–275
- 用于创建的鼠标手势，865
- 概述，207–208
- 查看 AS.NET 表单活动，418–420
- 工作流构造函数 (`Workflow Constructor`)，255
- 工作流实现和，259, 261

活动数据字段 (`activity data fields`)，261, 709

活动计划 (`activity plans`)，781–782

活动规则 (`Active Rules`)

- 目标规则 (`Deination Rule`)，230–237
- 升级规则 (`Escalation Rule`)，237
- “如何”以及，226–227
- 前置规则 (`Preceding Rule`)，222
- 开始规则 (`Start Rule`)，229–230
- 后续规则 (`succeeding Rule`)，237

活动计划 (`activity plans`)，262–263

活动向导 (`activity wizards`)

- 默认活动 (`Default Activity`)，262

默认活动 (`Default Activity`)，262

流程设计中的参与者识别 (`actors, identifying in process design)`，203

添加自定义事件向导 (`Add Custom Event`)，741

添加通知事件向导 (`Add Notification Event`)，738–741

事件管理 (`administration of Event`)，755

服务器管理 (`administration of servers`)

归档 (`archiving`)，549–550

BDC 选项，562

配置管理器 (`Configuration Manager`)，564–365

环境和 (`Environment and)`，532–536

管理控制台 (`Management Console and)`，528

概述 (`overview of)`，525

流程实例管理 (`process instance management`)，540–541

服务器组件管理 (`administration of components`)

服务器管理 (`administration, of servers`)

流程版本管理 (`process version management`)，541–543

报告数据源 (`report sources`)，556–558

角色 (`roles`)，536–738

运行时服务 (`Runtime Services`)，552–553

服务器架构 (`server architecture`)，525–527

SharePoint 组件 (`SharePoint components`)，558–561

SmartObject (`SmartObject`)，548–549

总结 (`summary`)，564–666

任务单元 (`Tasklet Web`)，563–564

工作流服务器 (`workflow server`)，528–530

工作列表 (`worklists`)，547–548

工作时间 (`working hours`)，534–540

工作区应用程序 (`Workspace applications`)，553–554

工作区日志 (`Workspace logging`)，553

工作区 Web (`Workspace Web`)，550–552

目标中的 SmartObjects (`SmartObjects in destinations`)，777–779

拆分合并场景 (`split and merge`)，792

操作和结果没有一对一匹配时，783–786

目标中的 XML 节点 (`XML nodes in destinations`)，779–781

应用程序池管理 (`application pool, managing`)，553

应用程序接口 (`application programming interfaces`)。参见 APIs (`application programming interfaces`)

应用程序日志级别 (`ApplicationLogLevel`)，日志文件部分，680

应用程序 (`applications`)

- 使用 K2 blackpearl 装饰，126
- 设计评审流程与 LOB 集成
- 动态业务，17–18
- 业务应用开发历史，18–19
- 流程感知 (`process-aware`)。参见 process-applications
- 流程设计，220
- SOX 合规场景，223
- 传统设计，14–15

应用程序，日志文件，概述，466

SharePoint 列表和库事件向导 (`SharePoint Lists and Libraries wizard`)，467

SharePoint 站点和事件向导 (`SharePoint Sites and Events wizard`)，466–467

SharePoint 用户管理事件向导 (`SharePoint User Management wizard`)，468–469

管理员组 (`Administrators group`)，607

ADO.NET 提供程序 (`ADO.NET providers`)，40

ADAM (`Active Directory Manager`)

配置对多个域的支持，612–614

安全设置 (`security settings`)，610

高级模式 (`Advanced Mode`)，目标规则向导，232

高级 (`advanced`)

- 高级设计流程。参见流程设计，
- 高级安全工具，607
- 高级设置
- 高级工作流，SharePoint，461

报警 (`alerts`)，700

“允许任何用户完成此事件”(`Allow Any User to Finish This Event`)，833–834

惊艳 K2 Spotlight (`Amazing K2 Spotlight`)，859–860

- InfoPath 集成 (`InfoPath Integration`)，355

SmartObjects。参见 SmartObjects, advanced

应用程序接口 (`API (application programming interfaces)`)

- 客户端 API (`client API`)，999
- 创建 SmartObjects 实例和，173–175
- 事件总线 (`Event Bus`)，748
- 扩展 K2 平台，42
- K2 API 中的命名空间和类，414
- 流程定义，498
- 安全提供者 API (`Security Provider API`)。参见 Security Provider API

应用程序访问请求流程 (`Application Access Request process`)

概述，775–777

操作的权限 (`rights on actions`)，178–788

# BPM 业务流程管理（续）

BPM（业务流程管理）（续）

- 概述，3–4
- 流程驱动型应用，9–10
- 总结，10–11
- 传统应用，14–15
- 什么是它，13–14
- 工作流和，5–6
- BPM 业务流程建模，19
- BPMS（业务流程管理），5
- BPR（业务流程重组，17）
- 基于浏览器的表单

    - 部署，297–396
    - 设计约束，395
    - InPath 中的表单，333, 338–339
    - 启动和执行工作流，457

- 构建工具，94
- 内置事件处理程序，748
- 业务活动监控，14
- 业务分析师

    - 用于 SharePoint 的 K2 Designer 和，505
    - 用于 Visio 的 K2 Designer 和，501
    - 流程设计规则，495–496
    - 项目角色，32

- 业务连续性计划（BCP），650。参见 DRP（灾难恢复计划）
- 业务数据目录。参见 BDC（业务数据目录）
- 智能，K2 blackpearl 的益处，45
- 业务智能（BI），MOSS，438
- 业务层，112–114
- 业务所有者角色，32
- 业务所有权，应用设计及，16
- 业务流程发现（BPD），17
- 业务流程管理。见 BPM（业务流程管理）
- 业务流程管理系统（BPMS），5
- 业务流程建模规范（BPMN），197
- 业务流程重组（BPR），17
- 业务生产力基础设施优化（BPIO），107
- 业务需求，35–36

    - 实体相关问题，36
    - 概述，35
    - 人相关问题，35
    - 流程相关问题，35
    - 收集所需的时间，17

- 业务用户。见

- 类别数据库，58
- 日志配置文件的 Category 部分，681–682
- 类别服务器，57
- 中央管理（Central Administration），MOSS，397
- SharePoint 中央管理，440
- 变更管理

    - 为了适应变化而构建的动态业务应用，18
    - 项目角色，33
    - 图表，699

- 交付物的检查点，34
- CIA 欺诈，569–571

    - 可用性，570–571
    - 机密性，569
    - 完整性，568–569

- K2 API 中的类，414
- 客户端 API，59
- 客户端组件，52–53

    - 用于 Visio 和 K2 Studio 的 K2 Designer，53
    - 用于 Visual Studio 的 K2 Designer，52

- 客户端事件向导，407
- 见激活的 InfoPath 客户端事件向导，237
- “允许任何用户完成此事件”833–834
- 等号（equals）中的默认结果，642–843
- 动态等号，848–849
- 表单，322–333

    - InfoPath，356–357
    - 概述，208–209
    - 每个定义的计划及，861–862
    - SharePoint，451
    - 类型，209–211

- 用于 SharePoint 工作流集成客户端事件的 URL，859
- 客户端层系统，87
- 客户端，InfoPath，351
- 集群

    - 用于大规模架构的集群，70
    - 与负载均衡对比，72
    - SQL Server 2005 灾难恢复选项，654

- 代码

    - ASNET 表单的益处，340
    - 创建 ASNET 表单工作流，411–414
    - 用于自定义服务提供程序，640–641
    - 使用代码部署，325–329
    - 作为代码的表单生成事件

        - 生成，335

    - 启动 ASNET 表单工作流，399–404
    - 使 K2 服务器，414–418
    - InfoPath 后置代码，338

- 冷备用，664

# C

- 缓存，未锁定的 SmartObjects，172–173
- CAML（协作应用程序标记语言），473, 477
- 流程定义目录，415–417
- 仪表板，设计评审过程和开发，18
- 应用程序中业务用户与 IT 部门的协作与通信及，521
- 协作设计师，40–41
- 创建机制，34
- 示例场景，538–519
- 角色识别和计划制定，519
- 用于 Studio 的 KV2 Designer，510
- 用于 Studio 的 KV2 Designer，515
- 用于 SharePoint 的 KV2 Web Designer，512
- 根据项目计划管理，519
- 源代码，519–521

# 协作应用程序标记语言（CAML），473, 477

- 集合响应定义，22
- 协作及，521
- 安全性，591–592
