

## 对象服务的类

对象服务的概念由 System.Data.Objects 和 System.Data.Objects.DataClasses 命名空间中的类实现。以下是与对象服务一起使用的一些类：

ObjectContext 类 – 表示用于与数据交互的主要类，该数据以 EDM 中定义的实体类型的实例对象的形式存在。ObjectContext 类封装了 .NET Framework 与数据库之间的连接。此类充当 CREATE、UPDATE 和 DELETE 操作的网关。ObjectContext 类的实例封装了以下内容：

- 一个 EntityConnection 对象，指定到数据库的连接
- 一个 MetadataWorkspace 对象，描述模型
- 一个 ObjectStateManager 对象，管理缓存中存在的对象

ObjectContext 类使用 System.Data.Objects 命名空间和 System.Data.Entity 程序集（在 system.data.entity.dll 中）来以对象形式处理实体数据。System.Data.Objects.ObjectContext 类的继承层次结构如下：

```
System.Object
System.Data.Objects.ObjectContext
```

声明 ObjectContext 类的语法如下：

```
public class ObjectContext : IDisposable
```

EntityConnection 类 – 表示到底层数据存储的连接。此类不能被继承。你需要使用 System.Data.EntityClient 命名空间和 System.Data.Entity 程序集（在 system.data.entity.dll 中）来使用此类。System.Data.EntityClient.EntityConnection 类的继承层次结构如下：

```
System.Object
System.MarshalByRefObject
System.ComponentModel.Component
System.Data.Common.DbConnection
System.Data.EntityClient.EntityConnection
```

声明 EntityConnection 类的语法如下：

```
public sealed class EntityConnection : DbConnection
```

MetadataWorkspace 类 – 表示 ADO.NET 元数据运行时服务组件，提供从各种源检索元数据的支持。你需要使用 System.Data.Metadata.Edm 命名空间和 System.Data.Entity 程序集（在 system.data.entity.dll 中）来使用此类。System.Data.Metadata.Edm.MetadataWorkspace 类的继承层次结构如下：

```
System.Object
System.Data.Metadata.Edm.MetadataWorkspace
```

## 对象服务的特性

对象服务为 Entity Framework 中的编程提供以下特性：

- **以对象形式查询数据** – 允许你使用 LINQ、Entity SQL 或查询生成器方法执行针对 EDM 的查询并以对象形式返回数据。Entity Framework 包含 ObjectQuery 泛型类。它表示返回零个或多个类型化实体的集合的查询。它始终与提供连接和元数据信息的现有对象上下文相关。
- **塑造查询结果** – 仅返回查询中明确请求的对象。我们可以指定查询是否返回相关对象，以防对象之间存在关系。
- **添加、更改和删除对象** – 在内存中保存数据对象，并使我们能够在对象上下文中添加、修改和删除对象。
- **将更改保存到持久化数据存储** – 缓存对象上下文中的更改。当我们显式调用服务时，更改会存储回数据存储。
- **将对象绑定到控件** – 启用将对象绑定到控件。这些控件必须支持数据绑定，例如 DataGridView 控件。
- **管理并发** – 当一个或多个属性的 ConcurrencyMode 属性设置为 fixed 时跟踪并发。当在应用程序中检测到并发冲突时，对象服务会引发特定异常。
- **附加和分离对象** – 指 ObjectContext 实例应在其应用程序执行期间持久存在。例如，只要应用程序执行，对象就应保持绑定到 Form 控件。对象可以被分离以释放不再需要的资源。它有助于增加对象的上下文大小。
- **序列化对象** – 支持 XML 序列化和二进制序列化。XML 序列化将对象的公共字段和属性值序列化为 XML 流，而二进制序列化在使用 ViewState 属性在 ASP.NET 应用程序中持久化对象时尤其有用。
- **管理对象标识和跟踪更改** – 使用标识值来帮助跟踪对象的更改、处理冲突并决定何时从数据存储检索数据。
- **管理连接** – 为对象上下文提供我们自己的连接，我们也可以显式管理对象使用的连接。
- **管理事务** – 支持 .NET Framework 事务以协调对数据存储的操作并注册分布式事务。它还支持事务的自动注册。
- **使用 EDM 的自定义对象** – 使你能够手动定义自己的对象或使用现有对象与 EDM。

