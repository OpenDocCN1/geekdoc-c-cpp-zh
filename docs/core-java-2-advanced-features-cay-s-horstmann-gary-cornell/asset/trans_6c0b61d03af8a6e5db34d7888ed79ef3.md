

## 代码清单 4.8 *（续）*

```java
List<String> lines = Files.readAllLines(Paths.get(args[0]), Charset.forName("UTF-8"));

String from = lines.get(0);
String to = lines.get(1);
String subject = lines.get(2);

StringBuilder builder = new StringBuilder();
for (int i = 3; i < lines.size(); i++)
{
    builder.append(lines.get(i));
    builder.append("\n");
}

Console console = System.console();
String password = new String(console.readPassword("Password: "));

Session mailSession = Session.getDefaultInstance(props);
// mailSession.setDebug(true);
MimeMessage message = new MimeMessage(mailSession);
message.setFrom(new InternetAddress(from));
message.addRecipient(RecipientType.TO, new InternetAddress(to));
message.setSubject(subject);
message.setText(builder.toString());
Transport tr = mailSession.getTransport();
try
{
    tr.connect(null, password);
    tr.sendMessage(message, message.getAllRecipients());
}
finally
{
    tr.close();
}
}
```

本章中，你已经了解了如何用 Java 编写网络客户端和服务器，以及如何从 Web 服务器传递信息。下一章将介绍数据库连接。你将学习如何使用 JDBC API 在 Java 中操作关系数据库。

## 第 5 章：数据库编程

**本章内容**

- 5.1 JDBC 的设计，第 282 页
- 5.2 结构化查询语言，第 285 页
- 5.3 JDBC 配置，第 291 页
- 5.4 使用 JDBC 语句，第 297 页
- 5.5 查询执行，第 309 页
- 5.6 可滚动和可更新的结果集，第 321 页
- 5.7 行集，第 328 页
- 5.8 元数据，第 333 页
- 5.9 事务，第 344 页
- 5.10 高级 SQL 类型，第 347 页
- 5.11 Web 与企业应用中的连接管理，第 349 页

1996 年，Sun 发布了 JDBC API 的第一个版本。该 API 让程序员可以连接到数据库，并使用结构化查询语言（SQL）查询或更新数据库。（SQL 通常读作“sequel”，是关系数据库访问的行业标准。）此后，JDBC 成为 Java 库中最常用的 API 之一。

JDBC 已经过多次更新。作为 1998 年 Java SE 1.2 发布的一部分，JDBC 的第二版发布。JDBC 3 随 Java SE 1.4 和 5.0 提供。在本书出版时，随 Java SE 8 提供的 JDBC 4.2 是当前最新版本。

在本章中，我们将解释 JDBC 背后的关键思想。我们将向你介绍（或帮你回顾）SQL，即关系数据库的行业标准结构化查询语言。然后，我们将提供足够的细节和示例，让你开始在常见编程场景中使用 JDBC。

> **注意：** 根据 Oracle 的说法，JDBC 是一个商标术语，而不是 Java Database Connectivity 的首字母缩写。之所以这样命名，是为了让人联想到 ODBC——一种由 Microsoft 率先提出的标准数据库 API，后来被纳入 SQL 标准。

### 5.1 JDBC 的设计

从一开始，Java 技术的开发者就意识到 Java 在处理数据库方面展现出的潜力。1995 年，他们开始着手扩展标准 Java 库，以处理对数据库的 SQL 访问。他们最初希望做的是扩展 Java，使程序只使用“纯”Java 就能与任意数据库通信。他们很快就意识到这是一项不可能完成的任务：现有的数据库太多，使用的协议也太多。此外，尽管数据库厂商都赞成 Java 提供用于数据库访问的标准网络协议，但他们只有在 Java 使用其网络协议时才赞成。

所有数据库厂商和工具厂商确实都同意的是：Java 提供用于 SQL 访问的纯 Java API，并提供一个驱动程序管理器来允许第三方驱动程序连接到特定数据库，这将是有用的。数据库厂商可以提供自己的驱动程序，插入到驱动程序管理器中。这样一来，就会有一种简单的机制来向驱动程序管理器注册第三方驱动程序。

这种组织方式遵循了 Microsoft ODBC 非常成功的模型，该模型提供了用于数据库访问的 C 编程语言接口。JDBC 和 ODBC 都基于相同的理念：按照该 API 编写的程序与驱动程序管理器通信，而驱动程序管理器又使用驱动程序与实际数据库通信。

这意味着，大多数程序员只需要与 JDBC API 打交道。

#### 5.1.1 JDBC 驱动类型

JDBC 规范将驱动程序分为以下类型：

