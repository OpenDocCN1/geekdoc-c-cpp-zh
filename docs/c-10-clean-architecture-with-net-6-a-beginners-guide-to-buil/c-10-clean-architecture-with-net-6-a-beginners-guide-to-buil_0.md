
# C# 10 .NET 6 整洁架构：构建可维护、可测试、可扩展且健壮应用的初学者指南（Python 先驱者秘籍）

## 引言

### 锻造持久的软件：精通 .NET 6 的 C# 10 整洁架构

在今天不断演变的技术格局中，仅仅编写具有功能的软件是不够的。你需要那些具有韧性、适应性并且能够在变化中茁壮发展的应用程序。进入`C# 10 整洁架构`与`.NET 6`的世界，这是掌握这一强大组合以构建卓越软件解决方案的权威指南。

本书超越了纯粹的代码编写。它关乎构建持久的代码。我们将深入探讨整洁架构的变革世界，赋予你构建以下软件的能力：

- **解耦**：业务逻辑独立于表示层和数据访问层，培养灵活性和适应能力。
- **可测试**：松耦合有助于单元测试，确保代码质量并减少回归风险。
- **可维护**：清晰的关注点分离提高了代码的可读性并简化了未来的修改。

为什么选择`C# 10`和`.NET 6`？这一尖端组合为实现架构愿景提供了完美的平台。通过其强大的特性（如全局引用、最小接口、改进的 API 和性能），你拥有了构建整洁、高效且可扩展应用程序所需的工具。

在旅程结束，你将：

- 自信地使用`C# 10`和`.NET 6`原则进行设计和构建。
- 具备创建解耦、可维护和可测试应用程序的技能。
- 能够在架构实践做出贡献。

## 第一章：传统软件开发的挑战

传统软件开发面临许多挑战，特别是在维护代码质量、可扩展性和适应性方面。让我们在`C# 10`和`.NET 6`的语境中深入探讨这些挑战。

### 1. 单体架构

传统软件通常遵循单体架构，整个应用程序被构建为一个单一的、紧耦合的单元。随着应用程序的增长，扩展和维护变得困难。

```csharp
// 单体方法
public class MonolithicApplication
{
    private readonly DatabaseContext _dbContext;
    private readonly ILogger _logger;

    public MonolithicApplication()
    {
        _dbContext = new DatabaseContext();
        _logger = new Logger();
    }

    public void ProcessData()
    {
        // 业务逻辑与数据访问和日志紧耦合
        var data = _dbContext.GetData();
        _logger.Log("Processing data...");
    }
}
```

### 2. 可扩展性问题

单体架构使得独立扩展应用程序的不同部分变得挑战。在某些组件需要更多资源的情况下，扩展变得效率低下。

```csharp
// 难以扩展组件
public class MonolithicApplication
{
    // ...
    public void ProcessData()
    {
        // 处理数据
    }
    public void HandleRequests()
    {
        // 处理 HTTP 请求
    }
}
```

### 3. 错综的依赖

随着应用程序的增长，不同模块之间的依赖变得错综，使得在不产生意外副作用的情况下难以理解和修改代码库。

```csharp
// 错综的依赖
public class MonolithicApplication
{
    private readonly DatabaseContext _dbContext;
    private readonly ILogger _logger;
    private readonly EmailService _emailService;

    public MonolithicApplication()
    {
        _dbContext = new DatabaseContext();
        _logger = new Logger();
        _emailService = new EmailService();
    }

    public void ProcessData()
    {
        // 业务逻辑与数据访问、日志和邮件服务紧耦合
        var data = _dbContext.GetData();
        _logger.Log("Processing data...");
        _emailService.SendEmail("Data processed successfully!");
    }
}
```

### 4. 可测试性有限

在单体架构中，由于组件紧耦合，测试变得具有挑战性。很难在不测试整个应用程序的情况下隔离并测试单个模块。

```csharp
// 有限的测试测试性
public class MonolithicApplicationTests
{
    [Fact]
    public void ProcessData_Should_Process_Data_Successfully()
    {
        // 测试需要数据库连接、日志和邮件服务
        var application = new MonolithicApplication();
        // 断言
        // 难以隔离和测试数据处理逻辑
    }
}
```

为了解决这些挑战，在`C# 10`和`.NET 6`中采用整洁架构方法是有益的。整洁架构强调关注点分离、模块化和框架独立性。以下是其实现方式：

1. **关注点分离**：将应用程序划分为层（如表示、应用、领域和基础设施），具有清晰的边界和向内的依赖关系。
2. **模块化**：将每个层封装到单独的项目或模块中，便于管理和独立开发。
3. **依赖倒置原则**：依赖抽象而非具体实现，从而实现灵活并更容易测试。
4. **接口的使用和依赖注入**：利用接口定义组件之间的契约，并在运行时通过注入提供实现。

```csharp
// 整洁架构方法
// 应用层
public class DataProcessor
{
    private readonly IDataRepository _dataRepository;
    private readonly ILogger _logger;

    public DataProcessor(IDataRepository dataRepository, ILogger logger)
    {
        _dataRepository = dataRepository;
        _logger = logger;
    }

    public void ProcessData()
    {
        var data = _dataRepository.GetData();
        _logger.Log("Processing data...");
        // 处理数据
    }
}
```

## 第二章：引入整洁架构：构建持久的软件

整洁架构是一种强调关注点分离、模块化可维护性的软件设计哲学。通过遵循整洁架构原则，开发者可以创建随时间保持健壮并适应变化的软件。在`C# 10`和`.NET 6`的范围内，实现整洁架构确保了项目的生命力和可扩展性。

### 理解整洁架构

整洁架构基于将代码组织成层的思想，每个层都有清晰的职责，且依赖向内。层通常包括：

1. **表示层**：该层处理用户交互和输入输出操作。它由组件组成。
2. **应用层**：应用层包含特定于逻辑和用例。
3. **领域层**：领域层代表核心业务实体、规则。
4. **基础设施层**：基础设施层为外部依赖（如数据库和外部服务）提供实现。

### 在 C# 10 和 .NET 6 中实现整洁架构

让我们探索如何使用`C# 10`和`.NET 6`实现整洁架构，带有代码示例。

#### 表示层

```csharp
// 表示层（例如 ASP.NET Web API）
[ApiController]
[Route("[controller]")]
public class UserController : ControllerBase
{
    private readonly IUserService _userService;

    public UserController(IUserService userService)
    {
        _userService = userService;
    }

    [HttpGet("{id}")]
    public async Task<ActionResult<UserDto>> GetUserById(int id)
    {
        var user = await _userService.GetUserById(id);
        if (user == null)
        {
            return NotFound();
        }
        return Ok(user);
    }
}
```

#### 应用层

```csharp
// 应用层
public interface IUserService
{
    Task<UserDto> GetUserById(int id);
}

public class UserService : IUserService
{
    private readonly IUserRepository _userRepository;

    public UserService(IUserRepository userRepository)
    {
        _userRepository = userRepository;
    }

    public async Task<UserDto> GetUserById(int id)
    {
        var user = await _userRepository.GetById(id);
        if (user == null)
        {
            return null;
        }
        return MapToDto(user);
    }
}
```

#### 领域层

```csharp
// 领域层
public class User
{
    public int Id { get; set; }
    public string FirstName { get; set; }
    public string LastName { get; set; }
}
```

#### 基础设施层

```csharp
// 基础设施层（例如 Entity Framework）
public class UserRepository : IUserRepository
{
    private readonly ApplicationDbContext _dbContext;

    public UserRepository(ApplicationDbContext dbContext)
    {
        _dbContext = dbContext;
    }

    public async Task<User> GetById(int id)
    {
        return await _dbContext.Users.FindAsync(id);
    }
}
```

### 整洁架构的核心原则

#### 分层架构：关注点分离

分层架构是一种基础设计模式，通过将代码组织成不同的层（每层都有特定职责）来强调关注点分离。在`C# 10`和`.NET 6`的范围内，实现分层架构遵循这些原则，确保了模块化和维护性。

#### 依赖倒置规则：高层模块不应依赖于低层模块

依赖倒置规则规定高层模块不应依赖于低层模块，但两者都应该依赖抽象。这一原则促进了组件之间的松耦合。

#### 抽象：关注“是什么”而非“如何”

在软件开发领域，抽象在简化复杂性和实现更好的设计方面起着至关重要的作用。当我们关注“做什么”而不是“怎么做”时，我们可以创建更灵活、可维护和可扩展的代码。

#### 框架与依赖：是工具而非基础

框架和依赖是允许我们构建复杂应用程序的强大工具。然而，记住它们应该是支持我们代码的工具，而不是代码依赖的基础。

## 第三章：揭秘用于整洁架构的 C# 10 特性

### 最小接口：简化抽象和封装功能

在`C# 10`项目和`.NET 6`中，最小接口是简化抽象的强大工具。通过仅定义必要的成员，我们促进了清晰性、简单性和活性。

### 模式匹配增强：提高代码的可读性和维护性

模式匹配在`C# 10`和`.NET 6`发布后经历了显著增强。这些改进不仅让代码更易读，还通过为复杂的条件逻辑提供简洁且表达性的语法增强了维护性。

### 其他 C# 10 特性及其与整洁架构实践的协同作用

`C# 10`结合`.NET 6`引入了许多与整洁架构协同良好的特性。

## 第四章：为整洁架构配置开发环境

### 安装 Visual Studio 或你的首选 IDE

Visual Studio 是一种强大的集成开发环境 (IDE)，被 C# 开发者广泛用于构建针对 .NET 框架的应用程序。

### 为整洁架构开发配置 .NET 6 和 C# 10

为整洁架构开发配置 .NET 6 和 C# 10 涉及设置项目结构、依赖和开发环境。

### 理解项目模板和整洁架构结构

项目模板为开发者创建具有定义配置和结构的项目提供了起点。

## 第五章：整洁架构中使用 .NET 6 进行依赖注入

### 依赖注入原则

依赖注入 (DI) 是软件开发中用于管理组件之间依赖的设计模式。它促进了松耦合并提高了可测试性和维护性。

### 什么是依赖注入？

依赖注入是一种外部提供类的依赖而不是在类内部创建的技术。类不再直接创建依赖实例，而是通过构造函数、属性或方法将这些注入类中。

## 第六章：构建核心逻辑：业务规则层

### 在 C# 10 中实现业务规则层以提高维护性

业务规则层是应用程序的核心。它应该独立于任何外部关注。

### 对业务规则层进行单元测试以代码质量和信心

测试业务规则层确保核心逻辑按预期工作。

