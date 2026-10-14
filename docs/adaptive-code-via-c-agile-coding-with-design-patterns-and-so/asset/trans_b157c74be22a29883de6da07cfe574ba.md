

![](img/65c1bad7a6b3cffae8cbb79664f0708b_105_0.png)

FIGURE 2-23 The third layer contains processing or business logic for the application.

再次，逻辑层与数据访问层类似，为客户端提供接口和实现程序集，以避免抽象泄漏。

Note
尽管三层架构对于 Web 应用程序非常常见，但它通常仅部署在两个层中。一个节点处理数据库，另一个节点处理几乎所有其他内容：用户界面、逻辑，甚至部分数据访问。

## Business logic

业务逻辑层的职责是：

- 处理来自用户界面层的命令。
- 对业务域进行建模以捕获业务流程、规则和工作流。

逻辑层可能是接收来自用户界面层的用户命令的命令处理器，并通过与数据访问层协作来解决特定问题或执行特定任务。它也可以是一个完全开发的领域模型，旨在将企业的流程映射到软件中。对于后者，数据访问层通常包含一个对象/关系映射组件，以便逻辑层可以直接实现到类中，可能使用领域驱动设计（DDD）。在领域模型中，不应存在进一步向下堆栈或通过某些特定于实现的技术的依赖。例如，领域模型的程序集不应依赖于对象/关系映射库。相反，应创建单独的映射程序集，该程序集特定于实现并指示 ORM 如何映射到领域模型。这允许领域模型的核心类在不依赖 ORM 的情况下被重用，并且可以在不影响领域模型或其客户端的情况下替换 ORM。图 2-24 显示了使用领域模型的逻辑层的一种可能实现。

![](img/65c1bad7a6b3cffae8cbb79664f0708b_106_0.png)

FIGURE 2-24 How the assemblies of a domain model collaborate to form a logic layer.

添加逻辑层是必要的，当应用程序中存在复杂逻辑时，例如旨在反映人们工作真实工作流程的业务规则。即使逻辑并不特别复杂但经常发生变化，这也是引入单独层来封装此行为的一个很好的论据。它简化了用户界面和数据访问层，使其能够完全专注于其唯一目的。

## Cross-cutting concerns

有时组件的职责并不容易限制在单个层中。诸如审计、安全和缓存之类的功能可以渗透整个应用程序，因为它们适用于每一层。例如，在应用程序已部署且无法附加 Visual Studio 调试器逐步执行代码时，跟踪每次方法调用和返回的代码操作是一个有用的调试工具。你可以手动生成参数值在传递过程中的输出，以及各种方法的返回值，如清单 2-23 所示。

## LISTING 2-23 Manually applying cross-cutting concerns quickly swamps the real intent of the code.

Click here to view code image

```
public void OpenNewAccount(Guid ownerID, string accountName, decimal openingBalance)
{
    log.WriteInfo("Creating new account for owner {0} with name '{1}' and an opening balance of {2}", ownerID, accountName, openingBalance);

    using(var transaction = session.BeginTransaction())
    {
        var user = userRepository.GetByID(ownerID);
        user.CreateAccount(accountName);
        var account = user.FindAccount(accountName);
        account.SetBalance(openingBalance);

        transaction.Commit();
    }
}
```

这很费力且容易出错，并且会立即用无关的样板代码污染每个方法，增加噪声与信号的比例。相反，你可以将此类横切关注点分解为封装的功能，并以侵入性更小的方式将其应用于代码。添加功能最常见且非侵入性的方式是通过面向方面的编程。

## Aspects

面向方面编程（AOP）是将横切关注点——或方面——应用于代码中多个层的应用。.NET Framework 有多个可供选择的 AOP 库（在 NuGet 中搜索 AOP），但这里给出的示例是针对 PostSharp 的，它有一个免费的 Express 版本，但功能有所减少。清单 2-24 显示了跟踪代码被分解为 PostSharp 方面并作为属性应用于某些方法。

## LISTING 2-24 Aspects are a great way to implement cross-cutting concerns.

Click here to view code image

```
[Logged]
[Transactional]
public void OpenNewAccount(Guid ownerID, string accountName, decimal openingBalance)
{
    var user = userRepository.GetByID(ownerID);
    user.CreateAccount(accountName);
    var account = user.FindAccount(accountName);
    account.SetBalance(openingBalance);
}
```

装饰 OpenNewAccount 方法的两个属性提供了与清单 2-23 中所示相同的功能，但该方法的意图更清晰。Logged 属性将有关方法调用的信息写入日志，包括参数值。Transactional 属性将方法包装在数据库事务中，并在成功时提交事务，在失败时回滚事务。关键在于，这两个属性足够通用，可以应用于任何方法，而不仅仅是此方法，因此可以多次重用。

## Asymmetric layering

应用程序的所有用户请求都通过提供的用户界面发生。然而，请求之后遵循的路径不一定总是相同的。分层可能是不对称的，这取决于所做请求的类型。这是由需要务实并考虑当前分层对于某些请求是否过度设计或对于某些请求是否不足所驱动的。

在过去几年中迅速流行起来的不对称分层模式是命令/查询职责分离（CQRS）。在讨论 CQRS 之前，该模式是一个架构模式，需要对其方法级影响因素——命令/查询分离——有一个基础。

## Command/query separation

Bertrand Meyer 在他的书《面向对象软件构造》（Prentice Hall，1997）中，使用了命令/查询分离（CQS）这一短语来解释所有对象方法应仅为两种事物之一：命令或查询。

命令是对行动的强制性调用，要求代码执行某些操作。这些方法允许更改系统的状态，但不应同时返回一个值。清单 2-25 显示了 CQS 合规的命令方法示例，后跟一个不合规的示例。

## LISTING 2-25 CQS-compliant and non-CQS-compliant command methods.

Click here to view code image

```
// Compliant command
Public void SaveUser(string name)
{
    session.Save(new User(name));
}
// Non-compliant command
public User SaveUser(string name)
{
    var user = new User(name);
    session.Save(user);
    return user;
}
```

查询是请求数据，要求代码获取某些内容。这些方法向调用客户端返回数据，但不应同时更改系统的状态。清单 2-26 显示了 CQS 合规的查询方法示例，后跟一个不合规的示例。

## LISTING 2-26 CQS-compliant and non-CQS-compliant query methods.

Click here to view code image

```
// Compliant query
Public IEnumerable<User> FindUserByID(Guid userID)
{
    return session.Get<User>(userID);
}
// Non-compliant query
public IEnumerable<User> FindUserByID(Guid userID)
{
    var user = session.Get<User>(userID);
    user.LastAccessed = DateTime.Now;
    return user;
}
```

因此，命令和查询通过返回值的存在与否来区分。如果方法返回一个值（并且符合 CQS），你可以安全地假设它不会更改对象的任何状态。优势在于，你可以重新排序查询调用，而知道它们对对象没有其他影响。方法没有返回值（并且符合 CQS）表示你可以假设它确实会更改对象的状态。对于这些调用，你在调用顺序上必须更加谨慎。

## Command/Query Responsibility Segregation

命令/查询职责分离模式归功于 Greg Young。该模式是在架构级别应用 CQS，并且是不对称分层的示例。命令和查询遵循与 CQS 相同的规则，但 CQRS 更进一步：它承认命令和查询可能需要通过分层遵循不同的路径才能得到最佳处理。

最小 CQRS 可以应用的一个例子是，当你使用领域模型开发三层架构时。在这种情况下，领域模型仅由应用程序的命令侧使用，而查询侧使用更简单的两层架构。图 2-25 举例说明了这种设计。

