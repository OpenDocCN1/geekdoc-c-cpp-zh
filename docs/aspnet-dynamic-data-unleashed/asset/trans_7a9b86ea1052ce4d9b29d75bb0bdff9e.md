
## 第 5 章

## 筛选模板

### 本章内容

- 使用 LINQ 进行筛选
- 创建筛选模板
- 动态 LINQ 查询
- 使用筛选模板构建搜索页面
- 筛选模板查找规则
- 内置筛选模板

搜索功能对于大多数数据库应用程序至关重要。无论是客户浏览产品目录，还是服务代表查询客户记录，用户都需要一种快速便捷的机制来查找所需信息。十多年来，ASP.NET 开发人员一直使用存储过程来实现一般的数据访问代码，特别是搜索功能。对于每个搜索屏幕，例如图 5.1 所示的客户搜索页面，都会创建一个或多个存储过程，每个存储过程接受多个表示搜索条件的参数并执行适当的 SELECT 语句。

尽管使用存储过程实现简单页面很容易，但随着搜索条件中额外参数数量的增加，复杂性会呈指数级增长。考虑图 5.1 所示的客户搜索页面。仅有 2 个搜索参数 City 和 Title，该搜索页面需要支持其值的 3 种不同组合——仅 City、仅 Title，以及 City 和 Title 均有。这需要在存储过程体中使用 IF 语句的形式，或在 SELECT 语句的 WHERE 子句中使用逻辑条件的形式放置条件逻辑，以处理这 3 种组合。使用 3 个搜索参数时，组合数跃升至 7；使用 4 个参数时，已达到 15；仅使用 5 个参数（对于典型应用程序中的高级搜索页面来说是一个非常适中的数字），可能的组合数就高达令人望而生畏的 31 种。

参数值的可能组合数之所以重要，有两个原因。一方面，它直接影响开发人员必须处理的数据库代码的复杂性

如果用户输入了 Title 的搜索字符串，则会调用第二个 Where 方法，SQL 查询如下所示：

```
select * from Customers where ContactTitle = @Title
```

只有当用户同时输入了 City 和 Title 搜索字符串时，才会调用两个 Where 方法，SQL 查询将包含两个列的条件：

```
select * from Customers where City = @City and ContactTitle = @Title
```

换句话说，在 LINQ 的帮助下，您可以构建仅包含用户提供的搜索值所需条件的聚焦查询。这有助于数据库服务器选择比典型的手工编写 SQL（如下所示）更高效的执行计划，后者试图处理两种搜索选项，通常需要数据库服务器执行全表扫描：

```
select * from Customers
where City = ISNULL(@City, City)
  and ContactTitle = ISNULL(@Title, ContactTitle)
```

### 创建筛选模板

筛选模板是一个用户控件，封装了实现单个列查询筛选所需的表示层和数据访问逻辑。在传统的搜索页面中，此逻辑通常分散在标记和代码隐藏文件中。考虑我们客户搜索页面中 City 列所需的筛选逻辑（请参阅清单 5.1 中的标记）。

**清单 5.1** 简单搜索页面（标记）

```
<%@ Page Title="" Language="C#"
    MasterPageFile="~/Site.master" CodeBehind="SamplePage.aspx.cs"
    Inherits="WebApplication.Samples.Ch05.LinqFilter.SamplePage" %>

<asp:Content ContentPlaceHolderID="main" runat="server">
    Customer City: <asp:TextBox runat="server" ID="cityFilter" />
    Title: <asp:TextBox runat="server" ID="titleFilter" />
    <asp:Button runat="server" Text="Find" OnClick="Find_Click" />
    <asp:GridView ID="gridView" runat="server" />
</asp:Content>
```

传统页面包含一个 TextBox 控件，用户可以在其中输入要在 City 列中搜索的值。基于此值筛选行的數據访问逻辑是清单 5.2 中所示的 Find_Click 事件处理程序的一部分。

## 实时数据大规模处理的分布式系统架构

现代数据密集型应用程序要求在保持容错性和水平可扩展性的同时，对高速数据流进行低延迟处理。传统的批处理架构已被证明不足以满足诸如欺诈检测、物联网遥测和推荐引擎等用例的需求，这些用例需要每秒持续摄取和分析数百万个事件。