让我们现在在下一节学习 Entity SQL 语言。

## 理解 Entity SQL 语言

Entity SQL 是一种类似于 SQL 的语言，由 ADO.NET Entity Framework 提供以支持 EDM。Entity SQL 支持 EDM 构造，使用户能够查询实体模型表示的数据。对象服务和 EntityClient 提供程序有助于返回数据，包括标量结果、结果集和对象图。对象服务和 EntityClient 提供程序都使我们能够使用 Entity SQL 对 EDM 执行查询并以强类型 CLR 对象的形式返回数据，这些对象是实体类型的实例。要创建 EntityCommand 对象，我们可以指定存储过程名称或通过将 Entity SQL 查询字符串分配给其 System.Data.EntityClient.EntityCommand.CommandText 属性来指定查询文本。现在，让我们详细讨论 Entity SQL 的特性。

## Entity SQL 的特性

由于电子商务网站的日益普及，业务应用程序在处理数据库时需要更具交互性。ADO.NET Entity Framework 提供的 Entity SQL 在此上下文中解决了开发人员遇到的许多问题，例如性能和处理数据库的便捷性。Entity SQL 的一些特性如下：

继承和关系支持—指定 Entity SQL 中的 OfType 运算符提供了从超类型实例集合中选择子类型实例的能力。Entity SQL 支持 EDM 功能，例如继承和关系。

子查询的统一处理—指定在传统 SQL 中，FROM 子句中的子查询被视为多集，但在 SELECT 子句中使用的相同子查询被视为标量子查询。在 IN 运算符左侧使用的子查询被视为标量子查询，而在右侧使用的子查询则预期为多集子查询。Entity SQL 将所有子查询都视为多集子查询，并提供 anyelement 运算符，该运算符对集合（如数组）进行操作。

左相关和别名—指定 Entity SQL 在 FROM 子句中概括左相关并统一处理它们。在使用 FROM 子句的 Entity SQL 表达式中，我们可以在同一子句中引用定义而无需额外语法。Entity SQL 还对涉及 group by 子句的查询施加了额外限制。我们可以在 Transact-SQL 中使用以下代码，但在 Entity SQL 中无效：

```
select z.a + z.b from Z as z group by z.a + z.b
```

要通过 Entity SQL 执行相同的查询，使用以下语法：

```
select k from Z as z group by (z.a + z.b) as k
```

此类查询的 SELECT 子句和 HAVING 子句中包含的表达式只能通过别名引用 GROUP BY 键。

引用表的列—指定在 Entity SQL 中，所有列引用必须使用表别名限定。以下语法在 Transact-SQL 中有效，但在 Entity-SQL 中无效：

```
select x from Z
```

在前面的表达式中，我们假设 x 是表 Z 的有效列。

使用 Entity SQL 编写相同查询的语法如下：

```
select Z.x as X from Z as z
```

FROM 子句中的表别名是可选的。表名可用作隐式别名。查询中的未限定引用可能导致某些错误；因此，在模式演进期间应谨慎处理。

表达式支持—指定为了更好地支持集合和嵌套集合，Entity SQL 将代码的每一行视为表达式。以下语法在 Transact-SQL 中有效，但在 Entity-SQL 中无效：

```
sal > all (select salary from employees)
sal > any (select salary from employees)
```

等效表达式可以在 Entity SQL 中写为如下：

```
not exists(select 0 from employees as emp where salary > e.salaries)
exists(select 0 from employees as emp where salary > e.salaries)
```

以下是有效的 Entity SQL 查询：

```
1+2 *3
"abc"
row(1 as a, 2 as b)
{ 1, 3, 5 }
e1 union all e2
set(e1)
```

通过对象导航—指定 Entity SQL 使用特定符号来支持通过对象的属性导航。假设 emp 是 employee 类型的表达式，那么以下是对名为 employee 的表中城市地址的 Entity SQL 语法。

```
emp.Address.City
```

基于集合的聚合—指定 Entity SQL 支持两种类型的聚合，即 SQL 风格聚合和基于集合的聚合。SQL 风格聚合的语法如下：

```
select x, sum(z.y) from Z as z group by z.x as x
```