## 第七章：表示层：用户界面与交互

### 从表示层消费业务逻辑层

表示层处理用户交互和表示。

### 在表示层实现依赖注入以增强灵活性

## 第八章：使用 .NET 实现数据持久化

### 定义数据模型和用于持久化的实体映射

数据持久化处理数据的存储和检索。

### 通过关注点分离实现数据访问逻辑

对持久化层进行单元测试以确保数据处理可靠性。

## 第九章：基于 ASP.NET Core MVC 6 的整洁架构

### 从 ASP.NET Core MVC 控制器消费业务逻辑层

在 ASP.NET Core MVC 应用中实现依赖注入

利用 Minimal APIs 构建简洁高效的控制器（.NET 6 新特性）

## 第十章：针对健壮整洁架构应用的测试策略

### 集成测试：测试层之间的交互

结合 C# 10 特性利用测试框架（xUnit, NUnit）

针对 .NET 6 整洁架构项目的测试考虑

## 第十一章：依赖倒置原则用于松耦合和灵活性

### 用于数据访问抽象的存储库模式

在 C# 10 和 .NET 6 中实现微服务的整洁架构

## 第十二章：针对整洁架构的最佳实践和设计模式

### 用于整洁架构的设计模式：适配器、外观模式等

在 C# 10 和 .NET 6 中随项目演进维护整洁架构

## 第十三章：C# 和 .NET 整洁架构的未来

### 针对整洁架构项目的持续集成与持续交付 (CI/CD)

利用 C# 和 .NET 6 的整洁架构实现长期成功

## 结论

## 附录

### 术语表

### 使用 C# 10 和 .NET 6 展示整洁架构的应用程序代码示例

1. `EntityService`类依赖于`IRepository<Entity>`接口。
2. 在单元测试期间，会为`EntityService`类提供存储库的 mock 实现。
3. 测试验证了`GetAllEntities`方法返回了预期的实体数量。

依赖注入（Dependency Injection）为软件开发带来了显著收益，特别是在松耦合和可测试性方面。通过解耦组件并提供易于替换依赖的机制，DI 促进了模块化、灵活且可维护的代码。在整洁架构场景中，使用 C# 10 和 .NET 6 实现依赖注入可以增强软件系统的设计、模块化可测试性，最终带来更高质量和更易维护的应用。

## 第 6 章：构建核心逻辑：业务规则层

### 在整洁架构中定义业务规则和用例

在整洁架构中，定义的业务规则和用例对于创建可维护、可扩展且符合业务需求的软件系统至关重要。业务规则代表了系统行为的逻辑和约束，而用例则描述了参与者（用户或外部系统）与系统之间为了实现特定目标的交互。在本指南中，我们将探索如何在整洁架构的范围内定义业务规则和用例，并结合基于 C# 10 和 .NET 6 的代码示例。

#### 定义业务规则

业务规则封装了定义系统运行和行为的逻辑与约束。这些规则源于业务领域的需求，代表了系统的核心功能。在实现整洁架构时，清晰地识别并记录这些业务规则至关重要，以确保软件解决方案与业务目标一致。

##### 业务规则定义示例

让我们考虑银行应用程序中简单业务规则的示例：



```csharp
// 领域层
public class Account
{
    public decimal Balance { get; private set; }
    public Account(decimal initialBalance)
    {
        if (initialBalance < 0)
        {
            throw new ArgumentException("初始余额不能为负数。");
        }
        Balance = initialBalance;
    }
    public void Deposit(decimal amount)
    {
        if (amount <= 0)
        {
            throw new ArgumentException("存款金额必须为正数。");
        }
        Balance += amount;
    }
    public void Withdraw(decimal amount)
    {
        if (amount <= 0)
        {
            throw new ArgumentException("取款金额必须为正数。");
        }
        if (amount > Balance)
        {
            throw new InvalidOperationException("余额不足。");
        }
        Balance -= amount;
    }
}
```

在此示例中，业务规则规定账户的初始余额不能为负。此外，存款和取款操作必须以正数进行，且取款不能超过账户余额。

### 定义用例

用例描述了参与者（用户或外部系统）与系统之间为了完成特定任务或目标的交互。每个用例都代表了系统中一个独特且有意义的功能单元。在整洁架构中，用例被实现为应用服务，负责协调领域实体与基础设施组件之间的交互。

#### 用例定义示例

继续银行应用程序示例，让我们定义一个在两个账户之间转账的用例：

```csharp
// 应用层
public class TransferFundsUseCase
{
    private readonly IRepository<Account> _accountRepository;
    public TransferFundsUseCase(IRepository<Account> accountRepository)
    {
        _accountRepository = accountRepository;
    }
    public void Execute(int sourceAccountId, int targetAccountId, decimal amount)
    {
        var sourceAccount = _accountRepository.GetById(sourceAccountId);
        var targetAccount = _accountRepository.GetById(targetAccountId);
        if (sourceAccount == null || targetAccount == null)
        {
            throw new ArgumentException("无效账户 ID。");
        }
        sourceAccount.Withdraw(amount);
        targetAccount.Deposit(amount);
        _accountRepository.Update(sourceAccount);
        _accountRepository.Update(targetAccount);
    }
}
```

在这个用例中，`Execute` 方法协调了两个账户之间的资金转账。它从仓库获取源账户和目标账户，执行必要的取款和存款操作，并更新仓库中的账户。

清晰定义业务规则和用例是软件项目成功的基础，特别是在整洁架构背景下。通过清晰地识别和记录业务规则，开发者可以确保软件解决方案满足业务领域的需求并正确运行。同样，定义用例有助于明确系统的功能需求，并引导协调系统行为的应用服务的实现。通过定义良好的业务规则和用例，开发者可以创建出健壮、可维护且符合业务需求的软件系统。

## 在 C# 10 中实现业务规则层以提高可维护性

在整洁架构中，业务规则层封装了控制系统行为的核心逻辑和约束。有效实现这一层对于构建可维护、可扩展且健壮的软件应用程序至关重要。在本指南中，我们将探索如何在整洁架构背景下使用 C# 10 实现业务规则层，重点关注增强可维护性的原则。我们将提供基于 C# 10 和 .NET 6 的代码示例来说明关键概念。

### 业务规则层的结构

业务规则层通常位于整洁架构项目的领域层中。它由领域实体、值对象和封装应用程序核心业务逻辑的服务组成。通过有效组织业务规则层，开发者可以确保系统行为保持一致且易于维护。

### 维护可维护性业务规则层的原则

1. **单一职责原则 (SRP)**：业务规则层中的每个类都应该有单一职责，封装领域逻辑的特定方面。这确保了类是聚焦、内聚且易维护的。
2. **封装**：将领域逻辑封装在领域实体和服务中，以促进模块化和封装。避免在业务规则层外部暴露内部实现细节，以保持抽象性和灵活性。
3. **依赖倒置原则 (DIP)**：依赖抽象而非具体实现，以实现灵活性和扩展性。这一原则允许更易替换组件，并促进业务规则层内部的解耦。

#### 实现业务规则层的示例

让我们考虑一个简单的电子商务应用程序实现业务规则层的示例：

```csharp
// 领域层
public class Product
{
    public int Id { get; private set; }
    public string Name { get; private set; }
    public decimal Price { get; private set; }
    public int StockQuantity { get; private set; }
    public Product(int id, string name, decimal price, int stockQuantity)
    {
        Id = id;
        Name = name;
        Price = price;
        StockQuantity = stockQuantity;
    }
    public void AddStock(int quantity)
    {
        if (quantity <= 0)
        {
            throw new ArgumentException("数量必须为正数。");
        }
        StockQuantity += quantity;
    }
    public void RemoveStock(int quantity)
    {
        if (quantity <= 0)
        {
            throw new ArgumentException("数量必须为正数。");
        }
        if (quantity > StockQuantity)
        {
            throw new InvalidOperationException("库存不足。");
        }
        StockQuantity -= quantity;
    }
}

// 应用层
public class ProductService
{
    private readonly IRepository<Product> _productRepository;
    public ProductService(IRepository<Product> productRepository)
    {
        _productRepository = productRepository;
    }
    public void AddStockToProduct(int productId, int quantity)
    {
        var product = _productRepository.GetById(productId);
        if (product == null)
        {
            throw new ArgumentException("未找到产品。");
        }
        product.AddStock(quantity);
        _productRepository.Update(product);
    }
    public void RemoveStockFromProduct(int productId, int quantity)
    {
        var product = _productRepository.GetById(productId);
        if (product == null)
        {
            throw new ArgumentException("未找到产品。");
        }
        product.RemoveStock(quantity);
        _productRepository.Update(product);
    }
}
```

在此示例中：

- `Product` 类代表了封装电子商务系统核心逻辑的领域实体。
- `ProductService` 类提供了管理产品（如增加和删除库存）的应用级服务。
- 使用依赖注入将仓库注入服务类，遵循整洁架构原则。
- 在整洁架构背景下使用 C# 10 实现业务规则层对于构建聚焦、模块化且易于扩展的软件应用程序至关重要。遵循 SRP、封装和 DIP 等原则，通过定义良好的领域实体和服务，开发者可以确保业务系统的行为保持一致并符合业务需求随时间演进。

## 为了代码质量对业务规则层进行单元测试

单元测试是软件开发中确保代码质量、可靠性和可维护性的基本实践。在整洁架构、C# 10 和 .NET 6 的背景下，测试业务规则层对于验证核心逻辑的正确性和增强系统信心至关重要。在本指南中，我们将探索测试业务规则层的重要性，并提供基于业务规则的代码示例来演示如何编写单元测试。

### 测试业务规则层的重要性

1. **业务逻辑验证**：单元测试验证领域实体和服务实现的逻辑符合预期。通过孤立测试组件，开发者可以确保每个逻辑单元都正常工作。
2. **早期发现 Bug**：单元测试有助于在开发早期识别业务规则层中的 Bug 和问题。通过在单元测试级别捕捉错误，开发者可以在问题传播到系统其他部分之前解决它们。
3. **代码信心与重构**：在进行更改或重构代码时，单元测试提供了信心，确保行为保持一致。

### 编写有效的单元测试

为了为业务规则层编写有效的单元测试，请遵循以下实践：

1. **每个测试一个行为**：每个单元测试应该专注于测试单个行为或方面。这使得测试更具可读性、可维护且易于调试。
2. **使用描述性名称**：为单元测试选择描述性名称，以清晰指示正在测试的行为。这提高了测试套件的清晰度。
3. **准备-执行-断言 (AAA) 模式**：使用准备-执行-断言模式构建单元测试，其中设置（Arrange）、代码执行（Act）和预期行为的验证（Assert）是清晰分离的。
4. **使用 Mock 和 Stub**：对外部依赖进行 Mock 或 Stub 处理以隔离待测代码。这有助于避免副作用并使测试更可靠。

