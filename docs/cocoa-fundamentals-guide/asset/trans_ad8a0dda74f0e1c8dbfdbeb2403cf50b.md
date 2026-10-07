

# 第一章

## 什么是 Cocoa？

| 类 | 比较 |
| --- | --- |
| NSResponder Responder | 这些类扮演的角色几乎完全相同。它们是抽象类，定义了用于响应事件和管理响应者链的接口。主要区别在于，NSResponder 事件处理方法是为鼠标和键盘定义的，而 UIResponder 方法是为多点触（Multi-Touch）事件定义的。 |
| NSWindow Window | UI 类在类层次结构中的位置与 AppKit 中的 NSWindow 类不同；它是 UIView 的子类，而 AppKit 类继承自 NSResponder。在应用程序中，UI 的角色要受限得多，它同时也负责提供一个显示视图的区域，向这些视图分发事件，并在窗口和视图坐标之间进行转换。 |
| NSView View | 这些类在目的和方法集上非常相似。它们允许你管理和缩放视图、管理视图内容以及转换视图坐标。然而，UIView 设计使得视图对象天生具备动画能力。 |
| NSControl Control | 这两个类都为按钮和滑块等对象定义了一种机制，当这些对象被操作时，控制对象会向目标对象发送动作消息。由于事件模型的差异，这些类以不同的方式实现了目标-动作（target-action）机制。[目标-动作机制](#) |
| NSViewController Controller | 这两个类的作用正如其名称所示是为了管理视图。它们完成这一任务的方式不同。NSViewController 提供的管理依赖于绑定（bindings），这是仅在 Mac OS X 支持的技术，用于 iOS 应用程序模型中的模态和导航用户界面（例如由导航控制的视图）。 |
| UITableView Table | UITableView 继承自 NSControl，但 UITableView 并不继承自 UITextView。更重要的是，UITableView 对象支持多列数据；UITableView 每次只显示单列数据，因此其列表功能少于表格数据功能。 |

你发现的许多类之间存在一些差异。例如，UIKit 有 `UITextField` 和 `ILabel`，前者用于可编辑文本字段，后者用于非空文本字段的标签；通过 `UITextField`，你可以通过简单设置文本属性来创建两种文本字段。同样，`NSIndicator` 类创建的对象样式对应 `UIProgressIndicator` 和 `ProgressBar` 类的实例。

## Core Data

Core Data 是一个为管理对象图提供基础设施的框架，包括对多种文件格式的持久化存储的支持。对象图管理包含诸如撤销（undo）、重做（redo）、验证以及确保对象关系完整性等功能。对象持久化意味着 Core Data 将对象保存到持久化存储中，并在持久化层需要 Core Data 应用程序时将其提取——即对象数据归档的最终形式——范围从 XML 文件到 SQL 数据库不等。Core Data 非常适用于作为关系型数据库的前端，但任何 Cocoa 应用程序都可以利用它的功能。

Core Data 的核心概念是“管理对象”（managed object）。管理对象仅仅是一个由 Core Data 管理的模型对象，但它必须是 `NSManagedObject` 类的实例或其子类。你使用名为“管理模型”（managed model）的模式（schema）来描述 Core Data 应用程序中的管理对象。模型包含了应用程序管理对象（也称为实体 entities）的描述。每个描述指定了实体的属性、它与其他实体的关系，以及元数据（如实体名称和代表性类名）。

在运行的 Core Data 应用程序中，一个被称为“管理对象上下文”（managed object context）的对象负责管理一组管理对象。图中的所有管理对象都必须在管理对象上下文中注册。上下文允许应用程序向图中添加对象或从图中移除对象。它还会跟踪对管理对象所做的更改，管理对象上下文确保对象处于有效状态。当 Core Data 应用程序想要从外部数据存储中检索数据时，它向管理对象上下文发送“获取请求”（fetch request）——这是一个指定一组标准的对象。管理对象上下文在注册对象后，从存储器返回匹配请求的对象。

管理对象上下文还充当指向底层持久化存储（persistence store）Core Data 对象集合的网关。持久化栈（persistence stack）在应用程序中的对象和外部数据存储之间起到协调作用。持久化存储位于栈的底部。它们将外部存储（例如 XML 文件）中的数据与管理对象上下文中的对应对象进行映射。然而，它们并不直接与管理对象上下文交互。栈中持久化存储上方是持久化存储协调器（persistent store coordinator），它为一个或多个管理对象上下文提供外观，使得下方的多个持久化存储看起来像单一的聚合存储。图 1-10 显示了 Core Data 架构中对象之间的关系。

图 1-10 管理对象上下文和持久化栈的示例

![](img/0c5ea7638a6e08e6bdc6bc222975f6ee_51_0.png)

Core Data 包含了 `NSPistentDocument` 类，它是 `NSDocument` 的子类，有助于集成 Core Data 和文档架构。持久化文档对象创建自己的持久化栈和管理对象上下文，将文档映射到外部数据存储。`NSPistentDocument` 对象提供了 `NSDocument` 读写文档数据方法的默认实现。

## 带有 Cocoa API 的其他框架

作为标准安装的一部分，Apple 除了两个平台的核心框架外，还包含了一些提供 Cocoa 编程接口的框架。你可以使用这些辅助框架为你的应用程序提供所需的、非必需的功能。一些著名的辅助框架包括：

- Sync Services（仅限 Mac OS X）：使用 Sync Services 可以同步现有的上下文、日历、书签以及应用程序数据。你也可以扩展 Sync Services。
- Address Book（仅限 Mac OS X）：通过 Address Book，应用程序可以从数据库中访问事件信息并允许用户为日历创建事件。该框架还支持高效获取事件记录、事件通知以及与日历数据库的自动同步。
- WebKit（不支持 iOS）：WebKit 框架提供了一组类用于在窗口显示网页内容，并默认实现了跟随链接的功能。
- iAd（仅限 iOS）：此框架允许应用程序通过向用户展示广告来获取收益。
- Map Kit（仅限 iOS）：此框架允许将地图嵌入窗口和视图中。它还支持注释（annotation）、覆盖和反地理编码（reverse geocoding）。
- Event Kit（仅限 iOS）：通过 Event Kit 框架，应用程序可以从数据库访问事件信息并允许用户为日历创建事件。
- Core Motion（仅限 iOS）：Core Motion 处理来自设备加速度计陀螺仪（如果可用）的底层数据，并将其交给应用程序处理。
- Core Location（仅限 iOS）：Core Location 让应用程序定义设备当前的位置或朝向。应用程序也可以定义地理区域并监控用户何时越这些区域边界。
- Media Player（仅限 iOS）：此框架允许应用程序播放电影、音乐、音频播客和声书文件。它让应用程序访问 iPod 库。
- Preference Panes（仅限 Mac OS X）：使用此框架，你可以创建记录用户偏好的用户界面，无论是针对应用程序还是系统级的。
- Screen Saver（仅限 Mac OS X）：屏幕保护框架帮助你创建屏幕效果模块，这些模块可以通过系统设置进行加载。

