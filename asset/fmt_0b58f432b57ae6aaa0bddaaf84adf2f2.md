
# ItemRepositoryTests.cs

完成该任务后，你应该再次运行测试。在这种情况下，测试可能仍然失败，但你应该养成经常运行测试的习惯。至少在完成每个任务后运行它们。

如所料，测试仍然失败。但它失败在不同的地方，原因也不同。这表明你取得了进展。新的失败发生在 `TypeRepository` 的 `Save` 方法中——具体是在 `TypeRepository` 的第 15 行。

```csharp
public class ItemTypeRepository : IItemTypeRepository
{
    public void Save(ItemType itemType)
    {
        throw new NotImplementedException();
    }
}
```

# TypeRepository.cs

我使用 JetBrains Resharper (www.jetbrains.com) 来增强我的 Visual Studio 开发环境。当使用 Resharper 创建此方法时，它会自动添加抛出 `NotImplementedException` 的实现。如果你没有使用 Resharper，实现它仍然是一个好主意，以确保代码已经实现。

为了完成此功能，你需要实现此方法。现在你只想编写可能运行的最简单代码：

```csharp
public class ItemTypeRepository : ITypeRepository
{
    public int Save(ItemType item)
    {
        return 1;
    }
}
```

# ItemTypeRepository.cs

没有人否认这是可能满足测试要求的简单代码。诚然，单行代码不太可能是该功能或其来源用户故事的解决方案。但根据你现在在该功能生命周期中所处的位置，这是逻辑上的下一步。再次运行测试产生了另一个失败，如图 7-8 所示。

![](img/15cb6759e167a2d15e60bc37de753a62_154_0.png)

# 图 7-8

在这种情况下，存储方法返回的值不是测试预期的。显然需要某些上下文。

为了更完整地定义上下文，你需要告诉测试在调用 `ItemRepository` 的 `Save` 方法时期望什么样的 `ItemType` ID。如果我正在编写向数据存储保存数据的测试，并且在运行时得到了某种 ID，我喜欢让单元测试在执行时随机选择：

```csharp
protected override void Establish_context()
{
    base.Establish_context();
    var randomNumberGenerator = new Random();
    _itemTypeId = randomNumberGenerator.Next(32000);
    _itemTypeRepository = new ItemRepositoryType();
}
```

## 第 7 章 实现第一个用户故事

从表面上看，你可能会观察这个单元测试并认为我引入了某种程度的不确定性。但事实并非如此。`ItemRepository` 类上的 `Save` 方法应该始终表现相同。它应该为正在保存到数据的实体返回一个 ID 号。我创建了一种情况，即每次测试运行时 ID 号都不同，但在每次测试执行的范围内它保持不变。由于随机 ID 的确定是在创建测试的过程中完成的，因此它不会为测试引入任何不确定性。我只是改变了返回的 ID 值；获取 ID 号的步骤并没有改变。在这种情况下，这种区别并不清晰，我将在演示 `ItemRepository` 的模拟依赖时触及这一点。

如果你运行此测试，你会发现它失败了，如图 7-9 所示。

![](img/15cb6759e167a2d15e60bc37de753a62_155_0.png)

# 图 7-9

在这种情况下，测试期望返回 42 作为 `forType Id`。`ItemRepository` 类 `Save` 方法的当前实现返回了 1。

是时候让这个测试通过迈向下一步了。在这个阶段，思考架构的设计是有帮助的。具体来说，是时候讨论持久化如何实现了。

该应用程序使用对象关系映射（ORM）框架 Fluent NH (FNH) 进行数据持久化。我在第 5 章中探讨了 ORM 的概念，并在第 8 章中向你展示如何使用它来处理持久化。.NET 世界提供了多种 ORM 框架供选择。我为此项目选择了 FNH，因为这是我最熟悉的框架。如果你或你的团队对像 Entity Framework 这样的 ORM 有更多经验，并且该工具满足你们的需求，那么它可能就是适合你们的 ORM。书中使用 FNH 的示例是可移植的，你可以选择使用你和团队决定使用的任何 ORM 实现相同的实践。