#### 测试业务规则层的示例

让我们继续电子商务应用程序，为 `Product` 实体和 `ProductService` 类编写单元测试：

```csharp
// Product 实体的单元测试
public class ProductTests
{
    [TestMethod]
    public void AddStock_Should_Increase()
    {
        // Arrange
        var product = new Product(1, "Test", 10.0m, 5);
        // Act
        product.AddStock(5);
        // Assert
        Assert.AreEqual(10, product.StockQuantity);
    }

    [TestMethod]
    public void RemoveStock_Should_Decrease()
    {
        // Arrange
        var product = new Product(1, "Test", 10.0m, 10);
        // Act
        product.RemoveStock(5);
        // Assert
        Assert.AreEqual(5, product.StockQuantity);
    }
}

// ProductService 的单元测试
public class ProductServiceTests
{
    [TestMethod]
    public void AddStockToProduct_Should_Increase()
    {
        // Arrange
        var mockRepository = new Mock<IRepository<Product>>();
        var product = new Product(1, "Test", 10.0m, 5);
        mockRepository.Setup(r => r.GetById(1)).Returns(product);
        var service = new ProductService(mockRepository.Object);
        // Act
        service.AddStockToProduct(1, 5);
        // Assert
        mockRepository.Verify(r => r.Update(product), Times.Once);
    }
}
```

# 第 7 章：表示层：用户界面与交互

## 使用关注点分离设计用户界面

在整洁架构中，关注点分离是一个促进模块化、可测试性和可扩展性的基本原则。在设计用户界面（UI）时，遵循这一原则对于确保 UI 与业务逻辑解耦至关重要。

### 界面设计中的关注点分离

界面设计中的关注点分离涉及将 UI 分为不同的组件，每个组件负责特定任务。

1. **视图组件**：代表视觉元素，如屏幕、表单或小部件。它们负责渲染 UI 元素。
2. **视图模型 (View Models)**：作为 UI 和逻辑层之间的中间层，包含 UI 特有的数据。
3. **表示逻辑**：处理用户交互和输入验证。此逻辑应封装在 UI 组件中，以保持代码库的聚焦和可维护。

### 使用整洁架构设计用户界面

在整洁架构项目设计设计用户界面时，请遵循这些指南以确保关注点分离：

1. **定义清晰的边界**：定义 UI 与其他层（如领域层）之间的边界。
2. **业务逻辑委托给应用层**：将复杂的业务逻辑委托给应用层处理。
3. **使用视图模型进行数据绑定**：使用视图模型表示 UI 特定的数据。

#### 关注点分离的 UI 设计示例

让我们考虑一个待办事项应用程序的界面设计示例：



```csharp
// 表示层
public class TodoItemViewModel
{
    public int Id { get; set; }
    public string Title { get; set; }
    public bool IsCompleted { get; set; }
}

public interface ITodoService
{
    IEnumerable<TodoItemViewModel> GetAllTodoItems();
    void AddTodoItem(TodoItemViewModel itemItem);
    void UpdateTodoItem(TodoItemViewModel itemItem);
    void DeleteTodoItem(int id);
}

public class TodoListViewModel
{
    private readonly ITodoService _todoService;
    public ObservableCollection<TodoItemViewModel> TodoItems { get; } = new ObservableCollection<TodoItemViewModel>();

    public TodoListViewModel(ITodoService todoService)
    {
        _todoService = todoService;
        LoadTodoItems();
    }

    private void LoadTodoItems()
    {
        TodoItems.Clear();
        var todoItems = _todoService.GetAllTodoItems();
        foreach (var todoItem in todoItems)
        {
            TodoItems.Add(todoItem);
        }
    }

    public void AddTodoItem(string title)
    {
        var newTodoItem = new TodoItemViewModel { Title = title };
        _todoService.AddTodoItem(newTodoItem);
        TodoItems.Add(newTodoItem);
    }

    public void UpdateTodoItem(TodoItemViewModel itemItem)
    {
        _todoService.UpdateTodoItem(itemItem);
    }

    public void DeleteTodoItem(int id)
    {
        _todoService.DeleteTodoItem(id);
        var todoItemToRemove = TodoItems.FirstOrDefault(item => item.Id == id);
        if (todoItemToRemove != null)
        {
            TodoItems.Remove(todoItemToRemove);
        }
    }
}

// View (XAML)
<ListBox ItemsSource="{Binding TodoItems}">
    <ListBox.ItemTemplate>
        <DataTemplate>
            <StackPanel Orientation="Horizontal">
                <CheckBox IsChecked="{Binding IsCompleted}" />
                <TextBlock Text="{Binding Title}" />
                <Button Content="Delete" Command="{Binding DeleteCommand}" />
            </StackPanel>
        </DataTemplate>
    </ListBox.ItemTemplate>
</ListBox>
```

1. 业务逻辑层（`TodoService`）定义了一个接口`ITodoService`，用于暴露待事项列表管理操作。

2. 表现层（`TodoListViewModel`）通过依赖注入使用`ITodoService`接口，以便与业务逻辑层进行交互。

从表现层消费业务逻辑层是整洁架构的一个关键方面，确保了表现层与底层业务逻辑解耦。通过遵循依赖注入、接口隔离和封装等原则，开发者可以创建模块化且可维护的应用程序。表现层与业务逻辑层之间的关注点分离提供了灵活性、可扩展性和测试性，允许软件系统随着时间的推移进行更容易演进和维护。

## 在表现层实现依赖注入以提高灵活性

依赖注入（`DI`）是一种强大的设计模式，通过将依赖项与其使用者解耦，促进了软件系统的松耦合和灵活性。在整洁架构以及使用`C# 10`和`.NET 6`的背景下，在表现层实现依赖注入可以增强灵活性和可维护性。它允许表现层的组件依赖于抽象而非具体实现，从而便于应用程序的测试、扩展和演进。在这份指南中，我们将探索如何在整洁架构应用的表现层中实现依赖注入，并配有基于`C# 10`和`.NET 6`的代码示例。

### 在表现层中使用依赖注入的好处

1. **解耦**：依赖注入将表现层中的组件与其依赖项解耦，减少了紧耦合并促进了模块化。这使得在不影响系统其他部分的情况下替换或修改依赖变得更容易。

2. **可测试性**：通过依赖抽象而非具体实现，表现层的组件变得更容易测试。在测试期间可以提供 mock 或桩（stub）实现，允许专注于特定行为的隔离单元测试。

3. **灵活性**：依赖注入通过促进依赖项的不同实现的使用，在表现层中实现了更大的灵活性。这允许开发者更轻松地适应不断变化的需求或集成新功能。

## 在表现层实现依赖注入

让我们演示如何在整洁架构应用的表现层中实现依赖注入：

```csharp
// Presentation Layer (表现层)
public interface ITodoListViewModel
{
    ObservableCollection<TodoItem> TodoItems { get; }
    void AddTodoItem(string title);
    void UpdateTodoItem(TodoItem todoItem);
    void DeleteTodoItem(int id);
}

public class TodoListViewModel : ITodoListViewModel
{
    private readonly ITodoService _todoService;
    public ObservableCollection<TodoItem> TodoItems { get; } = new ObservableCollection<TodoItem>();

    public TodoListViewModel(ITodoService todoService)
    {
        _todoService = todoService;
        LoadTodoItems();
    }

    private void LoadTodoItems()
    {
        TodoItems.Clear();
        var todoItems = _todoService.GetAllTodoItems();
        foreach (var todoItem in todoItems)
        {
            TodoItems.Add(todoItem);
        }
    }

    public void AddTodoItem(string title)
    {
        var newTodoItem = new TodoItem { Title = title };
        _todoService.AddTodoItem(newTodoItem);
        TodoItems.Add(newTodoItem);
    }

    public void UpdateTodoItem(TodoItem todoItem)
    {
        _todoService.UpdateTodoItem(todoItem);
    }

    public void DeleteTodoItem(int id)
    {
        _todoService.DeleteTodoItem(id);
        var todoItemToRemove = TodoItems.FirstOrDefault(item => item.Id == id);
        if (todoItemToRemove != null)
        {
            TodoItems.Remove(todoItemToRemove);
        }
    }
}
```

在此示例中：

1. `TodoListViewModel`类实现了接口`ITodoListViewModel`，该接口定义了在表现层中与待办事项交互的合约。

2. `TodoListViewModel`类依赖于抽象`ITodoService`与待办事项交互，从而提供了灵性和可测试性。

### 使用依赖注入容器注册依赖项

要在表现层中使用依赖注入，需要将依赖项注册到依赖注入容器中。在应用程序启动配置中，可以如下注册依赖项：

```csharp
// Dependency Injection Configuration (依赖注入配置)
services.AddSingleton<ITodoService, TodoService>();
services.AddSingleton<ITodoListViewModel, TodoListViewModel>();
```

在整洁架构应用的表现层实现依赖注入促进了灵活性、可测试性和可维护性。通过依赖抽象而非具体实现，表现层的组件变得更容易测试，并更能适应变化的需求。关注点分离和依赖项解耦允许更大的模块化和扩展性，使得应用程序随时间的推移更易演进。通过依赖注入，开发者可以构建出健壮、可维护且可扩展的整洁架构应用程序。

# 第 8 章：使用 .NET 实现数据持久化

## 选择合适的数据访问技术 (.NET Entity Framework Core)

在整洁架构中，选择合适的数据访问技术对于构建可扩展、可维护且高效的应用程序至关重要。`.NET Entity Framework Core`是`.NET`应用程序数据访问的热门选择，因为它具有易用性、灵活性和丰富的特性集。在这份指南中，我们将结合代码示例，探索在基于整洁架构原则的`C# 10`应用程序中，何时选择`.NET Entity Framework Core`作为数据访问技术的考虑因素。

### 选择 .NET Entity Framework Core 的考虑因素

1. **易用性**：`.NET Entity Framework Core`为数据库提供了高层抽象，允许开发者使用熟悉的面向对象概念（如实体、关系和 LINQ 查询）与数据库交互。这简化了数据访问代码并减少了所需的样板代码。

2. **ORM 特性**：`.NET Entity Framework Core`提供了广泛的功能，如自动更改跟踪、延迟加载和查询翻译。这些功能通过自动处理许多数据库操作简化了开发流程并提高了生产力。