### 1. 引言

本文探讨了一种分层架构，将摄取、处理、存储和服务解耦。摄取层充当持久缓冲区，吸收突发流量并按需重放数据。处理引擎以精确一次语义运行分布式计算，而服务层为应用程序和仪表板提供对有状态视图的索引访问。

- **关键设计目标：**
  - 低延迟（p99 < 100 ms）
  - 精确一次状态语义
  - 跨通用硬件的弹性分区
  - 自动故障转移和再平衡

### 2. 相关工作

> "根本挑战不是处理速度，而是跨分区的协调状态管理。"
> — M. Chen, 2023

Apache Flink、Kafka Streams 和 Spark Streaming 等现有框架在延迟、吞吐量和状态一致性之间采用了不同的权衡。我们的工作在这些基础上扩展，采用统一的基于日志的存储模型和自适应分区策略。

### 3. 系统概述

![](img/11b373b78859e17d318fd76939a0df9d_159_0.png)

您可以使用内置或第三方 ASP.NET 控件来实现适合输入模板设计处理的数据类型搜索值的用户界面。此模板专为 String 列设计。它使用与前面示例搜索页面中使用的类似的 TextBox 控件。OnTextChanged 事件处理程序用于在用户更改搜索值时刷新查询结果。

**清单 5.4** 文本筛选模板（代码隐藏）

```
using System;
using System.Linq;
using System.Linq.Dynamic;
using System.Web.DynamicData;
using System.Web.UI;

namespace WebApplication.DynamicData.Filters
{
    public partial class TextFilter : QueryableFilterUserControl
    {
        public override IQueryable GetQueryable(IQueryable query)
        {
            if (!string.IsNullOrEmpty(this.textBox.Text))
            {
                string filter = this.Column.Name + " == @0";
                query = query.Where (filter, this.textBox.Text);
            }

            return query;
        }

        protected override void OnInit(EventArgs e)
        {
            base.OnInit(e);
            this.textBox.MaxLength = this.Column.MaxLength;
            this.textBox.Text = this.DefaultValue;
        }

        protected void TextBox_TextChanged(object sender, EventArgs e)
        {
            this.OnFilterChanged();
        }
    }
}
```

筛选模板继承自 Dynamic Data 提供的特殊基类 `QueryableFilterUserControl`。该类定义了子类需要重写的多个虚方法和属性，并提供了多个帮助方法，旨在帮助实现具体的筛选模板。

### GetQueryable 方法

GetQueryable 方法是筛选模板的核心。它在 `QueryableFilterUserControl` 基类中定义为抽象方法，所有筛选模板都必须重写它以实现数据访问逻辑。此方法接收一个查询对象，即 `IQueryable` 的实例，它需要根据用户输入的搜索值对其进行修改。如果用户未为此特定列输入任何搜索条件，则 GetQueryable 方法应返回原始查询。请注意，清单 5.4 中的代码如何检查 TextBox 控件的内容，并且仅在不为空时才修改查询。

### OnFilterChanged 方法

QueryableFilterUserControl 基类的 OnFilterChanged 方法会通知负责执行查询并从数据库获取行的数据源控件，查询可能已更改。基类在响应 OnFilterChanged 时调用 GetQueryable 方法。

在此示例中，OnFilterChanged 方法由 TextBox_TextChanged 方法调用，后者处理 TextBox 控件的 OnTextChanged 事件。这确保了在回发期间检测到文本框中输入的搜索值的任何更改，并调用 GetQueryable 方法以应用筛选器。

### DefaultValue 属性

DefaultValue 属性提供初始筛选值。当作为清单页面模板的一部分实例化时，该模板在第 6 章“页面模板”中讨论，筛选器可以通过页面请求 URL 传递列名和值来进行初始化。虽然对于新的筛选模板不是必需的，但支持此功能对于使它们的行为与 Dynamic Data 项目模板提供的内置模板保持一致非常重要。

### 动态 LINQ 查询

大多数筛选模板，例如本示例中的 Text.ascx，可以重用于任何匹配类型的列。动态筛选模板，例如此模板，不能在查询中硬编码列名。相反，使用通过 QueryableFilterUserControl 基类的 Column 属性可用的列元数据来获取列名并动态构建查询：
