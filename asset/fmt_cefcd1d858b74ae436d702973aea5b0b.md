
# 第 5 章 模拟外部资源

## 依赖注入模式

尝试运行此代码将会失败，因为此时代码无法编译，如图 5-3 所示。

为了使其能够运行，你需要从 `Inject` 内核请求一个对象并赋值给 `actual`。使用你需要的 `Inject` 类，并在你的单元测试的开头为 `Inject` 程序集添加 `using` 语句：

![](img/15cb6759e167a2d15e60bc37de753a62_110_1.png)

现在，你需要在你的单元测试中添加代码，以创建一个 `Inject` 内核的实例并从它创建一个 `BusinessService` 实例：

```csharp
[Test]
public void ShouldBeAbleToGetBusinessServiceFromInject() {
    BusinessService actual;
    var kernel = new StandardKernel(new CoreModule());
    actual = kernel.Get<BusinessService>();
    Assert.IsNotNull(actual);
}
```

在创建 Ninject 的 `StandardKernel` 实例时，你需要为它提供一个 `CoreModule` 实例。这让 Ninject 知道了创建对象的规则和步骤。在示例中，`StandardKernel` 只接受一个模块（`CoreModule`）作为它的规则集。这个示例是可以的，因为只处理了一个库（`BusinessApplication.Core`）。但如果你有多个程序集呢？你可以创建一个包含解决方案中所有内容创建规则的模块，但这不是好主意。它还要求项目模块固定以感知所有其他项目和程序集。它还限制了解决方案中组件的重用。如果你在库 B 中有一个组件，但它的创建规则在库 A 中，那么你现在依赖于库 A 及其所有依赖项。要解决这个问题，为解决方案中的每个项目创建一个模块，为该库中的所有类和接口提供创建规则。这意味着库之间的依赖性降低了，重用也变得更容易。

`StandardKernel` 的构造函数有一个接受模块数组的重载方法。这允许你为应用程序创建一个单一内核（在实践中，此内核应该是单例），它包含在应用程序任何地方创建你所需内容的信息。创建此类内核的语法如下：

```csharp
var kernel = new StandardKernel(new ModuleA(),
              new ModuleB(),
              new ModuleC());
```

运行测试显示存在一个问题，如图 5-4 所示。

![](img/15cb6759e167a2d15e60bc37de753a62_111_0.png)

堆栈轨迹告诉你 `CoreModule.cs` 文件中的第 32 行存在问题：

```csharp
var databaseConnectionString = ConfigurationManager
              .ConnectionStrings["MyConnectionString"].ConnectionString;
```

当单元需要来自应用程序配置文件（`web.config` 或 `app.config`）的信息时，它需要该文件的自己的实例。该文件是添加到测试所在的 Visual Studio 项目中，还是从另一个项目复制的，并不重要。它无法访问另一个项目的配置文件。要解决这个问题，你可以向 `BusinessApplication.UnitTests` 项目添加一个 `app.config` 文件，并用连接字符串填充它：

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <connectionStrings>
    <add name="MyConnectionString" connectionString="Sample Configuration" />
  </connectionStrings>