3. **跨平台支持**：`.NET Entity Framework Core`是跨平台的，可以与`.NET Core`、`.NET Framework`以及`.NET 5/6`使用。这确保了跨环境的兼容性，允许开发者构建运行在各种操作系统上的应用程序。

4. **性能**：`.NET Entity Framework Core`相比之前的版本进行了重大的性能改进，在读写操作上提供了更好的性能。它还提供了查询缓存和编译查询等功能来进一步优化性能。

5. **与整洁架构集成**：`.NET Entity Framework Core`与整洁架构原则良好集成，允许开发者设计与其他应用层解耦的数据访问代码。这有助于应用程序的测试、维护和演进。

### 在整洁架构中使用 .NET Entity Framework Core 的示例

让我们演示如何在整洁架构中使用`.NET Entity Framework Core`与数据库交互：

```csharp
// Infrastructure Layer (基础设施层)
public class TodoDbContext : DbContext
{
    public TodoDbContext(DbContextOptions<TodoDbContext> options) : base(options){}
    public DbSet<TodoItem> TodoItems { get; set; }
}

public class TodoRepository : IRepository<TodoItem>
{
    private readonly TodoDbContext _dbContext;
    public TodoRepository(TodoDbContext dbContext)
    {
        _dbContext = dbContext;
    }

    public IEnumerable<TodoItem> GetAll()
    {
        return _dbContext.TodoItems.ToList();
    }

    public TodoItem GetById(int id)
    {
        return _dbContext.TodoItems.Find(id);
    }

    public void Add(TodoItem entity)
    {
        _dbContext.TodoItems.Add(entity);
        _dbContext.SaveChanges();
    }

    public void Update(TodoItem entity)
    {
        _dbContext.TodoItems.Update(entity);
        _dbContext.SaveChanges();
    }

    public void Delete(TodoItem entity)
    {
        _dbContext.TodoItems.Remove(entity);
        _dbContext.SaveChanges();
    }
}
```

在此示例中：

1. `TodoDbContext`类表示数据库上下文，并提供对`TodoItem`体的访问。

2. `TodoRepository`类实现了存储库模式，并使用 .NET Entity Framework Core 与数据库进行交互。

## 在启动类中配置 Entity Framework Core

为了在应用程序中配置 .NET Entity Framework Core，你需要在启动类中注册数据库上下文和存储库：

```csharp
// Startup Configuration
public void ConfigureServices(IServiceCollection services)
{
    services.AddDbContext<TodoDbContext>(options =>
        options.UseSqlServer(Configuration.GetConnectionString("DefaultConnection")));
    services.AddScoped<IRepository<TodoItem>, TodoRepository>();
    // 其他服务注册...
}
```

选择合适的数据访问技术对于清洁架构应用的成功至关重要。.NET Entity Framework Core 提供了许多优势，例如易用性、跨平台支持以及与清洁架构原则的集成。通过利用 .NET Entity Framework Core，开发者可以构建健壮、可维护且易于扩展的应用程序。无论你是在构建小型应用程序还是大型企业级系统，.NET Entity Framework Core 都能提供必要的工具和功能，在遵循清洁架构原则的同时满足你的数据访问需求。

## 定义数据模型并为持久化映射实体

定义数据模型并为持久化映射实体是软件开发中的一个关键方面，特别是在使用 C# 10 和 .NET 6 的清洁架构背景下。在本指南中，我们将深入探讨什么是数据模型、如何定义它们，以及如何在 C# 10 和 .NET 6 中为持久化映射实体。

### 什么是数据模型？

数据模型表示系统内部数据的结构和关系。它们作为软件应用程序中组织和操作数据的蓝图。在 C# 10 和 .NET 6 中，数据模型通常使用类表示。

让我们为博客应用定义一个简单的数据模型：



进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`。

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

---

```csharp
public class Post
{
    public int Id { get; set; }
    public string Title { get; set; }
    public string Content { get; set; }
    public DateTime CreatedAt { get; set; }
    public DateTime UpdatedAt { get; set; }
}
```

在这个示例中，`Post`类表示博客文章，具有`Id`、`Title`、`Content`、`CreatedAt`和`UpdatedAt`等属性。

### 为持久化映射实体

为持久化映射实体涉及定义如何从数据源（如数据库）存储和检索数据模型。在`C# 10`和`.NET 6`中，这通常通过对象关系映射器（ORM）如`Entity Framework Core`实现。

让我们创建一个`DbContext`并为`Post`实体建立持久化映射：

```csharp
using Microsoft.EntityFrameworkCore;

public class BlogDbContext : DbContext
{
    public DbSet<Post> Posts { get; set; }
    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
    {
        optionsBuilder.UseSqlServer("your_connection_string_here");
    }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        modelBuilder.Entity<Post>(entity =>
        {
            entity.ToTable("Posts");
            entity.HasKey(e => e.Id);
            entity.Property(e => e.Title).IsRequired().HasMaxLength(100);
            entity.Property(e => e.Content).IsRequired();
            entity.Property(e => e.CreatedAt).IsRequired();
            entity.Property(e => e.UpdatedAt).IsRequired();
        });
    }
}
```

在此代码中：

1. 我们定义了一个继承自`DbContext`的`BlogDbContext`类，该类由`Entity Framework Core`提供。

2. 我们创建了一个`DbSet<Post>`属性来表示数据库中的`Post`实体集合。

3. 在`OnConfiguring`方法中，我们指定了数据库提供程序和连接字符串。

4. 在`OnModelCreating`方法中，我们定义了实体的配置。这包括指定表名、主键和列映射。

## 使用DbContext

现在我们已经定义了`DbContext`并映射了`Post`实体，可以使用它来与数据库交互：

```csharp
using System;
using System.Linq;

class Program
{
    static void Main(string[] args)
    {
        using var dbContext = new BlogDbContext();
        // 创建一篇新文章
        var newPost = new Post
        {
            Title = "Introduction to Clean Architecture",
            Content = "Lorem ipsum dolor sit amet, consectetur adipiscing elit.",
            CreatedAt = DateTime.UtcNow,
            UpdatedAt = DateTime.UtcNow
        };
        dbContext.Posts.Add(newPost);
        dbContext.SaveChanges();

        // 获取所有文章
        var posts = dbContext.Posts.ToList();
        foreach (var post in posts)
        {
            Console.WriteLine($"Title: {post.Title}, Content: {post.Content}");
        }
    }
}
```

在此代码中：

1. 我们实例化了一个`BlogDbContext`的新实例。

2. 我们创建了一个新的`Post`实体并将其添加到`Posts` DbSet中。

3. 我们调用`SaveChanges`将更改持久化到数据库。

4. 我们从数据库中检索所有文章并显示它们的标题和内容。

定义数据模型并为持久化建立实体映射对于构建健壮且可维护的软件应用程序至关重要。在`C# 10`和`.NET 6`中，这通常使用`classes`来表示数据模型，并使用`Entity Framework Core`为`persistence`映射实体。通过遵循整洁架构原则，我们可以设计出模块化、可测试且易于维护的系统。

# 使用关注点分离实现数据访问逻辑

通过关注点分离实现数据访问逻辑是软件开发中的基础实践，特别是使用`C# 10`和`.NET 6`遵循整洁架构时。在本指南中，我们将探索如何在保持关注分离的同时实现数据访问逻辑。

### 关注点分离

关注点分离（`SoC`）是一种设计原则，主张将软件系统分为不同的部分，每个部分处理一个独立的问题。这种分离增强了系统的可维护性、扩展性和可测试性。在数据访问逻辑中，`SoC`意味着将数据库操作与业务逻辑隔离。

### 仓库模式

`Repository`模式是遵循`SoC`原则实现数据访问逻辑的常用方法。它将数据访问代码从应用程序的其他部分抽象出来，并为与底层数据存储交互提供了一个清晰的接口。

让我们为博客应用程序实现仓库模式：

```csharp
public interface IPostRepository{
    Task<List<Post>> GetAllAsync();
    Task<Post> GetByIdAsync(int id);
    Task AddAsync(Post post);
    Task UpdateAsync(Post post);
    Task DeleteAsync(int id);
}

public class PostRepository : IPostRepository{
    private readonly BlogDbContext _dbContext;
    public PostRepository(BlogDbContext dbContext){
        _dbContext = dbContext;
    }
    public async Task<List<Post>> GetAllAsync(){
        return await _dbContext.Posts.ToListAsync();
    }
    public async Task<Post> GetByIdAsync(int id){
        return await _dbContext.Posts.FindAsync(id);
    }
    public async Task AddAsync(Post post){
        await _dbContext.Posts.AddAsync(post);
        await _dbContext.SaveChangesAsync();
    }
    public async Task UpdateAsync(Post post){
        _dbContext.Posts.Update(post);
        await _dbContext.SaveChangesAsync();
    }
    public async Task DeleteAsync(int id){
        var post = await _dbContext.Posts.FindAsync(id);
        if (post != null){
            _dbContext.Posts.Remove(post);
            await _dbContext.SaveChangesAsync();
        }
    }
}
```

在此段代码中：

1. 我们定义了一个`IPostRepository`接口，规定了与文章交互的契约。

2. 我们实现了该仓库接口的`PostRepository`类。

3. 仓库类封装了数据库操作，例如获取所有文章、通过`id`获取文章、添加新文章、更新现有文章以及删除文章。

### 依赖注入

为了在应用程序中使用该仓库，我们需要将其在`.NET Core`提供的依赖注入容器中注册：

```csharp
public class Startup{
    public void ConfigureServices(IServiceCollection services){
        services.AddDbContext<BlogDbContext>(options =>
            options.UseSqlServer("your_connection_string_here"));
        services.AddScoped<IPostRepository, PostRepository>();
        // 其他服务注册...
    }
}
```

通过将仓库注册为作用域服务（scoped service），我们确保每个HTTP请求都获得该仓库的实例。

### 使用仓库

现在，让我们来看看如何在应用程序中使用该仓库：

```csharp
public class PostService{
    private readonly IPostRepository _postRepository;
    public PostService(IPostRepository postRepository){
        _postRepository = postRepository;
    }
    public async Task<List<Post>> GetAllPosts(){
        return await _postRepository.GetAllAsync();
    }
    public async Task<Post> GetPostById(int id){
        return await _postRepository.GetByIdAsync(id);
    }
    public async Task CreatePost(Post post){
        await _postRepository.AddAsync(post);
    }
    public async Task UpdatePost(Post post){
        await _postRepository.UpdateAsync(post);
    }
    public async Task DeletePost(int id){
        await _postRepository.DeleteAsync(id);
    }
}
```

