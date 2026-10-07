
使用 C# 的 SQL Server 数据库编程

## II. 单选题

7. 可以在表之间创建外键
a. 在创建任何表之前
b. 在创建某些表时
c. 在创建所有表之后
d. 无需限制

8. 为了在表之间创建外键，首先必须选择包含该键的表，然后选择另一个具有 ____ 的表
a. 主键，外键
b. 主键，主键
c. 外键，外键
d. 外键，外键

9. SQL 数据库中的数据类型 varchar(50) 是一种长度为 ____ 的字符串
a. 长度限制为 50
b. 固定长度为 50
c. 特定数量的字母
d. 可变长度

10. 对于 SQL Server 中的数据表，空白值必须被 ____。
a. 用 NULL 索引
b. 留为空白
c. 由 NULL 或空白表示
d. 由 NULL 标识

## III. 练习题

1. 与集成数据库方法相比，使用文件处理方法的优势是什么？
2. 定义实体完整性和引用完整性。描述执行这些规则的理由。
3. 实体可以有三种关系：一对一、一对多和多对多。绘制 ER 图来说明每种关系。
4. 列出在 SQL Server Management Studio 中为 SQL Server 2019 数据库创建数据表外键的所有步骤。使用真实示例说明这些步骤。
5. 列出在 SQL Server Management Studio 中为 SQL Server 2019 数据库创建数据表外键的所有步骤。使用真实示例说明这些步骤。

![](img/d59a47501d0a20fc046a49c6fb70.png)

# 3 ADO 简介

对于开发者来说，实现复杂的数据处理技术以增强数据操作是一段漫长的。。访问的演变是一个漫长的过程，主要关注如何以更灵活的方式处理关系数据。该方法一直关注基于微软的 API，例如 ODBC、OLEDB、数据访问对象 (DAO) 和远程数据对象 (RDO)，此外还有许多非微软的 API。这些 API 无法跨越多种语言建立面向对象和半结构化 (XML) 数据之间的鸿沟，且具有挑战性，同时也为完整架构提供了机会。ADO.NET 被认为是关系数据库 API 的良好解决方案，它是随 Visual Studio 2005 引入的。ADO.NET 的最新版本是 4.0，它随着 .NET Framework 4.0 和 Visual Studio 发布。在本章中，我们将对 ADO.NET 的历史进行详细回顾，然后充分讨论 ADO.NET 的组件和架构。最后我们将介绍一些新功能和组件。

## 3.1 ADO 和 ADO.NET

ActiveX 数据对象 (ADO) 基于对象链接与嵌入 (OLE) 和组件对象模型 (COM) 技术开发。开发者使用 COM 创建可重用的软件组件、链接应用程序并利用 Windows 服务。在过去的几十年里，ADO 一直是 Visual Basic 程序员访问各种数据源的首选接口。数据访问方法的发展可以溯到 20 世纪 90 年代中期的数据访问对象 (DAO)；随后是基于开放数据库连接 (ODBC) 的远程数据对象 (RDO)。20 世纪 90 年代后期出现了基于 OLEDB 的 ADO 开发。ADO.NET 是 ADO 的最新版本，主要基于 .NET Framework 4.0。通用语言运行时 (CLR) 与 COM 提供双向的透明集成。这意味着 ADO.NET 应用程序和组件可以使用每个系统的功能。然而，ADO.NET 为开发者提供了许多益处，包括更健壮的安全模型、自动内存管理、原生支持和集成查询 (LINQ)。对于新开发，由于其强大的运行时环境，强烈推荐将 ADO.NET 作为首选技术。本章将对 ADO.NET 及其组件进行详细介绍，这些组件将在全书的剩余部分中使用。

在本章中，你将：

- 学习 ADO.NET 中的基本类及其架构
- 学习不同的 ADO.NET 数据提供程序
- 学习 Connection（连接）和 Command（命令）组件
- 学习 Parameters（参数）集合
- 学习 DataAdapter 和 DataReader（数据读取器）组件
- 学习 DataSet 和 DataTable 组件
- 学习 ADO.NET 实体框架 (EF)
- 学习 ADO.NET 实体框架工具 (EFT)
- 学习 ADO.NET 实体数据模型 (EDM)

首先，让我们仔细观察 ADO.NET 并对它的组件有一个全局概念。

## 3.2 ADO.NET 概述

ADO.NET 是一组向微软 .NET 编程暴露访问服务的类。ADO.NET 提供了一系列丰富的组件，用于创建分布式、数据共享应用程序。它是 .NET 框架不可或缺的一部分，提供了对关系、XML 和应用程序数据的访问。ADO.NET 支持多种开发需求，包括通过应用程序、工具、语言或 Internet 浏览器创建前端数据库类和中间层业务对象。

所有 ADO.NET 类都位于 System.Data 命名空间，并引用 System.Data 和 System.Xml。

基本上，ADO.NET 提供了一类类支持你开发数据库应用程序，并允许你连接数据源以检索、处理和更新数据。ADO.NET 提供的类是开发专业数据驱动应用程序的核心，可以分为三个主要组件：

- Data Provider
- DataSet
- DataTable

这三个组件位于不同的命名空间。DataSet 和 DataTable 类根据数据提供程序的类型位于不同的命名空间。

数据提供程序包含四个类：Connection、Command、DataAdapter 和 DataReader。这四个类用于执行不同的功能，帮助你：

1) 使用 Connection 对象建立你的项目与数据源之间的连接
2) 使用 Command 对象执行数据查询以检索、处理和更新数据
3) 使用 DataAdapter 对象在你的 DataSet 和数据库之间移动数据
4) 使用 DataReader 对象从数据库执行数据查询（只读）

DataSet 类被视为一个表并可以包含多个表。这些数据表只是数据库中真实数据的映射。但这些表也可以在不连接的情况下单独使用。在这种情况下，每个数据表都可以被视为 DataTable 对象。

DataSet 和 DataTable 类与 Data Provider 类没有直接关系；因此它们通常被称为数据提供程序无关组件。四个类，Connection,