</configuration>
```

当你运行测试时，Ninject 已经创建了 `BusinessService` 实例及其所有依赖对象，如图 5 所示。

| C:\Users\Desktop\Test\Book\BusinessApplication | Run | C:\Users\Desktop\Test\Book\Chapter 5\Code\SampleAfter\BusinessApplication\BusinessApplicationUnitTest |
|---|---|---|
| BusinessApplication | | |
| UnitTests | | |
| BusinessServiceTests | | |
| ShouldAbleToGetBusiness | | |
| Passed: 1 Failed: 0 Errors: 0 Inconclusive: 0 Invalid: 0 Skipped: 0 Ignored: 0 Elapsed: 1.650968 |

## 使用存储模式隔离数据

最终开发者决定，虽然智能对象可能有所帮助，但更大的好处是将数据访问逻辑从业务实体中分离。这样做创建了解耦，允许业务开发独立于数据访问和数据存储开发进行演进。这种独立性意味着后端数据存储可以发生变化，有时是巨大的变化，而业务领域逻辑和实体不受这些变化的影响。这种松耦合使得开发者更容易为他们的业务逻辑编写隔离单元测试。

### 抽象数据访问层

大多数业务应用程序使用某种数据存储。它可以是数据库管理系统 (DBMS)、文本或二进制文件、Web 服务或其他用于持久化数据的机制。在编写单元测试时，重要的是将被测试的代码与访问数据的隔离开来。存储模式抽象了应用程序中负责访问数据存储组件。

### 将数据库关注从业务代码中移出

.NET 1.0 发布时，它对 Microsoft ActiveX Data Object (ADO) 框架进行了更新，称为 ADO.NET。ADO.NET 不仅仅是 ADO 的 .NET 版本；它增加了许多旨在让开发者轻松处理类和对象的特性。因此，ADO.NET 的早期用户采用了“智能对象”架构，它是自持久的。通常，这会在类中嵌入数据读取器或数据集来检索和存储数据。

虽然这创建了一个可以快速地开发这些自持久对象的代码库，但它导致了许多其他问题。将访问逻辑分布在整个应用程序中会导致许多维护问题，对某个类的处理很少局限于该类。正因如此，无法围绕数据访问构建单一故障点。

这还引发了类之间复杂关系的问题。在某些情况下，一个类在没有实例化几个对象的情况下无法正确实例化自己。这产生了与前节类似的问题，即特定对象的逻辑和规则碎片化到了整个应用程序中。在这些情况下，无法在不违反 SRP 的情况下拥有运行的系统。

最后，这种模式使得隔离单元测试成为噩梦，如果可以的话。紧嵌入的 ADO.NET 代码无法快速或轻松地从业务逻辑中解耦。这使得为这些数据库连接点提供模拟对象变得困难，如果可能的话。

### 使用存储模式隔离数据

最终开发者决定，虽然智能对象可能有所帮助，但更大的好处是将数据访问逻辑从业务实体中移开。这样做创建了解耦，允许业务开发独立于数据访问和数据存储开发进行演进。

简而言之，仓库模式规定所有数据访问都将封装在一个仓库对象中，业务领域类将使用该对象来执行任何持久化工作（图 5-6）。

| 实体 CRUD（创建、检索、更新、删除）命令 | |
| :--- | :--- |
| 业务领域服务 | 响应实体对象或成功/失败返回值 |
| 实体仓库 | |

![](img/15cb6759e167a2d15e60bc37de753a62_114_0.png)

仓库在业务领域和数据存储之间创建了一个**接层**（shim）。仓库封装了关于数据如何以扁平格式存储，以及如何将这些数据从这种扁平格式翻译为实体对象的知识。每个实体都应该有自己的仓库。不同类型的仓库应该具有相似的接口和通用的基类，以帮助数据访问代码保持 DRY（不要重复）原则，并让学习如何使用仓库变得更容易。

可以使用任何数据访问技术创建仓库，包括 ADO.NET、服务和文件存储。许多对象关系映射（ORM）框架使得创建仓库变得简单。在使用了 Entity Framework 或 nHibernate 等框架来管理持久化的系统中，可以编写一个单一的仓库，接受任何实体作为泛型，并将特定于类型的工作交给框架。请检查您的 ORM 文档以获取更多信息。

### 注入仓库

你可以通过创建一个 `Person` 实体来对之前示例中的解决方案进行一些补充。

```csharp
public class Person {
    public int Id { get; set; }
    public string FirstName { get; set; }
    public string LastName { get; set; }
}
```

`PersonService` 类作为业务领域类，从执行业务规则和在业务工作中使用 `Person` 的角度处理 `Person` 对象。以下是 `PersonService` 的接口：

```csharp
public interface IPersonService {
    Person GetPerson(int personId);
}
```

`PersonService` 使用 `PersonRepository` 实例进行数据持久化。此示例仅实现了 `GetPerson` 方法，并且没有使用数据库后端，而是使用一个 `IList` 成员来持有 `Person` 数据：

```csharp
public interface IPersonRepository {
    Person GetPerson(int personId);
}
```

```csharp
public class PersonRepository : IPersonRepository {
    private readonly IList<Person> _personList;

    public Person GetPerson(int personId) {
        return _personList.Where(person => person.Id == personId).FirstOrDefault();
    }

    public PersonRepository() {
        _personList = new List<Person> {
            new Person { Id = 1, FirstName = "John", LastName = "Doe" },
            new Person { Id = 2, FirstName = "Richard", LastName = "Roe" },
            new Person { Id = 3, FirstName = "Amy", LastName = "Adams" }
        };
    }
}
```

现在已经定义了运行中的应用程序部分，你可以实现 `PersonService`：

```csharp
public class PersonService : IPersonService {
    public PersonService() {
    }

    public Person GetPerson(int personId) {
        return new Person();
    }
}
```

现在 `PersonService` 有一个空构造函数。你需要注入 `PersonRepository`，以便 `PersonService` 有方法访问数据存储并更改 `GetPerson` 方法的实现：

```csharp
public class PersonService : IPersonService {
    private readonly IPersonRepository _personRepository;

    public PersonService(IPersonRepository personRepository) {
        _personRepository = personRepository;
    }

    public Person GetPerson(int personId) {
        return _personRepository.GetPerson(personId);
    }
}
```

最后，你需要在 `CoreModule` 中定义创建 `PersonService` 和 `PersonRepository` 的规则：

```csharp
Bind<IPersonRepository>().To<PersonRepository>();
Bind<IPersonService>().To<PersonService>();
```

为了验证所有内容都正确连接，你想要编写一个单元测试来验证你可以从 Ninject 获取 `PersonService` 实例，并获取一个指示 `PersonService` 可以调用 `PersonRepository` 的 `Person` 对象：

```csharp
[TestFixture]
public class PersonServiceTests {
    [Test]
    public void ShouldBeAbleToCallPersonServiceGetPerson() {
        var expected = new Person { Id = 1, FirstName = "John", LastName = "Doe" };
    }
}
```