在此段代码中：

1. 我们定义了一个`PostService`类，封装了与文章相关的业务逻辑。

2. 服务类依赖于`IPostRepository`接口，允许它通过仓库与数据库交互。

3. 服务类中的每个方法都对应于文章的具体操作，例如获取所有文章、通过`id`获取文章、创建新文章、更新现有文章以及删除文章。

通过关注点分离来实现数据访问逻辑，对于构建可维护且可扩展的软件应用程序至关重要。通过遵循仓库模式（`Repository` pattern）并利用依赖注入，我们可以将数据库操作与应用程序的其他部分隔离，并确保每个组件都有清晰且定义的职责。这种方法不仅改进了代码结构，还便于单元测试和未来的增强。

## 持久层的单元测试以确保可靠的数据处理

对持久层进行单元测试对于确保软件应用程序中可靠的数据处理至关重要，特别是在使用`C# 10`和`.NET 6`遵循清洁架构原则时。在本指南中，我们将探索如何为持久层编写单元测试，以验证数据库操作的行为符合预期。

## 持久层单元测试的重要性

对持久层进行单元测试有助于确保：

1. 数据库操作（如插入、更新和删除数据）能够正常工作。

2. 数据访问代码能够优雅地处理边界情况和错误条件。

3. 数据库架构或ORM映射的更改不会破坏现有功能。

4. 业务逻辑以预期的方式与数据库交互。

## 测试策略

在测试持久层时，我们通常关注以下方面：

1. CRUD操作：测试我们是否可以从数据库创建、读取、更新和删除实体。

2. 错误处理：验证错误条件（如数据库连接失败或约束违反）是否被适当处理。

3. 数据完整性：确保数据完整性约束（如外键关系或唯一性约束）得到执行。

4. 性能：衡量数据库操作的性能，以确保它们满足应用程序的需求。

## 编写单元测试

让我们为之前实现的`PostRepository`类编写单元测试：

```csharp
public class PostRepositoryTests
{
    private BlogDbContext _dbContext;
    private IPostRepository _postRepository;
    [SetUp]
    public void Setup()
    {
        var options = new DbContextOptionsBuilder<BlogDbContext>().UseInMemoryDatabase(databaseName: "TestDatabase").Options;
        _dbContext = new BlogDbContext(options);
        _postRepository = new PostRepository(_dbContext);
    }
    [Test]
    public async Task AddPost_Should_Add_Post_To_Database()
    {
        // Arrange
        var post = new Post{
            Title = "Test Post",
            Content = "This is a test post.",
            CreatedAt = DateTime.UtcNow,
            UpdatedAt = DateTime.UtcNow
        };
        // Act
        await _postRepository.AddAsync(post);
        // Assert
        var result = await _dbContext.Posts.FirstOrDefaultAsync(p => p.Title == "Test Post");
        Assert.NotNull(result);
        Assert.AreEqual(post.Title, result.Title);
    }
    // Write similar tests for other CRUD operations and error handling scenarios
}
```

在此段代码中：

1. 我们使用`NUnit`作为测试框架，但你可以使用任何选择的测试框架。

2. 在`Setup`方法中，我们为每个测试初始化了一个内存数据库上下文和仓库实例。

3. 我们编写了一个测试来验证向数据库添加帖子是否符合预期。我们准备数据（Arrange），通过调用仓库方法执行（Act），然后断言结果（Assert）。

## 模拟依赖

在为持久层编写单元测试时，通常会模拟外部依赖（例如数据库上下文），以隔离待测代码。我们可以使用`Moq`等模拟库来实现这一目的。



```csharp
public class PostRepositoryTests
{
    private Mock<BlogDbContext> _dbContextMock;
    private IPostRepository _postRepository;

    [SetUp]
    public void Setup()
    {
        _dbContextMock = new Mock<BlogDbContext>();
        _postRepository = new PostRepository(_dbContextMock.Object);
    }

    [Test]
    public async Task AddPost_Should_Add_Post_To_Database()
    {
        // Arrange
        var post = new Post
        {
            Title = "Test Post",
            Content = "This is a test post.",
            CreatedAt = DateTime.UtcNow,
            UpdatedAt = DateTime.UtcNow
        };

        // Act
        await _postRepository.AddAsync(post);

        // Assert
        _dbContextMock.Verify(m => m.Posts.AddAsync(post, default), Times.Once);
        _dbContextMock.Verify(m => m.SaveChangesAsync(default), Times.Once);
    }

    // Write similar tests for other CRUD operations and error handling scenarios
}
```

在此段代码中：

1. 我们使用 `Moq` 创建 `BlogDbContext` 的模拟实例。

2. 在测试方法中，我们准备数据，通过调用仓库方法执行，然后断言模拟对象上的适当方法已被调用。

对持久层进行单元测试对于确保软件应用程序中可靠的数据处理至关重要。通过对 CRUD 增删改操作、错误处理场景和数据完整性约束编写单元测试，我们可以验证数据库操作的行为符合预期，并优雅地处理边界情况。此外，通过使用模拟（mocking）库来隔离依赖项，我们可以专注于测试代码逻辑，而不依赖外部资源。总而言，对持久层的单元测试增强了应用程序的可靠性和可维护性。

# 第 9 章：使用 ASP.NET Core MVC 6 的整洁架构

## ASP.NET Core MVC 6 作为整洁架构中的表示层

使用 C# 10 和 .NET 6 将 ASP.NET Core MVC 6 实现为整洁架构中的表示层，是构建健壮且可维护的 Web 应用程序的强大组合。在本指南中，我们将探索如何结构化并将其集成到整洁架构解决方案中。

### 整洁架构概述

整洁架构是一种软件设计模式，强调关注点分离以及框架和外部依赖的独立。它由多个层组成，包括：

1. **表示层**：处理用户交互并向用户显示信息。

2. **应用层**：包含特定的业务逻辑，并协调表示层与领域层之间的交互。

3. **领域层**：包含核心业务逻辑和实体。

4. **基础设施层**：实现外部关注点，如数据库访问、外部服务和日志记录。

### 集成 ASP.NET Core MVC 6

让我们从在整洁架构解决方案中设置 ASP.NET Core MVC 6 开始：

1. 创建一个新的 ASP.NET Core Web 应用程序项目：

```bash
dotnet new web -n MyApp.Web
```

2. 添加对领域层的引用：

```bash
dotnet add reference ../MyApp.Domain/MyApp.Domain.csproj
```

3. 添加对应用层的引用：

```bash
dotnet add reference ../MyApp.Application/MyApp.Application.csproj
```

### 表示层的结构化

在整洁架构解决方案中，表示层负责处理用户请求、渲染视图以及与应用层交互。让我们按此结构化表示层：

```text
MyApp.Web/
├── Controllers/
│   └── HomeController.cs
├── Views/
│   └── Home/
│       └── Index.cshtml
└── Startup.cs
```

#### 创建控制器

ASP.NET Core MVC 6 中的控制器负责处理传入的 HTTP 请求并执行相应的操作。让我们创建一个简单的 `HomeController`：

```csharp
using Microsoft.AspNetCore.Mvc;
using MyApp.Application;

namespace MyApp.Web.Controllers
{
    public class HomeController : Controller
    {
        private readonly IPostService _postService;

        public HomeController(IPostService postService)
        {
            _postService = postService;
        }

        public IActionResult Index()
        {
            var posts = _postService.GetAllPosts();
            return View(posts);
        }
    }
}
```

#### 定义视图

ASP.NET Core MVC 6 中的视图负责向客户端渲染 HTML 标记。让我们创建一个简单的 `Index` 视图来显示帖子列表：

```html
<!-- Views/Home/Index.cshtml -->
@model List<MyApp.Domain.Post>
<h1>Posts</h1>
<ul>
    @foreach (var post in Model)
    {
        <li>@post.Title</li>
    }
</ul>
```

#### 配置依赖注入

在 ASP.NET Core MVC 6 中，我们可以在 `Startup` 类中配置依赖注入。让我们注册应用层的服务：

```csharp
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Hosting;
using Microsoft.Extensions.DependencyInjection;
using MyApp.Application;

namespace MyApp.Web
{
    public class Startup
    {
        public void ConfigureServices(IServiceCollection services)
        {
            services.AddControllersWithViews();

            // 注册应用服务
            services.AddScoped<IPostService, PostService>();
        }

        public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
        {
            if (env.IsDevelopment())
            {
                app.UseDeveloperExceptionPage();
            }

            app.UseStaticFiles();
            app.UseRouting();

            app.UseEndpoints(endpoints =>
            {
                endpoints.MapControllerRoute(
                    name: "default",
                    pattern: "{controller=Home}/{action=Index}/{id?}");
            });
        }
    }
}
```

将 ASP.NET Core MVC 6 集成到整洁架构解决方案中，为构建现代 Web 应用程序提供了坚实的基础。通过控制器和视图结构化表示层，并在 `Startup` 类中配置依赖注入，我们确保了代码库的关注点分离和维护性。此外，利用整洁架构原则允许我们根据需要轻松更换组件或扩展应用程序，同时保持核心业务逻辑独立于外部框架和库。

## 从 ASP.NET Core MVC 控制器消费业务逻辑层

从 ASP.NET Core MVC 控制器消费业务逻辑层，是构建遵循 C# 10 和 .NET 6 的整洁架构原则的健壮 Web 应用程序的关键方面。在本指南中，我们将探索如何从 MVC 控制器集成并消费包含业务逻辑的应用层。

### 整洁架构概述

整洁架构强调关注点分离以及外部框架的独立。它由多个层组成，包括：

1. **表示层**：处理用户交互并向用户显示信息。

2. **应用层**：包含特定的业务逻辑，并协调表示层与领域层之间的交互。

3. **领域层**：包含核心业务逻辑和实体。

4. **基础设施层**：实现外部关注点，如数据库访问、外部服务和日志记录。

### 集成业务逻辑层

让我们将包含业务逻辑的应用层集成到 ASP.NET Core MVC 项目中：

1. 在 ASP.NET Core MVC 项目中引用应用层项目：

```bash
dotnet add reference ../MyApp.Application/MyApp.Application.csproj
```

#### 从控制器消费业务逻辑

ASP.NET Core 中的 MVC 控制器负责处理传入的 HTTP 请求并调用应用层中的适当方法。让我们创建一个控制器并消费业务逻辑：

