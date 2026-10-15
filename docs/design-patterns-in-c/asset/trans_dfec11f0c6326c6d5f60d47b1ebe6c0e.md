

## 摘要

在本章中，我们通过内置的 ADO.NET `DbProviderFactory` 类了解了抽象工厂模式的使用。在下一章工厂方法模式中，将使用上述讨论的代码。因此，本章不附带任何源代码。

## 12. 工厂方法模式

在上一章中，你可能已经了解了抽象工厂。它涉及对具有相关对象的类进行抽象。在本章中，我们将讨论工厂方法模式。我使用相同的 ADO.NET Provider Factory 类作为示例。让我们看看挑战并逐步演化出解决方案。

## 挑战

你正在开发一个 Windows 应用程序。根据他们拥有的数据库许可证，该应用程序有 2 类用户：Sql Server 或 Oracle。

因此，对于每个数据库操作，你需要根据枚举 `DatabaseType` 创建正确的数据库类。

```
public void InsertRecord()
{
    if (AppContext.DatabaseType == DatabaseType.SqlServer)
    {
        SqlConnection connection = new SqlConnection();
        SqlCommand command = new SqlCommand();

        command.Connection = connection;
        command.ExecuteNonQuery();
    }
    else if (AppContext.DatabaseType == DatabaseType.Oracle)
    {
        OracleConnection connection = new OracleConnection();
        OracleCommand command = new OracleCommand();

        command.Connection = connection;
        command.ExecuteNonQuery();
    }
}
```

上述代码看起来复杂，并且在整个应用程序中，每个数据库操作都需要重复编写。

如何避免重复代码并让事情变得更好？

## 定义

GoF 定义：“定义一个用于创建对象的接口，但让子类决定实例化哪个类。工厂方法让类将实例化推迟到子类。”

## 实现

上述问题可以使用工厂方法模式解决。这里我们提供一个抽象类来定义结构并关联所有相关对象（使用抽象工厂）。然后创建派生自该抽象类的子类。子类决定要实例化哪些类。

优点是质量更高、代码更少。这里我们必须定义一个名为 `DbProviderFactory` 的抽象类。（ADO.NET 已经包含它）

```
public abstract class DbProviderFactory
{
    public virtual DbCommand CreateCommand();
    public virtual DbCommandBuilder CreateCommandBuilder();
    public virtual DbConnection CreateConnection();
    public virtual DbDataAdapter CreateDataAdapter();
    public virtual DbParameter CreateParameter();
}
```

然后，我们可以从上述抽象类派生出具体类。

```
public class SqlClientFactory : DbProviderFactory
{
    public override DbConnection CreateConnection()
    {
        return new SqlConnection();
    }

    public override DbCommand CreateCommand()
    {
        return new SqlCommand();
    }
}
```

从上述代码中你可以看到，`SqlConnection()` 和 `SqlCommand()` 对象被创建并分别提供给 `DbConnection` 和 `DbCommand` 类型。这里 `DbConnection` 和 `DbCommand` 是其他抽象类。

类似地，Oracle 实现如下：

```
public class OracleClientFactory : DbProviderFactory
{
    public override DbConnection CreateConnection()
    {
        return new OracleConnection();
    }

    public override DbCommand CreateCommand()
    {
        return new OracleCommand();
    }
}
```

## 替换原始代码

现在我们准备用工厂方法类替换 `Insert()` 方法代码。这里我们使用 `AppInit()` 代码来创建将在整个应用程序中使用的工厂。

```
public void AppInit()
{
    if (AppContext.DatabaseType == DatabaseType.SqlServer)
        AppContext.DbProviderFactory = SqlClientFactory.Instance;
```

```
else if (AppContext.DatabaseType == DatabaseType.Oracle)
    AppContext.DbProviderFactory = OracleClientFactory.Instance;
}

// NewInsertRecord method
private void NewInsertRecord()
{
    DbConnection connection = AppContext.DbProviderFactory.CreateConnection();
    DbCommand command = AppContext.DbProviderFactory.CreateCommand();

    command.Connection = connection;
    command.ExecuteNonQuery();
}
```