> 如果你不熟悉 FNH，不要担心。这个示例没有使用 FNH 框架的任何高级功能。我将停下来并简要解释示例中针对 FNH 的步骤。

FNH 像现代 ORM 一样，鼓励使用第 5 章讨论的仓库模式。我经常使用 FNH，我开发了一个基础泛型仓库可以用于项目。使用 FNH 配合 `Specification` 类，我在大多数项目中利用此类。该仓库包含了下载的代码；但是此示例演示了如何从零构建仓库。

FNH 提供了一个 `Session` 类来处理与数据的交互。从应用程序代码到仓库的调用始终通过 `ISessionFactory` 实例创建的 FNH Session 对象结束。要在 `ItemTypeRepository` 中使用这些内容，你需要添加引用 `FluentNHibernate` 和 `NHibernate`，如图 7-10 所示。

![](img/15cb6759e167a2d15e60bc37de753a62_156_0.png)

# 图 7-10

在 `ItemTypeRepository` 识别 FNH 框架类之前，你需要在 `ItemTypeRepository.cs` 中添加语句：

```csharp
using NHibernate;
```

# ItemTypeRepository.cs

现在你需要在 `ItemTypeRepository` 类中添加成员变量来存储 `ISessionFactory` 对象：

```csharp
public class ItemTypeRepository : ITypeRepository
{
    private ISessionFactory _sessionFactory;

    public int Save(ItemType item)
    {
        return 1;
    }
}
```

# ItemTypeRepository.cs

最后，你需要在 `ItemTypeRepository` 类中添加一个构造函数，允许在创建 `ItemTypeRepository` 时提供 `ISessionFactory` 的类：

```csharp
public ItemTypeRepository(ISessionFactory sessionFactory)
{
    _sessionFactory = sessionFactory;
}
```

# ItemTypeRepository.cs

## 第 7 章 实现第一个用户故事

回顾一下，这里是 `ItemTypeRepository` 类的完整列表：

```csharp
public class ItemTypeRepository : ITypeRepository
{
    private ISessionFactory _sessionFactory;

    public ItemTypeRepository(ISessionFactory sessionFactory)
    {
        _sessionFactory = sessionFactory;
    }

    public int Save(ItemType itemType)
    {
        return 1;
    }
}
```

现在是尝试运行测试的指南。遗憾的是，应用程序不再编译。当你创建一个允许客户端注入 `ISessionFactory` 值的 `ItemTypeRepository` 构造函数时，你删除了默认（无参数）构造函数。要使用 `ItemTypeRepository`，你需要为实现 `ISessionFactory` 的构造函数提供一个值。由于是单元测试，你需要提供一个模拟对象而不是有效的 FNH Session Factory。

正如你在第 2 章记得的，模拟框架允许你向要测试的类创建存根对象，以确保代码与外部依赖隔离开。要使用 Moq 框架，你需要在 `OSIM.UnitTests` 项目中添加引用，如图 7-11 所示。

![](img/15cb6759e167a2d15e60bc37de753a62_157_0.png)

# 图 7-11

下一步是在 `saving_valid_item_type` 类的 `Establish_context` 方法中添加代码，以在 FNH `ISessionFactory` 接口上创建一个模拟对象：

```csharp
protected override void Establish_context()
{
    base.Establish_context();
    var randomNumberGenerator = new Random();
    _itemId = randomNumberGenerator.Next(32000);
    var sessionFactory = new Mock<ISessionFactory>();
    _itemTypeRepository = new ItemTypeRepository();
}
```

![](img/15cb6759e167a2d15e60bc37de753a62_157_1.png)

### 实现功能

你会注意到 Visual Studio 提示它没有 `ISessionFactory` 的定义。这是因为 `OSIM.UnitTests` 项目没有 FNH 库的引用。需要添加它们（见图 7-12）。