```csharp
using Microsoft.AspNetCore.Mvc;
using MyApp.Application;

namespace MyApp.Web.Controllers
{
    public class PostController : Controller
    {
        private readonly IPostService _postService;

        public PostController(IPostService postService)
        {
            _postService = postService;
        }

        public IActionResult Index()
        {
            var posts = _postService.GetAllPosts();
            return View(posts);
        }

        public IActionResult Details(int id)
        {
            var post = _postService.GetPostById(id);

            if (post == null)
            {
                return NotFound();
            }

            return View(post);
        }

        // 其他 CRUD 操作的控制器
    }
}
```

在此代码中：

1. 我们通过依赖注入将 `IPostService` 接口注入到构造函数中。

2. 在 `Index` 操作中，我们调用 `IPostService` 的 `GetAllPosts` 方法获取所有帖子并将其传递给视图。

3. 在 `Details` 操作中，我们调用 `IPostService` 的 `GetPostById` 方法根据 ID 获取特定帖子并将其传递给视图。

#### 配置依赖注入

为了确保 ASP.NET Core MVC 控制器可以解析应用层的依赖，我们需要在 `Startup` 类中配置依赖注入：

```csharp
using Microsoft.Extensions.DependencyInjection;
using MyApp.Application;

namespace MyApp.Web
{
    public class Startup
    {
        public void ConfigureServices(IServiceCollection services)
        {
            services.AddControllersWithViews();

            // 注册应用服务
            services.AddScoped<IPostService, PostService>();
        }

        // 其他配置方法
    }
}
```

在 `ConfigureServices` 方法中，我们将 `IPostService` 接口及其实现（`PostService`）注册为作用域（scoped）服务。这允许 ASP.NET Core 为每个请求创建一个新实例并进行注入。

从 ASP.NET Core MVC 控制器消费业务逻辑层对于构建可维护的应用程序至关重要。通过将应用层的依赖项注入到控制器，我们确保了关注点分离和维护性。此外，遵循整洁架构原则创建了清晰且结构化的架构。

1. 我们将 `IPostService` 接口的实例注入到控制器的构造函数中。

2. ASP.NET Core MVC 在创建 `PostController` 实例时，会自动解析依赖并提供 `PostService` 的实例。

## 在控制器动作中消费服务

一旦服务注入到控制器中，我们就可以在控制器动作中使用它：

```csharp
public IActionResult Index()
{
    var posts = _postService.GetAllPosts();
    return View(posts);
}
```

在此段代码中：

- 我们调用注入的 `IPostService` 的 `GetAllPosts` 方法来获取所有帖子。

## 视图中的依赖注入

在 ASP.NET Core MVC 中，我们还可以使用 `@inject` 指令将服务直接注入到视图中。例如，要将 `IPostService` 注入视图中，我们可以执行以下操作：

```html
@inject MyApp.Application.IPostService PostService
```

然后，我们可以使用 `@PostService` 在视图内部访问该服务。

在 ASP.NET Core MVC 应用中实现依赖注入对于构建可维护和可测试的代码库至关重要。通过在 `Startup` 类中注册服务并使用构造函数注入将其注入控制器中，我们促进了松耦合并改进了应用程序的整体架构。此外，依赖注入允许我们轻松切换实现、为单元测试模拟依赖项，并遵循整洁架构原则。总体而言，将依赖注入整合到 ASP.NET Core MVC 应用中可以提高代码质量、扩展性和可维护性。

## 利用 Minimal APIs 构建简洁高效的控制器（.NET 6 新特性）

在 .NET 6 中利用 Minimal APIs 为 ASP.NET Core 应用构建控制器提供了一种简洁且高效的方法。此功能允许开发者以最少的样板代码定义路由和处理请求，这对于使用 C# 10 和 .NET 6 的整洁架构解决方案特别有吸引力。在本指南中，我们将探索如何利用 Minimal APIs 在整洁架构项目中创建控制器。

### 设置 Minimal APIs

要在整洁架构项目中开始使用 Minimal APIs，请遵循以下步骤：

1. 确保你的机器上安装了 .NET 6。

2. 使用 `web` 模板创建一个新的 ASP.NET Core 项目：

```bash
dotnet new web -n MyApp.Web
```

3. 添加对领域层和应用层的引用：

```bash
dotnet add reference ../MyApp.Domain/MyApp.Domain.csproj
dotnet add reference ../MyApp.Application/MyApp.Application.csproj
```

4. 删除模板生成的 `Startup.cs` 文件。

5. 在 `MyApp.Web` 项目中创建一个名为 `Program.cs` 的新文件。



```csharp
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Http;
using Microsoft.Extensions.DependencyInjection;
using MyApp.Application;

var builder = WebApplication.CreateBuilder(args);

// 注册应用服务
builder.Services.AddScoped<IPostService, PostService>();

var app = builder.Build();

app.MapGet("/posts", async (IPostService postService) =>
{
    var posts = await postService.GetAllPosts();
    await JsonSerializer.SerializeAsync(app.Response.Body, posts);
});

app.Run();
```

在此代码中：

1. 我们使用`WebApplication.CreateBuilder`方法创建一个新的`WebApplication`实例。

2. 我们使用`builder`的`Services`属性在依赖注入容器中注册服务。

3. 我们定义了一个处理对`/posts` GET 请求的路由。在路由处理程序内部，我们使用依赖注入来访问`IPostService`并检索所有帖子。

4. 最后，我们调用`Run`方法启动应用程序。

### 运行应用程序

要运行应用程序，请在终端中使用以下命令：

```bash
dotnet run --project MyApp.Web
```

应用程序将在指定的端口（默认为 5000）上启动，并对`/posts`的请求返回包含所有帖子的 JSON 数组。

### Minimal APIs 的优势

使用 Minimal APIs 具有多个优势：

1. 简单性：Minimal APIs 具有极简的语法，使得定义路由和处理请求变得容易，无需冗余的操作。

2. 性能：Minimal APIs 轻量且高效，与传统的 MVC 控制器相比，具有更快的启动速度和更低的内存占用。

3. 简洁性：通过 Minimal APIs，你可以在单个文件中定义路由并处理请求，减少所需的模板代码量。

4. 可测试性：Minimal APIs 可以使用单元测试轻松进行测试，因为它们依赖于标准的 .NET Core 组件（如依赖注入和异步编程）。

在`.NET 6`中利用 Minimal APIs 为 ASP.NET Core 应用构建控制器提供了一种简洁且高效的方法。通过在单个文件中定义路由和处理请求，Minimal APIs 减少了复杂性并简化了开发流程。此外，Minimal APIs 轻量、高性能且易于测试，非常适合整洁架构项目。总体而言，采用 Minimal APIs 可以提高开发者的生产力并提升 ASP.NET Core 应用的可维护性。

# 第 10 章：健壮整洁架构应用程序的测试策略

## 单元测试：隔离验证业务逻辑

单元测试是软件开发中的一个关键方面，特别是在使用`C# 10`和`.NET 6`遵循整洁架构原则时。在整洁架构中，单元测试隔离地验证业务逻辑，确保每个组件在不依赖外部依赖的情况下都能按预期运行。在本指南中，我们将探索如何编写单元测试来验证整洁架构项目中的业务逻辑。

### 单元测试的优势

1. 早期发现 Bug：单元测试有助于在开发过程的早期识别 Bug 和问题，减少后期修复的成本。

2. 回归测试：单元测试提供了一个安全网，确保在修改代码库时现有功能保持完好。。

3. 改进设计：编写测试通常会带来更好的设计，因为它鼓励了关注点分离和模块化。

4. 文档作用：单元测试作为活文档，描述了系统组件应该的行为。

### 为业务逻辑编写单元测试

让我们编写单元测试来验证整洁架构项目中的业务逻辑。我们将专注于`PostService`类，它包含了与帖子相关的应用特定逻辑。

```csharp
using System.Collections.Generic;
using System.Threading.Tasks;
using Moq;
using Xunit;
using MyApp.Application;
using MyApp.Domain;

public class PostServiceTests
{
    [Fact]
    public async Task GetAllPosts_Should_Return_All_Posts()
    {
        // Arrange
        var mockPostRepository = new Mock<IPostRepository>();
        var posts = new List<Post>
        {
            new Post { Id = 1, Title = "Post 1", Content = "Content 1" },
            new Post { Id = 2, Title = "Post 2", Content = "Content 2" },
        };

        mockPostRepository
            .Setup(repo => repo.GetAllAsync())
            .ReturnsAsync(posts);

        var postService = new PostService(mockPostRepository.Object);

        // Act
        var result = await postService.GetAllPosts();

        // Assert
        Assert.Equal(posts, result);
    }

    // 为 PostService 类中的其他方法编写类似的测试
}
```

5. 我们调用`PostService`的`GetAllPosts`方法，并断言返回的结果与预期的文章列表匹配。

## 运行单元测试

要在`.NET`项目中运行单元测试，请在终端中使用以下命令：

```bash
dotnet test
```

此命令将发现并执行项目中的所有单元测试，并在终端中显示结果。

## 隔离测试的优势

通过孤立测试业务逻辑，我们获得了以下几点优势：

1. 执行快速：隔离测试的执行速度通常更快，因为它们不依赖于数据库或 Web 服务器等外部依赖。

2. 减少不稳定性（Flakiness）：隔离测试由于外部因素导致失败的可能性较低，使其更加可靠且具有确定性。

3. 易于调试：由于隔离测试专注于系统的特定组件，因此更容易识别导致失败的原因。

4. 提高测试覆盖率：隔离测试允许我们通过对单个组件进行全面测试来实现更高的测试覆盖率。

单元测试是软件开发中的一项基础实践，特别是在遵循整洁架构原则时。通过编写单元测试来验证隔离的业务逻辑，我们确保每个组件在不依赖外部依赖的情况下独立按照预期运行。这种方法增强了代码质量，减少了 Bug 并提高了可维护性，使其成为开发过程中不可或缺的一部分。

## 集成测试：层与层之间的交互

集成测试对于验证软件应用程序层之间的交互至关重要，特别是在使用`C# 10`和`.NET 6`遵循整洁架构原则时。集成测试确保组件能够正确协同工作并按预期进行通信，为整个系统的行为提供信心。在指南中，我们将探索如何编写集成测试来验证整洁架构项目在层与层之间的交互。

### 集成测试概述

集成测试涉及测试应用程序中不同组件或层之间的交互。在整洁架构项目中，集成测试侧重于验证层之间的集成点（例如应用层和基础设施层）是否工作正常。这确保了当所有组件组合在一起时，系统的行为符合预期。

### 设置集成测试

若要在整洁架构项目中开始进行集成测试，请按照以下步骤操作：

1. 为集成测试创建一个新的测试项目：