从上述代码中你可以看到，使用工厂方法后代码量显著减少，但代价是新增了一些类。该模式为添加新数据库提供了很大的灵活性。（如果再来一位使用 PostgreSQL 的客户 ☺）

## 抽象与具体派生

下图描述了我们讨论的抽象类与具体类之间的关系。

![](img/10a39e9a5b1ae55cb003d638eba7aaa0_51_0.png)

![](img/10a39e9a5b1ae55cb003d638eba7aaa0_51_1.png)

![](img/10a39e9a5b1ae55cb003d638eba7aaa0_51_2.png)

## 注意

ADO.NET 已经包含了 `DbProviderFactory` 抽象类以及像 `SqlClientFactory`、`OleDbFactory` 等具体类。此外，使用像 Entity Framework 这样的 ORM 会自动处理数据库切换。这里提到的场景仅用于学习目的。

## 摘要

在这种方法中，我们已经了解了工厂方法模式。我们讨论的示例包含在附件中。

## 13. 享元模式

在本章中，我们将讨论享元设计模式。它是 23 种设计模式之一，提供了一种改进的对象管理方式。

## 挑战

你正在开发一个身份证创建 Web 应用程序。该应用程序有 10 万条学生记录，需要为这些记录创建身份证。

以下是执行身份证生成的 `StudentCard` 类。在分配学生姓名、地址、照片属性后，我们需要调用 `GenerateIdCard()` 方法获取身份证图像。生成的每张卡片图像都会保存到文件系统。

![](img/10a39e9a5b1ae55cb003d638eba7aaa0_52_0.png)

问题是创建了 10 万个类实例。如何减少实例数量？

## 定义

GoF 定义：“使用共享来高效地支持大量细粒度对象”

## 实现

使用享元模式，我们可以解决上述问题。从上述问题中我们可以看到，任一时刻只需要一个实例。

我们可以只使用一个 `StudentCard` 类实例，并在循环内共享它来分配属性和生成身份证。

该模式建议在以下情况使用：

- 减少实例数量
- 共享公共属性

这是旧过程：

![](img/10a39e9a5b1ae55cb003d638eba7aaa0_53_0.png)

这里根据学生数量，创建 `StudentCard` 的实例。

这将是新过程：

![](img/10a39e9a5b1ae55cb003d638eba7aaa0_53_1.png)

这里只创建了 1 个 `StudentCard` 实例。

## 缺点

尽管享元模式解决了许多问题，我想列出使用它的一些可能缺点。

- 需要更多的配置代码来在属性之间切换
- 如果使用锁，会降低多线程环境中的性能

## 摘要

在本章中，我们探讨了享元设计模式。如果正确使用，该模式有助于减少系统资源消耗。相关源代码包含我们讨论的示例。请让我知道你对本章的评论。

## 14. 代理模式

在本章中，我们将讨论代理设计模式。它是 GoF 的 23 种设计模式之一。像往常一样，我们可以从挑战和解决方案的风格开始。

## 挑战

你正在处理 Excel COM 对象的自动化。业务逻辑需要过多考虑 COM 的实例化、在调用实际功能之前进行基础工作等。

同样的代码明天可能会被 DCOM 取代。因此，Excel 访问代码遍布你的应用程序。如何设计得更好？

![](img/10a39e9a5b1ae55cb003d638eba7aaa0_56_0.png)

## 定义

GoF 定义：“为另一个对象提供代理或占位符以控制对其的访问”

## 实现

我们可以使用代理模式解决上述问题。正如定义所说，我们需要创建一个占位符或包装器包裹原始对象，以控制对其的访问。这样我们可以获得以下优势：

- 通过在一处更改配置来与 COM 或 DCOM Excel 对象通信
- 为应用程序提供一个简单的接口来与 Excel COM/DCOM 通信
- 让应用程序感觉自己正在与本地对象通信

## 应用

以下是带有数据的应用程序：