然后你需要在 `ItemRepository.cs` 文件中添加 `using` 语句以包含所需的 FNH 命名空间：

```csharp
using NHibernate;
```

现在你可以使用你模拟的 Session Factory 作为参数 `ITypeRepository` 的构造函数：

```csharp
protected override void Establish_context()
{
    var randomNumberGenerator = new Random();
    _itemTypeId = randomNumberGenerator.Next(32000);
    var sessionFactory = new Mock<ISessionFactory>(sessionFactory.Object);
    _itemTypeRepository = new ITypeRepository(sessionFactory);
}
```

![](img/15cb6759e167a2d15e60bc37de753a62_158_0.png)

# 图 7-12

![](img/15cb6759e167a2d15e60bc37de753a62_158_1.png)

# ITypeRepository.cs

现在是时候为 `ITypeRepository` 方法创建一个调用 FNH API 的 `Save` 方法实现了。正如提到的，FNH 的所有数据库访问都是通过 `Session` 类的。你通过实现 `ISessionFactory` 接口的方法实例获取 `Session` 类实例。这里是 `ITypeRepository` 中利用 `Session` 类将 `IType` 保存到数据库的实现：

```csharp
public int Save(IType itemType)
{
    int id;
    using (var session = _sessionFactory.OpenSession())
    {
        id = (int) session.Save(itemType);
        session.Flush();
    }
    return id;
}
```

# ITypeRepository.cs

如果你从未用过 FNH 框架，这些特定的 FNH 命令需要一些解释。第一步是从 `SessionFactory` 获取 `Session`。这本质上是你与数据库的连接。`SessionFactory` 在创建时配置了连接数据库所需的信息。这个主题在第 8 章会有更详细的介绍。第一个调用是将 Session 对象 传递给 `Save` 方法。该方法将实体保存到数据库并返回主键或 ID 值。指定实体中的哪个字段是 ID 是在映射中完成的，这将在第 8 章介绍。接下来调用 `Flush` 以确保任何对数据库的待处理操作已完成。当到达 `using` 块结束时，Session 将关闭。

再次运行测试将产生另一个失败，如图 7-13 所示。

![](img/15cb6759e167a2d15e60bc37de753a62_159_0.png)

# 图 7-13

ItemRepository.cs 文件的第 26 行是对 Session 类 Save 方法的调用。`NullReferenceException` 告诉你在调用 OpenSession 方法时 Session 返回了 null。这意味着你需要向该对象再添加一个 mock 来代表 Session。你还需要为 SessionFactory.OpenSession 添加一个存根方法（stub method），返回 mock 的 Session 对象：

```csharp
protected override void Establish_context()
{
    base.Establish_context();
    var randomNumberGenerator = new Random();
    var _itemId = randomNumberGenerator.Next(32000);
    var sessionFactory = new Mock<ISessionFactory>();
    var session = new Mock<ISession>();
    sessionFactory.Setup(sf => sf.OpenSession()).Returns(session.Object).Returns(sessionFactory.Object);
    _itemRepository = new ItemRepositoryTests;
}
```

这种语法看起来与第 2 章“Mock 基础”部分中的代码相似。它指示代表 SessionFactory 的 mock，在调用 SessionFactory 上的 OpenSession 方法时，返回你为 Session 创建的 mock。尽管如此，在此设置下运行测试显示你的工作仍未完成（见图 7-14）。

### 实现功能

| 运行 | 状态 |
|---|---|
| 通过: 失败: 1 错误: 0 未完成: 0 无效: 0 忽略: 0 跳过: 0耗时: 0.05s | |

```
C:\Users\James\Documents\Exception\TDD\Chapter7\Tests.cs
at ISM.Persistence.ItemRepository.Save(itemType) in C:\Users\James
set : System.NullReferenceException was not set to an instance of an object.
```

```
at ISM.Persistence.ItemRepository.Save(itemType) in C:\Users\James
Documents\Exception\TDD\Chapter7\Tests.cs
at C:\Users\James
```
