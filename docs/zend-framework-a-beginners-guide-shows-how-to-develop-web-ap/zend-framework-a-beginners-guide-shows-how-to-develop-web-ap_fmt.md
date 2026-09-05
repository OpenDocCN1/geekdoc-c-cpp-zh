
# Zend Framework 初学者指南

展示了如何使用 PHP 和 Zend Framework 开发 Web 应用；涵盖 XML、Ajax 和 Web 服务；包含分步项目和代码示例。

## 前言

前言由 Matthew Weier O'Phinney 撰写。

Zend Framework 项目负责人。

## 本书内容

- 展示了如何使用 PHP 和 Zend Framework 开发 Web 应用
- 涵盖 XML、Ajax 和 Web 服务
- 包含循序渐进的项目和代码示例

> 关于 Zend Framework 组件的详细描述，以及如何用更少投入完成更多工作的价值提示和最佳实践。任何使用 Zend Framework 的人员的必读参考资料。
>
> ——Michelangelo van Dam，Zend Framework 顾问及 PHPB 董事成员

Vikram Vaswani

> 送给一直问“为什么？”的 Tonka，以及总是知道答案的 Farah。

# 作者简介

**Vikram Vaswani** 是 Melonfire（`http://www.melonfire.com/`）的创始人兼首席执行官，这是一家在开源工具和技术领域拥有专长的咨询公司。作为 Web 开发人员和产品经理，他拥有 12 年 PHP 和 MySQL 工作经验，并为企业内网、高流量网站和关键任务轻客户端应用程序创建并部署了多种 PHP 应用。

Vikram 是开源运动的热情支持者，通过其在 Zend Developer Zone 的定期专栏为社区定期贡献 PHP、MySQL、XML 及相关工具的文章和教程。

他是 IBM DeveloperWorks 针对 PHP 初学者的广受好评的 Zend PHP 101 系列的作者。他之前的书籍包括《MySQL: The Complete Reference》（`http://www.myphp-t.com/`）、《How to Do Everything with PHP & MySQL》（`http://www.everythingphpmysysql.com/`）、《PHP Programming Solutions》（`http://www.php-programming-solutions.com/`）以及《PHP: A Beginner’s Guide》（`http://www.php-beginners-guide.com/`）。

作为英国牛津大学的 Felix 学金奖获得者，Vikram 将对 Web 应用开发的兴趣与其他各种活动相结合。在没有构思统治世界的计划时，他通过读小说、看电影、打壁球、写博客来消遣自己，并警惕地留意史密斯探。

# 技术编辑

**Ryan Mauger** 是 Lupimedia（`http://www.upimedia.com/`）的首席开发人员，这是一家位于英国塞福克、专注于面向网站设计的多媒体机构。他是 Zend Framework 的忠实支持者和贡献者，经常在 IRC 上回答问题。Ryan 是一个父亲，喜欢钓鱼。了解更多关于他的信息请访问 `http://www.auger.co.uk`。

# 目录

- 创建默认模块 ........................................ 33
- 定义自定义路由 ................................................... 39
- 设置必填和默认值 ........ 65
- 获取并处理表单输入 ....................... 81
- 定义搜索表单 ................................................................... 174

## 理解异常 242

### 理解默认错误处理流程 246

### 使用自定义异常类 249

### 控制异常的可见性 251

尝试 8-1：创建一个自定义错误页面 252

## 记录日志数据 254

### 写入日志消息 254

### 在日志消息中添加数据 259

### 格式化日志消息 259

尝试 8-2：记录应用异常 263

### 定义日志位置 263

### 定义数据库日志写入器 264

### 更新错误控制器 265

总结 268

## 理解本地化与区域设置（Locales）272

### 设置应用区域设置 274

### 本地化数字 277

### 本地化日期和时间 279

### 本地化货币 282

### 本地化测量 285

### 本地化字符串 287

### 使用适配器和数据源工作 289

### 使用应用区域设置 291

### 使用翻译视图助手 293

尝试 9-1：本地化示例应用 294

### 设置应用区域设置 294

### 本地化数字和日期 294

### 定义字符串本地化目标 298

### 创建翻译源 300

### 注册翻译对象 302

### 支持手动选择区域设置 306

### 更新主布局 307

总结 309

### 理解新闻馈格式 313

### 消费新闻馈 313

### 创建新闻馈 317

### 访问 Web 服务 319

### 理解 Web 服务 319

### 消费 Web 服务 322

- 尝试 10-1：集成 Twitter 和博客搜索结果 ................................... 328
- 定义自定义路由 ..................................................................................................... 328
- 定义控制器和视图 ........................................................................................ 328
- 更新主布局 ................................................................................................ 331
- 创建基于 REST 的 Web 服务 ................................................................................ 332
- 理解 REST 路由 ................................................................................................ 332
- 尝试 10-2：实现基于 REST 的 Web 服务 ................................................. 334
- 创建新模块 ..................................................................................................... 334
- 定义控制器 ................................................................................................. 334
- 定义 GET 操作 ................................................................................................... 336
- 定义 POST 操作 ................................................................................................. 339
- 初始化 REST 路由 ................................................................................................ 340

总结 342

- 与结构工作 ................................................................... 346
- 理解页面和容器 ................................................................................ 346
- 渲染导航元素 ................................................................................ 351
- 尝试 11-1：添加导航菜单 ................................................................. 355
- 注册导航对象 ................................................................................. 357
- 创建导航操作 ................................................................................ 358
- 与 Dojo 工具包工作 ................................................................................ 361
- 处理 Dojo 数据 ........................................................................................ 361
- 使用 Dojo 视图助手 ................................................... 362
- 使用 Dojo 表单 ...................................................................... 365
- 尝试 11-2：添加 Dojo 自动完成小组件 ................................................ 368
- 更新表单 ................................................................................................. 368
- 初始化 Dojo 视图助手 ................................................................................ 369
- 更新主布局 ...................................................................... 370
- 尝试 11-3：添加 YUI 日历小组件 ........................................ 372
- 更新表单 ................................................................................................. 372
- 更新主布局 ...................................................................................... 374
- 更新控制器 ....................................................................................... 375
- 更新视图 ................................................................................................. 377

总结 378

- 分析性能 ................................................................................... 382
- 基准测试 ................................................................................................ 382
- 代码分析 ............................................................................................ 384
- 查询分析 ...................................................................................... 387

## 理解缓存操作 392

### 理解缓存前端和后端 395

### 使用缓存管理器 398

### 缓存 Doctrine 查询 399

### 优化应用代码 401

### 查询调优 401

### 懒加载 404

尝试 12-1：提高应用性能 405

### 配置应用缓存 405

### 缓存翻译字符串 406

### 缓存查询结果 406

### 缓存 Twitter 和博客馈 408

总结 410

# A 安装和配置所需软件 413

### 获取软件 414

### 安装和配置软件 416

### 在 UNIX 上安装 416

### 在 Windows 上安装 420

### 测试软件 426

### 测试 MySQL 426

### 测试 PHP 427

### 设置 MySQL 超用户密码 428

总结 428

# 前言

在过去的六年里，PHP 生态系统发生了巨大的变化。在 PHP 5 出现之前，我们这些 PHP 开发者主要是以临时的方式创建项目，每个项目都与前一个项目有所不同；如果我们留心，每个项目都会比前一个项目有所改进——但这并没有保证。虽然存在管理代码质量和标准的工具和实践，但它们仍处于成熟阶段，尚未被广泛使用。结果是，尽管 PHP 正在为网络上一些流量最大的网站提供支持，但将 PHP 作为构建稳定的、企业级应用程序的基础的想法曾受到广泛的嘲笑。



随着 `PHP 5` 的出现，我们开始更多地关注稳健的编程实践。通过修订和重构对象模型，我们现在有了一个坚实的基础来构建可重用的对象。像 `PHPUnit` 这样的工具利用对象模型，简化并实现了稳健的测试实践。这反过来导致了 `PHP` 应用生命周期中代码质量的关注日益增加。

`PHP` 框架正是从这个生态系统中开始兴生的。虽然有几个框架始于 `PHP 4`，但这一理念在 `PHP 5` 中大放异彩，少数框架在整个领域开始崛起。这些框架旨在为用户提供最佳实践，并为他们构建的应用程序提供重复、可重用的结构。

其中就 `Zend Framework`。根据其网站，`Zend Framework` 的使命非常简单：扩展 `PHP` 的艺术和精神，`Zend Framework` 基于简单性、面向对象的最佳实践、企业友好的许可协议以及经过严格测试的敏捷代码库。`Zend Framework` 专注于构建更安全、更可靠、更现代的 `Web 2.0` 应用程序和 Web 服务，并消费广泛使用的 API。

在书中，你将从一位作者那里学习 `Zend Framework` 如何实现这些目标，他既精通该领域，又是一位优秀且清晰的技术作家。你将获得详尽且易懂的解释以及完整的示例——并希望在读完书后，能够产生使用这一已成为行业事实标准的 `Zend Framework` 来开发你自己的应用程序的愿望。

> —Matthew Weier O'Phinney, Zend Framework 项目负责人

# 致谢

`Zend Framework` 是一项复杂的软件，关于它写一本书——正如我在过去八个月里发现的那样——并不是一项特别简单的任务。幸运的是，我在一个多元化且充满活力的人群帮助下完成了这一过程，他们每个人在将这本书交到你手中都发挥了重要作用。

首先，非常感谢我的妻子，她支持了我的整个过程，并确保我有一个舒适、无压力的工作环境。我非常确定，如果没有她的帮助，这本书永远不会走向世界。谢谢，亲爱的！

`McGraw-Hill` 的编辑和营销团队也值得在此感谢。这是我与他们合作的第六本书了，与他们合作非常愉快。收购协调员 Joya Anthony、编辑主管 Patty Mon 以及编辑 Jane Brownlow 和 Megan Morin 都引导了这手手稿的开发过程，并在将其从纸页变成你手中精美、专业的产品的过程中发挥了巨大作用。我要感谢他们的专业知识、奉献，以及代表我所做出的努力。

我还想对本书的技术编辑 Ryan Mauger 表以特殊表扬。Ryan 审阅了每一行代码，并运用他对 `Zend Framework` 的丰富知识，确保最终产品在技术上是可靠的，并反映了当前的最佳实践。感谢他在整个书籍写作过程中提供的帮助和建议。如果你正在寻找一位 `PHP` 专家，没有比他更好的选择了！

最后，为了让整个书籍写作过程比通常情况更加愉快，感谢：Patrick Quillen, Ian Fleming, Bryan Adams, Peter O'Donnell, MAD Magazine, Scott Adams, Gary Larson, VH1, Britney Spears, George Michael, Kylie Minogue, Buffy the Slayer, Farah Malegam, Stephen King, Shikhara, Anahita Marker, John le Carre, The Surtays, Barry White, Gwen Stefan, Ping Pong, Roberts, Robert B. Baker, Baz Luhmann, Jennifer Hudson, Mambo and Tito's, Easyjet, Humphrey Bogart, Taylor Pavilion, Wikipedia, Amazon.com, U2, Ubuntu, The Three Stooges, Pacha, Oscar Wilde, Hugh Grant, Alex Rider, Punch, Kelly Clarkson, Steven Turow, Slacklinux, Calvin and Hobbes, Yo Sushi, Blizzard Entertainment, Alfred Kropp, Otto, Pablo Picasso, Popeye and Olive Oyl, Dennis Leah, Trattoria, Dire Straits, Bruce Springsteen, David Mitchell, The West Wing, Wagamama, Santana, Rod Stewart，以及我家里及其他所有的朋友。

`Zend Framework` 确实是埃纳斯特·海明威所说的一场“流动的盛宴”。它被构想并实现为 `PHP` 开发者的一个健壮、功能丰富的组件库，允许你快速、高效地执行各种常见的应用程序开发任务，包括创建和验证表单输入、处理 `XML`、生成动态菜单、数据分页、处理 Web 服务以及更多更多！

然而，`Zend Framework` 最重要的贡献也许是它通过向 `PHP` 开发者引入更标准化、更结构化的 `PHP` 编程方法，推进了 `PHP` 开发的艺术。这种结构化的方法产生了更整洁、更易维护且更安全的应用程序，这也是越来越多的开发者从旧的“临时性”编程风格转向较新的基于框架的方法的关键原因之一。

但是，对于初级 `PHP` 开发者来说，`Zend Framework` 是一次向未知领域的惊险跳跃。模型-视图-控制器（`MVC`）模式、松耦合架构以及大量的可用组件通常有助于那些习惯于过程化代码的人消除这一过程神秘感。模型-视图-控制器（`MVC`）模式是一种通过分离业务逻辑、用户界面和数据来组织代码的设计模式。

松耦合架构意味着应用程序的不同部分可以独立进行开发和测试。这使得应用程序更容易维护和演进。`Zend Framework` 中大量的可用组件为开发者提供了广泛的工具，帮助他们快速地构建复杂的应用程序。

正如你从标题中猜到的样，《Zend Framework 入学者指南》面向对该框架的新用户。它假设你对 `PHP`、`HTML`、`CSS` 和 `JavaScript` 有一定的了解。如果你完全是编程新手，这本书可能并不最适合你。

- 第 9 章“理解应用本地化”讨论了 `Zend Framework` 中提供的各种工具，用于构建本地化、多语言应用程序，这些应用可以轻松地“移植”到不同的国家和地区。
- 第 10 章“处理新闻订阅和 Web 服务”讨论了如何使用 `Zend Framework` 生成和读取 `Atom` 或 `RSS` 新闻订阅；使用 `SOAP` 或 `REST` 访问第三方 Web 服务；允许开发者使用 `REST` 访问您的应用程序。
- 第 11 章“处理用户界面元素”讨论了如何通过菜单、面包屑导航和站点地图改进网站导航，还解释了 `Zend Framework` 与 `Dojo` 的集成，并提供了 `AJAX` 自动完成表单字段和弹出日历组件的示例。
- 第 12 章“优化性能”讨论了衡量和改进 Web 应用性能的各种技术，包括基准测试、压力测试、代码分析、缓存和查询优化。
- 附录“安装和配置所需软件”指导你完成在 `Windows` 和 `Linux` 上安装和配置 `Apache/PHP/MySQL` 开发环境的过程。

本书使用不同类型的格式来突出特殊建议。列表如下：

> 注意
>
> 关于该主题的额外见解或信息

> 提示
>
> 帮助你更好地完成工作的技巧或窍门

> 警告
>
> 需要注意的事

`Q`：常见问题，...

`A`：... 及其答案

在本书的代码列表中，粗体显示的文本是在提示符处要输入的命令。例如，在以下列表所示：

```text
mysql> INSERT INTO movies (title, myear) VALUES ('Rear Window', 1954);
Query OK, 1 row affected (0.06 sec)
```

加粗的行是在你在命令行提示符中输入的查询。你可以以此作为指南，尝试书中的命令。

你可以在本书讨论的示例应用程序的伴侣网站 `http://www.zf-beginners-guide.com/` 上找到其代码。代码归库按章节组织，可以直接下载并用于你的 `Zend Framework` 开发环境。

# 第 1 章：介绍 Zend Framework

# 第 2 章：Zend Framework：入门指南

## 核心技能与概念

- 学习基于框架开发的好处
- 理解 `Zend Framework` 的历史和独特进展
- 理解 `Zend Framework` 应用程序的结构
- 安装并开始使用 `Zend Framework`

毫不夸张地说，`PHP` 现在是世界上最流行的编程语言之一，也是全球数百万 Web 应用开发者的首选工具包。根据最近的统计，该语言已在超过 2200 万个网站和全球三个 Web 服务器上运行——这非同小事，尤其是考虑到 `PHP` 完全是由一个志愿者社区完全开发和维护的，没有任何没有任何商业背景支持！

`PHP` 流行的原因并不难理解。它具有可扩展性、易于获取，并且与第三方软件很好地协作。它使用清晰的语法并追求非混淆的代码，易于学习并鼓励快速应用开发。而且，它与商业编程工具包相比具有巨大优势，因为它在开源许可下，对包括 `UNIX`、`Microsoft Windows` 和 `Mac OS` 在内的各种平台和架构上都是免费的。

开发者对 `PHP` 表现出很高的满意度。在 Evans Data Corporation 于 2009 年 8 月对十种脚本语言的一项研究中，`PHP` 拥有最高的用户满意度（紧随其的是 `Ruby` 和 `Python` 用户）。特别是，`PHP` 在跨平台兼容性、工具的可用性和质量以及性能方面排名第一，在可维护性、可读性、可扩展性、易用性和安全性方面排名第二。

对于组织和独立开发者来说，所有这些事实归于一点：使用 `PHP` 可以节省金钱和时间。使用 `PHP` 构建应用程序成本低，因为这种语言可以用于多种用途，而无需支付许可费或投资昂贵的硬件或软件。使用 `PHP` 還在不牺牲质量的情况下缩短了开发时间，因为可以轻松获取现成的、健壮且经过社区测试的扩展，开发者可以使用这些扩展为语言添加新功能。

现在，乍看可能并不明显，`PHP` 深受推誉的易用性既有好处也有坏处。好处在于，不像 `C++` 或 `Java`，`PHP` 程序相对容易阅读和理解，这鼓励了初级程序员尝试这种语言并掌握基础知识，而不需要进行深入学习。坏处在于，`PHP` 相应的缺乏“严谨性”可能会某些程序员产生虚假的安全感，并鼓励他们在意识到代码质量、安全性和重用性必要标准的情况下，编写供公共消费的应用程序。

考虑到这一点，过去几年里，`PHP` 社区一直做出一致且而易见的努力，试图从即时的“随心所欲”编程转向更标准、面向框架的方法。这种方法不仅让从零开始构建 `PHP` 应用程序变得更容易，而且能产生更整洁、更一致且安全的应用程序代码。本章以及本书的其余部分将向你介绍这样一个框架——`Zend Framework`，它为严肃的开发者提供了一种灵活且可扩展的构建 `PHP` 应用的方法。

## 概述

用官方网站（`http://framework.zend.com/`）的话说，`Zend Framework` 是“一个使用 `PHP 5` 开发 Web 应用和服务的开源框架……基于简单性、面向对象的实践、企业友好的许可协议和经过严格测试的代码库。”它提供了一套完整的工具来构建和部署基于 `PHP` 的应用程序，并内置了用于安全、输入验证、缓存、数据库操作和国际化等常用函数的 API。

与许多其他框架不同，`Zend Framework` 使用了“松耦合”架构。简单来说，这意味着尽管框架本身由许多组件组成，但这些组件在很大程度上是独立的，彼此之间的链接非常少。这种松耦合架构有助于轻量级应用，因为开发者可以只选择任务所需的特定组件。例如，想要为应用程序添加身份验证或缓存的开发者可以直接使用 `Zend_Auth` 或 `Zend_Cache` 组件，而不需要框架的其他部分。

`Zend Framework` 提供了一个完整的模型-视图-控制器（`MVC`）模式实现，允许应用程序逻辑与用户界面和数据模型分离。这种模式适用于中等到复杂的应用程序，并常用于 Web 应用开发，因为它鼓励代码重用并提供了更易管理的代码结构。`Zend Framework` 对 `MVC` 模式的实现将在第 2 章详细讨论。

`Zend Framework` 由 `Zend Technologies` 创建并维护，这是一家商业软件供应商，其创始人 Andiman 和 Zee Suraski 还负责了 `PHP` 解析器的首次重大重写，并于 1997 年作为 `PHP 3.0` 发布。`Zend Framework` 的第一个版本 `v1.0` 于 2007 年 7 月发布，包含 35 个核心组件，包括缓存、身份验证、配置管理、数据库访问、RSS 和 Atom Feed 生成以及本地化。

从那时起，框架经历了多次迭代，最新版本 `v1.10` 现在包含超过 65 个组件，支持 Adobe 的动作消息格式（`AMF`）、Google 的 `GData API` 以及亚马逊的 `EC2` 和 `SQS` 服务。幸运的是，组件数量的增加也伴随着文档的相应增加——`Zend Framework v1.9` 手册（约 2009 年）的大小为 `3.7MB`，而 2007 年随 `Zend Framework v1.0` 发布的手册仅为 `780KB`。

尽管 `Zend Technologies` 在多个不同市场进行商业运营，但它将 `Zend Framework` 作为基于 `BSD` 许可证的开源项目向公众开放，允许在不支付许可费用的情况下将其自由用于专有商业产品。这种“对业务友好”的许可策略使得 `Zend Framework` 在企业用户和独立用户中广受欢迎。初创公司、财富富 500 强企业、独立开发者和 `PHP` 爱好者都是该项目的粉丝——截至编写时，`Zend Framework` 的下载量已超过 1000 万次，且有超过 400 个基于 `Zend Framework` 或其扩展的开源项目。

在邮件列表和 wiki 上，可以发现一个活力、热情的开发者社区正在交流 Bug 和技巧，在线手册和参考指南还提供了额外的支持。社区还鼓励开发者通过提交新组件向框架“回馈”——目前该项目有 500 多名独立贡献者——只要这些贡献符合 `Zend` 对文档和单元测试的要求即可。

你可能会想，为什么使用 `Zend Framework` 比你现在这样做的那样自己编写代码是一个更主主意？嗯，以下是一些原因。

## 标准合规与最佳实践

与其他某些编程语言不同，`PHP` 并不强制执行通用编码标准。结果，`PHP` 应用程序的编写方式在开发者之间存在显著差异，导致很难确保整个项目的一致性。`PHP` 相对缺乏“严谨性”也可能产生无法遵循最佳实践的代码，使其容易受到攻击。

相比之下，`Zend Framework` 整合了关于最佳实践的最新理念，提供了标准的布局，并为常见的开发任务（如输入验证和清理）提供了内置支持。因此，将其作为 `PHP` 项目的基础可以自动生成更高质量的代码，以及在安全问题上更具前瞻性的应用程序。此外，由于 `Zend Framework` 拥有完备的文档，晚些加入项目团队的开发者将拥有更短的学习曲线，并能够更快地开始为项目做出贡献。

## 可重用性

`Zend Framework` 是面向对象的，并利用了 `PHP 5.x` 中的新对象模型。这种面向对象编程（`OOP`）架构鼓励代码重用，允许开发者显著减少编写重复代码花费的时间。这一事实在 Web 应用中尤为重要，因为 Web 应用通常需要对其数据暴露多个接口。例如，假设你希望为应用程序现有的搜索功能添加一个 `XML` 接口。使用 `Zend Framework`，这只需定义一个新的视图，将控制器的输出重新格式化为 `XML` 即可，整个过程是透明且易于完成的。

## 国际化

作为一个旨在用于 Web 应用开发的项目，如果 `Zend Framework` 不包含对应用程序国际化和本地化的全面支持，那将是不寻常的。`Zend_Locale` 组件允许在应用程序级别对用户的本地区域进行控制；`Zend_Translate` 组件使得支持包含拉丁字母、中文和欧洲字符集的多语言应用程序成为可能。其他有用的组件包括 `Zend_Date` 和 `Zend_Currency`，用于本地化的日期/时间和货币格式化。

## 开源

`Zend Framework` 是一个开源项目。虽然该项目由 `Zend Technologies` 赞助，但大部分开发由全球志愿者团队负责，他们负责修复 Bug 和添加新功能。`Zend Technologies` 为项目提供方向，并配备了一组“大师工程师”，他们决定哪些内容进入最终产品。正如前面提到的，该框架可以在不支付许可费用或不投资昂贵硬件或软件的情况下使用。这在不影响灵活性或可靠性的情况下降低了开发成本。代码的开放性进一步意味着任何地点的任何开发者都可以检查代码、发现错误并提出可能的修复方案；这产生了一个稳定、健壮的产品，Bug 一旦发现就会在发现后的几小时内迅速解决！

## 社区支持

正在寻找将 `Flickr` 组件或 `Google Maps` 数据集成到应用程序中的方法？尝试 `Zend_Service_Flickr` 或 `Zend_Gdata` 组件。使用 `Adobe Message Format (AMF)` 与 `Flash` 应用程序通信？请使用 `Zend_Amf` 组件。要快速将 `RSS` 馈集成到你的应用程序中？`Zend_Feed` 拥有你的一切。

正如这些示例所示，像 `Zend Framework` 这样一个由社区支持的项目，其优点之一是可以接触到全球开发者的创造力和想象力。`Zend Framework` 由大量独立组件组成，开发者可以使用这些组件为他们的 `PHP` 项目添加新功能。使用这些组件通常比自己编写代码是更具时间和成本效益的替代方案。

## 独特优势

现在，有人可能会认为上述特性适用于所有 `PHP` 框架，而不仅仅是 `Zend Framework`。然而，`Zend Framework` 确实拥有一些使其在竞争中脱颖而出的特性。

### 松耦合

与框架各个部分之间紧密关联的其他框架不同，`Zend Framework` 的组件可以很容易地分离并“按需”使用。因此，虽然 `Zend Framework` 包含了构建现代、符合 `MVC` 标准的 Web 应用所需的一切，但它并没有强迫你这样做——你完全可以从各个库组件中提取它们并集成到你的非 `MVC` 应用程序中。这种松耦合有助于减少应用程序的占用，并为未来的变化保留留灵活性。

### 快速发布周期



Zend Framework 团队遵循激进的发布计划，平均每月发布一到三次。除了这些稳定版本外，还有预览版（previews）和候选版本（release candidates），它们用于让社区了解最终发布准备期间的预期。这些频繁的发布不仅是为了保持项目前进，还为了确保 Bug 能够尽快被发现和解决。开发者还可以从项目的 Subversion 仓库访问“前沿”代码。

### 单元测试策略

鉴于 Zend Framework 是一个处于持续开发的松耦合组件集，单元测试对于确保组件持续运行和代码库稳定至关重要。Zend Framework 拥有严格的单元测试策略，规定组件只有带有足够完整且可运行的测试集（使用 `PHPUnit` 框架编写）才能加入框架。该策略确保了版本之间的后兼容性，并使回归问题清晰可见。

### 代码生成工具

Zend Framework 包含一项“工具”功能，允许开发者以极小的努力启动一个新的 Zend Framework 项目。该功能实现为基于 `Zend Tool` 组件的命令行脚本，负责为新项目创建基础文件系统布局并填充初始的控制器、视图和操作。开发者可以使用此脚本作为方便的快捷方式，在开发进行过程中快速创建新对象。

### 市场信誉

Zend Framework 由 Zend Technologies 赞助，它是 PHP 领域最知名的软件公司之一。该公司为企业级使用生产多种商业产品，并在为 PHP 开发者创建成功创新的产品方面拥有长期记录，例如 Zend Server（用于业务关键应用程序的 PHP Web 应用）和 Zend Studio（用于 PHP 开发的集成 IDE）。Technologies 的客户包括 IBM、McAfee、FOX Interactive Media、Lockheed Martin、Salesforce.com、NASA 和加拿大电信；作为支持，Zend Framework 确保了市场上的即时信誉，并成为说服客户和/或高级管理转向框架开发时的有用工具。

### 第三方应用程序互操作性

Zend Technologies 作为企业级 PHP 解决方案领先供应商之一的市场地位，使其 Zend Framework 获得了广泛的行业支持。

## 第 1 章：Zend Framework 简介

原生支持第三方工具和技术，包括 Adobe Action Message Format (AMF)、Google Data APIs、Dojo Toolkit、Microsoft CardSpace 以及来自 Amazon、Yahoo!、Twitter、Flickr 和 Del.io.com 的 Web 服务。

并非如此。PHP 的优势之一一直是对各种数据库、文件格式和协议的支持。Zend Framework 通过其 `Zend_DB` 组件提供了通用的 API，用于访问 MySQL、PostgreSQL、Oracle 和 Microsoft SQL Server 等数据库；它还提供了用于 SMTP、IMAP 和 POP3 协议设计和接收信息的组件；使用 SOAP 和 REST 协议的 Web 服务；JSON 数据的编解码；Atom 和 RSS 格式的解析；以及创建和操作 PDF 文档。

Zend Framework 是“免费”的——用户可以根据 BSD 许可证条款免费下载和使用。同样，用户预计通过列表和 wiki 等社区工具自力支持。对于寻求更层次支持的公司和个人，Zend Technologies 提供了商业支持和培训包、来自 Zend 工程师的咨询服务，以及专有的 PHP 开发和部署工具，以帮助和优化 Zend Framework 的开发。对于许多商业机构来说，付费获取这些技术支持是选择 Zend Framework 作为其应用工具包的关键原因。此外还有 Zend Framework 认证计划，它提供了衡量个人 Zend Framework 技能的尺度，并在整个行业内被认为是个人 Zend Framework 能力的指标。

## 广泛的文档

Zend Framework 为核心发行版中包含的 60 多个组件提供了详尽的文档。这些文档包含一份超过 1000 页的程序员参考指南：面向经验丰富的开发者的“快速上手”指南；详细的 API 文档；视频教程；由知名 Zend 工程师制作的网络研讨会和播客。这些丰富的学习材料可以显著降低新手和资深程序员的学习曲线，事实上，这也是 Zend Framework 优于竞争性 PHP 框架的关键领域之一。

## 应用环境

所有的 Zend Framework 应用程序都是 PHP 应用程序，可以在任何支持 PHP 的环境中运行。该环境通常包含以下组件：

- 基础操作系统，通常是 Linux 或 Microsoft Windows。
- 一个 Web 服务器，通常是 Linux 上的 Apache 或 Windows 上的 Internet Services，用于拦截 HTTP 请求并直接提供服务或将其传递给 PHP 解释器执行。

![](img/222e7e58871b088cc6397852e1452b57_26_0.png)

**图 1-1** 典型 PHP 应用环境的组件

- 一个 PHP 解释器，用于解析并执行 PHP 代码，并将结果返回给 Web 服务器。

还有一个第四个可选但非常有用的组件：

- 数据库引擎，例如 MySQL 或 PostgreSQL，用于存储应用程序数据，接受来自 PHP 层的连接并修改或检索数据库的数据。

图 1-1 展示了这些组件之间的交互。

值得注意的是，Linux/Apache/PHP/MySQL 的组合在开发者中非常流行，被俗称为“LAMP 栈”。LAMP 栈之所以流行是因为它的所有组件都是开源项目，因此可以从互联网免费下载。根据一般原则，将这些组件用于个人或商业目的，或开发和分发使用它们的应用程序，不需要任何费用或收费。如果你打算编写商业应用程序，最好查看与这些每个组件相关的许可条款；你可以在组件的官方网站以及产品存档中找到它们。

现在你已经对 Zend Framework 有了初步了解，让我们直接进入如何在它中实际构建应用程序。作为第一步，你必须确保你已经有一个可以工作的 Apache/PHP/MySQL 开发环境。本书的附录提供了关于获取这些组件、安装它们以及测试你的开发环境以确保其正常运行的详细说明，你可以先跳过去，等准备好了回到这里。

都完成了吗？下一步是将 Zend Framework 下载并安装到你的开发环境中。访问 Zend Framework 官方网站 `http://framework.zend.com/` 并获取软件最新版本的副本。Zend Technologies 提供了两个版本的包：“最小”（minimal）版本，仅包含标准库和命令行工具；以及“完整”（full）版本，包含了额外的文档、示例、单元和第三方工具包。建议使用完整版本。

一旦下载了代码包，请将其内容解压到文件系统中的临时区域。

```shell
cd /tmp
tar -xzvf ZendFramework-XX.tar.gz
```

你将得到一个类似于图 1-2 的目录结构。在所有这些目录中，你立即需要的是 `library/` 和 `bin/` 目录。`library/` 包含了所有的 Zend Framework 组件，而 `bin/` 包含了有助于初始化新项目并向其添加对象的命令行工具。这些目录需要按照如下方式进行修改：

- `library/` 目录的内容应该移动到你的 PHP “include path”列表中。在 UNIX/Linux 系统上，良好的位置是 `/usr/local/lib/php` 或 `/usr/share/php`。在 Windows 上，考虑使用你的 PHP 或 PEAR 安装目录，例如 `C:\ProgramFiles\PHP` 或 `C:\ProgramFiles`。注意，如果目标目录不在你的 PHP “include path”列表中，你必须在继续之前添加它。

![](img/222e7e58871b088cc6397852e1452b57_27_0.png)

`bin/` 目录包含三个脚本：用于 UNIX/Linux 的命令行接口 `zf.sh`；用于 Windows 的 `zf.bat`；以及主脚本 `zf.php`。在 UNIX/Linux 上，你需要赋予 `zf.sh` 执行权限；你可能也想对其重命名或设置别名以便访问。

图 1-2 Zend Framework 存档包的内容

```text
192.168.1.4 - PuTTY
root@achilles:/tmp# zf --help
end Framework Command Tool v1.9.0
Usage:
  zf [-global-options] action-name [--action-options] provider-name [--provider-options] [parameters ...]
Note: 你可以在上述用法字符串的任何位置使用 "?" 请求特定的帮助信息。
例如：“zf ?”将列出版本的所有可用操作
Providers and their actions:
Version
  zf show [-mini] name-included
Note: 有特殊功能，可以使用 zf show? 获取特定帮助。

Phpinfo
  zf show phpinfo

Manifest
  zf show manifest
```

**图 1-3** `zf --help` 命令的输出

以下是执行这些任务的命令示例：

```shell
cd ZendFramework-XX
mv library/* /usr/local/lib/php/
mv bin/* /usr/local/bin/
chmod +x /usr/local/bin/zf.sh
ln -s /usr/local/bin/zf.sh /usr/local/bin/zf
```

你应该能够在 shell 提示符（无论是 Linux 还是 Windows）中访问 `zf` 命令行脚本。尝试在你的 shell 提示符中使用以下命令：

```shell
zf --help
```

如果它工作正常，你应该看到一个选项列表。图 1-3 展示了在 Linux 下的输出。

一旦你安装了 Zend Framework 并让 `zf` 命令行脚本工作，你就可以使用它创建应用程序了。接下来的步骤将讨论如何完成此任务。

## 第 1 章：Zend Framework 1

### 理解应用需求

在深入研究代码之前，花几分钟时间了解你将在本书前半部分将构建的示例应用程序是值得的。该应用程序是一个虚拟商店的网站，专门向邮票爱好者和专业集邮家出售稀有邮票。然而，与其他爱好者商店不同，它有一个有趣的之处：它充当在线邮票寻源机构，允许个人收藏家将他们可能想要出售的邮票照片和描述上传到中央数据库，并让买家按国家、年份和关键词搜索该数据库。如果遇到市场需求，商店将从卖者处购买邮票并将其转售给买家……当然了，价格不菲！

指定的网站管理员将可以直接访问已上传的列表，并手动批准合适的项目以显示在搜索结果中。管理员还可以访问一个用于新闻和新闻稿的简单内容管理系统；这些信息既可以通过网站访问，也可以通过 RSS 馈访问。为了增加趣味性，邮票数据库还可以通过 SOAP 接口提供，以便于与第三方应用程序集成。

听起来很酷吗？确实如此，而且还有一个很酷的名字：朋友们喜欢称其为邮票查询与研究引擎，即 SQUARE。SQUARE 示例应用程序的设计理念是涵盖了日常开发中遇到的许多需求：静态页面、输入表单、图像上传、受登录保护的管理面板、数据分页和排序、多种输出类型以及关键词搜索。实现这些功能要求人们理解数据库处理、输入验证、会话管理、身份验证与安全、CRUD 数据库操作、Web 服务 API 以及与第三方库的集成细节。因此，它是使用 Zend Framework 开发应用的良好起点。

## 创建应用目录

让我们开始吧。切换到 Web 服务器的文档根目录（在 UNIX/Linux 上通常为 `/usr/local/apache/htdocs`，在 Windows 上为 `C:\Program Files\Apache\htdocs`），并为你的应用程序创建一个新的子目录。由于上一节中已解释的原因，请将此目录命名为 `square/`。

```shell
cd /usr/local/apache/htdocs
mkdir square
```

该目录在本书中被称为 `$APP_DIR`。

下一步是初始化应用程序并为 Zend Framework 骨架应用程序创建基础文件和目录。`zf` 命令行脚本可以为你完成此工作——只需切换到 `$APP_DIR` 并运行以下命令（参见图 1-4）：

```shell
cd /usr/local/apache/htdocs/square
zf create project
```

```text
192.168.1.4 - PuTTY
root@achilles://usr/local/apache/htdocs/square# zf create project
Creating project at /usr/local/apache2/htdocs/

root@achilles://usr/local/apache/htdocs/square# ls -ai
total 28
drwxr-xr-x 6 root 4096 2009-08-13 17:40 /
drwxr-xr-x 4 root 4096 2009-08-13 17:39 ..
-rw-r--r-- 1 root 2210 2009-08-13 17:40 .zfproject.xml
drwxr-xr-x 6 root 4096 2009-08-13 17:40 application/
drwxr-xr-x 2 root 4096 2009-08-13 17:40 library/
drwxr-xr-x 2 root 4096 2009-08-13 17:40 public/
drwxr-xr-x 4 root 4096 2009-08-13 17:40 tests/
root@achilles://usr/local/apache/htdocs/square# _
```

图 1-4 `zf create project` 命令的输出

脚本现在将创建一个空的应用程序容器，并为其填充一组初始文件。一旦过程完成，你将在应用程序目录中看到许多新的子目录，如图 1-5 所示。这是 Zend Framework 的默认目录结构。每个目录都有不同的用途，如下文列表的所示：

- `$APP_DIR/application/` 是主应用目录，包含所有的应用程序代码，包括控制器、视图和模型。
- `$APP_DIR/library/` 存放应用程序使用的第三方库和类。如果你决定在构建应用时一起构建 Zend Framework（参见下一节），你将把它放在这里。
- `$APP_DIR/public/` 存放公开访问的内容，如图像和媒体文件、CSS 样式表、JavaScript 代码和其他静态资源。
- `$APP_DIR/tests/` 存放用于应用程序的单元测试。

| 文件夹 |
| --- |
| square |
| application |
| configs |
| controllers |
| models |
| views |
| helpers |
| scripts |
| error |
| index |
| library |
| public |
| tests |

图 1-5 新 Zend Framework 应用程序的默认目录结构

## 添加 Zend Framework 库

此时，你有一个重要的决定要做出。你必须决定是将 Zend Framework 库包含在你的应用程序中，还是让用户自己下载并安装这些库。每种方案都有优缺点：

- 要求用户自行下载 Zend Framework 库可以确保他们始终可以使用最新的代码（以及修复）。然而，这对初学者来说可能很困难，而且如果新版本与旧不兼容，可能会出现难以追踪的错误。
- 将 Zend Framework 库与应用程序打包可以确保用户开箱即用。然而，这将用户锁定在特定版本的 Zend Framework 上，可能难以升级到具有新功能或修复的版本。

为了本书起，我将假设 Zend Framework 库将与应用程序打包。因此，使用以下命令将 Zend Framework `library/` 目录的内容复制到 `$APP_DIR/library/`。默认设置是在该位置查找库。

```shell
cp -R /usr/local/lib/php/Zend library/
```

为了方便访问应用程序，建议定义一个新的虚拟主机并指向应用程序的公共目录。这是一个可选但推荐的步骤，它可以模拟“线上”环境，并以用户的视角呈现应用程序资源（URL）。

假设你正在使用 Apache 服务器，可以通过编辑 Apache 配置文件（`httpd.conf` 或 `httpd-hosts.conf`）并添加以下内容为应用程序设置虚拟主机：

```apacheconf
<VirtualHost *:80>
  DocumentRoot "/usr/local/apache/htdocs/square/public"
  ServerName square.localhost
</VirtualHost>
```

这些行定义了一个新的虚拟主机 `square.localhost`，其文档根对应 `$APP_DIR/public` 目录。重启 Web 服务器以激活这些设置。注意，如果你在网络环境中，可能需要更新网络 DNS 服务器以让它识别新主机。

一旦完成这些步骤，打开你的 Web 浏览器并访问刚刚设置的虚拟主机，输入 URL `http://square.localhost/`。（等等，流程...)

## 使用命令行工具

如上一节所示，`zf` 命令行脚本允许你执行许多不同的操作。例如，进入命令行提示符并执行以下命令：

```shell
zf show version
```

**Q**：我可以在共享托管环境中使用 Zend Framework 吗？在那种环境下，我可能对全局 PHP 配置指令（如 PHP 的“include path”）只有有限或没有控制权。

**A**：可以，完全可以。有几种方法可以实现这一点：



- 如果你担心在应用程序中使用 Zend Framework 类，你只需要将 `library/Zend` 目录复制到你的主目录下，然后在应用程序脚本中使用 `ini_set()` 函数动态地将此位置添加到你的 PHP 路径中。

- 如果你想使用 `zf` 命令行脚本，你还应该将 `bin/` 目录也复制到你的主目录下（即与 `library/` 目录处于同一级）。你应该能够像往常一样通过在脚本名前加上完整的文件系统路径来调用 `zf` 命令行脚本。这种方法是有效的：如果从 PHP 包含路径中找不到 Zend Framework，`zf` 命令行脚本也会在当前目录层级中的上一级中查找 `library/Zend` 目录，如果可用则将使用它。或者，你也可以通过将 `ZEND_TOOL_INCLUDE_PATH_PREPEND` 变量设置为适当的位置，显式地告诉 `zf` 命令行脚本去哪里查找你的 Zend Framework 安装。

此命令显示当前安装的 Zend Framework 版本号。图 1-7 和图 1-8 分别说明了 Linux 和 Windows 上的输出。你可以使用以下命令获取 `phpinfo()` 信息：

```shell
shell zf show phpinfo
```

`zf` 命令行工具还提供了一种快速方便的方法来查看应用程序的“配置”（profile）。此配置包含应用程序当前内容的层次列表，并对其中的文件进行描述，它是在无需手动进入每个目录的情况下获取应用程序视图的绝佳方法。

| 192.168.1.4 - PuTTY |
| :--- |
| root@achilles:/tmp# zf show version |
| Zend Framework Version: 1.9.0 |
| root@achilles:/tmp# _ |

**图 1-7** 在 Linux 上运行 `zf show version` 命令的输出

**图 1-8** 在 Windows 上运行 `zf show version` 命令的输出

尝试通过切换目录到 `$APP_DIR` 并执行以下命令来测试：

```shell
shell> zf show profile
```

图 1-9 展示了在 Linux 上的输出。

![](img/222e7e58871b088cc6397852e1452b57_34_0.png)

**图 1-9** 示例项目配置

### 总结

- Zend Framework 官方网站：http://framework.zend.com/
- Zend Framework 社区维基：http://framework.zend.com/wiki/
- Zend Framework 使用统计数据：http://framework.zend.com/about/numbers
- Zend Framework 案例研究：http://framework.zend.com/about/casestudies
- Zend Framework 组件：http://framework.zend.com/about/components
- Zend Framework CLI 工具：http://framework.zend.com/manual/en/zend.tool.framework.clitool.html
- Zend Framework 文件系统布局：http://framework.zend.com/wiki/display/ZFDEV/Choosing+Your+Application+%27s+Directory+Layout
- Zend Framework 开发路线图：http://framework.zend.com/roadmap

# 第 2 章：与模型、视图、控制器和路由的操作

## Zend Framework：入门指南

### 核心技能与概念

- 理解模型-视图-控制器（MVC）模式的基础
- 了解 URL 请求在 Zend Framework 应用中是如何处理的
- 模块化目录布局的优势
- 为应用程序视图定义并应用全局模板
- 为应用程序资源创建自定义路由
- 学习提供静态内容页面

上一章让你对 Zend Framework 进行了简要介绍，引导你完成了安装框架和启动新项目的过程。现在，你需要开始用代码来填充应用程序骨架，使其具有功能性。本章将帮助你完成这一点，向你介绍 Zend Framework 的基本设计原则，然后将这些知识应用于构建真实应用程序的任务中。话话不多说，让我们直接开始吧！

## 理解基本概念

在开发 PHP 应用程序时，典型的方法是使用特殊分隔符将 PHP 代码嵌入到一个或多个 HTML 文档中。这使得使用变量和函数调用等编程结构构建动态 Web 页面变得简单；只需更改 HTML 代码中嵌入的变量值，页面显示的内容就会随之改变。

然而，每个应用程序开发者都清楚，这种便利是有代价的。上一段描述的方法——与 HTML 代码紧密交织的 PHP 脚本——意味着维护它们是一场噩梦。由于物理文件通常包含 HTML 界面元素和 PHP 代码，开发者和设计师必须相互协调以进行更改。最常见的例子是界面设计师需要更改 Web 应用程序的外观和感受——通常，他们对 HTML 代码所做的更改必须由开发者监控，以确保嵌入的业务逻辑的完整性。

这种安排很容易被识别。为了解决这个问题，模型-视图-控制器（MVC）模式将业务逻辑与表示层分离开。

## 第 2 章：与模型、视图、控制器和路由的操作

在开发 PHP 应用程序时，典型的方法是使用特殊分隔符将 PHP 代码嵌入到一个或多个 HTML 文档中。这使得使用变量和函数调用等编程结构构建动态 Web 页面变得简单；只需更改 HTML 代码中嵌入的变量值，页面显示的内容就会随之改变。

然而，每个应用程序开发者都清楚，这种便利是有代价的。上一段描述的方法——与 HTML 代码紧密交织的 PHP 脚本——意味着维护它们是一场噩梦。由于物理文件通常包含 HTML 界面元素和 PHP 代码，开发者和设计师必须相互协调以进行更改。最常见的例子是界面设计师需要更改 Web 应用程序的外观和感受——通常，他们对 HTML 代码所做的更改必须由开发者监控，以确保嵌入的业务逻辑的完整性。

这种安排很容易被识别。为了解决这个问题，模型-视图-控制器（MVC）模式将业务逻辑与表示层分离开。

### 模型

当应用程序数据存储在数据库中（如 MySQL、SQLite 或 PostgreSQL）时，模型可能会使用底层抽象层来处理连接和执行 SQL 查询。Zend Framework 包含一个数据库抽象层 `Zend_Db`，它为许多数据库提供了通用接口，Zend Framework 中的模型使用数据映射（Data Mapper）模式。集成第三方模型（如使用 Doctrine 或 Propel 创建的模型）也非常容易。

为了说明，考虑一个允许用户发布广告的简单应用程序。在 MVC 模式下，模型负责访问和操作数据。以下是此类模型的示例：

```php
<?php
class ListingModel
{
    public function __construct()
    {
        // 构造函数
    }

    public function read($id)
    {
        // 使用 ID 获取单个列表
    }

    public function find($criteria)
    {
        // 获取匹配条件的列表
    }

    public function save()
    {
        // 插入或更新列表
    }

    public function delete()
    {
        // 删除列表
    }
}
```

### 视图

如果模型只关注访问和操作应用程序的原始数据，那么视图只关注如何将这些数据呈现给用户。视图可以简单地认为是“用户界面层”，负责显示数据但无法访问或操作它。视图也可以接收用户的输入，但它们的责任再次与输入表单的外观和行为有关；它们不负责处理、清理或验证输入。

在之前讨论分类应用中，视图将负责显示当前列表并生成输入新列表的表单。在所有这些情况下，控制器和或模型将处理检索和处理数据的任务，而视图将负责将这些数据转换为相应的格式并渲染给用户。

这里是一个用于显示最新列表的视图示例：

```html
<!DOCTYPE html PUBLIC "//W3C//DTD HTML 1.0//EN"
"http://www.w3.org/TR/DTD/xhtml-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">
<head>
<meta http-equiv="Content-Type" content="text/html;
charset=utf-8"/>
<base href="/" />
</head>
<body>
<div id="header">
<div id="logo">
*
```

## 第 2 章：使用模型、视图、控制器和路由 23

```html
<img src="images/logo.gif" />
</div>
</div>
<div id="content">
<h1>最近列表</h1>
<?php foreach ($this->listings as $l): ?>
<div class="listing">
  <h3 class="listing_title">
  <a href="listing/view/<?php echo $l->id; ?>?">
    <?php echo $l->title; ?>
  </a>
  </h3>
  <span class="listing_content">
  <?php echo $l->content; ?>
  </span>
</div>
<?php endforeach; ?>
</div>
</body>
</html>
```

正如这个示例所所示的，视图通常表示为包含 HTML 代码或标记的 PHP 脚本，这些代码用于正确地向用户渲染和显示内容。脚本可以包含用于动态数据的变量占位符；这些占位符的值由响应的控制器设置，并在渲染视图时插值到视图中。在 Zend Framework 下，视图由 `Zend View` 组件渲染，该组件还提供了用于输出转义的辅助函数以及一组用于导航、分页和链接生成等常见任务的“助手”。通过扩展 `Zend_View_Interface` 类，可以很容易将 Smarty 或 Savant 等第三方模板引擎集成到 Zend Framework 应用中。

## 控制器

控制器是模型和视图之间的桥梁。它们使用模型对应用程序数据进行更改，然后调用视图将结果显示给用户。控制器可能链接到多个视图，并根据任何时刻要显示的响应调用不同的视图。因此，控制器可以被视为“处理层”，负责响应用户操作、触发应用程序更改并向用户显示新状态。

在之前讨论的应用程序上下文中，控制器将负责读取和验证请求参数，使用模型函数保存和检索列表，并选择合适的视图来显示列表详情。例如，控制器将拦截对最新列表的请求，使用 `ListingModel` 模型获取最新条目列表，选择合适的视图，将条目插值到视图中，并渲染视图。同样，如果用户选择添加新列表，控制器将选择并渲染一个输入视图，验证并清理用户输入，使用 `ListingModel` 将清理后的输入插入数据存储器中，然后选择并渲染另一个视图来显示操作是否成功。

这是一个结合了之前插图的模型和视图的控制器示例：

```php
<?php
class ListingController
{
    function indexAction()
    {
        // 初始化模型的代码
        // 并检索数据
        $listing = new ListingModel();
        $matches = $listing->find(
            array(
                'date' => '-10 days',
                'status' => 'published'
            )
        );
        // 使用模型返回的数据初始化视图
        $view = new ListingView();
        $view->listings = $matches;
        echo $view->render('recent.php');
    }
}
?>
```

正如这个示例所示的，控制器充当了中间人的角色，调用模型对应用程序数据执行操作，并使用视图将这些操作的结果显示给用户。在 Zend Framework 下，控制器被创建为 `Zend_Controller_Action` 类的子类，并包含称为“动作”（actions）的方法，这些方法包含了与模型和视图交互所需的处理逻辑。还有一个控制器，即前端控制器（front controller），负责拦截用户请求并调用适当的控制器和动作方法来满足这些请求（更多内容见下一节）。

除了上述的三个组件外，Zend Framework 还引入了一些额外的细节来简化应用程序开发。这些细节将在后续章节中描述。

## 模块

默认情况下，所有模型、控制器、动作和视图都位于——还能是什么呢——“默认”（default）模块。然而，你可能希望根据 Web 应用程序不同的功能区域，将模型、视图和控制器组合在独立的“箱”中。

模块提供了一种实现此的方法。例如，如果你的应用程序包含搜索、用户配置管理和新闻功能，你可以创建的“搜索”、“配置”和“新闻”模块，并将每个模块相应的模型、视图和控制器放在这些模块中。

模块提供了一种组织应用程序代码的方便方法，或者提供了一种构建可以轻松插入现有安装的第三方应用程序组件的方法。Zend Framework 的默认路由器完全感知模块的，允许你无需任何自定义编程即可在应用程序中使用模块，而且每个模块（“默认”模块外）都有它们自己的命名空间，以防止对象和变量冲突。

### 路由

路由提供了用户请求与动作之间的链接。当用户对应用程序 URL 发起请求时，前端控制器会拦截该请求并根据 URL 模式决定应该调用哪个控制器和动作来满足请求。这种将请求路由到控制器的过程是应用程序执行流的关键部分，并且可以进行广泛的配置。路由利用正则表达式进行模式匹配，可以使用 XML 或 INI 文件表示。

默认情况下，Zend Framework 包含了一些适用于小型复杂度应用程序的标准路由。这些标准路由假设应用程序 URL 采用 `/module/controller/action` 的形式，并相应地分发用户请求。例如，位于 `http://application/auto/listing/index` 请求将自动映射到“auto”模块中的 `ListingController::indexAction`。注意控制器和动作名称遵循特定的约定。

> **注意**
>
> Zend Framework 会对不符合 `/module/controller/action` 格式的路由应用默认值。关于这些默认值及其映射影响的详细讨论，可以在“理解组件交互”章节中找到。

如果上一节的标准路由对于你的应用程序需求过于局限或缺乏活性，Zend Framework 还支持自定义路由。这些路由支持（包括）可选参数、默认值和多链路由，并允许你精细管理应用程序的路由，使得应用程序 URL 不需要反映你内部对控制器、动作和模块的分类。

### 布局

在经典意义上，布局是元素排列的定义。在 Zend Framework 应用程序上下文中，布局可以被视为界面模板，提供了一种使用或多个标准全局界面“装饰”应用程序内容的方法。布局提供了一种将常用界面元素（如页眉页脚和全局导航组件）抽象到独立文件的方法，这些文件可以独立于视图进行编辑和维护。

应用程序拥有多个布局是非常常见的。例如，你可能希望向用户展示一种界面，向管理员展示另一种，或者允许用户通过从预定义的界面主题中选择来定制他们的体验。布局使得实现这些相关选项变得相当容易。

> **注意**
>
> 你将在本章稍后的部分开始处理模块、自定义路由和布局。

### 理解组件交互

如果你把 Zend Framework 应用程序比作马戏团（这个比喻往往确实如此），那么控制器就是团长，负责调度表演并确保观众满意。本节将更详细地检查它的角色，并在拦截和满足应用程序请求的步骤上下文中进行说明。

图 2-1 展示了请求通过典型 Zend Framework 应用程序的流。

**图 2-1** 模型、视图和控制器之间的交互

# 第 2 章：使用模型、视图、控制器和路由 27

作为负责拦截客户端请求并将其重定向到适当目标以响应的控制器，前端控制器（front controller）在请求通过应用程序的整体流程中起着关键作用。

- 当请求到达时，Web 服务器的 `.htaccess` 文件会自动将其重写为标准格式，并传递给 `index.php` 脚本。该脚本会设置应用环境，读取应用配置文件，并创建前端控制器的实例。

- 前端控制器检查请求并确定 URL 的关键组件。它尝试将请求路由到适当的控制器（controller）和动作（action）。为了执行路由，前端控制器将检查默认路由和自定义路由，并利用模式匹配技术为请求选择一个适当的目标。

- 如果找到匹配项，前端控制器将跳转到相应的控制器和动作。一旦被调用，动作将使用一个或多个模型来更改应用状态。它还会选择要显示的视图并设置任何必要的属性。一旦动作完成，所选视图将渲染其输出，并根据需要将其封装在布局（layout）中。该输出将传回给请求的客户端。

- 如果应用程序定义的任何路由都不匹配请求，则会抛出异常并调用错误控制器和错误动作。根据异常的参数，错误控制器将渲染一个包含失败通知的视图。该输出将传回给请求的客户端。

### 注意

在请求处理过程中生成的任何意外异常都将调用错误控制器和相应的动作。这将产生一个包含失败通知的视图，并将其传回给请求的客户端。



如前所述，路由系统会自动将`module/controller/action`格式的 URL 映射到相应的模块、控制器和动作。例如，要访问“auto”模块中的`Listing::saveAction`，你需要请求 URL`http://application/auto/listing/save`。同样，要访问“content”模块中的`NewsController::edit`，你需要请求`http://application/content/news/edit`。

如果路由系统收到的请求不符合`/module/controller/action`格式，它将自动应用默认值，具体如下所示：

- 对于没有模块名称的请求，路由系统会自动假设模块为“default（默认）”模块。
- 对于没有控制器的请求，路由系统会自动假设控制器为所选模块的`IndexController`。
- 对于没有动作名称的请求，路由子系统会自动假设动作名称为所选控制器的`indexAction`。

为了更好地理解这些默认值在实践中如何运作，请考虑以下示例：

- “default”模块中的`UserController::sendAction`可以通过`http://application/default/contact/send`和`http://application/contact/send`访问。
- “default”模块中的`PostController::indexAction`可以通过`http://application/default/post/index`和`http://application/post/`访问。
- “content”模块中的`NewsController::indexAction`可以通过`http://application/content/news/index`和`http://application/content/news`访问。

## 深入了解默认索引页的背后

有了这些背景信息，让我们回到第 1 章中 ZF 命令行工具生成的代码，仔细观察 Zend Framework 欢迎页是如何生成的。我们将从头开始，从对`http://square.localhost/`的初始请求开始。这产生了图 2-2 所示的默认应用程序页面。

实现这一过程的因素是什么？嗯，考虑当你请求 URL`http://square.localhost/`时，上一节中的默认路由就会开始作用，该 URL 被自动重写为`http://square.localhost/default/index`。Zend Framework 的路由系统会将此请求重定向到“default”模块的`IndexController`和`indexAction()`方法。

此控制器和`indexAction`是由 ZF 命令行工具自动创建的，按照约定，它们存储在`$APP_DIR/application/controllers/IndexController.php`。如下所示：

```php
<?php
class IndexController extends Zend_Controller
{
    public function init()
    {
        /* 在此处初始化控制器 */
    }

    public function indexAction()
    {
        // 动作主体
    }
}
```

在这里，`indexAction()`方法是一个没有任何可执行代码的简单存根。一旦执行完成，它会自动选择它的默认视图进行渲染。按照约定，此视图以控制器和动作命名，可以在相应的视图脚本目录中找到，在这种情况下，该目录为`$APP_DIR/application/views/scripts/index/index.php`。

打开此文件，你将看到生成图 2-2 所示输出的 HTML 标记：

```css
<style>
  a:link,
  a:visited
{
  color: #0398CA;
}

span#zf-name
{
  color: #91BE3F;
}

div#welcome
{
  color: #FFFFFF;
  background-image: url(//framework.zend.com/images/bkg_header.jpg);
  width: 600px;
  height: 400px;
  border: 2px solid #444444;
  overflow: hidden;
  text-align: center;
}
```

```css
div#more-information
{
    background-image: url(
      http://framework.zend.com/images/bkg_bottom.gif);
    height: 100%;
}
</style>
<div id="welcome">
  <h1>Welcome to the <span id="zf-name">Zend Framework!</span></h1>
  <h3>This is your project's main page</h3>
  <div id="more-information">
    <p>Helpful Links: <br />
    <a href="http://framework.zend.com/">Zend Framework Website</a>
    <a href="http://framework.zend.com/manual/en/">Zend Framework Manual</a></p>
  </div>
</div>
```

从这里可以很清楚，只要你命名了控制器和视图，其实并没有多少工作要做。

| 目录 | 描述 |
| --- | --- |
| `$APP_DIR/application` | 主应用程序目录 |
| `$APP_DIR/application/controllers` | 全局控制器 |
| `$APP_DIR/application/views` | 全局视图 |
| `$APP_DIR/application/models` | 全局模型 |
| `$APP_DIR/application/configs` | 全局配置 |
| `$APP_DIR/application/layouts` | 全局布局 |
| `$APP_DIR/application/modules` | 模块 |
| `$APP_DIR/library` | 第三方库和类 |
| `$APP_DIR/public` | 主公共访问目录 |
| `$APP_DIR/public/css` | CSS 样式表 |
| `$APP_DIR/public/js` | JavaScript 程序代码 |
| `$APP_DIR/public/images` | 图像 |
| `$APP_DIR/tests` | 单元 |
| `$APP_DIR/temp` | 临时数据 |

**表 2-1** Zend Framework 应用程序中的关键目录

## 理解模块化布局

在上一节中，你看到了命令行工具如何为你创建目录结构。在初始状态下，该结构只包含运行基本应用程序所需的目录。随着你通过新功能来丰富应用程序，你还需要扩展此结构，并创建额外的目录来存放不同类型的数据。

为了更好地理解这一点，请考虑图 2-3，它展示了完整的目录结构。

图 2-3 所示的每个目录都有特定的用途，如表 2-1 所示，符合您应用程序的需求和结构。

尽管如此，这些章节中描述的 SQUARE 示例应用程序大量使用了模块，本书建议在 Zend Framework 应用开发中通用模块，原因如下：

- 将代码组织成模块可以产生一个结构化的代码树，因为所有与特定功能或一组功能相关的控制器、视图和模型都存储在同一个目录树中。基于模块的目录布局使得应用程序内部的逻辑分离区域一目了然，无需额外的文档，而且从长远来看更具维护性。
- 将代码组织成模块鼓励了创建健壮且可扩展的软件。模块可以结构化为独立的包，拥有自己的控制器、视图和模型。因此，模块可以被视为可重用的组件，可以插入到现有应用程序中，以快速为其提供新功能。

当你在使用 Zend Framework 的默认路由使用模块时，必须在 URL 请求中包含模块名称，格式为`/module/controller/action`。当路由子系统接收到一个不包含模块名称的请求时，它会自动查找它认为的“默认”模块——全局应用程序目录`$APP_DIR/`。

当应用程序在`$APP_DIR/application/modules/`中包含额外模块时，这种行为可能会在 URL 中产生小程度的不一致性。因此，在遵循模块化目录结构时，最好显式为“默认”模块创建一个目录，路径为`$APP_DIR/application/modules/default`，并将之前存储在`$APP_DIR/application/*`层级下的更多控制器、视图和模型移动到`$APP_DIR/application/modules/default/*`层级下。

![](img/222e7e58871b088cc6397852e1452b57_50_0.png)

**图 2-4** Zend Framework 应用程序模块的推荐结构

- `modules`
  - `default`
    - `controllers`
    - `helpers`
    - `models`
    - `views`
  - `views`
    - `filters`
    - `helpers`
    - `scripts`
  - `news`
    - `controllers`
    - `models`
    - `views`
  - `search`
    - `controllers`
    - `models`
    - `views`

### 尝试 2-1 使用模块化目录布局

如上一节所述，模块化目录布局强制了一致性，并产生了更易管理的代码树。接下来的步骤将讨论如何为第 1 章创建的示例应用程序采用这种布局，作为开始应用程序开发的准备。

### 创建默认模块

第一步是创建`$APP_DIR/application/modules/`目录，然后在该目录下创建一组子目录用于默认模块及其控制器和视图。`zf`命令行工具不会创建这些目录，因此需要手动执行此任务。

```shell
cd /usr/local/apache/htdocs/square/application
shell mkdir modules
shell mkdir modules/default
```

接下来，将现有的模型、控制器和视图从`$APP_DIR/application/*`移动到`$APP_DIR/application/modules/default/`：

```shell
mv controllers modules/default/
shell mv views modules/default/
shell mv models modules/default/
```

### 更新应用程序配置文件

下一步是更新全局应用程序配置文件（位于`$APP_DIR/application/configs/application.ini`），包含模块目录的路径。这告诉 Zend Framework 的路由子系统解析特定模块实体。

要执行此操作，请在文本编辑器中打开应用程序配置文件，并在`[production]`部分添加以下行：

```ini
resources.frontController.moduleDirectory = APPLICATION_PATH " /modules"
resources.modules = " "
```

一旦完成上述步骤，使用 URL`http://square.localhost/`和`http://square.localhost/default/index/index`访问应用程序首页。如果一切进展顺利，你应该在两种情况下都看到默认应用程序首页，如图 2-2 所示。

> 提示：无论你是否将应用程序组织成模块，记住你可以通过自定义路由将 URL 重定向到特定的模块、控制器和操作。

### 理解主布局和自定义路由

此时，你已经足够了解 Zend Framework 应用程序的内部原理，可以开始编写自己的代码。接下来的章节将引导你完成创建欢迎页面、为应用程序设置主布局以及构建自定义路由的过程。

为了防止命名冲突，Zend Framework 还允许使用命名空间，这些可以作为对象或类的前缀。这些命名空间可以通过自动加载器注册，根据需要自动加载相应的定义。

**图 2-5** 更新后的应用程序首页

## 设置主布局

应用程序首页现在显示了相关内容，但视觉上还有很大差距。因此，下一步是通过添加一些图像和导航来赋予它一些美感。这些元素对于应用程序的所有页面都是通用的，尽管你可以更改每个视图，但由于布局存储在单个文件中，随着应用程序的演进，更改会更容易。

要为应用程序设置主布局，请执行以下步骤。

### 创建模板文件

第一步是创建`$APP_DIR/application/layouts/`目录，这是 Zend Framework 下布局文件的默认位置。

```shell
cd /usr/local/apache/htdocs/square/application
shell mkdir layouts
```

在此目录中创建一个包含以下标记的新文本文件：

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 1.0 Strict//EN"
"http://www.w3.org/TR/html1/strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">
<head>
  <meta http-equiv="Content-Type" content="text/html;
  <meta charset="utf-8" />
  <base href="/" />
  <link rel="stylesheet" type="text/css" href="css/master.css" />
</head>
<body>
  <div id="header">
    <div id="logo">
      <img src="images/logo.gif" />
    </div>
    <div id="menu">
      <a href="#">HOME</a>
      <a href="#">SERVICES</a>
      <a href="#">CONTACT</a>
    </div>
  </div>
  <div id="content">
    <?php echo $this->content() ?>
  </div>
  <div id="footer">
    <p>Created with <a href="http://framework.zend.com/">Zend Framework</a>. Licensed under <a href="http://www.creativecommons.org/">Creative Commons</a>.</p>
  </div>
</body>
</html>
```

将此文件保存为`$APP_DIR/layouts/master.html`。你会注意到布局在使用两个资源——样式表和标志图像。这些文件位于应用程序的公共区域，以便客户端可以通过 HTTP 获取。同样，创建`$APP_DIR/public/css/`和`$APP_DIR/public/images/`目录并将必要的资源复制到这些位置。你可以在本章的代码存档中找到这些资源，该存档可以从本书的配套网站`http://www.zf-beginners-guide.com`下载。

### 更新应用程序配置文件

下一步是更新全局应用程序配置文件（位于`$APP_DIR/application/configs/application.ini`），包含布局目录的路径以及渲染视图时使用的默认布局名称。在文本编辑器中打开文件，并在`[production]`部分添加以下指令：

```ini
resources.layout.layoutPath = APPLICATION_PATH "layouts"
resources.layout.layout = master
```

现在，当你再次访问应用程序首页时，你应该能看到色彩完备的新布局，如图 2-6 所示。

### 使用自定义路由

自定义路由使得将 URL 映射到特定的模块、控制器和操作成为可能，当 Zend Framework 的默认路由被证明不足或具有局限性时，它们特别有用。

为了说明，假设你想映射应用程序 URL`/home`将用户重定向到应用程序首页。要创建一个将此 URL 映射到“默认”模块`IndexController::indexAction`的自定义路由，请更新`$APP_DIR/application/configs/application.ini`配置文件并在`[production]`部分添加以下路由条目：

```ini
resources.router.routes.home.route = /home
resources.router.routes.home.defaults.module = default
resources.router.routes.home.defaults.controller = index
resources.router.routes.home.defaults.action = index
```



路由条目通常包含 `route`、`module`、`controller` 和 `action` 属性。`route` 属性指定了应该匹配的 URL 模式，而 `module`、`controller` 和 `action` 属性则指示了应该使用哪个模块、控制器和操作，用于满足请求。每个路由都有一个唯一的名称（在本例中为 `home`），它作为视图内部自动生成 URL 的快捷方式。

# 38 Zend Framework：初学者指南

在保存更改后，尝试在你的 Web 浏览器中访问 URL `http://square.localhost/home`。如果一切正常，你应该看到应用程序的索引页，如图 2-6 所示。

### 提示

路由名称非常有用，因为你可以配合 `url()` 视图辅助函数在视图内部自动生成 URL。例如，在脚本内部调用 `$view->url(array(), 'home')` 将自动生成 URL 字符串 `/home`。

**图 2-6** 封装在自定义布局中的应用程序索引页

# 第 2 章：与模型、视图、控制器和路由工作 39

### 提问专家

**问：为什么布局（Layouts）存储在全局级别而不是模块级别？**

**答：** 在 Web 应用程序中，不同模块的视图共享同一个布局是非常常见的。因此，Zend Framework 的默认目录结构建议将布局存放在 `$APP_DIR/application/layouts/` 下的全局或按应用级别，而不是 `$APP_DIR/application/modules/` 层次结构下。

也就是说，如果你的应用程序结构使得每个模块使用不同的布局，你可以将布局文件移动到模块级别，并编写一个自定义插件，根据访问的模块动态更改布局。你可以在本章末尾的链接中找到如何执行此操作的详细讨论。

# 尝试一下 2-2 提供静态内容

在之前的章节中，你的活动仅限于修改应用程序现有的控制器和视图。然而，随着开发的进行，你会发现有必要创建控制器、动作（actions）和视图来封装额外的功能。这不需要担心，因为每当你需要为 Zend Framework 应用程序添加新功能时，都有可以遵循的标准流程。

这些步骤将在后续章节中说明，它们将引导你完成添加 `StaticContentController` 以及相关的视图，这些视图将负责提供“关于我们”和“服务”等静态内容页面。

### 定义自定义路由

第一步是为静态内容页定义基础路由。我们假设所有静态内容页的 URL 形式均为 `/content/xx`。

```php
resources.router.routes.static-content.route = /content/:page
resources.router.routes.static-content.defaults.module = default
resources.router.routes.static-content.defaults.controller = static-content
resources.router.routes.static-content.defaults.action = display
```

此路由比你之前看到的稍微复杂一点，因为它包含一个变量占位符。Zend Framework 支持在路由模式中使用变量占位符（以前面的冒号 `:` 标识），并自动将该请求转换为控制器内可以访问的变量。这意味着，例如，如果客户端请求 URL `/content/hello-world`，路由子系统将自动捕获 URL 段“hello-world”，并将其存储在名为 `page` 的请求变量中。

### 定义控制器

为什么我们需要捕获 URL 的最后一段并将其存储为请求变量？这个问题在下一段中会有答案，但在那之前，让我们创建“default”模块的 `StaticContentController`。根据惯例，它应该位于 `$APP_DIR/application/modules/default/controllers/StaticContentController.php`。创建此文件并填充以下内容：

```php
<?php
class StaticContentController extends Zend_Controller_Action
{
    public function init()
    {
    }

    // 显示静态视图
    public function displayAction()
{
        $page = $this->getRequest()->getParam('page');
        if (file_exists($this->view->getScriptPath(null)) .
            "/" . $this->getRequest()->getControllerName() .
            "/$page.php" . $this->view->viewSuffix) {
            $this->render($page);
        } else {
            throw new Zend_Controller_Action_Exception('Page not found', 404);
        }
    }
}}
```

该控制器暴露了一个动作 `displayAction()`，它负责使用请求对象的 `getParam()` 方法读取路由子系统设置的页面变量。然后它尝试寻找与该变量值匹配的视图脚本。如果找到了匹配的视图脚本，则将其渲染并发送给客户端。例如，如果客户端请求的 URL 是 `/content/hello-world`，`$request->getParam('page')` 将返回值“hello-world”，因此该动作将尝试渲染视图映射 `$APP_DIR/application/modules/default/views/scripts/static-content/hello-world.phtml`。

如果找不到匹配的视图，将抛出 404 异常并传播到默认异常处理器，由它将其格式化为可读的错误并显示给客户端。

### 提问专家

**问：** 为什么本章中所有的类定义都不包含 PHP 标签？

**答：** 根据 Zend Framework 的编码规范，仅包含 PHP 代码的文件不应包含闭合标签 `?>`，因为如果你使用的文本编辑器自动在文件末尾添加新行，这可能会导致 HTTP 响应出现 header 头部问题。有关 Zend Framework 编码规范的更多信息，请参阅本章末尾的链接。

### 定义视图

下一步（也是最后一步）是为上一步创建的控制器和动作创建相应的视图。在大多数情况下，视图名称将根据创建的控制器和动作确定。在这种特殊情况下，视图是一个接收 URL 变量的动作。要在 URL `/content/services` 处定义“服务”页面，请创建 `$APP_DIR/application/modules/default/views/scripts/static-content/services.php` 文件并填充以下示例：

```php
<h2>Services</h2>
<p>我们提供各种服务，包括订单。请联系我们以获取更多信息。</p>
```

同样，要定义 URL `/content/about-us` 处的“关于我们”页面，请创建 `$APP_DIR/application/modules/default/views/scripts/static-content/about-us.php` 并填充以下示例：

```php
<h2>About Us</h2>
<p>我们自1927年以来一直从事此，并以国际网络闻名。</p>
```

# 42 Zend Framework：初学者指南

如果你现在通过 Web 浏览器访问 `http://square.localhost/content/about-us` 或 `http://square.localhost/content/services`，你将看到上面的静态页面。图 2 展示了结果示例。

### 更新主布局

作为最后一步，你可以使用 `url()` 方法更新主菜单中的导航链接以反映新的静态页面。要执行此操作，请更新 `$APP_DIR/application/master.php` 布局，并加粗显示更改：

```html
<!DOCTYPE html "-//W3C//DTD HTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml/html1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" lang="en">
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <link href="/ />
    <link rel="stylesheet" type="text/css" href="css/master.css" />
</head>
<body>
    <div id="header">
        <div id="logo">
            <img src="/images/logo.gif" />
        </div>
    </div>

    <div id="menu">
        <a href="<?php $this->url(array( 'home')); ?>">HOME</a>
        <a href="<?php $this->url(array('page' => 'services', 'static-content')); ?>">SERVICES</a>
        <a href="#CONTACT">CONTACT</a>
    </div>
</body>
</html>
```

图 2-7 一个静态内容页面

```html
<div id="content">
  <?php echo $this->layout() ->content ?>
</div>

<div id="footer">
  <p>Created with <a href="http://framework.zend.com/">
Zend Framework</a></a>. Licensed under
  <a href="http://www.creativecommons.org/">Creative Commons</a></a>.
</p>
</div>
</body>
</html>
```

在这里，使用了 `url()` 助手方法来自动为 `/home` 和 `/content/services` 路由生成 URL。该助手接受两个参数——用于插值到 URL 字符串中的键值对数组，以及路由名称——然后在渲染视图时生成与这些参数对应的 URL 字符串。如果你重新访问应用程序索引页，你会发现“首页”（Home）和“服务”（Services）主菜单链接处于激活状态，并在点击时会显示正确的内容。

# 44 Zend Framework：学者指南

### 注意

值得注意的是，在 Zend Framework 中提供静态页面有一种简单的方法：你只需将它们作为 HTML 文件放在 `$APP_DIR/public/` 目录下，并手动链接到它们。然而，这些页面无法使用 Zend Framework 的任何内置功能，例如全局布局、路由、缓存或安全防护，因此这种方法通常不被推荐。

### 总结

现在你已经到达本章的末尾，你应该对运行 Zend Framework 应用程序的要素有更深入的理解。本章从模型-视图-控制器（MVC）设计模式开始，解释了模型、视图和控制器是什么，以及它们如何相互作用以产生逻辑分离的分层应用程序。它还介绍了重要的概念，如模块（modules）、布局（layouts）和前端控制器，并解释了在应用程序上下文中如何请求和处理用户的基本知识。最后，通过将这些理论应用于现实世界，开始自定义和增强上一章末创建的简单测试应用程序。

SQUARE 示例应用程序仍处于早期阶段：它具有自定义布局，知道如何处理模块，并且可以提供静态内容。这看起来可能不多，但实现这些非常基础的功能将帮助你理解基于 Zend Framework 的 MVC 开发的主要原理，并为后续章节高级内容奠定坚实的基础。

要了解更多本章讨论的话题，请考虑访问以下链接：

- Wikipedia 关于模型-视图-控制器架构的讨论：<http://en.wikipedia.org/wiki/Model-view-controller>
- Zend Framework MVC 实现的基础知识：<http://framework.zend.com/docs/quickstart>
- Zend Framework 路由器：<http://framework.zend.com/manual/en/zend.controller.router.html>
- Zend Framework 前端控制器：<http://framework.zend.com/manual/en/zend.controller.front.html>
- Zend Framework 布局引擎：<http://framework.zend.com/manual/en/zend.layout.html>
- 关于使用 Zend Framework 构建模块化应用程序的讨论（Jeroen Keppens）：<http://blog.keppens.biz/2009/06/create-modular-application-with-zend.html>
- Zend Framework wiki 和论坛上关于每模块布局的讨论：<http://framework.zend.com/wiki/display/ZFPROP/Zend_Layout> 以及 <http://www.zffor.com/zend-framework-components-13/model-view-mvc-21/modules-layouts-2654.html>
- Zend Framework 目录布局：<http://framework.zend.com/wiki/display/ZFPROP/Zend+Framework+Default+Project+Structure+-With+BeerItem>
- Zend Framework 编码规范：<http://framework.zend.com/manual/en/coding-standard.html>

本页特意留

# 第 3 章

## 处理表单

### Zend Framework：学者指南

#### 核心技能与概念

- 学习通过编程创建表单和表单元素
- 理解如何过滤和验证用户输入
- 防止表单免受跨站请求伪造（CSRF）攻击和垃圾邮件机器人
- 控制表单元素和错误信息的外观
- 创建一个可工作的联系表单

#### 理解基础

在本章中，你将学习如何在 Zend Framework 中使用表单。我们将从创建一个简单的联系表单开始，然后通过验证、过滤和安全功能来扩展其功能。

首先，让我们来看表单的一个基础示例。

```php
<!DOCTYPE html>
<html PUBLIC "-//W3C//DTD HTML 1.0 Transitional//EN" "http://www.w3.org/TR/REC-html4transitional.dtd" lang="en">
<head>
  <title>创建项目</title>
</head>
<body>
  <h2>创建项目</h2>
  <form method="post" action="create.php">
    <?php if (!isset($_POST['submit'])): ?>
      <table>
        <tr>
          <td>名称：</td>
          <td><input type="text" name="name" size="30"></td>
        </tr>
        <tr>
          <td>数量：</td>
          <td><input type="text" name="qty" size="30"></td>
        </tr>
      </table>
      <input type="submit" name="submit" value="提交" />
    <?php else: ?>
      <?php
        // 处理表单数据
      ?>
    <?php endif; ?>
  </form>
</body>
</html>
```

在上面的示例中，我们使用标准的 HTML 表单来收集两个信息：名称和数量。我们使用一个简单的 `if` 语句通过查找 `POST['submit']` 变量来判断表单是否提交。如果没有提交，我们显示表单；如果提交了，我们提供一个处理数据的地方。

现在，让我们看看可能如何处理表单数据。

```php
<?php
try {
  // 尝试连接
  $pdo = new PDO('mysql:dbname=test;host=localhost', 'user', 'pass');

  // 处理输入
  $name = $pdo->quote($_POST['name']);
  $qty = $pdo->quote($_POST['qty']);

  // 创建并执行查询
  $sql = "INSERT INTO shoppinglist (name, qty) VALUES ($name, $qty)";
  $pdo->exec($sql) or die("错误：" . implode(":", $pdo->errorInfo()));

  // 关闭连接
  unset($pdo);

  // 显示成功消息
  echo '感谢您的提交';
} catch (Exception $e) {
  die("错误：" . $e->getMessage());
}
?>
```



上面的代码使用 PDO 连接数据库并插入表单数据。我们使用`quote()`方法转义输入，这有助于防止 SQL 注入。我们还将代码封装在`try-catch`块中以处理任何可能的异常。

虽然这是一个基础示例，但我们有很多改进它的方法。在随后的章节中，我们将探索如何添加验证、过滤和安全功能，使我们的表单更加健壮和安全。

# 第 3 章：处理表单

Zend Framework 自带了一组组件，统称为 Zend Form，这些组件解决了上述问题。为了说明，请考虑以下示例，它使用`Zend_Form`来产生与之前的脚本等效的结果：

```php
<?php
class Form_Item_Create extends Zend_Form {
    public function init() {
        // initialize form
        $this->setAction('/item/create')
            ->setMethod('post');

        // create text input for name
        $name = new Zend_Form_Element('name');
        $name->label('Item name:')
            ->setOptions(array('size' => '35'))
            ->setRequired(true)
            ->addValidator('NotEmpty', true)
            ->addValidator('Alpha', true)
            ->addFilter('HTMLEntities')
            ->addFilter('StringTrim());

        // create text input for quantity
        $qty = new Zend_Form_Element('qty');
        $qty->label('Item quantity:')
            ->setOptions(array('size' => '4'))
            ->setRequired(true)
            ->addValidator('NotEmpty', true)
            ->addValidator('Int', true)
            ->addFilter('HTMLEntities')
            ->addFilter('StringTrim());

        // create submit button
        $submit = new Zend_Form_Element_Submit('submit');
        $submit->label('Submit')
            ->setOptions(array('class' => 'submit'));

        // attach elements to form
        $this->addElement($name)
            ->addElement($qty)
            ->addElement($submit);
    }
}
class ExampleController extends Zend_Controller_Action {

public function formAction() {
  $form = new Form_Item_Create();
  $this->view->form = $form;
  if ($this->getRequest()->isPost()) {
    if ($form->isValid($this->getRequest()->getPost())) {
      $values = $form->getValues();
      $pdo = new PDO('mysql:dbname=test;host=localhost', 'user',
      'pass');

      $sql = sprintf('INSERT INTO shoppinglist (name, qty) VALUES (%s, %d)', $values['name'], $values['qty']);
      $pdo->exec($sql);
      $this->helper->getHelper('FlashMessenger')
        ->showMessage('Thank you for your submission');
      $this->redirect('/index/success');
    }
  }
}
```

图 3-2 展示了该表单的样子。

你会立即注意到图 3-2 中创建表单的代码有三点不同：

- 脚本中没有一行 HTML 代码。表单和表单元素被表示为 PHP 对象，并使用对象方法进行配置。这确保了一致性并生成了符合标准的 Web 表单。
- 提供了预定义的验证器（validators）和过滤器（filters），用于常见的输入验证和清理任务。这减少了工作量，产生了更具维护性的代码，并避免了重复。验证器可以组合或扩展以支持自定义需求。
- 验证器是在指定表单字段的同时指定的。这允许表单“知道”每个字段支持的内容，并轻松地识别输入错误的来源。单个字段可以与多个验证器关联，以进行更严格的输入验证。

从这些点可以清楚看出，`Zend_Form`为表单创建和数据验证提供了一个方便、可维护且可扩展的解决方案。本章的剩余部分将详细探讨`Zend_Form`，并在实际环境中对其进行说明。

图 3-2 使用`Zend_Form`组件创建的表单

## 创建表单和表单元素

从上一节中，你知道`Zend_Form`提供了一个面向对象的 API 来生成表单和验证输入。在`Zend_Form`方法下，表单被表示为`Zend_Form`基类的实例或继承该基类的对象。该基类暴露了许多方法来控制表单的操作，包括用于设置表单操作 URL 的`setAction()`方法和用于设置提交方法的`setMethod()`方法。还有一个通用的`setAttrs()`方法，允许你设置其他表单属性。以下是使用这些方法的示例：

```php
<?php
class Form_Example extends Zend_Form
{
    public function init()
    {
        // initialize form
        $this->setAttribute('/my/action')
            ->setAttrs(array(
                'class' => 'form',
                'id' => 'example'
            ))
            ->setMethod('post');
    }
}
```

通过实例化相应的`Zend_Form_Element*`对象、通过类方法设置元素属性，然后使用`addElement()`方法将其附加到表单来添加表单元素。以下是在表单中添加文本输入和提交按钮的示例：

```php
<?php
class Form_Example extends Zend_Form
{
    public function init()
    {
        // initialize form
        $this->setAttribute('/my/action')
            ->setAttrs(array(
                'class' => 'form',
                'id' => 'example'
            ))
            ->setMethod('post');

        // create text input for title
        $title = new Zend_Form_Element_Text('title');
        $title->setLabel('Title:')
            ->setOptions(array(
                'size' => '35'
            ));

        // create submit button
        $submit = new Zend_Form_Element_Submit('submit');
        $submit->label('Submit')
            ->setOptions(array('class' => 'submit'));

        // attach elements to form
        $this->addElement($title)
            ->addElement($submit);
    }
}
```

# Zend Framework：学者指南

| 元素类 | 描述 |
| --- | --- |
| `Zend_Form_Element_Text` | 文本输入字段 |
| `Zend_Form_Element_Hidden` | 隐藏字段 |
| `Zend_Form_Element_Password` | 密码字段 |
| `Zend_Form_Element_Radio` | 单选按钮 |
| `Zend_Form_Element_Checkbox` | 复选框 |
| `Zend_Form_Element_MultiCheckbox` | 一组相关的复选框 |
| `Zend_Form_Element_Select` | 选择列表（单选） |
| `Zend_Form_Element_MultiSelect` | 选择列表（多选） |
| `Zend_Form_Element_Textarea` | 文本区域输入字段 |
| `Zend_Form_Element_File` | 文件输入字段 |
| `Zend_Form_Element_Image` | 图像 |
| `Zend_Form_Element_Button` | 按钮 |
| `Zend_Form_Element_Hash` | 唯一字符串（用于会话识别） |
| `Zend_Form_Element_Captcha` | 验证码（用于垃圾邮件过滤） |
| `Zend_Form_Element_Reset` | 重置按钮 |
| `Zend_Form_Element_Submit` | 提交按钮 |

表 3-1 Zend Framework 的表单元素类

```php
$name = new Zend_Form_Element_Text('name');
$name->setLabel('First name:')
  ->setOptions(array('id' => 'fname'));

// 创建密码输入
$pass = new Zend_Form_Element_Password('pass');
$pass->setLabel('Password:')
  ->setOptions(array('id' => 'upass'));

// 创建隐藏输入
$uid = new Zend_Form_Element_Hidden('uid');
$uid->setValue('49');

// 创建用于注释的文本区域
$comment = new Zend_Form_Element_Textarea('comment');
$comment->setLabel('Comment:')
  ->setOptions(array(
  'id' => 'comment',
  'rows' => '10',
  'cols' => '30',
));

// 将元素附加到表单
$this->addElement($name)
  ->addElement($pass)
  ->addElement($uid)
  ->addElement($comment);
```

图 3-3 展示了执行结果。

# 单选按钮和复选框

单选按钮由`Zend_Element_Radio`类表示，而复选框由`Zend_Element_Checkbox`类表示。以下是这两个类用法的示例：

> 图 3-3 带有包含文本和隐藏元素的表单

```php
<?php
class Form_Example extends Zend_Form
{
  public function init()
  {
    // 初始化表单
    $this->setAction('/sandbox/example/form')
      ->setMethod('post');

    // 创建名称的文本输入
    $name = new Zend_Form_Element_Text('name');
    $name->setLabel(array('id' => 'fname'));

    // 创建种类型的单选按钮
    $type = new Zend_Form_Element_Radio('type');
    $type->setLabel('Membership type:')
      ->setMultiOptions(array(
        'silver' => 'Silver',
        'gold' => 'Gold',
        'platinum' => 'Platinum'
      ))
      ->setOptions(array('id' => 'mtype'));

    // 创建订阅时事的复选框
    $subscribe = new Zend_Form_Element_Checkbox('subscribe');
    $subscribe->setLabel('Subscribe to newsletter')
      ->setCheckedValue('yes')
      ->setUncheckedValue('no');

// 将元素附加到表单
$this->addElement($name)
->addElement($type)
->addElement($subscribe);
}
```

`Zend_Form_Element_Radio`对象的`setMultiOptions()`方法接受一个数组，并使用它设置可用单选按钮列表。数组的键代表将要提交的值，对应的值代表每个选项的可读标签。同样，`Form_Element_Checkbox`对象的`setCheckedValue()`和`setUncheckedValue()`方法允许您自定义元素已选中和未选中状态下的值。默认情况下，这些值分别被设置为 1 和 0。

图 3-4 展示了执行结果。

如果你希望用户从某些选项中选择，`Zend_Form_Element_MultiCheckbox`类比`Zend_Form_Checkbox`类更好，因为它暴露了`setMultiOptions()`方法，允许选择多个项目。生成的集合随后被格式化为数组。以下是它的用法示例：

```php
<?php
class Form_Example extends Zend_Form
{
    public function __construct()
    {
        // 初始化表单
        $this->setAction('/sandbox/example/form')
            ->setMethod('post');

        // 创建名称的文本输入
        $name = new Zend_Form_Element_Text('name');
        $name->setLabel('Name:')
            ->setOptions(array('id' => 'fname'));

        // 创建种类型的单选按钮
        $type = new Zend_Form_Element_Radio('type');
        $type->setLabel('Pizza crust;');
        ->setMultiOptions(array(
          'thin' => 'Thin',
          'thick' => 'Thick'
        ));

// 创建配料的复选框
$toppings = new Zend_Form_Element_Checkbox('toppings');
$toppings->setLabel('Toppings:')
  ->setCheckedValue('yes')
  ->setUncheckedValue('no');

// 将元素附加到表单
$this->addElement($name)
->addElement($type);
}
```

图 3-4 带有单选按钮和复选框

## 第 3 章：使用表单

### 选择列表

单选和多选列表通过`Zend_Form_Select`和`Zend_Form_MultiSelect`类支持，它们暴露了`setMultiOptions()`方法，用于设置可用选项列表。以下示例演示了两种类型：



```php
<?php
class Form_Example extends Zend_Form
{
  public function init()
  {
    // 初始化表单
    $this->setAction('/sandbox/example/form')
      ->setMethod('post');

    // 创建名称的文本输入
    $name = new Zend_Form_Element_Text('name');
    $name->setLabel('Name:')
      ->setOptions(array('id' => 'fname'));

    // 创建源地选择列表
    $from = new Zend_Form_Element_Select('from');
    $from->setLabel('Travelling from:')
      ->setMultiOptions(array(
        'IT' => 'Italy',
        'US' => 'United States',
        'DE' => 'Germany',
        'FR' => 'France',
        'UK' => 'United Kingdom',
        'SG' => 'Singapore',
        'TR' => 'Turkey',
        'DK' => 'Denmark',
        'ES' => 'Spain',
        'PT' => 'Portugal',
        'RU' => 'Russia',
      ));

    // 创建目的地多选列表
    $to = new Zend_Form_Element_MultiSelect('to');
    $to->setLabel('Travelling to:')
      ->setMultiOptions(array(
        'IN' => 'India',
        'PL' => 'Poland',
      ));

    // 将元素附加到表单
    $this->addElement($name)
      ->addElement($from)
      ->addElement($to);
  }
}
```

图 3-5 展示了执行结果。

### 文件上传

如果你希望通过表单上传一个或多个文件，你需要使用`Zend_Element_File`类，它提供了一个可浏览的文件输入。以下是它的示例：

```php
<?php
class Form_Example extends Zend_Form
{
  public function init()
  {
    // 初始化表单
    $this->setAction('/sandbox/example/form')
      ->setEncoding('multipart/form-data')
      ->setMethod('post');

    // 创建用于上传照片的文件输入
    $photo = new Zend_Element_File('photo');
    $photo->setLabel('Photo:')
      ->setDestination('/tmp/upload/');

    // 将元素附加到表单
    $this->addElement($photo);
  }
}
```

> **注意**
>
> 记得将表单编码设置为`multipart/form-data`，以便表单上传被正确处理。这可以通过表单对象的`setEncoding()`方法来实现。

图 3-6 展示了它的样子。

图 3-6 带有文件输入字段的表单

### 按钮

每个表单都需要一个提交按钮以及一个重置按钮。这两个关键的表单元素分别由`Zend_Form_Element_Submit`和`Zend_Form_Element_Reset`类表示，它们将在下一个列表中演示：

```php
<?php
class Form_Example extends Zend_Form
{
    public function init()
    {
        // 初始化表单
        $this->setAction('/sandbox/example/form')
        ->setMethod('post');

        // 创建标题的文本输入
```

```php
$title = new Zend_Form_Element_Text('title')
$title->setLabel('Title:')
   ->setOptions(array('size' => '35'));
```

```php
// 创建提交按钮
$submit = new Zend_Form_Element_Submit('submit');
$submit->setLabel('Submit');
```

```php
// 创建重置按钮
$reset = new Zend_Form_Element_Reset('reset')
$reset->setLabel('Cancel');
```

```php
// 将元素添加到表单
$this->addElement($title)
   ->addElement($submit)
   ->addElement($reset)
}
```

图 3-8 展示了生成的输出。如果你想要一个更通用的表单按钮，可以在`Zend_Form_Element_Button`类中找到，它提供了一个简单的、可点击的表单按钮，适用于许多不同的用途。图像按钮可以使用`Zend_Form_Element_Image`类生成；使用`setImage`方法来指定按钮的源图像。这里是此类图片的示例：

![](img/222e7e58871b088cc6397852e1452b57_80_0.png)

```php
<?php
class Form_Example extends Zend_Form
{
    public function init()
    {
        // 初始化表单
        $this->setAction('/sandbox/example/form')
           ->setMethod('post');

// 创建标题的文本输入
$title = new Zend_Form_Element_Text('title')
$title->setLabel('Title:')
   ->setOptions(array('size' => '35'));
```

```php
// 创建图像提交按钮
$submit = new Zend_Form_Element_Image('submit')
$submit->setImage('/images/submit.jpg');
```

```php
// 将元素添加到表单
$this->addElement($title)
->addElement($submit);
}
```

图 3-9 展示了生成的输出。

### Hash 和 CAPTCHA 字段

图 3-9 带有图像按钮的表单

Zend Framework 使用两个“特殊”表单元素来辅助维护输入安全：Hash 和 CAPTCHA 元素。它们分别由`Zend_Form_Hash`和`Zend_Form_Captcha`类表示。

Hash 元素使用盐值（salt）为表单生成一个唯一的密钥并将其存储在 session 中。当表单提交时，随表单提交的 hash 值将自动与 session 中存储的值进行比较。如果找到匹配项，则认为表单提交是真实的。如果不匹配，则可以合理推断表单已被劫持并正被用于跨站请求伪造（CSRF）攻击。以下是使用该元素的示例：

```php
<?php
class Form_Example extends Zend_Form
{
    public function init()
    {
        // 初始化表单
        $this->setAction('/sandbox/example/form')
            ->setMethod('post');

        // 创建数量的文本输入
        $cc = new Zend_Form_Element_Text('ccanum');
        $cc->setLabel('Credit card number:')
            ->setOptions(array('size' => '16'));

        // 创建金额的文本输入
        $amount = new Zend_Form_Element_Text('amount');
        $amount->setLabel('Payment amount:')
            ->setOptions(array('size' => '4'));

        // 创建哈
        $hash = new Zend_Form_Element_Hash('hash');
        $hash->setSalt('hf23hflw03jj');

        // 创建提交按钮
        $submit = new Zend_Form_Element_Submit('submit');
        $submit->setLabel('Submit');

        // 将元素添加到表单
$this->addElement($cc)
->addElement($amount)
->addElement($hash)
->addElement($submit);
```

CAPTCHA 元素会自动生成 CAPTCHA 验证输入，这是一个过滤自动化表单提交的有用工具。越来越多的网站正在使用 CAPTCHA 来减少通过在线收到的虚假注册和/或垃圾信息数量。虽然手动生成和验证 CAPTCHA 是一个繁琐的过程，但`Zend_Form_Element_Captcha`让它变得像在表单中添加几行代码一样简单。这里是一个示例：

```php
<?php
class Form_Example extends Zend_Form
{
    public function init()
    {
        // 初始化表单
        $this->setAction('/sandbox/example/form')
            ->setMethod('post');

        // 创建用户名的文本输入
        $name = new Zend_Form_Element_Text('username');
        $name->setLabel('Username:')
            ->setOptions(array('size' => '16'));
    }
}
```

### 什么是攻击，我该如何防止它？

**问：** 什么是 CSRF 攻击，

**答：** 通常，用户访问受保护的 Web 网站并验证其/她的访问凭据，生成一个用户会话，并在每次请求时从 session 数据中验证访问凭据。CSRF 攻击涉及劫持已验证的用户会话并利用用户与主机应用程序之间已存在的隐式信任关系来隐形地传输请求。通过为每个表单使用唯一的哈希，开发者能够让未经授权的实体难以代表用户执行操作。

### 设置必填项和默认值

你可以通过调用`setRequired()`方法并传递`true`参数将输入元素标记为必填项。这里有一个示例：

```php
<?php
class Form_Example extends Zend_Form
{
    public function init()
    {
        // 初始化表单
        $this->setAction('/sandbox/example/form')
          ->setMethod('post');

// 创建密码输入
$pass = new Zend_Form_Element_Password('password')
$pass->setLabel('Password:')
    ->setOptions(array('size' => '16'))
    ->setRequired(true);

// 创建验证码
$captcha = new Zend_Form_Element_Captcha('captcha',
    array('type' => 'simple'));
$captcha->setLabel('Verification:');

// 创建提交按钮
$submit = new Zend_Form_Element_Submit('submit')
$submit->setLabel('Sign Up');

// 将元素添加到表单
$this->addElement($name)
->addElement($pass)
->addElement($captcha)
->addElement($submit);
```

当你对输入字段使用`setRequired()`方法时，Zend_Form 会自动为该字段附加`NotEmpty`验证器。结果是，如果在提交表单时字段为空，将出现一条错误消息。图 3-11 展示了结果。

> **提示**
>
> 你可以通过显式调用元素的`autoInsertNotEmptyValidator(false)`来告诉 Zend_Form 不要为必填元素附加`NotEmpty`验证器。验证器将在下一节详细讨论。

你可以通过调用元素对象的`setValue()`方法传递默认值，或调用表单对象的`setDefault()`方法传递默认值数组来为元素附加默认值。对于文本输入字段，可以是任何字符串值；

CAPTCHA（全自动区分计算机与图灵测试）是一种用于识别连接另一端实体是人类还是计算机的常用响应测试。在 Web 上，CAPTCHA 的典型形式是扭曲的字母数字序列，其原理是计算机无法看到扭曲，但具有更感知能力的人类能够识别该序列。此类 CAPTCHA 通常附加到 Web 上的输入表单（例如用户注册表单），并且在处理输入之前必须正确解决。

# 68 Zend Framework：初学者指南

对于单选按钮和选择列表，它持有所选项的索引。这里有一个示例，展示了这两种方法：

```php
<?php
class Form_Example extends Zend_Form
{
    public function init()
    {
        // 初始化表单
        $this->setAction('/sandbox/example/form')
            ->setMethod('post');

        //为姓名创建文本输入框
        $name = new Zend_Form_Element_Text('name');
        $name->setName('Name:')
            ->setOptions(array('size' => '35'))
            ->setRequired(true)
            ->setValue('Enter your name');

        //为地址创建电子邮件输入框
        $email = new Zend_Form_Element_Text('email');
        $email->setLabel('Email address:
        $email->setOptions(array('size' => '50'))
            ->setRequired(true)
            ->setValue('Enter your email address');

        //为类型创建单选按钮
        $type = new Zend_Form_Element_Radio('type');
        $type->setLabel('Membership type:')
            ->setMultiOptions(array(
                'silver' => 'Silver',
                'gold' => 'Gold',
                'platinum' => 'Platinum'
            ));

        //为新闻订阅创建复选框
        $subscribe = new Zend_Form_Element_Checkbox('subscribe');
        $subscribe->setLabel('Subscribe to newsletter')
            ->setCheckedValue('yes')
            ->setUncheckedValue('no');

        //为来源国家创建选择列表
        $from = new Zend_Form_Element_Select('from');
        $from->setLabel('Country:')
            ->setMultiOptions(array(
                'IN' => 'India',
                'US' => 'United States',
                'DE' => 'Germany',
                'FR' => 'France'
            ));
```

# 第 3 章：处理表单 69

```php
'UK' => 'United Kingdom'

));
```



```php
// 创建提交按钮
$submit = new Zend_Form_Element_Submit(
    array('class' => 'submit')
);
$submit->setLabel('Sign Up');

// 将元素添加到表单
$this->addElement($name)
    ->addElement($email)
    ->addElement($type)
    ->addElement($from)
    ->addElement($subscribe)
    ->addElement($submit);

// 设置默认值
$this->setDefaults(array(
    'type' => 'platinum',
    'subscribe' => 'yes',
    'from' => 'FR'
));
```

图 3-12 展示了结果的外观。

### 示例表单

![](img/222e7e58871b088cc6397852e1452b57_87_0.png)

图 3-12 使用默认值渲染的表单

# 70 Zend Framework：初学者指南

## 过滤和验证表单输入

作为 Web 应用程序开发者，有一个必须面对的不愉快的事实：总有人会通过发现你代码中的漏洞并从中取乐，同时利用这些漏洞达到恶意目的。因此，开发者为保护应用程序所能做的最重要的事情之一，就是对通过程序的所有输入进行适当的过滤和验证。

接下来的章节将讨论 Zend Framework 中提供的过滤和验证工具，以及如何将它们与 Web 表单结合使用以确保应用程序的安全。

## 使用输入过滤器

大多数时候，输入攻击包括向你的应用程序发送明显贬值的数值，从而“欺骗”它去执行它真的、非常不应该做的事情。这类攻击的一个常见例子是 SQL 注入攻击，攻击者通过嵌入在表单输入中的 SQL 查询来操纵你的数据库。因此，开发者在使用用户提供的任何输入之前，必须做的重要工作之一就是通过移除其中的任何特殊字符或符号来对其进行“清理”。

PHP 有多种函数来协助开发者完成清理输入的任务。例如，`htmlspecialchars()` 函数会转义输入中的特殊字符（如引号和反斜杠），使其能够安全地存数据库；`strip_tags()` 函数会移除字符串中所有的 HTML 和 PHP 标签，只返回 ASCII 内容。还有一个 `htmlspecialchars()` 函数（此处），通常用于将 `&`、`<` 和 `>` 等特殊字符替换为相应的 HTML 实体值，使其变得无害。

这里是使用 `htmlspecialchars()` 函数清理输入的示例：

```php
<?php
// 清理后的数据数组
$sanitized = array();

// 从 POST 输入中移除标签
if (isset($_POST['name']) && !empty($_POST['name'])) {
    $sanitized['name'] = htmlspecialchars($_POST['name']);
}

// 处理代码 //
?>
```

在过滤输入时，Zend Framework 提供了一套完整的输入过滤器，这些过滤器既可以通过 `addFilter()` 方法附加到表单元素，也可以作为独立基础用于即时的输入清理。这里是在文本输入字段上使用 `EntitiesFilter` 的示例：

```php
<?php
class Form_Example extends Zend_Form
{
    public function init()
    {
        // 初始化表单
        $this->setAction('/sandbox/example/form')
            ->setMethod('post');

        // 为用户名创建文本输入框
        // 过滤特殊字符
        $name = new Zend_Form_Element_Text('name');
        $name->setLabel('Username:')
            ->setOptions(array('size' => '16'))
            ->addFilter('Alpha');

        // 创建提交按钮
        $submit = new Zend_Form_Element_Submit('submit');

        // 将元素添加到表单
        $this->addElement($name)
            ->addElement($submit);
    }
}
```

你可以向 `addFilter()` 方法传递类实例，如下所示：

```php
<?php
class Form_Example extends Zend_Form
{
    public function init()
    {
        // 初始化表单
        $this->setAction('/sandbox/example/form')
            ->setMethod('post');

        // 为用户名创建文本输入框
        // 过滤特殊字符
        $name = new Zend_Form_Element_Text('name');
        $name->setLabel('Username:')
            ->setOptions(array('size' => '16'))
            ->addFilter('HtmlEntities');

        // 创建提交按钮
        $submit = new Zend_Form_Element_Submit('submit');

        // 将元素添加到表单
        $this->addElement($name)
            ->addElement($submit);
    }
}
```

有些过滤器支持额外的选项，可以通过多次调用 `addFilter()` 方法（每次使用不同的过滤器名称），或者通过 `addFilters()` 方法并传递一个过滤器列表来实现。

# 90 Zend Framework

# 72 Zend Framework：初学者指南

```php
addElement($submit)
```

你可以向 `addFilter()` 方法传递一个数组，或者如果你使用类实例，考虑下面的示例，它使用了 `Alpha` 过滤器：

```php
<?php
class Form_Example extends Zend_Form
{
    public function init()
    {
        // 初始化表单
        $this->setAction('/sandbox/example/form')
            ->setMethod('post');

        // 为姓名创建文本输入框
        // 允许空格
        $name = new Zend_Form_Element_Text('name');
        $name->setLabel('Name:')
            ->setOptions(array('size' => '35'))
            ->addFilter('Alpha', array('allowWhitespace' => true));

        // 创建提交按钮
        $submit = new Zend_Form_Element_Submit('submit');

        // 将元素添加到表单
        $this->addElement($name)
            ->addElement($submit);
    }
}
```

有些过滤器支持额外的选项，可以通过多次调用 `addFilter()` 方法（每次使用不同的过滤器名称），或者通过 `addFilters()` 方法并传递一个过滤器列表来实现。

```php
<?php
class Form_Example extends Zend_Form
{
    public function init()
    {
        // 初始化表单
        $this->setAction('/sandbox/example/form')
            ->setMethod('post');

        // 为姓名创建文本输入框
        // 允许空格
        $name = new Zend_Form_Element_Text('name');
        $name->setLabel('Name:')
            ->setOptions(array('size' => '35'))
            ->addFilter('Alpha', array('allowWhitespace' => true));

        // 创建提交按钮
        $submit = new Zend_Form_Element_Submit('submit');

        // 将元素添加到表单
        $this->addElement($name)
            ->addElement($submit);
    }
}
```

```php
<?php
class Form_Example extends Zend_Form
{
    public function init()
    {
        // 初始化表单
        $this->setAction('/sandbox/example/form')
            ->setMethod('post');

        // 为姓名创建文本输入框
        // 允许空格
        $name = new Zend_Form_Element_Text('name');
        $name->setLabel('Name:')
            ->setOptions(array('size' => '35'))
            ->addFilter('Alpha', array('allowWhitespace' => true));

        // 创建提交按钮
        $submit = new Zend_Form_Element_Submit('submit');

        // 将元素添加到表单
        $this->addElement($name)
            ->addElement($submit);
    }
}
```

```php
<?php
class Form_Example extends Zend_Form
{
    public function init()
    {
        // 初始化表单
        $this->setAction('/sandbox/example/form')
            ->setMethod('post');
    }
}
```

作为 Web 应用程序开发者，有一个必须面对的不愉快的事实：总有人会通过发现你代码中的漏洞并从中取乐，同时利用这些漏洞达到恶意目的。因此，开发者为保护应用程序所能做的最重要的事情之一，就是对通过程序的所有输入进行适当的过滤和验证。

接下来的章节将讨论 Zend Framework 中提供的过滤和验证工具，以及如何将它们与 Web 表单结合使用以确保应用程序的安全。

### 使用输入过滤器

大多数时候，输入攻击包括向你的应用程序发送明显贬值的数值，从而“欺骗”它去执行它真的、非常不应该做的事情。这类攻击的一个常见例子是 SQL 注入攻击，攻击者通过嵌入在表单输入中的 SQL 查询来操纵你的数据库。因此，开发者在使用用户提供的任何输入之前，必须做的重要工作之一就是通过移除其中的任何特殊字符或符号来对其进行“清理”。

PHP 有多种函数来协助开发者完成清理输入的任务。例如，`htmlspecialchars()` 函数会转义输入中的特殊字符（如引号和反斜杠），使其能够安全地存数据库；`strip_tags()` 函数会移除字符串中所有的 HTML 和 PHP 标签，只返回 ASCII 内容。还有一个 `htmlspecialchars()` 函数，通常用于将 `&`、`<` 和 `>` 等特殊字符替换为相应的 HTML 实体值，使其变得无害。

这里是使用 `htmlspecialchars()` 函数清理输入的示例：

```php
<?php
// 清理后的数据数组
$sanitized = array();

// 从 POST 输入中移除标签
if (isset($_POST['name']) && !empty($_POST['name'])) {
    $sanitized['name'] = htmlspecialchars($_POST['name']);
}

// 处理代码 //
?>
```

在过滤输入时，Zend Framework 提供了一套完整的输入过滤器，这些过滤器既可以通过 `addFilter()` 方法附加到表单元素，也可以作为独立基础用于即时的输入清理。这里是在文本输入字段上使用 `EntitiesFilter` 的示例：

```php
<?php
class Form_Example extends Zend_Form
```

# 68 Zend Framework：初学者指南

单选按钮和选择列表，它持有所选项的索引。这里有一个示例，展示了这两种方法：

```php
<?php
class Form_Example extends Zend_Form
{
    public function init()
    {
        // 初始化表单
```



# 第3章：处理表单

## 示例表单

```php
$this->setAction('/sandbox/example/form')
    ->setMethod('post');

// 为姓名创建文本输入框
$name = new Zend_Form_Element_Text('name');
$name->setName('Name:')
    ->setOptions(array('size' => '35'))
    ->setRequired(true)
    ->setValue('Enter your name');

// 为地址创建电子邮件输入框
$email = new Zend_Form_Element_Text('email');
$email->setLabel('Email address:');
$email->setOptions(array('size' => '50'))
    ->setRequired(true)
    ->setValue('Enter your email address');

// 为类型创建单选按钮
$type = new Zend_Form_Element_Radio('type');
$type->setLabel('Membership type:')
    ->setMultiOptions(array(
        'silver' => 'Silver',
        'gold' => 'Gold',
        'platinum' => 'Platinum'
    ));

// 为新闻订阅创建复选框
$subscribe = new Zend_Form_Element_Checkbox('subscribe');
$subscribe->setLabel('Subscribe to newsletter')
    ->setCheckedValue('yes')
    ->setUncheckedValue('no');

// 为来源国家创建选择列表
$from = new Zend_Form_Element_Select('from');
$from->setLabel('Country:')
    ->setMultiOptions(array(
        'IN' => 'India',
        'US' => 'United States',
        'DE' => 'Germany',
        'FR' => 'France',
        'UK' => 'United Kingdom'
    ));

// 创建提交按钮
$submit = new Zend_Form_Element_Submit(
    array('class' => 'submit')
);
$submit->setLabel('Sign Up');

// 将元素添加到表单
$this->addElement($name)
    ->addElement($email)
    ->addElement($type)
    ->addElement($from)
    ->addElement($subscribe)
    ->addElement($submit);

// 设置默认值
$this->setDefaults(array(
    'type' => 'platinum',
    'subscribe' => 'yes',
    'from' => 'FR'
));
```

图 3-12 展示了结果的外。

![](img/222e7e58871b088cc6397852e1452b57_87_0.png)

图 3-12 使用默认值渲染的表单

## 过滤和验证表单输入

作为 Web 应用程序开发者，有一个必须面对的不愉快的事实：总有人会通过发现你代码中的漏洞并从中取乐，同时利用这些漏洞达到恶意目的。因此，开发者为保护应用程序所能做的最重要的事情之一，就是对通过程序的所有输入进行适当的过滤和验证。

接下来的章节将讨论 Zend Framework 中提供的过滤和验证工具，以及如何将它们与 Web 表单结合使用以确保应用程序的安全。

### 使用输入过滤器

大多数时候，输入攻击包括向你的应用程序发送明显贬值的数值，从而“欺骗”它去执行它真的、非常不应该做的事情。这类攻击的一个常见例子是 SQL 注入攻击，攻击者通过嵌入在表单输入中的 SQL 查询来操纵你的数据库。因此，开发者在使用用户提供的任何输入之前，必须做的重要工作之一就是通过移除其中的任何特殊字符或符号来对其进行“清理”。

PHP 有多种函数来协助开发者完成清理输入的任务。例如，`htmlspecialchars()` 函数会转义输入中的特殊字符（如引号和反斜杠），使其能够安全地存数据库；`strip_tags()` 函数会移除字符串中所有的 HTML 和 PHP 标签，只返回 ASCII 内容。还有一个 `htmlspecialchars()` 函数，通常用于将 `&`、`<` 和 `>` 等特殊字符替换为相应的 HTML 实体值，使其变得无害。

这里是使用 `htmlspecialchars()` 函数清理输入的示例：

```php
<?php
// 清理后的数据数组
$sanitized = array();

// 从 POST 输入中移除标签
if (isset($_POST['name']) && !empty($_POST['name'])) {
    $sanitized['name'] = htmlspecialchars($_POST['name']);
}

// 处理代码 //
?>
```

在过滤输入时，Zend Framework 提供了一套完整的输入过滤器，这些过滤器既可以通过 `addFilter()` 方法附加到表单元素，也可以作为独立基础用于即时的输入清理。这里是在文本输入字段上使用 `EntitiesFilter` 的示例：

```php
<?php
class Form_Example extends Zend_Form
{
  public function init() {
    // 初始化表单
    $this->setAction('/sandbox/example/form')
      ->setMethod('post');

    // 为用户名创建文本输入框
    // 过滤特殊字符
    $name = new Zend_Form_Element_Text('name');
    $name->setLabel('Username:')
      ->setOptions(array('size' => '16'))
      ->addFilter('Alpha');

    // 创建提交按钮
    $submit = new Zend_Form_Element_Submit('submit');

    // 将元素添加到表单
    $this->addElement($name)
      ->addElement($submit);
  }
}
```

你可以向 `addFilter()` 方法传递类实例，如下所示：

```php
<?php
class Form_Example extends Zend_Form {
  public function init() {
    // 初始化表单
    $this->setAction('/sandbox/example/form')
      ->setMethod('post');

    // 为用户名创建文本输入框
    // 过滤特殊字符
    $name = new Zend_Form_Element_Text('name');
    $name->setLabel('Username:')
      ->setOptions(array('size' => '16'))
      ->addFilter('HtmlEntities');

    // 创建提交按钮
    $submit = new Zend_Form_Element_Submit('submit');

    // 将元素添加到表单
    $this->addElement($name)
      ->addElement($submit);
  }
}
```

有些过滤器支持额外的选项，可以通过多次调用 `addFilter()` 方法（每次使用不同的过滤器名称），或者通过 `addFilters()` 方法并传递一个过滤器列表来实现。

```php
<?php
class Form_Example extends Zend_Form
{
    public function init() {
        // 初始化表单
        $this->setAction('/sandbox/example/form')
            ->setMethod('post');
```

猜想接下来会发生什么并不难。应用程序将执行几次内部计算，并尝试将应付总金额除以指定的期数（term）。由于在这种情况下期数是一个字符串，PHP 将其强制转换为数字 0，从而产生除以零的错误。随之出现的一系列难陋的错误信息可能会让即使是见老不惯的开发者也感到困惑；更重要的是，如果输入值也被原样保存到数据库中，那么每当对该记录进行计算时，错误都会发生。考虑到数据库中散布着数百条包含类似错误的记录，你很快就会发现缺乏适当的输入验证会如何严重损害应用程序。

PHP 提供了各种函数来帮助开发者完成输入验证的任务。例如，`is_numeric()` 函数用于测试一个值是否为数字，而 `ctype_alpha()` 和 `ctype_alnum()` 函数可以用于处理字母字符串和字母数字字符串。还有 `filter_var()` 函数，可用于测试地址和 URL 的有效性，以及 `preg_match()` 函数，允许使用正则表达式进行模式验证。以下是这些函数的用法示例：

```php
<?php
// 定义有效数据的数组
$valid = array();

// 检查年龄是否为数字
if (is_numeric(trim($_POST['age']))) {
    $valid['age'] = trim($_POST['age']);
} else {
    die('ERROR：年龄不是数字.');
}

// 检查名字是否有效
if (isset($_POST['firstname']) && ctype_alpha($_POST['firstname'])) {
    $valid['firstname'] = trim($_POST['firstname']);
} else {
    die('ERROR：名字不存在或无效。');
}

// 检查邮箱地址是否有效
if (isset($_POST['email']) && filter_var($_POST['email'], FILTER_VALIDATE_EMAIL)) {
    $valid['email'] = trim($_POST['email']);
} else {
    die('ERROR：邮箱地址不存在或无效.');
}

// 此处为处理代码 //
?>
```

作为过滤器，Zend Framework 自带了大量的预定义输入验证器，统称为 `Zend_Validate`。这些验证器可以通过 `addValidator()` 方法附加到表单元素上，也可以临时即时使用。验证器特定的选项可以作为键值对的关联数组传递给 `addFilter()` 方法的第三个参数，如下所示：

```php
<?php
class Form_Example extends ZendForm
{
    public function init()
    {
        // 初始化表单
        $this->setAction('/sandbox/example/form')
             ->setMethod('post');

        // 创建年龄的文本输入
        // 应只包含 1 到 100 之间的整数值
        $age = new Zend_Form_Element_Text('age');
        $age->setLabel('Age:')
             ->setOptions(array('size' => '4'))
             ->setRequired(true)
             ->addValidator('Int')
             ->addValidator('Between', false, array(1,100));

        // 创建名字的文本输入
        // 应只包含字母数字字符和空格
        $name = new Zend_Form_Element_Text('name');
        $name->setLabel('First name:')
             ->setOptions(array('size' => '16'))
             ->setRequired(true)
             ->addValidator('Alpha', false, array('allowWhiteSpace' => true));

        // 创建邮箱地址的文本输入
        // 应包含一个有效的邮箱地址
        $email = new Zend_Form_Element_Text('email');
        $email->setLabel('Email address:')
             ->setOptions(array('size' => '16'))
             ->setRequired(true)
             ->addValidator('EmailAddress');

        // 创建提交按钮
        $submit = new Zend_Form_Element_Submit('submit');
        $submit->setLabel('Sign Up');

        // 将元素附加到表单
        $this->addElement($age)
             ->addElement($email)
             ->addElement($submit);
    }
}
```

与过滤器一样，验证器也可以指定为相应 `Zend_Validate*` 类的实例，并将验证器选项作为参数传递给对象的构造函数。下一个示例与上一个相同，说明了这种方法。

```php
<?php
class Form_Example extends Zend_Form {
    public function init() {
        // 初始化表单
        $this->setAction('/sandbox/example/form')
            ->setMethod('post');

        // 创建年龄的文本输入
        // 应只包含 1 到 100 之间的整数值
        $age = new Zend_Form_Element_Text('age')
            ->setLabel('Age:')
            ->setOptions(array('size' => '4'))
            ->setRequired(true)
            ->addValidator(new Zend_Validate_Int())
            ->addValidator(new Zend_Validate_Between(1,100));

        // 创建名字的文本输入
        // 应只包含字母字符和空格
        $name = new Zend_Form_Element_Text('name')
            ->setLabel('First name:')
            ->setOptions(array('size' => '16'))
            ->setRequired(true)
            ->addValidator(new Zend_Validate_Alpha(true));
```



```php
// 创建邮箱地址的文本输入
// 应包含一个有效的邮箱地址
$email = new Zend_Form_Element_Text('email')
    ->setLabel('Email address:')
    ->setOptions(array('size' => '16'))
    ->setRequired(true)
    ->addValidator(new Zend_Validate_EmailAddress());

// 创建提交按钮
$submit = new Zend_Form_Element_Submit('submit')
    ->setLabel('Sign Up');

// 将元素附加到表单
$this->addElement($age)
     ->addElement($email)
     ->addElement($submit);
}
}
```

图 13 展示了提交无效值表单的结果。

| 验证器名称 | 描述 |
|---|---|
| `NotEmpty` | 如果为空则返回 `false` |
| `StringLength` | 如果长度不符合返回 `false` |
| `InArray` | 如果不在数组内返回 `false` |
| `Identical` | 如果不匹配返回 `false` |
| `Alnum` | 如果不包含字母数字则返回 `false` |
| `Alpha` | 如果不包含字母返回 `false` |
| `Int` | 如果不是整数返回 `false` |
| `Float` | 如果不是浮点数返回 `false` |
| `Hex` | 如果不是十六进制返回 `false` |
| `Digits` | 如果不包含数字返回 `false` |
| `Between` | 如果不在指定的范围内返回 `false` |

表 3-3 Zend Framework 包含的验证器

## 78 Zend Framework：入门指南

| 验证器名称 | 描述 |
|---|---|
| `GreaterThan` | 如果大于指定值则返回 `false` |
| `LessThan` | 如果小于指定值则返回 `false` |
| `Date` | 如果不是有效的日期返回 `false` |
| `EmailAddress` | 如果不符合标准邮箱地址返回 `false` |
| `Hostname` | 如果不符合标准主机名返回 `false` |
| `Ip` | 如果不符合标准 IP 地址返回 `false` |
| `Regex` | 如果不符合正则表达式返回 `false` |
| `Barcode` | 如果不是有效的条形码返回 `false` |
| `Cnum` | 如果不符合标准信用卡 Luhn 算法返回 `false` |
| `Iban` | 如果不是有效的 IBAN 号返回 `false` |
| `Exists` | 如果不存在返回 `false` |
| `Count` | 如果上传的文件数量不在指定范围内返回 `false` |
| `Size` | 如果上传的文件大小不在指定范围内返回 `false` |
| `FilesSize` | 如果上传的文件总大小不在指定范围内返回 `false` |
| `Extension` | 如果文件扩展名不匹配指定的项返回 `false` |
| `MimeType` | 如果文件 MIME 类型不匹配指定的项返回 `false` |
| `IsCompressed` | 如果不是压缩包文件返回 `false` |
| `IsImage` | 如果不是图片文件返回 `false` |
| `ImageSize` | 如果上传图片的尺寸不在指定范围内返回 `false` |
| `Crc32, Md5, Sha1, Hash` | 如果文件内容不匹配参数中的哈希值返回 `false`（支持 `crc32`、`md5` 和 `sha1` 算法） |
| `ExcludeExtension` | 如果文件扩展名匹配指定的项返回 `false` |
| `ExcludeMimetype` | 如果文件 MIME 类型匹配指定的项返回 `false` |
| `WordCount` | 如果上传文件中的单词数不在指定范围内返回 `false` |
| `Db_RecordExists` | 如果特定记录在指定的数据库和表中不存在则返回 `false` |
| `Db_NoRecordExists` | 如果特定记录在指定的数据库和表中则返回 `false` |

表 3-3 Zend Framework 包含的验证器（续）

### 提问专家

**Q：我已经在使用 JavaScript 对表单输入进行验证了。为什么我还需要用 PHP 来进行验证呢？**

**答：**使用 JavaScript 或 VBScript 等客户端脚本语言进行客户端输入验证是常见做法。然而，这种类型的客户端验证并不是万无一失的——如果用户在客户端禁用了 JavaScript，你所有的客户端代码都将失效。因此，将客户端验证（速度更快）与服务器端验证（安全性更高）结合起来是一个很好的主意。**

### 使用 Validator 和 Filter 链

`Zend_Filter` 和 `Zend_Validate` 组件最有趣的功能之一是它们支持链式（chaining）或堆叠（stacking）。本质上，这意味着你可以为单个输入元素附加多个过滤器，然后在提交表单时，这些过滤器会按顺序自动运行。下面的示例说明了如何设置一个过滤器链：

```php
<?php

// 为 name 创建文本输入框
// 过滤标签、实体和空白
$name = new Zend_Form_Element_Text('name');

$name->setLabel('First name:')
    ->setOptions(array('size' => '16'))
    ->setRequired(true)
    ->addFilter('StripTags')
    ->addFilter('HTMLEntity')
    ->addFilter('StringTrim')
    ->addFilter('ToLower');
```

在这个示例中，第一个过滤器从输入中删除 HTML，第二个过滤器对实体进行编码，第三个修剪两端的空白字符，第四个将结果转换为小写。这些过滤器按照它们在链中出现的顺序在输入值上执行。

验证器的工作方式类似，但多了一个属性。验证器链可以配置为：任何一个验证器的失败都会带上错误消息并终止整个链。这种行为由 `addValidator()` 方法的第二个参数控制，当该参数设置为 `true` 时，如果相应的验证器发生失败，将断开链。考虑下一个示例，它说明了这一点：

```php
<?php

// 为 age 创建文本输入框
// 应该包含 1 到 100 之间的整数值
$age = new Zend_Form_Element_Text('age');

$age->setLabel('Age:')
    ->setOptions(array('size' => '4'))
    ->setRequired(true)
    ->addValidator('NotEmpty', true)
    ->addValidator('Int', true)
    ->addValidator('Between', true, array(1, 100));
```

## 80 Zend Framework：入门指南

在这个示例中，任何一个验证器的失败都会断开链，剩余的验证器将不再被处理。例如，如果输入不是整数值，验证链将以 `Int` 验证器生成的错误消息终止，`Between` 验证器将不会执行。将其与下一个代码列表进行对比：

```php
<?php // 为 age 创建文本输入框

// 应该包含 1 到 100 之间的整数值
$age = new Zend_Form_Element_Text('age');

$age->setLabel('Age:')
    ->setOptions(array('size' => '4'))
    ->setRequired(true)
    ->addValidator('NotEmpty', false)
    ->addValidator('Int', false)
    ->addValidator('Between', false, array(1, 100));

?>
```

在这个版本中，即使其中一个验证器失败，剩余的验证器仍然会运行，任何后续失败生成的错误消息都将添加到消息栈中。这在图 3-14 和图 3-15 中有所体现，它们对比了这两个代码列表行为的差异。

**图 3-14** 验证器链，在第一次失败时断开

**图 3-15** 验证器链，在失败时不断开

**提示：**如果 Zend Framework 预定义的过滤器和验证器不能满足你的需求，记住你始终可以编写自己的。

### 获取和处理输入

在控制器中，你可以使用许多方法在提交后获取并处理输入：

- `isValid()` 方法检查输入是否有效并返回 `true` 或 `false`。
- 如果输入无效，`getMessages()` 方法返回错误列表。
- 如果输入有效，`getValue()` 方法获取值。
- `getUnfiltered()` 方法返回原始输入。
- `getValues()` 方法返回过滤后的值。

**提示：**下一个示例说明了这些方法通常如何在控制器中使用：

```php
<?php

class ExampleController extends Zend_Controller
{
    public function indexAction()
    {
        $form = new Example();
        $this->view->form = $form;

        if ($this->getRequest()->isPost()) {
            if ($form->isValid($this->getRequest())) {
                // 有效数据：保存到数据库
                $values = $form->getValues();
                $this->redirect('/form/success');
            } else {
                // 无效数据：显示表单
                $this->view->messages = $form->getMessages();
            }
        }
    }
}

?>
```

### 创建表单

有了背景知识，让我们来看看如何在实际应用程序中使用。接下来的部分将所学的内容应用于一个表单。

### 定义表单

首先，考虑输入表单的要求。它们并不复杂——用户只需要三个字段：姓名、电子邮件和消息。为了确保真实性以便管理员能够回复邮件、过滤自动提交并减少垃圾邮件发生，包含一个 CAPTCHA 会很不错——这使用 Zend_Form 非常简单。以下是表单定义的示例：

```php
<?php

class Form_Contact extends Zend_Form
{
    public function init()
    {
        // 初始化表单
        $this->setAction('/contact/index')
            ->setMethod('post');

        // 为 name 创建文本输入框
        $name = new Zend_Form_Element_Text('name');

        $name->setLabel('Name:')
            ->setOptions(array('size' => '35'))
            ->setRequired(true)
            ->addValidator('NotEmpty', true)
            ->addValidator('Alpha', true)
            ->addFilter('HTMLEntities')
            ->addFilter('StringTrim');

        // 为 email address 创建文本输入框
        $email = new Zend_Form_Element_Text('email');

        $email->setEmail('Email address:')
            ->setOptions(array('size' => '50'))
            ->setRequired(true)
            ->addValidator('NotEmpty', true)
            ->addValidator('EmailAddress', true)
            ->addFilter('HTMLToLower')
            ->addFilter('StringTrim');

        // 为消息主体创建文本输入框
        $message = new Zend_Form_Element_Textarea('message');

        $message->setLabel('Message:')
            ->setOptions(array('rows' => '8', 'cols' => '40'))
            ->setRequired(true)
            ->addValidator('NotEmpty', true)
            ->addFilter('HTMLEntities')
            ->addFilter('StringTrim');

        // 创建验证码
        $captcha = new Zend_Form_Element_Captcha('captcha', array(
            'captcha' => array(
                'captcha' => 'Image',
            )
        ));
```

## 84 Zend Framework：初学者指南

```php
        'wordLen' => 6,
        'timeout' => 300,
        'width' => 300,
        'height' => 100,
        'imgUrl' => '/captcha' . '../public/captcha',
        'imgDir' => APPLICATION_PATH . '/../../',
        'font' => APPLICATION_PATH . '/../../public/fonts/LiberationSansSansRegular.ttf',
    );

    $captcha->setLabel('验证码:');

    // 创建提交按钮
    $submit = new Zend_Form_Element_Submit('submit');

    $submit->setLabel('发送消息')
        ->setOptions(array('class' => 'submit'));

    // 将元素添加到表单
    $this->addElement($name)
        ->addElement($email)
        ->addElement($message)
        ->addElement($captcha)
        ->addElement($submit);
    }
}
?>
```




你应该对上述大部分代码非常熟悉。表单包含两个用于用户姓名和电子邮件的文本元素，一个用于消息正文的区域，以及一个用于验证的 CAPTCHA（验证码）元素。姓名和消息正文字段附加了 `Alpha` 和 `NotEmpty` 验证器，并使用 `EmailAddress` 验证器来检查电子邮件地址。所有字段都使用 `HTMLEntities` 验证器进行过滤，并使用 `StringToLower` 验证器将电子邮件转换为小写。

与之前章节中所示示例所传递的选项不同，此定义通过在杂乱的背景上动态重载随机字符序列生成了一个更复杂的 CAPTCHA。这种类型的 CAPTCHA 通常用于 Web 表单的自动化提交，这可能包含对象字符识别（OCR）算法，该算法可以“读取”叠加在清晰背景上的内容。传递给对象实例的选项包括 CAPTCHA 图像的尺寸、存储生成的 CAPTCHA 的磁盘位置、CAPTCHA 中的字符数量以及用于文本的字体文件。

### 注意

如果你正在使用无法重新分发的受版权保护字体，你应该将`$APP_DIR/public/fonts/`移动到服务器文档根目录之外的位置，例如`$APP_DIR/application/fonts/`，以确保字体不会通过网络浏览器公开访问。如果这样做，请记住同时更新应用代码以反映新路径。

## 第 3 章：处理表单

你会注意到上一个示例使用了自定义字体，并将生成的 CAPTCHA 存储在指定的目录中。相应的，也要创建`$APP_DIR/public/captcha/`和`$APP_DIR/public/fonts/`目录，并将必要的资源复制到这些位置。你可以在本章的代码归包中找到这些文件，可以从本书的配套网站`http://www.zf-beginners-guide.com`下载。

### 注意

示例中 CAPTCHA 使用的字体是 Liberation Sans 字体，它是 RedHat Inc. 在 2007 年根据 GNU 通用公共许可证向社区发布的一系列字体组成部分。用户可以根据 GNU GPL 的条款自由地使用、修改、复制和分发这些字体。

### 使用自定义命名空间

上一节中的定义使用了自定义命名空间“Square”，它作为类名的名前缀。对于你为应用空间创建的任何自定义对象或库，这是一个推荐的做法，因为它有助于避免你的定义与应用空间可能存在的其他定义之间的命名冲突。另一个好处是，如果你向 Zend Framework 的自动加载器注册了你的自定义命名空间，然后在应用目录结构中正确找到了你的定义，Zend Framework 将在运行时自动找到并加载它们。

考虑到这一点，将上述代码中的类定义保存到`$APP_DIR/library/Square/Form/Contact.php`，然后将以下指令添加到应用配置文件（如`$APP_DIR/application/configs/autoload.ini`），以向自动加载器注册 "Square" 命名空间：

```ini
autoloaderNamespaces[] = "Square_"
```

### 注意

如果你的类使用下划线分隔命名空间与类名的其余部分，那么在向 Zend Framework 自动加载器注册命名空间时，必须包含此下划线。

### 定义自定义路由

现在为新表单添加自定义路由的好时机。当你从编辑器中打开应用配置文件时，向其添加以下路由定义：

```ini
resources.router.routes.contact.route = /contact
resources.router.routes.contact.defaults.module = default
resources.router.routes.contact.defaults.controller = contact
resources.router.routes.contact.defaults.action = index
```

（续）

## 86 Zend Framework：初学者指南

根据第 2 章中讨论的内容，这对你来说应该非常熟悉——它设置了一个路由，使得对应用 URL`/contact`的请求由“default”模块的`ViewController::indexAction`处理。

### 定义控制器和视图

下一步是定义上述`ViewController::indexAction`。按照惯，此控制器应该位于`$APP_DIR/application/modules/default/controllers/ContactController.php`，并且看起来应该像这样：

```php
class ContactController extends Zend_Controller_Action
{
    public function __init()
    {
        $this->view->doctype('HTML1_STRICT');
    }

    public function indexAction()
    {
        $form = new Square_Form();
        $this->view->form = $form;

        if ($this->getRequest()->isPost()) {
            if ($form->isValid($this->getRequest()->getData())) {
                $values = $form->getValues();

                $mail = new Zend_Mail();
                $mail->setBodyText($values['message']);
                $mail->setFrom($values['email'], $values['name']);
                $mail->addTo('info@example.com');
                $mail->setSubject('Contact form');
                $mail->send();

                $this->helper('FlashMessenger')->addMessage('感谢。您的消息已成功发送。');
                $this->redirect('/contact/success');
            }
        }
    }

    public function successAction()
    {
        if ($this->helper('FlashMessenger')->getMessages()) {
            $this->view->messages = $this->helper('FlashMessenger')->getMessages();
        } else {
            $this->redirect('/');
        }
    }
}
```

## 第 3 章：处理表单

大部分工作由`indexAction()`方法完成，它创建了之前提到的`Square_Form`对象并将其附加到视图。当表单提交时，使用`isValid()`方法验证用户提交的内容。如果输入有效，将创建一个`Zend_Mail`实例，并将输入格式化为电子邮件消息发送到指定的电子邮件地址。一旦消息发送，控制将转移到`successAction()`方法，该方法返回一个成功视图。相反，如果输入无效，`isValid`方法将返回 false 并重新加载视图，同时带有指示来源的错误消息。`Square_Form`还会填充表单值，以确保用户不需要重新输入。此外，该控制器引入了一个新工具`FlashMessenger`助手，这是一个向用户显示消息状态的有用小助手。消息可以通过`addMessage()`方法添加到`FlashMessenger`对象中；这些消息存储在会话中，直到调用`getMessages()`方法检索时才会从会话中移除。这使得`FlashMessenger`成为在操作结束和随后渲染视图之间临时存储消息的场所，你将在书中到处看到它。

### 注意

为了让`Zend_Mail`对象的`send()`方法正常工作，邮件传输代理（如 sendmail）必须在`php.ini`文件中可用并配置正确。如果不是这样，消息传输将失败，`send()`将故障点抛出异常。

### 注意

你会注意到控制器的`init()`方法将视图的文档类型设为 XHTML 1.0 Strict。这是因为默认情况下，`Zend_Form`不产生良好的 XHTML 标记。通过这种方式设置文档类型可以强制它这样做。显然，你还需要两个视图，一个用于输入表单，另一个用于成功消息。按照惯，输入视图应该位于`$APP_DIR/default/views/scripts/index.php`。

```html
<h2>联系我们</h2>

<?php echo $this->form; ?>
```

## 88 Zend Framework：学者指南

这里是成功页面，按照约定，它应该存储在`$APP_DIR/application/modules/default/views/scripts/contact/success.php`：

```php
<h2>Success</h2>

<?php echo implode($this->messages); ?>
```

### 更新主布局（Master Layout）

现在剩下的工作就是更新应用`$url()`助手方法中的导航链接了。要完成这一点，请更新主布局文件，即`$APP_DIR/application/layouts/master.php`，并对加粗显示的内容进行修改：

```html
<!DOCTYPE html PUBLIC "//W3C//DTD HTML 1.0//Strict//EN"
"http://www.w3.org/TR/html1/html-strict.dtd">

<html xmlns="http://www.w3.org/1999/xhtml" xml="en" lang="en">
<head>
  <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
  <base href="/" />
  <link rel="stylesheet" type="text/css" href="/master.css" />
</head>

<body>
  <div id="header">
    <div id="logo">
      <img src="/images/logo.gif" />
    </div>
  </div>

  <div id="menu">
    <a href="<?php echo $this->url(array('home'); ?>">HOME</a>
    <a href="<?php echo $this->url(array('page' => 'services', 'static-content'); ?>">SERVICES</a>
    <a href="<?php echo $this->url(array(), 'contact'); ?>">CONTACT</a>
  </div>

  <div id="content">
    <?php echo $this->layout()->content; ?>
  </div>

  <div id="footer">
    <p>Created with <a href="http://framework.zend.com/">Zend Framework</a>. Licensed under
    <a href="http://www.creativecommons.org/">Creative Commons</a> 许可。</p>
  </div>
</body>
</html>
```

图 3-16 SQUARE 联系表单

如果你现在尝试通过浏览器访问 URL`http://square.localhost/contact`，你应该看到一个类似于图 3-16 所示的表单。在表单字段中输入值并提交；如果一切顺利，你应该看到类似于图 3-17 所示的成功消息。

图 3-17 成功提交 SQUARE 联系表单的结果

## 90 Zend Framework：学者指南

图 3-18 使用无效输入值提交 SQUARE 联系表单的结果

你也可以尝试使用无效值提交表单。内建的验证器会捕获你的无效输入并带有错误消息重新重绘表单，如图 3-18 所示。

### 注意

切记更新`Controller::indexAction`中的收件人邮箱地址以反映你的邮箱地址，否则由`Zend_Mail`组件生成的邮件信息将永远无法收到。

### 自定义表单外观

现在，你应该对如何使用 Zend Framework 构建表单有了相当充分的了解，并且对帮助你保护应用程序免受无效和恶意输入侵害的工具有了一些见解。本节将快速查看某些可以帮助你改进表单外观和行为的工具，旨在使其更加清晰且包含更多信息。

## 第 3 章：处理表单

### 使用自定义错误消息

每个输入验证器都带有一组与验证数据类型适当的默认错误消息。大多数情况下，这些默认错误消息为用户提供了足够的信息来定位并纠正输入中的错误。然而，当这些默认消息需要更具描述性且对用户友好时，也会出现这种情况。

这样做并不困难，因为每个验证器都可以通过传递给`add()`方法的选项数组中的`'messages'`键来配置显示自定义错误消息。考虑下面的示例，它说明了这一点：

```php
class Form_Example extends Zend_Form
{
    public function init()
    {
        // 初始化表单
        $this->setAction('/sandbox/example/form')
            ->setMethod('post');

        // 创建姓名的输入
        $name = new Zend_Form_Element_Text('name');
        $name->Label('Name:')
            ->setOptions(array('size' => '35'))
            ->setRequired(true)
            ->addValidator('Alpha', false, array(
                'messages' => array(
                    Zend_Validate_Alpha::INVALID => "ERROR: Invalid name",
                    Zend_Validate_Alpha::NOT_ALPHA => "ERROR: Name cannot contain non-alpha characters",
                    Zend_Validate_Alpha::STRING_EMPTY => "ERROR: Name cannot be empty"
                )
            ))
            ->addFilter('StringTrim');
    }

    $validator = $name->getValidator('Alpha');

    // 创建邮箱地址的输入
    $email = new Zend_Form_Element_Text('email');
    $email->setLabel('Email address:')
        ->setOptions(array('size' => '50'))
        ->setRequired(true)
        ->addValidator('EmailAddress', array(
            'messages' => array(
                Zend_Validate_EmailAddress::INVALID => "ERROR: Invalid email address",
                Zend_Validate_EmailAddress::HOSTNAME => "ERROR: Invalid hostname",
                Zend_Validate_EmailAddress::LOCAL_PART => "ERROR: Invalid username",
                Zend_Validate_EmailAddress::LENGTH_EXCEEDED => "ERROR: Email too long"
            )
        ));
}
```

## 92 Zend Framework：学者指南

### 使用显示组（Display Groups）

通常情况下，将彼此之间存在某种逻辑联系的表单元素分组是一个很好的主意。这比将元素堆在一起而没有任何分类的方法更具可用性和可读性。在`Zend_Form`中，这通过使用显示组来实现。

显示组通过对象的`addDisplayGroup()`方法添加到表单，该方法接受两个参数：包含元素的数组以及组的名称。被讨论的元素应该已经通过`addElement()`方法添加到表单。`setLegend()`方法用于指定组的名称。在渲染时，这些显示组分别由`<fieldset>`和`<legend>`元素表示。

这是一个示例代码：

```php
<?php

class Form_Example extends Zend_Form
{
```




```php
public function init()
{
    // 初始化表单
    $this->setAction('/sandbox/example/form')
        ->setMethod('post');

    // 创建姓名的输入
    $name = new Zend_Form_Element_Text('name');

    $name->Label('Name:')
        ->setOptions(array('size' => '35'))
        ->setRequired(true)
        ->addFilter('StringTrim');

    // 创建邮箱地址的输入
    $email = new Zend_Form_Element_Text('email');

    $email->setLabel('Email address:')
        ->setOptions(array('size' => '50'))
        ->setRequired(true)
        ->addValidator('EmailAddress', true)
        ->addFilter('StringTrim');

    // 创建电话号码文本输入
    $tel = new Zend_Form_Element_Text('tel');

    $tel->setLabel('Telephone number:')
        ->setOptions(array('size' => '50'))
        ->setRequired(true);

    // 创建提交按钮
    $submit = new Zend_Form_Element_Submit('submit');

    $submit->setLabel('Sign Up');

    // 将元素附加表单
    $this->addElement($name);
    $this->addElement($email);
    $this->addElement($tel);
    $this->addElement($submit);

    // 添加显示组
    $this->addDisplayGroup(array($name, $email), 'Contact Information');
    $this->addDisplayGroup(array($tel, $submit), 'Submission Details');
}
```

### 提示

你也可以通过 `setMessages()` 方法向验证器传递自定义错误消息。

图 3-19 带有错误消息的表单

```php
// 将元素添加到表单
$this->addElement($name)
    ->addElement($email)
    ->addElement($tel);
```

```php
// 添加显示分组
$this->setDisplayGroup(
    array('name', 'email', 'tel', 'address'),
    'contact'
);

$this->getDisplayGroup('contact')
    ->setLegend('Contact Information');
```

```php
$this->addElement($submit);
}
```

图 3-20 展示了结果的样式。

### 使用 3-20 装饰器

在渲染表单时，`Zend_Form` 会将每个表单元素封装在一组 HTML 代码块中，这些代码控制元素的位置和外观。这些 HTML 标记块被称为装饰器（decorators），除了为基于 CSS 的操作提供现成的钩子外，还可以针对每个元素进行自定义，从而从根本上改变表单元素的渲染方式。

图 3-20 带有显示分组的表单

## 第 3 章：处理表单

| 装饰器名称 | 说明 |
| --- | --- |
| Form | 控制表单周围的标记 |
| FormElements | 控制表单字段周围的标记 |
| HtmlTag | 控制表单字段周围的标记 |
| ViewHelper | 控制视图助手 |
| Errors | 控制验证错误周围的标记（每个字段） |
| FormErrors | 控制验证错误周围的标记（摘要） |
| Description | 控制字段描述周围的标记 |
| Label | 控制字段标签周围的标记 |
| Fieldset | 控制字段集（fieldset）周围的标记 |

表 3-4 常用表单装饰器

与过滤器和验证器一样，Zend Framework 自带了许多默认装饰器。表 3-4 列出了你最可能遇到的那些。

默认的 `Zend` 装饰器使用以下映射：

- 表单标签被封装在 `<dt>...</dt>` 元素中。
- 输入字段被封装在 `<dd>...</dd>` 元素中。
- 验证错误被渲染为封装在 `<<ul>>...</<ul>>` 元素中的列表项。

图 3-21 展示了一个表单的 HTML 源代码，而图 3-22 展示了渲染后的结果。

**图 3-21** 使用默认装饰器的表单源代码

图 3-22 图 3-21 中表单的渲染版本

通常，这种布局并不适用于你应用程序的用户界面。要更改它，可以使用以下方法之一：

- `addDecorators()` 方法接受装饰器名称数组，并向元素添加相应的装饰器。如果你添加了已存在的装饰器，则该装饰器的设置将用 `addDecorators()` 方法中指定的值覆盖。
- `clearDecorators()` 方法移除元素所有的现有装饰器。
- `setDecorators()` 方法接受装饰器名称数组，移除元素所有的现有装饰器，并将一组新的装饰器附加到其上。

### 提示

要禁用特定表单或元素的默认装饰器，请向该表单或元素的数组中添加 `disableLoadDefaultDecorators` 键。请注意，如果你禁用了默认装饰器，仍然应该通过 `addDecorators()` 或 `setDecorators()` 方法重新添加 `ViewHelper` 装饰器，因为该装饰器生成了表单及其元素的基础标记。

为了说明这些装饰器的工作原理，请考虑以下示例：

```php
<?php

class Form_Example extends Zend_Form
{
    public $formDecorators = array(
        array('FormElements'),
        array('Form'),
    );

    public $elementDecorators = array(
        array('ViewHelper'),
        array('Label'),
        array('Errors'),
    );
```

```php
public $buttonDecorators = array(
    array('ViewHelper'),
    array('HtmlTag'), array('tag') => 'p')
);
```

```php
public function init()
{
    // 初始化表单
    $this->setAction('/sandbox/example/form')
        ->setMethod('post')
        ->setDecorators($this->formDecorators);
```

```php
// 为姓名创建文本输入
$name = new Zend_Form_Element_Text('name');

$name->setLabel(array('size') => 'Name')
    ->setRequired(true)
    ->setDecorators($this->elementDecorators);
```

```php
// 为电子邮件地址创建文本输入
$email = new Zend_Form_Element_Text('email');

$email->setLabel('Email address:');
$email->setOptions(array('size') => '50')
    ->setRequired(true)
    ->setDecorators($this->elementDecorators);
```

```php
// 为新闻通讯订阅创建复选框
$subscribe = new Zend_Form_Element_Checkbox('subscribe');

$subscribe->setLabel('Subscribe to newsletter:')
    ->setCheckedValue('yes')
    ->setUncheckedValue('no')
    ->setDecorators($this->elementDecorators);
```

```php
// 创建提交按钮
$submit = new Zend_Form_Submit(
    array('class') => 'submit'
);

$submit->setLabel('Sign Up')
    ->setDecorators($this->buttonDecorators);
```

```php
// 将元素添加到表单
$this->addElement($name)
    ->addElement($email)
    ->addElement($tel);
```

```php
// 添加显示分组
$this->setDisplayGroup(
    array('name', 'email', 'tel', 'address'),
    'contact'
);

$this->getDisplayGroup('contact')
    ->setLegend('Contact Information');
```

```php
$this->addElement($submit);
}
```

## 第 4 章：模型操作

### Zend Framework：初学者指南

#### 核心技能与概念

- 理解模型在模型-视图-控制器（MVC）模式中的作用
- 学习“胖模型，瘦控制器”方法的优处
- 将 Doctrine 对象-关系映射（ORM）工具包集成到 Zend Framework 中
- 使用 Doctrine 模型生成器创建模型
- 使用 Doctrine 模型从 MySQL 数据库中检索记录
- 了解如何使用 `Zend_Filter_Input` 组件过滤输入
- 使用 Zend Framework bootstopper 调优应用程序启动过程

上一章你已经快速学习了如何使用 Zend Framework 创建、验证和处理表单的基础知识。然而，表单输入并不会凭空地进入真空中；它必须去往某处。通常情况下，这个“某处”是数据库，例如 MySQL、SQLite 或 PostgreSQL，因此为应用程序添加数据库支持成为应用程序开发人员的一项关键任务。

数据库只是谜图的一部分：你需要模型来与它交互。模型在逻辑上独立于控制器，它们充当应用程序的“数据层”，并提供操作应用程序数据所需的所有功能。Zend Framework 使编写特定特定要求的模型变得简单；你还可以集成由 Doctrine 和 Propel 等流行第三方工具生成的模型。

本章将你的 Zend 技能提升几个台阶，向你展示如何在应用程序中创建并添加模型，以及使用这些模型从 MySQL 数据库中检索数据。它还将向你介绍 Doctrine，这是一个强大（免费）的数据映射工具，它可以显著简化这些任务。

### 理解模型

到此时，你应该已经相当熟悉视图和控制器，它们分别代表符合 MVC 的应用程序的“用户层”和“处理层”。模型代表“数据层”，负责提供一个访问数据的通道，以便维护和强制执行与该数据相关的任何业务规则。因此，如果你正在为在线图书馆构建一个入库系统，你可能有一个 `Transaction`（事务）模型，它不仅记录书籍借入和借出的详情，还包含了规则，防止单个成员一次借出超过五本书，或者重新计算期归还费用并从相应的会员账户中扣款。同样，如果你正在构建一个航空公司票务应用程序，

你可能有一个 `Ticket`（票务）模型，它不仅能够保存和检索机票购买记录，还可以根据特定航班的当前客量自动增加或减少票价。

这里是一个简单模型的示例：

```php
// 处理成员数据的模型
class MemberModel
{
    protected $db;

    public $id;
    public $name;
    public $age;
    public $type;

    private $rate;

    // 构造函数
    // 初始化数据库连接
    public function __construct()
    {
        $this->db = new PDO(
            'mysql:dbname=$db;host=localhost',
            'user',
            'pass'
        );

        $this->db->setAttribute(
            PDO::ATTR_ERRMODE,
            PDO::ERRMODE_EXCEPTION
        );
    }

    // 根据 id 获取成员记录
    public function fetch($id)
    {
        $id = $this->db->quote($id);

        $rs = $this->db->query(
            "SELECT * FROM member WHERE id = $id"
        );

        return $rs->fetchAll(PDO::FETCH_ASSOC);
    }

    // 获取所有成员记录
    public function fetchAll()
    {
        $rs = $this->db->query("SELECT * FROM member");

        return $rs->fetchAll(PDO::FETCH_ASSOC);
    }

    // 添加新成员记录
    public function save()
    {
        // 过滤输入数据
        $f = array();
        $f['name'] = htmlspecialchars($this->name);
        $f['age'] = htmlspecialchars($this->age);
```

```php
$f['type'] = htmlentities($this->type);

// 验证年龄
if ($f['age'] < 18) {
    throw new Exception('Member under 18');
}

// 根据会员类型自动计算折扣
switch ($f['type']) {
    case 'silver':
        $f['rate'] = 0;
        break;

    case 'gold':
        $f['rate'] = 0.10;
        break;

    case 'platinum':
        $f['rate'] = 0.25;
        break;
}

$this->db->exec(
    'INSERT INTO member (Name, Age, Type, DiscountRate) VALUES ('
    . $this->db->quote($f['name']) . ', '
    . $this->db->quote($f['age']) . ', '
    . $this->db->quote($f['type']) . ', '
    . $this->db->quote($f['rate']) . ')'
);

return $this->db->lastInsertId();
}
```

如你所示，这个模型使用 PHP 的 PDO 抽象层与 MySQL 数据库交互。它暴露了许多方法来从数据库检索记录和保存记录到数据库。它包含了一些业务规则（根据会员类型自动计算折扣）和一些输入验证规则（验证成员是否满 18 岁或以上）。对于所有良好的模型，其目的始止于数据；它与数据的格式化无关。以下是你在应用程序中使用它的方式：

```php
class Sandbox_ExampleController extends Zend_Controller
{
    public function saveAction()
    {
        if ($this->getRequest()->isPost()) {
            $model = new MemberModel;

            $model->name = $this->getRequest()->getPost('name');
            $model->age = $this->getRequest()->getPost('age');
            $model->type = $this->getRequest()->getPost('type');

            $id = $model->save();

            $this->view->message = "Record saved with ID: $id";
        }
    }
}
```



# 第 4 章：模型操作

## 模型模式

在处理模型时，有两种常用的模式：DataMapper 模式和 ActiveRecord 模式。之前的示例说明了 ActiveRecord 模式，其中类直接对应于数据库表，并暴露 `save()`、`update()` 和 `delete()` 方法来管理表中的记录。显然，在这种模式下，模型和数据库表是密切耦合的，一个的变化会导致另一个的变化。

DataMapper 模式略有不同，模型类与底层数据库之间并不存在 1:1 的对应关系。相反，这种模式使用一个中间层（映射）来处理从模型类到数据库字段的数据。在这种情况下，是映射类暴露了 `save()`、`update()` 和 `fetch()` 方法，并在内部执行映射成员到数据库字段所需的翻译。

你应该用哪种？这个问题没有简单的答案，因为这就像在问哪种口味的冰淇淋最好。ActiveRecord 模式定义假设数据存储和基于该模式的模型与数据库结构紧密耦合。这对于较小项目或关键功能与标准 `SELECT`、`INSERT`、`UPDATE` 和 `DELETE` 命令密切对应的项目很好。

DataMapper 模式允许应用程序业务规则与数据存储进行显式分离，并且模型本身（而非底层数据库）被认为是主要的数据定义代理。这种模式的一个推论是你不受限于数据库；映射器可以轻松地将数据映射到其他存储类型中，例如平面文件、XML 或 LDAP。这种模式适用于具有复杂数据结构和/或自定义存储格式的项目，或者关键功能需要应用程序实体之间进行更复杂交互的项目。

## 模型范围

在划分哪些属于模型、哪些属于控制器时，通常是困难的。例如，在之前描述的银行示例中，可能会认为与金额和位置相关的验证应该在控制器中，而不是模型中。通常，开发者社区很大程度上采纳了包括 Martin 在内的许多思想领袖所推荐的“胖模型，瘦控制器”方法。

Fowler、James Buck 和 Chris Hartjes（你可以在本章末尾找到链接）建议尽可能将业务逻辑置于模型（models）中，而不是控制器（controllers）中。这种方法具有许多优势：

- 减少“胖”模型（Fat models），并通过将关键业务规则封装在可重用的对象和对象方法中，帮助开发者遵循“不要重复自己”（DRY）原则。然后可以使用继承链在整个应用程序中一致地应用这些规则。使用面向对象编程（OOP）原则指定模型，还允许根据需要为基模型扩展附加功能，并在较大的应用程序空间内区分公属性和私有属性。
- 自给成足的“胖”模型封装了其正常运行所需的所有业务规则，它们比依赖应用程序控制器来执行业务规则的“瘦”模型（thin models）更具移植性。由于应用程序的大部分业务逻辑都在模型中而不是控制器中，切换到不同的框架（例如）将变得更容易，因为模型可以交换到新系统中，并且通常不需要重大的重构即可工作。
- 当“胖”模型处理了大部分繁重工作时，控制器通常只包含几行高度集中的代码。这使得它们更容易理解和阅读，并有助于提高整体性能（因为控制器的调用频率通常高于模型）。它还能产生更具维护性的代码：例如，如果你需要更改特定应用程序实体的业务规则，只需要更新该实体模型，而不需要更新使用它的所有控制器。
- 调试和测试比“胖模型、瘦控制器”方法更加透明，因为通常很容易识别错误源于模型还是控制器，并可以在对应用程序其他部分影响最小的范围内进行修正。

此时需要注意的是，Zend Framework 并不带有 `Zend_Model` 组件，或一组预定义的模型可以供你直接“丢进”应用程序中；你总是需要创建自己的模型。

## 专家问答

**问：**“模型”仅仅是一组封装好的 SQL 语句吗？

**答：**不，绝对不是。一种常见的误解是认为模型仅仅是数据库表的对象表示，其方法对应于 SQL `INSERT`、`UPDATE` 和 `DELETE` 语句。实际上，模型远比结构化查询语言（SQL）封装器复杂。它们可以（也应该）强制执行特定的业务规则、执行计算、处理转换、应用过滤器并对数据执行任何所需的操作。记住，模型的工作越少，你的应用程序的可维护性和可移植性就越高。

# 第 4 章：与模型工作

Zend Framework 包含了许多可以帮助你完成此任务的工具，例如 `Zend_Db_Adapter` 数据库抽象层和用于表操作 `Zend_Db_Table` 接口。然而，你也可以第三方工具（如 Qcodec 或 Propel）创建应用程序模型，并将其集成到你的 Zend Framework 应用程序中。事实上，这正是下一节的重点。

## 安装 Doctrine

虽然你可以使用 Zend Framework 提供的组件从零开始应用程序模型，但有一种更容易的方法：使用对象关系映射（ORM）工具来自动生成它们。这些工具可以自动扫描现有数据库，并使用 ActiveRecord 模式或 DataMapper 模式创建与表相对应的模型类。然后，将这些增强后的模型添加到应用程序中，并根据需要进行扩展以支持特定需求就非常简单了。

PHP 有许多免费、开源的 ORM 工具可用，如 Propel、Doctrine、RedBean 和 Qc。本书使用了 Doctrine，它因其易用性、灵活性和广泛的扩展性而在开发者中极受欢迎。Doctrine 软件包包含一个数据库抽象层（支持大多数常见的 RDBMS 系统）、自定义的 SQL 查询语言（DQL）以及用于从现有数据库架构自动生成模型类的工具。这些模型类基于 ActiveRecord 模式，完全符合 PHP 5.3.x 对象。

要开始使用 Doctrine，访问其官方网站下载并安装最新版本解压到你的开发环境：

```bash
$ cd /tmp
$ tar -xzf Doctrine.gz
```

解压后，目录结构如图 4 所示。`lib/` 目录包含了 Doctrine 组件，你需要将其添加到 PHP 路径中；`test/` 目录包含了用例。

```php
<?php

// include Doctrine

include_once 'Doctrine.php';

// autoloader

spl_autoload_register(array('Doctrine', 'autoloader'));

// create manager

$manager = Doctrine_Manager::getInstance();

// create connection

$conn = Doctrine_Manager::connection('mysql:root@localhost');

// get list of databases

$databases = $conn->listDatabases();

print_r($databases);

?>
```

在命令行界面（CLI）执行以下脚本进行验证：

```bash
$ cd /tmp/
$ php ./test.php
```

图 4-1 展示了你将看到的输出：

![img/227e587c1452.png](img/227e587c1452.png)

**图 4-1** 可用数据库列表

## 生成与集成模型

第一步是为应用程序创建一个 MySQL 数据库。执行此操作，切换到命令行，启动 MySQL 客户端，并使用以下命令创建一个新数据库：

```text
mysql -u root -p

Enter password: ******

Welcome to the MySQL monitor. Commands end with ; or \g.

Your MySQL connection id is 17

Server version: 5.1.30-community MySQL Community Server (GPL)
```

```sql
mysql> CREATE DATABASE square;

Query OK, 0 rows affected (0.00 sec)

mysql> USE square;

Database changed
```

如下所示，向该数据库添加一些表：

```sql
mysql> CREATE TABLE IF NOT EXISTS country (
  -> CountryID INT(11) NOT NULL AUTO_INCREMENT,
  -> CountryName VARCHAR(255) NOT NULL,
  -> PRIMARY KEY (CountryID)
  -> ENGINE=InnoDB DEFAULT CHARSET=utf8;

Query OK, 0 rows affected (0.09 sec)
```

```sql
- ENGINE=InnoDB DEFAULT CHARSET=utf8;

Query OK, 0 rows affected (0.09 sec)
```

```sql
mysql CREATE TABLE IF NOT EXISTS type (
-> TypeID INT(11) NOT NULL AUTO_INCREMENT,
-> TypeName VARCHAR(255) NOT NULL,
-> PRIMARY KEY (TypeID)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

Query OK, 0 rows affected (0.09 sec)
```

```sql
mysql CREATE TABLE IF NOT EXISTS item (
-> RecordID INT(11) NOT NULL AUTO_INCREMENT,
-> RecordDate DATE NOT NULL,
-> SellerName VARCHAR(255) NOT NULL,
-> SellerTel VARCHAR(50) DEFAULT NULL,
-> SellerAddress TEXT,
-> Title VARCHAR(255) NOT NULL,
-> Year INT(4) NOT NULL,
-> CountryID INT(4) NOT NULL,
-> Denomination FLOAT NOT NULL,
-> TypeID INT(4) NOT NULL,
-> GradePriceMin FLOAT NOT NULL,
-> SalePrice FLOAT NOT NULL,
-> Description TEXT NOT NULL,
-> DisplayStatus TINYINT(1) NOT NULL,
-> DisplayUntil DATE DEFAULT NULL,
-> PRIMARY KEY (RecordID)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

Query OK, 0 rows affected (0.09 sec)
```

```sql
mysql CREATE TABLE IF NOT EXISTS user (
-> RecordID INT(4) NOT NULL AUTO_INCREMENT,
-> Username VARCHAR(10) NOT NULL,
-> Password TEXT NOT NULL,
-> PRIMARY KEY (RecordID)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

Query OK, 0 rows affected (0.09 sec)
```

```sql
mysql CREATE TABLE IF NOT EXISTS log (
-> RecordID int(11) NOT NULL AUTO_INCREMENT,
-> LogMessage text NOT NULL,
-> LogLevel varchar(30) NOT NULL,
-> LogTime varchar(30) NOT NULL,
-> Stack text,
-> Request text,
-> PRIMARY KEY (RecordID)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

Query OK, 0 rows affected (0.09 sec)
```

# 第 4 章：模型模型（Models）

| 表名 | 包含 |
|---|---|
| item | 待售邮票列表，以及卖家联系信息 |
| user | 授权用户列表 |
| country | 国家主列表 |
| grade | 邮票等级主列表 |
| type | 邮票类型主列表 |
| log | 错误日志 |

**表 4-1** 应用程序数据库简述

## 专家问

**问：**如果 Zend Framework 的约定是实体名称使用驼峰命名法（camel-casing），为什么本章中的 MySQL 数据库和表名指定为小写？

**答：**在文件系统层面，MySQL 分别将数据库和表表示为目录和文件。某些文件（例如 Windows）区分文件名的大小写，而另一些（例如 Linux）则区分。因此，为了简化不同操作系统之间的数据库和表，通常建议将所有数据库和表名转换为小写，并确保它们由字母、数字和下划线组成。显然，你也应该尽量避免使用 MySQL 的保留关键字作为数据库名。

表 4-1 给出了这些表的简要描述。要理解这些表是如何连接的，请看图 4-3，它展示了本章中 MySQL 数据库的实体关系图。继续用一些记录初始化主表：

```sql
mysql> INSERT INTO country (CountryID, CountryName) VALUES
  -> (1, 'United States'),
  -> (2, 'United Kingdom'),
  -> (3, 'India'),
  -> (4, 'Singapore'),
  -> (5, 'Germany'),
  -> (6, 'France'),
  -> (7, 'Italy'),
  -> (8, 'Spain'),
-> (9, 'Hungary');

Query OK, 9 rows affected (0.09 sec)

Records: 9 Duplicates: 0 Warnings: 0
```

```sql
mysql INSERT INTO grade (GradeID, GradeName) VALUES
-> (1, 'Very Fine'),
-> (2, 'Fine'),
-> (3, 'Good'),
-> (4, 'Average'),
-> (5, 'Poor');

Query OK, 5 rows affected (0.09 sec)

Records: 5 Duplicates: 0 Warnings: 0
```

```sql
mysql INSERT INTO type (TypeID, TypeName) VALUES
-> (1, 'Commemorative'),
-> (2, 'Decorative'),
-> (3, 'Definitive'),
-> (4, 'Special'),
-> (5, 'Other');

Query OK, 5 rows affected (0.09 sec)

Records: 5 Duplicates: 0 Warnings: 0
```

![](img/222e7e58871b088cc6397852e1452b57_130_0.png)

你也可以向 `item` 表中插入几条虚拟记录，让流程运转：

```sql
mysql> INSERT INTO item (RecordID, RecordDate, SellerName,
-> SellerEmail, SellerTel, SellerAddress, Title,
-> Year, CountryID, Denomination, TypeID,
-> SalePrice, PriceMax, Description,
-> DisplayStatus) VALUES
-> ('1', '2009-12-06', 'John Doe', 'john@example.com', '123456789102', 'Green House, Red Road, Blue City', '1958', 3, 5.00, 1, 15.0, 'Himalayas - Silver Jubilee. Aerial view of snow-capped condition.', 0);

Query OK, 1 row affected (0.02 sec)
```

```sql
mysql> INSERT INTO item (RecordID, RecordDate, SellerName,
-> SellerEmail, SellerTel, SellerAddress, Title,
-> Year, CountryID, Denomination, TypeID,
-> SalePrice, PriceMax, Description,
-> DisplayStatus) VALUES
-> ('2', '2009-10-05', 'Susan Doe', 'susan@example.com', '198765432198', 'Tiger Palace, Animal City', '1966', 2, 4.00, 1, 24.0, 'WWII Fighter Plane on blue sky.', 0);

Query OK, 1 row affected (0.02 sec)
```

出于安全考虑，创建一个仅访问此数据库的专用 MySQL 用户也是好主意。请使用以下命令执行此操作：

```sql
mysql> GRANT ALL ON square.* TO square@localhost IDENTIFIED BY 'square';

Query OK, 0 rows affected
```



现在数据库已就绪，你可以开始创建模型了！

## 生成 Doctrine 模型（Doctrine Models）

Doctrine 自带了一个强大的模型生成器，它可以“读取”现有数据库并从中生成一组模型类。要查看运行效果，请创建并运行以下 PHP 脚本：

```php
<?php

// 包含主类
include_once 'Doctrine.php';

spl_autoload_register(array('Doctrine', 'autoload'));

// 创建管理器
$manager = Doctrine_Manager::getInstance();

// 创建数据库连接
$conn = Doctrine_Manager::connection(
    'mysql://square@localhost/square'
);

// 自动生成模型
Doctrine::generateModels(
    '/tmp/models',
    array('doctrine'),
    array('classPrefix' => 'Square_Model_')
);
```

该脚本设置了上一节的数据库，然后使用 `generateModels()` 动态生成对应表的模型。这些模型将保存到方法的第一个参数指定的目录。注意传递给方法的第三个参数，有一个选项可以让 Doctrine 为每个类名添加自定义字符串。让模型符合 Zend Framework 的自动加载系统是有用的。

使用 PHP CLI 在命令行提示符执行此脚本：

```bash
cd /tmp
php ./doctrine-models.php
```

如果一切顺利，Doctrine 将一组模型写入指定的目录。查看一下，你应该能看到图 4-4 的内容。这些模型现在应该复制到 `$APP_DIR`，执行以下命令：

```bash
mkdir library/Square/Model
cp /tmp/models/* library/Square/Model

# （注：此处此处应为生成的文件的逻辑）
```

默认情况下，Doctrine 生成器使用类名作为相应的文件名。例如，名为 `Square_Model_Item` 的类将被保存为 `Square_Model_Item.php`。遗憾的是，这种安排不符合 Zend Framework 的加载器，它期望将 `Square_Model_Item` 类保存为 `Square/Model/Item.php`。为了解决这个问题，必须手动重命名每个模型类文件，删除 Doctrine 自动添加的前缀。这里有一个示例：

```bash
cd library/Square/Model
mv Square_Model_BaseCountry.php BaseCountry.php
```

过程结束后，你应该得到一个类似于图 4-5 的结构。

**提示**

如果你正在使用 Doctrine v1.2，可以向 `generateModelsFromDb()` 方法传递一个额外的 `classPrefix` 选项。这指定了是否要在模型文件名中添加类前缀。将其设置为 `'false'` 可以减少将 Doctrine 模型集成到应用程序中的工作，因为不再需要重命名每个模型文件以符合 Zend Framework 的约定。

注意 Doctrine 将数据库中的每个表映射到两个模型类：基类和子类。基类扩展 `Doctrine_Record` 类，包含表定义，并通过继承暴露所有常用数据库操作的方法。子类是派自基类的存根类，作为你想添加到模型的自定义方法的容器。

## 设置模型关系（Setting Model Relationships）

现在，虽然 Doctrine 可以产生对应单个表的模型并暴露操作方法，但它没有自动检测表之间关系的智能。然而，关系在实际使用中通常至关重要，因此需要开发者通过链接模型来定义这些关系。

Doctrine 只需两个方法就可以复制 RDBMS 中可能的不同关系类型——一对一、一对多、多对多和自引用：`hasOne()` 和 `hasMany()`。这两个方法都接受两个参数：在关系中使用的另一个模型名称，以及一个指定关系参数的选项数组。为了确保这些关系在模型实例化时自动加载，它们应该在模型的 `setUp()` 中。

![图 4-5 集成到应用程序后的自动生成的 Doctrine 模型](img/222e7e58871b088cc6397852e1452b57_133_0.png)

## 116 Zend Framework：入门指南

要理解其工作原理，请向后翻几页查看图 4-3，该图说明了各个数据库表之间的关系。从图 4-3 可以清楚看出，国家（country）、等级（grade）和类型（type）主表与项目（item）表之间存在 1:n 关系。这种关系利用了 `item.Country`、`item.Grade` 和 `item.TypeId` 外键，并通过在 `Item` 模型中添加以下代码在 Doctrine 中实现：

```php
<?php

class Square_Model_Item extends Square_Model_BaseItem
{
    public function setUp()
    {
        $this->hasOne('Square_Model_Grade', array(
            'local' => 'GradeID',
            'foreign' => 'GradeID'
        ));

        $this->hasOne('Square_Model_Country', array(
            'local' => 'CountryID',
            'foreign' => 'CountryID'
        ));

        $this->hasOne('Square_Model_Type', array(
            'local' => 'TypeID',
            'foreign' => 'TypeID'
        ));
    }
}
```

`setUp()` 方法负责自动定义 `Item` 模型与 `Country`、`Grade` 以及 `Item` 模型之间的外键关系。这在 Doctrine 查询中连接这些表时非常有用（你很快就会看到这一点）。

### Doctrine 的自动加载

现在剩下的唯一工作就是让 Zend Framework 应用程序和 Doctrine 之间进行通信了。实现这一目标主要有几种方法，但推荐的方法是在引导文件（bootstrap file）中初始化 Doctrine，并配置其按需要“懒加载”模型。这种方法受到了 Zend Framework 领先开发人员（如 Matthew Weier O’Phinney 和 Eric Leclerc）的推崇，你可以在章末找到他们作品的链接。

第一步是决定是将 Doctrine 库包含在你的应用程序中，还是允许用户自行下载并安装这些库。要理解这些选项的优缺点，请回顾第 1 章，当时你曾对 Zend Framework 库做过类似的决定。为了与之前的决定保持一致，让我们假设 Doctrine 库将与应用程序捆绑。因此，使用以下命令将 Doctrine `lib/` 目录的内容复制到 `$APP_DIR/library/Doctrine`：

```shell
cp -R /usr/local/lib/php/Doctrine library/
```

下一步是更新应用程序配置文件（位于 `$APP_DIR/application/configs/application.ini`），添加一个数据源名称（DSN），以便 Doctrine 使用它来连接之前创建的 MySQL 数据库。要执行此操作，请用文本编辑器打开应用程序配置文件，并在 `[production]` 区域添加以下行：

```ini
doctrine.dsn = "mysql://square:square@localhost/square"
```

最后一步是通过向应用程序引导程序中添加必要的代码来初始化 Doctrine。正如名称所示，当“bootstrap”需要资源时，该组件会被自动调用。它被定义为扩展 `Zend_Application_Bootstrap_Bootstrap` 的类，位于 `$APP_DIR/application/Bootstrap.php`。

用文本编辑器打开此文件，并使用新的 `_initDoctrine()` 方法进行更新，如下如下：

```php
<?php

class Bootstrap extends Zend_Application_Bootstrap_Bootstrap
{
    protected function _initDoctrine()
    {
        require_once 'Doctrine/Doctrine.php';

        $this->getApplication()
            ->getAutoloader(array('Doctrine', 'autoload'));

        $manager = Doctrine_Manager::getInstance();

        $manager->setAttribute(
            Doctrine::ATTR_MODEL_LOADING,
            Doctrine::MODEL_LOADING_CONSERVATIVE
        );

        $config = $this->getOption('doctrine');

        $conn = Doctrine_Manager::connection(
            $config['dsn'],
            'doctrine'
        );

        return $conn;
    }
}
```

在 Zend Framework 的引导程序系统中，任何属于 `Bootstrap` 类并以特殊前缀 `_init*` 命名的保护方法都会被视为资源方法，并由引导程序自动执行。前面的列表定义了 `_initDoctrine()` 资源方法，它首先包含主 Doctrine 类，并使用有关如何加载 Doctrine 类的信息来配置自动加载器。它创建了 `Doctrine_Manager` 类的实例，配置了 Doctrine 的懒加载，从应用程序配置文件中读取 DSN，并打开与数据库的连接。

由于此方法会在每次请求时自动执行，因此 Doctrine 模型可以在任何应用程序控制器中可用。Doctrine 已经准备就绪了！

## 与 Doctrine 模型工作

在继续之前之前，让我们快速进入 Doctrine 模型的世界。正如之前讨论的，Doctrine 模型实现了 ActiveRecord 模式，其中模型类的每个实例都代表底层表的一条记录，实例的每个属性都代表记录的一个字段。模型扩展了 `Doctrine_Record` 基类，该类暴露了许多方法以简化添加、编辑、删除和搜索记录的工作。接下来的章节将更详细地检查这些方面。

### 获取记录

使用 Doctrine 模型获取记录有几种不同的方法。如果你有记录的主键，一种方法是使用 `find()` 方法，如下：

```php
<?php

$member = Doctrine::getTable('Member')->find(1);

var_dump($member->toArray());
?>
```

如果你更喜欢获取所有记录，可以使用 `findAll()` 方法，如下：

```php
<?php

$members = Doctrine::getTable('Member')->findAll();

var_dump($members->toArray());
?>
```

Doctrine 拥有它自己的 SQL 变体，称为 Doctrine 查询语言（DQL），它提供了一个创建和执行查询的流式接口。考虑以下简单示例，它可以检索所有内容：

```php
<?php

$q = Doctrine_Query::create()
    ->from('Member');

$result = $q->fetchArray();
?>
```

### 使用过滤器

你可以使用 `where()` 方法为查询添加条件。例如，假设你只想活跃的账户：

```php
<?php

$q = Doctrine_Query::create()
    ->from('Member')
    ->where('Status = ?', 1);

$result = $q->fetchArray();
?>
```

你可以使用 `addWhere()` 方法为查询附加多个过滤器。这里有一个检索位于英国成员的示例：

```php
<?php

$q = Doctrine_Query::create()
    ->from('Member')
    ->where('Status = ?', 1)
    ->addWhere('Location = ?', 'UK');

$result = $q->fetchArray();
?>
```

### 结果分组和排序

你可以使用 `orderBy()` 和 `groupBy()` 方法对结果集进行分组和排序。这里是按国家分组的示例：

```php
<?php

$q = Doctrine_Query::create()
    ->from('Member')
    ->where('Status = ?', 1)
    ->groupBy('Location')
    ->orderBy('Location DESC');

$result = $q->fetchArray();
?>
```

### 连接表

你还可以使用 `leftJoin()` 和 `innerJoin()` 方法通过 DQL 执行表之间的连接。这里有一个左连接的示例：

```php
<?php

$q = Doctrine_Query::create()
    ->from('Member m')
    ->leftJoin('m.Country', 'c')
    ->leftJoin('m.OrgType', 'o')
    ->where('o.DisplayStatus = 1');

$result = $q->execute();
?>
```

这里是内连接的示例：

```php
<?php

$q = Doctrine_Query::create()
    ->innerJoin('Member m', 'Country c');

$result = $q->execute();
?>
```

用于连接的字段由 Doctrine 根据源模型 `setUp()` 方法定义的关系自动设置。

> **提示** 使用 DQL 时，你可能需要查看特定查询的生成代码。Doctrine 允许你通过其 `gql()` 方法获取原始 SQL。

### 添加、更新和删除记录

使用 Doctrine 模型向数据库添加新记录非常简单：只需实例化模型，将字段值设为模型属性，然后调用模型的 `save()` 方法即可。这是一个示例：

```php
<?php

$member = new Member;

$member->FirstName = 'Jack';
$member->LastName = 'Frost';
$member->Email = 'jack@example.com';
?>
```

### 专家问答

**问** DQL 支持右连接吗？

**答** 不支持。DQL 目前支持左连接和内连接。但这不应该影响你的进度，因为左连接和右连接是可以相互转换的，取决于你站在的哪一侧。为了说明，请考虑以下两个查询：

```sql
SELECT * FROM c LEFT JOIN a USING (id)

SELECT * FROM a RIGHT JOIN c USING (id);
```

## 第 4 章：模型操作

```php
<?php

$member->JoinDate = '2009-11-11';
$member->Status = 1;

$id = $member->save();
?>
```

要更新记录，请使用 `find()` 方法或 DQL 查询检索它，更新必要的属性，然后使用 `save()` 方法将其保存回数据库。以下是一个示例：

```php
<?php

$member = Doctrine::getTable('Member')->find(1);

$member->FirstName = 'John';
$member->Status = 2;

$member->save();
?>
```

如需更多细节，你也可以使用 DQL `update()` 方法更新记录。以下是一个示例，它与上一个等效：

```php
<?php

$q = Doctrine_Query::create()
    ->update('Member m')
    ->set('m.FirstName', '?', 'John')
    ->set('m.Status', '?', '2')
    ->addWhere('m.RecordID = ?', 1);

$q->execute();
?>
```

同样，你可以通过调用模型的 `delete()` 方法或使用 DQL 查询来删除记录。下面的列表说明了这两种方法：

```php
<?php

// 使用模型方法
$member = Doctrine::getTable('Member')->find(11);
$member->delete();

// 使用 DQL
$q = Doctrine_Query::create()
    ->delete('Member m')
    ->addWhere('m.RecordID = ?', 11);

$q->execute();
?>
```



虽然对 Doctrine 包的完整解释超出了本书的范围，但前面的示例应该让你对模型操作的基础有了些见解，并为你理解后续章节的内容提供了基础。有关更多信息和更多示例，请参考本章末尾的链接。

## Zend Framework：入门指南

### 示例 4-2：检索数据库记录

现在你已经了解了一些 Doctrine 模型是如何工作的，想用这些知识做些实际操作吗？接下来的部分向你展示如何使用这些模型从数据库中检索单个邮票列表，对其进行格式化，并在 SQUARE 示例应用程序的范围内显示它们。

### 创建新模块

到目前为止，所有的示例都是在“default”模块下创建。然而，使用模块化目录布局的优势之一是，它允许你将相关的控制器组合在一起，从而产生更具可维护性和组织有序的代码树。考虑到这一点，创建一个名为“catalog”的新模块，该模块将包含所有与添加、检索、搜索和操作你的应用程序邮票目录相关的控制器和视图。

要创建此“catalog”模块，切换到`$APP_DIR/application/`并执行以下命令：

```shell
mkdir modules/catalog
mkdir modules/catalog/controllers
mkdir modules/catalog/views
mkdir modules/catalog/views/scripts
```

### 定义自定义路由

接下来，让我们为显示 URL 定义一个路由。为了简单起见，我们假设所有的显示 URL 都采用`/catalog/item/display/xx`的形式，其中`xx`是指示 ID 的变量。要设置自定义路由来处理 URL，请在`$APP_DIR/application/configs/application.ini`应用程序配置文件中添加以下路由定义：

```ini
resources.router.routes.catalog-display.route = /catalog/item/display/:id
resources.router.routes.catalog-display.defaults = catalog
resources.router.routes.catalog-display.defaults.controller = item
resources.router.routes.catalog-display.defaults.action = display
```

### 定义控制器

下一步是定义一个与上一节中路由定义对应的控制器和动作。按照惯例，此控制器将位于`$APP_DIR/application/modules/catalog/controllers/ItemController.php`。它的样子如下所示：

```php
<?php

class Catalog_ItemController extends Zend_Controller_Action
{
    public function init()
    {
    }

    // 显示目录项的动作
    public function displayAction()
    {
        // 为 GET 输入设置过滤器和验证器
        $filters = array(
            'id' => array('HtmlEntities', 'StripTags', 'StringTrim')
        );

        $validators = array(
            'id' => array('NotEmpty', 'Int')
        );

        // 测试输入是否有效
        // 检索请求的记录
        // 附加到视图
        $input = new Zend_Filter_Input($filters, $validators);
        $input->setData($this->getRequest()->getParams());

        if ($input->isValid()) {
            $Sq = Doctrine_Query::create()
                ->from('Square_Model_Item', 'i')
                ->leftJoin('i.Square_Model_Country', 'c')
                ->leftJoin('i.Square_Model_Type', 't')
                ->where('i.RecordID = ?', $input->id);

            $result = $Sq->fetchArray();

            if (count($result) == 1) {
                $this->view->item = $result[0];
            } else {
                throw new Zend_Controller_Action_Exception('Page not found', 404);
            }
        } else {
            throw new Zend_Controller_Action_Exception('Invalid input');
        }
    }
}
```

### 注意

在 Zend Framework 下，每个模块（“default”模块除外）都有自己的命名空间，以防止对象和变量冲突。你可以在`Catalog_ItemController`中看到这一点，该控制器位于命名空间。

（继续）

在这个示例中，`displayAction()`方法检索`$GET['id']`值，将其传递给查询。如果查询返回记录，则将其赋值给视图。如果没有找到记录或找到了多条记录，则将抛出异常并传递到错误处理程序。

本节介绍了一个新组件`Zend_Filter_Input`。它是如何工作的？`Zend_Filter_Input`类接受三个参数——过滤器数组、验证器数组和数据数组——尽管前两个通常通过构造函数传递。该类提供了设置数据、验证数据和检索过滤数据的方法。

### 定义视图

假设请求的 ID 有效且找到了记录，控制器将渲染相应的视图，它应该存储在`$APP_DIR/application/modules/catalog/views/display.php`。它的样子如下：

```html
<h2><?php echo $this->escape($this->item['Title']); ?></h2>

<h3>SALE: <?php echo $this->escape($this->item['Year']); ?></h3>

<div id="container">
    <table>
        <tr>
            <td class="key">Title</td>
            <td class="value"><?php echo $this->escape($this->item['Title']); ?></td>
        </tr>
        <tr>
            <td class="key">Type</td>
            <td class="value"><?php echo $this->escape($this->item['Square_Model_Type']['TypeName']); ?></td>
        </tr>
        <tr>
            <td class="key">Year</td>
            <td class="value"><?php echo $this->escape($this->item['Year']); ?></td>
        </tr>
        <tr>
            <td class="key">Country</td>
            <td class="value"><?php echo $this->escape($this->item['Square_Model_Country']['Country']); ?></td>
        </tr>
        <tr>
            <td class="key">Denomination</td>
            <td class="value"><?php echo $this->escape(sprintf('%01.2f', $this->item['Denomination'])); ?></td>
        </tr>
        <tr>
            <td class="key">Grade</td>
            <td class="value"><?php echo $this->escape($this->item['Square_Model_Grade']['GradeName']); ?></td>
        </tr>
        <tr>
            <td class="key">Sale price</td>
            <td class="value"><?php echo $this->escape($this->item['SalePriceMin']); ?> - <?php echo $this->escape($this->item['SalePriceMax']); ?></td>
        </tr>
        <tr>
            <td class="key">Description</td>
            <td class="value"><?php echo $this->escape($this->item['Description']); ?></td>
        </tr>
    </table>
</div>
```

## Zend Framework：入门指南

### 查看项目

出售：喜马拉雅 - 银禧纪念 - 1958 - 精良 (Fine)

| 标题 | 喜马拉雅 - 银禧纪念 |
| :--- | :--- |
| 类型 | 纪念币 |
| 年份 | 1958 |
| 国家 | 印度 |
| 面值 | 5.00 |
| 等级 | 精良 (Fine) |
| 售价 | $10 - $15 |
| 描述 | 雪雪的喜马拉雅山的银禧纪念视图。顶部页边处有一条水平橙色条纹。状况极佳，无痕迹。 |

**图 4-6** 成功检索数据库记录的结果

这里没什么复杂的。此视图仅格式化由上一步中模型检索到的记录，并以一种可用且可读的格式将其显示出来。注意使用`escape()`方法，在显示给用户之前自动对视图的输出进行转义。

要查看效果，请尝试在浏览器中访问 URL `http://square.localhost/catalog/item/1`。如果一切运行正常，控制器将从数据库中检索 ID 为 #1 的记录（你是在初始化数据库时手动添加此记录的），将其分配给视图并进行渲染。输出应该类似于图 4-6 所示。作为测试，你也可以再次尝试相同的 URL，但使用无效或缺失的 ID。你应该看到“页面未找到”或“无效输入”错误，如图 4-7 所示。

### 发生错误

**异常：**

**消息：** 无效输入

**堆栈跟踪：**

```
array (
```

**图 4-7** 检索失败的结果

## 咨询专家

**Q**：为什么我在显示输出之前需要对它进行转义？

**A**：作为一个一般原则，你不应该信任任何来自外部源的数据。这是因为攻击者总有可能向这些数据中嵌入恶意内容，如果你在不对其进行清理的情况下使用它，可能会让你的用户面临风险。此类攻击的一个常见示例是“跨站脚本”，攻击者通过向你的页面中注入恶意的 JavaScript 或 HTML 代码来获取敏感数据。考虑到这一点，在将输出显示给用户之前，将其通过净化处理是至关重要的。

## 总结

前面的章节侧重于视图和控制器，而这一章聚焦于模型：它们是什么、如何工作，以及它们在 MVC 应用中扮演什么角色。虽然 Zend Framework 没有附带专门的模型组件，但创建自己的模型或集成第三方模型（例如由 ORM 包生成的模型）绝非易事。本章演示了这一过程，展示了如何在 Zend Framework 应用程序的上下文中使用模型并配置模型。它还向你引入了`Zend_Filter_Input`组件，这是一个用于即时过滤和验证的实用工具，以及`Bootstrap`类，它为初始化应用程序例提供了一个框架。示例现在也变得简单得许多。它有一个用于持久化存储的数据库，以及一个可以交互以检索和显示数据库记录的控制器。更重要的是，它拥有一套健壮且可扩展的模型。这将简化数据访问和操作，并将为后续章节中讨论的高级功能提供基础。

要了解更多关于本章讨论的话题，请考虑访问以下链接：

- Doctrine 官方网站和手册：http://www.doctrine-project.org/documentation/en/
- 模型模型介绍：http://www.doctrine-project.org/documentation/en/introduction-to-models
- 关于如何使用模型表示数据库关系的信息：http://www.doctrine-project.org/documentation/manual/en/defining-models
- 使用 Doctrine 的示例查询：http://www.doctrine-project.org/documentation/manual/en/working-with-models
- 维基 ActiveRecord 模式的讨论：http://en.wikipedia.org/wiki/ActiveRecord_pattern
- 维基对象关系映射的讨论：http://en.wikipedia.org/wiki/Object_Relational_Mapping

## Zend Framework：初学者指南

```php
--setOptions(array('rows' => '6', 'cols' => '36'))
--addFilter('HtmlEntities')
--addFilter('StringTrim');
```

```php
// 创建项目标题文本输入
$title = new Zend_Form_Element_Text('Title');

$title->setLabel('Title:')
    ->setOptions(array('size' => '60'))
    ->setRequired(true)
    ->addFilter('HtmlEntities')
    ->addFilter('StringTrim');
```

```php
// 创建项目年份文本输入
$year = new Zend_Form_Element_Text('Year');

$year->setLabel('Year:')
    ->setOptions(array('size' => '8', 'length' => '4'))
    ->addValidator('Between', false, array(
        'min' => 1700, 'max' => 2015
    ))
    ->addFilter('HtmlEntities')
    ->addFilter('StringTrim');
```

```php
// 创建项目国家选择输入
$country = new Zend_Form_Element_Select('CountryID');

$country->setLabel('Country:')
    ->setRequired(true)
    ->addValidator('Int')
    ->addFilter('HtmlEntities')
    ->addFilter('StringTrim')
    ->addFilter('StringToUpper');

foreach ($this->getCountries() as $c) {
    $country->addOption($c['Country'], $c['CountryName']);
}
```

```php
// 创建项目金额文本输入
$denomination = new Zend_Form_Element_Text('Denomination');

$denomination->setLabel('Denomination:')
    ->setOptions(array('size' => '8'))
    ->setRequired(true)
    ->addValidator('Float')
    ->addFilter('HtmlEntities')
    ->addFilter('StringTrim');
```

```php
// 创建项目类型单选输入
$type = new Zend_Form_Element_Radio('Type');

$type->setLabel('Type:')
    ->setRequired(true)
    ->addValidator('Int');
```

## 第 5 章：处理 CRUD 操作

```php
->addFilter('HtmlEntities')
->addFilter('StringTrim');

foreach ($this->getTypes() as $t) {
    $type->addMultiOption($t['TypeID'], $t['TypeName']);
}

$type->setValue(1);
```



```php
// 创建项目等级选择输入

$grade = new Zend_Form_Element_Select('GradeID');

$grade->setLabel('Grade:')
    ->setRequired(true)
    ->addValidator('Int')
    ->addFilter('HtmlEntities')
    ->addFilter('StringTrim');

foreach ($this->getGrades() as $g) {
    $grade->addMultiOption($g['GradeID'], $g['GradeName']);
}
```

```php
// 创建销售价格（最低）输入

$priceMin = new Zend_Form_Element_Text('SalePriceMin');

$priceMin->setLabel('Sale price (min):')
    ->setOptions(array('size' => '8'))
    ->setRequired(true)
    ->addValidator('Float')
    ->addFilter('HtmlEntities')
    ->addFilter('StringTrim');
```

```php
// 创建销售价格（最高）输入

$priceMax = new Zend_Form_Element_Text('SalePriceMax');

$priceMax->setLabel('Sale price (max):')
    ->setOptions(array('size' => '8'))
    ->setRequired(true)
    ->addValidator('Float')
    ->addFilter('HtmlEntities')
    ->addFilter('StringTrim');
```

```php
// 创建项目描述输入

$notes = new Zend_Form_Element_TextArea('Description');

$notes->setLabel('Description:')
    ->setOptions(array('rows' => '15', 'cols' => '60'))
    ->setRequired(true)
    ->addFilter('HtmlEntities')
    ->addFilter('StripTags')
    ->addFilter('StringTrim');
```

```php
// 创建验证用的 CAPTCHA

$captcha = new Zend_Form_Element_Captcha('Captcha', array(
    'captcha' => array(
        'captcha' => 'Image',
        'wordLen' => 6,
        'timeout' => 300,
        'width' => 300,
        'height' => 100,
        'imgUrl' => '/captcha',
        'imgDir' => APPLICATION_PATH . '../public/captcha',
        'font' => APPLICATION_PATH . '/public/fonts/LiberationSansRegular.ttf',
    )
);
```

```php
// 创建提交按钮

$submit = new Zend_Form_Element_Submit('submit');

$submit->setLabel('Submit Entry')
    ->setOrder(100)
    ->setOptions(array('class' => 'submit'));
```

```php
// 将元素绑定到表单

$this->addElement($name)
    ->addElement($email)
    ->addElement($tel)
    ->addElement($address);
```

```php
// 创建卖家信息显示组

$this->setDisplayGroup(
    array('SellerName', 'SellerTel', 'SellerAddress', 'contact'),
    $this->setDisplayGroup('contact')
)->setOrder(10)
    ->setLegend('Seller Information');
```

```php
// 将元素绑定到表单

$this->addElement($title)
    ->addElement($year)
    ->addElement($country)
    ->addElement($denomination)
    ->addElement($type)
    ->addElement($grade)
    ->addElement($priceMin)
    ->addElement($priceMax)
    ->addElement($notes);
```

```php
// 创建项目信息显示组

$this->setDisplayGroup(
    array(
        'Title',
        'Year',
        'CountryID',
        'Denomination',
        'TypeID',
        'GradeID',
        'SalePriceMin',
        'SalePriceMax',
        'Description',
        'item'
    ),
    'item'
)->setOrder(20)
    ->setLegend('Item Information');

// 将元素绑定到表单

$this->addElement($captcha);

// 创建 CAPTCHA 显示组

$this->setDisplayGroup(
    array('Captcha', 'verification'),
    'verification'
)->setOrder(30)
    ->setLegend('Verification Code');

// 将元素绑定到表单

$this->addElement($submit);
```

```php
public function getCountries()
{
    $q = Doctrine_Query::create()
        ->from('Square_Model', 'c');

    return $q->fetchArray();
}

public function getGrades()
{
    $q = Doctrine_Query::create()
        ->from('Square_Model', 'g');

    return $q->fetchArray();
}

public function getTypes()
{
    $q = Doctrine_Query::create()
        ->from('Square_Model', 't');

    return $q->fetchArray();
}
```

这些内容你在第 3 章中已经熟悉。此表单包含了文本输入字段和选择列表，与之前的数据库字段紧密对应。所有字段都使用了 `HtmlEntities` 和 `StringTrim` 输入过滤器，许多字段还包含了验证器。特别注意使用正则表达式验证器来验证名称和电话号码。正如第 3 章所示，为了提高可用性，表单元素被组织成显示组，某些情况下也使用了自定义错误消息。

### 定义控制器和视图

然而上述代码中表单定义最有趣的地方在于使用 Doctrine 方法来填充三个选择列表。注意该类包含了辅助方法 `getCountries()`、`getGrades()` 和 `getTypes()`，它们在内部调用第 4 章创建的 Doctrine 模型从主表中获取选项。这些选项通过 `addMultiOption()` 方法附加表单元素。

上一节定义的表单操作 URL 指定为 `/catalog/item/create`。根据标准的框架命名规范，这对应于“catalog”模块中的 `ItemController::createAction`。该控制器是在第 4 章创建的；现在需要用新操作进行更新。代码如下：

```php
<?php

class Catalog_ItemController extends Zend_Controller_Action
{
    public function createAction()
    {
        // 生成输入表单

        $form = new Square_Form_ItemCreate;

        $this->view->form = $form;

        // 测试有效输入

        // 如果有效，填充模型

        // 为某些字段分配默认值

        // 保存到数据库

        if ($this->isValid($this->getRequest()->isPost())) {
            $item = new Square_Model_Item;

            $item->fromArray($form->getValues());

            $item->RecordDate = date('Y-m-d', time());

            $item->DisplayUntil = null;

            $item->save();

            $id = $item->RecordID();

            $this->_helper->getHelper('FlashMessenger')->addMessage(
                '您的提交已被接受，项目编号 #' . $id
                . '. 管理员将进行审核，如果通过，将在 48 小时内出现在网站上。'
            );

            $this->redirect('/catalog/item/success');
        }
    }

    public function successAction()
    {
        if ($this->_helper->getHelper('FlashMessenger')->getMessages()) {
            $this->view->messages = $this->_helper
                ->getHelper('FlashMessenger')
                ->getMessages();
        } else {
            $this->redirect('/');
        }
    }
}
```

假设表单输入有效，`createAction()` 方法会创建 Item 模型的实例并使用通过 Web 表单提交的输入填充它。对输入数据的任何必要自定义调整（例如将接收者的显示状态设置为隐藏）在此处完成，并通过调用模型的 `save()` 方法将记录保存到数据库，该方法会构建并执行必要的 `INSERT` 查询。过程中的任何错误都将作为 Doctrine 异常并传递给默认异常处理器进行解决。

如果记录保存，状态消息会被添加到 FlashMessenger，并转移到 `successAction()` 方法，该方法渲染成功视图。根据惯例，此视图脚本位于 `$APP_DIR/application/modules/catalog/views/scripts/item/success.phtml`。它看起来如下：

```html
<h2>成功</h2>

<?php echo implode($this->messages); ?>
```

### 专家问答

- **Q:** 为什么在之前的示例中保存记录后，你重定向到 `successAction()`，而不是直接在 `createAction()` 中渲染成功视图？
- **A:** 这是在任何成功的 POST 操作后都应该遵循的方法，特别是为了避免所谓的“双重提交（double post）”问题。考虑一下，在 `createAction()` 直接渲染成功视图的情况下，如果应用程序用户在成功视图渲染后点击浏览器的刷新/重新加载按钮，会导致相同的数据再次 POST 到服务器。然而，通过将成功消息存储在 FlashMessenger 操作辅助程序中并定向到 `successAction()` 来渲染此成功视图，问题被完全消除了；在这种场景下刷新页面将再次生成成功视图（而不会引起双重提交），或者将客户端重定向到索引页。

## 第 5 章：处理 CRUD 操作

同样，输入表单脚本位于 `$APP_DIR/application/modules/catalog/views/scripts/item/create.php`，其内容如下：

```php
<h2>Add Item</h2>

<?php echo $this->form; ?>
```

这就完成了！要查看运行效果，请访问 URL `http://square.localhost/catalog/item/create`，你将看到一个如图 5-1 所示的表单。  
在表单中输入值并提交。如果输入通过了验证，将创建一个新记录并插入到 item 表中，然后渲染成功视图。图 5-2 展示了成功提交的结果。

你可以通过在 URL `http://square.localhost/catalog/item/display/xx` 访问第 4 章中的 `ItemController::displayAction` 来验证记录是否成功插入，其中 xx 是新插入记录的 ID。

如果你的输入无效，表单将重新渲染并显示错误消息，说明哪里出了问题，如图 5-3 所示。

图 5-1 向 SQUARE 目录添加新物品的表单

图 5-2 成功向 SQUARE 目录添加新物品的结果

图 5-3 使用无效输入值提交表单的结果

## 处理管理操作

此时，SQUARE 应用程序的一个核心目标——允许卖家直接上传可用邮票的列表——已经实现。然而，这些内容并不会在公共领域立即可见，因为应用程序管理员必须手动审核已的物品，并批准其显示或将其从数据库中移除。这正是 SQUARE 管理面板大显身场的地方。

SQUARE 管理面板是应用程序中专门为应用程序管理员保留的一个部分。它为管理员提供了更新、查看和删除目录项的接口，它是演示如何实现剩余 CRUD 操作的绝佳场所。但在深入代码之前，最好了解在 Zend Framework 应用程序上下文中处理管理操作的不同方法。这里有三个方面需要考虑：结构、路由和布局。

### 结构（Structure）

在模块化应用程序中，管理操作有多种结构组织方式：

- 在默认模块中创建一个单一控制器，包含应用程序所有的管理操作。在这种方法下，单个控制器将包含程序所有模块的管理操作（见图 5-4）。除非是非常小的应用程序，否则不建议使用这种方法，因为单个控制器可能会迅速膨胀到非常大，影响性能和可维护性。

- 创建一个独立的模块，包含应用程序所有的管理操作。这个新模块将包含应用程序管理操作的各个控制器，每个模块一个控制器（见图 5-5）。这是一种常用方法，但如图 5-5 所示，它也并不容易维护，因为你最终会得到管理每个模块内多个控制器的单一控制器。在构建自包含的模块时，这也是理想的，因为每个模块的操作并不存储在同一个文件系统位置。

![](img/222e7e58871b088cc6397852e1452b57_158_0.png)

图 5-4 单一控制器中的管理操作

![](img/222e7e58871b088cc6397852e1452b57_158_1.png)

图 5-5 独立模块中的管理控制器

- 在每个模块内创建一个独立的控制器，包含该模块所有的管理操作。在这种方法下，每个模块至少包含两个控制器：一个用于公共操作，另一个用于相应的管理操作（见图 5-6）。出于各种原因，推荐这种方法：它在逻辑和物理视角上都是合理的，因为特定模块的所有操作都存储在同一个文件系统位置；它足够容易维护；而且足够灵活，可以适应不同的目的。

![](img/222e7e58871b088cc6397852e1452b57_159_0.png)

### 路由（Routing）

为了确保一致性，让管理路由模仿其对应的公共路由通常是一个好主意。例如，如果公共路由是 `article/edit/5`，那么对应的管理路由可能是 `/admin/article/edit/5` 形式；使用 `/admin` 前缀是为了为应用程序功能标记一个清晰且一致的接口，同时保持简单性。如果以后（例如）决定同样暴露 REST 或 SOAP 功能，这种一致性就尤为重要了。

与其他框架不同，Zend Framework 不内置管理路由。因此，有必要手动配置这些路由，通过在应用程序配置文件指定指定，或者通过扩展基础路由器来使其能够“感知前缀”。前者的示例位于代码所示；请查看列表末尾的示例：

```ini
resources.router.routes.list.route = /admin/routes/index
resources.router.routes.list.defaults.module = system
resources.router.routes.list.defaults.controller = articles
resources.router.routes.list.defaults.action = list

resources.router.routes.view.route = /admin/routes/view
resources.router.routes.view.defaults.module = system
resources.router.routes.view.defaults.controller = articles
```



`resources.router.routes.view.defaults.action = view`

`resources.router.routes.update.route = /admin/routes/update`

`resources.router.routes.update.defaults.module = system`

`resources.router.routes.update.defaults.controller = articles`

`resources.router.routes.update.defaults.action = update`

```ini
resources.router.routes.delete.route = /admin/routes/delete

resources.router.routes.delete.defaults.module = system

resources.router.routes.delete.defaults.controller = articles

resources.router.routes.delete.defaults.action = delete
```

> 图 5-6 每个模块内的管理控制器

## 142 Zend Framework：入门指南

### 布局（Layout）

默认情况下，所有视图将使用应用程序配置文件中的主布局。客户通常要求应用程序的管理视图具有不同的外观，可能是为了审美，也可能是为了在视觉上提醒他们已进入应用程序的不同部分。

在 Zend Framework 中实现并不困难：只需为管理视图创建一个新布局，然后在需要的操作中进行切换。

这是一个示例：

```php
class SandboxExampleController extends Zend_Controller_Action {

    public function adminDeleteAction() {

        $this->_helper->setLayout('admin');

        // continue

    }

}
```

当处理大量操作时，这样做可能非常麻烦（而且难以维护）。因此，另一种方法是在渲染视图之前，在控制器的 `init()` 或 `preDispatch()` 方法中检查并自动切换布局。这种方法将在下一节详细介绍。

## 尝试 5-2 列出、删除和更新数据库记录

考虑到所有背景信息，让我们开始构建 SQUARE 管理面板。正如之前提到的，为了保持简单，我们假设管理员只需要查看、编辑和删除目录中的物品。接下来的章节将详细讨论这些功能。

### 设置管理布局

第一步是为管理视图定义一个新的主布局。由于此布局的主要目的是将管理界面与公共界面区分开，它不需要特别复杂。以下是其可能样式的示例：

```html
<!DOCTYPE html PUBLIC "//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml/DTD/xhtml-strict.dtd">
```

## 第 5 章：处理 CRUD 操作

```html
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">

<head>

  <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />

  <base href="/ />

  <link rel="stylesheet" type="text/css" href="/css/master.css" />

  <link rel="stylesheet" type="text/css" href="/css/admin.css" />

  <script src="/js/form.js"></script>

</head>

<body>

  <div id="header">

    <div id="logo">

      <img src="images/logo-admin.gif" />

    </div>

  </div>

  <div id="menu">

    <a href="<?php echo $this->url(array(), 'admin-catalog-index'); ?>">目录</a>

  </div>

</div>

  <div id="content">

    <?php echo $this->layout() ->$content ?> own  </div>

  <div id="footer">

    <p>创建于 <a href="http://framework.zend.com/">Zend Framework/</a>。遵循 <a href="http://www.creativecommons.org/">Creative Commons/</a> 许可。</p>

  </div>

</body>

</html>
```

就像你在第 2 章中所做的那样，将此布局模板保存到应用程序的布局目录 `$APP_DIR/application/layouts/admin.php`。

你会发现该布局还使用了三个额外的资源——一个 CSS 文件、一个 JavaScript 文件和一个 logo 图片。这些文件需要位于应用程序的公共区域，以便连接客户端可以通过 HTTP 获取它们。你可以在本章的代码归档中找到这些资源，该归档可以从书籍配套网站 `http://www.zf-beginners-guide.com/` 下载。

下一步是设置相关项，使得每当路由器遇到带有 `/admin` 前缀的 URL 时，框架会自动将默认布局切换到新的管理布局。正如之前讨论的，实现此点的方法之一是在每个路由定义中指定新布局的名称。然而，更简单的选项是在控制器的 `preDispatch()` 方法中执行此切换，该方法会在 action 被调用之前自动执行。

（续）

## 144 Zend Framework：初学者指南

### 专家问答

**Q：什么是 `preDispatch()` 方法？**

**A：`preDispatch()` 方法是一个特殊的“存根”方法，由控制器在请求的 action 被调用之前自动执行。它对于预处理、日志记录或在将请求传递给指定的 action 之前对其内容进行其他操作非常有用。而且，如果你好奇的话，还有一个 `postDispatch()` 方法，它在请求的 action 被调用后由控制器自动执行。**

此代码应添加到 `Catalog_AdminItemController` 文件 `$APP_DIR/modules/catalog/controllers/AdminItemController.php` 中，如下例所示：

```php
<?php

class Catalog_AdminItemController extends Zend_Controller {

    // 处理管理 URL 的 action

    public function preDispatch()

    {

        // 检查 URL 是否匹配 /admin 模式

        // 设置管理布局

        $url = $this->getRequest()->getRequestUri();

        $this->_helper->layout->setLayout('admin');

    }

}
```

这段代码检查当前请求并使用 `setLayout()` 方法切换到管理布局模板。

### 定义自定义路由

下一步是为管理功能定义自定义路由。此时有必要对这些路由的样式做出一些假设，让我们假设：

1. 摘要列表 URL 的形式为 `/admin/catalog/item/index`。
2. 所有显示 URL 的形式为 `/admin/catalog/item/display/xx`，其中 `xx` 是表示记录 ID 的变量。
3. 所有更新 URL 的形式为 `/admin/catalog/item/update/xx`，其中 `xx` 是表示记录 ID 的变量。
4. 所有删除 URL 的形式为 `/admin/catalog/item/delete/xx`，其中 `xx` 是表示记录 ID 的变量。

要设置与资源 URL 对应的自定义路由，请将以下路由定义添加到应用程序配置文件 `$APP_DIR/application/configs/application.ini` 中：

```ini
resources.router.routes.admin-catalog-index.route = /admin/catalog/item/index

resources.router.routes.admin-catalog-index.defaults.module = catalog

resources.router.routes.admin-catalog-index.defaults.controller = admin.item

resources.router.routes.admin-catalog-index.defaults.action = index

resources.router.routes.admin-catalog-display.route = /admin/catalog/item/display/:id

resources.router.routes.admin-catalog-display.defaults.module = catalog

resources.router.routes.admin-catalog-display.defaults.controller = admin.item

resources.router.routes.admin-catalog-display.defaults.action = display

resources.router.routes.admin-catalog-update.route = /admin/catalog/item/update/:id

resources.router.routes.admin-catalog-update.defaults.module = catalog

resources.router.routes.admin-catalog-update.defaults.controller = admin.item

resources.router.routes.admin-catalog-update.defaults.action = update

resources.router.routes.admin-catalog-delete.route = /admin/catalog/item/delete/:id

resources.router.routes.admin-catalog-delete.defaults.module = catalog

resources.router.routes.admin-catalog-delete.defaults.controller = admin.item

resources.router.routes.admin-catalog-delete.defaults.action = delete
```

## 第 5 章：处理 CRUD 操作

## 146 Zend Framework：初学者指南

### 定义 Action 和视图

有了这些准备工作，我们就可以开始编写代码了。考虑以下 `indexAction`，它从数据库获取记录列表并将其附加到视图：

```php
<?php

class Catalog_AdminItemController extends Zend_Controller {

    // 处理管理 URL 的 action

    public function indexAction()

    {

        $q = Doctrine_Query::create()

            ->from('item', 'i')

            ->select('*');

        $this->view->records = $q->fetchArray();

    }

}
```

视图接收并格式化信息。脚本如下（按照约定，它应保存为 `$APP_DIR/application/views/admin/item/index.php`）：

```php
<h2>项目列表</h2>

<?php if (count($this->records)) : ?>

<div id="records">

<form method="post" action="admin-delete">

<table>

  <tr>

    <th>项目 ID</th>

    <th>标题</th>

    <th>面值</th>

    <th>等级</th>

    <th>年份</th>

    <th>显示</th>

    <th>更新</th>

  </tr>

  <?php foreach ($this->records as $r): ?>

  <tr>

    <td><input type="checkbox" name="ids[]" value="<?php echo $r['RecordID']; ?>" style="width:2px" /></td>

    <td><?php echo $this->escape($r['RecordID']); ?></td>

    <td><?php echo $this->escape($r['Title']); ?></td>

    <td><?php echo $this->escape(sprintf('%1.2f', $r['Denomination'])); ?></td>

    <td><?php echo $this->escape($r['Country']); ?></td>

    <td><?php echo $this->escape($r['Year']); ?></td>

    <td><a href="<?php echo $this->url(array('id' => $r['RecordID'], 'admin-display')); ?>)">显示</a></td>

    <td><a href="<?php echo $this->url(array('id' => $r['RecordID'], 'admin-update')); ?>)">更新</a></td>

  </tr>

  <?php endforeach; ?>

  <tr>

    <td colspan="10"><input type="submit" name="submit" style="width:150px" value="删除所选" /></td>

  </tr>

</table>

</form>

</div>

<?php else : ?>

未找到记录

<?php endif; ?>
```

在查看视图之前，有几个点点需要注意：

- 所有字段值在渲染之前都经过了转义（escape）。正如第 4 章所述的，这是你在处理输出值时应该采取的一种基本安全措施，以降低 CSRF 和 XSS 攻击的风险。
- 显示 `<table>` 被封装在 `<form>` 内部。这是为了处理每条记录旁出现的复选框，以实现多条记录删除。请注意，此表单是在视图脚本中手动生成的，而不是通过 Zend_Form 创建的，因为在 Zend_Form 中没有简单的方法可以创建这种“表单+表格”的组合。
- 每条记录都带有“更新（Update）”和“显示（Display）”链接。这些链接对应上一节中配置的路由，并在运行时使用 `url()` 辅助函数动态生成。注意记录 ID 作为 GET 参数包含在请求 URL 中。

要查看此视图的运行效果，启动浏览器并指向 `http://square.localhost/admin/catalog/item/index`。你应该看到一个如图 5-7 所示的摘要页面。

## 定义删除操作

当用户选择一个或多个记录进行删除时，所选的记录 ID 将以数组的形式 POST 到 `Catalog_AdminController::deleteAction`。该 `deleteAction()` 方法读取所选的 ID 和 Doctrine 模型，以构建一个 DELETE 查询，将它们从数据库中删除。如下所示：

```5-7
SQUARE 管理面板中的目录摘要页
```



```php
<?php
class Catalog_AdminItemController extends Zend_Controller_Action
{
    // 删除目录项的操作
    public function deleteAction()
    {
        // 为 POST 输入设置过滤器和验证器
        $filters = array(
            'ids' => array('HtmlEntities', 'StripTags', 'StringTrim'),
        );
        $validators = array(
            'ids' => array('NotEmpty', 'Int')
        );
        $input = new Zend_Filter_Input($filters, $validators);
        $input->setData($this->getRequest()->getParams());

        // 测试输入是否有效
        // 读取记录标识数组
        // 从数据库中删除记录
        if ($input->isValid()) {
            $q = Doctrine_Query::create()
                ->delete('Square_Model_Item i')
                ->where('i.RecordID', $input->ids);
            $result = $q->execute();

            $this->_helper->getHelper('FlashMessenger')
                ->addMessage('The records were successfully deleted.');
            $this->redirect('/admin/catalog/item/success');
        } else {
            throw new Zend_Controller_Action_Exception('Invalid input');
        }
    }

    // 操作
    public function successAction()
    {
        if ($this->_helper->getHelper('FlashMessenger')) {
            $this->_view->messages = $this->_helper
                ->getHelper('FlashMessenger')->getMessages();
        } else {
            $this->redirect('/admin/catalog/item/index');
        }
    }
}
```

（续）

**图 5-8** 在 SQUARE 管理面板中成功删除项目的结果。

要查看此效果，请在摘要页面上勾选相应的复选框选择一个或多个记录进行删除，然后使用“删除选中（Delete Selected）”按钮提交表单。记录应从数据库中删除，并且你会收到一个如图 5-8 所示的成功消息。

## 定义更新表单

管理员拥有能够更新特权用户无法更新的更多记录字段的能力，这是非常常见的。例如，在 SQUARE 应用中，除了通常的项目描述字段外，管理员还应该能够更新项目的显示状态，并定义项目在公共目录中可见的期限。

`Zend_Form` 采用面向对象的表单创建方法，特别适合满足这一需求。利用继承和扩展的 OOP 概念，可以通过扩展父类并通过 `Zend_Form::addElement()` 和 `removeElement()` 方法添加或删除表单元素来派生子表单类。

为了说明，请考虑以下 `UpdateForm` 类，它继承自本章开头创建的 `ItemCreate` 类。该子类与其父类共享许多输入元素；但由于它仅供管理员使用，因此删除了不需要的元素（CAPTCHA 输入），并添加了必要的元素（显示状态和数据输入）。代码如下：

```php
<?php
class Square_Form_ItemUpdate extends Square_Form_ItemCreate
{
    public function init()
    {
        // 获取父表单
        parent::init();

        // 设置操作（设置为当前 URL 为 false）
        $this->setAction('/admin/catalog/item/update');

        // 移除不需要的元素
        $this->removeElement('Captcha');
        $this->removeDisplayGroup('verification'); 
    }

// 为项目 ID 创建隐藏输入
$id = new Zend_Form_Element_Hidden('RecordID');
$id->addValidator('Int')
  ->addFilter('HtmlEntities')
  ->addFilter('StringTrim');

// 为显示状态创建选择输入
$display = new Zend_Form_Element_Select('DisplayStatus');
array('onChange' => 
  'javascript:handleInputDisplayOnSelect('DisplayStatus',divDisplayUntil,new Array(\'1'));
$display->setLabel('Display status:')
  ->setRequired(true)
  ->addValidator('Int')
  ->addFilter('HtmlEntities')
  ->addFilter('StringTrim');

// 为显示状态创建选择输入
$displayUntil = new Zend_Form_Element_Hidden('DisplayStatus');
$displayUntil->addValidator('Int')
  ->addFilter('HtmlEntities')
  ->addFilter('StringTrim');

// 为显示状态创建选择输入
$displayDay = new Zend_Form_Element_Select('DisplayStatus');
$displayDay->addValidator('Int')
  ->addFilter('HtmlEntities')
  ->addFilter('StringTrim');

// 为显示状态创建选择输入
$displayMonth = new Zend_Form_Element_Select('DisplayStatus');
$displayMonth->addValidator('Int')
  ->addFilter('HtmlEntities')
  ->addFilter('StringTrim');

// 为显示状态创建选择输入
$displayYear = new Zend_Form_Element_Select('DisplayStatus');
$displayYear->addValidator('Int')
  ->addFilter('HtmlEntities')
  ->addFilter('StringTrim');
```

## Zend Framework：入门指南

## 定义更新操作与视图（View）

更新记录通常涉及两个不同的查询：

1. 第一个查询是读取查询，在用户选择某条记录进行更新时发生。`updateAction()` 必须从数据库读取所选的记录，用数据库中当前存储的字段值预填充 Web 表单，并将此表单渲染给用户。

2. 第二个查询是写入查询，在用户提交表单时发生。`updateAction()` 必须接收、过滤并验证提交的值。如果值有效，则该操作必须将记录的新版本写入数据库。

`Catalog_AdminItemController::updateAction` 执行了这两个功能。它的样子如下：

```php
<?php
class Catalog_AdminItemController extends Zend_Controller
{
    // 修改单个目录条目
    public function updateAction()
    {
        // 生成输入表单
        $form = new Square_Form_ItemUpdate();
        $this->view = $form;

        if ($this->getRequest()->isPost()) {
            // 如果是 POST 请求
            // 测试输入是否有效
            // 获取当前记录
            // 更新值并替换数据库数据
            $postData = $this->getRequest()->getPost();
            $postData['DisplayUntil'] = sprintf('%04d-%02d-%02d',
                $this->getRequest()->getPost('DisplayUntil_year'),
                $this->getRequest()->getPost('DisplayUntil_month'),
                $this->getRequest()->getPost('DisplayUntil_day'));

            if (isValid($postData)) {
                $input = $form->getValues();
                $item = Doctrine::table('Square_Model_Item')
                    ->find($input['RecordID']);
                $item->fromArray($input);
                $item->DisplayUntil =
                    ($item->DisplayStatus == 0) ? null : $item->DisplayUntil;
                $item->save();
                $this->helper->getHelper('FlashMessenger')
                    ->addMessage('The record was successfully updated.');
                $this->redirect('/admin/catalog/item/success');
            }
        } else {
            // 如果是 GET 请求
            // 为 GET 输入设置过滤器和验证器
        }
    }
}
?>
```

## 第 5 章：处理 CRUD 操作

```php
// 测试输入是否有效
// 获取请求的记录
// 预填充表单
$filters = array(
	'id' => array('HtmlEntities', 'StripTags', 'StringTrim'),
);
$validators = array(
	'id' => array('NotEmpty', 'Int')
);
$input = new Zend_Filter_Input($filters, $validators);
$input->setData($this->getRequest()->getParams());
if ($input->isValid()) {
$q = Doctrine_Query::create()
    ->from('Square_Model_Item i')
    ->leftJoin('i.Square_Model_Grade c')
    ->leftJoin('i.Square_Model_Type t')
    ->where('i.RecordID = ?', $input->id);
$result = $q->execute();
if (count($result)) {
    // 执行日期选择执行调整
    $date = $result[0]['DisplayUntil'] = date('d', strtotime($date));
    $result[0]['DisplayUntil_month'] = date('m', strtotime($date));
    $result[0]['DisplayUntil_year'] = date('Y', strtotime($date));
    $this->view->form->populate($result[0]);
} else {
    throw new Zend_Controller_Action_Exception('Page not found', 404);
}
} else {
    throw new Zend_Controller_Action_Exception('Invalid input');
}
```

广义来说，此 `updateAction()` 方法由两个部分组成，通过条件划分：

1. 如果请求是 POST 请求，操作获取 POST 输入并创建一个 YYYY-MM-DD 格式的复合字符串，如前面的讨论。它使用 `Zend_Form` 对象的 `isValid()` 方法来测试输入是否有效。假设输入有效，操作使用 Doctrine `find()` 方法获取记录。

2. 如果请求是 GET 请求，操作从 URL 获取 ID，对其进行验证并执行查询以获取记录。然后它使用 `Zend_Form` 的 `populate()` 方法用当前值预填充表单。对应的视图应保存为 `$APP_DIR/modules/catalog/views/item/update.php`：

```html
<h2>更新条目</h2>
<?php echo $this->form; ?>
```

要查看此效果，请使用管理面板，例如 `http://localhost/admin/catalog/item/1`。注意，此 `updateAction()` 还考虑了显示状态。

## 更新显示

| 显示状态 | 显示直到 |
|---|---|
| 可见 | 19 |
| 隐藏 | 20 |

通过此更改，只有被标记为可见的项目才能通过接口访问。任何访问其他项目的尝试将抛出 404 异常，该异常将传递给默认异常处理器显示给请求客户端。

你可能奇怪为什么这一章没有包含读取单个记录（CRUD 中的 R？）的内容？这方面已经在第 4 章标题为“检索数据库记录”的节中涵盖过了，该节使用 Doctrine 模型通过 ID 读取并显示。本章讨论的管理面板包含类似的功能，你可以在本章的代码存档中找到它。代码存档可以从本书的配套网站 `http://www.zf-beginners-guide.com/` 下载。

到目前为止，管理面板已经完成，管理员可以通过浏览器界面对记录执行读取、更新和删除操作。然而，这些操作目前没有任何保护，结果是任何用户都可以通过 URL 路由访问它们。这显然是一个安全风险，下一步必须实现一种机制，允许应用程序区分“无权限用户”和“管理员”，并仅允许后者访问管理功能。

# 第 5 章：处理 CRUD 操作 159

Zend Framework 包含一个专门用于处理用户身份验证任务的组件。该组件被称为 `Zend_Auth`，提供了一个 API 和一组适配器，用于根据多种数据源验证用户凭据，包括符合 SQL 的数据库系统、文本文件、LDAP 目录和 OpenID 提供者。通过验证的身份将由 `Zend_Auth` 自动存储在会中，控制器或操作可以随时对其进行检索或重新验证。

### 注意

默认情况下，`Zend_Auth` 仅支持基于会话的存储。然而，只需通过扩展 `Zend_Auth_Storage` 接口类即可添加对其他存储机制的支持。更多信息以及如何操作的示例可以在本章末尾的链接中找到。

为了理解这在实践中是如何工作的，请考虑以下示例：



```php
<?php
class Sandbox_ExampleController extends Zend_Controller
{
    public function authenticateAction(){
        // generate a login form
        $form = new Form_Example_Auth;
        $this->view->form = $this->getRequest()->isPost()
        if ($form->isValid($this->getRequest()->Post())) {
            // get credentials from user input
            // initialize authentication adapter
            // perform authentication and test result
            $values = $form->getValues();
            $adapter = new Zend_Auth_Adapter_DbTable($this->db);
            $adapter->setIdentity($values['username'])
                ->setCredential($values['password']);
            $auth = Zend_Auth::getInstance();
            $result = $auth->authenticate($adapter);
            if ($result->isValid()){
                $this->helper->getHelper('FlashMessage')
                    ->addMessage('You were successfully logged in.');
                $this->redirect('/admin/index/');
            } else {
                $this->view->message =
                    'You could not be logged in. Please try again.';
            }
        }
    }
}
```

## Zend Framework：学者指南

此示例使用了 `DbTable` 数据库身份验证适配器，该适配器使用 `Zend_Db_Adapter_Abstract` 类的实例进行初始化。向该适配器传递一组凭据，然后使用 `Zend_Auth` 单例对这些凭据进行身份验证。`Zend_Auth::authenticate` 方法的返回值是一个 `Zend_Auth_Result` 对象；该对象可以通过其 `isValid()` 方法进行测试，以确定身份验证成功还是失败。

`Zend_Auth` 还暴露了许多其他方法，可以在单个控制器和执行器中使用，以验证是否存在已验证的会话。例如，`hasIdentity()` 方法返回一个布尔值，表示是否存在已验证的用户会话，而 `getIdentity()` 方法返回已验证用户的身份。这些方法可以从各个操作中调用，以测试用户是否已通过身份验证，从而允许或拒绝用户的操作。

这里有一个示例，确保 `protectedAction()` 仅对已身份验证的用户可用：

```php
class SandboxExampleController extends Zend_Controller_Action
{
    public function protectedAction()
    {
        // check if user is authenticated
        // if no, redirect to login page
        // if yes, proceed as normal
        if (!Zend_Auth::getInstance()->hasIdentity()) {
            $this->redirect('/admin/login');
        } else {
            $model = new MemberModel();
            $this->view->data = $model->fetchAll();
        }
    }
}
```

同样，通过简单扩展基类 `Zend_Auth_Adapter_Interface` 类，也可以创建根据其他源验证凭据的自定义身份验证适配器。该类至少必须实现一个接受用户凭据的构造函数，以及一个根据身份验证提供者验证这些凭据的 `authenticate()` 方法。`authenticate()` 方法的返回值必须是 `Zend_Auth_Result` 类的实例，并带有一个常量来指示身份验证是否成功。你将在下一节中看到其中一个自定义身份验证适配器的示例。

### 尝试 5-3 创建登录/注销系统

`Zend_Auth` 是那些难以解释的组件之一，通过实际示例可以得到更好的理解。基于如此，让我们在实际语境中让它运行起来，通过构建一个简单的登录/注销系统来保护对 SQUARE 管理面板的访问。后续章节将引导你完成这一过程。

### 定义自定义路由

一如既往，良好的开始点是路由定义。通过在位于 `$APP_DIR/application/configs/application.ini` 的应用程序配置文件中添加以下定义，为你的管理面板定义登录和注销路由：

```
resources.router.routes.login = /admin/login
resources.router.routes.login.defaults.module = default
resources.router.routes.login.defaults.controller = login
resources.router.routes.login.defaults.action = login
```

```
resources.router.routes.login-success.route = /admin/login/success
resources.router.routes.login-success.defaults.module = default
resources.router.routes.login-success.defaults.controller = login
resources.router.routes.login-success.defaults.action = success
```

```
resources.router.routes.logout.route = /admin/logout
resources.router.routes.logout.defaults.module = default
resources.router.routes.logout.defaults.controller = login
resources.router.routes.logout.defaults.action = logout
```

## 定义登录表单

下一步是定义登录表单本身。这不需要非常复杂——你真正只需要一个用户名字段、一个密码字段和一个提交按钮。以下是表单定义，应该保存为 `$APP_DIR/library/Square/Form.php`：

```php
<?php
class Square_Form_Login extends Zend_Form
{
    public function init()
    {
        // initialize form
        $this->setAction('/admin/login')
        ->setMethod('post');

        // create text input for name
        $username = new Zend_Form_Element_Text('username');
        $username->setLabel('Username:')
        ->setOptions(array('size' => '30'))
        ->setRequired(true)
        ->addValidator('Alnum')
        ->addFilter('HtmlEntities')
        ->addFilter('StringTrim');

        // create text input for password
        $password = new Zend_Form_Element_Password('password');
        $password->setLabel('Password:')
        ->setOptions(array('size' => '30'))
        ->setRequired(true)
        ->addFilter('HtmlEntities')
        ->addFilter('StringTrim');

        // create submit button
        $submit = new Zend_Form_Element_Submit('submit');
        $submit->setLabel('Log In')
        ->setOptions(array('class' => 'submit'));

        // attach elements to form
        $this->addElement($username)
        ->addElement($password)
        ->addElement($submit);
    }
}
```

# 定义身份验证适配器

上一节中的表单将其数据提交到“default”模块中的 `LoginController::loginAction`。在进入该操作的代码之前，我们需要花几分钟创建一个身份验证适配器，使其如何根据第 4 章创建的用户表验证提供的用户名和密码。

如所述，使用 `Zend_Auth` 创建自定义身份验证适配器并不困难。只需扩展基类 `Zend_Auth_Adapter_Interface` 类，并确保子类暴露一个知道执行所需身份验证的 `authenticate` 方法。更重要的问题是，当 `Zend_Auth` 已经包含内置的数据库身份验证适配器时，为什么还需要创建一个自定义适配器？

原因完全是为了效率和一致性。首先，`Zend_Auth_DbTable` 适配器仅适用于 `Zend_Db` 类的实例，无法直接与 Doctrine 模型配合。而 `Zend_Db` 预期的数据库连接参数格式与 Doctrine 预期的格式不同。因此，为了直接使用 `Zend_Auth_Adapter_DbTable`，需要在应用程序配置文件中以不同的格式指定相同的数据库连接参数（这意味着每次更新...

## 第 5 章：处理 CRUD 操作

`Zend_Db` 期望的数组格式（由于可能的 DSN 变体很多，非常繁琐且容易出错）。

此外还有一致性的小问题。到目前为止，所有的数据库访问都是通过 Doctrine 模型进行的。仅为了身份验证查询切换到 `Zend_Db` 会令人困惑；而且由于应用程序现在需要加载两套库而不是一套，这在效率也是低的。出于各种考虑，创建一个使用 Doctrine 的自定义身份验证适配器是合理的，而不是使用提供的 `Zend_Auth_Adapter_DbTableadapter`。

解释完这些之后，让我们进入实际代码。考虑下面的列表，它创建了一个符合 `Zend_Auth` 规范的 Doctrine 身份验证适配器：

```php
<?php
class Square_Auth_Adapter_Doctrine implements Zend_Auth_Adapter_Interface
{
    // 已认证用户记录的数组
    protected $resultArray;

    // 构造函数
    // 接收用户名和密码
    public function __construct($username, $password)
    {
        $this->username = $username;
        $this->password = $password;
    }

    // 主要身份验证方法
    // 查询数据库以匹配身份验证凭据
    // 返回带有成功/失败代码的 Zend_Auth_Result
    public function authenticate()
    {
        $q = Doctrine_Query::create('u')
            ->where('u.Username = :username AND u.Password = PASSWORD(?)')
            ->array('username' => $this->username, 'password' => $this->password);

        $result = $q->fetchArray();
        if (count($result) == 1) {
            return new Zend_Auth_Result(
                Zend_Auth_Result::SUCCESS, $this->username, array());
        } else {
            return new Zend_Auth_Result(
                Zend_Auth_Result::FAILURE, null,
                array('Authentication unsuccessful')
            );
        }
    }

    // 返回代表认证用户记录的数组
    // 根据需要排除指定的用户字段
    public function getResultArray($excludeFields = null)
    {
        if (!$this->resultArray) {
            return false;
        }

        if ($excludeFields != null) {
            $excludeFields = (array)$excludeFields;
            foreach ($this->resultArray as $key => $value) {
                if (in_array($key, $excludeFields)) {
                    unset($this->resultArray[$key]);
                }
            }
        }
        return $this->resultArray;
    }
}
```

将此类选择为 `$APP_DIR/library/Square/Auth/Adapter/Doctrine.php`。该类中的主要工作是 `authenticate()` 方法，它执行查询以检查提供的用户名和密码是否有效。该方法返回 `Zend_Auth_Result` 实例，包含三个属性：一个指示成功或失败的代码，成功时的用户名（或身份），以及在未成功时包含错误消息的数组。

除了简单的成功和失败指示外，还有许多其他结果代码可用。这些代码可以提供有关身份验证失败的更具体信息——例如，失败是与用户名还是密码有关，用户记录是否存在歧义，或其他类型的错误。这些结果代码的完整列表可以在 Zend Framework 手册中找到。

虽然 `authenticate()` 方法返回用户是否通过身份验证，但 `getResultArray()` 方法以数组形式返回已认证用户的完整用户记录。该方法可选地接收要排除的字段列表，并从返回的数组中删除它们。这是一个包含在适配器中的非常方便的方法，因为它允许一次性访问整个用户记录，并方便在会话中持久化用户记录以便其他操作。你将在下一节中看到此示例。

### 定义登录 Action 和视图

将大部分困难工作委派给身份验证适配器后，创建 `LoginController::loginAction` 变得轻而易举。以下是代码，应保存为 `$APP_DIR/application/default/controllers/LoginController.php`：



```php
<?php
class LoginController extends Zend_Controller_Action
{
    public function init()
    {
        $this->helper->setLayout('admin');
    }

    // 登录 action
    public function loginAction()
    {
        $form = new Square_Form_Login;
        $this->view->form = $form;

        // 检查有效输入
        // 将用户记录到会话
        // 如果存在则重定向到原始 URL
        if ($this->getRequest()->isPost()) {
            if ($form->isValid($this->getRequest())) {
                $values = $form->getValues();
                $adapter = new Square_Auth_Adapter_Doctrine(
                    $values['username'], $values['password']
                );
                $auth = Zend_Auth::getInstance();
                $result = $auth->authenticate($adapter);

                if ($result->isValid()) {
                    $session = new Zend_Session_Namespace('auth.auth');
                    $session->user = $adapter->getResultArray('Password');

                    if (isset($session->requestURL)) {
                        $url = $session->requestURL;
                        unset($session->requestURL);
                        $this->redirect($url);
                    } else {
                        $this->helper->getHelper('FlashMessenger')
                            ->addMessage('You were successfully logged in.');
                        $this->redirect('/admin/login/success');
                    }
                }
            } else {
                $this->view->message =
                    'You could not be logged in. Please try again.';
            }
        }
    }
}
```

登录视图脚本`$APP_DIR/application/default/views/login.php`如下：

```html
<h2>登录</h2>
<div style="color:red; font-weight:bold">
    <?php echo $this->message; ?>
</div>
<?php echo $this->form; ?>
```

### 定义注销 Action

`loginAction()`的对应是`logoutAction()`，它销毁认证会话并通过`Zend_Auth::clearIdentity`方法清除身份。它如下：

```php
<?php
class LoginController extends Zend_Controller_Action
{
    public function logoutAction()
    {
        Zend_Auth::getInstance() ->clearIdentity();
        Zend_Session::destroy();
        $this->redirect('/admin/login');
    }
}
```

### 管理 Action

最后一步是为你想要保护的 action 附加身份检查。由于目前创建的所有管理操作都位于同一个控制器`Catalog_AdminItemController`中，这些检查可以方便地添加到控制器的`preDispatch()`方法中。更新后的`preDispatch()`方法如下：

```php
<?php
class Catalog_AdminItemController extends Zend_Controller_Action
{
    // 处理管理 URL 的 action
    public function preDispatch()
    {
        // 检查用户是否通过身份验证
        // 如果没有，重定向到登录页面
        $url = $this->getRequest()->getRequestUri();
        $this->_helper->setLayout('admin');

        if (!Zend_Auth::getInstance() ->hasIdentity()) {
            $session = new Zend_Session_Namespace('square.auth');
            $session->requestURL = $url;
            $this->redirect('/admin/login');
        }
    }
}
```

由于此更改，每当路由器接收到管理操作的请求时，`preDispatch()`方法将首先检查用户身份是否已身份验证。

## 168 Zend Framework：初学者指南

使用`Zend_Auth::hasIdentity`方法。如果不存在身份，该方法将返回`false`。如果发生这种情况，请求 URL 将存储在会话，客户端将被重定向到登录方法。

登录成功后，`loginAction()`（在前节中讨论过）将从会话获取请求 URL，并将客户端重定向回该 URL。此时将执行`preDispatch()`方法，由于用户的身份已经过确认，`hasIdentity()`将返回`true`，并且请求的操作将以正常方式分发。

### 更新主布局

如前一节所示，`Zend_Auth`对象的`hasIdentity()`方法提供了一个方便的测试，用于检查用户是否已经通过身份验证。这一特性在管理布局中非常好用，可以根据用户是否登录来选择性地显示菜单项。这里有一个示例，通过`APP_DIR/application/layouts/admin.phtml`在用户登录时在主区域显示“注销”项目。更改已用粗体标记。

```html
<!DOCTYPE html PUBLIC "//W3C//DTD HTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml11-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xmlns:lang="en" lang="en">
<head>
  <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
  <base href="/" />
  <link rel="stylesheet" type="text/css" href="css/master.css" />
  <link rel="stylesheet" type="text/css" href="css/admin.css" />
  <link rel="stylesheet" type="text/css" href="css/calendar.css" />
  <script src="js/form.js"></script>
</head>
<body>
  <div id="header">
    <div id="logo">
      <img src="images/logo-admin.gif" />
    </div>
  </div>
  <div id="menu">
    <?php if (Zend_Auth::hasIdentity()): ?>
    <a href="<?php echo $this->url(array(
      'admin-catalog-index');
    ));">CATALOG</a>
    <a href="<?php echo $this->url(array(), 'logout'));?>">LOGOUT</a>
    <?php else: ?>
  </div>
```

## 第 5 章：处理 CRUD 操作

```html
<a href="<?php echo $this->url(array(), 'login'); ?>">LOGIN</a>
<?php endif ?>
</div>
```

```html
<div id="content">
<?php echo $this->layout()->content ?>
</div>
<div id="footer">
<p>由 <a href="http://framework.zend.com/">Zend Framework/</a> 创建。基于 <a href="http://www.creativecommons.org/">Creative Commons</a> 许可协议。</p>
</div>
</body>
</html>
```

你已经大功告成了！要查看运行效果，请尝试访问`http://square.localhost/admin/catalog/item/index`上的摘要页面。你应该看到一个登录表单，如图 5-11 所示。

一旦你通过此表单提交了有效的凭据，你应该就会被自动重定向到摘要页面。主菜单也应该通过显示新的“注销”链接来反映你的登录状态，如图 5-12 所示。

![](img/222e7e58871b088cc6397852e1452b57_187_0.png)

图 5-12 SQUARE 管理面板中的登录后菜单

## 专家问答

**Q：**我可以使用`Zend_Auth`根据用户角色或权限来授予或拒绝应用程序资源的访问吗？

**A：**正如 Zend Framework 手册所出的，`Zend_Auth`关注的是用户验证（验证用户确实是其所声称的），而不是用户访问控制（验证用户是否有权访问特定的应用程序）。在实践中，这意味着如果通过验证，用户可以访问任何或所有受保护的操作；系统不允许对哪个用户拥有哪些操作进行细粒度的控制。如果你的应用程序需要根据用户角色控制特定操作，你应该考虑使用`Zend_Acl`组件。

### 总结

本章关注了构建 Web 应用时会遇到的最常见任务之一：实现 CRUD 操作和用户验证。在之前几节讨论的技术的基础上，它展示了如何使用 MVC 范式列出、创建、更新和删除数据库记录。它还向你介绍了`Zend_Auth`组件，并解释了如何使用简单的用户验证系统来保护对特定操作的访问。

在本章结束时，SQUARE 示例应用程序已经变得非常丰富了。用户现在可以直接向在线目录添加待售商品，而管理员有能力通过一个相当完善的管理面板审核这些列表、批准其显示、修改它们或删除它们。对这些管理功能的访问通过基本的登录/注销系统得到了保护，甚至还有一些很贴心的细节，例如自动重定向的功能。

# 第 6 章：数据的索引、搜索与格式化

（续）

## 176 Zend Framework：入门指南

```php
array('messages' => $this->messages)
->addFilter('HtmlEntities')
->addFilter('StringTrim')
->addMultiOption('', 'Any');

foreach ($this->getGrades() as $g) {
    $grade->addMultiOption($g['GradeID'], $g['GradeName']);
}

// 创建提交按钮
$submit = new Zend_Form_Element_Submit('submit');
$submit->setLabel('Search')
    ->setOptions(array('class' => 'submit'));

// 将元素添加到表单
$this->addElement($year)
    ->addElement($price)
    ->addElement($grade)
    ->addElement($submit);

// 设置元素装饰器
$this->elementDecorators(array(
    array('ViewHelper'),
    array('Label', array('tag' => '<span>'))
));

$submit->setDecorators(array(
    array('ViewHelper'),
));

public function getGrades() {
    $q = Doctrine_Query::create()
        ->from('Square_Model_g', 'g');

    return $q->fetchArray();
}
```

这是一个相当标准的表单定义，是你现在应该已经熟悉的类型：包含两个输入字段、一个选择列表和一个提交按钮，全部封装在`init()`方法中。注意，默认的`Label`装饰器已通过修改，将每个元素标签包裹在`<span>`元素中（而不是`<td>`元素），确保表单元素水平渲染而不是垂直渲染。

有一点需要注意。到此为止，在之前的所有示例中，验证错误会自动显示在相应输入元素的下方。通常，应用程序或用户界面要求将这些错误合并显示在表单顶部的单个区块中，而不是各个元素下方。实现这一点并不困难——有一个内置的`FormErrors`装饰器可以自动完成此操作——但要实现，你需要禁用默认附加到每个元素的`Errors`装饰器。上述代码中的表单定义通过`Zend_Form`对象的`setDecorators()`方法添加`FormErrors`装饰器，并专门通过`Zend_Form`对象的`setElementDecorators()`方法从应用于每个元素的装饰器列表中排除`Errors`装饰器来完成任务。

一旦你理解了表单定义，将其保存为`$APP_DIR/library/Square/Form/Search.php`。

### 定义控制器和视图

下一步是为浏览器/搜索界面定义 action 和视图。更新`$APP_DIR/modules/catalog/controllers/ItemController.php`中的`Catalog_ItemController`类，添加如下的`searchAction()`：

```php
<?php
class Catalog_ItemController extends Zend_Controller_Action
{
    public function searchAction() {
        // 生成输入表单
        $form = new Square_Form_Search;
        $this->view->form = $form;

        // 检查有效输入
        // 生成基础查询
        if ($form->isValid($this->getRequest()->getParameters())) {
            $input = $form->getValues();
            $q = Doctrine_Query::create()
                ->from('Square_Model_Item i')
                ->leftJoin('i.Square_Model_Country c')
                ->leftJoin('i.Square_Model_Grade g')
                ->leftJoin('i.Square_Model_Type t')
                ->where('i.DisplayStatus = 1')
                ->addWhere('i.DisplayUntil >= CURDATE()');
        }

        // 将条件附加到基础查询
        if (!empty($input['y'])) {
            $q->addWhere('i.Year = ?', $input['y']);
        }
    }
}
```

（续）



```php
if (!empty($input['g'])) {
    $q->addWhere('i.GradeID = ?', $input['g']);
}
if (!empty($input['p'])) {
    $q->addWhere('? BETWEEN $i.SalePriceMin AND $i.SalePriceMax',
    $input['p']);
}

// 执行查询并将结果附加到视图
$results = $q->fetchArray();
$this->view->results = $results;
```

`searchAction()` 方法首先构建一个基础查询，返回目录中所有已批准的项目列表。根据用户输入的内容，它随后向该查询附加 `Where` 子句，以根据指定的标准过滤结果集。一旦执行查询，结果将赋值给视图变量。如果提交的输入无效，验证错误消息列表也将赋值给视图变量。

视图脚本负责遍历结果集并格式化每条记录以便显示。如果有错误，将通过 `FormErrors` 装饰器显示在结果页顶部。以下是视图脚本，它应该保存为 `$APP_DIR/modules/catalog/views/scripts/search.php$`：

```html
<h2>Search</h2>
<?php echo $this->form; ?>
```

```html
<h2>Search Results</h2>
<p><?php echo count($this->results); ?> result(s) found.</p>
```

```php
<?php if (count($this->results)): { ?>
<?php $x=1; ?>
<?php foreach ($this->results as $r): { ?>
<div>
<?php echo $x++; ?>.
<a href="<?php echo $this->url('id' => $r['RecordID'], 'catalog-display'); ?>"><?php echo $this->escape($r['Title']); ?></a>
<?php echo $this->escape($r['Year']); ?>

<?php if (!empty($r['Description'])): ?>
<br><?php echo $this->escape($r['Description']); ?>
<?php endif; ?>
```

```html
<br/>
<strong>
Grade:
<?php echo $this->escape($r['Square_Model_Grade']['GradeName']); ?>
|
Country:
<?php echo $this->escape($r['Square_Model_Country']['CountryName']); ?> |
Sale price:
<?php echo sprintf('%0.2f', $r['SalePriceMin']); ?> to
<?php echo sprintf('%0.2f', $r['SalePriceMax']); ?>

<br>
</div>
<br/><?php $x++; ?>
<?php endforeach; ?>
<?php endif; ?>

<div>
<a href="<?php echo $this->url(array(
'module' => 'catalog',
'controller' => 'item',
'action' => 'create'),
null, true)); ?>">Add Item</a>
</div>
```

### 更新主布局

剩下的工作是使用 `url` 助手更新主菜单中的导航链接，以反映新的浏览器/搜索表单。要完成这一点，请更新 `$APP_DIR/layouts/master.php` 中的主布局，更改部分已加粗：

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml-strict.dtd">

<html xmlns="http://www.w3.org/1999/xhtml" lang="en">

<div id="menu">

<a href="<?php echo $this->url(array(), 'home')); ?>">HOME</a>

<a href="<?php echo $this->url(array('page' => 'services', 'static-content')); ?>">SERVICES</a>

<a href="<?php echo $this->url(array('module' => 'catalog', 'controller' => 'item', 'action' => 'search'), 'default', true)); ?>">CATALOG</a>
```

图 6-1 SQUARE 搜索表单

`img/222e7e58871b08cc639785e1452b57_199_0.png`

`img/222e7e58871b08cc639785e1452b57_199_1.png`

你也可以尝试使用无效值提交表单。内置验证器将捕获你的无效输入并在页面顶部以区块的形式显示错误消息，如图 6-3 所示。

### 添加全文搜索

当你构建应用程序搜索引擎时，有两种不同的方法可以采用。你可以创建一个基于过滤的搜索引擎，用户输入的特定标准用于过滤搜索结果列表，如上一节所示。或者，你可以创建一个全文搜索引擎，它索引应用程序内容并根据用户输入的关键词查找匹配项。在现代 Web 应用程序中，通常倾向于全文搜索，因为它通常比数据库搜索更快且结果更准确。

Zend Framework 自带一个强大的全文搜索组件，名为 `Zend_Search_Lucene`。该组件是 Apache Lucene 项目的纯 PHP 实现，用于索引各种文档类型（包括 HTML 和某些 Office 2007 格式），还可以对索引数据执行不同类型的搜索查询。

使用 `Zend_Search_Lucene` 实现全文搜索涉及两个主要操作：索引数据和搜索数据。索引扫描文档集并创建内容的索引；搜索查找此索引以找到符合用户指定的文档。以下章节提供了这两个操作的概述。

### 索引数据

`Zend_Search_Lucene` 索引由单个文档组成，每个文档可能进一步拆分为字段。当你构建索引时，`Zend_Search_Lucene` 允许对文档的每个字段进行精确控制。这里的两个基本参数是索引和存储：索引字段可用于搜索，而存储字段可以显示在结果中。字段有五种基本类型：

- 关键字（Keyword fields）不分词，但在索引中被索引和存储。
- 文本（Text fields）被分词、索引并存储。
- 未存储字段（Unstored fields）被分词并索引，但不存储。
- 未索引字段（Unindexed fields）被分词并存储，但不被索引。
- 二进制字段（Binary fields）不分词并存储。

在决定在你的 `Zend_Search_Lucene` 索引中使用哪些字段类型时，明确将使用哪些字段作为搜索标准以及计划哪些字段显示在搜索结果中是非常重要的。为了说明这在实践中如何工作，假设你有一组如下格式的 XML 文档：

```xml
<?xml version='1.0'>

<document>

  <id>5468</id>

  <from>Jim Doe <jim@example.com></from>

  <to>Jane Doe <jane@example.com></to>

  <subject>Hello</subject>

  <date>Tuesday, February 27, 2008 10:45 PM</date>

  <body>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed eius eiusmod incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum</body>

</document>
```

## 第 6 章：数据的索引、搜索与格式化

以下是一些示例代码，展示了如何对文档集合进行索引：

```php
<?php

class Sandbox_ExampleController extends Zend_Controller_Action
{
    public function indexAction()
    {
        // 获取索引目录
        $index = Zend_Search_Lucene::create('/tmp/indexes/');

        foreach (glob('*.xml') as $file) {
            // 读取源 xml 文件
            $xml = simplexml_load_file($file);

            // 在索引中创建新文档
            $doc = new Zend_Search_Lucene_Document();

            // 索引并存储字段
            $doc->addField(Zend_Search_Lucene::Field::UnIndexed('id', $xml->id));
            $doc->addField(Zend_Search_Lucene::Field::Text('from', $xml->to));
            $doc->addField(Zend_Search_Lucene::Field::Text('date', strtotime($xml->date)));
            $doc->addField(Zend_Search_Lucene::Field::UnStored('subject', $xml->subject));
            $doc->addField(Zend_Search_Lucene::Field::UnStored('body', $xml->body));

            // 将结果保存到索引
            $index->addDocument($doc);
        }

        // 设置索引中的文档数量
        $count = $index->count();
    }
}
```

索引中的每个文档都表示为一个 `Zend_Search_Lucene_Document` 对象，而每个消息的各个字段则表示为 `Zend_Search_Lucene_Field` 对象。这些字段通过 `Zend_Search_Lucene_Document::addField()` 方法进行索引并添加到文档中，然后通过 `Zend_Search_Lucene::addDocument()` 方法将最终文档添加到索引中。

在索引数据时，定义哪些字段是可搜索的、哪些字段应该在搜索结果显示是一个关键任务。上一个示例显示，接收者（recipient）、日期（date）、主题（subject）和正文（body）字段应该是可搜索的，而只有接收者日期字段应该在搜索结果中显示。将正文和主题字段标记为 `UnStored`（不存储）字段，可以使它们可搜索，同时减少索引消耗的磁盘空间；而将接收者和日期字段标记为 `Text` 字段，则可以对它们进行搜索并在搜索结果中显示。

## 搜索数据

一旦数据完成了索引，下一步就是搜索这些数据。`Zend_Search_Lucene` 自带了一个功能全的查询引擎，可对索引进行简单和复杂的查询。查询可以通过对用户输入应用内置的查询解析器来创建，也可以通过 API 方法以编程的方式生成。对于简单的关键词查询，标准查询解析器就足够；对于包含修饰符、邻近约束、子查询或字段组的更复杂查询，应使用 API 方法来创建。

以下示例代码展示了如何搜索已索引的文档集合并显示结果：

```php
<?php

class SandboxExampleController extends Zend_Controller
{
    public function searchAction()
    {
        // 从 $_GET['query'] 获取查询字符串

        // 如果有效，打开索引并解析查询字符串

        // 执行查询 $data = $input->setData($this->getRequest()->getParams());

        if ($input->isValid()) {
            $index = Zend_Search_Lucene::open('/tmp/indexes/');

            $results = $index->find(
                Zend_Search_Lucene_QueryParser::parse($input->query)
            );

            $this->view = $results;
        }
    }
}
```

如前面的代码所示，第一步是使用 `Zend_Search_Lucene::open()` 方法打开之前创建的索引句。将查询字符串传递给 `Zend_Search_Lucene::find()` 方法，以扫描索引中匹配的文档。结果以 `Zend_Search_Lucene_QueryHit` 对象的形式返回，并按得分排序。这些对象中的每一个都将文档编号和文档得分作为对象属性暴露出来。文档的其他存储字段可以作为对象属性访问，如上一个示例所示。所有字段值都会被自动转换为 UTF-8。

传递给 `find()` 方法的查询字符串可能包含关键词、短语、通配符、范围约束、邻近修饰符以及如 `AND`、`OR` 类的布尔操作符。当用户提交此查询时，最好将其传递给 `Zend_Search_Lucene_Searching_QueryParser::parse()` 方法处理，该方法会自动解析并分词查询字符串，并将其转换为查询对象。这还减少了所需的输入验证量。

### 专家问答

**Q：如何排序或限制 `Zend_Search_Lucene` 的搜索结果？**

**A：**默认情况下，`Zend_Search_Lucene` 返回所有匹配的文档并按得分排序。如果这不符合你的，可以通过向 `find()` 方法添加额外参数来定义排序字段和排序顺序。同样，可以通过 `setLimit()` 方法指定限制来限制返回的匹配项数量。

> **注意**
>
> 由于本书范围有限，无法对 `Zend_Search_Lucene` 支持的查询语言进行全面讨论。不过，可以使用章节末尾的链接查找该主题的详细信息。

## 尝试此 6-2：创建全文搜索引擎

有了这些背景信息，让我们来看看 `Zend_Search_Lucene` 在实际场景中是如何工作的。接下来的部分将在本章之前为 SQUARE 应用创建的基于过滤的搜索引擎，替换为基于 `Zend_Search_Lucene` 的全文搜索系统。

### 定义索引位置

`Zend_Search_Lucene` 的全文搜索索引以磁盘文件的形式存储，首要任务之一就是为它们找到一个位置。因此，在 Zend Framework 下创建一个位置：

```bash
cd /usr/local/apache/htdocs/square
mkdir data
mkdir data/indexes
```

建议更新 `$APP_DIR/application/configs/application.ini` 配置，以便可以使用：

```ini
indexPath = "../data/indexes
```

### 定义自定义路由

在更新应用配置时，建议为 `createFulltextIndexAction()` 添加路由。由于索引创建通常是管理任务，该 action 应该是 `Catalog_AdminController` 的一部分。对应的路由如下：

```ini
resources.router.routes.admin-fulltext-index-create.route = /admin/catalog/fulltext-index-create
resources.router.routes.admin-fulltext-index-create.defaults.module = catalog
resources.router.routes.admin-fulltext-index-create.defaults.controller = admin
```

### 定义索引 Action 和视图

下一步是为存储在数据库中的内容构建全文索引。最简单的方法是执行 Doctrine 查询从数据库中提取记录，然后在循环中将这些记录交给 `Zend_Search_Lucene` 索引器。以下是 `createFulltextIndexAction()` 方法的代码，它负责该任务：

```php
<?php

class Catalog_AdminController extends Zend_Controller
{
    // 创建全文索引的 action
```



```php
public function createFulltextIndexAction()
{
    // 创建并执行查询
    $q = Doctrine_Query::create()
        ->from('Square_Model i')
        ->leftJoin('i.Square_Model_Country c')
        ->leftJoin('i.Square_Model_Grade g')
        ->leftJoin('i.Square_Model_Type t')
        ->where('i.DisplayUntil >= CURDATE()')
        ->addWhere('i.DisplayUntil = 1');

    $result = $q->fetchAllArray();

    // 获取索引目录
    $config = $this->getInvokeArg('bootstrap')->getOption('indexes');
    $index = Zend_Search_Lucene::create($config['indexPath']);

    foreach ($result as $r) {
        // 在索引中创建新文档
        $doc = new Zend_Search_Lucene_Document();

        // ... (其余索引逻辑)
    }
}
```

## 第 6 章：索引、搜索与数据格式化

```php
// index and store fields

$doc->addField(Zend_Search_Lucene_Field::Text('Title', $r['Title']));

$doc->addField(
    Zend_Search_Lucene_Field::Text(
        'Country',
        $r['Square_Model_Country']['CountryName']
    )
);

$doc->addField(
    Zend_Search_Lucene_Field::Text(
        'Grade',
        $r['Square_Model_Grade']['GradeName']
    )
);

$doc->addField(Zend_Search_Lucene_Field::Text('Year', $r['Year']));

$doc->addField(
    Zend_Search_Lucene_Field::Unstored('Description', $r['Description'])
);

$doc->addField(
    Zend_Search_Lucene_Field::Unstored('Denomination', $r['Denomination'])
);

$doc->addField(
    Zend_Search_Lucene_Field::Unstored(
        'Type',
        $r['Square_Model_Type']['TypeName']
    )
);

$doc->addField(
    Zend_Search_Lucene_Field::Unindexed('SalePriceMin', $r['Denomination'])
);

$doc->addField(
    Zend_Search_Lucene_Field::Unindexed('SalePrice', $r['Denomination'])
);

$doc->addField(
    Zend_Search_Lucene_Field::Unindexed('RecordID', $r['RecordID'])
);

// save result to index
$index->addDocument($doc);
}

// set number of documents in index
$count = $index->count();

$this->_helper->getHelper('FlashMessenger')
    ->addMessage(
        "The index was successfully created with $count documents."
    );

$this->->_redirect('/admin/catalog/item/success');
}
```

`createFulltextIndexAction` 首先执行一个 Doctrine 查询以检索所有已批准的目录项目列表。它使用上一步骤中指定的索引位置初始化一个 `Zend_Search_Lucene` 索引（如何使用 `getInvokeArg` 方法获取配置文件的值），然后遍历获取到的记录，将每条记录作为单独的文档喂给索引器。对于每个文档，标题、描述、国家、等级、年份、面值和类型都会被索引；在这些内容中，只有标题、国家、等级和年份会被存储在索引中用于搜索结果，连同记录 ID 和销售价格范围。一旦索引完成，将生成一个成功视图，汇总已索引的文档数量。

## 188 Zend Framework：学者指南

### 更新摘要视图

更新管理摘要页面（路径为 `$APP_DIR/application/modules/catalog/views/scripts/admin-item/index.php`）也是一个好主意，用以显示指向新操作的链接。视图脚本中的更改将以粗体显示。

```html
<h2>列出项目</h2>

<?php if (count($this->records)) : ?>

<div id="records">
  <form method="post" action="<?php echo $this->url(array(), 'admin-catalog-delete'); ?>">
    <table>
      <tr>
        <td colspan="7">
          <input type="submit" name="submit" style="width:150px" value="Delete Selected" />
        </td>
        <td colspan="2">
          <a href="<?php echo $this->url(array(), 'admin-full-text-index-create'); ?>">更新全文本索引</a>
        </td>
      </tr>
    </table>
  </form>
</div>
```

```php
<?php else : ?>

未找到记录

<?php endif; ?>
```

### 更新搜索表单

一旦索引结束，就剩下搜索引擎需要处理了。通过更新搜索表单定义（路径为 `$APP_DIR/library/Form/Search.php`），使其仅包含一个用于搜索关键词的文本输入字段。以下是修改后的定义：

```php
<?php

class Square_Form_Search extends Zend_Form
{
    public function init()
    {
        // 初始化表单
        $this->setAction('/catalog/item/search')
            ->setMethod('get');

        // 为关键词创建文本输入
        $query = new Zend_Form_Element_Text('q');

        $query->setLabel('关键词:')
            ->setOptions(array('size' => '20'))
            ->addFilter('HtmlEntities')
            ->addFilter('StringTrim');

        $query->setDecorators(array(
            array('ViewHelper'),
```

```php
array('Errors'),
array('Label', array('tag') => '<span>'),
);
```

```php
// 创建提交按钮
$submit = new Zend_Form_Element_Submit('submit');

$submit->setLabel('搜索')
    ->setOptions(array('class' => 'submit'))
    ->setDecorators(array(
        array('ViewHelper'),
    ));
```

```php
// 将元素附加到表单
$this->addElement($query)
    ->addElement($submit);
}
```

### 更新搜索 Action 和视图

最后一步是更新 `Catalog_ItemController::searchAction`，使用 `Zend_Search_Lucene` 的全文本索引代替 Doctrine 查询。以下是修改后的代码：

```php
<?php

class Catalog_ItemController extends Zend_Controller
{
    // 执行全文本搜索的操作
    public function searchAction()
    {
        // 生成输入表单
        $form = new Square_Form_Search;
        $this->view->form = $form;

        // 获取匹配搜索的项
        if ($form->isValid($this->getRequest())) {
            $input = $form->getValues();

            if (!empty($input['q'])) {
                $config = $this->getInvoke('bootstrap')->getOption('indexes');
                $index = Zend_Search_Lucene::open($config['indexPathPath']);
                $results = Zend_Search_Lucene_QueryParser::parse($input['q']);
                $this->view->results = $results;
            }
        }
    }
}
```

## 190 Zend Framework：学者指南

`Zend_Search_Lucene::find()` 方法的返回值与 `fetchArray()` 方法不同；值现在是以属性而不是数组的形式暴露的。因此，有必要如下更新对应的视图 `$APP_DIR/modules/catalog/views/scripts/search.php`：

```html
<h2>搜索</h2>

<?php echo $this->form; ?>

<h2>搜索结果</h2>

<p>找到了 <?php echo count($this->results); ?> 条结果。</p>

<?php if (count($this->results)): ?>

<?php $x = 1; ?>

<?php foreach ($this->results as $r): ?>

<div>
    <?php echo $x; ?>

    <a href="<?php echo $this->url(array('id' => $r->RecordID), 'catalog-display'); ?>">
        <?php echo escape($r->Title); ?> (<?php echo escape($r->Year); ?>)
    </a>

    <br/>
    得分: <?php printf('%f', $escape($r->score)); ?><br/>

    <strong>
        等级: <?php echo escape($r->Grade); ?> |
        国家: <?php echo escape($r->Country); ?> |
        销售价格: <?php echo sprintf('%f', $escape($r->SalePriceMin)); ?> 到
        <?php echo sprintf('%f', $escape($r->SalePriceMax)); ?>
    </strong>
</div>

<?php $x++; ?>

<?php endforeach; ?>

<?php endif; ?>
```

```html
<div>
    <a href="<?php echo $this->url(array('module' => 'catalog', 'controller' => 'item', 'action' => 'create')); ?>">添加项目</a>
</div>
```

## 第 6 章：索引、搜索与数据格式化

**图 6-4** 成功创建目录全文本索引的结果

要查看此操作，首先登录 square 管理面板，通过访问 URL `http://square.localhost/admin/catalog/fulltext-index/create` 创建全文本索引。一旦索引创建完成，你应该会看到一个成功页面，如图 6-4 所示。

你现在可以通过网络浏览器访问 `http://square.localhost/catalog/item/search` 来尝试搜索索引。你应该看到一个修改后的搜索表单，如图 6-5。向输入字段输入一个或多个键并提交，如果一切顺利，你应该看到匹配你的关键词的项目列表，如图 6-6 所示。

**图 6-5** 修改后的目录搜索表单

**图 6-6** 匹配表单输入的全文本搜索标准的目录列表

### 提问专家

**Q:** 哪个更好：使用磁盘索引的全文本搜索还是基于数据库查询的搜索？

**A:** 通常情况下，全文本搜索比数据库搜索产生更好的结果，原因有几个。允许用户通过数据库记录的每一个维度进行搜索通常是不实际的；此外，大多数 RDBMS 内置的全搜索功能不如 Lucene、Sphinx 或 Sol 等更专注于全文本搜索的工具复杂或高效。它通常比数据库搜索更快，因为搜索是使用磁盘索引而不是数据库连接进行的。尽管如此，全文本搜索依赖于从源内容创建的静态索引，因此在源内容频繁更新的情况下，全文本搜索结果可能会后于实际可用内容。数据库搜索因为直接在内容上运行，会受到这种延迟的影响。与其他问题一样，这个问题的答案是主观的，取决于你希望在性能和准确性之间实现的精确平衡。

### 处理多种输出类型

现代 Web 应用不仅支持 HTML——它们通常还能提供 RSS、JSON、XML 以及其他多种格式。由于 MVC 模式区分了数据和表示，它非常适合这类工作：支持新的输出类型变得只需创建一个包含适当格式化代码和/或标记的新视图。最重要的是，这些更改局限于视图层，可以在不对控制器和模型层进行任何修改的情况下完成。框架内置了一个处理多种输出类型（上下文）的处理器，称为 `ContextSwitch` 助手。该助手处理所有涉及切换到不同输出格式的任务、禁用默认布局、选择合适的视图脚本以及为所选格式发送正确的头部。为了说明其工作原理，请考虑以下示例，它为 YAML 输出设置了一个新上下文：

```php
<?php

class Sandbox_ExampleController extends Zend_Controller_Action
{
    public function init()
    {
        // 初始化上下文切换助手
        $contextSwitch = $this->_helper->getHelper('contextSwitch');

        $contextSwitch->addContext(
            'yaml',
            array(
```

# 第 6 章：索引、搜索与数据格式化 193

```php
'suffix' => 'yaml',
'headers' => array('Content-Type' => 'text/yaml')
);

$contextSwitch->addActionContext('list', 'yaml')
    ->initContext();
}
```




在使用 `ContextSwitch` 助手类支持新的输出类型时，需要遵循以下四个基本步骤：

1. **定义上下文参数。** `ContextSwitch` 助手类带有一个 `addContext()` 方法，可用于定义新的上下文。该 `addContext()` 方法接受两个参数：一个包含新输出类型名称的字符串，以及一个包含额外配置信息的数组（例如发送给请求客户端的头部以及在视图脚本中查找的文件后缀名）。在上述示例中，`addContext()` 方法指定了 `.yaml` 视图后缀和 `text/yaml` 的 `Content-Type` 头部。

   > 注意：当处理预定义的 XML 和 JSON 上下文时，可以跳过此步骤。

2. **将上下文与一个或多个操作关联。** 一旦定义了输出类型，就可以使用 `ContextSwitch` 助手类的 `addActionContext()` 方法将其映射到一个或多个操作。在上述示例中，`addActionContext()` 方法指定了 `listAction()` 也可以以 YAML 格式返回。

   > 提示：如果你有许多不同的上下文和操作需要处理，请考虑使用 `addActionContexts()` 方法。它接受一个上下文-操作对的数组，作为在单个方法调用中处理多个上下文和操作的便捷方式。

3. **为上下文创建视图脚本。** 下一步是为每个操作和上下文创建一个视图脚本。默认情况下，此视图脚本以 `addContext()` 方法中指定的后缀命名，并包含生成指定格式的输出所需的所有格式化代码、标记和业务逻辑。为了说明，在上述示例中，视图脚本 `list.yaml.shtml` 将负责生成 `listAction()` 方法输出的 YAML 视图。同样，如果所需的输出类型是 XLS，则视图脚本将命名为 `list.xls.shtml`，它将包含生成 Microsoft Excel 格式电子表格所需的 PHP 代码。

# Zend 框架：入门指南

4. **初始化上下文。** 这是最后一步，也是简单的一步，即调用 `ContextSwitch` 助手类的 `initContext()` 方法。当在不带任何参数的情况下调用时，该方法会初始化所有定义的上下文并开始运行。你可以将特殊的 `?format=context-name` 参数附加到操作的 URL 上，以便为 `ContextSwitch` 提供所需的输出类型——例如用于 YAML 输出的 `?format=yaml` 或用于 XLS 输出的 `?format=xls`。

# 尝试此：6-3 用 XML 表示搜索结果

为了说明 `ContextSwitch` 助手在实践中如何工作，让我们增强本章之前创建的搜索引擎，以支持 XML 输出。以下章节将引导你完成这一过程。

# 启用 XML 上下文

由于 `ContextSwitch` 助手内置了 XML 和 JSON 上下文的定义，因此没有必要使用 `addContext()` 方法定义它们。相反，我们可以直接使用 `addActionContext()` 方法将 XML 上下文映射到 `searchAction()` 方法。将此方法添加到 `Catalog_ItemController` 类的 `init()` 方法中，如下：

```php
<?php

class Catalog_ItemController extends Zend_Controller_Action
{
    public function init()
    {
        // 初始化 $contextSwitch 助手
        $contextSwitch = $this->getHelper('contextSwitch');

        $contextSwitch->addActionContext('search', 'xml')
            ->initContext();
    }
}
```

# 定义 XML 视图

一旦 XML 上下文已映射并初始化，任何对 XML 格式搜索结果的请求将由相应的 XML 视图脚本处理。按照惯例，此视图应保存为 `APP_DIR/application/modules/catalog/views/scripts/item/search.xmlhtml`。以下是它应该的内容：

```php
<?php

// 创建 XML 文档
$dom = new DOMDocument('1.0', 'utf-8');
```

```php
// 创建根元素
$root = $dom->createElementNS(
    'http://square.localhost',
    'square:document'
);
$dom->appendChild($root);

// 转换为 SimpleXML
$xml = simplexml_import_dom($dom);

// 添加摘要元素
$xml->addChild('matches', count($this->results));
$xml->addChild('searchTime', time());

// 添加结果元素
$results = $xml->addChild('results');

foreach ($this->results as $r) {
    $result = $results->addChild('result');

    $result->addChild('id', $this->escape($r->RecordID));
    $result->addChild('title', $this->escape($r->Title));
    $result->addChild('year', $this->escape($r->Year));
    $result->addChild('grade', $this->escape($r->Grade));
    $result->addChild('country', $this->escape($r->Country));

    $price = $result->addChild('price');
    $price->addChild('min', $this->escape($r->SaleMin));
    $price->addChild('max', $this->escape($r->SaleMax));
}

// 返回输出
echo $xml->asXML();
?>
```

如果你熟悉 PHP 的 SimpleXML 和 DOM 扩展，前面的脚本应该相当简单。它首先使用 PHP 的 DOM 生成新文档。处理结果集后，使用 `ContextSwitch` 助手输出 XML。要查看效果，在 `http://localhost/item/search` 进行搜索并输入一组关键词，将获得搜索结果。通过在 URL 字符串附加 `?format=xml`，`ContextSwitch` 助手将切换输出类型并向你展示 XML 结果。

196 Zend 框架：入门指南

> 提示：传递给 `ContextSwitch` 的 `format` 参数只需要指定。它可以来自任何参数来源。

### 总结

一旦你的应用程序的基础 CRUD 函数运行，用户和管理员就可以自由地添加数据。本章专注于此，引导你向应用程序添加搜索功能，并展示了如何使用 `Zend_Search_Lucene` 组件。它还演示了 `ContextSwitch` 助手，它可以轻松支持 XML、JSON 等格式。

# 索引、搜索与格式化

要了解更多关于本章讨论的主题，请访问以下链接：

- [Zend_Search_Lucene 组件](https://framework.zend.com/manual/en/zend/search.html)
- [Zend_Search_Lucene 查询语言](https://framework.zend.com/manual/en/zend.search.lucene.query-language)
- [ContextSwitch 助手](https://framework.zend.com/manual/en/zend.controller.actionhelpers.html)
- [PHP SimpleXML 扩展](https://www.php.net/simplexml)
- [PHP DOM 扩展](https://www.php.net/dom)
- [使用 ContextSwitch 助手导出 Excel 电子表格的讨论](https://www.pablovquez.com/2009/08/export-excel-spreadsheets-using-zend-framework/)
- [使用 ContextSwitch 动态布局的讨论](https://morecowbell.net.au/2009/02/changing-layouts-with-zend-contextswitch/)
- [使用 ContextSwitch 助手创建 REST API 的讨论](https://www.chrisdanielson.com/2009/02/creating-a-php-rest-api-using-the-zend-framework/)
- [用 Zend_Search_Lucene 和 Sphinx 索引邮件的比较](https://devzone.zend.com/article/4887-Indexing-Email-Messages-with-PHP-Zend-Lucene-and-Sphinx)

## 第 7 章：分页、排序与数据上传

# Zend Framework：入门指南

### 核心技能与概念

- 对数据库结果集进行分页和排序
- 通过 Web 表单对文件上传进行过滤、验证和处理
- 读写 INI 和 XML 格式的配置文件

当你正在构建一个软件应用程序时，最重要的任务之一就是识别应用程序行为的哪些方面应该是允许由用户进行配置的。例如，如果你正在构建一个内容管理系统，你可能希望允许应用程序管理员有足够的灵活性来决定日期和时间的显示方式、是否允许为文章添加图片，以及评论是否需要经过审核员的批准。然而，你可能不希望管理员处理数据存储的文件格式或异常的处理方式，因为这些是应用程序的内部逻辑，且（通常）不适用于用户级配置。

识别应用程序的哪些方面应该是用户可配置的，并没有听起来那么容易。为了正确执行分析，开发者需要对软件目标以及其旨在解决的终端需求有深入的理解。然而，一旦分析完成，事情就会变得简单得多。识别出的变量可以移动到单独存储区域（通常是一个或多个配置文件），现在轮由开发人员提供一个接口，让应用程序管理员可以在运行时操作这些变量了。

Zend Framework 包含一个 `ZendConfig` 组件，它提供了一个功能完备的 API，用于读写各种格式的配置文件。本章将详细检查该组件，讨论如何在 SQUARE 示例应用程序的背景下使用它来管理配置数据。它还回顾了之前章节中的两个组件 `ZendForm` 和 Doctrine，并说明了如何使用它们来满足两个常见需求：启用文件上传以及结果集的分页和排序。

### 尝试一下 7-1：分页与排序数据库记录

在 Web 应用程序中处理大数据集时，简单地将所有可用数据倾倒到一个页面中并让用户自己排序通常被认为是一件坏事（Bad Thing）。分页涉及将大型数据集拆分成较小的块（或页面），这是在这种情况下提高可读性和导航的常用界面模式。分页很重要，因为它允许用户控制在任何给定时刻显示哪部分数据，从而避免淹没在无尽的数据海洋中。当与数据库服务器配合使用时，分页还通过产生较小的结果集来减轻服务器负载。

分页的有趣之处在于，实现这种模式的程序代码是非常标准的，不太可能在不同项目之间发生变化。这使其成为实现为复用组件的理想选择，事实上，大多数框架和数据库抽象层都带有一个现成的分页组件。例如，Zend Framework 包含一个 `Zend_Pager` 组件，它带有针对不同数据源的适配器（包括一个针对 `Zend_DB` 的适配器）。同样，Doctrine 也带有 `Doctrine_Pager` 组件，它可以直接处理并对查询进行分页。

在将单个数据集划分为更小的子集，以及通过生成导航链接在不同子集之间来回移动，并没有太多的选择。然而，由于分页最与数据库结果集相关联，通常使用数据库抽象层推荐或包含的分页器组件是有意义的。由于本书建议对所有的数据库访问操作都使用 Doctrine，接下来的讨论将集中在 `Doctrine_Pager` 和 `Doctrine_Query` 组件，说明如何在 SQUARE 示例应用程序的背景下使用它们对结果集进行分页和排序。

### 在路由中添加页码

分页组件的典型操作非常简单。组件首先配置每页显示的项目数量。然后，它通过将数据集中的项目数除以每页请求的项目数来计算总页数，然后动态生成一组用于在页面之间移动的导航链接。每个链接都包含一个额外的 GET 参数（页码），分页控制器可以使用该参数来确定请求的是哪部分数据集。

为了说明这是如何工作的，请打开 `\$APP_DIR/application/config/application.ini` 中的应用程序配置文件，并如下所示为管理摘要页的路由添加额外的参数：

```ini
resources.router.routes.admin-catalog-index.route = /admin/catalog/item/index/:page
resources.router.routes.admin-catalog-index.defaults.module = catalog
resources.router.routes.admin-catalog-index.defaults.controller = admin.item
resources.router.routes.admin-catalog-index.defaults.action = index
resources.router.routes.admin-catalog-index.defaults.page = 1
```

### 更新索引控制器和视图

下一步是更新 `Catalog_AdminItemController::indexAction`，以便在构建 SELECT 查询时使用此参数。这就是 `Doctrine_Pager` 组件派上用场。以下是更新后的 action 内容：

```php
class Catalog_AdminItemController extends Zend_Controller_Action
{
    // 显示目录项目列表的 action
    public function indexAction()
    {
        // 为 GET 输入设置过滤器和验证器
        $filters = array(
            'page' => array('HtmlEntities', 'StripTags', 'StringTrim')
        );

        $validators = array(
            'page' => array()
        );

        // 测试输入是否有效
        $input = $this->getRequest()->fromGet(
            'page',
            1,
            $filters,
            $validators
        );

        if ($input->isValid()) {
            $page = (int) $input->getValue();
        } else {
            $page = 1;
        }

        $query = $this->model->getQuery();
        $pager = new Doctrine_Pager($query, $page, 4);
        $result = $pager->getResult();

        $pagerLayout = new Doctrine_Pager_Layout($pager);
        $pagerLayout->setTemplate('<a href="{url}">{%page}</a>');
        $pagerLayout->setSelectedTemplate(
            '<span class="current">{%page}</span>'
        );
        $pagerLayout->setSeparator('&nbsp;');

        $this->view->records = $result;
        $this->view->pages = $pagerLayout->display();
    }
}
```

# 为路由中添加排序标准

分页是切分处理数据集的一种方法，但也有其他方法。另一种极其常见的需求是允许用户根据其中一个字段对数据集进行排序。在这里，URL 请求中也会附加指示字段和排序方向的额外参数，页面控制器将被配置为在将数据交给视图显示之前，根据这些参数对数据进行排序。

要查看此功能，请返回 `\$APP_DIR/application/configs/application.ini` 的应用程序配置文件，并按照下面的示例，使用两个额外的参数进一步修订路由定义：

```ini
resources.router.routes.admin-catalog-index.route = /admin/catalog/index/:page/:sort=:dir
resources.router.routes.admin-catalog-index.defaults.module = catalog
resources.router.routes.admin-catalog-index.defaults.controller = admin.item
resources.router.routes.admin-catalog-index.defaults.action = index
```




`resources.router.routes.admin-catalog-index.defaults.page = 1`

`resources.router.routes.admin-catalog-index.defaults.sort = RecordID`

`resources.router.routes.admin-catalog-index.defaults.dir = asc`

### 更新控制器和视图

这些参数应该整合到 `Catalog\AdminItemController::indexAction` 生成的 Doctrine 查询中。可以使用 `InArray` 验证器来确保只有有效参数会被传回 action 的主体。修订后的 action 代码如下示例所示：

```php
<?php

class Catalog_AdminItemController extends Zend_Controller_Action
```

```php
// 显示目录项列表的 action
public function indexAction()
{
    // 为 GET 输入设置过滤器和验证器
    $filters = array(
        'sort' => array('HtmlEntities', 'StripTags', 'StringTrim'),
        'dir' => array('HtmlEntities', 'StripTags', 'StringTrim'),
        'page' => array('HtmlEntities', 'StripTags', 'StringTrim')
    );

    $validators = array(
        'sort' => array(
            'Alpha',
            array('InArray', 'haystack' =>
                array('RecordID', 'Title', 'Denomination',
                    'CountryID', 'GradeID', 'Year'))
        ),
        'dir' => array(
            'Alpha',
            array('InArray', 'haystack' =>
                array('asc', 'desc'))
        ),
        'page' => array('Int')
    );
    $input = new Filter_Input($filters, $validators);
    $input->setData($this->getRequest()->getParams());

    // 测试输入是否有效
    // 创建查询并设置分页参数
    if ($input->isValid()) {
        $q = Doctrine_Query::create()
            ->from('Square_Model_Item i')
            ->leftJoin('i.Square_Model_Grade g')
            ->leftJoin('i.Square_Model_Country c')
            ->leftJoin('i.Square_Model_Type t')
            ->orderBy(sprintf('%s %s', $input->sort, $input->dir));

        $perPage = 4;
        $numPageLinks = 5;

        // 初始化分页器
        $pager = new Doctrine_Pager($q, $input->page, $perPage);

        // 执行分页查询
        $result = $pager->execute(array(), Doctrine::HYDRATE_ARRAY);
    }

    // 初始化分页布局
    $pagerRange = new Doctrine_Pager_Range_Sliding(array('chunk' => $numPageLinks), $pager);
    $pagerBase = $this->view->url(array(), 'admin-catalog-index', 1) . "/{%page}/{$input->sort}/{$input->dir}";
    $pagerLayout = new Doctrine_Pager_Layout($pager, $pagerRange, $pagerBase);

    // 设置分页链接模板
    $pagerLayout->setTemplate('<a href="{%url}">{%page}</a>');
    $pagerLayout->setSelectedTemplate('<span class="current">{%page}</span>');
    $pagerLayout->setSeparatorTemplate('&nbsp;&nbsp;');

    // 设置视图变量
    $this->view->records = $result;
    $this->view->pages = $pagerLayout->display(null, true);
} else {
    throw new ZendController_ActionException('Invalid input');
}
```

包含必要的排序参数，以便在切换页面时排序标准不会“丢失”。

最后一步是更新视图并包含供用户对数据集排序的链接。以下是修订后的视图：

```php
<h2>Items</h2>

<?php if (count($this->records)): ?>

<div id="pager">
    Pages: <?php echo $this->pages; ?>
</div>

<div id="records">
    <form method="post" action="<?php echo $this->url(array(), 'admin-catalog-index'); ?>">
        <table>
            <tr>
                <td class="key">
                    Item ID
                    <a href="<?php echo $this->url(array('sort' => 'RecordID', 'dir' => 'asc'), 'admin-catalog-index'); ?>">asc</a>
                    <a href="<?php echo $this->url(array('sort' => 'RecordID', 'dir' => 'desc'), 'admin-catalog-index'); ?>">desc</a>
                </td>
            </tr>
            <tr>
                <td class="key">
                    Title
                    <a href="<?php echo $this->url(array('sort' => 'Title', 'dir' => 'asc'), 'admin-catalog-index'); ?>">asc</a>
                    <a href="<?php echo $this->url(array('sort' => 'Title', 'dir' => 'desc'), 'admin-catalog-index'); ?>">desc</a>
                </td>
            </tr>
            <tr>
                <td class="key">
                    Denomination
                    <a href="<?php echo $this->url(array('sort' => 'Denomination', 'dir' => 'asc'), 'admin-catalog-index'); ?>">asc</a>
                    <a href="<?php echo $this->url(array('sort' => 'Denomination', 'dir' => 'desc'), 'admin-catalog-index'); ?>">desc</a>
                </td>
            </tr>
            <tr>
                <td class="key">
                    Country
                    <a href="<?php echo $this->url(array('sort' => 'CountryID', 'dir' => 'asc'), 'admin-catalog-index'); ?>">asc</a>
                    <a href="<?php echo $this->url(array('sort' => 'CountryID', 'dir' => 'desc'), 'admin-catalog-index'); ?>">desc</a>
                </td>
            </tr>
            <tr>
                <td class="key">
                    Grade
                    <a href="<?php echo $this->url(array('sort' => 'Grade', 'dir' => 'asc'), 'admin-catalog-index'); ?>">asc</a>
                    <a href="<?php echo $this->url(array('sort' => 'Grade', 'dir' => 'desc'), 'admin-catalog-index'); ?>">desc</a>
                </td>
            </tr>
            <tr>
                <td class="key">
                    Year
                    <a href="<?php echo $this->url(array('sort' => 'Year', 'dir' => 'asc'), 'admin-catalog-index'); ?>">asc</a>
                    <a href="<?php echo $this->url(array('sort' => 'Year', 'dir' => 'desc'), 'admin-catalog-index'); ?>">desc</a>
                </td>
            </tr>
            <tr>
                <td><td></td>
            </tr>

            <?php foreach ($this->records as $r) : ?>
                <td><?php echo $this->escape($r['RecordID']); ?></td>
                <td><?php echo $this->escape($r['Title']); ?></td>
                ...
            <?php endforeach; ?>
```

```php
<?php endforeach; ?>

<tr>
    <td colspan="7">
        <input type="submit" name="submit" style="width:150px" value="Delete Selected" />
    </td>
    <td colspan="2">
        <a href="<?php echo $this->url(array('admin-fulltext-index-create')); ?>">Update full-text indices/</a>
    </td>
</tr>

</table>
</form>
</div>
```

```php
<div id="pager">
    Pages: <?php echo $this->pages; ?>
</div>

<?php else: ?>

No records found

<?php endif; ?>
```

现在，当你再次访问 URL `http://square.localhost/admin/catalog/item/index` 时，你会发现你可以根据各种字段对数据集进行排序，方向可以是升序或降序。即使在数据集的页面之间移动，这种排序选择也会被保留。如果没有说明排序标准，路由默认值将确保数据集按项目 ID 升序自动排序。

图 7-2 显示了按等级排序的输出示例（查看浏览器中的 URL 以更好地了解其工作原理）。

**图 7-2** 启用排序和分页的目录摘要

# 处理文件上传

在第 3 章中，你学习了如何使用 `Zend_Form` 创建和处理表单，后续章节通过将这些技术应用于不同类型的表单深化了你对 `Zend_Form` 的理解。然而，目前尚未涵盖的需求是处理文件上传。

PHP 多年来一直支持文件上传表单，并提供了特殊的 `$_FILES` 全局变量以及许多内置方法，如 `uploaded_file()` 和 `move_uploaded_file()`，以协助安全高效地管理文件上传。在 Zend Framework 中，类似的功能可以通过 `Zend_File_Transfer` 组件实现，它提供了一套完整的接收、验证和处理上传文件的 API。该组件还可以无缝处理通过 `Zend_Form` 元素引发的文件传输。

### 注意

虽然 PHP 原生支持 POST 和文件上传，`Zend_File_Transfer` 组件目前支持 POST 上传。

理解文件传输在 `Zend_Form` 下如何工作的最佳方法是使用示例。考虑以下代码，它设置了一个包含文件上传元素和提交按钮的简单表单：

```php
<?php

class Form_Example extends Zend_Form
{
    public function init()
    {
        // 初始化表单
        $this->setAction('/sandbox/example/form')
            ->setMethod('post');

        // 创建用于照片的文件输入
        $photo = new Zend_Form_Element_File('photo');

        $photo->setLabel('Photo:')
            ->setDestination('/tmp/upload/');

        // 创建提交按钮
        $submit = new Zend_Form_Element_Submit('submit');
        $submit->setLabel('Submit');

        // 将元素附加到表单
        $this->addElement($photo)
            ->addElement($submit);

        return $this;
    }
}
```

为了说明这些过滤器和验证器的实际用法，请考虑之前显示的表单定义的修订版本。该版本结合了过滤器和验证器，将上传限制为 40KB 以下的 JPEG，并将其重命名为唯一文件名。

| 验证器名称 | 描述 |
|---|---|
| `Exists` |  |
| `Count` | 如果上传的文件数量不在参数指定的范围内，则返回 `false` |
| `Size` | 如果上传的文件的大小不在参数指定的范围内，则返回 `false` |
| `FileSize` | 如果上传的文件总大小不在参数指定的范围内，则返回 `false` |
| `Extension` | 如果上传的文件扩展名与参数中指定的不符，则返回 `false` |
| `MimeType` | 如果上传的文件的 MIME 类型与参数中指定的不符，则返回 `false` |
| `IsCompressed` | 如果上传的文件不是压缩包文件，则返回 `false` |
| `IsImage` | 如果上传的文件不是图像文件，则返回 `false` |
| `ImageSize` | 如果上传文件的尺寸不在参数指定的范围内，则返回 `false` |
| `Crc32`、`Md5`、`Sha1`、`Hash` | 如果上传的文件内容与参数中指定的哈希值不匹配，则返回 `false`（支持 `crc32`、`md5` 和 `sha1` 哈希算法） |
| `ExcludeExtension` | 如果上传文件的扩展名匹配参数中指定的扩展名，则返回 `false` |
| `ExcludeMimeType` | 如果上传文件的 MIME 类型匹配参数中指定的类型，则返回 `false` |
| `WordCount` | 如果上传文件的单词数不在参数指定的范围内，则返回 `false` |

**表 7-1** Zend Framework 包含的文件上传验证器

| 过滤器名称 | 描述 |
|---|---|
| `Encrypt` | 加密上传文件的内容 |
| `Decrypt` | 解密上传文件的内容 |
| `LowerCase` | 将上传文件的内容转换为小写 |
| `UpperCase` | 将上传文件的内容转换为大写 |
| `Rename` | 重命名上传的文件 |

**表 7-2** Zend Framework 包含的文件上传过滤器

```php
<?php

class FormExample extends Zend_Form
{
    public function init()
    {
        // initialize form
        $this->setToAction('/sandbox/example/form')
            ->setMethod('post');

        // create file input for photo upload
        $photo = new Zend_Form_Element_File('photo');

        $photo->setLabel('Photo:')
            ->setDestination('/tmp/upload')
            ->addFilter(
                'Rename',
                sprintf('p-%s.jpg', uniqid(md5(time()), true))
            )
            ->addValidator('Extension', false, 'jpg')
            ->addValidator('MimeType', false, 'image/jpeg')
            ->addValidator('Size', false, 40000);
```



```php
// create submit button

$submit = new Zend_Form_Element_Submit('submit');

$submit->setLabel('Submit');

// attach elements to form

$this->addElement($photo)
    ->addElement($submit);

return $this;

}
}
```

图 7-4 显示了尝试上传不符合指定约束的文件时看到的输出示例。

**图 7-4 上传无效文件的结果**

## 尝试 7-2 启用图像上传

在有了这些背景信息后，让我们考虑更新 SQUARE 示例，允许卖家为其目录条目添加最多三张照片。后续章节将讨论如何启用此功能。

### 定义上传目标

第一步是为上传的图像定义规则。由于这些图像最终将显示在公共目录中，因此必须被未验证的 URL 请求访问，因此将它们存储在 `$APP_DIR/public/` 目录层次下是合理的。因此，按照如下方式创建 `$APP_DIR/public/uploads/`：

```shell
cd /usr/apache/htdocs/square/public
mkdir uploads
```

由于不同的控制器和操作都需要此信息，因此将其集中管理在应用程序配置文件中也是合理的。打开应用程序配置文件，路径为 `$APP_DIR/application/configs/application.ini`，并向其中添加以下指令：

```ini
uploads.uploadPath = APPLICATION_PATH ../public/uploads
```

### 更新表单定义

下一步是更新创建新目录条目的表单，添加额外的文件元素。要做到这一点，请更新位于 `$APP_DIR/library/Square/FormItemCreate.php` 的表单定义，并注意**加粗**标记的更改：

```php
<?php

class Square_Form_ItemCreate extends Zend_Form
{
    public function init()
    {
        // initialize form

        $this->setAction('/catalog/item/create')
            ->setMethod('post');

        // element definitions abbreviated due to space constraints /

        // refer to Chapter 4 or the code archive //

        // for the complete form definition //

        // create file input for item images

        $images = new Zend_Form_Element_File('images');

        $images->setMultiFile(3)
            ->addValidator('IsImage')
            ->addValidator('Size', false, '204800')
            ->addValidator('Extension', false, 'jpg,png,gif')
            ->addValidator('ImageSize', false, array(
                'width' => 204800,
                'height' => 204800
            ))
            ->setDisabled(true);

        // attach element to form

        $this->addElement($images);

        // create display group for files

        $this->setDisplayGroup(array('images'), 'files');

        // attach element to form

        $this->addElement($submit);
    }
}
```

### 专家问答

**问：为什么要调用 `Zend_Form_Element_File` 的 `setValueDisabled()` 方法？**

**答：这防止了在调用 `getValues()` 方法时自动接收文件。然而，真正的问题是，为什么不应该自动接收文件呢？Thomas Wiedner 是一位知名的 Framework 开发者，他建议为每个文件动态设置 `Rename` 过滤器，然后使用 `Zend_File_Transfer` 适配器手动接收。因此，调用 `setValueDisabled()` 是为这种手动接收和重命名的过程留出了空间。**

## 上传文件

`Zend_Form_Element::getTransferAdapter()` 方法返回一个 `Zend_File_Transfer` HTTP 适配器的实例。该适配器作为接收、验证和处理多个上传文件的控制点。它暴露了一个 `receive()` 方法，可用于手动接收多文件中的各个元素。使用 `Rename` 可以确保这些文件使用特定的命名规范进行自动重命名，该规范在文件名中包含了条目的记录 ID 和文件序列 ID。重命名后的文件将保存到 `Zend_Form_Element::getDestination()` 方法指定的磁盘目录中。

```php
$this->_helper->getHelper('FlashMessenger')->addMessage(
    'Your submission has been accepted as item # ' . $id
    . '. A moderator will review it and, if approved, it will appear on the site within 48 hours.'
);

$this->_redirect('/catalog/item/success');
```

### 注意事项

当你使用原始文件名上传文件时，请记住在通过 `receive()` 方法接收文件之前对文件名进行验证。这样做是为了消除文件通过如 `../etc/passwd` 或 `../index.php` 等文件名注入服务器文件系统的可能性，这在配置不当的服务器上显然会导致严重问题。

## 更新显示 Action 和视图

大部分繁重工作已经完成。下一步是更新 `Catalog_ItemController::displayAction`，以显示上传的图片以及条目的其他详细信息。以下是修订后的 `displayAction()` 方法代码。

```php
<?php

class Catalog_ItemController extends Zend_Controller_Action
{
    // 显示目录项

    public function displayAction()
    {
        // 为 GET 输入设置过滤器和验证器

        $filters = array(
            'id' => array('HtmlEntities', 'StripTags', 'StringTrim')
        );

        $validators = array(
            'id' => array('NotEmpty', 'Int')
        );
```

## 第 7 章：分页、排序和数据上传

```php
$input = new Zend_Filter_Input($filters, $validators);

$input->setData($this->getRequest()->getParams());

// 测试输入是否有效

// 获取请求的记录

// 挂到视图

if ($input->isValid()) {
    $q = Doctrine_Query::create()
        ->from('Square_Model_Item i')
        ->leftJoin('i', 'Square_Model_Country c')
        ->leftJoin('i', 'Square_Model_Grade g')
        ->leftJoin('i', 'Square_Model_Type t')
        ->where('i.RecordID = ?', $input->id)
        ->where('i.DisplayStatus = 1')
        ->where('i.DisplayUntil >= CURDATE()');

    $result = $q->fetchArray();

    if (count($result) == 1) {
        $this->view->item = $result[0];

        $this->view->images = array();

        $config = $this->getInvokeArg('bootstrap')
            ->getOption('uploads');

        foreach (glob($config['UploadPath']/*") as $file) {
            $this->view->images[$file] = basename($file);
        }
    } else {
        throw new Zend_Controller_Action_Exception('Page not found');
    }
} else {
    throw new Zend_Controller_Action_Exception('Invalid input');
}
```

额外的代码从应用程序配置文件读取上传目录的路径，使用 PHP 的 `glob` 函数获取该目录下与项目 ID 对应的所有文件列表，然后将结果列表作为数组发送给视图。视图脚本现在处理此数组并在画廊中显示图片，如下：

### 查看项目

```php
待售物品:

<?php echo $this->escape($this->item['Title']); ?>

<?php echo $this->escape($this->item['Year']); ?>

<?php echo $this->escape($this->item['Square_Model_Grade']['GradeName']); ?>
```

```html
<div id="container">
  <div id="images">
    <?php foreach ($this->images as $image): ?>
    <img src="uploads/<?php echo $this->escape($image); ?>" width="150" height="150" />
    <?php endforeach; ?>
  </div>
  <div id="record">
    <<table>
      <tr>
        <td class="key">标题:</td>
        <td class="value">
          <?php echo $this->escape($this->item['Title']); ?>
        </td>
      </tr>
      <tr>
        <td class="key">描述:</td>
        <td class="value">
          <?php echo $this->escape($this->item['Description']); ?>
        </td>
      </tr>
    </table>
  </div>
</div>
```

以类似的方式，你应该更新 `Catalog_AdminItemController::displayAction` 和相应的视图脚本，以显示与每个项目相关的图片。你可以在本章的代码存档中找到必要的代码，这些代码可以从本书的配套网站 http://www.zf-beginners.com 下载。

## 更新删除 Action

最后，你还应该更新 `Catalog_AdminItemController::deleteAction`，以便在删除每个项目时移除与之相关的图片。这并不困难，如下所示：

（注：后续代码部分原文不完整，未翻译）

# 第 7 章：分页、排序与数据上传 223

```php
// 将 view->b 设置为 'white'
$this->view->b = $config->object->typeface->color;
```

### 注意事项

默认情况下，在 `Zend_Config` 对象中表示的配置数据是只读的，任何修改它的尝试都将产生异常。要允许修改，请将额外的 `options` 数组作为第三参数传递给 `Zend_Config` 对象，并将 `'allowModifications'` 键指定为 `true`。关于此点的更多信息可以参考本章末尾的链接。

还有一个名为 `Zend_Config_Xml` 的适配器，专门用于处理 XML 编码的配置。

```xml
<?xml version="1.0"?>
<configuration>
  <application>
    <name>SomeApp</name>
    <version>2.3</version>
    <window>
      <height>600</height>
      <width>500</width>
      <titlebar>
        <title>Export Data</title>
        <foregroundColor>#ffffff</foregroundColor>
        <backColor>#0000ff</backColor>
      </titlebar>
    </window>
  </application>
</configuration>
```

这里是一个使用 `Zend_Config_Xml` 适配器读取此文件并从内部访问配置值的示例：

```php
<?php

class Sandbox_ExampleController extends Zend_Controller_Action
{
    public function configAction()
    {
        // 初始化配置对象

        $config = new Zend_Config_Xml(
            APPLICATION_PATH . "/configs/example.xml"
        );
    }

    // 将 view->a 设置为 '2.3'

    $this->view->a = $config->application->version;
```

# 224 Zend Framework：入门指南

```php
// 将 $view->b 设置为 'Export Data'

$this->view->b = $config->application->window->titlebar->title;
}
```

### 写入配置文件

这解决了读取文件问题，但如何写入文件呢？`Zend_Config` 包含一个写入组件 `Zend_Config_Writer`，它可以用于创建 PHP、XML 或 INI 格式的配置文件。配置数据可以分层次或分节排列，以获得更高的可读性。

以下是一个说明如何使用 `Zend_Config_Writer` 生成 INI 格式的配置文件的示例：



```php
<?php
class SandboxExampleController extends Zend_Controller_Action {
    public function configAction() {
        // 创建配置对象
        $config = new Zend_Config(array(), 1);

        // 创建节
        $config->blog = array();
        $config->blog->allowComments = 'yes';
        $config->blog->displayComments = 'yes';
        $config->blog->allowTrackbacks = 'yes';
        $config->blog->defaultAuthor = 'Jack Frost';
        $config->blog->numPostsOnIndexPage = 5;

        // 创建节
        $config->calendar = array();
        $config->calendar->weekStartOn = 'Monday';
        $config->calendar->highlightToday = 1;

        // 创建子节
        $config->calendar->events = array();
        $config->calendar->events->displayTitle = 1;
        $config->calendar->events->displayStartTime = 1;
        $config->calendar->events->displayEndTime = 0;
        $config->calendar->events->displayLocation = 1;

        // 将数据写入文件
        $writer = new Zend_Config_Writer_Ini();
        $writer->write(APPLICATION_PATH . "/configs/example.ini", $config);
    }
}
```

# 第 7 章：分页、排序与数据上传

第一步是初始化一个 `Zend_Config` 对象，它代表配置数据。该对象的初始化应该使用包含配置数据的数组（如果没有数据存在，则使用空数组）以及一个指示配置数据是否可以被修改的布尔参数。`Zend_Config` 对象初始化后，可以使用标准的对象表示法将单个配置变量设置为属性。它支持分层数据结构，只需通过链式调用属性即可；取决于所选择的输出格式，这种层次结构通过分隔符（INI）或嵌套（XML）表示。

由上述代码生成的配置文件如下：

```ini
[blog]
allowComments = "yes"
displayComments = "yes"
allowTrackbacks = "yes"
defaultAuthor = "Jack Frost"
numPostsOnPageIndex = 5
```

```ini
[calendar]
weekStartsOn = "Monday"
highlightToday = 1
events.displayTitle = 1
```

```php
第一步是初始化一个 `Zend_Config` 对象，它代表配置数据。该对象的初始化应该使用包含配置数据的数组（如果没有数据存在，则使用空数组）以及一个指示配置数据是否可以被修改的布尔参数。`Zend_Config` 对象初始化后，可以使用标准的对象表示法将单个配置变量设置为属性。它支持分层数据结构，只需通过链式调用属性即可；取决于所选择的输出格式，这种层次结构通过分隔符（INI）或嵌套（XML）表示。

由上述代码生成的配置文件如下：

```ini
[blog]
allowComments = "yes"
displayComments = "yes"
allowTrackbacks = "yes"
defaultAuthor = "Jack Frost"
numPostsOnPageIndex = 5
```

```ini
[calendar]
weekStartsOn = "Monday"
highlightToday = 1
events.displayTitle = 1
```

抱歉，我需要重新翻译最后一段，因为之前的逻辑出现了混乱。以下是正确的翻译：

```ini
[calendar]
weekStartsOn = "Monday"
highlightToday = 1
events.displayTitle = 1
```

（等等，我发现原文文本在最后似乎出现了重复和错乱，我将根据你提供的原文内容重新梳理并翻译，确保逻辑完整性。）

---

**重新翻译的文本（基于你提供的乱乱原文修复）：**

# 第 7 章：分页、排序与数据上传

```php
// 将 view->b 设置为 'white'
$this->view->b = $config->object->typeface->color;
```

### 注意事项

默认情况下，在 `Zend_Config` 对象中表示的配置数据是只读的，任何修改它的尝试都将产生异常。要允许修改，请将额外的 `options` 数组作为第三参数传递给 `Zend_Config` 对象，并将 `allowModifications` 键指定为 `true`。关于此点的更多信息可以参考本章末尾的链接。

还有一个名为 `Zend_Config_Xml` 的适配器，专门用于处理 XML 编码的配置。

```xml
<?xml version="1.0"?>
<configuration>
  <application>
    <name>SomeApp</name>
    <version>2.3</version>
    <window>
      <height>600</height>
      <width>500</width>
      <titlebar>
        <title>Export Data</title>
        <foregroundColor>#ffffff</foregroundColor>
        <backColor>#0000ff</backColor>
      </titlebar>
    </window>
  </application>
</configuration>
```

这里是一个使用 `Zend_Config_Xml` 适配器读取此文件并从内部访问配置值的示例：

```php
<?php
class Sandbox_ExampleController extends Zend_Controller_Action
{
    public function configAction()
    {
        // 初始化配置对象
        $config = new Zend_Config_Xml(APPLICATION_PATH . "/configs/example.xml");
    }

    // 将 view->a 设置为 '2.3'
    $this->view->a = $config->application->version;
```

# Zend Framework：入门指南

```php
// 将 $view->b 设置为 'Export Data'
$this->view->b = $config->application->window->titlebar->title;
}
```

### 写入配置文件

这解决了读取文件问题，但如何写入文件呢？`Zend_Config` 包含一个写入组件 `Zend_Config_Writer`，它可以用于创建 PHP、XML 或 INI 格式的配置文件。配置数据可以分层次或分节排列，以获得更高的可读性。

以下是一个说明如何使用 `Zend_Config_Writer` 生成 INI 格式的配置文件的示例：

```php
<?php
class SandboxExampleController extends Zend_Controller_Action {
    public function configAction() {
        // 创建配置对象
        $config = new Zend_Config(array(), 1);

        // 创建节
        $config->blog = array();
        $config->blog->allowComments = 'yes';
        $config->blog->displayComments = 'yes';
        $config->blog->allowTrackbacks = 'yes';
        $config->blog->defaultAuthor = 'Jack Frost';
        $config->blog->numPostsOnIndexPage = 5;

        // 创建节
        $config->calendar = array();
        $config->calendar->weekStartOn = 'Monday';
        $config->calendar->highlightToday = 1;

        // 创建子节
        $config->calendar->events = array();
        $config->calendar->events->displayTitle = 1;
        $config->calendar->events->displayStartTime = 1;
        $config->calendar->events->displayEndTime = 0;
        $config->calendar->events->displayLocation = 1;

        // 将数据写入文件
        $writer = new Zend_Config_Writer_Ini();
        $writer->write(APPLICATION_PATH . "/configs/example.ini", $config);
    }
}
```

# 第 7 章：分页、排序与数据上传

第一步是初始化一个 `Zend_Config` 对象，它代表配置数据。该对象的初始化应该使用包含配置数据的数组（如果没有数据存在，则使用空数组）以及一个指示配置数据是否可以被修改的布尔参数。`Zend_Config` 对象初始化后，可以使用标准的对象表示法将单个配置变量设置为属性。它支持分层数据结构，只需通过链式调用属性即可；取决于所选择的输出格式，这种层次结构通过分隔符（INI）或嵌套（XML）表示。

由上述代码生成的配置文件如下：

```ini
[blog]
allowComments = "yes"
displayComments = "yes"
allowTrackbacks = "yes"
defaultAuthor = "Jack Frost"
numPostsOnPageIndex = 5
```

```ini
[calendar]
weekStartsOn = "Monday"
highlightToday = 1
events.displayTitle = 1
```

（注：由于原文后半部分出现了严重的文本重复和错乱，此处已根据你提供的逻辑片段进行了清理和翻译。）

## Zend Framework：入门指南

……可配置的，并且已经决定了应该如何呈现这些配置选项。在这种情况下，让我们假设应用程序的以下方面是可配置的：

- 通过联系表单发送消息的电子邮件地址
- 所有应用程序和用户消息的默认（或回备）电子邮件地址
- 管理控制面板中每页显示的项目数量
- 公共目录中卖家名称和地址的可见性
- 异常日志记录到磁盘文件中

以下是相应的表单定义，应保存到 `$APP_DIR/library/Square/Form/Configure.php`：

```php
<?php
class Square_Form_Configure extends ZendForm {
    public function init() {
        // 初始化表单
        $this->setAction('/admin/config')
            ->setMethod('post');

        // 为默认邮箱创建文本输入
        $default = new Zend_Form_Element_Text('defaultEmailAddress')
            ->Label('所有操作的回备邮箱地址：')
            ->setOptions(array('size' => '40'))
            ->setRequired(true)
            ->addValidator('EmailAddress')
            ->addFilter('HtmlEntities')
            ->addFilter('StringTrim');

        // 为销售邮箱创建文本输入
        $sales = new Zend_Form_Element_Text('salesEmailAddress')
            ->Label('销售查询的默认邮箱地址：')
            ->setOptions(array('size' => '40'))
            ->addValidator('EmailAddress')
            ->addFilter('HtmlEntities')
            ->addFilter('StringTrim');

        // 为管理摘要中的每页项目数创建文本输入
        $items = new Zend_Form_Element_Text('itemsPerPage')
            ->setLabel('管理视图中每页的项目数：')
            ->setOptions(array('size' => '4'))
            ->setRequired(true)
            ->addValidator('Int');
```

```php
->addFilter('HtmlEntities')
->addFilter('StringTrim');

// 为显示卖家名称和地址创建单选按钮
$seller = new Zend_Form_Element_Radio('displaySellerInfo');

$seller->setLabel('目录显示卖家名称和地址：')
    ->setRequired(true)
    ->setMultiOptions(array(
        '1' => 'Yes',
        '0' => 'No'
    ));

// 为异常日志创建单选按钮
$log = new Zend_Form_Element_Radio('logExceptionsToFile');

$log->setLabel('异常记录到文件：')
    ->setRequired(true)
    ->setMultiOptions(array(
        '1' => 'Yes',
        '0' => 'No'
    ));

// 创建提交按钮
$submit = new Zend_Form_Element_Submit('submit');

$submit->setLabel('保存配置')
    ->setOptions(array('class' => 'submit'));

// 将元素附加到表单
$this->addElement($sales)
    ->addElement($default)
    ->addElement($items)
    ->addElement($seller)
    ->addElement($log)
    ->addElement($submit);
}
```

## 第 7 章：分页、排序和数据上传

### 定义配置文件

下一步是定义存储用户级配置设置的文件。Zend Framework 建议使用 `$APP_DIR/application/configs/` 目录用于所有配置，因此让我们使用该目录。打开位于 `$APP_DIR/application/configs/application.ini` 的主应用程序配置文件，并添加以下指令来定义用户级配置文件的位置：

```ini
configs.localConfigPath = APPLICATION_PATH "configs/square.ini"
```

（续）

## Zend Framework：入门指南

### 定义自定义路由

下一步是定义通往配置控制器的路由。由于配置面板不属于任何特定模块，因此该控制器可以放在通用的“default”模块中。以下是路由定义，应添加到 `$APP_DIR/application/configs/application.ini` 的应用程序配置文件中：

```ini
resources.router.routes.admin-config.route = /admin/config
resources.router.routes.admin-config.defaults.module = default
```



`resources.router.routes.admin-config.defaults.controller = config`

`resources.router.routes.admin-config.defaults.action = index`

```

```

`resources.router.routes.admin-config-success.route = /admin/config/`

`resources.router.routes.admin-config-success.module = default`

`resources.router.routes.admin-config-success.defaults.controller = config`

`resources.router.routes.admin-config-success.defaults.action = success`

## 问问专家

**Q：** 我我很困惑。为什么要在一个配置文件中存储另一个配置文件的位置呢？

**A：** 位于 `$APP_DIR/application/configs/application.ini` 的应用程序配置文件是一个全局文件，由 Zend Framework 应用程序读取。通常，它包含许多由应用程序设计师定义的设置，在不经过考虑的情况下不应进行修改。尽管如此，每个应用程序都有各种用户级设置，这些设置应该允许应用程序用户和管理员进行配置。对于 SQUARE 应用程序，这些设置存储在单独的用户级配置文件中，路径为 `$APP_DIR/application/configs/square.ini`。

通常建议这种这种将系统级设置与用户级设置分离，因为这允许这两种类型的变量独立进行操作，而不会有损坏的风险。然而，两者之间也需要一个链接。

## 第 7 章：分页、排序和数据上传

### 定义控制器

下一步是定义配置的控制器和视图。以下是控制器的代码，应保存如下：

```php
<?php

class ConfigController extends Zend_Controller_Action
{
    protected $localPath;

    public function init()
    {
        // 生成表单
        $form = new Square_Form_Configure();
        $this->view->form = $form;

        // 如果配置存在
        // 读取配置
        // 使用值预填充表单
        if (file_exists($this->localPath)) {
            $config = new Zend_Config_Ini($this->localPath);
            $data['defaultEmailAddress'] = $config->global->defaultEmailAddress;
            $data['salesEmailAddress'] = $config->user->salesEmailAddress;
            $data['itemsPage'] = $config->admin->itemsPage;
            $data['displaySellerInfo'] = $config->user->displaySellerInfo;
            $data['logExceptionsToFile'] = $config->global->logExceptionsToFile;
            $form->populate($data);
        }
    }

    // 处理设置的动作
    public function indexAction()
    {
        // 检查用户是否已认证
        if (!Zend_Auth::getAuth()->hasIdentity()) {
            $session = new Zend_Session_Namespace('square');
            $session->URL = $this->getRequest()->Uri();
            $this->_redirect('/login');
        }
    }

    // 保存配置的动作
    public function saveAction()
    {
        // 测试有效输入
        // 如果有效，创建新的配置对象
        // 创建配置部分
        // 将配置值保存到文件
        // 覆盖之前的版本
        if ($form->getRequest()->isPost()) {
            if ($form->isValid($this->getRequest()->getPost())) {
                $values = $form->getValues();

                $config = new Zend_Config(array(), true);
                $config->global = array();
                $config->admin = array();
                $config->user = array();

                $config->global->defaultEmailAddress = $values['defaultEmailAddress'];
                $config->user->salesEmailAddress = $values['salesEmailAddress'];
                $config->admin->itemsPage = $values['itemsPage'];
                $config->user->displaySellerInfo = $values['displaySellerInfo'];
                $config->global->logExceptionsToFile = $values['logExceptionsToFile'];

                $writer = new Zend_Config_Writer_Ini();
                $writer->write($this->localPath, $config);

                $this->_helper->getHelper('FlashMessenger')->addMessage(
                    '感谢您。您的配置已成功保存。'
                );

                $this->_redirect('/admin/config/success');
            }
        }
    }

    // 成功动作
    public function successAction()
    {
        if ($this->_helper->getHelper('FlashMessenger')->getMessages()) {
            $this->view->messages =
                $this->_helper->getHelper('FlashMessenger')->getMessages();
        }
    }
}
```

```php
$this->redirect('/');
}

}
```

该控制器的主要工作由 `indexAction()` 方法完成，它负责验证接收到的输入，并使用 `ZendConfigWriter` 组件将配置数据写入 INI 文件。在初始化配置表单时，`indexAction()` 方法还会使用 `ZendConfig` 组件读取源配置文件（如果可用），并用当前的配置设置对其进行预填充。

配置文件的位置直接从应用程序文件中读取，并在控制器的 `init()` 方法中存储为受保护的类属性。由于该控制器仅供管理员使用，因此 `preDispatch()` 方法会检查是否存在已身份验证的用户，如果不存在则将重定向到登录页面。

以下是对应的视图脚本，它应该保存为 `$APP_DIR/application/modules/default/views/scripts/config/index.php`：

```php
<h2>Edit Settings</h2>

<?php echo $this->form; ?>
```

### 更新主布局

剩下的所有工作就是更新 `$APP_DIR/application/layouts/admin.php` 中的管理布局，以便在用户登录时在主菜单中显示“Settings（设置）”项。布局的修订在下面的示例中用粗体标记：

```html
<!DOCTYPE html PUBLIC "//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">

<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">

<div id="menu">

  <?php if ($user->hasIdentity()): ?>

    <a href="<?php echo $this->url(array(
      'admin-catalog-index');
    ))">CATALOG</a>

    <a href="<?php echo $this->url(array(
      'admin-config');
    ))">SETTINGS</a>

    <a href="<?php echo $this->url(array(
      'logout');
    ))">LOGOUT</a>

  <?php else: ?>

    <a href="<?php echo $this->url(array(
      'login');
    ))">LOGIN</a>

  <?php endif; ?>

</div>

</html>
```

## Zend Framework：初学者指南

**图 7-9** SQUARE 应用配置表单

你现在可以尝试一下了，登录应用程序的管理面板并浏览到 URL `http://square.localhost/admin/config`。图 7-9 展示了你应该看到的配置表单。

在此配置表单中输入值并提交。数据现在应该被保存到文件 `$APP_DIR/application/configs/square.ini` 中。查看此文件，你将看到 INI 格式的数据，如图 7-10 所示。

如果你再次访问 URL `http://square.localhost/admin/config`，你会发现配置表单自动预填充了之前保存的设置。图 7-11 显示了输出。

![](img/222e7e58871b088cc6397852e1452b57_252_0.png)

**图 7-10** INI 格式的示例配置数据

![](img/222e7e58871b088cc6397852e1452b57_253_0.png)

## 使用配置数据

成功读取和写入配置数据只赢得了一半战斗——你仍然需要利用这些数据来告知特定控制器和操作的行为。例如，考虑 `ContactController::indexAction` 现在应该根据该文件的说明进行修改。以下是修订后的 `ContactController::indexAction`：用于读取用户级配置文件并将其消息发送到该文件中的销售地址。

```php
<?php

class ContactController extends Zend_Controller_Action
{
    public function indexAction()
    {
        $form = new Square_Form_Config();
        $this->view->form = $form;

        if ($this->getRequest()->isPost()) {
            if ($this->getRequest()->getPost()) {
                $values = $form->getValues();
                $configs = $this->invokeArg('bootstrap');
                $localConfig = new Zend_Config($opt['localConfigPath']);

                $to = (empty($localConfig->user->salesEmailAddress)) ?
                    $localConfig->user->salesEmailAddress :
                    $localConfig->global->defaultEmailAddress;

                $mail = new Zend_Mail();
                $mail->setBodyText($values['message']);
            }
        }
    }
}
```

```php
$this->setFrom($values['email'], $values['name']);
$this->addTo($to);
$this->setSubject('Contact form submission');
$this->send();

$this->_helper->getHelper('FlashMessenger')->addMessage(
    'Thank you. Your message was successfully sent.'
);

$this->redirect('/contact/success');
```

同样地，`Catalog_ItemController::displayAction` 也应该更新，以检查目录中是否显示卖家信息，并显示这些信息。以下是修订后的 `Catalog_ItemController::displayAction`，它在读取用户级配置后为视图设置了一个标志：

```php
<?php

class CatalogItemController extends Zend_Controller
{
    public function displayAction()
    {
        // set filters
        $filters = array(
            'id' => array('NotEmpty')
        );

        $validators = array(
            'id' => array('NotEmpty', 'Trim')
        );

        $input = new Zend_Filter($this->getRequest()->get('id'), $filters);
        $input = new Zend_Validator($this->getRequest()->get('id'), $validators);

        // test if input is valid
        if ($input->isValid()) {
            // retrieve record
            $configs = $this->invokeArg('bootstrap')->getResource('config');
            $localConfig = new Zend_Config($configs['localConfigPath']);
            $this->view->seller = $localConfig->user;

            $q = Doctrine_Query::create()
                ->from('item', 'i')
                ->leftJoin('grade', 'i.grade_id = g.id', 'g')
                ->leftJoin('country', 'i.country_id = c.id', 'c')
                ->leftJoin('type', 'i.type_id = t.id', 't')
                ->where('i.id = ?', $input->getValue())
                ->where('i.Status = 1');

            $result = $q->fetchArray();

            if (count($result) == 1) {
                $this->view->item = $result[0];
            } else {



```php
throw new Zend_Controller_Exception('Page not found');
```

```php
}

} else {

    throw new Zend_Controller_Exception('Invalid input');

}

}

}
```

## 第 7 章：分页、排序与上传数据

```php
<?php echo $this->escape($this->item['Title']); ?>
```

```php
<?php echo $this->escape($this->item['Year']); ?>
```

```php
<?php echo $this->escape($this->item['GradeName']); ?>
```

```html
<h2>View Item</h2>

<h3>FOR SALE:</h3>
```

```html
<table>
```

```html
<tr>
  <td></td>
</tr>
```

```html
<tr>
  <td>Title:</td>
  <td><?php echo $this->escape($this->item['Title']); ?></td>
</tr>

<!-- other display fields -->

<tr>
  <td>Description:</td>
  <td><?php echo $this->escape($this->item['Description']); ?></td>
</tr>

<?php if ($this->seller != 1): ?>
<tr>
  <td>Seller:</td>
  <td>
    <?php echo $this->escape($this->item['SellerName']); ?>,
    <?php echo $this->escape($this->item['SellerAddress']); ?>
  </td>
</tr>
<?php endif; ?>

</table>
```

```html
</div>
```

将用户级配置与 `Catalog_AdminController::indexAction` 中的 `Doctrine_Pager` 组件相结合，确保每页显示的项目数量反映用户指定的值，而不是应用程序设计师设置的任意值。代码由于空间限制未包含，但你可以在本章的代码存档中找到它。

### 提示

如果你有许多控制器和操作从同一个用户级配置文件读取数据，可以通过让应用程序引导自动将其读取到本地资源注册表来节省某些代码。该注册表可以通过 `Zend_Application_Bootstrap` 类的 `getResource()` 方法在应用程序的任何地方访问。在内部，注册表由 `Zend_Registry` 组件的实例表示，该组件为全局对象或变量提供了应用程序级的存储区域。有关应用程序引导和 `Zend_Registry` 组件更多可以通过可以通过末尾的链接获取，你将在后续章节中找到大量使用 `Zend_Registry` 的示例。

## 第 7 章：分页、排序与数据上传 239

## 摘要

本章重点介绍了三个组件，它们对你来说都是全新的领域：`Doctrine_Pager` 组件，它为大型数据库结果集的分页提供了一个框架；`Zend_File_Transfer` 组件，它提供了一个功能完整的 API，用于验证、过滤和接收通过 Web 表单上传的文件；以及 `Zend_Config` 组件，它能够方便地处理不同格式的配置数据引用。所有这些组件都通过 SQUARE 示例中的实际功能进行了演示说明，该示例现在配备了分页和排序功能、配置面板以及图像上传系统。

如需了解更多关于本章所讨论的话题，请考虑访问以下链接：

- `Doctrine_Pager` 组件，位于：http://www.doctrine-project.org/documentation/manual/1/en/utilities#pagination:working-with-pager
- `Zend_Paginator` 组件，位于：http://framework.zend.com/manual/en/zendpaginator.html
- `Zend_File_Transfer` 组件，位于：http://framework.zend.com/manual/en/zend.file.html
- `Zend_File_Transfer` 组件的过滤器和验证器，位于：http://framework.zend.com/manual/en/zend.file.transfer.filters.html 和 http://framework.zend.com/manual/en/zend.file.transfer.validators.html
- `Zend_Config` 组件，位于：http://framework.zend.com/manual/en/zend.config.html
- `Zend_Registry` 组件，位于：http://framework.zend.com/manual/en/zend.registry.html
- Bootstrap 类和本地资源注册表，位于：http://framework.zend.com/manual/en/zend.application.theory-of-operation.html
- 注册模式（Registry pattern）的解释（Martin Fowler），位于：http://martinfowler.com/eaaCatalog/registry.html
- 为 Zend Framework 启动器创建自定义资源插件的讨论（Stefan Schmalhaus），位于：http://blog.log2e.com/2009/06/01/creating-a-custom-resource-plugin-in-zend-framework/18/
- `Zend_Config` 组件的教程（Aaron Wormus），位于：http://devzone.zend.com/article/1264

## 第 8 章：日志记录与异常调试

## Zend Framework：初学者指南

### 核心技能与概念

- 学习 PHP 5.x 异常模型
- 理解 Zend Framework 应用中是如何处理异常的
- 将自定义异常类与默认的 Zend Framework 错误处理器集成
- 控制生产环境中错误信息的可见性
- 通过将异常记录到文件或数据库中来维护异常的永久记录
- 使用额外的调试信息增强日志消息
- 使用 Firebug 控制台调试器实时跟踪异常

在经验较浅的开发者中，一个常见的误解是认为一个“好的”程序是不产生错误运行的程序。事实上，这并不完全正确：一个更好的定义可能是，一个好的程序是能够预见到所有可能的错误情况，并以一致的方式处理它们的程序。

编写符合这种定义的“智能”程序既是一门艺术也是一门科学。经验和想象力在评估潜在错误原因和定义纠正措施方面起着重要作用，但编程框架本身定义了用于捕获和解决错误的可用工具和函数。

通过使用 Zend Framework 开发应用程序，错误处理并不像许多其他框架那样令人担忧。Zend Framework 提供的错误处理器可以开箱即用处理大多数常见情况，还有许多组件（如 `Zend_Log` 和 `Zend_Debug`）可以为开发者和管理员提供额外信息。本章将向你介绍所有这些工具，并解释如何在实际场景中使用它们。

## 理解异常

PHP 5.x 引入了一种新的异常模型，类似于 Java 和 Python 等其他编程语言所使用的模型。在这种基于异常的方法中，程序代码被封装在 `try` 块中，其生成的异常由一个或多个 `catch` 块“捕获”并解决。由于存在多个 `catch` 块，开发者可以捕获不同类型的异常并对每个类型进行不同的处理。

## 第 8 章：日志记录与异常调试 243

为了说明这是如何工作的，请考虑以下代码列表，它尝试使用 `ArrayIterator` 访问一个不存在的数组元素：

```php
<?php

// 定义数组

$cities = array(
  'London',
  'Washington',
  'Paris',
  'Delhi'
);

// 尝试访问不存在的数组元素

// 生成 OutOfBoundsException

try {
  $iterator = new ArrayIterator($cities);
  $iterator->seek(10);
} catch (Exception $e) {
  echo "ERROR: Something went wrong!\n";
  echo "error: " . $e->getMessage() . "\n";
  echo "Error code: " . $e->getCode() . "\n";
  echo "File name: " . $e->getFile() . "\n";
  echo "Line: " . $e->getLine() . "\n";
  echo "Backtrace: " . $e->getTraceAsString() . "\n";
}

?>
```

当 PHP 遇到封装在 `try-catch` 块中的代码时，它首先尝试执行 `try` 块中的代码。如果处理这段代码时没有生成任何异常，控制权将转移到 `try` 块之后的行。

### 专家问答

**Q：** 我看到未捕获的异常会产生终止脚本的致命错误。我可以更改它吗？

**A：** 可以，也不行。PHP 提供了 `set_exception_handler()` 函数，它允许你用自己的代码替换 PHP 默认异常处理器，方式就像 `set_error_handler()` 做的那样。然而，有一个重要的注意事项需要注意：虽然你可以更改通知的方式和外观，但你无法让脚本在生成异常的地方继续执行。

| 方法名 | 描述 |
| --- | --- |
| `getMessage()` | 返回描述发生错误的消息 |
| `getCode()` | 返回数值错误代码 |
| `getFile()` | 返回生成异常的脚本磁盘路径和名称 |
| `getLine()` | 返回生成异常的行号 |
| `getTrace()` | 返回导致错误的调用堆栈（数组形式） |
| `getTraceAsString()` | 返回导致错误的调用堆栈（字符串形式） |

**表 8-1** PHP 异常的方法

每个异常对象都包含了用于调试错误源的额外信息。（后略）

一种更高级的方法是继承通用的 `Exception` 并为每种可能的错误创建特定的异常对象。为了处理不同类型的异常，当你需要为每个异常类型使用独立的 `catch` 块（以及处理代码）时，这种方法非常有用。以下是前面示例的修订版本，它说明了这一点：

```php
<?php

// 继承 Exception

class MissingFileException extends Exception { }

class DuplicateFileException extends Exception { }

class FileIOFileException extends Exception { }

// 设置文件名

// 尝试复制并删除文件

$file = 'dummy.txt';

try {
    if (file_exists($file)) {
        throw new MissingFileException($file);
    }

    if (file_exists("$file.new")) {
        throw new DuplicateFileException("$file.new");
    }
```

```php
if (!copy($file, "$file.new")) {
    throw new FileIOException("$file.new");
}

if (!unlink($file)) {
    throw new FileIOException($file);
}
```

```php
catch (MissingFileException $e) {
    echo 'ERROR: Could not find file ' . $e->getMessage() . '\n';
    exit();
} catch (DuplicateFileException $e) {
    echo 'ERROR: Destination file ' . $e->getMessage() . ' already exists';
    exit();
} catch (FileIOException $e) {
    echo 'ERROR: Could not perform file input/output operation on file ' . $e->getMessage() . '\n';
    exit();
} catch (Exception $e) {
    echo 'ERROR: Something happened on line ' . $e->getLine() . ': ' . $e->getMessage();
    exit();
}
```

```php
echo 'SUCCESS: File operation successful.';
?>
```

此脚本扩展了 Base 类并创建了三种新的异常类型，每种类型代表一种不同的错误。为每个异常设置一个独立的 `catch` 块，可以自定义处理这些异常的方式。最后一个 `catch` 块是一个通用的“全能捕获”处理器。未被上述更具体的代码块处理的异常将传递到此处理器并由其处理。

基于异常的方法具有许多优势：

- 在没有异常处理机制的情况下，必须检查每个被调用的函数的返回值，以识别是否发生了错误并采取纠正措施。这会产生不必要的复杂且深度嵌套的代码块。可以使用单个 `catch` 块来捕获前一个代码块中发生的任何错误。这消除了多个级联错误测试的需要，使代码更简单、更具可读性。
- 在没有异常的情况下，错误处理本质上是指令性的：它要求开发者思考所有可能的路径并为每种可能性编写代码。相比之下，基于异常的方法更加灵活。通用的异常处理器像安全网一样，可以捕获并处理即使没有编写特定处理代码的错误。这有助于使应用程序代码更加健壮，并对意外情况更具韧性。
- 由于异常模型使用了基于对象的方法，开发者可以使用继承和扩展等 OOP 概念对基对象进行子类化，并为不同类型的异常创建不同的 `Exception` 对象。这使得区分不同类型的错误并以不同的方式处理每个类型成为可能。
- 基于异常的方法迫使开发者对如何处理不同类型的错误做出艰难决策。在没有异常的情况下，开发者可以很容易地（通过审计或设计）省略检查函数返回值的测试。然而，异常并不容易被忽略。通过要求开发者创建并填充 `catch` 块，异常模型迫使他们思考错误的原因和后果，最终导致更优的设计和更健壮的实现。

所有 Zend Framework 组件都显式设计为默认使用异常模型，每个组件根据需要扩展基 `Zend_Exception` 类。因此，无论你是将 Zend Framework 组件作为大型应用程序的独立部分使用，还是在 Zend Framework MVC 应用程序上下文中使用，方法的一致性都可以显著减少开发级错误处理功能所需的时间。

### 理解默认错误处理流程

让我们更仔细地观察 Zend Framework MVC 应用程序中的异常处理。默认情况下，当抛出异常时，异常会沿着执行链“向上冒泡”，直到到达前端控制器（front controller）。前端控制器包含一个错误处理器插件（作为引导过程的一部分自动注册），该插件负责将异常转发到应用程序的默认错误控制器。然后，错误控制器检查异常并向请求客户端显示适当的错误视图。

这个错误控制器从哪里来？对于使用命令行脚本创建的项目，它会自动在默认项目层中生成。对于手动创建的项目，必须手动生成。在任何情况下，它都被表示为一个独立的控制器和动作 `ErrorController::errorAction`，并位于应用程序的“default”模块中。以下是其典型外观示例：

```php
<?php

class ErrorController extends Zend_Controller_Action
{
    public function errorAction()
    {
        $errors = $this->getParam('error_handler');
    }

    switch ($errors->type) {
        case Zend_Controller_Plugin_ErrorHandler::EXCEPTION_NO_CONTROLLER:
        case Zend_Controller_Plugin_ErrorHandler::EXCEPTION_NO_ACTION:
            // 404 - 未找到控制器或动作

            $this->getResponse()->setStatusCode(404);
            $this->view->message = 'Page not found';
            break;

        default:
            // 应用程序错误

            $this->getResponse()->setHttpResponseCode(500);
            $this->view->message = 'Application error';
            break;
    }

    $this->view->exception = $errors->exception;
    $this->view->request = $errors->request;
```




该错误控制器旨在处理两种情况：无效的 HTTP 请求和动作代码生成的异常。它对前者响应 404 错误码，对后者响应 500 错误码。要查看其运行效果，请考虑以下示例：

```php
<?php

class Sandbox_ExampleController extends Zend_Controller_Action
{
    public function failAction()
    {
        // 尝试访问不存在的数组元素
        // 生成 OutOfBoundsException
        $cities = array(
            'London',
            'Washington',
            'Paris',
            'Delhi'
        );

        $iterator = new ArrayIterator($cities);
        $iterator->seek(10);
    }
}
```

在这种情况下，异常将一直向上传递直到到达前端控制器。前端控制器包含一个错误处理器插件（作为引导过程的一部分自动注册），该插件负责将异常转发到应用程序的默认错误控制器。错误控制器随后检查异常并向请求客户端显示适当的错误视图。

该错误控制器设计用于处理两种情况：无效的 HTTP 请求和动作代码生成的异常。它对前者响应 404 错误码，对后者响应 500 错误码。

（此处省略原文中重复的内容）

### 使用自定义异常类

如果你的应用程序使用了自定义类，通常应该修改默认错误控制器以根据捕获的异常类型切换其处理方式。这允许开发者超越默认控制器处理的两种基本错误类型，并对不同类型的异常进行更细粒度的控制。为了说明其工作原理，请考虑之前代码列表的以下变体：

注意除了错误消息外，默认视图还包含堆栈跟踪。图 8-1 显示了错误的示例。

错误处理器的行为符合大多数应用程序的需求——在大多数情况下，期望响应为 500。然而，如果你的应用程序使用了自定义类，通常应该修改默认错误控制器以根据捕获的异常类型切换其处理方式。这将在下一节中进行讨论。

## 250 Zend Framework：入门指南

当你以这种方式使用自定义异常时，通常会更改默认错误控制器并为不同的异常类型添加特定的处理代码。以下是一个操作方法示例：

```php
<?php

class ErrorController extends ZendControllerAction
{
    public function errorAction()
    {
        $errors = $this->param('error_handler');
        $this->view->exception = $errors->exception;
        $this->view->request = $errors->request;

        switch (class_get($errors->exception)) {
            // 处理无效文件异常
            case 'Invalid_File_Exception':
                $this->getResponse()->setHttpResponse(500);
                $this->view->title = '文件未找到';
                $this->view->message =
                    '读取应用程序所需的文件时发生错误。';
                break;

            // 处理重复文件异常
            case 'Duplicate_File_Exception':
                $this->getResponse()->setHttpResponse(500);
                $this->view->title = '文件已存在';
                $this->view->message =
                    '写入应用程序所需的文件时发生错误。';
                break;

            // 处理 404 异常
            case 'Zend_Dispatcher_Exception':
                $this->getResponse()->setHttpResponse(404);
                $this->view->title = '页面未找到';
                $this->view->message = '找不到请求的页面。';
                break;

            // 处理通用的操作异常
            case 'Zend_Controller_Exception':
                if ($errors->getCode() == 404) {
                    $this->getResponse()->setHttpResponse(404);
                    $this->view->title = '页面未找到';
                    $this->view->message = '找不到请求的页面。';
                } else {
                    $this->getResponse()->setHttpResponse(500);
                    $this->view->title = '内部服务器错误';
                    $this->view->message =
                        '由于应用程序错误，无法显示
                        请求的页面。';
                }
                break;

            // 处理其他所有情况
            default:
                $this->getResponse()->setHttpStatusCode(500);
                $this->view->title = '内部服务器错误';
                $this->view->message = \
'由于应用程序错误，请求的页面\n无法显示。';
```

在这里，`errorHandler()` 首先通过 `'error_handler'` 请求参数获取操作控制器抛出的异常对象。它检查异常类，并根据异常名称切换到不同的代码分支。在这个示例中，除了标准情况（请求无效资源和通用的未捕获异常）外，控制器还为应用程序使用的自定义异常类设置了特定分支。不言而喻，这个 `switch-case()` 语句可以扩展，以显示所需的任意数量的自定义异常类。

### 控制异常的可见性

通常情况下，当应用程序迁移到生产环境时，在错误消息中包含堆栈跟踪和其他调试信息并不是一个好主意。这些信息包含敏感信息，例如 SQL 查询输出、文件位置和用户密码，恶意用户可以利用这些信息识别应用程序的弱点并对其远程发起攻击。在生产环境中隐藏这些信息是提高应用程序安全性的重要步骤。

典型的 Zend Framework 应用带有四种环境的配置设置：开发、测试、阶段（staging）和生产。在默认设置下，这些环境中的错误显示处理如下：

- 在开发和测试环境中，PHP 的 `display_errors` 和 `display_startup_errors` 配置变量被设置为 `true`，导致错误消息显示给用户。在阶段和生产环境中，这些变量被设置为 `false`，结果错误消息对用户隐藏了。

### 提问专家

**Q：** 我如何在生产环境和开发环境之间切换？

**答：** 当前环境的信息在 `.htaccess` 文件中指定，作为名为 `APPLICATION_ENV` 的服务器环境变量。在每次请求中，`index.php` 脚本都会检查该变量并将其传递给 Zend Application 组件。然后 Zend 读取配置文件的适当块，并根据该块指定的指令设置应用程序变量。因此，要从一个环境切换到另一个环境，只需编辑应用程序的 `.htaccess` 文件，并将 `APPLICATION_ENV` 变量的值设置为所需的环境名称。

## 252 Zend Framework：入门指南

在开发环境中，默认错误视图包含错误消息、堆栈跟踪和请求空间的变量转储（variable dump）。在生产、阶段和测试环境中，仅向用户显示错误消息。

可以通过修改应用程序配置文件中的适当块，并更改错误视图以根据当前正在使用的环境显示更多或更少的信息来调整这些设置（下一节将提供此类示例）。

## 尝试此 8-1 创建一个自定义错误页面

考虑到所有这些点，让我们尝试为 SQUARE 示例创建一个自定义的错误页面。

由于我们没有任何特殊处理需求，我们可以保持控制器不变，只进行一个微小的更改：为页面标题添加一个视图变量。你将在“尝试此 8-2”章节中看到这一微改，并可以在该章节的代码存档中找到它。

我们现在可以通过更新默认错误视图脚本来自定义错误视图，该路径为 `$APP_DIR/application/modules/default/views/scripts/error.php`，以包含一些内容：

```php
<div id="error">
  <img src="error.gif" />
  <h1><?php echo $title;</h1>
  <p><?php echo $message; ?></p>
  <?php if ('development' == APPLICATION_ENV) : ?>
  <div id="data">
    <h2>异常消息</h2>
    <pre><?php echo $exception->getMessage(); ?></pre>
    <h2>堆栈跟踪</h2>
    <pre><?php echo $exception->getTraceString(); ?></pre>
    <h2>请求方法</h2>
    <pre><?php echo $request->getMethod(); ?></pre>
    <h2>请求参数</h2>
    <pre><?php echo $request->getParameters(); ?></pre>
    <h2>服务器环境</h2>
    <pre><?php echo $request->getServer(); ?></pre>
    <h2>系统环境</h2>
    <pre><?php echo $request->getEnv(); ?></pre>
  </div>
  <?php endif ?>
</div>
```

此错误视图根据错误是 404 还是 500 显示两种消息之一。显示的信息也取决于环境。例如，图 8-4 显示了生产环境下的输出，而图 8-5 显示了开发环境下的输出。

## 254 Zend Framework：入门指南

### 提问专家

**Q：** 什么是 `Zend_Debug`？

**答：** `Zend_Debug` 提供了一种检查 PHP 变量的方便方法。它暴露了一个单一静态方法 `dump()`，可以将变量的内容转到标准输出，同时添加 `<pre>...</pre>` 标签并清理换行以获得更好的格式。

**TIP** `Zend_Controller_Request_Http` 对象暴露了获取当前请求信息的各种方法，其中一些用在之前的列表中。`getParameters()` 方法返回请求参数的数组，`getServer()` 方法返回环境变量（`$_SERVER`）的数组，`getEnv()` 方法返回当前环境（`$_ENV`）的数组。

## 日志记录

你已经在上一节中看到，在生产环境中可以更改呈现给调试信息量。然而，尽管这些信息不应该显示给用户，但对应用程序开发人员和管理员是有值的。因此，Zend Framework 包含 `Zend_Log` 组件，它提供了一个通用的日志框架，可以将任何类型的数据（包括但不限于异常）记录到文件或其他存储中。这种审计通常用于调试、审计或报告。

`Zend_Log` 组件非常灵活。它支持多个日志目标（标准输出设备、文件、数据库、电子邮件、XML 或自定义）以及多个日志优先级（从信息到紧急）。它的其他功能还包括用户定义的优先级、用户定义的日志格式、基于优先级的日志过滤器以及对 Firefox（浏览器调试器）控制台输出的支持。

后续章节将详细介绍这些特性。

### 日志消息

这是一个使用 `Zend_Log` 按指定格式记录消息的简单示例：

```php
<?php
class Sandbox_ExampleController extends Zend_Controller_Action
{
    public function logAction()
    {
```

## 第 8 章：日志与异常调试

```php
// initialize logging engine
$logger = new Zend_Log();
```

```php
// attach writer to logging engine
$writer = new Zend_Log_Writer_Stream(
    APPLICATION_PATH . '/../data/logs/example.log'
);
$logger->addWriter($writer);
```

```php
// attach formatter to writer
$format = '%timestamp%% %priorityName%% %message%' . PHP_EOL;
$formatter = new Zend_Log_Formatter_Simple($format);
$writer->setFormatter($formatter);
```

```php
// write log message
$logger->log('Body temperature critical', Zend_Log::EMERG);
```

图 8-6 展示了输出的样式。从前面的示例可以清楚地看到，日志消息涉及多个不同的对象。

- `Zend_Log` 对象作为生成日志消息的主要控制器。它暴露了一个 `log()` 方法用于启动日志写入操作。

- `Zend_Log_Writer` 对象负责将日志消息写入指定的数据存储目标，无论是文件、数据库、电子邮件地址还是系统日志。它通过 `Zend_Log` 对象的 `add()` 方法进行附加。一个 `Zend_Log` 对象可以附加多个写入器。表 8-2 显示了 Zend Framework 包含的内置写入器列表。

- `Zend_Log_Formatter` 对象负责对日志消息进行重新格式化，将其转换为 XML 或用户定义的格式。它始终与写入器相关联，并通过写入器的 `setFormatter()` 方法进行附加。每个写入器只允许一个格式化器。表 8-3 提供了 Zend Framework 包含的内置格式化器列表。

**图 8-6** 写入文件的示例日志消息

| Writer | Description |
| --- | --- |
| `Zend_Log_Writer_Stream` | 将日志消息写入 PHP 流（输出设备、错误设备、URL 或本地文件） |
| `Zend_Log_Writer_Db` | 将日志消息写入数据库 |
| `Zend_Log_Writer_Firebug` | 将日志消息写入 Firebug 控制台 |
| `Zend_Log_Writer_Mail` | 将日志消息写入电子邮件地址 |
| `Zend_Log_Writer_Mock` | 为了测试目的将日志消息写回自身 |
| `Zend_Log_Writer_Null` | 将日志消息写入 `/dev/null` |
| `Zend_Log_Writer_Syslog` | 将日志消息写入系统记录器（UNIX 上的 syslog 和 Windows 事件查看器） |

**表 8-2** Zend Framework 包含的日志写入器

注意传递给 `Zend_Log` 对象的 `log()` 方法的第二个参数。该参数指定消息优先级，可以是八个预定义优先级级别中的任何一个。这些级别列在表 8-4 中，并与 UNIX 系统记录器（syslog）使用的级别对应。开发者可以根据日志消息的重要性为每条消息指定级别。

要将日志写入数据库而不是文件（在日志并发性较高时推荐），请使用 `Zend_Log_Writer_Db` 写入器。该写入器的初始化需要一个 `Zend_Db_Adapter` 类的实例（代表要使用的数据库连接）、目标表以及一个指定用于日志消息不同元素的字段数组。以下是一个示例：

```php
class Sandbox_ExampleController extends Zend_Controller_Action
{
    public function logAction()
    {
        // initialize logging engine
        $logger = new Zend_Log();

        // define database mapping
    }
}
```

| Formatter | Description |
| --- | --- |
| `Zend_Log_Formatter_Simple` | 将日志消息格式化为自定义格式 |
| `Zend_Log_Formatter_Firebug` | 为 Firebug 控制台格式化日志消息 |
| `Zend_Log_Formatter_Xml` | 将日志消息格式化为 XML |




### 表 8-3 Zend Framework 包含的日志格式化器

| Log Level | Description |
| --- | --- |
| DEBUG | 调试通知 |
| INFO | 信息通知 |
| NOTICE | 通知 |
| WARNING | 警告通知 |
| ERR | 错误通知 |
| CRIT | Critical错误通知 |
| ALERT | 警告通知 |
| EMERG | 紧急错误通知 |

### 表 8-4 Zend_Log 组件支持的日志级别

```php
$table = 'log';
$fields = array(
  'LogLevel' => 'priority',
  'LogMessage' => 'message',
  'LogTime' => 'timestamp'
);

// attach writer to logging engine
$writer = new Zend_Log_Writer_Db($this->adapter, $table, $fields);
$logger->addWriter($writer);

// write log message
$logger->log('Body temperature critical', Zend_Log::EMERG);
```

## 注意

数据库日志写入器无法配合格式化器使用。尝试这样做会导致异常异常。

还可以使用 `Zend_Log_Writer_Mail` 写入器将消息写入电子邮件地址，该写入器接受一个配置过的 `Zend_Log_Writer_Mail`。如下所示：

```php
class Sandbox_ExampleController extends Zend_Controller_Action
{
    public function logAction()
    {
        // initialize logging engine
        $logger = new Zend_Log();

        // define database mapping
        $mail = new Zend_Log_Writer_Mail();
        $mail->setFrom('error@example.com');
        $mail->addTo('admin@example.com');
        $mail->setSubject('Log Error');
        $logger->addWriter($mail);

        // write log message
        $logger->log('Body temperature critical', Zend_Log::EMERG);
    }
}
```

## Zend Framework：入门指南

默认的格式字符串包含时间戳、日志级别（包括数字和字符串形式）以及日志消息。然而，可以修改此格式并重新排列项以适应特定的应用程序需求。为了说明，这里有另一个示例，它通过 `setEventItem()` 方法使用了额外的键值：

```php
class SandboxExampleController extends ZendController_Action
{
    public function logAction() {
        // 初始化日志引擎
        $logger = new Zend_Log();

        // 将写入器附加日志引擎
        $writer = new Zend_Log_Writer_Stream(APPLICATION_PATH . '/../data/logs/example.log');
        $logger->addWriter($writer);

        // 将格式化器附加写入器
        $format = '%timestamp%% %priorityName%% %request%%'; PHP_EOL;
        $formatter = new Zend_Log_Formatter_Simple($format);
        $writer->setFormatter($formatter);

        // 将客户端 IP 和请求 URL 添加日志消息
        $logger->setEventItem('request', $this->getRequest()->getRequestUri());
        $logger->setEventItem('host', $this->getRequest()->getClientIp());

        // 写入日志消息
        $logger->log('Body temperature critical', Zend_Log::EMERG);
    }
}
```

8-7 图展示了上述列表的可能输出。

### 注意

当使用 `Zend_Log_Formatter_Simple` 格式化器时，通过 `setWidgetItem` 方法指定的额外键默认不会写入日志。要将这些项包含在日志中，请在传递给格式化器的格式字符串中明确包含它们。

![](img/222e7e58871b088cc6397852e1452b57_278_0.png)

图 8-7 带有额外信息的日志消息示例

## 第 8 章：日志记录与异常调试

要以 XML 格式而非纯文本格式记录数据，请如下切换到 `Zend_Log_Formatter_Xml` 格式化器：

```php
<?php
class Sandbox_ExampleController extends Zend_Controller_Action
{
    public function logAction()
    {
        // 初始化日志引擎
        $logger = new Zend_Log();

        // 将写入器附加日志引擎
        $writer = new Zend_Log_Writer_Stream(
            APPLICATION_PATH . '/../data/logs/example.log');
        $logger->addWriter($writer);

        // 将格式化器附加写入器
        $formatter = new Zend_Log_Formatter_Xml();
        $writer->setFormatter($formatter);

        // 将客户端 ID 和请求添加到日志消息
        $logger->setItemItem('request', $this->getRequest()->getRequestUri());
        $logger->setItemItem('host', $this->getRequest()->getClientIp());

        // 写入日志消息
        $logger->log('Body temperature critical', Zend_Log::EMERGENCY);
    }
}
```

在这种情况下，消息被格式化为 XML 条目，适用于任何 XML 处理器解析。与 `Zend_Log_Formatter_Simple` 格式化器一样，可以通过指定不同的元素名称来自定义输出 XML。这些信息应该作为数组传递给 `Zend_Log_Formatter_Simple` 构造函数。这里是一个说明此功能的示例：

```php
<?php
class Sandbox_ExampleController extends Zend_Controller_Action
{
    public function logAction()
    {
        // 初始化日志引擎
        $logger = new Zend_Log();

        // 将写入器附加日志引擎
        $writer = new Zend_Log_Writer_Stream(
            APPLICATION_PATH . '/../data/logs/example.log');
        $logger->addWriter($writer);

        // 设置 XML 元素配置
        $xml = array(
            'data' => 'message',
            'time' => 'timestamp',
            'level' => 'priorityName',
            'request' => 'request',
            'host' => 'host',
        );

        // 将格式化器附加写入器
        $formatter = new Zend_Log_Formatter_Xml('entry', $xml);
        $writer->setFormatter($formatter);

        // 将客户端 IP 和请求 URI 添加日志消息
        $logger->setEventItem('request', $this->getRequest()->getRequestUri());
        $logger->setEventItem('host', $this->getRequest()->getClientIp());

        // 写入日志消息
        $logger->log('Body temperature critical', Zend_Log::EMERG);
    }
}
```

图 8-8 显示了修订后的输出示例。

图 8-8 以 XML 格式化的日志消息示例

图 8-9 使用自定义元素名称以 XML 格式化的日志消息示例

## 第 8 章：日志记录与异常调试

### 尝试此：8-2 日志记录异常

现在，让我们通过更新 SQUARE 应用以一个完整的异常日志系统，将所有信息应用于实际场景。该系统会将异常数据记录到文件、数据库和 Firefox 控制台。正如你所看到的，这实际上非常简单，可以相对容易地完成。后续章节将引导你完成这一过程。

> **注意** 接下来的章节包含了关于如何将异常数据记录到 Firefox（浏览器调试器）的讨论。这假设你已经安装了可以正常工作的 Firefox 浏览器，以及 Firefox 和 FirePHP 扩展。如果你还没有这些组件，可以从章节末尾的链接从网上下载。

### 定义日志位置

第一步是为文件定义位置。在你的项目根目录下创建一个 `logs` 目录：

```bash
mkdir logs
```

### 定义数据库写入器

下一步是创建一个与数据库集成的写入器。这是通过扩展 `Zend_Log_Writer_Abstract` 类实现的：

```php
<?php
class Square_Log_Writer_Doctrine extends Zend_Writer_Abstract
{
    /**
     * 接收模型名和列映射
     */
    public function __construct($modelName, $columnMap)
    {
        $this->_modelName = $modelName;
        $this->_columnMap = $columnMap;
    }

    /**
     * 设置格式化器
     */
    public function setFormatter($formatter)
    {
        throw new Zend_Log_Exception('不支持 formatting');
    }

    /**
     * 主写入方法
     * 将消息映射到数据库
     */
    protected function _write($message)
    {
        $data = array();
        foreach ($this->_columnMap as $messageField => $modelField) {
            $data[$modelField] = $message[$messageField];
        }
        $model = new $this->_modelName();
        $model->fromArray($data);
        $model->save();
    }

    /**
     * 工厂方法
     */
    public static function factory($config)
    {
        return new self($config['modelName'], $config['columnMap']);
    }
}
```

将此类保存为 `library/Square/Log/Writer/Doctrine.php`。该类基于 Matthew Lurz 在 Zend Framework wiki 上创建的原型（参见章节末尾的链接）。它的核心是 `_write()` 方法，它初始化 Doctrine 模型并填充数据。然后使用模型的 `save()` 方法将日志消息写入数据库。

### 更新错误控制器

现在只需更新 `ErrorController::errorAction`，使其自动记录到文件和 Firefox 控制台。以下是修改后的 `application/modules/default/controllers/ErrorController.php`，修改部分已高亮：

```php
<?php
class ErrorController extends Zend_Controller
{
  public function errorAction()
  {
    $errors = $this->getParam('error_handler');
    switch ($errors->type) {
      case Zend_Controller_Plugin_ErrorHandler::EXCEPTION_NO_CONTROLLER:
      case Zend_Controller_Plugin_ErrorHandler::EXCEPTION_NO_ACTION:

        // 404 错误 - 未找到控制器或动作
        $this->getResponse() ->setStatusCode(404);
        $this->view->title = 'Page Not Found';
        $this->view->message = 'The requested page could not be found.';
        break;
      default:
        // 应用错误
        $this->getResponse() ->setStatusCode(500);
        $this->view->title = 'Internal Server Error';
        $this->view->message = 'Due to an application error, the requested page could not';
    }
  }
}
```

## 266 Zend Framework：学者指南

'被显示。'

```php
break;

$this->view->exception = $errors->exception;
$this->view->request = $errors->request
```

```php
// 初始化日志引擎
$logger = new Zend_Log();

// 添加 XML 写入器
$config = $this->getInvokeArg('bootstrap')->getOption('logs');
$xmlWriter = new Zend_Log_Writer_Stream($config['logPath'] . '/error.log.xml');
$logger->addWriter($xmlWriter);
$formatter = new Zend_Log_Formatter_Xml();
$xmlWriter->setFormatter($formatter);
```

```php
// 添加 Doctrine 写入器
$columnMap = array(
'message' => 'LogMessage',
'priority' => 'LogLevel',
'timestamp' => 'LogTime',
'stacktrace' => 'Stack',
'request' => 'Request',
);

$dbWriter = new Square_Log_Writer_Doctrine('Square_Model_Log', $columnMap);
$logger->addWriter($dbWriter);
```

```php
// Firebug 写入器
$fbWriter = new Zend_Log_Writer_Firebug();
$logger->addWriter($fbWriter);
```

```php
// 日志消息的额外数据 - 堆栈跟踪和请求参数
$logger->setEvent('stacktrace',
$errors->exception->getTraceAsString());
$logger->setEvent('request',
Zend_Debug::dump($errors->request->getParams()));
```



```php
// 将异常写入器
$logger->log($errors->exception->getMessage(), Zend_Log::ERR);
```

这段代码初始化了`Zend_Log`组件的实例，并为其附加了三个写入器：标准文件写入器、在前节中创建的`Doctrine`数据库写入器，以及`Firebug`控制台。`Zend_Log`对象的`setTimeout`方法用于向日志消息中添加两个额外信息，即异常的堆栈跟踪和请求参数列表。由于这些修改，任何冒泡到`ErrorController::action`的异常将自动记录到三个不同的目的地。

图 8-10 一个应用程序异常，以 XML 格式记录到文件中

要查看此效果，请尝试访问一个不存在的应用程序 URL，例如`http://localhost/no/such/resource`。将抛出一个异常到错误控制器，并向请求客户端返回 404 响应。此异常也将记录到文件中（图 8-10）、应用程序数据库（图 8-11）以及`Firebug`控制台（图 8-12）。

图 8-11 一个应用程序异常，记录到应用程序数据库

（续）

## 268 Zend Framework：学者指南

![](img/222e7e58871b088cc6397852e1452b57_286_0.png)

> **注意**
>
> 需要注意的是，正如本节讨论的，在生产环境中并不建议将异常记录到三个不同的目的地。由于文件锁定或网络延迟等问题，将数据记录到文件或数据库可能会影响性能，而将数据记录到`Firebug`控制台则会增加服务器发送给客户端的数据包大小。为 Zend Framework 应用程序添加日志功能时，必须仔细研究这些及其他性能问题。

### 总结

本章标志着本书第一部分的结束，该部分旨在教你使用 Zend Framework 进行基础应用程序开发技术。恰好，它涵盖了异常处理，这是应用程序开发的重要部分，也是每个开发者都应该熟悉的领域。

本章从介绍 PHP 5.x 引入的新异常模型开始，概述了其相对于较旧的 PHP 4.x 模型的优势。在有了这些背景信息后，接着检查了 Zend Framework 内置的默认异常处理系统，概述了默认错误控制器的功能，并研究了如何调整默认流程以适应不同情况。它还简要看了如何根据应用程序运行在开发环境还是生产环境中（以及应该）修改异常处理，并演示了自定义错误页的实际应用。

## 第 8 章：异常的记录与调试

本章的后半部分专门关注`Zend/Log`组件，它为 Zend Framework 应用程序中的消息记录提供了一个功能框架。该组件可以将消息记录到各种不同的存储介质，包括文件、数据库、电子邮件地址、系统日志记录器和`Firebug`控制台，它还可以扩展以支持新的日志目的地。这些功能中的一些已经在实际上下文中进行了演示，通过向 SQUARE 示例应用程序添加异常日志代码。如需了解更多本章讨论的主题，请考虑访问以下链接：

- PHP 5.x 中异常和异常处理的概述，访问：<http://www.php.net/manual/en/language.exceptions.php>
- Zend Framework 中异常和异常处理的概述，访问：<http://framework.zend.com/manual/en/zend.controller.exceptions.html>
- Zend Framework 错误处理器插件，访问：<http://framework.zend.com/manual/en/zend.controller.plugins.html>
- `Zend_Log`组件，访问：<http://framework.zend.com/manual/en/zend.log.html>
- `Zend_Debug`组件，访问：<http://framework.zend.com/manual/en/zend.debug.html>
- Firefox Web 浏览器，访问：<http://www.mozilla.com/firefox>
- PHP 5.x 中异常和异常处理的概述，访问：<http://www.php.net/manual/en/language.exceptions.php>
- Zend Framework 中异常和异常处理的概述，访问：<http://framework.zend.com/manual/en/zend.controller.exceptions.html>
- Zend Framework 错误处理器插件，访问：<http://framework.zend.com/manual/en/zend.controller.plugins.html>
- `Zend_Log`组件，访问：<http://framework.zend.com/manual/en/zend.log.html>
- `Zend_Debug`组件，访问：<http://framework.zend.com/manual/en/zend.debug.html>
- Firefox Web 浏览器，访问：<http://www.mozilla.com/firefox>
- 关于`firephp`和 Zend framework 的讨论，访问：<http://christoph.com/2008/02/firephp-and-zend-framework>
- 关于 Zend framework 中处理错误的讨论，访问：<http://utopia.net/2009/03/handling-errors-in-zend-framework>
- 更高级的 Zend Framework 异常，访问：<http://code.google.com/p/zend-framework-exception>
- Doctrine 写入器的原始提案和源码，访问：<http://framework.zend.com/wiki/Zend_Log_Writer_Doctrine>
- Doctrine 写入器，Matthew Lurz

本页留白

## 第 9 章：理解应用程序本地化

## Zend Framework：学者指南

### 关键技能与概念

- 将应用程序本地化到全球不同地区
- 自动应用日期、货币、衡量的本地习惯
- 构建多语言应用程序

### 理解本地化与区域

全球化专家们往往认为世界正在变成一个日益同质的地方，但实际上，每个国家仍然具有独特的身份和文化习俗。这些差异既存在感知层面——例如，意大利人被认为对时尚非常敏锐，而法国人是美食之国——也存在更平庸的文化产物中，如语言、货币、计量等。例如，在美国，2011年7月4日的写法是 7/4/2011，而在印度，日期将表示为 4/7/2011。同样，德国、法国、意大利、印度等许多国家以公里表示距离，而在美国则以英里表示。

本地化是使应用程序适配到特定的地理区域、国家和/或语言的过程。这可能仅仅是确保日期、时间和货币以符合所选区域的正确格式显示，也可能复杂——此处文本截断了。

## 第 9 章：理解应用本地化 273

即将将应用程序标签、菜单和消息翻译成该地区的本地语言。其原理很简单：应用程序越“本地化”，不同地区的用户就越容易理解和使用它。大多数流行的 Web 应用程序将此视为家常便饭：为了说明，请参考图 9-1，它显示了 Google 搜索引擎在世界上三个不同国家的界面：美国、法国和印度。

本地化过程的核心概念是语言区域（locales）和区域标识符（locale identifiers）。区域标识符是一个表示用户语言和地理区域的字符串。该标识符由一个语言代码和一个国家代码组成并用下划线分隔。此标识符旨在为应用程序提供有关用户当前位置和语言的精确信息，从而使其能够按照该位置和语言的惯例展示其信息。

一个例子会让这一点更清晰。例如，考虑一个设置为区域`en_US`（语言：英语，国家：美国）的应用程序。如果应用程序具有区域感知能力，它将使用这些信息来确保例如日期以`MM-DD-YYYY`格式显示，并在货币前加上美元（$）符号。如果应用程序被重新配置为区域`de_AT`（语言：德语，国家：奥地利），它会自动执行必要的内部调整，以`DD-MM-YYYY`格式显示日期并在货币前加上欧元（€）符号。

![](img/222e7e58871b088cc6397852e1452b57_291_0.png)

## 274 Zend Framework：入门指南

| 区域 | 语言 | 国家 |
|---|---|---|
| `en_US` | 英语 | 美国 |
| `en_GB` | 英语 | 英国 |
| `fr_FR` | 法语 | 法国 |
| `fr_CA` | 法语 | 加拿大 |
| `fr_BE` | 法语 | 比时 |
| `fr_CH` | 法语 | 瑞士 |
| `de_DE` | 德语 | 德国 |
| `it_IT` | 意大利语 | 意大利 |
| `es_ES` | 西班牙语 | 西班牙 |
| `es_US` | 西班牙语 | 美国 |
| `cs_CZ` | 捷克语 | 捷克共和国 |
| `hi_IN` | 印地语 | 印度 |
| `mr_IN` | 马拉地语 | 印度 |
| `en_IN` | 英语 | 印度 |
| `pt_BR` | 葡萄牙语 | 巴西 |
| `zh_CN` | 中文 | 中国 |

**表 9-1** 常见区域标识符

表 9-1 提供了常见区域标识符的列表，以及它们所代表的语言和国家的描述。

> **注意（NOTE）**
>
> 在区域标识符中找到语言代码完整列表可以在 ISO 639 标准中找到，而相应的国家代码列表可以在 ISO 3166 标准中找到。你将在章节末找到这些标准的链接。

### 设置应用区域

Zend Framework 包含一个名为`Zend_Locale`的组件，用于定义应用程序的区域。该组件可以手动设置应用程序区域，也可以通过运行时的自动检测过程设置。以下是手动将区域设置为`fr_FR`（语言：法语，国家：法国）的示例：

```php
<?php
class Sandbox_ExampleController extends Zend_Controller_Action
{
    public function localeAction()
    {
        $locale = new Zend_Locale('fr_FR');
    }
}
```

## 第 9 章：理解应用本地化 275

区域标识符的各个组件可以通过`Zend_Locale`对象的`getLanguage()`和`getRegion()`方法获取，如下：

```php
<?php
class SandboxExampleController extends Zend_Controller_Action
{
    public function localeAction()
    {
        // 定义区域
        $locale = new Zend_Locale('fr_BE');

        // 结果：'fr'
        $this->view->message = $locale->getLanguage();

        // 结果：'BE'
        $this->view->message = $locale->getRegion();
    }
}
```

通常，`Zend_Locale`对象在应用引导（bootstrap）中初始化，并通过应用注册表（registry）持久化。一旦以这种方式注册，其他区域感知的 Zend Framework 组件（如`Zend_Date`和`Zend_Form`）将自动读取所选区域并调整自身以按照该区域的惯例显示信息。这是一个示例示例，你将在整个章节中多次看到它。

```php
<?php
class Bootstrap extends Zend_Application_Bootstrap_Bootstrap
{
    protected function initLocale()
    {
        // 定义区域
        $locale = new Zend_Locale('fr_FR');

        // 注册区域
        $registry = Zend_Registry::getInstance();
        $registry->set('Zend_Locale', $locale);
    }
}
```

除非你确定应用程序将只在一个区域使用，否则不建议在设计时手动设置应用区域。`Zend_Locale`包含一个自动区域检测功能，可以在检查以下信息源后在运行时动态设置区域：

- **客户端环境设置**：大多数 Web 客户端允许用户选择查看 Web 页面时的首选语言和区域。在 PHP 应用中可以通过`$_SERVER['HTTP_ACCEPT_LANGUAGES']`数组访问这些信息。当这些信息可用时，`Zend_Local`将使用它们来自动设置应用区域。（此处注：由于原始文本存在大量 OCR 重复和错误，此处已根据逻辑流进行了清理和翻译。）

# 278 Zend Framework：学者指南

```php
public function numberAction()
{
    // 格式化数字
    // result: '195,740.676'
    $this->view->message = Zend_Locale_Format::toNumber(195740.676, array('locale' => 'en_GB'));
}
```

```php
// result: '195,740.676'
$this->view->message = Zend_Locale_Format::toNumber(
    195740.676, array('locale' => 'en_GB');
);
```

值得注意的是，与`Zend_Date`和`Zend_Currency`不同，`Zend_Locale_Format`无法从注册表（registry）直接获取应用 locale。因此，必须将 locale 标识作为参数传递给`toNumber()`方法。

还可以通过指定自定义格式和精度来自定义输出。这些选项可以通过选项数组传递给`toNumber()`方法。以下是一些示例：

```php
<?php
class SandboxExampleController extends Zend_Controller_Action
{
    public function numberAction()
    {
        // 使用自定义数字格式
        // result: '1,95,740.67'
        $this->view->message = Zend_Locale_Format::toNumber(195740.676, array(
            'locale' => 'en_GB',
            'number_format' => '##,##.00'
        ));
    }
}
```

`Zend_Locale_Format`组件中的另一个方法是静态方法`convertNumerals()`，它允许在阿拉伯数字脚本和拉丁脚本之间进行转换。这要求 PHP 的 PCRE 引擎在编译时支持 UTF-8（Windows 上的 PHP 安装通常缺少此支持）。以下是它的用法示例：

```php
<?php
class SandboxExampleController extends Zend_Controller_Action
{
    public function numberAction()
    {
        // 转换数字脚本
        $this->view->message = Zend_Locale_Format::convertNumerals('1956', 'Latn', 'Thai');
        $this->view->message = Zend_Locale_Format::convertNumerals('6482093.6498', 'Latn', 'Deva');
    }
}
```

## 第 9 章：理解应用本地化

> **提示**
>
> 通过调用`Zend_Locale::getTranslationList('script')`可以获取`Zend_Locale_Format::convertNumerals`支持的所有数字脚本列表。

### 本地化日期和时间

Zend Framework 带了一个专门用于处理时间显示和操作的组件。该组件`Zend_Date`提供了一个简单的 API 来创建和格式化日期与时间值；它还支持通过 PHP 内置的`mtime()`函数更广泛的时间戳，并且可以自动检测应用 locale（如果通过`Zend_Locale`设置），并根据该 locale 的惯例展示日期和时间值。

以下是`Zend_Date`运行的一个简单示例：

```php
<?php

class Sandbox_ExampleController extends Zend_Controller_Action
{
    public function dateAction()
    {
        // 将日期设置为当前
        $date = new Zend_Date();

        // result: 'Dec 18, 2009 5:58:38 AM'
        $this->view->message = $date;
    }
}
```

如这些示例所示，`Zend_Date`对象会自动初始化为当前日期和时间。也可以通过向构造函数传递人类可读的日期字符串、UNIX 时间戳或日期/时间段数组来初始化为特定的日期和时间。以下是一些示例：

```php
<?php

class Sandbox_ExampleController extends Zend_Controller_Action
{
    public function dateAction()
    {
        // 使用 UNIX 时间戳设置日期
        $date = new Zend_Date(1261125725);

        // result: '2009-12-18T08:42:05+00:00'
```



```php
$this->view->message = $date->get(Zend_Date::ISO_8601);

// 使用字符串设置日期

// result: '2010-12-25T15:56:00+00:00'

$date->set('25/12/2010 15:56');

$this->view->message = $date->get(Zend_Date::ISO_8601);

// 使用数组设置日期

// returns '2010-06-24T16:35:00+00:00'

$date->set(
    array(
        'year' => 2010,
        'month' => 6,
        'day' => 24,
        'hour' => 16,
        'minute' => 35,
        'second' => 0
    )
);

$this->view->message = $date->get(Zend_Date::ISO_8601);
```

### 注意

避免创建多个 `Zend_Date` 实例，因为每个实例都会产生显著的启动成本。因此，在需要多个实例的情况下，重用现有实例比实例化多个实例要高效得多。

如上一个示例所示，`Zend_Date` 包含了一set预定义的格式，例如 ISO8601 和 UNIX 时间戳。这些可以传递给 `get()` 方法来获取日期和时间。以下示例演示了这些用法：

```php
<?php
class Sandbox_ExampleController extends Zend_Controller_Action
{
    public function dateAction()
    {
        // 使用字符串设置日期
        $date = new Zend_Date('25/12/2010 15:56');
        $this->view->message = $date->get(Zend_Date::ISO_8601);

        // result: '2010-12-25T15:56:00+00:00'
        $this->view->message = $date->get(Zend_Date::ATOM);
    }
}
```

## 第 9 章：理解本地化

### 提示

如果预定义的格式不能满足你的需求，你也可以使用 `Zend_Date` 对象创建自定义格式。以下示例演示了这些场景：

```php
<?php
class Sandbox_ExampleController extends Zend_Controller_Action
{
    public function dateAction()
    {
        // 定义并注册 locale
        $locale = new Zend_Locale('fr_FR');
        $registry = Zend_Registry::getInstance();
        $registry->set('Zend_Locale', $locale);

        // 创建日期对象
        // locale 将自动检测
        $date = new Zend_Date();

        // result: 'vendredi 18 décembre 2009'
        $this->view->message = $date->get(Zend_Date::DATE_FULL);
    }
}
```

## 第 9 章：理解应用程序本地化

默认情况下，新实例化的 `Zend_Currency` 对象将检查应用程序是否包含已注册的 `Zend_Locale` 对象，如果是，它将在本地化货币值时使用此注册的区域。你也可以覆盖此行为，并显式地将区域作为参数传递给 `Zend_Currency` 构造函数。无论哪情况下，`Zend_Currency` 都会自动为该区域选择合适的货币。现在可以通过调用 `Zend_Currency` 对象的 `toCurrency()` 方法来获取本地化的货币值，该方法接受一个货币值作为参数。

考虑以下示例，它展示了实际操作中的用法：

```php
<?php
class SandboxExampleController extends Zend_Controller_Action
{
    public function currencyAction()
    {
        // 初始化货币对象
        $currency = new Zend_Currency('fr_FR');

        // 结果: '990,65 €'
        $this->view->message = $currency->toCurrency(990.65);
    }
}
```

### 注意

当你向 `Zend_Currency` 传递区域标识符时，必须包含语言代码和区域代码。遗漏这两个代码中的任何一个都会导致异常，因为 `Zend_Currency` 需要完整的区域标识符来正确识别对应的货币。

对于拥有多种货币的区域，或者为了覆盖默认的货币选择，`Zend_Currency` 构造函数接受一个货币代码作为额外的可选参数。这里是一个示例：

```php
<?php
class SandboxExampleController extends Zend_Controller_Action
{
    public function currencyAction()
    {
        // 初始化货币对象
        $currency = new Zend_Currency('fr_FR', 'FRP');

        // 结果: '990,65 F'
        $this->view->message = $currency->toCurrency(990.65);
    }
}
```

## 284 Zend Framework：入门指南

### 备注

货币代码的完整列表可以在 ISO 4217 标准中找到。你将在本末尾找到指向该标准的链接。

还可以使用 `setFormat()` 方法自定义 `Zend_Currency` 返回的货币字符串，以调整货币符号的位置、货币名称、数字精度以及三位货币代码的可见性。该方法接受一个键值对数组并相应地重新格式化货币字符串。以下示例说明了这一点：

```php
<?php
class Sandbox_ExampleController extends Zend_Controller_Action
{
    public function currencyAction()
    {
        // 初始化货币对象
        $currency = new Zend_Currency('hi_IN');

        // 调整货币格式
        $currency->setFormat(
            array(
                'position' => Zend_Currency::RIGHT,
                'display' => Zend_Currency::USE_NAME,
                'precision' => 2,
            )
        );

        // 结果: '990.65भारतीय रुपया'
        $this->view->message = $currency->toCurrency(990.65);

        // 创建自定义货币格式
        $currency->setFormat(
            array(
                'position' => Zend_Currency::LEFT,
                'display' => Zend_Currency::USE_SYMBOL,
                'precision' => 4,
                'name' => 'Driit',
                'symbol' => 'DRT'
            )
        );

        // 结果: 'DRT 990.6500'
        $this->view->message = $currency->toCurrency(990.65);
    }
}
```

## 第 9 章：理解应用程序本地化

### 提示

`Zend_Currency` 包含了在本地化货币值之前对其进行汇率转换的能力。或者，可以考虑 PEAR Services_ExchangeRates 包，它提供了一个 API，用于使用当前汇率执行实时货币转换。你将在本末尾找到包含更多信息的链接。

## 量的本地化

重量和度是另一个经常需要本地化的领域，Zend Framework 在这里也有解决方案：`Zend_Measure`，这是一个旨在帮助在不同测量单位之间转换并根据本地习惯展示的组件。该组件支持超过 30 种不同的测量类型，从长度、重量、体积和温度等常见类型，到加速度、照度、功率、频率和能量等不常见的类型。

要初始化一个 `Zend_Measure` 对象，需要向对象构造函数传递两个参数：一个数值测量值和一个表示其所用尺度的常量。考虑以下示例，它通过创建一个 `Zend_Measure_Temperature` 来说明：

```php
<?php
class Sandbox_ExampleController extends Zend_Controller_Action
{
    public function measureAction()
    {
        // 初始化测量对象
        $tempF = new Zend_Measure_Temperature(
            98.6,
            Zend_Measure_Temperature::FAHRENHEIT
        );

        // 结果: '98.6 °F'
        $this->view->message = $tempF;
    }
}
```

这是另一个示例，它创建了 `Zend_Measure_Length` 和 `Zend_Measure_Weight` 对象：

```php
<?php
class Sandbox_ExampleController extends Zend_Controller_Action
{
    public function measureAction()
    {
        // 初始化测量对象
        $lengthCm = new Zend_Measure_Length(
            2540,
            Zend_Measure_Length::CENTIMETER
        );

        // 结果: '2,540 cm'
        $this->view->message = $lengthCm;
    }
}
```

## 286 Zend Framework：入门指南

`Zend_Measure` 暴露了一个 `convertTo()` 方法，用于将一种测量单位转换为另一种。这里是一些说明此点的示例：

```php
<?php
class Sandbox_ExampleController extends Zend_Controller_Action
{
    public function measureAction()
    {
        // 初始化测量对象
        $tempF = new Zend_Measure_Temperature(
            98.6,
            Zend_Measure_Temperature::FAHRENHEIT
        );

        // 结果: '98.6 °F'
        $this->view->message = $tempF;
    }
}
```

```php
<?php
class Sandbox_ExampleController extends Zend_Controller_Action
{
    public function measureAction()
    {
        // 初始化测量对象
        $lengthCm = new Zend_Measure_Length(
            2540,
            Zend_Measure_Length::CENTIMETER
        );

        // 结果: '2,540 cm'
        $this->view->message = $lengthCm;
    }
}
```

```php
<?php
class Sandbox_ExampleController extends Zend_Controller_Action
{
    public function measureAction()
    {
        // 初始化测量对象
        $weightKg = new Zend_Measure_Weight(
            6500,
            Zend_Measure_Weight::KOGRAM
        );

        // 结果: '6,500 kg'
        $this->view->message = $weightKg;
    }
}
```

### 注意

当你向 `Zend_Currency` 传递区域标识符时，必须包含语言代码和区域代码。遗漏这两个代码中的任何一个都会导致异常，因为 `Zend_Currency` 需要完整的区域标识符来正确识别对应的货币。

对于拥有多种货币的区域，或者为了覆盖默认的货币选择，`Zend_Currency` 构造函数接受一个货币代码作为额外的可选参数。这里是一个示例：

```php
<?php
class SandboxExampleController extends Zend_Controller_Action
{
    public function currencyAction()
    {
        // 初始化货币对象
        $currency = new Zend_Currency('fr_FR', 'FRP');

        // 结果: '990,65 F'
        $this->view->message = $currency->toCurrency(990.65);
    }
}
```

## 第 9 章：理解应用程序本地化

```php
<?php
class Sandbox_ExampleController extends Zend_Controller_Action
{
    public function measureAction()
    {
        // 初始化测量对象
        $tempF = new Zend_Measure_Temperature(
            98.6,
            Zend_Measure_Temperature::FAHRENHEIT
        );

        // 结果: '98.6 °F'
        $this->view->message = $tempF;
    }
}
```

```php
<?php
class Sandbox_ExampleController extends Zend_Controller_Action
{
    public function measureAction()
    {
        // 初始化测量对象
        $lengthCm = new Zend_Measure_Length(
            2540,
            Zend_Measure_Length::CENTIMETER
        );

        // 结果: '2,540 cm'
        $this->view->message = $lengthCm;
    }
}
```

```php
<?php
class Sandbox_ExampleController extends Zend_Controller_Action
{
    public function measureAction()
    {
        // 初始化测量对象
        $weightKg = new Zend_Measure_Weight(
            6500,
            Zend_Measure_Weight::KOGRAM
        );

        // 结果: '6,500 kg'
        $this->view->message = $weightKg;
    }
}
```

### 字符串

虽然你最可能是在 Web 上，但请记住，仍有很大比例的 Internet 用户英语不是他们的母语。这一事实在本地化 Web 应用程序时具有特殊的意义，任何本地化项目最大的部分是将应用程序的文本内容翻译成多种语言。

Zend Framework 提供了一个全面的 API 来管理不同语言的翻译字符串，通过其 `Zend_Translate` 组件。该组件支持多种翻译源，包括 CSV 文件、PHP 数组、GNU gettext 文件，并可以扩展以支持其他数据源（例如，来自数据库的翻译字符串）。与本章讨论的其他组件一样，它是完全感知区域的，并根据已注册的 `Zend_Locale` 对象或客户端区域设置动态地选择应用程序所需的语言。

## 288 Zend Framework：初学者指南

这是翻译文件最简单的格式，由一个 PHP 关联数组组成，其键映射对应的本地语言字符串。`Zend_Translate` 现在可以配置为读取这些文件，并根据所选区域在运行时动态翻译字符串。以下是一个示例：



```php
<?php
class SandboxExampleController extends Zend_ControllerAction
{
    public function translateAction()
    {
        // 创建翻译对象
        // 指定翻译适配器
        // 为每个区域指定源文件
        $translate = new Zend_Translate('array', APPLICATION_PATH . 
            '../languages/messages.es.php', 'es_ES');
        $translate->addTranslation(APPLICATION_PATH . 
            '../languages/messages.de.php', 'de_DE');
        $translate->addTranslation(APPLICATION_PATH . 
            '../languages/messages.fr_FR.php', 'fr_FR');

        // 设置当前区域
        $translate->setLocale('fr_FR');

        // 翻译字符串
        // 结果: 'un, deux, trois'
        $this->view->message = sprintf('%s, %s, %s', 
            $translate->translate('one'), 
            $translate->translate('two'), 
            $translate->translate('three')
        );

        // 设置当前区域
        $translate->setLocale('de_DE');

        // 翻译字符串
        // 结果: 'eins, zwei, drei'
        $this->view->message = sprintf('%s, %s, %s', 
            $translate->translate('one'), 
            $translate->translate('two'), 
            $translate->translate('three')
        );
    }
}
```

## 第 9 章：理解应用程序本地化 289

`Zend_Translate` 对象初始化时需要三个参数：使用的翻译适配器类型、翻译源文件的位置以及文件的区域设置。`setLocale()` 方法用于定义当前区域。有了这些信息，`Zend_Translate` 能够查找适当的翻译文件并返回每个字符串的翻译。

> 提示
> 
> 如果 `Zend_Translate` 无法找到指定区域的翻译源，它将返回原始翻译键并生成 PHP 错误通知。要禁用此通知，请向 `Zend_Translate` 构造函数的第四参数传递特殊的 `'disableNotices'` 选项。

### 使用适配器和数据源

`Zend_Translate` 支持多种不同的翻译源文件适配器。之前的示例使用了 `Array` 适配器，它适用于许多场景。然而，其他其他选项，如表 9-2 所示。

`Zend_Translate` 还可以递归扫描目录树，并通过自动检测过程将找到的所有翻译源附加到 `Zend_Translate` 对象上。每个翻译文件的区域根据相应的对应和/或目录名称自动检测。这消除了使用 `addTranslation()` 方法手动添加翻译源的需求。

| 适配器 | 描述 |
| :--- | :--- |
| `Zend_Translate_Adapter_Array` | 读取以 PHP 数组表示的翻译源 |
| `Zend_Translate_Adapter_Csv` | 读取以 CSV 格式表示的翻译源 |
| `Zend_Translate_Adapter_Ini` | 读取以 INI 格式表示的翻译源 |
| `Zend_Translate_Adapter_Gettext` | 读取以 GNU 二进制格式表示的翻译源 |
| `Zend_Translate_Adapter_Tbx` | 读取以 TermBaseXChange (TBX) 格式表示的翻译源 |
| `Zend_Translate_Adapter_Tmx` | 读取以 Translation Memory exchange (TMX) 格式表示的翻译源 |
| `Zend_Translate_Adapter_Qt` | 读取以 QtLinguistic 格式表示的翻译源 |
| `Zend_Translate_Adapter_Xiff` | 读取以 XML Localization Interchange File Format (XLIFF) 表示的翻译源 |
| `Zend_Translate_Adapter_XlTm` | 读取以 XML Text Memory (XML:TM) 格式表示的翻译源 |

表 9-2 Zend Framework 包含翻译适配器

为了说明，请考虑图 9-2，它展示了如何使用特定区域的目录作为翻译源，以及以下代码列表显示 `Zend_Translate` 自动扫描此目录结构并整合所有翻译源：

```php
<?php
class SandboxExampleController extends Zend_Controller_Action
{
    public function translateAction()
    {
        // 创建翻译对象
        // 为每个区域指定翻译源文件
        // 自动查找源文件
        $translate = new Zend_Translate('array', APPLICATION_PATH .
            '/../../languages', null,
            array('scan' => Zend_Translate::LOCALE_DIRECTORY));
    }
}
```

注意，在这种情况下，第二个参数仅仅是 `Zend_Translate` 对象构造函数要扫描的根目录，第四个参数表示应从每个目录的名称读取区域信息。

另一种方法是使用基于文件的结构，其中每个文件名确定了对应翻译源的区域标识符。图 9-3 展示了这样的系统，以下代码演示了如何配合 `Zend_Translate` 使用它：

```php
<?php
class SandboxExampleController extends Zend_Controller_Action
{
    public function translateAction()
    {
        // ... 基于文件的结构逻辑 ...
    }
}
```

### 使用应用程序区域

与其他许多 `Zend_Framework` 组件一样，`Zend_Translate` 是感知区域的：如果可用注册的 `Zend_Locale` 实例，它可以自动将此区域作为所有翻译操作的默认值。这非常方便，因为它允许在应用程序引导（bootstrap）中设置一次区域并应用于整个应用程序。

### 专家问答

问：什么是 GNU gettext？我该如何使用它？

答：GNU gettext 是 GNU 翻译项目的一部分，为应用程序创建和使用翻译表提供了一种标准方法。在该系统中，不同语言的翻译字符串指定在每种语言的可读消息模板 (*po) 文件中。这些文件被转换为二进制格式 (*mo) 文件，并随应用程序一起发布。

按照惯例，gettext 对 *.mo 使用基于目录的布局，不同语言的翻译文件存储在根据区域命名的独立目录中（图 9-4）。值得注意的是，`Zend_Translate` 的源检测功能可以自动识别并使用这种目录布局，从而允许开发者无需额外修改即可在 PHP 应用程序中使用现有的 gettext 源。

```php
<?php
// 定义并注册区域
$locale = new Zend_Locale('de_DE');
$registry = Zend_Registry::getInstance();
$registry->set('Zend_Locale', $locale);

// 创建翻译对象
$translate = new Zend_Translate('array', APPLICATION_PATH . '../languages/', null, array('scan' => Zend_Translate::LOCALE_FILENAME));
```

## 第 9 章：理解应用程序本地化 293

```php
$translate->_('two'),
$translate->_('three');

}
```

需要注意的是，如果 `ZendTranslate` 无法为完全限定的区域（locale）找到翻译源，它将自动对区域进行“降级”处理，并使用匹配降级后区域的翻译源。例如，如果应用程序区域设置为 `fr_LU`（语言：法语；国家：卢森堡），但没有 `fr_LU` 区域的翻译源，则 `Zend_Translate` 将自动使用 `fr` 区域的翻译源（如果可用）。

## 使用翻译视图辅助器（Translation View Helper）

之前章节中的示例演示了在控制器（controller）范围内的翻译操作。然而，实际上的方法是在视图脚本（view script）范围内执行翻译操作，而不是控制器中。`Zend_Translate` 包含一个翻译视图辅助器，可以在视图脚本中执行操作。

要使用翻译视图辅助器，必须将 `Zend_Translate` 对象注册到应用程序注册表（application registry）中，以便在整个应用程序中都可以访问。以下是这样做的示例：

```php
<?php
class Bootstrap extends Zend_Application_Bootstrap_Bootstrap
{
    protected function _initTranslate()
    {
        // 初始化并注册翻译对象
        $translate = new Zend_Translate('array',
            APPLICATION_PATH . '../languages/',
            null,
            array('scan' => Zend_Translate::LOCALE_FILENAME));
        $registry->set('Zend_Translate', $translate);
    }
}
```

一旦完成此操作，只需通过调用对象的 `translate()` 方法即可在视图脚本中执行翻译，如下代码所示。通过这种方式，翻译视图辅助器将在渲染视图之前检索相应的本地语言字符串并将其插值到视图脚本中。

```php
<div id="header">
<?php echo $this->translate('welcome'); ?>
</div>
```

## 294 Zend Framework：入门指南

一旦 `Zend_Translate` 对象已注册到应用程序注册表中，其他 Zend Framework 组件也可以使用它来get字符串本地化。这方面的最佳例子是 `Zend_Form`，它可以自动使用注册的 `Zend_Translate` 来准备本地化版本的表单字段和按钮标签、选项元素、字段集图例（fieldset legends）以及验证错误消息。你将在下一节中看到相关的示例。

## 尝试一下 9-1 本地化示例应用程序

如前面的章节所示，Zend Framework 为应用程序本地化提供了全面的 API。现在你已经了解了理论，让我们在实际场景中应用它，通过对 SQUARE 示例进行本地化来支持三种不同的语言：英语（包括英国和美国）、法语和德语。

### 设置应用程序区域

应用程序本地化的第一步是定义应用程序的区域。此区域信息可以被其他组件（如 `Zend_Date` 和 `Zend_Translate`）使用。推荐的方法是首先尝试从用户的客户端进行区域自动发现，如果失败，则手动将区域设置为一个合理的值。

通过编辑应用程序的引导文件（路径为 `$APP_DIR/application/Bootstrap.php`），并添加一个执行区域自动发现的方法，如下所示：

```php
<?php
class Bootstrap extends Zend_Application_Bootstrap_Bootstrap {
    protected function _initLocale() {
        try {
            $locale = new Zend_Locale('browser');
        } catch (Zend_Locale_Exception $e) {
            $locale = new Zend_Locale('en_GB');
        }
        $registry = Zend_Registry::getInstance();
        $registry->set('Zend_Locale', $locale);
    }
}
```

在这种情况下，`Zend_Locale` 将自动检测用户的当前区域，如果无法检测，它会将区域设置为 `en_GB`（语言：英语；国家：英国）。该区域将通过 `Zend_Registry` 注册到应用程序注册表中，以便其他感知区域的组件也能使用它。

### 本地化数字和日期

在完成区域定义后，下一步是检查应用程序并开始本地化数字和日期的过程。如果你查看邮票目录视图，你会发现每条邮票记录都包含一些数值：邮票的面值，以及邮票的最低和最高售价。理想情况下，这些值应该被格式化，以反映用户的本地习惯。

目前每个邮票详情页中缺失的另一个项目是其提供的日期。这对于潜在买家来说是有用的信息，因为这让他们能够判断列表有多“新”，此日期值也应该以用户的本地语言和习惯呈现。

`Zend_Format` 静态方法通过其静态方法 `toNumber()` 本地化数字的工具，而 `Zend_Date` 对象可以处理日期的本地化和格式化。要使用这些工具，请更新 `$APP_DIR/application/catalog/controllers/ItemController.php` 中的 `displayAction`，如下示例所示：

```php
<?php
class ItemController extends Zend_Controller {
    // 显示目录项的动作
    public function displayAction() {
        // 为 GET 输入设置过滤器和验证器
        $filters = array(
            'id' => array('HtmlEntities', 'StripTags', 'StringTrim'),
        );
        $validators = array('NotEmpty', 'Int');
        $input = new Zend_Filter_Input($filters, $validators);
        $input->setData($this->getRequest()->getParams());

        // 测试输入有效
        // 获取记录
        // 附加到视图
        if ($input->isValid()){
            $sq = Doctrine_Query::create()
                ->from('Square_Item', 'i')
                ->leftJoin('i', 'Square_Model_Country', 'c')
                ->leftJoin('i', 'Square_Model_Grade', 'g')
                ->leftJoin('i', 'Square_Model_Type', 't')
                ->where('i.RecordID = ?', $input->id)
                ->addWhere('i.DisplayStatus = 1')
                ->addWhere('i.DisplayUntil <= CURDATE()');
            $result = $sq->fetchArray();
            if (count($result) == 1) {
                $this->view->item = $result[0];
                $this->view->images = array();
                $config = $this->view('bootstrap')->getOption('uploads');
                foreach (glob("$config['uploadPath']{$this->view->item['RecordID']}_*") as $file) {
                    $this->view->images[] = basename($file);
                }
            } else {
                throw new Zend_Controller_Action_Exception('Page not found', 404);
            }
        } else {
            throw new Zend_Controller_Action_Exception('Invalid input');
        }
    }
}
```

（续）

## 296 Zend Framework：入门指南



```php
$configs = $this->getInvoke('bootstrap')->getOption('configs');
$localConfig = new Zend_Config_Ini($configs['localConfigPath']);
$this->view->seller = $localConfig->user->displayInfo();
$registry = Zend_Registry::getInstance();
$this->view->locale = $registry->get('Zend_Locale');
$this->view->recorddate = new Zend_Date($result[0]['RecordDate']);
```

在这里，`displayAction()` 方法从应用程序注册表中获取当前区域，它还获取记录并将其添加到 `Zend_Date` 对象中。现在可以在视图脚本中本地化这些日期和数字，如 `$APP_DIR/application/modules/catalog/views/scripts/item.php`：

```php
<h2>View Item</h2>
<h3>
FOR SALE:
<?php echo $this->escape($this->item['Title']); ?>
<?php echo $this->escape($this->item['Year']); ?>
<?php echo $this->escape($this->item['Square_Model_Grade'])['GradeName']); ?>
</h3>
<div id="container">
<div id="images">
<?php foreach ($this->images as $image) : ?>
<img src="uploads/<?php echo $this->escape($image); ?>" width="150" height="150" />
<?php endforeach; ?>
</div>
<div id="record">
<table>
<tr>
<td class="key">Denomination:</td>
<td class="value">
<?php echo $this->escape(
Zend_Locale_Format::toNumber($this->item['Denomination'],
array(
    'locale' => $this->locale,
    'precision' => 2
)); ?>
</td></tr>
</table>
</div>
</div>
```

## 第 9 章：理解应用本地化

```php
<table>
  <tr>
    <td class="key">等级：</td>
    <td class="value">
      <?php echo $this->escape($this->item['Square_Model_Grade']['GradeName']); ?> ?>
    </td>
  </tr>
  <tr>
    <td class="key">销售价格：</td>
    <td class="value">
      <?php echo $this->escape(
        Zend_locale_Format::toNumber($this->item['SalePriceMin'],
        array(
          'locale' => $this->locale,
          'precision' => 2
        )
      )); ?> - <?php echo $this->escape(
      Zend_locale_Format::toNumber($this->item['SalePriceMax'],
      array(
        'locale' => $this->locale,
        'precision' => 2
      )
    )); ?>
    </td>
  </tr>
  <tr>
    <td class="key">描述：</td>
    <td class="value">
      <?php echo $this->escape($this->item['Description']); ?> ?>
    </td>
  </tr>
  <tr>
    <td class="key">发布日期：</td>
    <td class="value">
      <?php echo $this->escape($this->recordDate(Zend_Date::DATE_FULL)); ?> ?>
    </td>
  </tr>
  <?php if ($this->seller == 1): ?>
  <tr>
    <td class="key">卖家：</td>
    <td class="value">
      <?php echo $this->escape($this->item['SellerName']); ?> ?,
      <?php echo $this->escape($this->item['SellerAddress']); ?> ?>
    </td>
  </tr>
  <?php endif; ?>
</table>
```

## Zend Framework：入门指南

### 定义字符串本地化目标

处理完日期和数字后，下一步是进行字符串本地化。由于本书的篇幅限制，无法对应用程序中的每个字符串进行本地化，因此，本文假设字符串本地化仅限于以下三个目标：应用程序的主菜单、页面页脚和联系表单。

要执行字符串本地化，需要编辑每个应用布局（layout）和视图（view），并使用翻译视图助手（translation view helper）动态地将字符串插值其中。一个好的起点是应用程序的主布局，它包含了主菜单。编辑此位于 `$APP_DIR/application/layouts/master.phtml` 的文件，并对**加粗**显示的部分进行修订：

```html
<!DOCTYPE html PUBLIC "//W3C//DTD HTML 1.0 Strict//EN"
"http://www.w3.org/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">

<div id="menu">
    <a href="<?php echo $this->url(array(array()), 'home'); ?>">
        <?php echo $this->translate('menu-home'); ?>
    </a>
    
    <a href="<?php echo $this->url(array('page' => 'services', 'static-content')); ?>">
        <?php echo $this->translate('menu-services'); ?>
    </a>
    
    <a href="<?php echo $this->url(array('module' => 'catalog', 'controller' => 'item', 'action' => 'search', 'default', true); true); ?>">
        <?php echo $this->translate('menu-catalog'); ?>
    </a>
    
    <a href="<?php echo $this->url(array('contact'), 'contact'); ?>">
        <?php echo $this->translate('menu-contact'); ?>
    </a>
</div>

<div id="content">
    <?php echo $this->layout()->content ?>
</div>

<div id="footer">
    <p>
        <?php echo $this->translate('created-with'); ?>
        <a href="http://framework.zend.com/Zend Framework">Zend Framework</a>/..
        <?php echo $this->translate('licensed-under'); ?>
        <a href="http://www.creativecommons.org/">Creative Commons</a>/.
    </p>
</div>
</body>
</html>
```

### 第 9 章：理解应用本地化

接下来是应用程序的联系表单。该表单的定义是使用 `ZendForm` 创建的，它可以自动检测并使用注册的 `ZendTranslate` 对象来执行运行时字符串本地化。因此，这里所需要的只是将每个元素的标签（label）替换为字符串标识符，该标识符将在运行时自动替换为翻译后的值。编辑位于 `$APP_DIR/library/Square/Form/Contact.php` 的表单定义，并进行**加粗**高出的更改：

```php
class Square_Form_Contact extends Zend_Form {
    public function __init() {
        // 初始化表单
        $this->setAction('/contact/index')
            ->setMethod('post');

        // 创建名称输入
        $name = new Zend_Form_Element('name');
        $name->setName('contact-name')
            ->setOptions(array('size' => '35'))
            ->setRequired(true)
            ->addValidator('NotEmpty');

        // 创建邮箱输入
        $email = new Zend_Form_Element('email');
        $email->setName('contact-email')
            ->setOptions(array('size' => '50'))
            ->setRequired(true)
            ->addValidator('EmailAddress');

        // 创建消息输入
        $message = new Zend_Form_Element('textarea');
        $message->setName('contact-message')
            ->setOptions(array('rows' => 8, 'cols' => 40))
            ->setRequired(true);

        // 创建验证码
        $captcha = new Zend_Form_Element('captcha');
        $captcha->setName('contact-captcha')
            ->setOptions(array('width' => 100, 'height' => 60))
            ->setRequired(true);

        // 创建提交按钮
        $submit = new Zend_Form_Element('submit');
        $submit->setName('contact-submit');

        // 添加所有元素
        $this->add($name);
        $this->add($email);
        $this->add($message);
        $this->add($captcha);
        $this->add($submit);
    }
}
```

## Zend Framework：入门指南

```php
class Square_Form_Contact extends Zend_Form {
    public function __init() {
        // 初始化表单
        $this->setAction('/contact/index')
            ->setMethod('post');

        // 创建名称输入
        $name = new Zend_Form_Element('name');
        $name->setName('contact-name')
            ->setOptions(array('size' => '35'))
            ->setRequired(true)
            ->addValidator('NotEmpty');

        // 创建邮箱输入
        $email = new Zend_Form_Element('email');
        $email->setName('contact-email')
            ->setOptions(array('size' => '50'))
            ->setRequired(true)
            ->addValidator('EmailAddress');

        // 创建消息输入
        $message = new Zend_Form_Element('textarea');
        $message->setName('contact-message')
            ->setOptions(array('rows' => 8, 'cols' => 40))
            ->setRequired(true);

        // 创建验证码
        $captcha = new Zend_Form_Element('captcha');
        $captcha->setName('contact-captcha')
            ->setOptions(array('width' => 100, 'height' => 60))
            ->setRequired(true);

        // 创建提交按钮
        $submit = new Zend_Form_Element('submit');
        $submit->setName('contact-submit');

        // 添加所有元素
        $this->add($name);
        $this->add($email);
        $this->add($message);
        $this->add($captcha);
        $this->add($submit);
    }
}
```

### 创建翻译源

一旦视图元素配置了本地化，下一步是为种语言创建翻译源。为了保持简单，将这些翻译源表示为 PHP 数组，并在文件名中指定区域。

通过切换到 `APP_DIR` 并执行以下命令为这些翻译源创建一个目录：

```bash
mkdir languages
```

然后，为支持的种语言创建翻译源文件。这里是法语翻译源示例，它应该保存为 `$APP_DIR/languages/fr.php`：

```php
<?php
return array(
  'menu-home' => 'ACCUEIL',
  'menu-services' => 'SERVICES',
  'menu-catalog' => 'BROCHURE',
  'menu-contact' => 'CONTACTEZ-NOUS',
  'welcome' => 'Bienvenue',
  'created-with' => 'Créé avec',
  'licensed-under' => 'Sous licence',
  'contact-name' => 'Nom',
  'contact-email' => 'Adresse email:',
  'contact-message' => 'Message:',
  'contact-verification' => 'Vérification:',
  'contact-send-message' => 'Envoyer Message',
  'contact-title' => 'Contactez-Nous',
);
```

完成后，你的目录结构应该像图 9-5 所示。

**提示**

在创建包含非拉丁字符的翻译文件时，使用 UTF-8 编码以避免数据损坏。某些免费和商业文本编辑器支持 UNIX 上的 `editic` 和 Windows 上的 `Notepad2`。下载链接可以在章末尾找到。

图 9-5 应用程序的翻译源，每个一个文件

## 专家问

**问**：为什么除了为 `en_US` 和 `en_GB` locale 创建文件外还要为 `en` locale 创建单独的翻译文件？



**答**：如本章之前提到的，如果`Zend_Translate`无法找到区域标识符的源文件，它将自动将区域标识符降级为仅语言代码，并使用该语言的通用翻译源文件（如果可用）。因此，建议为计划支持的每种语言始终包含一个通用翻译文件，此外还有更具体的翻译文件。

## 302 Zend Framework：入门指南

### 注册翻译对象

最后一步是更新应用启动文件（bootstrap），以配置并注册`Zend_Translate`对象的实例。该实例将在所有应用程序控制器和视图可用，从而可以使用翻译视图辅助器和`Zend_Form`的自动翻译功能。

为此，请更新`$APP_DIR/application/Bootstrap.php`中的应用启动文件，并向其中添加以下方法：

```php
<?php
class Bootstrap extends Zend_Application_Bootstrap_Bootstrap
{
    protected function _initTranslate() {
        $translate = new Zend_Translate('array',
            APPLICATION_PATH . '../languages/',
            null,
            array('scan' => Zend_Translate::LOCALE_FILENAME,
            'disableNotices' => 1));

        $registry = Zend_Registry::getInstance();
        $registry->set('Zend_Translate', $translate);
    }
}
```

### 提示

与其获取`Zend_Registry`实例，你可以使用简写方法`Zend_Registry::get($index)`和`Zend_Registry::set($index, $value)`直接访问注册表值。

大功告成了！要查看此效果，请配置你的浏览器设置并将法语或德语设置为你的首选语言。图 9-6 显示了如何在 Mozilla Firefox 中进行操作的示例，而图 9-7 显示了如何在 Microsoft Internet Explorer 中进行操作的示例。

图 9-6 在 Mozilla Firefox 中配置页面语言

## 第 9 章：理解应用本地化 303

![](img/222e7e58871b088cc6397852e1452b57_321_0.png)

**图 9-7** 在 Microsoft Internet Explorer 中配置页面语言

然后，访问`http://square.localhost/`的应用程序首页，你应该会看到类似于图 9-8 的内容。注意主菜单和页脚以所选的本地语言显示。

访问`http://square.localhost/contact`的联系表单，你会发现字段标签也由`Zend_Form`自动翻译了（见图 9-9）。

**图 9-8** 应用首页，已自动本地化为法语（续）

## 304 Zend Framework：入门指南

![](img/222e7e58871b088cc6397852e1452b57_322_0.png)

如果你调整浏览器设置以使用另一种首选语言，并且`Zend_Translate`能够找到该语言的翻译源，内容将自动翻译为所选语言（见图 9-10）。相反，如果`Zend_Translate`无法找到该语言的翻译源，将无法进行翻译，而是显示原始字符串标识符（见图 9-11）。最后，如果你的浏览器没有设置使用任何特定语言，区域自动检测将失败，`Zend_Locale`和`Zend_Translate`将将使用备用区域`en_GB`（见图 9-12）。

![](img/222e7e58871b088cc6397852e1452b57_322_1.png)

![](img/222e7e58871b088cc6397852e1452b57_323_0.png)

### 注意

你会注意到，无论区域自动检测如何，静态页面内容仍以美式英语显示。在本章有限的篇幅内无法涵盖本地化的这一方面，但你可以通过为每种语言创建单独的静态页面，并调整静态页面控制器以渲染对应当前区域或语言的页面来轻松处理。这种方法比创建包含每个静态页面内容的翻译密钥要好，因为维护如此大块的本地化内容会迅速变成问题。

![](img/222e7e58871b088cc6397852e1452b57_323_1.png)

（续）

## Zend Framework：入门指南

### 专家问答

**Q：翻译密钥（translation keys）应该是小写的吗？**

**A：**没有惯例要求你仅对翻译密钥使用小写。这样做意味着你需要在应用程序视图中，将`translate()`调用封装在`strtoupper()`和/或`ucfirst()`调用中，这这是一项繁琐的工作。此外，不同的语言可能对同一个单词有不同的大小写要求，而在应用程序视图中应用大小写转换将无法实现。最后，如果`Zend_Translate`无法找到所选语言的翻译源，它将退回到显示密钥本身。因此，将翻译密钥限制为小写通常是不理想的。然而，你应该确保你的翻译密钥命名正确，以便它们能作为`Zend_Translate`可行的备用方案。

## 支持手动选择区域

现在，虽然区域自动检测很方便，但你可能也希望用户能够手动选择他们所需的语言和区域。在很多情况下，此功能在应用程序用户界面中实现为一组可点击的旗帜图标；点击这些图标之一会将应用程序切换到相应的语言。

要添加此功能，请在应用程序的“default”模块中定义一个新的`LocaleController`，它将负责手动设置区域。在`$APP_DIR/application/controllers/LocaleController.php`创建此文件并使用以下代码：

```php
<?php
class LocaleController extends Zend_Controller_Action
{
    public function indexAction()
    {
        $locale = $this->getRequest()->getParam('locale');
        if ($locale) {
            $this->session->setItem('locale', $locale);
        }

        $url = $this->getRequest()->getServer('HTTP_REFERER');
        $this->redirect($url);
    }
}
```

现在，最后一步是将图标字符串添加到应用程序的主菜单中。要实现这一点，请更新`$APP_DIR/layouts/master.php`布局文件，高亮部分如下：

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 1.0//EN" "http://www.w3.org/TR/html1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="<?php echo $this->session->getItem('locale') ?: 'en'; ?>" lang="<?php echo $this->session->getItem('locale') ?: 'en'; ?>">
...
    <div id="menu-container">
        <div id="locale">
            <a href="<?php echo $this->url(array('module' => 'default', 'controller' => 'locale', 'action' => 'index', 'locale' => 'en_GB')); ?>">
                <img src="/images/locale/en_gb.gif" />
            </a>
            <a href="<?php echo $this->url(array('module' => 'default', 'controller' => 'locale', 'action' => 'index', 'locale' => 'en_US')); ?>">
                <img src="/images/locale/en_us.gif" />
            </a>
            <a href="<?php echo $this->url(array('module' => 'default', 'controller' => 'locale', 'action' => 'index', 'locale' => 'fr_FR')); ?>">
                <img src="/images/locale/fr_fr.gif" />
            </a>
            <a href="<?php echo $this->url(array('module' => 'default', 'controller' => 'locale', 'action' => 'index', 'locale' => 'de_DE')); ?>">
                <img src="/images/locale/de_de.gif" />
            </a>
        </div>
    </div>
</div>
</html>
```

现在，当你再次访问`http://square.localhost/`的应用程序首页时，你将能够从出现在每个页面上的菜单栏中手动选择语言。这种语言选择将覆盖从浏览器设置中自动检测的区域，并在你访问整个网站期间持续有效。图 9-13 所示了输出结果。

图 9-13 应用首页，带有手动选择语言的控件

## 第 9 章：理解应用本地化

### 总结

正如本章所示，Zend Framework 包含了将应用程序完全本地化到不同语言和国家所需的所有内容。`Zend_Locale`组件提供了一个定义应用程序区域语言的框架，既可以在设计时通过手动设置，也可以通过运行时自动检测过程来实现。无论何种情况，Zend Framework 组件（如`Zend_Date`、`Zend_Currency`和`Zend_Measure`）都能自动检测此区域语言并调整其行为，以反映日期、货币和量的本地惯例。

任何本地化项目最复杂的方面都是将应用程序翻译成不同的语言，Zend Framework 在这里也通过`Zend_Translate`解决方案。`Zend_Translate`提供了一个灵活的 API 用于处理许多不同格式的翻译，并且可以通过翻译视图助手（translation view helper）与`Zend_View`集成，以简化运行时本地化的任务。

本地化的这些方面都在 SQUARE 示例中得到了说明，在本章结束时，它现在支持四种区域语言，并能够以用户当前或选定的语言日期、数字和（部分）内容。虽然在本书有限的范围内无法进行完整的本地化练习，但该练习仍能让你对该过程有一定的深入了解，并为未来的研究奠基础。

要了解更多本章讨论的话题，请参考以下链接：

- `Zend_Locale`组件，访问`http://framework.zend.com/manual/en/zend.locale.html`
- `Zend_Date`组件，访问`http://framework.zend.com/manual/en/zend.date.html`
- `Zend_Date`格式化符，访问`http://framework.zend.com/manual/en/zend.date.constants.html`
- `Zend_Currency`组件，访问`http://framework.zend.com/manual/en/zend/currency.html`
- `Zend_Currency`汇率转换，访问`http://framework.zend.com/manual/en/zend.currency.exchange.html`
- `Zend_Measure`组件，访问`http://framework.zend.com/manual/en/zend/measure.html`
- `Zend_Translate`组件，访问`http://framework.zend.com/manual/en/zend/translate.html`
- `Zend_Translate`源文件目录布局，访问`http://framework.zend.com/manual/en/zend.translate.using.html`
- GNU gettext 项目，访问`http://www.gnu.org/software/gettext/`
- ISO 639 标准（语言代码），访问`http://www.iso.org/iso/support/faqs/widely_used_standards/widely_used_standards_other/language_codes`
- ISO 3166 标准（国家代码），访问`http://www.iso.org/iso/support/faqs/widely_used_standards/widely_used_standards_other/country_name_codes.htm`
- ISO 4217 标准（货币代码），访问`http://www.iso.org/iso/support/faqs/faqs_widely_used_standards/widely_used_standards_other/currency_codes.htm`
- PEAR `Services_ExchangeRates`包，访问`http://pear.php.net/package/Services_ExchangeRates/`
- gedit 文本编辑器，访问`http://www.gnome.org/projects/gedit/`
- Notepad2 文本编辑器，访问`http://www.flos.freeware.ch/notepad2.html`
- 使用 Zend Framework 构建多语言网站的讨论（Jason Gilmore），访问`http://www.developer.com/design/article.php/3683571/Build-Multi-lingual-Websites-With-the-Zend-Framework.htm`
- 使用 gettext 和 Zend Framework 进行字符串本地化的讨论（Peter Törnstrand），访问`http://www.tornstrand.com/2008/03/29/string-localization-with-gettext-and-zend-framework/`

## 第 10 章：处理新闻提送（News Feeds）与 Web 服务

Zend Framework 带有几个帮助处理此类提送的组件。`Zend_Feed_Reader`组件提供了 API 用于读取和解析两种常用格式的新闻提送，而`Zend_Feed`组件允许从原生 PHP 数据结构生成新提送或修改现有提送。接下来的章节将详细解释这些组件。

## 理解新闻提送格式

通常，新闻提送以 Really Simple Syndication (RSS) 格式或 Atom Syndication Format (ASF) 或更常见的“Atom”格式发布。这两种格式都是基于 XML 的，包含资源的标记列表，每个资源都标记有描述性信息，如标题、描述、URL 和日期。这两种格式还可以引用各种资源类型，包括文档（通常是博客文章或新闻项目）、图像以及视频和音频流。

与 RSS 类似，Atom 提送包含其描述的资源的摘要信息；然而，Atom 提送比 RSS 提送稍微复杂，而且 Atom 聚合格式已被接受互联网工程任务组 (IETF) 标准，这是 RSS 格式尚未比拟的。这些差异并非有意：Atom 格式是 2003 年作为 RSS 格式的替代方案提出的，而 RSS 格式最初是由 Netscape Communications 在 1997 年初设计的。自引入以来，RSS 格式经过了多次迭代和竞争性版本，而 Atom 格式被构想为一种新颖的方法，其优势是不需要与现有提送保持向后兼容。

图 10-1 展示了 RSS 和 Atom 格式之间的相似之处（以及差异）。

## 使用新闻提送

将新闻提送集成到 Zend Framework 应用中最简单的方法是使用`Zend_Reader`组件，它提供了一个简单、可扩展的框架用于解析提送和条目数据。`Zend_Reader`能够处理 Atom 和 RSS 提送，并支持所有版本。这是一个非常方便的方法，考虑到目前的提送用法。考虑以下示例，它说明了使用`Zend_Reader`的过程：

```php
<?php
class Sandbox_Example extends Zend_Controller_Action
{
    public function feedAction()
    {
        // 获取提送
        $feed = Zend_Reader::import('http://www.melonfire.com/feed.php?format=rss');

        // 视图数据
        $this->view->feed = array();
```

Zend Framework 在区域语言的哲学中指出：“你不必关心提送是 RSS 还是 Atom，只要你能提取你想要的信息。”

（注：此处由于原文不完整性，后续代码部分已根据上下文逻辑翻译并保留了 XML 结构。）

# 第 10 章：使用新闻源与 Web 服务 315



```php
'title' => $feed->getTitle(),
'description' => $feed->getDescription(),
'url' => $feed->getLink(),
'generator' => $feed->getGenerator(),
'numEntries' => $feed->count()
);

// 获取 feed 中的第一条目
$feed->rewind();
$entry = $feed->current();
$this->view->entries = array(
    'title' => $entry->getTitle(),
    'description' => $entry->getDescription(),
    'body' => $entry->getContent(),
    'url' => $entry->getLink(),
    'date' => $entry->getDateModified()
);
```

正如示例所示，使用 `Zend_Feed_Reader` 消费 feed 第一步是使用 `import()` 方法将其导入。该方法接受一个 feed 的 URL，并根据导入的 feed 类型返回一个 `Zend_Feed_Reader_Feed_Rss` 或 `Zend_Feed_Reader_Feed_Atom` 对象。该对象是访问 feed 数据的主要入口，并暴露了各种方法来访问 feed 摘要信息，如 `getTitle()`、`getLink()` 和 `getDescription()` 方法。

可以通过遍历主 feed 对象来访问 feed 内的条目。单个条目对象暴露了类似的方法。特别注意 `getTitle()`、`getDescription()`、`getLink()`、`getDateModified()`、`getCreated()` 和 `getContent()` 方法，它们分别返回条目标题、描述、URL、最后修改日期、创建日期和条目内容。这些方法足以满足大多数常见需求。

还可以作为 `DOMDocument`、`DOMXPath` 或 `DOMElement` 对象来访问 feed 的底层 XML 表达式。这在需要直接处理 feed XML 的情况下非常有用，可以通过 feed 对象的 `getDocument()`、`getElement()` 和 `getXPath()` 方法实现。这里有一个说明了此点的示例：

```php
class Sandbox_ExampleController extends Zend_Controller_Action
{
    public function feedAction()
    {
        // 从 URL 导入
```

# 316 Zend Framework：入门指南

```php
$feed = Zend_Feed_Reader::import(
'http://news.google.com/news?hl=en&topic=w&output=rss');
```

```php
// 获取底层的 XPath 对象
$xpath = $feed->getXPath();
```

```php
// 查询所有项目标题列表
$titles = $xpath->query('//item/title');
```

```php
// 返回列表中的第三项
$this->view->title = $titles->item(2)->nodeValue;
```

### 注意

还可以分别使用 `Zend_Feed_Reader::importFile()` 和 `Zend_Feed_Reader::importString()` 方法从文件或字符串导入新闻源。

除了 `Zend_Feed_Reader` 之外，Zend Framework 还包含了 `Zend_Feed` 组件，它为 feed 的生成和修改提供了一个全面的 API。虽然 `Zend_Feed` 可用于解析 feed，但 `Zend_Feed_Reader` 通常是更好的替代方案，因为它的 API 更简单，并且能够自动检测 feed 类型。尽管如此，为了完整起见，文中还包含了一个使用 `Zend_Feed` 消费 RSS feed 的示例：

```php
class SandboxExampleController extends Zend_Controller_Action
{
    public function feedAction()
    {
        // 从 URL 导入 feed
        $feed = Zend_Feed_Reader::import(
            'http://news.google.com/news?hl=en&topic=w&output=rss');

        // 获取 feed 级别的摘要元素
        $this->view->feed = array(
            'title' => $feed->title(),
            'description' => $feed->description(),
            'url' => $feed->link(),
            'generator' => $feed->generator(),
            'numEntries' => $feed->count()
        );

        // 获取 feed 中的第一条目
        $feed->rewind();
        $entry = $feed->current();
        $this->view->entries = array(
```

# 第 10 章：使用新闻源与 Web 服务 317

```php
array(
  'title' => $entry->title(),
  'description' => $entry->description(),
  'url' => $entry->link(),
  'date' => $entry->pubDate()
);
```

请注意，当使用 Zend 时，单个 feed 级和条目级元素的内容是通过 `object->method` 语法访问的，其中方法名与元素名对应。例如，`$feed->title()` 获取 feed `<title>` 元素的内容，而 `$entry->description()` 获取条目 `<description>` 元素的内容。

### 创建新闻源

现在读取 feed 的已经解决了。那么，如何创建新的 feed 呢？

创建一个新 feed 非常简单，通过 `Zend_Feed` 即可完成。要做到这一点，只需向 `ZendFeed::importArray` 方法传递一个表示 feed 和输出格式（RSS 或 Atom）的数组，它将生成一个指定格式的正确编码的 feed，适用于任何符合标准的 feed 阅读器。这里有一个示例，它展示了如何从数据库查询结果构建一个 Atom feed：

```php
class Sandbox_ExampleController extends Zend_ControllerAction

    public function feedAction()
{
        // 查询最近的 10 篇文章
        $q = Doctrine_Query::create()
            ->from('App_Model_Posts p')
            ->where('p.status = 1')
            ->orderBy('p.date desc')
            ->limit(10);
        $result = $q->fetchAll();

        // 生成输出数组
        // 设置 feed 级元素
        $output = array(
            'title' => 'Newest posts on',
            'link' => 'http://www.melonfire.com/columns/',
            'author' => 'Melonfire Feed/1.0',
            'charset' => 'UTF-8',
            'entries' => array()
        );
    }
```

# 318 Zend Framework：入门指南

```php
// 遍历结果
// 设置条目级元素
foreach ($result as $r) {
    $entry = array(
        'title' => $r['title'],
        'link' => 'http://www.melonfire.com/columns/',
        'id' => $r['id'],
        'description' => $r['abstract'],
        'lastUpdate' => strtotime($r['date'])
    );
    $output['entries'][] = $entry;
}

// 将数组导入 Zend_Feed 并转换为 Atom
$feed = Zend_Feed::importArray($output, 'atom');

// 禁用布局和视图渲染
$this->layout->disableLayout();
$this->getHelper('viewRenderer')->setNoRender(true);

// 发送 feed 到客户端
$feed->send();
exit();
```

Zend 的 `send()` 方法会设置自己的头部，所以如果你不需要这样做，或者想自定义头部，请考虑手动设置头部并使用 `saveXml()` 方法发送 feed。

之前的列表构建了一个包含 feed 和内容的嵌套数组，然后将其传递给 `Zend_Feed::importArray` 方法转换为 Atom feed。该方法的返回值是一个 `Zend_Feed_Atom` 对象，它暴露了两个实用方法：`send()` 和 `saveXml()`。图 10-2 显示了由示例生成的 feed。

### 注意

新版本的 Zend Framework 还包含了 `Zend_Feed_Writer` 组件，它为创建和修改 feed 提供了另一种 API。

第 10 章：使用新闻源与 Web 服务 319

图 10-2 动态生成的 Atom feed

### 访问 Web 服务

在近年来，面向消费者的 Web 应用几乎都通过 Web 服务暴露其部分或全部功能和数据以供第三方使用。Google、Facebook、Twitter、Technorati 和 Flickr 是如今数以万计允许此类访问的 Web 应用示例。作为应用程序开发者，你很可能会发现自己需要将这些 Web 服务集成到应用程序中，或者创建自己的 Web 服务供他人访问和消费。

Zend Framework 提供了许多常用 Web 服务的实现（包括上文提到的所有服务以及其他一些）。它还提供了通用的 SOAP 和 REST 客户端，用于访问基于 SOAP 和 REST 的 Web 服务。以下章节将详细介绍这些组件。

### 理解 Web 服务

将 Web 服务视为一个“远程 API”，它允许客户端在远程服务器上请求操作或执行查询。请求的性质各不相同；常见示例包括查找并返回匹配特定标识符的数据库记录、验证信用卡号，或检索特定代码对应的纬度和经度。服务器将接收请求，执行必要的查询或操作，并以结构化格式将结果返回给请求客户端。

Web 服务可能基于简单对象访问协议（SOAP）或表述状态迁移（REST）架构。在这两种情况下，客户端都通过 HTTP 传输请求并接收响应。区别在于这些请求和响应的编码方式。对于基于 SOAP 的服务，请求消息通常封装在 XML 封中，并以简单的 XML 包传输到服务器。而基于 REST 的请求和响应不进行 XML 编码，从客户端传输到服务器的 HTTP 方法（无论是 GET、POST、PUT 还是 DELETE）在决定服务操作和响应方面起着积极作用。

由于 REST 模型使用现有的 HTTP 词（如 GET（获取数据）、POST（创建数据）、PUT（更新数据）和 DELETE（删除数据））来通信意图，它通常被认为比 SOAP 模型更容易、更简单。为了更好地理解，请参考图 10-3，它说明了 SOAP 和 REST 请求响应包之间的区别。

如果你曾在聚会上提过问题或在听力范围内要求过回复，以下是 SOAP 和 REST 方法之间的一些关键区别点：

- SOAP 大量使用 XML 进行请求和响应编码，并使用数据类型来确保在客户端和服务器之间传递的数据完整性。相比之下，REST 请求和响应可以使用 ASCII、XML、JSON 或任何客户端和服务器都能理解的格式进行传输。此外，REST 模型没有内置的数据类型要求。因此，REST 请求和响应包通常比相应的 SOAP 包要小得多。
- 在 SOAP 模型下，HTTP 传输层大部分是被动的旁观者，其角色局限于使用 POST 方法从客户端向服务器传输 SOAP 请求。服务请求的细节（如过程名称和输入参数）被编码在请求体中。而 REST 架构将 HTTP 传输层视为事务的积极参与者，利用现有的 HTTP“动词”（如 GET、POST、PUT 和 DELETE）来指示所需的服务类型。从开发的角度来看，REST 请求通常更容易构建和理解，并且可以寄载在现有的、广为人知的 HTTP 接口上。
- SOAP 模型支持某种程度的自省，允许服务开发人员在 Web 服务描述语言（WSDL）文件中描述 API。这些文件的创建相当复杂；然而，这种努力通常是值得的，因为 SOAP 客户端可以通过此 WSDL 文件获取有关方法名和签名、输入和输出数据类型以及返回值的详细信息。

## 第 10 章：使用新闻订阅和 Web 服务

```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-Envelope
  xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"
  xmlns:ns1="http://rpc.geocoder.us/Geo/Coder/US/"
  xmlns:xsd="http://www.w3.org/2001/XMLSchema"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xmlns:soapenv="http://schemas.xmlsoap.org/soap/encoding/"
  SOAP-ENV:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/">
<SOAP-ENV:Body>
  <ns1:getCode>
    <ns1:location xsi:type="string">1600 Pennsylvania Av, Washington, DC</ns1:location>
  </ns1:getCode>
</SOAP-ENV:Body>
</SOAP-Envelope>
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xmlns:soapenv="http://schemas.xmlsoap.org/soap/encoding/"
xmlns:xsd="http://www.w3.org/2001/XMLSchema"
xmlns:soapenv="http://schemas.xmlsoap.org/soap/encoding/"/>
<geo:codeResponse xmlns="http://rpc.geocoder.us/Geo/Coder/US/">
  <geo:soapenv:arrayType="geo:GeocoderAddressResult[1]">
  <geo:type xmlns="http://rpc.geocoder.us/Geo/Coder/US/">
    <geo:number xsi:type="xsd:int">1600</geo:number>
    <geo:street xsi:type="xsd:string">Pennsylvania Av</geo:street>
    <geo:state xsi:type="xsd:string">DC</geo:state>
    <geo:city xsi:type="xsd:string">Washington</geo:city>
    <geo:zip xsi:type="xsd:int">20502</geo:zip>
    <geo:country xsi:type="xsd:string">US</geo:country>
    <geo:long_suffix xsi:type="xsd:string">geo</geo:long_suffix>
    <geo:long xsi:type="xsd:float">-77.037684</geo:long>
    <geo:lat xsi:type="xsd:float">38.898748</geo:lat>
    <geo:prefix xsi:type="xsd:string">/</geo:prefix>
  </geo:type>
</geo:codeResponse>
```

### SOAP 请求和响应

```http
GET /geocode?address=1600+Pennsylvania+Av,+Washington,+DC HTTP/1.1
```

## 324 Zend Framework：入门指南



这是另一个示例，使用`Zend_Gdata`组件查询 YouTube 服务以当前最热门的五个视频列表：

```php
<?php
class Sandbox_ExampleController extends Zend_Controller_Action
{
    public function youtubeAction()
    {
        // 初始化服务对象
        $client = new Zend_Gdata_YouTube();

        // 获取热门视频的馈
        $feed = $client->getFeed(
            'http://gdata.youtube.com/feeds/standardfeeds/most_popular?
            max-results=5'
        );

        // 处理馈并获取单个条目
        // 为每个条目获取标题、分类、评分、播放次数和 URL
        $this->view->mostViewed = array(
            foreach ($feed as $entry) {
                'title' => $entry->getTitle(),
                'rating' => $entry->getVideoRatingInfo(),
                'category' => $entry->getVideoCategory(),
                'views' => $entry->getVideoViewCount(),
                'watch' => $entry->getVideoWatchPageUrl()
            }
        );
    }
}
?>
```

在这个示例中，`getVideoFeed()`方法返回一个 YouTube 视频结果的 Atom 馈；该馈会被自动解析并转换为`Zend_Gdata_YouTube_VideoEntry`对象的数组，每个对象代表馈中的一个条目。遍历此数组、使用对象属性检索每个条目的详情并将其表示为 Web 页面要简单得多。

最后，这是一个`Zend_Service_Amazon`实现的示例，用于在 Amazon.com 上搜索特定作者的书籍：

```php
<?php
class Sandbox_ExampleController extends Zend_Controller_Action
{
    public function amazonAction()
    {
        // 初始化服务对象
        $client = new Zend_Service_Amazon('ACCESS-KEY', 'US', 'SECRET-KEY');
```

## 第 10 章：使用新闻馈和 Web 服务

```php
// 按属性在 Amazon.com 上搜索项目
$items = $client->itemSearch(array(
    'SearchIndex' => 'Books',
    'Author' => 'Dan Brown',
    'ResponseGroup' => 'Large'
));

// 处理搜索结果
$this->view->results = array();
foreach ($items as $i) {
    $this->view->results[$i] = array (
        'asin' => $i->ASIN,
        'title' => $i->Title,
        'author' => $i->Author,
        'url' => $i->DetailPageURL,
        'rating' => $i->AverageRating,
        'salesRank' => $i->SalesRank
    );
}
```

搜索对象的`itemSearch()`方法查询 Amazon Web 服务以获取匹配指定参数的产品列表，并返回一个`Zend_Service_AmazonItem`对象的数组，其中包含对应项目的信息。遍历此对象数组并提取相关信息进行显示是非常简单的。

## 使用通用客户端实现

如果你正尝试访问一个没有预定义服务实现的 Web 服务，不要灰心：Zend Framework 还包含了用于访问此类服务的通用 SOAP 和 REST 客户端。这些客户端分别在`Zend_Soap_Client`和`Zend_Rest_Client`组件中实现。

为了为了说明这一点，请考虑以下示例，它使用通用 SOAP 客户端访问 GeoCoder Web 服务，并返回特定地址对应的纬度和经度：

```php
<?php
class SandboxExampleController extends Zend_Controller_Action {
    public function soapAction() {
        // 初始化 SOAP 客户端
        $soap = new GeoCoderSoap_wsdl(
            'http://geocoder.us/dist/clients/GeoPHP.wsdl', array(
                'soap_version' => SOAP_1_1,
                'compression' => SOAP_COMPRESSION_ACCEPT
            )
        );
```

## 326 Zend Framework：入门指南

```php
// 获取地址的纬度/经度结果
$response = $soap->geocode('E Capitol St NE & 1st St NE, Washington, DC');
$this->view->results = array();
foreach ($response as $r) {
    $this->view->results[] = array(
        'zip' => $r->zip,
        'latitude' => $r->lat,
        'longitude' => $r->long
    );
}

// 获取地址的纬度/经度结果
$this->view->request = $soap->getLastRequest();
$this->view->response = $soap->getLastResponse();
```

此示例创建了一个新的`Soap_Client`对象并使用 WSDL 对其实例化。一旦`Soap_Client`对象实例化，就可以通过代理 WSDL 文件来访问远程方法。`Soap_Client`对象将负责创建 SOAP 消息、将其传输到服务器、接收数据并解码响应。

`Zend_Soap_Client`组件利用 PHP 的 soap 扩展，如果你的 PHP 环境没有包含此扩展，它将无法运行。类似地，可以使用`Zend_Rest_Client`实现以通用且一致的方式访问基于 REST 的 Web 服务。考虑这个示例，它通过尝试访问国家的 GeoNames REST 服务来说明这一点：

```php
<?php
class Sandbox_ExampleController extends Zend_Controller_Action
{
    public function restAction()
    {
        // 初始化 REST 客户端
        $client = new Zend_Rest_Client('http://www.geonames.org/countryInfo');

        // 设置参数
        $client->country('IN');

        // 为国家信息发送 GET 请求
        // 解析结果
        $result = $client->get();
        $this->view->countryName = $result->countryName();
        $this->view->countryCode = $result->countryCode();
        $this->view->capital = $result->capital();
        $this->view->areaKm = $result->areaInKm();
        $this->view->population = $result->population();
        $this->view->languages = $result->languages();
        $this->view->mapCoordinates = array(
            $result->bBoxWest(),
            $result->bBoxNorth(),
            $result->bBoxSouth()
        );

        // 获取 REST 请求和响应用于调试
        $this->view->request = $client->getLastRequest();
        $this->view->response = $client->getLastResponse();
    }
}
?>
```

## Zend Framework：入门指南

正如这两个示例所示，Zend Framework 能够轻松地访问任何基于 SOAP-REST 的 Web 服务，即使在尚未存在特定服务实现的情况下，也不需要对服务接口有深入了解。这使其成为将第三方 Web 服务快速高效地集成到 PHP 应用程序中的极佳工具。

### 提示

请注意上一个列表中的`getLastRequest()`和`getLastResponse()`方法。这些方法对于调试 SOAP 和 REST 事务，以及验证请求和响应包的内容非常有用。

## 尝试此操作：第 10 章 集成 Twitter 和博客搜索结果

有了这些背景信息，让我们来看看它们在现实世界中如何运作。接下来的章节将说明如何结合前面章节中的组件，在 SQUARE 示例应用程序中显示与“集邮”主题相关的最新新闻、博客文章和 Twitter 更新。

### 定义自定义路由

第一步一如既往，为新闻页面定义一个自定义路由。编辑应用程序配置文件`$APP_DIR/application/configs/application.ini`，并将以下路由定义添加到：

```ini
resources.router.routes.news.route = /news
resources.router.routes.news.defaults.module = default
resources.router.routes.news.defaults.controller = news
resources.router.routes.news.defaults.action = index
```

### 定义控制器和视图

下一步是为新闻接口定义动作（action）和视图（view）。以下是`NewsController`的代码，应保存为`$APP_DIR/application/modules/default/NewsController.php`：

```php
<?php
class NewsController extends Zend_Controller
{
    public function indexAction()
    {
        // 获取 Twitter 搜索
        $q = 'philately';
        $this->view->q = $q;
        $twitter = new Zend_Service_Twitter_Search();
        $this->view->tweets = $twitter->search($q,
            array('lang' => 'en', 'rpp' => 8, 'show_user' => true));

// 获取 Google News Atom 馈
$this->view->feeds = array();
$gnewsFeed = "http://news.google.com/news?hl=en=$q&output=atom";
$this->view->feeds[0] = Zend_Feed_Reader::import($gnewsFeed);

// 获取 BPMA RSS 馈
$bpmaFeed = "http://www.postalheritage.org.uk/news/RSS";
$this->view->feeds[1] = Zend_Feed_Reader::import($bpmaFeed);
```

`indexAction()`方法负责访问和交互各种数据源（feeds）以及 Web 服务。

- 搜索包含“philately”（集邮）关键词的最新状态更新。对象的方法接受一个查询词，以及一个指定语言过滤器、返回结果数量以及每个结果是否应包含源用户 Twitter 用户名的选项。该方法的返回值是一个匹配搜索结果的嵌套数组，该数组被附加到视图中进行处理。
- `Zend_Feed_Reader`的实现用于导入两个新闻馈。第一个是 Atom 馈，它将 Google News 中与“philately”相关的最新新闻标题连接起来；第二个是英国邮政博物馆和档案馆（BPMA）官方博客的近期帖子列表。生成的馈对象被赋值为脚本变量。

以下是对应的视图，应保存为`$APP_DIR/application/modules/default/views/scripts/news/index.php`：

```html
<h2>News</h2>
<div id="feeds">

<div id="posts">
<strong>Recent news about</strong>
<a href="http://news.google.com/news?hl=en=$q=<?php echo $this->q; ?>">
'<?php echo $this->q; ?>'
</a>:
<strong></strong>
<p id="div"></p>
<?php $count = 0; ?>
<?php foreach ($this->feeds[0] as $entry) :?>
<?php if ($count >= 5) break; ?>
<p class="post">
<span class="text">
<a href="<?php echo $entry->getLink(); ?>">
  <?php echo $entry->getTitle(); ?>
</a>
<span class="time">
  <?php echo $entry->getDateModified(); ?>
</span>
</p>
<?php $count++; ?>
<?php endforeach; ?>

<p style="padding-top: 4px"/>

<strong>Recent posts from
<a href="http://www.postalheritage.org.uk/">
  the British Postal Museum and Archive
</a> blog:
</strong>
<p><div id="div"></div></p>
<?php $count = 0; ?>
<?php foreach ($this->feeds[1] as $entry): ?>
<?php if ($count >= 5) break; ?>
<p class="post">
<span class="text">
<a href="<?php echo $entry->getLink(); ?>">
  <?php echo $entry->getTitle(); ?>
</a>
<span class="time">
  <?php echo $entry->getDateModified(); ?>
</span>
</p>
<?php $count++; ?>
<?php endforeach; ?>
</div>
<div>
<strong>Recent tweets about
<a href="http://search.twitter.com/search?q=<?php echo $this->q; ?>">
  '<?php echo $this->q; ?>'
</a>
<strong>

<?php foreach ($this->tweets as $tweet): ?>
<p class="post">
<span class="text">
<a href="<?php echo $tweet->getLink(); ?>">
  <?php echo $tweet->getTitle(); ?>
</a>
<span class="time">
  <?php echo $tweet->getDateModified(); ?>
</span>
</p>
<?php endforeach; ?>
</div>
</div>
```

# 334 Zend Framework：入门指南

```php
public function putAction()
{
    // 处理 PUT 请求
}

public function deleteAction()
{
    // 处理 DELETE 请求
}
```

# 尝试此节：10-2 实现基于 REST 的 Web 服务

从上一个节中可以清楚地看出，在应用中采用 REST 架构（特别是参考标准的 CRUD 操作）涉及两个核心组成部分：



- 1. 一个继承 `Zend_Rest_Controller` 的控制器，并实现与标准 HTTP 方法对应的动作（actions）。
- 2. 一个使用 `Zend_Rest_Route` 的路由，用于将传入的 URL 请求与上述控制器动作进行匹配。

理解其工作原理的最佳方法是使用示例。接下来的章节将通过为 SQUARE 示例应用程序构建简单的基于 REST 的 API 来说明这一点。该 API 将支持 GET 和 POST 方法，并允许用户检索现有目录项的信息以及发布新条目。

### 创建新模块

第一步是创建一个新模块——我们将其命名为“api”，用于存放 REST 控制器。要执行此操作，请更改`SAPP_DIR/application/`并执行以下命令：

```shell
shell> mkdir modules/api
shell> mkdir modules/api/controllers
shell> mkdir modules/api/views
shell> mkdir modules/api/views/scripts
```

### 定义控制器

下一步是定义 API 控制器，它将处理所有的 REST 请求。如之前所述，该控制器应该继承抽象类 `Zend_Rest_Controller` 并实现其所有的抽象方法。它的代码结构如下：

```php
<?php
class ApiCatalogController extends Zend_Rest_Controller
{
    // 禁用布局和渲染
    public function init()
    {
        $this->apiBaseUrl = 'http://square.localhost/api/catalog';
        $this->_helper->layout->layout->disableLayout();
        $this->_getHelper('viewRenderer')->setNoRender(true);
    }

    public function indexAction()
    {
        // 处理 GET 请求
    }

    public function getAction()
    {
        // 处理 GET 请求
    }

    public function postAction()
    {
        // 处理 POST 请求
    }

    public function putAction()
    {
        // 处理 PUT 请求
    }

    public function deleteAction()
    {
        // 处理 DELETE 请求
    }
}
```

注意控制器的 `init()` 方法，它禁用了所有的布局和视图脚本渲染。这是因为 REST API 通常会以 XML、JSON 或（某些情况下）ASCII 文本返回响应。这些输出可以在控制器内部生成并直接发送给请求客户端。

将此控制器保存为`$APP_DIR/application/modules/api/controllers/CatalogController.php`。

## 定义 GET 动作

接下来，让我们定义 `ApiCatalogController::indexAction`。你可能记得当路由器遇到没有 "id" 请求变量的 GET 请求时，该动作会被自动分发，并且应该返回所有匹配资源的列表。代码如下：

```php
<?php
class Api_CatalogController extends Zend_Rest_Controller
{
    public function indexAction()
    {
        // 从数据库获取记录
        $q = Doctrine_Query::create()
            ->from('i.Square_Model_Item i')
            ->leftJoin('i.Square_Model_Country c')
            ->leftJoin('i.Square_Model_Grade g')
            ->leftJoin('i.Square_Model_Type t')
            ->where('i.DisplayStatus = 1');
        $result = $q->fetchArray();

        // 设置 feed 元素
        $output = array(
            'title' => 'Catalog records',
            'link' => $this->apiBaseUrl,
            'author' => 'Square API/1.0',
            'charset' => 'UTF-8',
            'entries' => array()
        );

        // 设置每个条目元素
        foreach ($result['entries'] as $r) {
            $output['title'] = $r['Title'] . ' - ' . $r['Year'],
            $output['link'] = $this->apiBaseUrl . '/' . $r['RecordID'],
            $output['description'] = $r['Description'],
            $output['lastUpdate'] = strtotime($r['RecordDate']),
            $output['square:title'] = $r['Title']
        }

        // 将数组导入 atom feed
        // 发送给客户端
        $feed = Zend_Feed::importArray($output, 'atom');
        $feed->send();
        exit;
    }

    // 转发到 indexAction
    public function listAction() {
        return $this->forward('index');
    }
```

`Api_Catalog::indexAction` 开始执行一个 Doctrine 查询以获取所有活动目录项的列表。它遍历结果集，将其转换为适用于通过 `Zend_Feed::Array` 转换为 Atom feed 的嵌套数组。此 Atom feed 使用 feed 对象的 `send()` 方法返回给客户端。

### 注意

Zend Framework v1.9 及更早版本包含一个 bug，导致路由器尝试删除指向 `indexAction()` 的 REST 请求，转而将其发送到 `listAction()`。下述列表说明了针对此问题的简单变通方法：使用控制器方法将 `listAction()` 请求（如果有）转发到 `indexAction()`。当路由器遇到带有 "id" 变量的 GET 请求时，会自动分发 `Api_CatalogController::getAction()`。在这种情况下，该动作必须为请求客户端检索详细信息。

```php
<?php
class Api_CatalogController extends Zend_Rest_Controller
{
    public function getAction()
    {
        // 从数据库获取记录
        $id = $this->getRequest('id');
        $q = Doctrine_Query::create()
            ->from('i.Square_Model_Item i')
            ->leftJoin('i.Square_Model_Country c')
            ->leftJoin('i.Square_Model_Grade g')
            ->leftJoin('i.Square_Model_Type t')
            ->where('i.RecordID = ?', $id)
            ->andWhere('i.DisplayStatus = 1');
        $result = $q->fetchArray();

        // 如果记录可用
        if (count($result) == 1) {
            $output = array(
                'title' => 'Catalog record for ' . $id,
                'link' => $this->apiBaseUrl . '/' . $id,
                'author' => 'Square API/1.0',
                'charset' => 'UTF-8',
                'entries' => array()
            );

            // 设置条目元素
            $output['entries'] = array(
                'title' => $result[0]['Title'] . ' - ' . $result[0]['Year'],
                'link' => $this->apiBaseUrl . '/' . $result[0]['RecordID'],
                'description' => $result[0]['Description'],
                'lastUpdate' => strtotime($result[0]['RecordDate']),
                'square:title' => $result[0]['Title']
            );

            // 将数组导入 atom feed
            $feed = Zend_Feed::importArray($output, 'atom');
            $feed->registerNamespace('square', 'http://square.localhost');

            // 设置命名空间元素
            $feed->rewind();
            $entry = $feed->current();
            if ($entry) {
                $entry['square:id'] = $result[0]['RecordID'];
                $entry['square:title'] = $result[0]['Title'];
                $entry['square:year'] = $result[0]['Year'];
                $entry['square:grade'] = $result[0]['Grade'];
                $entry['square:Model_Grade'] = $result[0]['GradeName'];
                $entry['square:description'] = $result[0]['Description'];
                $entry['square:country'] = $result[0]['Country'];
                $entry['square:Model_Country'] = $result[0]['CountryName'];
                $entry['square:price'] = null;
                $entry['square:price']['square:min'] = $result[0]['PriceMin'];
                $entry['square:price']['square:max'] = $result[0]['PriceMax'];
            }

            // 输出给客户端
            $feed->send();
            exit;
        } else {
            $this->getResponse()->setStatusCode(404);
            echo 'Invalid record identifier';
            exit;
        }
    }
}
```

这与上一个列表非常相似，不同在于在这种情况下，Atom feed 包含了额外的元素（位于自定义命名空间的类型、等级、位置和描述中）。注意，如果提供的资源 ID 未匹配到数据库中的记录，将跳过 feed 创建过程并直接发送 404（页面未找到）错误。这是 REST 架构利用现有标准（在此例中为 HTTP 错误代码）来提供请求状态信息的示例。

## 第10章：处理新闻订阅与网络服务 339

## 定义 POST 操作

当路由器遇到 POST 请求时，会自动分发 `Api_CameraController::postAction`。根据 REST 惯例，此类请求应该导致创建一个新资源，请求体包含创建该资源所需的原始数据。代码如下：

```php
<?php
class Api_ApiController extends Zend_Rest_Controller
{
    public function postAction()
    {
        // 读取 POST 参数并保存到数据库
        $item = new Square_Item;
        $item->fromArray($this->getRequest()->getPost());
        $item->setRecordDate(date('Y-m-d', mtime(time())));
        $item->setDisplayUntil = null;
        $item->save();
        $id = $item->getRecordID();

        // 将响应码设置为 201
        // 发送新创建记录的 ID
        $this->getResponse()->setHttpResponseCode(201);
        $this->getResponse()->setHeader('Location', $this->getApiBaseUrl().'/'.$id);
        echo $this->getApiBaseUrl().'.'.$id;
        exit;
    }
}
```

注意，一旦资源记录被创建并保存到数据库，客户端将收到一个 201（已创建）响应码以及新创建资源的 URL。

### 专家问答

**Q：** 为什么你的 REST API 以 Atom 馈的形式返回结果？

**A：** 虽然基于 REST 的 API 可以以任何格式返回数据，但它们返回 Atom 或 RSS 馈是非常常见的。这是因为大多数现代 HTTP 客户端都内置了对这些馈的支持，大多数编程语言也包含了内置或易用的这些格式解析器。

## 初始化 REST 路由

最后一步是初始化 REST API 路由。要做到这一点，请使用应用程序引导程序并向其添加以下方法：

```php
<?php
class Bootstrap extends Zend_Application_Bootstrap_Bootstrap
{
    protected function _initRoutes()
    {
        $front = Zend_Controller_Front::getInstance();
        $router = $front->getRouter();
        $restRoute = new Zend_Rest_Route($front, array(), array('api'));
        $router->addRoute('api', $restRoute);
    }
}
```

图 10-5 获取所有记录 GET 请求的 API 响应

此 `initRoutes()` 方法负责初始化一个新的 `Zend_Rest_Route` 实例，并映射到第一步中创建的新“api”模块。`Zend_Rest_Route` 构造函数的第三个参数指定了启用 REST 的模块或控制器名称数组。

此时，你的 REST API 已经运行。你可以通过在 Web 浏览器中访问 URL `http://square.localhost/api/catalog` 来测试它，它应该产生一个来自邮票目录数据库的活动列表的 Atom 馈。图 10-5 展示了输出的内容。

在类似的视图中，带有额外项目标识符访问相同的 URL（例如 `http://square.localhost/api/catalog/1`）将生成一个包含请求项目详情的 Atom 馈。图 10-6 展示了这可能的样子。

图 10-6 获取特定请求 GET 请求的 API 响应

**图 10-7** POST 请求的 API 响应



最后，向 URL `http://square.localhost/api/catalog` POST 一个数据数组将导致数据库中创建一个新的项目记录，并向客户端返回项目 URL 的引用（见图 10-7）。

### 总结

大多数博客和新闻网站使用 RSS 或 Atom 馈，这些馈可以将新内容分发到第三方应用程序。编写解析器来消费这些馈是一项常见的应用开发任务，而 Zend Framework 通过提供一组预定义的组件来生成、修改和解析新闻馈，简化了这一工作。本章详细讨论了这些组件，说明了如何使用它们将来自在线新闻源的馈集成到 SQUARE 示例应用程序中。

通过允许第三方访问应用程序的功能，网络服务实现了更广泛的“杂烩”（mashups）和衍生产品，这些产品在整合多个源数据的同时鼓励了创新。Zend Framework 让人们轻松加入网络服务的行列：它包含了用于 REST 和 SOAP 的通用客户端，以及由 Google、Amazon 和 Twitter 等流行应用程序暴露的网络服务的就绪实现。本章演示了这些实现中的部分，并说明了使用 SQUARE 示例从零创建基于 REST 的网络服务的知识。

要了解更多关于本章讨论的话题，请访问以下链接：

- Zend_Feed_Reader 组件，位于 `http://square.localhost/`
- Zend_Feed 组件，位于 `http://square.localhost/`
- Zend_Rest 组件，位于 `http://square.localhost/`

# 第 11 章：使用用户界面元素

标签（label）以及一个 URL 或模块/控制器/动作的组合；它可能还包含其他可选信息，如可见性、排序顺序、访问权限以及前向和反向关系。页面被进一步组织成导航容器，导航容器简单来说就是页面的分级集合。

为了更好地理解这一点，请考虑下面的 PHP 示例，它展示了页面与容器之间的关系：

```php
<?php
class SandboxExampleController extends Zend_Controller_Action {
    function navAction() {
        // initialize pages
        $config = array(
            Zend_Navigation_Page::factory(array(
                'label' => 'Foreword',
                'uri' => '/forward',
            )),
            Zend_Navigation_Page::factory(array(
                'label' => 'Chapter 1: Introducing the Zend Framework',
                'uri' => '/chapter-01',
                'pages' => array(
                    Zend_Navigation_Page::factory(array(
                        'label' => 'Overview',
                        'uri' => '/chapter-01/overview',
                    )),
                    Zend_Navigation_Page::factory(array(
                        'label' => 'Features',
                        'uri' => '/chapter-01/features',
                    ))
                )
            )),
            Zend_Navigation_Page::factory(array(
                'label' => 'Index',
                'uri' => '/index',
            ))
        );
        // initialize navigation container
        $container = new Zend_Navigation($config);
    }
}
```

上面的列表为书籍设置了一个示例导航容器。容器本身表示为 `Zend_Navigation` 对象，并接收一个 `Zend_Navigation_Page` 对象的数组。容器中的每个顶层 `Zend_Navigation_Page` 对象代表导航层级结构顶部的页面，每个页面都有标题和 URL。每个页面本身也可以包含更多页面；这些页面以 `Zend_Navigation_Page` 对象的形式表示并作为嵌套数组附加到父页面。这种分级结构可以轻松扩展到覆盖整个网站的表面。

页面对象是通过 `Zend_Navigation_Page_Mvc` 类或 `Zend_Navigation_Page_Uri` 类的实例创建的，这两者都扩展了抽象的 `Zend_Navigation_Page` 类。两者之间的区别在于页面链接定义：前者通过指定每个页面的模块、动作和控制器来利用 Zend Framework 的路由器，而后者则直接将页面链接指定为 URL。下面的示例说明了这种区别：

```php
<?php
class Sandbox_ExampleController extends Zend_Controller_Action
{
    function action()
    {
        // define MVC page
        $page = Zend_Navigation_Page::factory(
            'label' => 'Contact Us',
            'module' => 'default',
            'controller' => 'contact',
            'action' => 'index',
        );

        // define URI page
        $page = Zend_Navigation_Page::factory(
            'label' => 'Contact Us',
            'uri' => '/contact/',
        );
    }
}
```

每个页面暴露了许多“getter”（获取）和“setter”（设置）方法，这些方法可设置页面属性。例如，标签、前向关系、反向关系和可见性都可以分别通过页面对象的 `setLabel()`、`setRel()`、`setRev()` 和 `setVisibility()` 方法设置，并可以通过相应的 `getLabel()`、`getRel()`、`getRev()` 和 `getVisibility()` 方法检索。还有一个 `isActive()` 方法，它用于返回页面是否匹配当前请求。

提示：在大多数情况下，优选使用 `Zend_Navigation_Page_Uri` 实例。它们不仅更易读，而且这些对象的灵活性意味着它们还可以用于创建通到外部或第三方资源的链接。如之前所示，`Zend_Navigation` 容器可以使用一个数组进行初始化。然而，对于长或复杂的导航结构，这种方法可能会变得非常臃肿，因此你可以使用 XML 文档。下面的示例展示了其中一个这样的文档：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<config>
  <home>
    <label>Foreword</label>
    <uri>/forward</uri>
  </home>
  <chapter1>
    <label>Chapter 1: Introducing the Zend Framework</label>
    <uri>/chapter-01</uri>
    <pages>
      <overview>
        <label>Overview</label>
        <uri>/chapter-01/overview</uri>
      </overview>
      <features>
        <label>Features</label>
        <uri>/chapter-01/features</uri>
      </features>
    </pages>
  </chapter1>
  <index>
    <label>Index</label>
    <uri>/index</uri>
  </index>
</config>
```

## Zend Framework：学者指南

# 渲染导航元素

当然，定义网站的导航结构只是问题的一部分；你仍然需要以某种方式使用它。通常，`Zend_Navigation` 容器在应用程序中初始化

# 352 Zend Framework：学者指南

在引导加载程序中初始化并通过应用程序注册表实现持久化。以下是一个说明如何设置容器的示例：

```php
<?php
class Bootstrap extends Zend_Application_Bootstrap_Bootstrap
{
    protected function initNavigation()
    {
        $config = new Zend_Config_Xml(APPLICATION_PATH . '/configs/site.xml');
        $container = new Zend_Navigation($config);
        $registry = Zend_Registry::getInstance();
        $registry->set('Zend_Navigation', $container);
    }
}
```

完成后，`Zend_Navigation` 视图助手会自动从脚本内部访问已注册的导航容器，并将其适用于 Web 页面的菜单、站点地图或面包屑导航。接下来的章节将详细讨论这些方面。

### 菜单 (Menus)

`Zend_Navigation` 菜单助手可以自动将导航数据转换为分层的无序列表。以下是如何在脚本中使用它的示例：

```php
<?php echo $this->navigation()->menu(); ?>
```

> 此代码的输出是嵌套的无序链接列表，如图 11-1 所示。也可以通过自定义此默认输出，例如指定仅显示活动菜单分支，并定义菜单树的深度。这些选项作为关联数组传递给视图助手的 `renderMenu()` 方法。以下是之前示例的修订版本，说明了这一点：

```php
<?php
echo $this->navigation()
    ->renderMenu(null, array(
        'minDepth' => null,
        'maxDepth' => 1,
        'ulClass' => 'nav',
        'onlyActiveBranch' => true
    ));
?>
```

图 11-2 展示了生成的输出。

### 提示 (TIP)

如果你希望使用自定义标记而不是默认的无序列表渲染菜单，可以使用 `setPartial()` 方法为 Menu 视图助手指定自定义视图脚本。

### 面包屑导航 (Breadcrumb Trails)

还有一个 Breadcrumbs 导航助手，根据当前请求的 URL 自动创建面包屑导航。在这种情况下，也可以自定义面包屑的外观，包括分隔符、缩进以及是否将最后一个面包屑渲染为链接。以下是在视图脚本中使用此助手的示例：

```php
<?php
echo $this->navigation()
  ->breadcrumbs()
  ->setLinkLast(true)
  ->setSeparator(' / ');
?>
```

图 11-3 展示了输出。

## Zend Framework：学者指南

![](img/222e7e58871b088cc6397852e1452b57_372_0.png)

### 链接 (Links)

Links 助手生成一组 `<link>` 元素，表示特定页面与文档集合中其他页的关系，并为搜索引擎提供额外信息。这些 `<link>` 元素可以表示正向和反向关系，并且始终出现在 HTML 文档的 `<head>` 中。

以下是在视图脚本中使用此助手的示例：

```php
<?php echo $this->navigation()->links(); ?>
```

图 11-4 展示了输出的示例。

### 站点地图 (Sitemaps)

Sitemap 助手允许根据导航容器中的数据自动生成 XML 站点地图。该站点地图符合 Google、Yahoo! 和微软采用的 Sitemap 协议，你可以在本末尾找到关于该协议更多信息的链接。

```xml
<link rel="start" href="home" title="Home">
<link rel="next" href="/products/men/75393" title="Shoes">
<link rel="prev" href="/products/men/16339" title="Dress Shirts">
<link rel="chapter" href="/products" title="Products">
<link rel="chapter" href="/about" title="About Us">
<link rel="chapter" href="/feedback" title="Feedback">
<link rel="subsection" href="/products/men" title="Men">
```

![](img/222e7e58871b088cc6397852e1452b57_373_0.png)

以下是在视图脚本中使用此方法的示例：

```php
<?php
echo $this->navigation()
    ->sitemap()
    ->setFormatOutput(true)
    ->setMaxDepth(1);
?>
```

图 11-5 有一个输出示例。

# 第 11 章：与用户界面元素交互

## 尝试 11-1 添加导航菜单

现在你已经了解了一点 `ZendNavigation` 的工作原理，让我们在 SQUARE 示例的上下中使用它。鉴于应用程序只有一个单级菜单，这并不构成太大挑战；但它仍然很好地说明了你在实际场景中可能如何使用 `ZendNavigation`。

### 定义导航页面和容器

第一步是定义导航容器并将页面挂载到其上。如前面的章节所述，表达这些信息最简单的方法之一是 XML 文件。因此，请在文本编辑器中创建一个新文件，并填充以下数据：

```xml
<?xml version="1.0" encoding="UTF-8"?>
```

# 第 11 章：使用用户界面元素 359

```php
<?php
// 代码贡献：Ryan Mauer，技术编辑
class Square_Controller_Action_Helper_Navigation extends
Zend_Controller_Action_Helper_Abstract
{
    protected $container;

    // 构造函数，设置导航容器
    public function __construct(Zend_Navigation $container = null)
    {
        if (null !== $container) {
            $this->container = $container;
        }
    }

    // 检查当前请求并设置活动页面
    public function preDispatch()
    {
        $this->getContainer()
            ->findBy('uri', $this->getRequest()->getUri())
            ->active(true);
    }

    // 获取导航容器
    public function getContainer()
    {
        if (null === $this->container) {
            $this->container = Zend_Registry::get('Zend_Navigation');
        }
        if (null === $this->container) {
            throw new RuntimeException('Navigation container unavailable');
        }
        return $this->container;
    }
}
```

此定义设置了一个新的助手，从应用程序注册表中获取 `Zend_Navigation` 容器，并使用容器的 `findBy()` 方法将当前请求 URL 与容器中的页面链接进行匹配。如果找到匹配项，则将相应的页面标记为活动（active）。由于将其放置在助手的 `preDispatch()` 中，此任务会在每次请求时执行。

## 使用 Menu 视图助手

我们为什么需要标识活动页面呢？这些信息对于 Menu 视图助手非常有用，它会在渲染时为相应的主菜单分支附加“active” CSS 类。这使得在任何时候都能在视觉上（并自动地）高亮活动菜单项。



要查看效果，请通过更新`$APP_DIR/application/layouts/master.php`处的主布局文件来使用`Menu`视图助手并动态生成主菜单，更改部分已用**加粗**显示：

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">

  <div id="menu">
    <?php echo $this->navigation() ->menu(); ?>
  </div>

</</html>
```

此时你还需要更新主布局样式表，并为动态生成的菜单和活动菜单项添加样式表规则。你可以在本章的代码存档中找到相应的样式表，可以从本书书的配套网站 http://www.zf-beginners-guide.com 下载。

当你访问应用程序首页并选择一个特定的主菜单项时——例如 http://square.localhost/contact 处的联系表单——你会发现相应的主菜单项现在会自动高亮显示。然后，查看幕后工作，你会发现`Zend_Navigation`的`Menu`视图助手已经为你动态生成了主菜单。

图 11-6 展示了渲染后的输出。

图 11-6 自动生成并高亮的导航菜单

## 使用 Dojo Toolkit

Dojo Toolkit 是一个跨浏览器 JavaScript 库，它包含了用于 AJAX 请求和响应的数据访问层（Dojo Data）以及一组预定义的用户界面组件（Dijit）。这些组件包括布局和菜单元素、数据网格、对话框、自动完成输入和数据选择器表单控件以及各种动画页面效果。该项目得到了 Web 领域大公司的支持，包括 Google、IBM、AOL 和 Sun Microsystems。

Zend Framework 使你能够轻松上手 Dojo Toolkit。Zend Framework 的完整版本带了完整的 Dojo 和 Dijit 接口组件，框架还包含一个`Zend_Dojo`组件，简化了在 Web 应用程序中激活和使用 Dojo Toolkit 的任务。该`Zend_Dojo`组件包含一个数据层实现、一个辅助设置 Dojo 环境的助手，以及一组用于在视图脚本中添加 Dojo/Dijit 功能的布局扩展。后续章节将详细讨论这些。

## 处理 Dojo Data

Dojo Toolkit 为客户端服务器的数据交换定义了统一格式，并提供了两个基本数据存储`dojo.data.ItemReadStore`和`dojo.data.ItemWriteStore`用于与数据交互。在最简单的情况下，这些数据表示为结构化的 JSON 对象，看起来如下：

```json
{
  "identifier":"name",
  "items": [
    {"name":"Agatha Christie"},
    {"name":"J. K. Rowling"},
    {"name":"Dan Brown"},
    {"name":"William Shakespeare"},
    {"name":"Dennis Lehane"}
  ]
}
```

`Zend_Dojo_Data`组件提供了一个面向对象的 API，用于构建此 JSON 表示、向其添加项、对其进行迭代并查询匹配。为了说明，请考虑以下列表，它产生的输出与之前的代码列表等效：

```php
<?php
class Sandbox_ExampleController extends Zend_ControllerAction
{
    public function dojoAction()
    {
        // 定义数据项
        $authors = array(
            'Agatha Christie', 'J. K. Rowling', 'Dan Brown',
            'William Shakespeare', 'Dennis Lehane'
        );
```

# 364 Zend Framework：初学者指南

```php
$element = $this->NumberSpinner('temp', 25, array(
  'min' => 12,
  'max' => 41,
  'places' => 2
));
$this->dojo()->setCdnBase(ZendDojo::CDN_BASE_AOL)
  ->addStyleModule('dijit.themes.tundra');
echo $this->dojo();
?>
</head>
<body class="tundra">
  <?php echo $element; ?>
</body>
</html>
```

此示例使用了`NumberSpinner`视图辅助器来生成一个 Dijit 数字表单控件。图 11-8 展示了由 Dojo 视图辅助器生成的标记标记。

| Dojo 视图辅助器 | 说明 |
|---|---|
| Button | 按钮 |
| CheckBox | 复选框 |
| ComboBox | 组合选择/文本输入 |
| ContentPane | 内容容器 |
| CurrencyTextBox | 货币输入 |
| DateTextBox | 日期选择器 |
| Editor | 富文本编辑器 |
| FilteringSelect | 带过滤的选取控件 |
| HorizontalSlider | 水平滑块 |
| NumberSpinner | 带有增量控制的数字输入 |
| StackContainer | 堆叠内容容器 |
| TabContainer | 标签页容器 |
| Textarea | 文本输入 |
| TextBox | 文本输入 |
| TimeTextBox | 时间选择器 |
| ValidationTextBox | 带验证器的器的文本输入 |
| VerticalSlider | 垂直滑块 |

**表 11-2 Zend Framework 包含的 Dojo 视图辅助器（非穷举列表）**

# 第 11 章：使用用户界面元素

```html
<style type="text/css">
<!--
@import "http://o.aolcdn.com/dojo/1.2.0/dijit/themes/tundra/tundra.css";
-->
</style>
<script type="text/javascript" src="http://o.aolcdn.com/dojo/1.2.0/dojo/xo.js"></script>
<script type="text/javascript">
//<!CDATA[[
dojo.require('dijit.form.NumberSpinner');
dojo.require('dojo,parser');
dojo.util.Ready(function(info) {
  dojo.forEach(zendbits, function(info) {
    var n = dojo.byId(info.id);
    if (null != n) {
      dojo.attr(n, dojo.mixin({id: info.id}, info.params));
    }
  });
  dojo.parser.parse();
});
var zendbits = [{"id":"temp","params":{"constraints":"min:12,max:41","places":2,"dojoType":"dijit.form.NumberSpinner"}}];
]]>
</script><input id="temp" name="temp" value="25" type="text" />
```

图 11-8 Dojo 视图辅助器自动生成的标记

## 使用 Dojo 表单元素

Dojo Toolkit 包含了许多现成部件，可以快速用于为 Web 表单添加常见功能：颜色选择器、WYSIWYG 文本编辑器、数字拨动器、自动完成文本输入、水平滑块控件等。`Zend_Form`经过扩展以支持这些额外元素，允许像使用普通的`Zend_Form_Element`实例一样使用它们。

表 11-3 列出了 Zend Framework 包含的 Dojo 特定表单部件列表。若要在表单中使用这些元素，请更新`Zend_Form`实例以扩展`Zend_Dojo_Form_Form`而不是`Zend_Form`，然后按照通常的方式附加`Zend_Form_Dojo_Element`元素。这里是一个示例，展示了如何创建一个带有选择器、文本编辑器、富文本编辑器和垂直滑块的 Web 表单：

```php
<?php
class Form_Example extends Zend_Dojo_Form
{
    public function init() {
        $this->setAction('/sandbox/example/form')
        ->setMethod('post')
        ->setOptions(array('class' => 'tundra'));

        // 创建富编辑器
        $message = new ZendDojo_Form_Element_Editor('message');
        $message->setLabel('Message:')
            ->setOptions(array(
                'width' => '150px',
                'height' => '100px'
            ));

        // 创建日期选择器
```

| 表单元素 | 说明 |
|---|---|
| ZendDojo_Form_Element_Button | 按钮 |
| ZendDojo_Form_Element_Checkbox | 复选框 |
| ZendDojo_Form_Element_ComboBox | 组合选择/输入 |
| ZendDojo_Form_Element_CurrencyTextBox | 货币输入 |
| ZendDojo_Form_Element_DateTextBox | 日期输入 |
| ZendDojo_Form_Element_DojoMulti | 复选框组 |
| ZendDojo_Form_Element_Editor | 富文本输入字段 |
| ZendDojo_Form_Element_FilteringSelect | 带过滤的选取控件 |
| ZendDojo_Form_Element_HorizontalSlider | 水平滑块 |
| ZendDojo_Form_Element_NumberSpinner | 带有增量控制的数字输入 |
| ZendDojo_Form_Element_NumberTextBox | 数字输入 |
| ZendDojo_Form_Element_PasswordTextBox | 密码输入 |
| ZendDojo_Form_Element_RadioButton | 单选按钮 |
| ZendDojo_Form_Element_Textarea | 文本输入 |
| ZendDojo_Form_Element_SubmitButton | 提交按钮 |
| ZendDojo_Form_Element_Textarea | 文本输入 |
| ZendDojo_Form_Element_TextBox | 文本输入 |
| ZendDojo_Form_Element_TimeTextBox | 时间输入 |
| ZendDojo_Form_Element_ValidationTextBox | 带有验证器的文本输入 |
| ZendDojo_Form_Element_VerticalSlider | 垂直滑块 |

**表 11-3 Zend Framework 包含的 Dojo 表单元素**

# 第 11 章：使用用户界面元素

```html
<style type="text/css">
<!--
@import "http://o.aolcdn.com/dojo/1.2.0/dijit/themes/tundra/tundra.css";
-->
</style>
<script type="text/javascript" src="http://o.aolcdn.com/dojo/1.2.0/dojo/xo.js"></script>
<script type="text/javascript">
//<!CDATA[[
dojo.require('dijit.form.NumberSpinner');
dojo.require('dojo,parser');
dojo.util.Ready(function(info) {
  dojo.forEach(zendbits, function(info) {
    var n = dojo.byId(info.id);
    if (null != n) {
      dojo.attr(n, dojo.mixin({id: info.id}, info.params));
    }
  });
  dojo.parser.parse();
});
var zendbits = [{"id":"temp","params":{"constraints":"min:12,max:41","places":2,"dojoType":"dijit.form.NumberSpinner"}}];
]]>
</script><input id="temp" name="temp" value="25" type="text" />
```

图 11-8 Dojo 视图辅助器自动生成的标记

## 使用 Dojo 表单元素

Dojo Toolkit 包含了许多现成部件，可以快速用于为 Web 表单添加常见功能：颜色选择器、WYSIWYG 文本编辑器、数字拨动器、自动完成文本输入、水平滑块控件等。`Zend_Form`经过扩展以支持这些额外元素，允许像使用普通的`Zend_Form_Element`实例一样使用它们。

表 11-3 列出了 Zend Framework 包含的 Dojo 特定表单部件列表。若要在表单中使用这些元素，请更新`Zend_Form`实例以扩展`Zend_Dojo_Form_Form`而不是`Zend_Form`，然后按照通常的方式附加`Zend_Form_Dojo_Element`元素。这里是一个示例，展示了如何创建一个带有选择器、文本编辑器、富文本编辑器和垂直滑块的 Web 表单：

```php
<?php
class Form_Example extends Zend_Dojo_Form
{
    public function init() {
        $this->setAction('/sandbox/example/form')
        ->setMethod('post')
        ->setOptions(array('class' => 'tundra'));

        // 创建富编辑器
        $message = new ZendDojo_Form_Element_Editor('message');
        $message->setLabel('Message:')
            ->setOptions(array(
                'width' => '150px',
                'height' => '100px'
            ));

        // 创建日期选择器
```

| 表单元素 | 说明 |
|---|---|
| ZendDojo_Form_Element_Button | 按钮 |
| ZendDojo_Form_Element_Checkbox | 复选框 |
| ZendDojo_Form_Element_ComboBox | 组合选择/输入 |
| ZendDojo_Form_Element_CurrencyTextBox | 货币输入 |
| ZendDojo_Form_Element_DateTextBox | 日期输入 |
| ZendDojo_Form_Element_DojoMulti | 复选框组 |
| ZendDojo_Form_Element_Editor | 富文本输入字段 |
| ZendDojo_Form_Element_FilteringSelect | 带过滤的选取控件 |
| ZendDojo_Form_Element_HorizontalSlider | 水平滑块 |
| ZendDojo_Form_Element_NumberSpinner | 带有增量控制的数字输入 |
| ZendDojo_Form_Element_NumberTextBox | 数字输入 |
| ZendDojo_Form_Element_PasswordTextBox | 密码输入 |
| ZendDojo_Form_Element_RadioButton | 单选按钮 |
| ZendDojo_Form_Element_Textarea | 文本输入 |
| ZendDojo_Form_Element_SubmitButton | 提交按钮 |
| ZendDojo_Form_Element_Textarea | 文本输入 |
| ZendDojo_Form_Element_TextBox | 文本输入 |
| ZendDojo_Form_Element_TimeTextBox | 时间输入 |
| ZendDojo_Form_Element_ValidationTextBox | 带有验证器的文本输入 |
| ZendDojo_Form_Element_VerticalSlider | 垂直滑块 |

**表 11-3 Zend Framework 包含的 Dojo 表单元素**



# 第 11 章：使用用户界面元素

## 使用 Dojo 表单元素

Dojo Toolkit 包含了许多现成部件，可以快速用于为 Web 表单添加常见功能：颜色选择器、WYSIWYG 文本编辑器、数字拨动器、自动完成文本输入、水平滑块控件等。`Zend_Form` 经过扩展以支持这些额外元素，允许像使用普通的 `Zend_Form_Element` 实例一样使用它们。

表 11-3 列出了 Zend Framework 包含的 Dojo 特定表单部件列表。若要在表单中使用这些元素，请更新 `Zend_Form` 实例以扩展 `Zend_Dojo_Form_Form` 而不是 `Zend_Form`，然后按照通常的方式附加 `Zend_Form_Dojo_Element` 元素。这里是一个示例，展示了如何创建一个带有选择器、文本编辑器、富文本编辑器和垂直滑块的 Web 表单：

```php
<?php
class Form_Example extends Zend_Dojo_Form
{
    public function init() {
        $this->setAction('/sandbox/example/form')
        ->setMethod('post')
        ->setOptions(array('class' => 'tundra'));

        // 创建富编辑器
        $message = new ZendDojo_Form_Element_Editor('message');
        $message->setLabel('Message:')
            ->setOptions(array(
                'width' => '150px',
                'height' => '100px'
            ));

        // 创建日期选择器
```

**表 11-3 Zend Framework 包含的 Dojo 表单元素**

| 表单元素 | 说明 |
|---|---|
| `ZendDojo_Form_Element_Button` | 按钮 |
| `ZendDojo_Form_Element_Checkbox` | 复选框 |
| `ZendDojo_Form_Element_ComboBox` | 组合选择/输入 |
| `ZendDojo_Form_Element_CurrencyTextBox` | 货币输入 |
| `ZendDojo_Form_Element_DateTextBox` | 日期输入 |
| `ZendDojo_Form_Element_DojoMulti` | 复选框组 |
| `ZendDojo_Form_Element_Editor` | 富文本输入字段 |
| `ZendDojo_Form_Element_FilteringSelect` | 带过滤的选取控件 |
| `ZendDojo_Form_Element_HorizontalSlider` | 水平滑块 |
| `ZendDojo_Form_Element_NumberSpinner` | 带有增量控制的数字输入 |
| `ZendDojo_Form_Element_NumberTextBox` | 数字输入 |
| `ZendDojo_Form_Element_PasswordTextBox` | 密码输入 |
| `ZendDojo_Form_Element_RadioButton` | 单选按钮 |
| `ZendDojo_Form_Element_Textarea` | 文本输入 |
| `ZendDojo_Form_Element_SubmitButton` | 提交按钮 |
| `ZendDojo_Form_Element_TextBox` | 文本输入 |
| `ZendDojo_Form_Element_TimeTextBox` | 时间输入 |
| `ZendDojo_Form_Element_ValidationTextBox` | 带有验证器的文本输入 |
| `ZendDojo_Form_Element_VerticalSlider` | 垂直滑块 |

## Dojo 视图辅助器

以下示例使用了 `NumberSpinner` 视图辅助器来生成一个 Dijit 数字表单控件：

```php
$element = $this->NumberSpinner('temp', 25, array(
  'min' => 12,
  'max' => 41,
  'places' => 2
));

$this->dojo()->setCdnBase(ZendDojo::CDN_BASE_AOL)
  ->addStyleModule('dijit.themes.tundra');

echo $this->dojo();
```

图 11-8 展示了由 Dojo 视图辅助器生成的标记：

```html
<style type="text/css">
<!--
@import "http://o.aolcdn.com/dojo/1.2.0/dijit/themes/tundra/tundra.css";
-->
</style>
<script type="text/javascript" src="http://o.aolcdn.com/dojo/1.2.0/dojo/xo.js"></script>
<script type="text/javascript">
//<!CDATA[[
dojo.require('dijit.form.NumberSpinner');
dojo.require('dojo,parser');
dojo.util.Ready(function(info) {
  dojo.forEach(zendbits, function(info) {
    var n = dojo.byId(info.id);
    if (null != n) {
      dojo.attr(n, dojo.mixin({id: info.id}, info.params));
    }
  });
  dojo.parser.parse();
});
var zendbits = [{"id":"temp","params":{"constraints":"min:12,max:41","places":2,"dojoType":"dijit.form.NumberSpinner"}}];
]]>
</script><input id="temp" name="temp" value="25" type="text" />
```

图 11-8 Dojo 视图辅助器自动生成的标记

**表 11-2 Zend Framework 包含的 Dojo 视图辅助器（非穷举列表）**

| Dojo 视图辅助器 | 说明 |
|---|---|
| `Button` | 按钮 |
| `CheckBox` | 复选框 |
| `ComboBox` | 组合选择/文本输入 |
| `ContentPane` | 内容容器 |
| `CurrencyTextBox` | 货币输入 |
| `DateTextBox` | 日期选择器 |
| `Editor` | 富文本编辑器 |
| `FilteringSelect` | 带过滤的选取控件 |
| `HorizontalSlider` | 水平滑块 |
| `NumberSpinner` | 带有增量控制的数字输入 |
| `StackContainer` | 堆叠内容容器 |
| `TabContainer` | 标签页容器 |
| `Textarea` | 文本输入 |
| `TextBox` | 文本输入 |
| `TimeTextBox` | 时间选择器 |
| `ValidationTextBox` | 带验证器的文本输入 |
| `VerticalSlider` | 垂直滑块 |

## 配置 Dojo

```php
protected function _initDojo() {
    // get view resource
    $this->bootstrap('view');
    $view = $this->getResource('view');

    // add helper path to view
    Zend_Dojo::enableView($view);

    // configure Dojo view helper, disable
    $view->dojo() -setCdnBase(Zend_Dojo::CDN_BASE_AOL)
        --addStylesheetModule('djit.themes.tundra')
        --disable();
}
```




此方法从资源插件中获取 `Zend_View` 实例，并使用 `Zend_Dojo::enableView` 方法为视图启用 Dojo 视图助手。随后它配置了 Dojo 环境，设置 CDN URL 和样式表，最后通过 `disable()` 方法禁用该助手。这样做的结果是：Dojo 视图助手已完成配置，但除非显式调用视图助手的 `enable()` 方法，否则 Dojo Toolkit 库将不会加载到视图脚本中。

### 更新主布局

下一步是更新布局以检查是否启用了 Dojo 视图助手，如果是，则加载 Dojo 环境。这并不困难，下面的对 `$APP_DIR/application/layouts/master.php` 布局中 `<head>` 标签的补充说明所示：

```html
<!DOCTYPE html PUBLIC "//W3C//DTD HTML 1.0 Strict//EN"
"http://www.w3.org/TR/html11/html1-strict.dtd">

<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">

<head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
    <base href="/ />
    <link rel="stylesheet" type="text/css" href="css/master.css" />

    <?php if ($this->dojo()->isEnabled()) {
        echo $this->dojo();
    } ?>
</head>

<body class="tundra">
</body>

</html>
```

# 第 11 章：与用户界面元素交互 371

### 更新控制器

最后一步是更新 `ContactController` 并为自动补全输入定义端点。以下是代码，应添加到 `$APP_DIR/application/modules/default/controllers/ContactController.php` 中：

```php
<?php

class ContactController extends Zend_Controller_Action {
    public function autocompleteAction() {
        // disable layout and view rendering
        $this->_helper->layout->disableLayout();
        $this->getHelper('viewRenderer')->setNoRender(true);

        // get country list from Zend_Locale
        $territories = Zend_Locale::getTranslationList('territ', null, 2);

        $items = array();

        foreach ($territories as $t) {
            $items[] = array('name' => $t);
        }

        // generate and return JSON string compliant with dijo.data structure
        $data = new Zend_Dojo_Data('name', $items);

        header('Content-Type: application/json');
        echo $data->toJson();
    }
}
```

此方法使用我们之前讨论过的 `Zend_Dojo_Data` 组件，将包含国家列表的数组转换为期望的 JSON 格式，并将其返回给请求客户端。

要查看此效果，请通过 `http://square.localhost/contact` 访问 SQUARE 应用，你应该看到一个新的国家名称文本输入框。在该字段中输入几个字符，Dojo 将请求并展示从上一节定义的 `ViewController::autocompleteAction` 获取的匹配建议列表。

图 11-10 展示了你可能会看到的示例。

# 联系方式

名称：

电子邮件地址：

国家

| 安道尔 |
| --- |
| 安提瓜和巴布达 |
| 安吉拉 |
| 安哥拉 |
| 南极洲 |

图 11-10 运行中的 Dojo ComboBox

## Zend Framework：初学者指南

# 尝试 11-3 添加 YUI 日历组件

在上一节中，你已经看到在 Zend 应用中添加 Dojo 组件是多么简单。然而，Dojo 并不是唯一的选择，集成来自其他客户端编程工具包的组件和库同样简单。接下来的部分将阐述如何向 Zend 实例添加一个来自 Yahoo! 用户界面库（YUI）的弹出日历组件。

在本例中，目标表单是第 5 章中首次定义的 `ItemUpdate` 表单，它允许管理员调整目录条目属性和显示状态。在本示例中，我们将更新表单，使用 YUI 的图形化日历组件进行单次日期输入，而不是显示日、月、年的选择列表。

为了本示例的这些：

### 更新表单

第一步是更新表单，创建一个包含日历组件的新元素，并移除之前的选择列表。以下是修改后的定义，应保存到 `$APP_DIR/library/Square/Form/ItemUpdate.php`。

```php
<?php

class Square_Form_ItemUpdate extends Square_Form_ItemCreate
{
    public function init()
    {
        // get form
    }
}
```

# 第 11 章：与用户界面元素交互 375

```html
...
</body>
</html>
```

### 更新控制器

下一步是更新 `Catalog_AdminItemController::updateAction` 方法，进行以下两处更改：

- 使用 `HeadLink` 和 `HeadScript` 视图辅助函数为 YUI 日历小部件指定源 JavaScript 和 CSS 文件。
- 调整代码以使用日历小部件提供的日期字符串，而不是当前选择列表提供的三个独立值（月份、日期和年份）。

以下是修改后的代码：

```php
<?php

class Catalog_AdminItemController extends Zend_Controller_Action
{
    // 用于修改单个目录项的 action

    public function updateAction()
    {
        // 加载 JavaScript 和 CSS 文件
        $this->view->headlink()->appendStylesheet(
            'http://ui.yahoo.com/combo2.8.0.r4/build/calendar/assets/skins/sam/calendar.css'
        );

        $this->view->headScript()->appendFile('/js/form.js');

        $this->view->headScript()->appendFile(
            'http://ui.yahoo.com/combo2.8.0.r4/build/yahoo-dom-event/yahoo-dom-event.js&2.8.0.r4/build/calendar/calendar-min.js'
        );

        // 生成输入表单
        $form = new Square_Form_ItemUpdate;
        $this->view->form = $form;

        if ($this->getRequest()->isPost()) {
            // 如果是 POST 请求
            // 测试输入是否有效
            // 获取当前记录
            // 更新值并替换数据库内容

            $postData = $this->getRequest()->getPost();

            // 注释日期调整
            // $postData['DisplayUntil'] = sprintf('%04d-%02d-%02d',
            //     $this->getRequest()->getParam('DisplayUntil_year',
            //     $this->getRequest()->getParam('DisplayUntil_month'),
            //     $this->getRequest()->getParam('DisplayUntil_day')
            // );

            if ($form->isValid($postData)) {
                $input = $form->getValues();

                $item = Doctrine::getTable('Square_Model_Item')
                    ->findArray($input['RecordID']);

                $item->fromArray($input);

                $item->DisplayUntil = ($item->getStatus() == 0)
                    ? null
                    : $item->DisplayUntil;

                $item->save();

                $this->_helper->getHelper('FlashMessenger')
                    ->addMessage('The record was successfully updated.');

                $this->_redirect('/admin/catalog/item/success');
            }
        } else {
            // GET 请求
            // 为 GET 输入设置过滤器和验证器
            // 如果输入有效
            // 获取请求的记录
            // 预填充表单

            $filters = array(
                'id' => array('HtmlEntities', 'StripsTags', 'StringTrim')
            );

            $validators = array(
                'id' => array('NotEmpty', 'Int')
            );

            $input = new Zend_Filter($filters, $validators);
            $input->setData($this->getRequest()->getParams());

            if ($input->isValid()) {
                $q = Doctrine_Query::create()
                    ->from('i.Square_Model_item', 'i')
                    ->leftJoin('i.Square_Model_Country', 'c')
                    ->leftJoin('i.Square_Model_Grade', 'g')
                    ->leftJoin('i.Square_Model_Type', 't')
                    ->where('i.RecordID = ?', $input->id);

                $result = $q->fetchArray();

                if (count($result) == 1) {
                    // 注释日期调整
                    $date = $result[0]['DisplayUntil'];
                    $result[0]['DisplayUntil_day'] = date('d', strtotime($date));
                    $result[0]['DisplayUntil_month'] = date('m', strtotime($date));
                    $result[0]['DisplayUntil_year'] = date('Y', strtotime($date));

                    $this->view->form->populate($result[0]);
                } else {
                    throw new Zend_Controller_Exception('Page not found', 404);
                }
            } else {
                throw new Zend_Controller_Action_Exception('Invalid input');
            }
        }
    }
}
```

### 更新视图

最后，需要少量 JavaScript 来初始化视图脚本，该文件位于 `$APP_DIR/application/modules/admin/views/scripts/admin-item/update.php`。

```html
<h2>更新条目</h2>

<?php echo $this->view; ?>

<script type="text/javascript">
handleInputOnSelect('DisplayStatus', 'divDisplayUntil', new Array('1'));

cal = YAHOO.widget.Calendar('cal', 'divCalendar', {close:true});

cal.render();

YHOO.util.addEventListener('DisplayUntil', 'click', cal.show, cal, true);

cal.SelectEvent.subscribe(handleSelect, cal, true);

function handleSelect(type, args, obj) {
    var dates = args[0];
    var date = dates[0];
    var year = date[0];
    var month = date[1];
    var day = date[2];
}
```

## 专家提问

**问：为什么你不在视图中为 YUI JavaScript 和 CSS 文件指定“硬”链接？**

**答：因为在视图布局中指定这些文件会导致在每个页面都请求它们，增加了不必要的开销。只有在需要时才加载它们才能获得更好的用户体验。**

# 第 12 章：优化性能

## 关键技能与概念

- 熟悉应用程序基准测试工具
- 理解缓存的益处和类型
- 了解如何缓存 Web 服务响应和 RSS 馈
- 学习优化数据库查询的各种技术

在过去的几年里，Web 应用变得日益复杂，引入了 AJAX 用户界面、流媒体和动态生成的内容，以吸引并留住游客。随着应用程序变得复杂，它们对动态数据的依赖性增加，随着每秒处理请求量的增加，性能首先受到影响。然而，有许多常用方法可以识别并绕过代码性能瓶颈。代码分析、缓存、重构和延迟加载等技术可以减轻服务器负载并提高响应速度。Zend Framework 提供了许多此类任务工具，本文将介绍其中。

## 分析性能

在开始微调 Web 应用之前，你需要详细了解应用程序哪些部分的性能下降。存在许多用于基准测试和分析的工具，接下来的章节将介绍它们。

### 基准测试

ApacheBench（简称 `ab`）是一种用于基准测试 Web 服务器响应时间的工具。它通过向服务器发送多个并发请求并计时响应，生成不同负载下的详细统计数据。ApacheBench 是 Apache 服务器发行的一部分，适用于 Windows 和 *NIX 平台。尽管它是 Apache 的一部分，但也可以用于基准测试任何符合 HTTP 标准的服务器。

以下是使用 ApacheBench 基准测试 Web 应用的示例，模拟每次发送 10 个请求 1000 次：

```shell
ab -n 1000 -c 10 http://server/request/url
```





图 12-1 展示了 ApacheBench 生成的输出报告示例。

## 第 12 章：优化性能

| 192.168.1.4 - PuTTY |
|---|
| 文档路径：`/catalog/item/search?q=fine` |
| 文档长度：3808 字节 |
| 并发级别：10 |
| 测试耗时：204.728 秒 |
| 完成请求数：1000 |
| 失败请求：0 |
| 写入错误：0 |
| 总传输量：4197000 字节 |
| HTML 传输量：380800 字节 |
| 每秒请求数：4.88 `[#sec]`（平均） |
| 每个请求时间：2047.290 `[ms]`（平均） |
| 每个请求时间：204.728 `[ms]`（平均，跨并发请求） |
| 传输速率：接收 20.02 `[Bytes/sec]` |

| 连接时间 `[ms]` | 最小 | +/- 标准差 | 中位数 | 最大值 |
|---|---:|---:|---:|---:|
| 连接 | 0 | 1 | 0.5 | 10 |
| 处理 | 988 | 2041 | 826.6 | 1699 | 5166 |
| 等待 | 987 | 2041 | 826.5 | 1698 | 5165 |
| 总计 | 968 | 2041 | 826.6 | 1700 | 5166 |

在特定时间内（ms）完成的请求百分比：

- 50% 1785
- 66% 2936
- 80% 3043
- 90% 3255
- 95% 3474
- 98% 3813
- 100% 5166（最长请求）

`root@aphrodite:/tmp#`

图 12-1 ApacheBench 汇总统计

如图 12-1 所示，该报告提供了关于服务器响应特定 URL 请求所需平均秒数的有用信息。在其他应用程序请求上运行类似的测试，可以准确地描述应用程序的哪些部分是“慢的”，并且可以从优化中获益。

ApacheBench 的替代方案是微软 Web 容量分析工具（WCAT）。与 ApacheBench 类似，该工具模拟对 Web 服务器的负载，返回测量的吞吐量和响应时间数据。尽管它仅适用于 Windows 平台，但它具有一些有趣的特性：它可以同时从多个客户端系统运行，并且可以对必须按特定顺序执行多个请求“事务”进行基准测试。

这是一个使用 WCAT 对 Web 应用进行基准测试的示例：

```shell
wcat.ws -terminate -run -clients localhost -t scenario.ubr -f settings.ubr -s -singleip -extended
```

图 12-2 展示了一个 WCAT 输出报告示例。

## Web 容量分析工具

计算机：192.168.1.2  
构建版本：  
收集时间：2010/2/15 23:46:18  
标题：

| 内容 | 摘要 |
|---|---|
| 警告 | 事务/秒 |
|  | 8.90 |
| 总体统计 | 路径长度/事务 |
| - 网络统计 |  |
| - 时间分析 |  |
| - 响应时间分析 |  |
| - 请求/响应统计 | 上下文切换/事务 |
| - HTTP 状态码 | 0.00 |
| - 事务统计 |  |
| - 错误 | 请求/秒 |
|  | 8.90 |
| 每个客户端统计 | 路径长度/请求 |
| - 时间分析（首次字节传输时间） | 上下文切换/请求 |
| - 响应时间分析（最后一个字节传输时间） | 0.00 |
| - 网络统计 | 处理器时间 % |
| - 请求/响应统计 | 0.00 |
| - HTTP 状态码 |  |
| - 错误 |  |
| 常规信息 | Mbits/sec |
| - 服务器信息 | 0.08 |
| - 测试设置 | 总错误数 |
|  | 0 |

图 12-2 一份 WCAT 基准测试报告

### 代码分析（Code Profiling）

一旦你获得了一些相关的数字并确定了改进区域，下一步是对相关的控制器和操作进行性能分析（profile），并理解瓶颈在哪里。用于此任务最流行的工具之一是 PHP 的 Xdebug 扩展，它适用于 Windows 和 `*NIX*` 版本的 PHP。

Xdebug 性能分析器会生成关于脚本中每个调用花费的时间，以及脚本编译和执行总耗时的详细统计。这些统计数据使得人们可以看到哪些函数调用产生了最大的处理开销，从而识别出潜在的优化区域。Xdebug 扩展还覆盖了 PHP 默认的异常处理程序，为致命和非致命错误提供了更详细的调试输出和堆栈跟踪。

图 12-3 在 Webgrid 中查看 Zend Framework 请求的 Xdebug 分析

一旦配置完成，Xdebug 将自动对通过 PHP 解释器执行的每个脚本进行性能分析。分析报告格式为 cachegrind 文件，可以使用许多开源工具查看，例如 WinCacheGrind（Windows 桌面）、KCacheGrind（NIX 桌面）或 Webgrid（PHP Web 应用）。分析文件存储在 `php.ini` 配置文件中 `xdebug.output_dir` 变量指定的输出目录。

图 12-3 展示了分析文件可能的样式。

这种类型的分析信息对于理解非常有用，例如，哪些方法调用或框架组件占据了大部分处理时间，因此是优化或通过其他库替换的合理目标。

### 注意

PHP 的 Xdebug 扩展以通常的方式安装在 PHP 的 `ext/` 目录下，并通过在 `php.ini` 配置文件中添加 `xdebug.extension_ts=/path/to/xdebug/` 指令来激活。你必须在配置文件中指定 `xdebug_profiler_enable`、`xdebug.output_dir` 和 `xdebug.trace_output_dir` 变量。详细安装说明请参见本章末尾 Xdebug 网站链接。

Xdebug 的替代方案是 PEAR Benchmark 类，它提供了一个对函数调用进行基准测试的 API。在这种情况下，基准测试工具嵌入特定的操作中，将操作代码封装在其 `start()` 和 `stop()` 方法的调用中。这些方法通常在操作的开始和结束时调用，尽管它们也可以用于对操作的子部分进行基准测试。

这些标记（markers）包含在报告中，因为它们可以帮助识别脚本承担的百分比。这里是你可能使用它的示例：

```php
$profiler = new Benchmark_Profiler();

$profiler->start();

// profile setup

$filters = array(
    'Html', 'StringTags', 'Trim',
);

$input = new Zend_Filter_Input($filters);
$input->setData($this->getRequest()->getParams());

$profiler->leaveSection("Setup");

// profile validation

$profiler->enterSection("Validate");

$check = $input->isValid();

$profiler->leaveSection("Validate");

// profile database

if ($check) {
    $profiler->enterSection("Query");

    $db = $this->getResource('database');

    $sql = "SELECT * FROM city AS ci,
            country AS co,
            countryLanguage AS cl
            WHERE ci.CountryCode = co.Code AND
                cl.Language = 'English' AND
                cl.IsOfficial = 'T'";

    $result = $db->fetchAll($sql);

    $this->view->records = $result;

    $profiler->leaveSection("Query");
}

$profiler->stop();

$this->view->profile = $profiler->getOutput('html');
```

图 12-4 PEAR 生成的分析数据示例

### 提示

PEAR Benchmark 类与其他 PEAR 类一样，默认不支持 Zend Framework 自动加载。要使其与 Zend Framework 自动加载兼容，请使用 PEAR 安装器安装，检查 PEAR 目录在 PHP 路径中，然后将行添加到应用程序文件中。

### 查询分析（Query Profiling）

Xdebug 和 PEAR Benchmark 对 PHP 代码分析非常有用，但它们无法提供关于 Web 应用常见瓶颈的信息：应用程序与数据库之间的交互。在任何分析工作中，都需要对应用程序的数据库查询进行分析，并理解哪里可以优化。如果你使用 `Zend_Db` 进行数据库查询，可以使用 `Zend_Db_Profiler` 组件对其进行分析，它可以检查应用程序查询并获取每个查询通过时间的报告。

| 总执行时间 | 净执行时间 | 调用次数 | 百比 | 调用者 |
|---|---:|---:|---:|---|
| Setup | 0.00324702622878 | 0.00324702622878 | 1 | 7.01% | Global (1) |
| Validate | 0.00511384010315 | 0.00511384010315 | 1 | 11.03% | Global (1) |
| Query | 0.03779387474406 | 0.03779387474406 | 1 | 81.54% | Global (1) |
| Global | 0.0463509559631 | 0.0001926218490601 | 1 | 100.00% | Setup (1), Validate (1), Query (1) |

图 12-4 一个 Zend Framework 请求的 PEAR Benchmark 分析

## 使用 Zend_Db_Profiler

使用 `Zend_Db_Profiler` 将其挂载到应用启动器的 `Zend_Db` 实例的最简单方法如下：

```php
<?php

class Bootstrap extends Zend_Application_Bootstrap_Bootstrap
{
    protected function _initDatabase()
    {
        $db = new Zend_Db_Adapter_Pdo_Mysql(array(
            'host' => '127.0.0.1',
            'username' => 'user',
            'password' => 'pass',
            'dbname' => 'world'
        ));

        $profiler = new Zend_Db_Profiler();
        $profiler->setEnabled(true);
        $db->setProfiler($profiler);

        return $db;
    }
}
```

可以通过 `Zend_Db_Profiler` 对象的 `getQueryProfiles()` 方法获取分析器捕获的查询。该方法返回一个包含 `QueryProfile` 对象的数组，每个对象都暴露了 `getQuery()` 和 `getElapsedSecs()` 方法，分别用于查询字符串和查询执行时间。以下是从这些方法检索配置数据的示例：

```php
<?php

class Sandbox_ExampleController extends Zend_Controller_Action
{
    public function queryAction()
    {
        // 获取数据库适配器
        $db = $this->getInvokeArg('bootstrap')->getResource('database');

        // 执行查询
        $sql = "SELECT * FROM city ci,
                country AS co,
                countrylang AS cl
                WHERE
                ci.Code = co.Code AND
                cl.CountryCode = co.Code AND
                cl.Language = 'English' AND
                cl.IsOfficial = 'T' AND
                co.Continent LIKE '%%%input->q%%";

        $result = $db->fetchAll($sql);

        $this->view->records = $result;
        $this->view->profiles = array();
    }

    // 获取查询配置数据
    foreach ($db->getProfiler()->getQueryProfiles() as $profile) {
        $this->view->profiles[] = array(
            'sql' => $profile->getQuery(),
            'time' => $profile->getElapsedSecs(),
        );
    }
}
```

图 12-5 展示了上述列表生成的配置数据示例。还有一个专门的 `Zend_Db_Profiler_Firebug` 扩展，它可以将查询分析数据直接发送到 Firefox 控制台。要进行此更新，使用应用启动器使用此扩展，如下：

```php
class Bootstrap extends Zend_Application_Bootstrap_Bootstrap
{
    protected function _initDatabase()
    {
        $db = new Zend_Db_Adapter_Pdo_Mysql(array(
            'host' => '127.0.0.1',
            'username' => 'user',
            'password' => 'pass',
            'dbname' => 'world'
        ));

        $profiler = new Zend_Db_Profiler_Firebug('Query log');
        $profiler->setEnabled(true);
        $db->setProfiler($profiler);

        return $db;
    }
}
```

图 12-5 由 `Zend_Db_Profiler` 生成的查询配置输出




图 12-6 展示了由 `Zend_Db` 分析器生成的 Firebug 控制台输出示例。Zend Framework 不包含基于 Doctrine 的数据库查询的内置分析器，但可以通过来自 Imprint 的第三方组件轻松地添加此功能。该项目包含了许多针对 Zend Framework 的 Doctrine 特有扩展，其中之一是 `Imind_Profiler_Firebug` 组件。该组件将 Doctrine 查询记录到 Firebug（Firefox 浏览器调试器）控制台，使得实时测量性能成为可能。要使用 Imprint 分析器分析 Doctrine 查询，请在应用启动器中将配置挂载到 Doctrine 连接管理器，如下：

```php
<?php

class Bootstrap extends Zend_Application_Bootstrap_Bootstrap
{
    protected function initDoctrine()
    {
        require_once 'Doctrine/Doctrine.php';
    }
}
```

![](img/222e7e58871b088cc6397852e1452b57_408_0.png)

图 2-6 由 `Zend_Db_Profiler` 生成的查询配置输出，如 Firebug 控制台所示

## 第 12 章：优化性能

```php
$this->getApplication()->getAutoloader()
    ->pushAutoloader(array('Doctrine', 'autoload'), 'Doctrine');

$manager = Doctrine_Manager::getInstance(
    Doctrine::ATTR_MODEL_LOADING,
    Doctrine::CONSERVATIVE
);

$config = $this->getOption('doctrine');
$conn = Doctrine_Manager::getInstance($config['dsn'],

$profiler = new Imind_Profiler_Firebug();
$conn->setListener($profiler);

return $conn;

}
```

由于上述添加，所有 Doctrine 查询都将被自动分析并显示在 Firebug 控制台中。图 12-7 展示了上述列表生成的配置数据示例。

## 注意

确保 Web 出现性能瓶颈的最快方法之一是使用缓存。你可能会问缓存是什么？简单来说，缓存是一个包含频繁请求信息的中间位置。每当对其中一个片段提出请求时，系统将从中提取并返回副本，这比从源生成信息要快得多。

缓存可以根据需要维护在不同层次。许多人不知道，最常用的缓存机制是浏览器本身。浏览器在渲染内容之前将其下载到硬盘上的临时位置。如果你再次访问同一页面，浏览器将从本地缓存读取（除非你配置了它）。

在你的工作中，你的 Internet 连接很可能通过代理服务器连接到大量用户。聪明的网络管理员通常使用代理服务器缓存来保存频繁页面的副本。对此类页面的后续请求将由代理服务器直接服务。这种系统在不同的层次上都有复制；发现 ISP 缓存内容以减少我们在骨干网上的带宽成本并不罕见。

最后，网站通常经常实现缓存系统来提供自己的内容。最简单的形式是向客户端发送动态页面的静态“快照”，而不是每次请求都重新渲染页面。这减轻了负载并为其他任务释放了资源。定期重新生成快照以确保其新鲜性。

### 缓存数据

Zend Framework 包含一个 Cache 组件，它提供了一个全面的 API 用于从缓存中存储和检索数据。这些数据可能包括数据库结果集、函数或方法的返回值、对象、静态文件或渲染后的页面输出。缓存本身可以实现为磁盘存储或内存存储；`Zend_Cache` 支持多种不同的存储方式，包括平面文件、SQLite 数据库、memcached 服务器和 APC 码缓存。

每个缓存都有两个关键属性：寿命（lifetime）和唯一标识符（identifier）。

- 寿命值（通常以秒为单位）表示缓存条目被认为“有效”或“新鲜”的期限。一旦过了这段时间，缓存就会变得“过期”，并且必须从原始数据源重新生成。
- 由于单个缓存可以包含多个条目，因此每个条目都必须是一个唯一标识符。该标识符作为缓存条目的标记，并用于检索缓存数据。

为了说明其工作原理，请考虑以下示例：

```php
<?php

class SandboxExampleController extends Zend_Controller_Action
{
    public function cacheAction()
    {
        // define cache configuration

        $front = array(
            'lifetime' => 600,
            'automatic_serialization' => true
        );

        $back = array(
            'cache_dir' => APPLICATION_PATH . '../tmp/cache'
        );

        // initialize cache if available
        $cache = Zend_Cache::factory('Core', 'File', $front, $back);

        // use cache if available
        if ($this->view->records = $cache->load('cities')) {
            // set query
            $sql = "SELECT * FROM city AS ci,
                    country AS co,
                    countrylanguage AS cl
                    WHERE
                    ci.CountryCode = co.Code AND
                    cl.Country = co.Code AND
                    cl.Language = 'English' AND
                    cl.IsOfficial = 'T'";
        }

        // get database adapter
        $db = $this->invokeArg('bootstrap')->getResource('database');

        // execute query and save results to cache
        $result = $db->fetchAll($sql);
        $cache->save($result, 'cities');
        $this->view->records = $result;
    }
}
```

此代码列表开始使用 `Zend_Cache::factory()` 初始化一个新的 `Zend_Cache` 实例。该方法接受缓存前端（frontend）和后端（backend）的名称，以及每个后端的配置选项数组。之前的示例使用了 `Core` 前端（这是可用的最简单的 `Zend_Cache` 前端）以及 `File` 后端（它将缓存条目存储为磁盘文件）。这些各项的配置选项（例如每个缓存条目的有效秒数以及缓存文件的目录位置）都是以关联数组的形式指定的。`Zend_Cache::factory()` 的返回值是一个配置正确的 `Zend_Cache` 实例。

缓存利用的基本逻辑非常简单，如图 12-8 所示的流程图所示。这种业务逻辑在之前的代码列表中得到了说明，该代码缓存了数据库查询的结果。代码首先检查缓存中是否存在所需的结果。如果存在，则直接将其赋值给视图，而无需涉及数据库服务器。

![](img/222e7e58871b088cc6397852e1452b57_412_0.png)

图 12-8 缓存操作流程图

如果不存在，则在数据库上执行查询以获取所需数据，并将结果的副本保存到缓存中。这些缓存数据随后将用于后续请求，直到它们过期并需要重新生成。

检查缓存中是否存在数据通过 `load()` 方法完成，将数据写入缓存则通过 `save()` 方法完成。注意，这两个方法都需要唯一的缓存标识符，在之前的代码列表中，该标识符是字符串 `'city'`。`save()` 方法还允许你通过可选的第三参数定义过期寿命（以秒为单位）；如果存在，此值将覆盖前端配置选项中指定的默认值。

> **提示**
>
> 许多 Zend Framework 组件（包括 `Zend_Translate`、`Zend_Db` 和 `Zend_Reader`）可以传递配置好的 `Zend_Cache` 实例，它们将自动使用此缓存来存储相关的元数据或查找信息。你将在本章稍后的部分看到相关的示例。

### 理解缓存前端和后端

如上一节所述，`Zend_Cache` 提供了许多不同的缓存前端和后端，每种都为不同的目的设计。表 12-1 和表 12-2 提供了列表。

几个示例对于说明如何在 MVC 应用中使用它们非常有用。例如，考虑 `Class` 和 `Function` 前端，它们使得缓存计算密集型过程变得可能，从而减少服务器负载。这里是 `Class` 运行的示例：

```php
<?php

class Sandbox_ExampleController extends Zend_Controller_Action
{
    public function cacheAction()
    {
        // define cache configuration
    }
}
```

| 缓存前端 | 描述 |
|---|---|
| Core | 通用基础缓存实现 |
| Class | 缓存方法的返回值 |
| Function | 缓存函数的返回值 |
| File | 缓存磁盘文件 |
| Capture | 缓存渲染后的页面输出或输出块 |
| Page | 缓存渲染后的页面输出 |

**表 12-1** Zend Framework 包含的缓存前端

| 缓存后端 | 描述 |
|---|---|
| Apc | 将条目缓存到 APC |
| File | 将条目缓存为磁盘文件 |
| Memcached | 将条目缓存到 memcached |
| SQLite | 在 SQLite 中缓存条目 |
| Static | 将条目缓存为静态 HTML |
| Two_Levels | 在两个位置缓存条目 |
| XCache | 使用 XCache 缓存条目 |
| ZendServer | 使用 Zend 服务器缓存条目 |
| Blackhole | 缓存条目的存根实现 |
| Test | 预定义的缓存实现 |

**表 12-2** Zend Framework 包含的缓存后端

```php
$front = array(
    'lifetime' => 600,
    'automatic_serialization' => true,
    'servers' => array(
        array(
            'host' => 'localhost',
            'port' => 1211,
            'timeout' => 5,
            'retry_interval' => 15,
        )
    )
);

$back = array();

// initialize cache
$cache = Zend_Cache::factory('Memcached', $front, $back);

// 使用缓存对象执行方法调用
$this->view->result = $cache->findCheapestProvider(100, 33.6, 1, 'NY');
```

在大多数情况下，这是一个涉及大量查询和 Web 服务调用的耗时过程。因此，缓存该方法的输出是有意义的，这样具有相同指的重复查询就可以从缓存中检索。这里是另一个使用 `File` 前端配合 `APC` 后端的示例：

```php
<?php

Sandbox_ExampleController extends Zend_Controller_Action
{
    public function cacheAction()
    {
        // 定义主文件
        $localConfigFile = APPLICATION_PATH . '/configs/my.ini';

        // 定义缓存配置
        $front = array(
            'lifetime' => 600,
            'automatic_serialization' => true,
            'master_files' => array($localConfigFile)
        );

        $back = array();

        // 初始化缓存
        // 从缓存加载主文件
        $cache = Zend_cache::factory('File', 'Apc', $front, $back);

        if (!$config = $cache->load('localconfig')) {
            if (file_exists($localConfigFile)) {
                $config = new Zend_Config_Ini($localConfigFile);
                $cache->save($config, 'localconfig');
            }
        }
    }
}
```

此示例将指定的此类文件自动缓存到 APC 共享内存中，并在后续请求中使用它。这里需要注意的是，`File` 前端会自动检测主文件的任何变化，并且当此类变化发生时，它会使缓存失效并在下次请求时重新创建。

> **注意**
>
> `Static` 后端非常有趣，因为它将渲染后的页面保存为磁盘上的静态 HTML 文件。这些文件可以响应请求而被提供，完全跳过 PHP，从而大幅提高性能。使用此后端需要对服务器的 URL 重写规则进行任何修改，但结果通常是值得的，特别是对于高流量 URL 而言。Zend Framework 手册提供了关于如何使用此后端的详细示例，以及可以根据不同场景扩展的示例重写规则。

### 使用管理器（Cache Manager）

在大多数情况下，缓存会在应用程序引导程序（bootrapper）中进行配置和初始化，并通过 `Zend_Registry` “导出”到整个应用程序中，以便在不同的动作（actions）中使用。然而，在许多情况下，需要根据被缓存数据的类型使用不同的缓存配置。例如，你可能希望将 RSS 和 Web 服务馈送缓存到磁盘文件中，而将频繁执行的查询结果存储在内存缓存中，因为从磁盘检索数据通常比从内存中提取数据花费更长。

在不同的缓存类型之间取得正确的平衡，对于实现速度与效率的最优结合至关重要。Zend Framework 的 `Zend_Cache_Manager` 组件和插件使得这项任务变得稍微简单，它允许你在应用程序配置文件中配置多种缓存类型。这减少了应用程序引导程序中需要的配置工作量，并允许为不同的动作（甚至在同一个动作内部）使用不同的缓存样式。

这里有一个缓存配置示例：

```ini
resources.cachemanager.mycache.frontend.name = Core
resources.cachemanager.mycache.frontend.options.lifetime = 600
resources.cachemanager.mycache.frontend.options.automatic_serialization = true
resources.cachemanager.mycache.backend.name = Apc
```

现在可以在动作中直接利用此缓存实例，如下：

```php
<?php

class SandboxExampleController extends Zend_ControllerAction
{
    public function cacheAction()
    {
        // 获取缓存
        $cache = $this->getInvokeArg('bootstrap')
            ->getResource('cachemanager')
            ->getCache('mycache');

        // 如果缓存可用则使用缓存
        if (!($this->view->records = $cache->load('cities'))) {
            // 执行查询
            $sql = "SELECT * FROM city AS ci,
                        country AS co,
                        countrylanguage AS cl
                    WHERE
                        ci.CountryCode = co.Code AND
                        cl.CountryCode = co.Code AND
```



```sql
cl.Language = 'English' AND

cl.IsOfficial = 'T'";
```

```php
// 获取并使用数据库适配器

$db = $this->getInvokeArg('bootstrap')->getResource('database');

$result = $db->fetchAll($sql);

$cache->save($result, 'cities');

$this->view->records = $result;
```

## 注意

需要注意的是，在应用程序配置文件中配置缓存不会自动初始化它。出于性能考虑，`Zend_Cache_Manager` 只会在通过 `getCache()` 方法按名称调用时才会初始化 `Zend_Cache` 实例，而不是提前。

### 缓存 Doctrine 查询

虽然 `Zend_Cache` 可以通用用于缓存数据库查询结果（如本节第一个示例所示），但也可以使用 Doctrine 自身的缓存机制来实现此目的。Doctrine 带有两种不同的缓存系统，一个用于查询，一个用于结果，两者都易于激活和使用，且代码重构工作极少。

Doctrine 查询缓存持有 `Doctrine_Query` 对象的解析后表示，允许重复的查询直接发送到服务器，而无需先进行解析。Doctrine 结果缓存执行了 Doctrine 查询缓存的所有工作，但还存储了查询结果的序列化表示，并在尽可能的情况下返回它们，从而将数据库服务器排除在之外并显著提高性能。缓存数据可以存储在 `memcached` 服务器、APC 共享内存缓存或任何其他 Doctrine 支持的数据库中。

激活查询缓存非常简单：为相应缓存后端的 Doctrine 驱动初始化，并使用 `Doctrine::ATTR_QUERY_CACHE` 属性将其传递给 `Doctrine_Manager` 实例。这里有一个示例：

```php
<?php

// 设置缓存驱动

$servers = array(
    'host' => 'localhost',
    'port' => 11211,
    'persistent' => false
);

$cache = new Doctrine_Cache_Memcache(array(
    'servers' => $servers,
    'compression' => false
));
```

```php
// 将缓存附加到 Doctrine 管理器

$manager = Doctrine_Manager::getInstance();

$manager->setAttribute(Doctrine::ATTR_QUERY_CACHE, $cache);
?>
```

一旦以这种方式初始化，Doctrine 查询缓存对所有通过 Doctrine 执行的查询将自动激活。

Doctrine 结果缓存也遵循类似的方法，如下：

```php
<?php

// 设置缓存驱动

$servers = array(
    'host' => 'localhost',
    'port' => 11211,
    'persistent' => false
);

$cache = new Doctrine_Cache_Memcache(array(
    'servers' => $servers,
    'compression' => false
));
```

```php
// 将缓存附加到 Doctrine 管理器

$manager = Doctrine_Manager::getInstance();

$manager->setAttribute(Doctrine::ATTR_RESULT_CACHE, $cache);
?>
```

但重要的是，Doctrine 结果缓存不会对所有通过 Doctrine 执行的查询自动激活；必须在每次查询的基础上显式地告诉 Doctrine 使用此功能，即在相应的 `Query` 对象上添加 `useResultCache()` 方法。这里是这样做的示例：

```php
<?php

class SandboxExampleController extends Zend_Controller_Action
{
    public function cacheAction()
    {
        $id = $this->getParam('id');

        $q = Doctrine_Query::create()
            ->from('Square_Model_Item', 'i')
            ->leftJoin('Square_Country', 'c')
            ->leftJoin('Square_Grade', 'g')
            ->leftJoin('Square_Type', 't')
            ->where('i.DisplayStatus = ?', $id)
            ->useResultCache(true);

        $this->view->result = $q->fetchArray();
    }
}
```

## 注意

如果你使用 MySQL 作为数据库，应该知道 MySQL 自带查询缓存，且它是默认开启的。该查询缓存存储 `SELECT` 查询的结果集，对于相同的查询，将从缓存中检索，而不是再次运行查询。请注意，只有文本匹配的查询才会生效；例如，`SELECT * FROM airport` 不会返回 `select * FROM airport` 的结果。

### 专家

**问：**内存缓存总是优于磁盘缓存吗？

**答：**磁盘缓存通常被认为比内存缓存“慢”，因为从磁盘检索数据通常比从 `memcached` 或 APC 等内存缓存中提取花费更长。在这种情况下，将频繁访问的数据缓存在内存缓存而非磁盘缓存中通常是合理的。

然而，认为通过将所有数据存储在内存缓存中可以最大化此应用程序性能是错误的，因为必须考虑被缓存数据的大小。在大多数情况下，内存是比磁盘空间稀缺得多的资源，因此当要缓存的数据很大时，使用磁盘缓存通常更合理。

# 第 12 章：优化性能

## 优化应用程序代码

虽然缓存确实可以为 Web 应用程序提供显著的性能提升，但它并不是开发者拥有的唯一工具。以下章节探讨了一些其他优化策略。

### 查询调优

有许多技术可以用来优化数据库查询的性能，并确保它们尽可能高效运行。以下章节讨论了其中一些技术，特别提到了现代 Web 应用程序开发中最常用的数据库 MySQL。

### 使用 Join 代替子查询

MySQL 对连接（join）的优化优于子查询，因此如果你发现 MySQL 服务器的负载达到不可接受的水平，请检查你的应用程序代码并尝试改进。

将你的子查询重写为连接（joins）或一系列连接。例如，以下子查询是合法的：

```sql
SELECT id, name FROM movie
WHERE directorid IN
(
    SELECT id FROM director
    WHERE name = 'Alfred Hitchcock'
);
```

但由于 MySQL 的优化算法，以下等效的连接运行速度更快：

```sql
SELECT m.id, m.name
FROM movie m, director AS d
WHERE d.id = m.director
  AND d.name = 'Alfred Hitchcock';
```

你还可以通过巧妙地使用 MySQL 的 `ORDER BY` 和 `LIMIT` 子句插入查询。考虑以下子查询：

```sql
SELECT id, duration FROM movie
WHERE duration =
(
    SELECT MAX(duration) FROM movie
);
```

这种方法比下面的查询更好，因为它更易读且运行速度快得多：

```sql
SELECT id, duration FROM movie
ORDER BY duration DESC
LIMIT 0, 1;
```

## 使用临时表处理瞬态数据或计算

MySQL 还允许你通过 `CREATE TEMPORARY TABLE` 命令创建临时表。这些表之所以被称为临时表，是因为它们仅在单个 MySQL 会话期间存在，并在客户端与 MySQL 服务器断开连接时自动删除。这些表对于瞬态的、基于会话的数据计算或数据的临时存储非常有用。而且它们是依赖会话的，两个会话可以使用相同的表名而不会发生冲突。

由于临时表存储在内存中，它们的速度明显快于基于磁盘表。它们可以有效地作为中间存储区域，通过帮助将复杂查询分解为简单的组件来加速查询执行，或者作为查询和连接支持的替代方案。

MySQL 的 `INSERT...SELECT` 语法结合 `IGNORE` 关键字，为临时表提供了许多巧妙重写 `SELECT` 查询以进行执行的机会。例如，如果你有一个涉及从特定字段选择一组唯一值的复杂查询，而 MySQL 引擎由于其复杂性无法优化你的查询，SQL 程序员可以通过将单个复杂查询拆分为许多简单查询（这些查询更利于优化），然后使用 `INSERT IGNORE...SELECT` 命令将生成的结果保存到临时表中（前提是先在相应字段上通过 `UNIQUE` 键创建临时表）。结果是得到该字段的一组唯一值，并可能获得更好的查询执行性能。

### 显式指定字段

我们经常看到如下查询：

```sql
SELECT (*) FROM airport;

SELECT COUNT(*) FROM airport;
```

这些查询为了方便使用了通配符星号（`*`）。然而，这种便利是有代价的：`*` 会强制 MySQL 读取表中的每个字段或记录，从而增加了整个查询的处理时间。为了避免这种情况，请显式命名你希望在结果集中看到的输出字段，如示例所示：

```sql
SELECT id, name FROM airport;

SELECT COUNT(id) FROM airport;
```

## 为连接字段建立索引

频繁访问的字段应该建立索引。根据一般原则，如果你有一个字段参与搜索、分组或排序，对其建立索引可能会带来性能提升。索引应该包含作为连接操作部分的字段，或者出现在 `WHERE`、`GROUP BY` 或 `ORDER BY` 子句中的字段。此外，连接字段而非字符字段会产生更好的性能。

### 使用小型事务

尽管这听起来可能很陈旧，但 KISS（保持简单，别太傻了！）原则在复杂的事务世界中尤为适用。这是因为 MySQL 使用行级锁机制来防止并发事务编辑同一条记录并导致损坏。行级锁机制防止多个事务同时访问某一行——这保护了数据，但缺点是会导致其他事务等待，直到发起锁的事务完成工作。只要事务是足够小的，这种等待就是不可察觉的。然而，当你处理大型数据库和许多复杂事务时，各种事务等待彼此锁的长时间等待会显著影响性能。

因此，通常情况下保持事务较小并让它们快速变化并退出是一个好主意，这样排在它们后面的其他事务就不会受到不当延迟。在应用层面，有两种实现此点的常用策略：

- 确保在发布 `START TRANSACTION` 命令之前，事务所需的所有用户输入已就绪。通常，初级应用程序设计人员在所需的完整值集尚未可用之前就启动了事务。同时启动的其他事务现在必须等待，直到用户输入所需数据、应用程序对其进行处理，然后请求更多数据，以此类推。在单用户环境中，这些延迟不会产生太大影响，因为没有其他事务会尝试访问数据库。在多用户场景下，单个事务引起的延迟可能会对系统中排队的所有其他事务产生连锁反应，导致严重的性能下降。
- 尝试将大事务拆分为较小的子事务并独立地执行它们。这将确保每个子事务都能快速执行，释放出原本会被维护系统状态的宝贵资源。

### 优化表设计和服务器配置

本节讨论的技术都是应用层优化的建议。然而，为了进一步提高性能，你还应该考虑在数据库层优化性能的各种技术，例如：

- 使用索引加速搜索、分组、排序
- 选择合适的表引擎
- 指定表连接字段具有相同的数据类型和长度
- 增加各种服务器端缓冲器的可用内存，例如读取缓冲区、排序缓冲区和线程缓存

### 懒加载

Zend 和 Doctrine 的自动加载器（autoloers）都可以根据需要自动查找并加载文件。这种技术通常被称为懒加载（lazy loading），通过减少文件读取次数显著提高性能。要激活 Zend Framework 自动加载器，手册建议在应用程序的 `index.php` 中添加以下代码行：

```php
<?php

require_once 'Zend/Loader/Autoloader.php';

Zend_Loader_Autoloader::getInstance();
?>
```

# 406 Zend Framework：初学者指南

```ini
resources.cachemanager.memory.backend.options.automatic_serialization = true
resources.cachemanager.memory.backend = Memcached
resources.cachemanager.memory.backend.options.servers.host = localhost
resources.cachemanager.memory.backend.options.servers.port = 11211
resources.cachemanager.memory.backend.options.servers.timeout = 5
resources.cachemanager.memory.backend.options.servers.retry_interval = 10
```

完成所有配置后，让我们开始缓存吧！

### 缓存翻译字符串

`ZendTranslate` 和 `Zend Locale` 都可以使用预先配置的 `ZendCache` 实例来存储区域数据和翻译字符串，以便快速查找。为这些组件设置缓存非常简单：只需将它们的 `setCache($)` 方法传递给配置恰当的 `Zend_Cache` 实例，它们就会处理剩下的工作。

若要启用这两个组件的缓存，请如下所示通过 `_initCache()` 方法更新应用启动引导器：

```php
<?php

class Bootstrap extends Zend_Application_Bootstrap
{
    protected function _initCache()
    {
        $this->bootstrap('cachemanager');

        $manager = $this->getResource('cachemanager');
        $memoryCache = $manager->getCache('memory');

        Zend_Locale::setCache($memoryCache);
        Zend_Translate::setCache($memoryCache);
    }
}
```

### 缓存查询结果

如果你查看 `Catalog_ItemController::displayAction` 和 `Catalog_AdminItemController::displayAction`，你会发现这两个操作都使用了 Doctrine 查询，但有一处微小的差别：第一个包含一个额外的检查，以确保目录项目已批准向公众显示。由于这本质上是重复了两次的代码，因此它是重构为模型方法（model method）的理想人选。

要实现这一点，请向 `$APP_DIR/library/Model/Item.php` 中的 `Square_Model_Item` 模型类添加以下方法：

```php
<?php

class Square_Model_Item extends Square_Model_BaseItem
{
    public function getItem($id, $active = true)
    {
        $q = Doctrine_Query::create()
            ->from('Square_Model_Item i')
            ->leftJoin('i.Square_Model_Country c')
            ->leftJoin('i.Square_Model_Grade g')
            ->leftJoin('i.Square_Model_Type t')
            ->where('i.RecordID = ?', $sid);

        if ($active) {
            $q->addWhere('i.DisplayStatus = 1')
                ->addWhere('i.DisplayUntil >= CURDATE()');
        }

        return $q->fetchArray();
    }
}
```

然后，更新 `Catalog_ItemController` 以引用模型中的 `getItem()` 方法，而不是直接构建 Doctrine 查询。顺便，直接使用前面提到的内存缓存对方法的结果进行缓存。以下是修改后的 `Catalog_ItemController::displayAction` 方法的写法：

```php
<?php

class Catalog_ItemController extends Zend_Controller
{
    // 显示目录项目的操作

    public function displayAction()
    {
        // 为 GET 输入设置过滤器和验证器

        $filters = array(
```



```php
'id' => array(HtmlEntities, 'StripsTags', 'StringTrim')

);

$validators = array(

    'id' => array('NotEmpty', 'Int')

);

$input = new Zend_Filter_Input($filters, $validators);

$this->setData($this->getRequest()->getParameters());

// 测试输入是否有效

// 从缓存或数据库检索请求记录

// 挂载到视图

if ($input->isValid()) {

    $memoryCache = $this->getResource('bootstrap')
        ->getCache('memory');

    if (!($memoryCache->load('public_item_'.$input->id()))) {

        $result = $this->getItem($input->get('id'), true);

        $memoryCache->save($result, 'public_item_'.$input->id());

    }

    if (count($result) == 1) {

        $this->view->item = $result[0];

    }

}

}

}
```

# 第 12 章：优化性能

（续）

## Zend Framework：初学者指南

## 缓存 Twitter 和 Feeds

在当前版本中，`NewsController::indexAction` 每次请求都会获取一组新的搜索结果以及最新的新闻和博客源。这些数据通过 HTTP 访问，获取成本高昂；同时，它们也是非关键的、低影响的信息。这使其成为缓存的理想目标。

考虑以下 `NewsController::indexAction` 的修订版本，它使用前端来缓存搜索结果和博客/新闻源，以提高响应速度：

```php
<?php

class NewsController extends Zend_Controller_Action

{

    public function indexAction()

    {

        // 获取 Twitter 搜索源

        $q = 'latest';

        $this->view->q = $q;

        // 获取缓存

        $fileCache = $this->getInvoke('bootstrap')
            ->getResource('cachemanager')
            ->getCache('news');

        $id = 'twitter';

        if (!$this->view->tweets = $fileCache->load($id)) {

            $tweets = new Zend_Service_Search();

            $this->view->tweets = $tweets->search($q,
                array('lang' => 'en', 'r' => 8, 'show_user' => true));

            $fileCache->save($this->tweets, $id);

        }

    }

}

Zend_Feed_Reader::setCache($fileCache);

$this->view->feeds = array();

// 获取 Google 新 Atom 源

$gNewsFeed = "http://news.google.com/news?hl=en&q=$q&output=atom";

$this->view->feeds[0] = Zend_Feed_Reader::import($gNewsFeed);

// 获取 BPMA RSS 源

$bpmaFeed = "http://www.postalheritage.org.uk/rss";

$this->view->feeds[1] = Zend_Feed_Reader::import($bpmaFeed);
```

注意通过简单调用 `Zend_Feed_Reader::setCache()` 并传递配置好的 Zend_Cache 实例即可启用缓存。

如果在进行上述更改后测量应用性能，你会发现明显的提升。为了说明，请看表 12-3，它显示了在测试部署上使用 ApacheBench 的统计数据。

### 问专家

Q：重构方法对性能有帮助吗？

A：第 12 章讨论了“胖模型、瘦控制器”方法，该方法建议将业务逻辑位于方法中，而不是控制器中。除了其他益处外，这种方法与缓存结合使用时可以提高性能。正如之前的“查询结果”部分所示，如果结果已存在，你可以使用缓存完全阻止方法的调用，从而减少需要执行的代码行。更少的代码意味着更快的脚本解析和执行。

Q：为什么没有使用 Doctrine 结果缓存来缓存查询结果？

A：虽然可以使用 Doctrine 结果缓存来缓存查询结果，但这样做不可避免地需要加载 Doctrine 模型。本示例中使用的方法跳过了这一步，使得 Doctrine 模型完全没有被调用。这进一步减少了执行的代码量。

| URL | 未开启缓存：每秒请求数 | 未开启缓存：平均请求时间 (ms) | 已开启缓存：每秒请求数 | 已开启缓存：平均请求时间 (ms) | 缓存提升（百分比） |
| --- | ---: | ---: | ---: | ---: | ---: |
| http://square.localhost/ | 0.45 | 2242.00 | 2.07 | 483.91 | 约 360% |
| http://square.localhost/catalog/item/1 | 3.32 | 301.563 | 9.52 | 105.00 | 约 187% |

**表 12-3** 示例应用在 ApacheBench 下的缓存实施前后对比数据。该报告针对 100 次总请求生成，并发级别为 10。

# 第 12 章：优化性能

为了了解更多关于性能优化的知识，并下载本章提到的某些工具，请参考以下链接：

- `Zend_Cache` 组件，位于 http://framework.zend.com/manual/en/zend.cache
- `Zend_Db_Profiler` 组件，位于 http://framework.zend.com/manual/en/zend.db.profiler
- 关于 Doctrine 缓存的信息，位于 http://www.doctrine-project.org/documentation/manual/1_1/en/caching
- 关于 MySQL 性能优化的信息，位于 http://dev.mysql.com/doc/refman/5/1/en/optimization
- Zend Framework 性能优化的策略，位于 http://framework.zend.com/manual/en/performance.html
- ApacheBench 文档，位于 http://httpd.apache.org/docs/2.0/programs/ab.html
- WCAT，位于 http://www.iis.net/downloads/default.aspx?tabid=34&i=1466&g=6
- Xdebug，位于 http://xdebug.org/
- Webgrid，位于 http://code.google.com/p/webgrid/
- Wincachegrid，位于 http://sourceforge.org/projects/wincachegrid/
- Kcachegrid，位于 http://kcachegrid.sourceforge/
- PEAR Benchmark 程序包，位于 http://pear.php.net/package/Benchmark
- Memcached，位于 http://memcached.org/
- PHP memcached 扩展，位于 http://pecl.php.net/package/memcache
- Imind Doctrine 分析分析器，位于 http://code.google.com/imind-php/wiki/Imind_Profiler_Doctrine_Firefox
- 使用 Xdebug 和 Webgrid 进行 PHP 脚本分析的讨论（Anant Garg），位于 http://anantarg.com/2009/03/10/php-xdebug-webgrid-installation/

尽管你已经读到了这本书的最后，但显而易见，你的 Zend Framework 之旅远未结束……如果可以的话，它才刚刚开始！前面的章节已经为你提供了创建高质量 Zend Framework 应用所需的准备。剩下的部分取决于你和你的想象力。祝你好运，编码愉快！

# 附录：安装与配置软件

## Zend Framework：初学者指南

### 核心技能与概念

- 学习从互联网获取并安装 MySQL、PHP 和 Apache 软件
- 执行基础测试以确保应用程序正常运行
- 了解如何在系统启动时自动激活所有必需组件
- 采取基本步骤保护你的 MySQL 安装安全

在本书中，你学习了 Zend Framework 以及如何使用它来构建 Web 应用。书中的示例假设你已经配置了正确的 Apache/MySQL/PHP 开发环境。如果你还没有，本节将向你展示如何安装和配置这些组件，并创建一个可以运行书中代码示例的开发环境。

### 注意事项

本附录旨在提供在 UNIX 和 Windows 上安装和配置 MySQL、PHP 和 Apache 的概述和指南。它并不打算替代每个软件包随附的安装文档。如果你在安装此处描述的各种程序时遇到困难，请访问相应程序的官方网站，或在网络上搜索详细的故障排除信息和建议（附录末尾提供了一些链接）。

### 获取软件

你有几种方法可以在你的 Windows 或 UNIX 系统上运行 Apache/MySQL/PHP 开发环境：

1. 你可以下载一个全面的集成堆栈，它包含了所有必要的部分和依赖项，并且经过预配置直接可以使用。
2. 你可以单独下载不同的部分并自己进行配置。

如果你是 PHP 或通用开源开发的新手，建议采用第一种方法，因为这将让你以最少的心力开始工作。以下是你应该考虑的两个流行堆栈：

- Server Community Edition 是由 Zend Technologies 提供的一个集成、健壮的堆栈。除了标准的 Apache/MySQL/PHP 组件外，它还包含了许多调试和优化工具，以及（作为奖励）最新版本的 Zend Framework。它适用于 Microsoft Windows、Mac OS 和 Linux 操作系统，可以从 http://www.zend.com/ 免费下载。
- XAMPP 是一个由社区支持的发行版，包含了最新版本的 Apache、PHP、MySQL 和 Perl。它经过完全配置，可开箱即用，对于快速搭建基于 PHP 的开发环境非常流行。它还包含了额外的工具，如 FTP 服务器和基于 Web 的 MySQL 管理工具。它适用于 Microsoft Windows、Mac OS X、Linux 和 Solaris，可以从 http://www.apachefriends.org/en/index.html 免费下载。

集成堆栈的缺点是，如果你使用第二种“自己来”的方法，你学到的东西会少得多，因为所有组件都已为你预配置好了。如果你有倾向和兴趣，单独配置各个部分将是一个极佳的学习体验；附录的其余部分将对此深入讨论。

第一步是确保你已拥有所需的所有软件。以下是列表：

- PHP 为 Web 和控制台应用程序提供应用框架。你可以从 http://www.php.net/ 下载。这里提供了适用于 WINDOW、UNIX 和 Mac OS 平台的源码和二进制版本。UNIX 用户应该下载最新的源码包，而 Windows 用户应该下载最新的二进制版本。在本书出版时，PHP 的最新版本是 v5.3.1。
- Apache 是一个与 PHP 集成的功能丰富的 Web 服务器。你可以从 http://httpd.apache.org/ 免费下载源码和二进制版本，适用于多种平台。UNIX 用户应该下载最新的源码包，而 Windows 用户应该下载适用于其版本的二进制安装程序。在本书出版时，Apache 服务器的最新版本是 v2.2.1。
- MySQL 数据库服务器提供了健壮且扩展的数据存储/检索。你可以从 http://www.mysql.com/ 获取源码和二进制版本。二进制发行版适用于 Linux、Solaris、FreeBSD、Mac OS X、HP-UX、IBM AIX、SCO OpenUNIX 和 SGI Iris；适用于 Windows 和 Unix 平台。推荐使用二进制版本，原因有两个：它更容易安装，并且开发团队针对不同平台进行了优化。在本书出版时，MySQL 服务器的最新版本是 v5.1.43。

除了这四个组件外，UNIX 用户可能还需要一些库。列表如下：

- `libxml2` 库，位于 http://www.xmlsoft.org/
- `zlib` 库，位于 http://www.gzip.org/
- `gd` 库，位于 http://www.gdell.com/

最后，两个平台的用户都需要一个能够处理 TAR（带归档）和 GZ（GNU 压缩）文件的解压工具。在 UNIX 上，`tar` 和 `gzip` 工具通常包含在操作系统中。在 Windows 中，一个很好的解压工具是 WinZip，位于 http://www.winzip.com/。

# 附：安装和配置所需软件

使用 `groupadd` 和 `useradd` 命令执行操作，然后将 MySQL 安装目录的所有权更改为此用户和组：

```bash
[root@#] groupadd mysql
[root@#] useradd -g mysql
[root@#] chown -R mysql /usr/local/mysql
[root@#] chgrp -R mysql /usr/local/mysql
```

5. 使用发行版包含的 `mysql_install_db` 初始化脚本初始化 MySQL 表。

```bash
[root@#] /usr/local/mysql/scripts/mysql_install_db --user=mysql
```

图 A-1 展示了执行此操作时你应该看到的内容。

如图 A-1 输出所示，该初始化脚本准备并安装了各种 MySQL 基础表，还为 MySQL 设置了默认的访问权限。

6. 修改 MySQL 二进制文件的所有权，使其归 root 所有。

```bash
[root@#] chown -R root /usr/local/mysql
```

确保第 4 步中创建的 MySQL 用户对 MySQL 目录具有读/写权限。

```bash
[root@#] chown -R mysql /usr/local/mysql/data
```

7. 通过运行 `mysql_safe` 脚本启动 MySQL 服务。

```bash
[root@#] /usr/local/mysql/bin/mysql_safe --user=mysql &
```

MySQL 现在应该正常启动。

![图 A-1 mysql_install_db 脚本的输出](img/222e7e58871b088cc6397852e1452b57_435_0.png)

## Zend Framework：初学者指南

一旦完成安装并启动服务器后，请跳转到“测试 MySQL”部分以验证其是否运行正常。

# 安装 Apache 和 PHP

PHP 可以通过两种方式集成到 Apache Web 服务器中：作为在运行时加载到 Apache Web 服务器的动态模块，或者作为在构建时集成到 Apache 源码树的静态模块。每种方案都有其优缺点：

- 将 PHP 安装为动态模块可以让你在日后更容易升级 PHP 版本，因为你只需要重新编译 PHP 模块，而不需要重新编译 Apache Web 服务器的其他部分。但另一方面，使用动态加载模块的性能通常低于与服务器集成更紧密的静态模块。
- 将 PHP 安装为静态模块可以提高性能，因为该模块被直接编译到 Apache 源码树中。这种选择有一个重要的缺点：如果你决定升级 PHP 版本，将需要将新的 PHP 模块重新整合到 Apache 源码树中并重新编译 Apache Web 服务器。

本节将展示如何将 PHP 编译为运行时加载到 Apache 服务器的动态模块。

1. 确保你已以系统 root 用户的身份登录。

```bash
[user@host] # su - root
```

2. 将 Apache 源码包的内容提取到系统的临时目录中。

```bash
[root@host] # cd /tmp
[root@host] # tar -xzvf /tmp/httpd-2.2.14.tar.gz
```

3. 为了动态启用 PHP，编译 Apache 服务器时必须开启动态共享对象（ISO）支持。这种支持通过在向 Apache 配置脚本传递 `--enable-module=so` 选项来实现，如下所示：

```bash
[root@host] # cd /tmp/httpd-2.2.14
```



```bash
[root@host]# ./configure --prefix=/usr/local/apache \
  --enable-module=so \
  --enable-rewrite
```

### 4. 编译并安装 Apache

现在，使用 `make` 命令编译服务器，并使用 `make install` 安装到系统。

```bash
[root@host]# make
[root@host]# make install
```

图 A-2 展示了你在编译过程中可能会看到的内容。

Apache 现在应该已经安装到`/usr/local/apache/`。

### 5. 编译并安装 PHP

接下来，继续编译并安装 PHP。将 PHP 源码包的内容提取到系统的临时目录中。

```bash
[root@host]# cd /tmp
[root@host]# tar -xzvf /tmp/php-5.3.1.tar.gz
```

## 附：安装和配置所需软件

### 6. 配置 PHP

这一步是 PHP 安装过程中最重要的一步。向 PHP 配置脚本发送参数以配置 PHP 模块。命令行参数指定了应该启用哪些扩展，它们还会告诉 PHP 寻找这些扩展所需的支持库。

```bash
[root@host]# cd /tmp/php-5.3.1
[root@host]# ./configure --prefix=/usr/local/php \
  --with-apache2=/usr/local/apache/bin/apxs \
  --with-zlib \
  --with-gd \
  --with-mysqli=mysql \
  --with-pdo-mysql=mysql
```

以下是每个参数作用的简单说明：

- `--with-apache2` 告诉 PHP 寻找 Apache APXS（Apache Extension）。该脚本简化了构建和安装 Apache 可加载模块的任务。
- `--with-zlib` 告诉 PHP 激活压缩（zip）功能，该功能会被其他 PHP 服务使用。
- `--with-gd` 告诉 PHP 激活图像处理功能。
- `--with-mysqli` 激活 PHP 的 MySQL 扩展并告诉 PHP 使用新的 MySQL 驱动（mysqlnd）作为 MySQL 客户端库。
- `--with-pdo-mysql` 激活 PHP 的 PDO 驱动并告诉 PHP 使用 MySQL 原生驱动作为 MySQL 客户端库。

### 7. 编译并安装 PHP

接下来，使用 `make` 和 `make install` 编译并安装 PHP。

```bash
[root@host]# make
[root@host]# make install
```

此时你也可以运行测试来执行 PHP 的单元测试并检查任何失败。如果一切顺利，PHP 现在应该已经安装到`/usr/local/php/`。

### 8. 配置 Apache 识别 PHP 页面

安装的最后步骤是配置 Apache 正确识别 PHP 页面。这通过文本编辑器打开 Apache 文件 `httpd.conf`（位于 Apache 安装目录的 `conf/` 子目录下），并添加以下行来实现：

```apache
AddType application/x-httpd-php .php
```

保存更改。同时，检查文件中是否存在以下行：

```apache
LoadModule php5_module modules/libphp5.so
```

### 9. 启动 Apache

通过手动运行 `apachectl` 脚本启动 Apache。

```bash
[root@host]# /usr/local/apache/bin/apachectl
```

Apache 应该正常启动。

一旦完成安装并成功启动服务器，请跳转到“测试 PHP”部分以验证一切。

## 在 Windows 上安装

在 Windows 上编译应用程序是一项挑战性任务，特别是对于初学者而言。基于此，建议用户专注于安装和配置预构建的二进制版本 MySQL、SQLite、PHP 和 Apache，而不是尝试从源码完成编译。这些版本可以从之前在“获取软件”部分列出的网站下载，并按照下述子节的概述逐一安装。

## 安装 MySQL

MySQL 适用于所有 32 位和 64 位的 Microsoft Windows，提供源码和二进制两种形式。通常，你会希望使用“Essentials”或“Complete”二进制发行版，它们包含一个自动化安装程序，可以在几分钟内让 MySQL 运行起来。

从二进制发行版安装 MySQL，请执行以下步骤：

1. 以管理员身份登录（如果你使用的是 Windows XP/Vista/7）。

2. 双击`mysql-*.msi`文件开始安装过程。你应该看到一个欢迎界面（见图 A-3）。

![图 A-3 在 Windows 上开始 MySQL 安装](img/222e7e58871b088cc6397852e1452b57_439_0.png)

3. 选择所需的安装类型。

   通常情况下，选择“典型（Typical）”安装即可；但如果你是那种喜欢调整默认设置的人，或者如果你的磁盘空间不足，请选择“自定义（Custom）”安装选项，并决定应该安装包中的哪些组件。

4. MySQL 现在应该开始安装到您的系统中。

5. 一旦安装完成，您将看到成功通知。此时，您可以选择启动“MySQL 服务器实例配置向导”来完成软件的配置，并将看到相应的欢迎界面。

6. 选择配置类型。在大多数情况下，使用“标准配置（Standard）”即可。

7. 将 MySQL 安装为 Windows 服务，这样它就会随 Windows 自动启动和停止（见图 A-4）。

8. 为 MySQL 管理员（root）账户输入密码（见图 A-5）。

服务器现在将根据您指定的设置进行配置并自动启动。所有所需任务完成后，您将看到成功通知。现在您可以按照“测试 MySQL”章节中的描述对服务器进行测试，以确保一切均按预期工作。

![图 A-4 设置 MySQL 服务器服务](img/222e7e58871b088cc6397852e1452b57_440_0.png)

![图 A-5 设置管理员密码](img/222e7e58871b088cc6397852e1452b57_440_1.png)

## 安装 Apache

安装 MySQL 后，下一步是安装 Apache Web 服务器。在 Windows 上，这是一个点击即可完成的过程，与安装 MySQL 类似。

1. 首先双击 Apache 安装程序以开始安装过程。您应该看到一个欢迎界面（见图 A-6）。

2. 读取许可协议并接受条款以继续。

![图 A-6 在 Windows 上开始 Apache 安装](img/222e7e58871b088cc6397852e1452b57_441_0.png)

3. 读取描述性信息，然后继续输入基本服务器信息以及显示在错误页面上的电子邮件地址。

4. 选择所需的安装类型。如果您想决定应该安装包中的哪些组件，可以选择“自定义（Custom）”安装选项。

5. 选择 Apache 安装的位置——例如`C:\Program Files\Apache\`。

6. Apache 现在应该开始安装到指定位置。安装过程需要几分钟完成，所以这段时间可以自己去喝杯咖啡。

7. 一旦安装完成，Apache 安装程序将显示成功通知并启动 Apache Web 服务器。

## 安装 PHP

Windows 有两个版本的 PHP 二进制发布版：一个 ZIP 压缩包（包含所有绑定的 PHP 扩展并需要手动安装），以及一个自动 Windows 安装版本（仅包含基础 PHP 二进制文件，不含额外扩展）。本节概述了 PHP ZIP 压缩包的安装过程。

1. 以管理员身份登录（如果您使用的是 Windows XP/Vista/7），并将分发包解压到系统中的某个目录——例如`C:\php\`。解压后，该目录看起来应该类似于图 A-7。

![图 A-7 解压 php 二进制分发包后创建的目录结构](img/222e7e58871b088cc6397852e1452b57_442_0.png)

2. 将您的 PHP 安装目录下的文件`php.ini-recommended`重命名为`php.ini`。该文件包含了 PHP 的配置设置，用于更改其工作方式。读取文件中的注释以了解更多可用设置。

3. 在`php.ini`文件中，找到以下行：

```ini
extension_dir = "../"
```

修改为：

```ini
extension_dir = "c:\php\ext\"
```

这告诉 PHP 在**何处**查找随包安装的扩展。请记住将路径`"c:\php"`替换为 PHP 安装的实际位置。

4. 接下来，查找以下行并删除开头的分号（如果存在），使其内容如下：

```ini
extension=php_mysql.dll
extension=php_pdo_sqlite.dll
extension=php_pdo_mysql.dll
extension=php_zip.dll
extension=php_gd2.dll
```

这处理了激活 PHP 的 MySQL、GD、Zip 和 PDO 扩展。

5. 用文本编辑器打开 Apache 配置`httpd.conf`（可以在 Apache 安装目录的`conf/`子目录下找到），并添加以下行：

```apache
Type application/x-httpd .php
LoadModule php_module
```

这些行告诉 Apache 如何处理`.php`脚本。

6. 配置完成后，通过`php.ini`配置文件重启 Apache。切换到命令行界面，启动 Apache 如下所示（见图 A-8）。

## 测试 PHP

一旦作为 Apache 模块安装成功，您应该测试它以确保 Web 服务器能够识别并处理脚本。要进行此测试，在任何文本编辑器中创建一个包含以下内容的 PHP 脚本：

```php
<?php
phpinfo();
?>
```

将文件保存为`test.php`并放在 Apache 安装目录的根目录（`docs/`子目录），并将浏览器指向`http://localhost/test.php`。您应该看到一个包含 PHP 构建信息的页面，如图 9 所示。

检查扩展列表，确保 MySQL、GD、SimpleXML 和 Zip 扩展已激活。如果没有激活，请检查安装步骤以及随软件附带的文档查看出了什么问题。

![PHP 信息页面](img/222e7e58871b088cc6397852e1452b57_445_0.png)

| 项目 | 值 | |
|---|---|---|
| 系统 | Windows NT 5.1 build 2600 (Windows XP Service Pack 3) | x86 |
| 构建日期 | 2009年11月19日 10:16:45 | |
| 编译器 | MSVC6 (Visual C++ 6.0) | |
| 架构 | x86 | |
| 命令 | `cscript php.php configure="--enable-snapshot-build" "--enable-disable-debug-pack" "--disable-isap" "--with-pdo-oracle=D:\php-dk-oracle\instantclient10id\sdk,shared" "--with-oci8=D:\php-dk-oracle\instantclient10id\sdk,shared" "--with-oci8-11g=D:\php-dk-oracle\instantclient11id\sdk,shared" "--enable-oracle-instance11id--enable-out-dir=./obj/"` | |
| 服务器 API | Apache 2.0 Handler | |
| 虚拟目录支持 | 已启用 | |
| `(php.ini)` 路径 | `C:\WINDOWS` | |
| 加载的配置文件 | `C:\Program Files\PHP\php.ini` | |
| 扫描此目录的额外 `.ini` 文件 | （无） | |

查看`phpinfo()`函数的输出。

## 设置 MySQL 超级密码

在首次安装 MySQL 时，数据库服务器的访问仅限于 MySQL 管理员，即`'root'`。默认情况下，该用户初始化时密码为空，这通常被认为是一个坏习惯（Bad Thing）。因此，您应该尽快通过`mysqldadmin`工具为该用户设置密码，在 UNIX 中请使用以下语法：

```bash
[root@host]# /usr/local/mysql/bin/mysqldadmin -u root password 'new-password'
```



在 Windows 中，您可以使用 MySQL Server 配置向导，它允许您设置或重置 MySQL 管理员密码（更多信息请参阅“在 Windows 上安装”章节）。

此密码更改将立即生效，无需重启服务器。

## 总结

作为开源应用程序，MySQL、Apache 和 PHP 适用于多种平台和架构，提供二进制和源码两种形式。本附录演示了安装和配置这些软件组件的过程，以便在两个常用的平台（UNIX 和 Windows）上创建 PHP 开发环境。它还展示了如何配置系统以便每次系统启动时自动启动这些组件，并根据 MySQL 安全性提供了一些建议。

要了解更多关于本附录概述的安装过程，或获取详细的故障排除建议和帮助，请访问以下页面：

- MySQL 安装说明，位于：`http://mysql.com/doc/refman/5.1/en/installing-binary.html`
- UNIX 上编译 Apache 的通用指南，位于：`http://httpd.apache.com/docs/2.2/install.html`
- Apache 安装的 Windows 特定说明，位于：`http://httpd.apache.com/docs/2.2/platform/windows.html`
- Windows 上安装 PHP 的说明，位于：`http://www.php.net/manual/en/install.windows.php`
- UNIX 上安装 PHP 的说明，位于：`http://www.php.net/manual/en/install.unix.php`
- Mac OS X 上安装 PHP 的说明，位于：`http://www.php.net/manual/en/install.macos.php`

## 索引

### A

- `ab` (ApacheBench) 工具, 382–383
- `action` 属性, 37
- 用于导航的 `action` 助手, 358–359
- Action 消息格式 (AMF), 3, 7
- actions 概述
  - 方法, 24
  - 命名规范, 34
- `ActionStack` 助手, 358
- ActiveRecord 模式, 105, 107
- 适配器 (adapters)
  - 身份, 162–164
  - 翻译文件, 289–291
- `addContext()` 方法, 193–194
- `addContext`, 193–194
- `addDecorators()` 方法, 96
- `setDisplayGroup()` 方法, 93
- `addDocument()` 方法, 183
- `addElement()` 方法, 53, 95, 150
- `addField()` 方法, 183
- `addFilter()` 方法, 70–72, 75
- `addFilters()` 方法, 72
- `addHelper()` 方法, 358
- 添加记录, 120–121
- `addMessage()` 方法, 87
- `addMultiOption()` 方法, 136
- `addPath()` 方法, 358
- `addPrefix()` 方法, 358
- `addSlash()` 函数, 70
- `addTranslation()` 方法, 290
- `addValidator()` 方法, 74, 79, 81, 92
- `addWhere()` 方法, 119
- `addWriter()` 方法, 255
- `/admin` 前缀, 141
- `adminDeleteAction()` 方法, 142
- 管理操作 (administrative actions), 140
  - 控制器, 141
  - 布局 (layout), 142–144
  - 保护, 167–168
  - 路由, 141–142
  - 结构, 140–141
- ALERT 日志级别, 257
- `Alnum` 过滤器, 73
- `Alnum` 验证器
- `Alpha` 过滤器, 73
- `Alpha` 验证器, 77, 84
- 字母和数字字符串的测试, 74
- Amazon Web service, 324–325
- `amazonAction()` 方法, 324
- AMF (Action Message Format), 3, 7
- Apache 文件, 13
- Apache Lucene 项目, 181
- ApacheBench (`ab`) 工具, 382–383
- `Apc` 缓存后端, 396
- `Api_Controller` 类, 335–339
- `$APP_DIR/` 目录, 11, 16
- `$APP_DIR/application/`, 31–33
- `Bootstrap.php` 文件, 117, 302, 357, 369
  - 内容, 12
  - 模块, 334
- `$APP_DIR/application/configs/`, 229
- `navigation.xml` 文件, 357
- `square.ini` 文件, 230, 234
- `$APP_DIR/configs/application.ini` 文件
  - 管理功能, 145
  - 应用配置, 37
  - 缓存 (caches), 405
  - Doctrine 集成, 117
  - 日志与登录, 161
  - 命名空间 (namespaces), 85
  - 页面查看, 328
  - 分页, 201
  - 搜索主机, 158
  - 上传目标地, 213
  - 用户级配置, 229–230
- `$APP_DIR/application/controller/Controller.php` 文件, 288
- `$APP_DIR/application/layouts/admin.php` 文件, 143, 168, 233, 374
- `$APP_DIR/application/layouts/master.php` 文件
  - 应用布局 (application layouts), 37
  - `autocomplete` 插件, 378
  - 表单 (forms), 88
  - 本地化 (localization), 298
  - Menu 视图
  - Menu 助手, 360
  - 新闻订阅 (news feeds), 331
  - 搜索 (searches), 179
- `$APP_DIR/application/modules/`
  - `admin/views/scripts-admin-update.php` 文件, 377
  - `api/controllers/CatalogController.php` 文件, 335
- `$APP_DIR/application/modules/catalog/directory`
  - `AdminItemController.php` 文件, 144
  - `ItemController.php` 文件, 122, 157, 215, 295
- `$APP_DIR/application/modules/catalog/scripts/item-directory/`
  - `index.php` 文件, 146
  - `index.php` 文件, 188
  - `update.php` 文件, 156
- `$APP_DIR/application/modules/catalog/views/scripts/item/directory`
  - `create.php` 文件, 138
  - `display.php` 文件, 124, 296
  - `search.php` 文件, 194
  - `success.php` 文件, 137
- `$APP_DIR/application/modules/default/`, 32
- `$APP_DIR/application/modules/default/controllers`
  - `ConfigController.php` 文件, 231
  - `ContactController.php` 文件, 371
  - `ErrorController.php` 文件, 265
  - `LocaleController.php` 文件, 307
  - `LoginController.php` 文件, 165
  - `NewsController.php` 文件, 328
- `$APP_DIR/application/modules/default/views/login.php` 文件, 166
- `$APP_DIR/application/modules/default/views/scripts/`
  - `config/index.php` 文件, 233
  - `contact/index.php` 文件, 87
  - `success/error.php` 文件, 252
  - `news/index.php` 文件, 329
- `$APP_DIR/application/views/scripts/index.php` 文件, 29, 35
- `$APP_DIR/data/indexes/`, 185
- `$APP_DIR/data/logs/`, 263
- `$APP_DIR/languages/messages.php`, 300
- `$APP_DIR/library/`, 12–13
- `$APP_DIR/library/Doctrine`, 117
- `$APP_DIR/library/Square/`
  - `Auth/Adapter/Doctrine.php` 文件, 164
  - `Controller/Helper/Navigation.php` 文件, 358
- `$APP_DIR/library/Square/Form/`
  - `Config.php` 文件, 228
  - `Contact.php` 文件, 299, 369
  - `ItemCreate.php` 文件, 130, 213
  - `ItemUpdate.php` 文件, 372
  - `Login.php` 文件, 161
- `Search.php` 文件, 177, 188
- `$APP_DIR/library/Square/Model/Item.php` 文件, 406
- `$APP_DIR/modules/catalog/`
  - `controllers/ItemController.php` 文件, 177
  - `scripts/item/search.php` 文件, 190
  - `scripts/search.php` 文件, 178
- `$APP_DIR/public/`, 12–13, 44
- `$APP_DIR/public/captcha/`, 85
- `$APP_DIR/public/css/`, 37
- `$APP_DIR/public/fonts/`, 84–85
- `$APP_DIR/public/images/`, 37
- `$APP_DIR/public/images/locale/`, 308
- `$APP_DIR/public/uploads/`, 213, 221
- `$APP_DIR/tests/`, 12
- application code, 401
- cache configuration, 405–406
- cache query results, 406–408
- cache translation strings, 406
- cache Twitter and blog feeds, 408–409
- lazy loading, 404–405
- query tuning, 401–404
- `APPLICATION_ENV` 变量, 251
- `application.ini` 文件, 230
- applications
  - configuration files, 33
  - database initialization, 109–113
  - environment, 7–8
  - index pages, 35
  - operability, 6–7
  - localization and locales. 见 localization and locales
  - master layouts, 36–37–42
  - optimizing. 见 code optimization
  - requirements, 11
  - routes, 37–40
  - views, 41–42
- `ArrayIterator`, 243
- 必填字段 (`*`), 403
- Atom System Format (ASF), 312–314
- `ATTR_QUERY_CACHE`, 300
- audio CAPTCHAs, 66
- `authenticate()`
  - `Square_Auth_Adapter_Doctrine`, 163–164
  - `Zend_Auth_Interface`, 160, 162
- authentication (method), 159–160
  - adapters, 162–164
  - user, 158–170
- auto locale, 276
- `Autocomplete` 助手, 358
- `autocomplete()` 方法, 371
- autoloading directory, 116–118

### B

- backends, cache, 395–397
- `Barcode` 验证器, 78
- `BaseName` 过滤器, 73
- benchmarking performance, 382–384
- 全文搜索的二进制字段, 182
- `Blackhole` 缓存后端, 396
- blogs
  - feeds, cache, 408–409
  - Twitter integration, 328–332
- `Bootstrap` 类
  - Doctrine initialization, 117
  - `view` 助手, 369–370
  - locales, 275–277, 293–294, 307
  - navigation objects, 352, 357
  - query profiling, 388–391
  - REST routes, 340–342
  - translation objects, 302, 406
- `Breadcrumbs` 导航助手, 353–354
- brokers 助手, 358
- browsers
  - caches, 392
  - locale, 276
- Buck, James, 106
- `Button` 视图助手, 364
  - 用于表单, 61–63

### C

- `cacheAction()`, 393–399, 401
- `cachegrind` 文件, 385
- caches, 392
  - cache manager, 398–399
  - configuring, 405–406
  - Doctrine queries, 399–401, 410
  - frontends and backends, 395–397
  - operations, 392–395
  - query results, 406–408
  - translation strings, 406
  - Twitter and blog feeds, 408–409
- calendars. 见 YUI calendar 插件
- `Callback` 过滤器, 73
- camel-case 名称, 34, 111
- 表单中的 CAPTCHA 字段, 63–65
- CAPTCHAs (全自动图灵测试), 66, 84
- 捕获前端, 395
- CardSpace, 7
- `Catalog_AdminController` 类
  - 管理操作, 144, 146–150, 155
  - 数据库记录, 201–206, 218–219
- `Catalog_AdminItemController` 类（续）
  - `index` 动作, 186–187
  - 日志记录动作, 167–168
  - YUI 清空小部件, 375–377
- `Catalog_ItemController` 类
  - 管理动作, 157–158
  - 应用配置, 236–237
  - 缓存, 206–208
  - 数据库记录, 122–124
  - 表单, 136–137
  - 数字位置, 295–296
  - 搜索, 177–188, 194
  - 上传的文件, 215–218
- `catch` 块, 242–245
- `Ccenum` 验证器, 78
- CDN (内容交付网络), 363
- 链
  - 过滤器, 79
  - 继承, 106
  - 方法, 54
- `CheckBox` 视图助手, 364
  - 表单复选框, 57–59
- Class case frontend, 395
- `clearDecorators()` 方法, 96
- 关闭的 PHP 标签, 41
- code
  - 优化。详见应用代码优化
  - 性能分析, 384–387
- 代码生成工具, 6
- `ComboBox` 视图助手, 364
- 命令行工具, 14
- 商业支持, 77
- 社区支持, 5
- 全自动公开图灵测试 (CAPTCHAs), 66, 84
- 组件交互, 26–28
- `configAction()` 方法, 222–227
- `ConfigController` 类, 213–233
- 配置文件
  - 应用, 33, 37
  - 控制器与视图, 213–233
  - 定义, 229
  - 表单, 227–229
  - 主布局, 233–235
  - 读取, 222–224
  - 路由, 230
  - 存储, 230
  - 使用, 235–238
  - 写入, 224–227
- 一致性, 264
- `__construct()` 方法
  - `MemberModel`, 103
  - `Square_Auth_Adapter_Doctrine`, 163
  - `Square_Controller_Action_Helper_Navigation`, 359
  - `Square_Log_Writer_Doctrine`, 264
- 消费
  - 新闻订阅, 313–317
  - Web 服务, 322–328
- 创建, 82
- Dojo 自动完成小部件, 368–369
  - 本地化目标, 299–300
- `ContentController` 类, 28, 86–90, 235–238, 371
- 容器, 346–355
- 内容交付网络 (CDN), 363
- `ContentPane` 视图助手, 364
- 上下文, 192–194
- `ContextSwitch` 助手, 192–358
- 控制器属性, 37
- controllers
  - 管理的, 140–141
  - 配置文件, 213–233
  - CRUD 操作, 136–139
  - Dojo 自动完成小部件, 371
  - 表单, 86–88
  - 模型, 122–124
  - MVC 模式, 23–24
  - 命名规范, 34
  - 新闻订阅, 328–331
  - 基于 REST 的 Web 服务, 334–335
  - 搜索, 177–179
  - YUI 清空小部件, 375–377
- conversions
  - 货币, 285
- `convertNumber()` 方法, 278–279
- `convertTo()` 方法, 286
- 受版权保护的文件, 84
- 核心缓存前端, 395
- `Count` 验证器, 78, 211
- 国家，区域, 274–273
- `crc32` 验证器, 78, 211
- 为上传的文件创建创建动作, 215–216
- 创建、读取、更新和删除。见 CRUD
- `CREATE TABLE` 命令, 402
- `createAction()` 方法, 136–137, 215–216
- `createElement()` 方法, 54
- `createFulltextIndexArray()` 方法, 186–187
- CRIT 日志级别, 257
- 标准则，排序, 204
- 跨站请求伪造 (CSRF) 攻击, 63–64
- 跨站脚本攻击, 127
- CRUD (创建、读取、更新和删除)
  - 操作, 130
- CSRF (跨站请求伪造) 攻击, 63–64
- `ctype_alnum()` 函数, 74
- `ctype_alpha()` 函数, 74
- 货币值, 273, 282–285
- `currency()` 方法, 283–284
- 货币视图助手, 364

### D

- `Api_CatalogController`, 335
- `Catalog_AdminItemController`, 148–149, 218
- `Sandbox_RestController`, 323
- `deleteAction()` 方法
  - 拒绝访问, 170
- 描述装饰器, 95
- `description()` 方法, 317
  - 上传的文件, 213
- `/dev/null` 文件, 256
- 开发环境, 251–252
- 数字过滤器, 73
- 数字验证器, 77
- 数据源 (DSN), 117–118
- 翻译数据, 269–291, 300–301
- 数据库，应用, 109–113
- DataMapper 模式, 105, 107
- `disable()` 方法, 370
- `disable` 选项, 289
- 禁用装饰器, 96
- 示例, 405–406
- 磁盘内存缓存, 399
- `date()` 方法, 281
- `Date` 验证器, 78
- `dateAction()` 方法, 279–282
- 显示动作, 157–158
- `display_errors`, 251
- 表单中的显示组, 93–94
- `display()` 方法, 203
- `display_startup_errors`, 251
- 表单输入, 153
- 区域, 273, 279–282
- `displayAction()` 方法
  - `Catalog_ItemController`, 123–124, 157–158, 216–218, 237–295, 406–408
  - `ItemController`, 138
  - `StaticContentController`, 40
- `Db_NoRecordExists` 验证器, 78
- `Db_RecordExists` 验证器, 78
- `<dd>` 元素, 95, 98
- DEBUG 日志级别, 257
- 表单装饰器, 94–99
- 解密过滤器, 73, 211
- 默认首页, 28–30
- 默认模块, 338
- 默认路由, 25
- 表单上的默认值, 65–69
- Del.icio.us 服务, 7
- delete actions
  - 管理动作, 167–168
  - 身份适配器, 162–164
  - 控制器与视图, 136–139
  - 数字输入, 153
  - 删除动作, 148–150
  - 显示动作, 157–158
  - 表单, 130
  - 定义, 148–150
  - 记录, 120–121
  - 上传的文件, 218–221
  - 布局, 142–144
  - 列表动作与视图, 146–148
  - 登录动作, 165–166
  - 登录表单, 161–162
  - 登出动作, 167
  - 主布局, 141–142, 144–145
  - 结构, 140
  - 摘要, 170–171
  - 更新动作与视图, 154–157
  - 更新表单, 150–152
- `delete()` 方法
  - DQL, 121
  - 模式, 105
- `DELETE` 方法
  - HTTP, 320
  - REST 路由, 333
- 删除 URL, 145
- `deleteAction()` 方法
- `Doctrine_Manager` 类, 118, 400
- `Doctrine_Pager` 类, 201, 203, 238
- `Doctrine_Pager_Layout` 类, 203, 206
- `Doctrine_Query` 类, 119, 399, 401
- Doctrine 查询语言 (DQL), 107, 118
- `Doctrine_Record` 类, 118
- `Doctrine_tool`, 22
  - 适配，并删除记录, 120–121
  - 自动加载, 116–118
  - 数据库查询, 390–391
  - 安装, 107–109
  - 模型生成, 113–115
  - 模型关系, 115–116
  - 查询缓存, 399–410
  - 记录检索, 118–120
- 文档, 7
- Dojo 自动完成小部件, 368
  - 控制器, 371
  - 表单, 368–369
  - 主层, 370
  - 视图助手, 369–370
- `dojo.data.itemFileReaderDatastore`, 361
- `dojo.data.itemFileWriteStore` datastore, 361
- dojo Toolkit, 346, 361
  - 数据, 361–362
  - 表单元素, 365–367
  - 视图助手, 362–365
- `dojo_Action()` 方法, 361
- 本地的美元 (`$`) 符号, 273
- `DOMDocument` 类, 315
- `DOMElement` 类, 315
- `DOMXPath` 类, 315
- 不要重复自己 (DRY) 方法, 106
- 双重问题, 137
- DQL (Doctrine 查询语言), 107, 118
- DRY (不要重复自己) 方法, 106
- DSN (数据源名称), 117–118
- `<dt>` 元素, 95, 98
- `dump()` 方法, 254
- `DuplicateFileException`, 244

### E

- EMERG 日志级别, 257
- `enable()` 方法, 370
- `enableView()` 方法, 363, 370
- 加密过滤器, 73, 211
- `$_ENV` 变量, 254
- 环境区域, 276
- ERR 日志级别, 257
- 默认过程, 246–249
- 错误页面, 252–254
- 异常类, 245–242
- 异常可见性, 251
- 汇率, 285
- `Extension` 验证器, 78, 211
- `Exists` 验证器, 78, 211
- `execute()` 方法, 203
- `EXPLAIN` 关键字, 392
- 日志事件, 258

### F

- `factory()` 方法, 247, 249
- `fail()` 方法
  - `Square_Log_Writer_Doctrine`, 265
  - `Zend_Cache`, 394
- 胖模型, 105–106
- `feedAction()` 方法, 313–318
- `fetch()` 方法
  - `MemberModel`, 103
  - 模式, 105
- `fetchAll()` 方法, 103
- `Editor` 视图助手, 364
- 效率, 264
- 邮箱地址, 90
- `EmailAddress` 验证器, 78
- `fetchArray()` 方法, 190
  - 新闻订阅, 313
  - 日志消息, 259–263
- `FormElements` 装饰器, 95
- `FormErrors` 装饰器, 95
- 表单, 55–57, 60–61, 63–65
  - 索引连接, 403
  - 必须, 403
  - 搜索, 182
- `Fieldset` 装饰器, 95
- 上传的文件, 60–61, 61–205
- 文件缓存后端, 396
- 文件缓存前端, 395
- 上传的文件, 60–61
  - 使用, 209–212
- `$_FILES` 全局变量, 209
- `FileSize` 验证器, 78, 211
- 基于过滤器的数据库查询对比全文搜索, 192
- `filter_var()` 函数, 74
- `FilteringSelect` 助手, 364
- 过滤器
  - 基础, 48–52
  - 按钮, 61–63
  - 配置, 227–229
  - 联系, 82
  - 控制器与查看器, 86–88
  - 数字输入, 153
  - 装饰器, 94–99
  - 定义, 82, 135–136
  - 显示组, 93–94
  - Dojo, 365–369
  - 元素创建, 53–55
  - 错误消息, 50, 91–92
  - 过滤器链, 79–81
  - Hash 和 CAPTCHA 字段, 63–65
  - 输入过滤器, 70
  - 输入检索和处理, 81–82
  - 输入验证器, 73–81
  - 本地化目标, 299–300
  - 登录, 161–162
  - 主布局, 88–89
  - 命名空间, 85
  - 单选按钮和复选框, 57–59
  - 必须和默认值, 65–69
  - 路由, 85–86
  - 搜索, 174, 177–188
  - 选择列表, 59–60
  - 摘要, 99–100
  - 文本和隐藏字段, 55–57
  - 更新, 150–152
  - YUI 日历小部件, 372–374
- 404 异常, 124, 158, 253
- Fowler, Martin, 105
- 前端控制器, 24, 27
- 前沿缓存, 395–397
- 全文系列, 181–182
  - 对比过滤器的数据库查询, 192
  - 索引动作与视图, 186–187
  - 索引位置, 185
  - 索引数据, 182–184
  - 路由, 186
  - 搜索动作与视图, 189–191
  - 搜索表单, 188–189
  - 搜索数据, 184
  - 摘要视图, 188
- 链, 79–81
- 表单, 52–70, 73–135
  - 记录检索, 119
  - 上传的文件, 210–211
- `find()`
  - Doctrine, 118, 155
  - DQL, 121
  - `Zend_Search_Lucene`, 180
- `findAll()` 方法, 118
- `findBy()`, 351, 359
- `findCheapestServiceProvider()` 方法, 396
- Firebug 控制台, 263, 389–391
- 500 异常, 243, 285
- `FlashMessenger` 工具, 87, 358
- `Float` 验证器, 77
- 链式接口, 119
- 字体，版权, 84
- 外键关系, 116
- `Form_Example` 类, 53–69
  - 装饰器, 96–98
- 完整版本, 9
- 缓存缓存前端, 395

### G

- GData APIs, 3
- `generateModelsFromDb()` 方法, 114–116
- 通用 Web 服务实现, 325–328
- `geocode()` 方法, 326
- GeoCoder Web 服务, 325
- GET 动作, 156
  - HTTP, 320
  - 基于 REST 的 Web 服务, 336–338
  - REST 路由, 333
- `get()` 方法
  - 日期和时间, 280
  - `Zend_Registry`, 302
  - `Zend_Http_Client`, 327
- `getAction()` 方法
  - `Api_CatalogController`, 335–338
  - `Sandbox_RestController`, 333
- `getCache()` 方法, 399
- `getCode()` 方法, 344
- `addContainer()` 方法, 359
- `getContent()` 方法, 315
- `getCountries()` 方法, 315
  - 创建, 135–136
- `dateModified()` 方法, 315
- `getDescription()` 方法, 315
- `getDomDocument()` 方法, 315
- `getElapsedSecs()` 方法, 388
- `getElement()` 方法, 254
- `getEnv()` 方法, 254
- `getFile()` 方法, 244
- `getGrades()` 方法
  - `Square_Form_ItemCreate`, 135–136
  - `Square_Form_Search`, 176
- `getHelper()` 方法, 358
- `getIdentity()` 方法, 160
- `getInvokeArg()` 方法, 187
- `getItem()` 方法, 406–407
- `getLabel()` 方法, 348
- `getLanguage()` 方法, 275
- `getLastRequest()` 方法, 328
- `getLastResponse()` 方法, 328
- `getLine()` 方法, 244
- `getLink()` 方法, 315
- `getMessage()` 方法, 244
  - 显示, 93–94
  - 检索结果, 119
- `getMessages()` 方法
  - `FlashMessenger`, 87
  - `Zend_Form`, 81
- `getParam()` 方法, 40
- `getParams()` 方法, 254
- `getQuery()` 方法, 388
- `getQueryProfiles()` 方法, 388
- `getRegion()` 方法, 275
- `getRel()` 方法, 348
- `getResource()` 方法, 238
- `getResultArray()` 方法, 164
- `getRev()` 方法, 348
- `getServer()` 方法, 254
- `getSql()` 方法, 120
- `getTimezone()` 方法, 282
- `getTitle()` 方法, 315
- `getTrace()` 方法, 244
- `getTraceString()` 方法, 244
- `getTransferAdapter()` 方法, 216
- `getTranslationList()` 方法, 279
- `getType()` 方法, 135–136
- `getUnfilteredValues()` 方法, 81
- `getValues()` 方法, 81, 214
- `getVideo()` 方法, 325
- `getVisibility()` 方法, 348
- `getXpath()` 方法, 315
- `glob()` 函数, 217
- GNU gettext, 291–292
- Google Data APIs, 7
- 授予访问, 170
- `GreaterThan` 验证器, 78
- `groupBy()` 方法, 119
- 组
  - 显示, 93–94
  - 检索结果, 119
- Gutmans, Andi, 3

### H

- `handleInputDisplayOnSelect()` 函数, 153, 156
- Hartjes, Chris, 106
- 哈希字段用于, 65–96
- `Hash` 验证器, 78, 211
- `hashIdentity()` 方法, 168
- `hasMany()` 方法, 115
- `hasOne()` 方法, 115
- `header()` 方法, 318
- `HeadLink` 视图助手, 374–375, 377
- `HeadScript` 视图助手, 374–377
- 助手代理, 358
- 助手，视图, 362–365, 369–370
- `Hex` 验证器, 77
- 表单隐藏字段用于, 55–57
- `HorizontalSlider` 视图助手, 364
- `Hostname` 验证器, 78
- `.htaccess` 文件, 27, 251
- `htmlEntities` 过滤器, 70, 135
- `htmlentities()` 函数, 70
- `htmlTag` 装饰器, 95, 153
- HTTP 方法, 320
- HTTP 请求, 369
- `httpd.conf` 文件, 13
- `httpd-hosts.conf` 文件, 13

### I

- `PostController`, 28
- `Sandbox_ExampleController`, 183
- `Sandbox_RestController`, 333
- `IndexController` 类, 27–28, 35, 37
- 索引
  - 动作, 186–187
  - 数据库记录, 201–204
  - 索引过程, 182–184
  - 位置, 185
- INFO 级别, 257
- 实例链, 106
- `ini_set()` 函数, 15
- `init()` 方法, 432
  - `Api_CatalogController`, 335
  - `Catalog_ItemController`, 122–194
  - `ConfigController`, 231
  - `ContactController`, 86–87, 220–236, 238
  - `IndexController`, 28, 35, 37
  - `ListingController`, 24–25
  - `LocaleController`, 306–307
  - `NewsController`, 28, 328–329, 408–409
- 输入表单
  - 日期, 153
  - 过滤器, 70–73
  - 检索和处理, 82
  - 验证器, 73–81
- `INSERT_SELECT` 语法, 402–403
- Acme 安装
  - Doctrine, 107–109
  - Zend Framework, 8–10
- `Int` 过滤器, 73
- `Int` 验证器, 77
- 国际化, 5
- 互联网工程任务组 (IETF)，标准, 313
- 应用程序互操作性, 6–7
- “无效输入”错误, 126
- `Ip` 验证器, 78
- `is_numeric()` 函数, 74
- `is_uploaded_file()` 方法, 209
- `IsCompressed` 验证器, 78, 211
- `IsImage` 验证器, 78, 211
- `isValid()` 方法
  - `Square_Form_Contact`, 87
  - `Zend_Auth_Result`, 160
  - `Zend_Filter_Input`, 124
  - `Zend_Form`, 81, 155
  - `ItemController`, 138
- `itemSearch()` 方法, 325

### J

- 连接表, 119–120
- 连接与子查询, 401–402
- jQuery 工具包, 346
- JSON 助手, 358

### K

- CacheGrind 工具, 385
- 表单键, 63
- 全文搜索关键词, 181–182
- KISS (Keep It Simple!), 403

### L

- `Label` 装饰器, 95
- 区域中的语言, 273–304
- 布局
  - 主布局, 25–26
- 懒性加载, 114–405
- 软耦合架构, 3–6
- `LessThan` 验证器, 78
- 库
  - 添加, 13
  - Yahoo! 用户界面, 372
  - 库目录, 9, 13
- 缓存生命周期属性, 393
- `Links` 助手, 354
- 列表动作, 146–148
- `listAction()` 方法, 193, 337
- `ListingController` 类, 24–25
- `ListingModel` 类, 261
- `load()` 方法, 395
- 加载
  - 缓存数据, 395
  - Doctrine, 116–118
  - 懒性加载, 404–405
  - 区域标识符, 273–274
- `localeAction()` 方法, 274–275, 292–293
- `LocaleController` 类, 306–307
- 本地化和区域, 272
  - 应用设置, 274–279
  - 货币, 282–285
  - 日期和时间, 279–282
  - 手动选择, 306–308
  - 主布局, 307
  - 测量值, 285–287
  - 数字, 277–279, 294–295
  - 概览, 272–274
  - 字符串, 287–294, 298–300
  - 翻译注册, 302–305
- `log()` 方法, 255–256
- `logAction()` 方法, 254
- 日志数据
  - 添加日志消息, 254
  - 错误控制器, 265–268
  - 格式化消息, 259–263
  - 日志位置, 263–264
  - 日志写入, 264–265
  - 写入日志消息, 254
- `loginAction()` 方法, 162, 165–168
- `LoginController` 类, 162, 165–167
- 登录
  - 动作和视图, 165–166
  - 身份验证适配器, 162–164
  - 表单, 161–162
  - 路由, 161
- 登出动作, 167
- `logoutAction()` 方法, 167
- `LowerCase` 过滤器, 73
- 小写翻译键, 306
- Lucas, Matthew, 265
- `leftJoin()` 方法, 119
- 本地化过滤器, 73

### M

- 手动区域选择, 306–307
- 多对多关系, 115–116
- 市场信誉, 63
- 主层, 33
  - 管理动作, 142–144
  - 应用, 36–37, 42–44
  - 配置文件, 233–235
  - CRUD 操作, 168–169
  - Dojo 自动补全组件, 370
  - 表单, 89
  - 本地化, 307–308
  - 新闻源, 331–332
  - 搜索, 179–181
  - 存储, 39
  - YUI 日历组件, 374–375
- 范围, 105–106
- 摘要, 127–128
- 视图, 124–127
- 模块属性, 37
- 模块
  - 创建, 122
  - 默认, 33
  - 覆盖方式, 24–25
- 基于 REST 的 Web 服务, 334
- MooTools 工具包, 346
- `move_uploaded_file()` 方法, 209
- `multipart/form-data` 类型, 61
- 多输出类型, 192–193
- 多选择列表, 59–60
- `Md5` 验证器, 78, 211
- `measureAction()` 方法, 285–287
- 测量区域, 285–287
- `MemberModel` 类, 103
- `Memcached` 缓存后端, 396
- 内存缓存
  - 与磁盘键对比, 309–406
- MVC (模型-视图-控制器) 模式, 31, 23
  - 控制器, 23–24
  - 模型, 21–22
  - 视图, 22–23
- MySQL 数据库
  - 初始化, 109–113
  - 表名, 111

### N

- 菜单
  - 导航结构, 352–353
  - 导航视图助手, 359–360
- 方法, 24
  - 链, 554
  - SOAP, 322
- Microsoft CardSpace, 7
- `MIMEType` 验证器, 78, 211
- 最小版本, 9
- `MissingException` 类, 244
- `mktime()` 函数, 279
- 模型-视图-控制器 (MVC) 模式, 3, 21
  - 控制器, 23–24
  - 模型, 21–22
  - 视图, 22–23
- 模型, 102
  - 应用数据库, 109–113
  - 控制器、动作和视图, 34
  - 数据库表, 111
  - 表单命名空间, 85
- `navAction()` 方法, 347–348, 350–351
- 导航结构, 346
  - 动作助手, 358–359
  - 面包屑, 353–354
  - 菜单视图助手, 359–360
  - 菜单, 352–353
  - 页面和容器, 346–361, 355–357
  - 注册导航对象, 357
  - 渲染, 351–355
  - Sitemap 助手, 354–356

### O

- 对象缓存前端, 395
- 面向对象设计, 4
- 输出缓存前端, 395

### P

- 分页, 201–204
- 页面和容器, 346–361
- 页面缓存, 392
- 页面标题, 37
- 部分, 352
- 密码, 161–162
- 性能, 382–384
- 性能分析, 384–387
- 权限, 167–168
- 持久性数据库连接, 404
- PHP
  - 安装, 14–15
  - 标签, 41
- 占位符, 95
- 插件, 24
- `postAction()` 方法
  - `Api_CatalogController`, 335, 339
  - `Sandbox_RestController`, 333
- POST 方法
  - HTTP, 320
  - REST 路由, 333
- 基于 REST 的 Web 服务, 339
- 预处理语句, 403
- 主布局, 25–26
- 私有消息, 7
- 生产环境, 251–252
- 性能分析器, 384–385
- 项目结构, 11–13
- Propel 工具, 22, 107
- `protectedAction()` 方法, 160
- 保护管理操作, 167–168
- PUT 动作
  - 文件上传, 209
  - HTTP, 320
  - REST 路由, 333
- `put()` 方法, 327
- `putAction()` 方法
  - `Api_CatalogController`, 335
  - `Sandbox_RestController`, 333–334

### Q

- Qcodo 工具, 107
- 查询
  - 缓存结果, 406–408
  - Doctrine, 399–401
  - 性能分析, 387–392
  - 调优, 401–404
- `queryAction()` 方法, 386–389
- 表单输入, 81–82
- 记录, 118–120

### R

- 可重用性, 4
- 右连接, 120
- `route` 属性, 37
- 路由, 33
  - 管理操作, 141–142
  - 应用, 37–40
  - 配置文件, 230
  - CRUD 操作, 141–142, 145, 161
  - 表单, 85–86
  - 全文搜索, 186
  - 登录和注销, 161
  - 模型, 122
  - 新闻馈送, 328
  - 概述, 25
  - 静态内容, 39–40
- 表单单选按钮, 57–59
- 快速发布周期, 6
- 读取配置文件, 222–224
- 简单 (RSS) 格式, 312–313
- `RealPath` 过滤器, 73
- `receive()` 方法, 214, 216
- 记录
  - 添加、更新和删除, 120–121
  - 分页与排序, 201–208
  - 检索, 118–120
- `RecursiveLocatorIterator` 类, 351
- Redbean 工具, 107
- `Redirector` 助手, 358
- 重构模型方法, 410
- `Regex` 验证器, 78, 135
- 页面码, 201
- 基于 REST 的 Web 服务, 332–334, 340
  - 控制器, 334–335
  - GET 动作, 336–338
  - 模块, 334
  - POST 动作, 339
  - 路由, 322–334, 340–342
- 排序标准, 204
- 注册
  - 导航对象, 357
  - 翻译对象, 302–305
- 表单验证的正则表达式, 74
- 模型中的关系, 115–116
- 远程 HTTP 请求, 369
- `removeElement()` 方法, 150
- `removeHelper()` 方法, 358
- 路由请求, 25
- 路由子系统, 34
- 行级锁机制, 403
- RSS (简单同义词) 格式, 312–333
- 重命名文件, 73
- `rename` 验证器, 211
- 渲染导航元素, 351–355
- `renderMenu()` 方法, 352
- `restAction()` 方法, 327
- 查询结果缓存, 406–410, 418

### S

- `Sandbox_ExampleController` 类
  - 管理操作, 142
  - 缓存前端和后端, 395–397
  - 缓存管理器, 398–399
  - 缓存操作, 393–394
  - 缓存 Doctrine 查询, 400–401
  - 代码性能分析, 386–387
  - 配置文件, 222–227
  - 货币本地区域, 283–285
  - 日期和时间本地区域, 279–282
  - Dojo, 361–362
  - 异常, 247, 249
  - 索引, 183–184
  - 本地区域, 274–277
  - 日志, 254–262
  - 测量本地区域, 285–287
  - 模型, 104–105
  - 多输出类型, 192–193
  - 新闻馈送创建, 313–317
  - 新闻数量, 277–279
  - 页面和计数器, 347–350
  - 查询性能分析, 388–389
  - 字符串本地区域, 278–280, 293
  - 上传的文件, 210
  - 用户认证, 159–160
  - Web 服务, 323–327
- `Sandbox_RestController` 类, 333–334
- Savant 模板, 23
- `save()` 方法
  - Doctrine, 155, 265
  - 表单, 137
  - `MemberModel`, 103–104
  - 模式, 105
  - `Zend_Cache`, 395
- `saveAction()` 方法, 104–105
- `saveXml()` 方法, 318
- 模型范围, 105
- `search()` 方法, 329
- `searchAction()` 方法, 194–195
  - `Catalog_ItemController`, 177, 178, 189
  - `Sandbox_ExampleController`, 184
- 控制器和视图, 177–179
- 表单, 174–177
- 全文搜索
  - 主布局, 179–181
  - 摘要, 196–197
  - XML, 194–196
- 选择列表, 59–60
- 自引用, 115
- `send()` 方法
  - `Zend_Feed`, 318, 337
  - `Zend_Mail`, 87
- `sendAction()` 方法, 28
- `$_SERVER` 数组, 254, 276
- 服务器配置, 404
- 服务器客户端, 322–325
- `set_error_handler()` 函数, 243
- `set_exception_handler()` 函数, 243
- `set()` 方法, 302
- `setAction()` 方法, 53
- `setAttribs()` 方法, 61
- `setAutoInsertNotEmptyValidator()` 方法, 67
- `setCache()` 方法, 409
- `setBase()` 方法, 363
- `setCheckedValue()` 方法, 58
- `setData()` 方法, 124
- `setDecorators()` 方法, 96, 98, 177
- `setDefaults()` 方法, 67
- `setDescription()` 方法, 54
- `setDestination()` 方法, 210
- `setElementDecorators()` 方法, 177
- `setEncType()` 方法, 61
- `setEvent()` 方法, 259–260
- `setFacility()` 方法, 258
- `setFormat()` 方法, 284
- `setFormatter()` 方法
  - `Square_Log_Writer_Doctrine`, 264
  - `Zend_Log_Writer`, 255
- `setImage()` 方法, 62
- `setLabel()` 方法, 54, 348
- `setLayout()` 方法, 144
- `setLegend()` 方法, 93
- `setLocale()` 方法, 276, 289
- `setLocalPath()` 方法, 363
- `setMessage()` 方法, 92
- `setMethod()` 方法, 53
- `setMultiFile()` 方法, 61, 214
- `setMultiOptions()` 方法, 58–59
- `setOptions()` 方法, 54
- `setPartial()` 方法, 352
- `setRel()` 方法, 348
- `setRequired()` 方法, 65, 67
- `setResultLimit()` 方法, 185
- `setRev()` 方法, 348
- `setTimezone()` 方法, 282
- `setUncheckedValue()` 方法, 58
- `setUp()` 方法, 115–116
- `setValue()` 方法, 67
- `setValueDisabled()` 方法, 214
- `setVisibility()` 方法, 348
- `Sha1` 验证器, 78, 211
- 共享托管环境, 15
- 简单对象访问协议 (SOAP), 320–322, 328
- `SimpleXML` 类, 195, 327
- 单控制器，创建, 140
- 单选择列表, 59–60
- `sitemap` 助手, 354–356
- `Size` 验证器, 281
- 骨架，应用, 11
- 小事务, 403–404
- SOAP (简单对象访问协议), 320–322, 328
- `soapAction()` 方法, 325
- 排序记录, 204–208
- 元素, 176
- `Sqlite` 缓存后端, 396
- SQ Web 服务, 3
- SQUARE 管理面板, 140
- `Square_Auth_Adapter_Doctrine` 类, 163–164
- `Square_Controller_Helper_Navigation` 类, 359
- SQUARE 示例应用, 11
- `Square_Form` 类, 228–229
- `Square_Form_Contact` 类, 83–84, 279, 368–369
- `Square_Form_ItemCreate` 类, 130–136, 213–214
- `Square_Form_ItemUpdate` 类, 150–152, 374
- `Square_Form_Search` 类, 175–177, 188–189
- `Square_Log_Writer` 类, 264–265
- `Square_Model_Item` 类, 116, 406–407
- `StackContainer` 视图助手, 364
- 栈过滤器, 79–81
- 标准合性, 4
- `start()` 方法, 385
- 启动项目, 10–16
- 静态缓存后端, 296–397
- 静态内容
  - 测试, 74
  - 控制器, 40
  - 路由, 39–40
  - `StaticContent` 类, 39–40
- `stop()` 方法, 385
- 存储配置文件, 230
- string-transposition 操作, 65
- `StringLength` 验证器, 77
- strings 本地, 287–294, 300
- `strip_tags()` 函数, 70
- `StripTags` 过滤器, 73
- `strtoupper()` 函数, 306
- 结构化管理操作, 140–141
- 导航结构
- 子查询, 401–402
- `successAction()` 方法
  - `Catalog_AdminController`, 149–150
  - `Catalog_ItemController`, 136–137
  - `ConfigController`, 232–233
  - `ContactController`, 86–87
  - `LoginController`, 166
- 支持, 5
- `switch-case()` 例程, 251
- 在生产和开发之间切换环境, 251

### T

- `TabContainer` 视图助手, 364
- 表名, 111
- 表格设计, 404
- 连接, 119–120
- 临时数据和计算, 402–403
- Technorati 服务, 7
- 模板文件, 36–37
- 临时表, 402–403
- `Test` 缓存后端, 396
- 文本字段, 55–57
- 全文搜索, 182
- `Textarea` 视图助手, 364
- 第三方互操作性, 6–7
- `Ticket` 模型, 103
- 时间，本地化, 279–282
- `TimeTextBox` 视图助手, 364
- 区域, 282
- `title()` 方法, 317
- `toArray()` 方法, 362
- `toCurrency()` 方法, 283
- `toJson()` 方法, 362
- `toNumber()` 方法, 277–278, 295
- transaction size, 403–404
- 临时数据和计算, 402–403
- `translate()` 函数, 306
- `translation()` 方法, 288, 290–291
- translation files, 277–288
  - 适配器数据结构, 289–291
  - 应用位置, 291–293
  - 数据源, 300–301
  - view helpers, 293–294
- translation keys, 306
- 翻译对象, 注册, 302–305
- translation strings, 缓存, 406
- `try` 块, 242–245
- Twitter 服务, 7
  - 日志搜索, 328–332
  - 缓存馈送, 408–409
- `two_Levels` 缓存后端

### U

- `ucfirst()` 函数, 306
- `ul` 元素, 95
- 本地区域中的下划线 (`_`), 273
- 全文搜索中的未索引字段, 182
- 缓存的唯一标识符属性, 393
- `UNIQUE` 关键字, 403
- 单元测试策略, 6
- 全文搜索中的未存储字段, 182
- 更新-表单, 150–152
- `update()` 方法, 105, 121
- update URLs, 145
- `updateAction()` 方法, 153–155, 375–376
- 更新配置文件, 327
- 显示动作, 157–158
- 记录, 120–121, 157
- 上传的文件, 209–212
- 路由, 39–40, 144–145
- 排序标准, 206, 208
- validity checking, 74
- 用户访问控制, 170
- 用户认证, 158–160, 170
- 用户界面元素
  - Dojo Toolkit, 361–371
  - 导航结构。参见导航结构
  - 概述, 346
  - YUI 日历组件, 372–378
- `useResultCache()` 方法, 401
- UTF-8 编码, 301

### V

- 表单验证, 50
- `ValidationTextBox` 视图助手, 364
- 验证器, 52
  - 输入, 73–81
  - 上传的文件, 210–211
- `var_dump()` 函数, 254
- `VerticalSlider` 视图助手
- view helpers, Dojo, 362–369, 370
- `ViewHelper` 装饰器, 95
- `ViewRenderer` 助手, 358
- 视图
  - 应用, 41–42
  - 配置文件, 231–233
  - CRUD 操作, 136–139, 146–148, 154–157
  - 表单, 86–88
  - 全文搜索, 186–191
  - 登录, 165–166
  - 模型, 124–127
  - MVC 模式, 22–23
  - 命名规范, 34
  - 新闻馈送, 328–331
  - 分页, 201–204
  - 搜索, 177–179
  - XML, 194–196
- 虚拟主机, 13–14
- 异常的可见性, 251

### W

- 浏览器缓存, 392
- Web 容量分析工具 (WCAT), 383–384
- Web 分布式数据交换 (WDDX), 312
- Web 服务描述语言 (WSDL) 文件, 320–321, 326
- Web 服务, 7
  - 消费端, 322–328
  - 概述, 319–322
  - 基于 REST 的, 332–344
- `Webgrind` 文件, 385
- `where()`, 119
- 必填字段通配符, 403
- `WinCacheGrind` 工具, 385
- `WordCount` 过滤器, 211
- `WordCount` 验证器, 159
- `_write()`
- WSDL (Web 服务描述) 语言, 320–321, 326

### X

- `XCache` 缓存后端, 396
- Xdebug 剖析器, 384–385
- `xdebug.profiler_output_dir` 变量, 385
- `xdebug.trace_output_dir` 变量, 385
- XML
  - 配置文件, 225–227
  - 上下文, 194
  - 日志数据, 261–263
  - 使用 SOAP, 320
  - 视图, 194–196
- XPath 查询, 327

### Y

- Yahoo! 服务, 7
- Yahoo! 用户界面库 (YUI), 372
- YahooFlickr 服务, 7
- `youtubeAction()` 方法, 324
- YUI (用户界面库), 372
- YUI 日历小部件, 372
  - 控制器, 375–377
  - 表单, 372–374
  - 主布局, 374–375
  - 视图, 377

### Z

- `Zend_Application_Bootstrap_Bootstrap` 类, 238
- `Zend_Auth` 类, 3, 159–162, 170
- `Zend_Auth_Adapter_DbTable` 类, 162–163
- `Zend_Auth_Interface` 类, 160, 164
- `Zend_Auth_Result` 类, 159
- `Zend_Auth_Storage_Interface`, 159
- `Zend_Cache` 类, 3, 392–395, 406
- `Zend_Cache_Manager` 类, 398–405
- `Zend_Config` 类, 222, 245–350
- `Zend_Config_Writer` 类, 224, 233
- `Zend_Config_Writer_Array` 类, 227
- `Zend_Config_Writer_Xml` 类, 225
- `Zend_Config_Xml` 类, 223
- `Zend_Controller_Action` 类, 24, 333
- `Zend_Controller_Request_Http` 类, 254
- `Zend_Currency` 类, 5, 282–285
- `Zend_Date` 类, 25, 275–282, 295
- `Zend_Db_Adapter` 类, 107, 256
- `Zend_Db_Adapter_Abstract` 类, 160
- `Zend_Db` 类, 22, 162–163, 387
- `Zend_Db_Profiler` 类, 387–388
- `Zend_Db_Profiler_Firebug` 类, 389
- `Zend_Db_Profiler_Query` 类, 388
- `Zend_Db_Table` 类, 107
- `Zend_Debug` 类, 242, 254
- `Zend_Doctrine_Manager` 类, 399
- `Zend_Dojo` 类, 342, 362, 365
- `Zend_Dojo_Data` 类, 362, 371
- `Zend_Dojo_Form_Element` 类, 365
- `Zend_Dojo_Form_Element_*` 类, 366
- `Zend_Exception` 类, 246
- `Zend_Feed` 类, 312, 316–318, 337
- `Zend_Feed_Reader` 类, 312–313, 315–329, 409
- `Zend_Feed_Atom` 类, 315
- `Zend_Feed_Reader_Feed_Rss` 类, 335
- `Zend_Feed_Writer` 类, 318
- `Zend_File_Transfer` 类, 209, 214
- `Zend_Filter` 类, 70, 79
- `Zend_Filter_Input` 类, 124
- `Zend_Form` 类
  - 装饰器, 95, 177
  - 文件上传, 210
  - 表单创建与验证, 51–53
  - 配置文件, 222–224
  - 上下文, 194
  - 日志数据, 261–263
  - 使用 SOAP, 320
  - 视图, 194–196
  - 输入表单, 83
  - 本地化, 275, 294, 299
  - 更新, 150
- `Zend_Form_Decorator_Abstract`, 98
- `Zend_Form_Element`, 56
- `Zend_Form_Element` 类, 365
- `Zend_Form_Element_Button`, 62
- `Zend_Form_Element_Captcha`, 84
- `Zend_Form_Element_Checkbox`, 57–58
- `Zend_Form_Element_File`, 60–61
- `Zend_Form_Element_Hash`, 63
- `Zend_Form_Element_Image`, 62
- `Zend_Form_Element_MultiSelect`, 59
- `Zend_Form_Element_Password`, 55
- `Zend_Form_Element_Radio`, 57–58
- `Zend_Form_Element_Select`, 59
- `Zend_Form_Element_Submit`, 61
- `Zend_Form_Element_Text`, 55
- `Zend_Form_Element_Textarea`, 55
- `Zend_Form_Validator`, 7
- `Zend_Log` 类, 234
- `Zend_Log_Writer_Abstract`, 254
- `Zend_Log_Writer_Doctrine`, 265
- `Zend_Log_Writer_Stream`, 255
- `Zend_Mail` 类, 87
- `Zend_Measure` 类, 285–286, 304
- `Zend_Measure_Number` 类, 295
- `Zend_Navigation` 类, 302–304
- `Zend_Navigation_Page_Mvc` 类, 311
- `Zend_Navigation_Page_Uri` 类, 312
- `Zend_Registry` 类, 314
- `Zend_Rest_Client` 类, 5, 351, 400
- `Zend_Rest_Controller` 类, 355
- `Zend_Rest_Route` 类, 377
- `Zend_Rest_Server` 类, 378
- `Zend_Search_Lucene` 类, 389
- `Zend_Search_Lucene_Field` 类, 390
- `Zend_Search_Lucene_Index` 类, 399
- `Zend_Soap_Client` 类, 401
- `Zend_Soap_Server` 类, 405
- `Zend_Translate` 类, 406
- `Zend_Translate_Adapter_Array` 类, 237–238
- `Zend_Translate_Adapter_Gettext` 类, 302
- `Zend_Uri` 类, 314
- `Zend_View` 类, 325
- `Zend_View_Helper` 类, 326
- `Zend_View_Helper_HeadLink` 类, 327
- `Zend_View_Helper_HeadScript` 类, 328
- `Zend_View_Helper_Navigation` 类, 329
- `Zend_View_Helper_Url` 类, 330
- `Zend_View_Interface` 类, 331
- `Zend_XmlRpc` 类, 332
- `Zend_XmlRpc_Client` 类, 333
- `Zend_XmlRpc_Server` 类, 334
- `Zend_XmlRpc_Value` 类, 335
- `Zend_XmlRpc_Request` 类, 336
- `Zend_XmlRpc_Response` 类, 337
- `Zend_XmlRpc_Fault` 类, 338
- `Zend_XmlRpc_Server_Cache` 类, 339
- `Zend_XmlRpc_Server_Fault` 类, 340
- `Zend_XmlRpc_Server_System` 类, 341
- `Zend_XmlRpc_Value_Array` 类, 342
- `Zend_XmlRpc_Value_Base64` 类, 343
- `Zend_XmlRpc_Value_Boolean` 类, 344
- `Zend_XmlRpc_Value_DateTime` 类, 345
- `Zend_XmlRpc_Value_Double` 类, 346
- `Zend_XmlRpc_Value_Integer` 类, 347
- `Zend_XmlRpc_Value_String` 类, 348
- `Zend_XmlRpc_Value_Struct` 类, 349
- `Zend_XmlRpc_Value_Nil` 类, 350
- `Zend_XmlRpc_Value_Exception` 类, 351
- `Zend_XmlRpc_Client_Http` 类, 352
- `Zend_XmlRpc_Client_ServerProxy` 类, 353
- `Zend_XmlRpc_Client_ServerIntrospection` 类, 354
- `Zend_XmlRpc_Request_Http` 类, 355
- `Zend_XmlRpc_Response_Http` 类, 356
- `Zend_XmlRpc_Server_Exception` 类, 357
- `Zend_XmlRpc_Value_Exception` 类, 358
- `Zend_XmlRpc_Client_Exception` 类, 359
- `Zend_XmlRpc_Server_Exception` 类, 360
- `Zend_XmlRpc_Server_Fault_Exception` 类, 361
- `Zend_XmlRpc_Server_System_Exception` 类, 362
- `Zend_XmlRpc_Value_Collection` 类, 363
- `Zend_XmlRpc_Value_Object` 类, 364
- `Zend_XmlRpc_Value_Scalar` 类, 365
- `Zend_XmlRpc_Value_Array` 类, 366
- `Zend_XmlRpc_Value_Base64` 类, 367
- `Zend_XmlRpc_Value_Boolean` 类, 368
- `Zend_XmlRpc_Value_DateTime` 类, 369
- `Zend_XmlRpc_Value_Double` 类, 370
- `Zend_XmlRpc_Value_Integer` 类, 371
- `Zend_XmlRpc_Value_String` 类, 372
- `Zend_XmlRpc_Value_Struct` 类, 373
- `Zend_XmlRpc_Value_Nil` 类, 374
- `Zend_XmlRpc_Value_Exception` 类, 375
- `Zend_XmlRpc_Client_Http` 类, 376
- `Zend_XmlRpc_Client_ServerProxy` 类, 377
- `Zend_XmlRpc_Client_ServerIntrospection` 类, 378
- `Zend_XmlRpc_Request_Http` 类, 379
- `Zend_XmlRpc_Response_Http` 类, 380
- `Zend_XmlRpc_Server_Exception` 类, 381
- `Zend_XmlRpc_Value_Exception` 类, 382
- `Zend_XmlRpc_Client_Exception` 类, 383
- `Zend_XmlRpc_Server_Exception` 类, 384
- `Zend_XmlRpc_Server_Fault_Exception` 类, 385
- `Zend_XmlRpc_Server_System_Exception` 类, 386
- `Zend_XmlRpc_Value_Collection` 类, 387
- `Zend_XmlRpc_Value_Object` 类, 388
- `Zend_XmlRpc_Value_Scalar` 类, 389
- `Zend_XmlRpc_Value_Array` 类, 390
- `Zend_XmlRpc_Value_Base64` 类, 391
- `Zend_XmlRpc_Value_Boolean` 类, 392
- `Zend_XmlRpc_Value_DateTime` 类, 393
- `Zend_XmlRpc_Value_Double` 类, 394
- `Zend_XmlRpc_Value_Integer` 类, 395
- `Zend_XmlRpc_Value_String` 类, 396
- `Zend_XmlRpc_Value_Struct` 类, 397
- `Zend_XmlRpc_Value_Nil` 类, 398
- `Zend_XmlRpc_Value_Exception` 类, 399
- `Zend_XmlRpc_Client_Http` 类, 400
- `Zend_XmlRpc_Client_ServerProxy` 类, 401
- `Zend_XmlRpc_Client_ServerIntrospection` 类, 402
- `Zend_XmlRpc_Request_Http` 类, 403
- `Zend_XmlRpc_Response_Http` 类, 404
- `Zend_XmlRpc_Server_Exception` 类, 405
- `Zend_XmlRpc_Value_Exception` 类, 406
- `Zend_XmlRpc_Client_Exception` 类, 407
- `Zend_XmlRpc_Server_Exception` 类, 408
- `Zend_XmlRpc_Server_Fault_Exception` 类, 409
- `Zend_XmlRpc_Server_System_Exception` 类, 410
- `Zend_XmlRpc_Value_Collection` 类, 411
- `Zend_XmlRpc_Value_Object` 类, 412
- `Zend_XmlRpc_Value_Scalar` 类, 413
- `Zend_XmlRpc_Value_Array` 类, 414
- `Zend_XmlRpc_Value_Base64` 类, 415
- `Zend_XmlRpc_Value_Boolean` 类, 416
- `Zend_XmlRpc_Value_DateTime` 类, 417
- `Zend_XmlRpc_Value_Double` 类, 418
- `Zend_XmlRpc_Value_Integer` 类, 419
- `Zend_XmlRpc_Value_String` 类, 420
- `Zend_XmlRpc_Value_Struct` 类, 421
- `Zend_XmlRpc_Value_Nil` 类, 422
- `Zend_XmlRpc_Value_Exception` 类, 423
- `Zend_XmlRpc_Client_Http` 类, 424
- `Zend_XmlRpc_Client_ServerProxy` 类, 425
- `Zend_XmlRpc_Client_ServerIntrospection` 类, 426
- `Zend_XmlRpc_Request_Http` 类, 427
- `Zend_XmlRpc_Response_Http` 类, 428
- `Zend_XmlRpc_Server_Exception` 类, 429
- `Zend_XmlRpc_Value_Exception` 类, 430
- `Zend_XmlRpc_Client_Exception` 类, 431
- `Zend_XmlRpc_Server_Exception` 类, 432
- `Zend_XmlRpc_Server_Fault_Exception` 类, 433
- `Zend_XmlRpc_Server_System_Exception` 类, 434
- `Zend_XmlRpc_Value_Collection` 类, 435
- `Zend_XmlRpc_Value_Object` 类, 436
- `Zend_XmlRpc_Value_Scalar` 类, 437
- `Zend_XmlRpc_Value_Array` 类, 438
- `Zend_XmlRpc_Value_Base64` 类, 439
- `Zend_XmlRpc_Value_Boolean` 类, 440
- `Zend_XmlRpc_Value_DateTime` 类, 441
- `Zend_XmlRpc_Value_Double` 类, 442
- `Zend_XmlRpc_Value_Integer` 类, 443
- `Zend_XmlRpc_Value_String` 类, 444
- `Zend_XmlRpc_Value_Struct` 类, 445
- `Zend_XmlRpc_Value_Nil` 类, 446
- `Zend_XmlRpc_Value_Exception` 类, 447
- `Zend_XmlRpc_Client_Http` 类, 448
- `Zend_XmlRpc_Client_ServerProxy` 类, 449
- `Zend_XmlRpc_Client_ServerIntrospection` 类, 450
- `Zend_XmlRpc_Request_Http` 类, 451
- `Zend_XmlRpc_Response_Http` 类, 452
- `Zend_XmlRpc_Server_Exception` 类, 453
- `Zend_XmlRpc_Value_Exception` 类, 454
- `Zend_XmlRpc_Client_Exception` 类, 455
- `Zend_XmlRpc_Server_Exception` 类, 456
- `Zend_XmlRpc_Server_Fault_Exception` 类, 457
- `Zend_XmlRpc_Server_System_Exception` 类, 458
- `Zend_XmlRpc_Value_Collection` 类, 459
- `Zend_XmlRpc_Value_Object` 类, 460
- `Zend_XmlRpc_Value_Scalar` 类, 461
- `Zend_XmlRpc_Value_Array` 类, 462
- `Zend_XmlRpc_Value_Base64` 类, 463