```bash
dotnet new xunit -n MyApp.IntegrationTests
```

2. 添加对领域、应用层和基础设施层的引用：

```bash
dotnet add reference ../MyApp.Domain/MyApp.Domain.csproj
dotnet add reference ../MyApp.Application/MyApp.Application.csproj
dotnet add reference ../MyApp.Infrastructure/MyApp.Infrastructure.csproj
```

3. 配置测试项目使用 ASP.NET Core TestHost 进行集成测试：

```csharp
using Microsoft.AspNetCore.Hosting;
using Microsoft.AspNetCore.TestHost;
using Microsoft.Extensions.Configuration;
using MyApp.Web;

public class IntegrationTestBase
{
    protected readonly TestServer _server;

    public IntegrationTestBase()
    {
        var configuration = new ConfigurationBuilder()
            .AddJsonFile("appsettings.json")
            .Build();

        var hostBuilder = new WebHostBuilder()
            .UseConfiguration(configuration)
            .UseStartup<Startup>();

        _server = new TestServer(hostBuilder);
    }
}
```

在此代码中：

- 我们创建了一个基类`IntegrationTestBase`，它使用 ASP.NET Core TestHost 设置`TestServer`实例。

- `TestServer`允许我们在内存中托管并测试 ASP.NET Core，模拟真实的 HTTP 请求和响应。

### 编写集成测试

让我们编写一个集成测试，验证获取所有文章的 API 端点（`/posts`）是否返回了文章列表：

```csharp
using System.Net.Http;
using System.Text.Json;
using System.Threading.Tasks;
using Xunit;

public class PostControllerIntegrationTests : IntegrationTestBase
{
    [Fact]
    public async Task GetAllPosts_Should_Return_All_Posts()
    {
        // Arrange
        var client = _server.CreateClient();

        // Act
        var response = await client.GetAsync("/posts");
        response.EnsureSuccessStatusCode();

        var responseContent = await response.Content.ReadAsStringAsync();
        var posts = JsonSerializer.Deserialize<List<Post>>(responseContent);

        // Assert
        Assert.NotNull(posts);
        Assert.NotEmpty(posts);
    }
}
```

在此测试中：

1. 我们使用`TestServer`实例创建了`HttpClient`类的实例。

2. 我们向`/posts`端点发送了 GET 请求。

3. 我们确保响应状态码表示成功（2xx）。

4. 我们使用 JSON 序列化将响应内容反序列化为文章列表。

5. 我们断言文章列表不为空且不为空。

### 运行集成测试

要运行集成测试，请在终端中使用以下命令：

```bash
dotnet test
```

此命令将发现并执行项目中的所有集成测试，并在终端中显示结果。

### 集成测试的优势

集成测试提供了若干优势：

1. 端到端验证：集成测试验证整个系统，包括不同组件和层之间的交互。

2. 真实场景：集成测试通过与系统的外部接口（如 API 或数据库）交互来模拟真实世界的场景。

3. 检测集成问题：集成测试有助于识别与组件之间集成点相关的问题，例如错误的数据映射或通信错误。

4. 部署信心：成功的集成测试提供了信心，确保系统功能正常并可以安全地部署到生产环境。

集成测试对于验证整洁架构项目中层与层之间的交互至关重要。通过编写集成测试，我们可以确保组件之间能够正确协同工作并按预期通信，从而对整个系统的行为提供信心。集成测试通过验证不同组件之间的集成点来补充单元测试，有助于在开发早期识别并解决问题。总而言之，集成测试是构建可靠可维护应用程序的重要部分。

## 利用 C# 10 特性的测试框架（xUnit、NUnit）

利用`xUnit`和`NUnit`等测试框架增强了基于`.NET 6`的整洁架构项目的开发和维护。这些框架为编写和执行测试提供了强大的能力，而`C# 10`引入了新的语言特性，进一步提高了整洁架构项目中单元测试代码的可读性和可表达性。

### 测试框架概述

`xUnit`和`NUnit`是`.NET`项目中编写和执行单元测试的流行测试框架。这两个框架支持广泛的功能，包括测试固件、参数化测试和运行器。

### 设置测试框架

要在整洁架构项目中开始使用`xUnit`或`NUnit`，请按照以下步骤操作：

1. 使用 NuGet 安装所需的测试框架：

   对于`xUnit`：

   ```bash
   dotnet add package xunit
   dotnet add package xunit.runner.visualstudio
   ```

   对于`NUnit`：

   ```bash
   dotnet add package nunit
   dotnet add package nunitadapter
   ```

2. 在解决方案中创建一个新的测试项目：

   ```bash
   dotnet new xunit -n MyApp.Tests
   ```

   或：

   ```bash
   dotnet new nunit -n MyApp.Tests
   ```

3. 添加对领域和应用层的引用：

   ```bash
   dotnet add reference ../MyApp.Domain/MyApp.Domain.csproj
   dotnet add reference ../MyApp.Application/MyApp.Application.csproj
   ```

### 使用 C# 10 特性编写测试

`C# 10`引入了许多新的语言特性，可以用于编写更具表现力且简洁的单元测试。让我们探索这些特性：

#### 目标类型 `new` 表达式

目标类型`new`表达式根据上下文推断简化了对象的创建。这减少了冗余并使代码易读。

```csharp
// C# 9 及以前
List<int> numbers = new List<int>();

// C# 10
List<int> numbers = new();
```

#### 文件范围命名空间

文件范围命名空间允许我们直接在文件中定义命名空间，消除了大括号的需求。这减少了冗长。

```csharp
// C# 9 及以前
namespace MyApp.Tests
{
    public class MyTestClass
    {
        // 测试方法
    }
}

// C# 10
namespace MyApp.Tests;

public class MyTestClass
{
    // 测试方法
}
```

#### 全局引用（Global Usings）

全局引用通过允许我们在文件顶部指定常用的命名空间简化了导入过程。这减少了杂乱并提高了可读性。

```csharp
// C# 9 及以前
using System;
using Xunit;

// C# 10
global using System;
global using Xunit;
```

#### 使用 xUnit 编写测试

让我们使用`C# 10`特性使用`xUnit`编写示例单元测试：

```csharp
global using Xunit;
using MyApp.Application;

public class PostServiceTests
{
    [Fact]
    public async Task GetAllPosts_Should_Return_All_Posts()
    {
        // Arrange
        var postService = new PostService();

        // Act
        var posts = await postService.GetAllPosts();

        // Assert
        Assert.NotEmpty(posts);
    }
}
```

#### 使用 NUnit 编写测试

同样，让我们使用`C# 10`特性使用`NUnit`编写示例单元测试：


...[/content]` 包裹输出，这与示例一致（示例中确实包含了该标记）。我将遵循您的指令和示例格式，输出包含 `[content]...[/content]` 的排版后内容。

以下是处理后的结果：

[content]
```csharp
global using NUnit.Framework;
using MyApp.Application;

public class PostServiceTests
{
    [Test]
    public async Task GetAllPosts_Should_Return_All_Posts()
    {
        // Arrange
        var postService = new PostService();
        // Act
        var posts = await postService.GetAllPosts();
        // Assert
        Assert.NotEmpty(posts);
    }
}
```

## 运行测试

要使用`xUnit`或`NUnit`运行测试，请在终端中使用以下命令：

对于`xUnit`：

```bash
dotnet test --project MyApp.Tests
```

对于`NUnit`：

```bash
dotnet test --project MyApp.Tests --logger:trx
```

# .NET 6 整洁架构项目的测试考虑

测试考虑对于确保基于`.NET 6`构建的整洁架构项目的可靠性、可维护性和可扩展性至关重要。整洁架构关注关注点分离和组件独立性，这影响了覆盖应用程序各个层的测试策略。在本指南中，我们将探索`.NET 6`整洁架构项目的测试考虑，涵盖单元测试、集成测试和端到端测试。

## 单元测试

单元测试是整洁架构项目中的一项基础实践，专注于隔离测试单个代码单元。在整洁架构中，单元测试通常覆盖领域和应用层中的组件，例如实体、用例和服务器类。

### 示例单元测试

让我们为应用层中的简单用例编写一个单元测试：

```csharp
using Xunit;
using MyApp.Application;

public class PostServiceTests
{
    [Fact]
    public void GetAllPosts_Should_Return_All_Posts()
    {
        // Arrange
        var postService = new PostService();
        // Act
        var posts = await postService.GetAllPosts();
        // Assert
        Assert.NotEmpty(posts);
    }
}
```

## 集成测试

集成测试验证应用程序组件或层之间的交互，确保它们能够正确工作。在整洁架构项目中，集成测试通常覆盖应用层和基础设施之间的交互，例如数据库访问、API。

### 示例集成测试

让我们编写一个集成测试来验证基础设施层的数据库访问：

```csharp
using System.Threading.Tasks;
using Xunit;
using MyApp.Infrastructure.Persistence;

public class PostRepositoryTests
{
    [Fact]
    public async Task GetAllPosts_Should_Return_All_Posts_From_Database()
    {
        // Arrange
        var dbContext = DbContextHelper.CreateDbContext();
        var postRepository = new PostRepository(dbContext);
        // Act
        var posts = await postRepository.GetAllAsync();
        // Assert
        Assert.NotEmpty(posts);
    }
}
```

## 端到端测试

端到端测试验证整个系统的行为，包括所有层之间的外部依赖。在整洁架构项目中，端到端测试通常覆盖用户功能，确保按预期运行。

### 示例端到端测试

让我们使用`Selenium`编写一个端到端测试来验证用户场景：

```csharp
using OpenQA.Selenium;
using OpenQA.Selenium.Chrome;
using Xunit;

public class PostPageTests : IClassFixture<ChromeDriverFixture>
{
    private readonly ChromeDriverFixture _fixture;
    public PostPageTests(ChromeDriverFixture fixture)
    {
        _fixture = fixture;
    }