- 一个 *第 1 类驱动程序* 将 JDBC 转换为 ODBC，并依赖 ODBC 驱动程序与数据库通信。Java 的早期版本包含一个这样的驱动程序，即 *JDBC/ODBC 桥接器*。然而，该桥接器需要部署并正确配置 ODBC 驱动程序。JDBC 最初发布时，该桥接器便于测试，但它从未打算用于生产环境。如今已有许多更好的驱动程序可用，并且 Java 8 不再提供 JDBC/ODBC 桥接器。
- 一个 *第 2 类驱动程序* 部分用 Java 编写，部分用本机代码编写；它与数据库的客户端 API 通信。使用此类驱动程序时，除了 Java 库之外，还必须在客户端上安装一些平台特定的代码。
- 一个 *第 3 类驱动程序* 是一个纯 Java 客户端库，它使用与数据库无关的协议将数据库请求传送到服务器组件，然后由服务器组件将这些请求转换为特定于数据库的协议。这简化了部署，因为平台特定的代码只位于服务器上。
- 一个 *第 4 类驱动程序* 是一个纯 Java 库，它将 JDBC 请求直接转换为特定于数据库的协议。

> **注意：** JDBC 规范可从 http://download.oracle.com/otndocs/jcp/jdbc-4_2-mr2-spec/ 获取。

大多数数据库厂商随其数据库提供第 3 类或第 4 类驱动程序。此外，许多第三方公司专门生产这样的驱动程序：它们具有更好的标准符合性、对更多平台的支持、更好的性能，或者在某些情况下，比数据库厂商提供的驱动程序更可靠。

总之，JDBC 的最终目标是使以下成为可能：

- 程序员可以用 Java 编程语言编写应用程序，使用标准 SQL 语句（甚至 SQL 的专用扩展）访问任何数据库，同时仍遵循 Java 语言约定。
- 数据库厂商和数据库工具厂商可以提供低级驱动程序。因此，他们可以针对自己的特定产品优化驱动程序。

> **注意：** 如果你想知道为什么 Java 没有直接采用 ODBC 模型，那么 1996 年 JavaOne 大会上给出的原因是：
>
> - ODBC 难以学习。
> - ODBC 只有少量命令，却带有大量复杂选项。Java 编程语言中更可取的做法是拥有简单直观的方法，但方法数量要多。
> - ODBC 依赖于使用 `void*` 指针以及其他在 Java 编程语言中不自然的 C 特性。
> - 与纯 Java 解决方案相比，基于 ODBC 的解决方案本质上更不安全，也更难部署。

#### 5.1.2 JDBC 的典型用途

传统的客户端/服务器模型在客户端有丰富的 GUI，在服务器上有数据库（见图 5.1）。在这种模型中，JDBC 驱动程序部署在客户端上。

![](img/7dd923a566750151a3aab0dacd0cdaa5_304_0.png)

**图 5.1** 传统的客户端/服务器应用程序

然而，如今更常见的是三层模型，其中客户端应用程序不进行数据库调用。相反，它调用服务器上的中间件层，再由中间件层进行数据库查询。三层模型有几个优点。它将*视觉呈现*（在客户端）与业务逻辑（在中间层）和原始数据（在数据库中）分离。因此，可以从多个客户端（如 Java 桌面应用程序、Web 浏览器或移动应用）访问相同的数据和相同的业务规则。客户端与中间层之间的通信通常通过 HTTP 进行。JDBC 管理中间层与后端数据库之间的通信。图 5.2 显示了基本架构。

![](img/7dd923a566750151a3aab0dacd0cdaa5_305_0.png)

**图 5.2** 三层应用程序

### 5.2 结构化查询语言

JDBC 让你使用 SQL 与数据库通信，SQL 基本上是所有现代关系数据库的命令语言。桌面数据库通常有一个 GUI，允许用户直接操作数据，而基于服务器的数据库则完全通过 SQL 访问。

JDBC 包可以被看作只不过是一个用于将 SQL 语句传递给数据库的 API。我们将在本节简要介绍 SQL。如果你以前从未见过 SQL，可能会觉得这些材料不够。如果是这样，可以查阅关于该主题的众多学习资源之一；我们推荐 Alan Beaulieu 的 *学习 SQL*（O’Reilly，2009 年），或在线书籍 *艰难学习 SQL*，网址为 http://sql.learncodethehardway.org/。

你可以把数据库看作一组具有行和列的命名表。每一列都有一个*列名*。每一行包含一组相关数据。

作为本书的示例数据库，我们使用一组数据库表，这些表描述了一组经典计算机科学书籍（见表 5.1 至 5.4）。