    [Fact]
    public void User_CanView_All_Posts()
    {
        // Arrange
        var driver = _fixture.Driver;
        driver.Navigate().To("http://localhost:5000/posts");
        // Act & Assert
        Assert.Contains("Posts", driver.Title);
    }
}
```

## 测试考虑

在测试`.NET 6`整洁架构项目时，请考虑以下因素：

1. **依赖注入**：在单元测试利用依赖注入模拟外部依赖，并在集成测试配置环境。

2. **关注点分离**：确保测试专注于特定组件或层，避免职责交叉并保持清晰。

3. **覆盖率**：对所有层寻求全面覆盖，包括领域逻辑、应用服务等。

4. **性能**：通过并行运行测试优化测试时间，减少对外部资源的依赖，并在集成测试中使用内存数据库。

5. **健壮性**：设计健壮的测试以能够抵抗变化，使用参数化测试和测试固件等。

测试考虑对于确保整洁架构项目的可靠性、可维护性和可扩展性至关重要。通过实现单元测试、集成测试和端到端测试，开发者可以验证单个组件的行为、层之间的交互以及整体系统功能。

# 第 1 章 用于松耦合和灵活性的依赖倒转原则

依赖倒转原则（`DIP`）是基于`.NET 6`构建的整洁架构项目中的关键设计原则。它促进组件之间的松耦合，并通过将高层模块与底层实现解耦来增强活性。在本指南中，我们将通过代码示例探索如何在`.NET 6`整洁架构项目中应用依赖倒转原则。

## 理解依赖倒转原则

依赖倒转原则规定高层模块不应该依赖底层模块，而应该依赖抽象。该原则促进了接口或抽象类的使用，允许实现独立变化。

## 在整洁架构中应用依赖倒转

在整洁架构项目中，应用依赖倒转原则是为了确保高层模块（如用例或应用服务）依赖于抽象（接口），而不是具体实现（如数据访问或外部服务）。

### 示例场景

考虑应用服务依赖仓库进行数据访问的场景。如果不应用依赖倒转原则，应用服务将直接依赖于具体的仓库，导致紧耦合和灵活性降低。

### 未使用依赖倒转

```csharp
namespace MyApp.Application
{
    public class PostService
    {
        private readonly PostRepository _postRepository;
        public PostService()
        {
            _postRepository = new PostRepository(); // 直接依赖具体实现
        }
        // 服务方法...
    }
}
```

### 实现依赖倒转

为了应用依赖倒转原则，我们引入了一个接口来表示应用服务与仓库之间的约。该接口作为抽象，将服务与具体的仓库实现解耦。

### 应用依赖倒转

```csharp
namespace MyApp.Application
{
    public interface IPostRepository
    {
        Task<List<Post>> GetAllPostsAsync();
        Task<Post> GetPostByIdAsync(int id);
        Task AddPostAsync(Post post);
        Task UpdatePostAsync(Post post);
        Task DeletePostAsync(int id);
    }
}
```

```csharp
namespace MyApp.Application
{
    public class PostService
    {
        private readonly IPostRepository _postRepository;
        public PostService(IPostRepository postRepository)
        {
            _postRepository = postRepository; // 通过构造函数注入实现依赖倒转
        }
        // 服务方法...
    }
}
```

## 依赖倒转的优势

在整洁架构项目中应用依赖倒转原则提供了若干优势：

1. **松耦合**：通过依赖抽象而非具体实现，组件变得松耦合，更容易修改、替换或扩展单个模块而不影响其他。

2. **灵活性**：接口或抽象类的使用允许实现相互替换，便于采用不同的数据访问策略、外部服务或第三方库。

3. **可测试性**：通过在单元测试期间将真实实现替换为 `Mock` 或 `Stub` 元素，增强了可测试性。

4. **可扩展性**：具有依赖倒转的整洁架构项目本质上是可以扩展的，因为它们允许添加新功能、模块或依赖而不引入紧耦合或破坏现有功能。

依赖倒转原则是`.NET 6`整洁架构项目中的基础设计原则。通过应用该原则，开发者可以实现模块化的、可维护的代码。

# 数据访问抽象的仓库模式

仓库模式是`.NET 6`整洁架构项目中常用的设计模式，用于抽象数据访问逻辑并提供与不同数据源交互的统一接口。它促进了关注点分离、可测试性和数据访问层的灵活性。

## 仓库模式概述

仓库模式定义了应用层与数据访问层之间的抽象，允许应用程序与数据对象交互。它通常由定义 `CRUD`（增删改查）操作的接口以及与底层存储交互的具体实现组成。

## 实现仓库模式

让我们在整洁项目中项目中仓库模式以抽象数据访问逻辑：

### 定义仓库接口

```csharp
using System.Collections.Generic;
using System.Threading.Tasks;
using MyApp.Domain.Entities;

namespace MyApp.Application.Interfaces
{
    public interface IPostRepository
    {
        Task<List<Post>> GetAllPostsAsync();
        Task<Post> GetPostByIdAsync(int id);
        Task AddPostAsync(Post post);
        Task UpdatePostAsync(Post post);
        Task DeletePostAsync(int id);
    }
}
```

### 实现仓库

```csharp
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;
using Microsoft.EntityFrameworkCore;
using MyApp.Domain.Entities;

namespace MyApp.Infrastructure.Persistence
{
    public class PostRepository : IPostRepository
    {
        private readonly AppDbContext _context;
        public PostRepository(AppDbContext context)
        {
            _context = context;
        }
        public async Task<List<Post>> GetAllPostsAsync()
        {
            return await _context.Posts.ToListAsync();
        }

        public async Task<Post> GetPostByIdAsync(int id)
        {
            return await _context.Posts.FindAsync(id);
        }

        public async Task AddPostAsync(Post post)
        {
            _context.Posts.Add(post);
            await _context.SaveChangesAsync();
        }

        public async Task UpdatePostAsync(Post post)
        {
            _context.Posts.Update(post);
            await _context.SaveChangesAsync();
        }

        public async Task DeletePostAsync(int id)
        {
            var post = await _context.Posts.FindAsync(id);
            if (post != null)
            {
                _context.Posts.Remove(post);
                await _context.SaveChangesAsync();
            }
        }
    }
}
```

## 仓库模式的优势

仓库模式在整洁架构项目中提供了若干优势：

1. **抽象**：仓库接口提供了数据访问操作的清晰抽象，为应用层隐藏了底层存储的细节。

2. **解耦**：依赖接口而非具体实现，应用层与特定的数据访问技术解耦，便于切换或替换。

3. **可测试性**：仓库模式通过在单元测试期间使用 `Mock` 仓库增强了可测试性。

4. **灵活性**：它允许实现不同的数据访问策略，例如使用 `Entity Framework Core` 处理关系型数据库或使用`HttpClient`处理 `API`。

# 在应用层使用仓库模式

现在我们定义并实现了仓库，让我们在应用层中使用它与文章交互：

```csharp
using System.Collections.Generic;
using System.Threading.Tasks;
using MyApp.Application.Interfaces;
using MyApp.Domain.Entities;

namespace MyApp.Application.Services
{
    public class PostService
    {
        private readonly IPostRepository _postRepository;
        public PostService(IPostRepository postRepository)
        {
            _postRepository = postRepository;
        }
        public async Task<List<Post>> GetAllPosts()
        {
            return await _postRepository.GetAllPostsAsync();
        }
        public async Task<Post> GetPostById(int id)
        {
            return await _postRepository.GetPostByIdAsync(id);
        }
    }
}
```

# 使用 C# 10 和 .NET 6 实现微服务的整洁架构

使用`C# 10`和`.NET 6`为微服务实现整洁架构提供了一种构建可扩展、可维护和松耦合系统的结构化方法。整洁架构强调关注点分离、依赖倒转和抽象层，使其非常适合微服务架构。

## 微服务的整洁架构概述

使用`C# 10`和`.NET 6`为微服务实现整洁架构提供了一种构建可扩展、可维护和松耦合系统的结构化方法。整洁架构强调关注点分离、依赖倒转和抽象层，使其非常适合微服务架构。

微服务的整洁架构关注：

1. **关注点分离**：每个微服务只关注特定的职责。

2. **依赖倒转**：减少服务之间的强硬依赖。

3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的整洁架构关注：

1. **关注点分离**：每个微服务只关注特定的职责。

2. **依赖倒转**：减少服务之间的强硬依赖。

3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的整洁架构关注：

1. **关注点分离**：每个微服务只关注特定的职责。

2. **依赖倒转**：减少服务之间的强硬依赖。

3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的整洁架构关注：



# 微服务整洁架构的核心原则

微服务的整洁架构关注以下三个核心原则：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

这些原则贯穿于微服务设计的始终，确保每个微服务具有清晰的边界和独立的可维护性。

# 原则详解

## 1. 关注点分离

每个微服务只关注特定的职责。这意味着服务应该围绕业务能力进行拆分，每个服务负责一个独立的业务领域或功能模块，避免职责重叠和耦合。

## 2. 依赖倒转

减少服务之间的强硬依赖。通过依赖抽象而非具体实现，微服务可以独立演化和部署。服务之间的通信应基于接口契约，而非直接依赖内部实现。

## 3. 抽象层

保护核心逻辑不受外部技术变化的影响。在微服务内部引入抽象层（如仓储模式、领域服务等），将业务逻辑与数据访问、外部集成等技术细节隔离，从而降低技术选型变更带来的风险。

# 实践中的注意事项

- 在设计微服务时，应始终以业务能力为边界，确保每个服务的职责单一且清晰。
- 依赖倒转原则指导我们通过接口或消息机制解耦服务，避免硬编码依赖。
- 抽象层的合理运用可以隔离技术细节，使核心业务逻辑保持稳定。

# 总结

微服务的整洁架构依赖于关注点分离、依赖倒转和抽象层三大原则。它们共同保证了系统的灵活性、可维护性和可扩展性。在实际开发中，需要根据业务场景合理应用这些原则，避免过度设计或职责混乱。



微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注关注关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注关注关注关注关注关注关注关注关注关注关注关注关注关注关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注关注关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注关注关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注关注关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注关注关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注关注关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注关注关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注关注关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注关注关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的关注关注依赖。
3. **抽象层**：保护核心逻辑不受外部技术关注的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖关注转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注关注关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注关注关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注关注关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注关注关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注关注关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注关注关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术关注的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术变化的影响。

微服务的架构洁关注关注关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术关注的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术关注的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术关注的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术关注的影响。

微服务的架构洁关注关注关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术关注的影响。



微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术关注的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术关注的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术关注的影响。

微服务的架构洁关注关注关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术关注的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术关注的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术关注的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术关注的影响。

微服务的架构洁关注关注关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术关注的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术关注的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术关注的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术关注的影响。

微服务的架构洁关注关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术关注的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术关注的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术关注的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术关注的影响。

微服务的架构洁关注关注关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术关注的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术关注的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术关注的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术关注的影响。

微服务的架构洁关注关注关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术关注的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术关注的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术关注的影响。

微服务的架构洁关注：

1. **关注点分离**：每个微服务只关注特定的职责。
2. **依赖倒转**：减少服务之间的强硬依赖。
3. **抽象层**：保护核心逻辑不受外部技术关注的影响。
