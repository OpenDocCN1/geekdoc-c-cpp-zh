
```
}

public EntityNotFoundException(string message)
    : base(message)
{

}
}
//...
public class UserNotFoundException : Exception
{
    public UserNotFoundException()
        : base()
    {

    }

    public UserNotFoundException(string message)
        : base(message)
    {

    }
}
```

相反，为了能用一个 catch 块同时捕获 EntityNotFoundException 和 UserNotFoundException，你只能求助于捕获通用的 Exception，而这是不推荐的做法。

在取自 EntityRepository 和 UserRepository 类的代码中，这个问题会更加严重，如清单 7-28 所示。

## 清单 7-28 接口的两种不同实现可能会抛出不同类型的异常。

单击此处查看代码图片

```
public Entity GetByID(Guid id)
{
    Contract.Requires<EntityNotFoundException>(id != Guid.Empty);

    return new Entity();
}
//...
public User GetByID(Guid id)
{
    Contract.Requires<UserNotFoundException>(id != Guid.Empty);

    return new User();
}
```

这两个类都使用代码契约来断言一个前置条件：所提供的 id 参数不能等于 Guid.Empty。如果契约被违反，它们各自会使用自己的异常类型。请思考一下，这对使用该仓库的客户端会产生什么影响。客户端需要捕获这两种异常，而且无法在不求助于捕获 Exception 类型的情况下，使用单个 catch 块同时针对这两种异常。清单 7-29 展示了一个单元测试，该测试是这两个仓库的客户端。

## 清单 7-29 此单元测试将会失败，因为 UserNotFoundException 不能赋给 EntityNotFoundException。

单击此处查看代码图片

```
[TestFixture(typeof(EntityRepository), typeof(Entity))]
[TestFixture(typeof(UserRepository), typeof(User))]
public class ExceptionRuleTests<TRepository, TEntity>
    where TRepository : IEntityRepository<TEntity>, new()
{
    [Test]
    public void GetByIDThrowsEntityNotFoundException()
    {
        var repo = new TRepository();
        Action getByID = () => repo.GetByID(Guid.Empty);

        getByID.ShouldThrow<EntityNotFoundException>();
    }
}
```

这个单元测试之所以失败，是因为 UserRepository 没有按要求抛出 EntityNotFoundException。如果 UserNotFoundException 是 EntityNotFoundException 类型的子类，该测试就会通过，而且单个 catch 块也能保证捕获这两种异常。

这就变成了客户端的维护问题。如果客户端将接口作为依赖项并使用，并调用该接口上的方法，它就不应该知道该接口背后的任何类的信息。这又回到了关于 Entourage 反模式与 Stairway 模式的讨论。如果引入了不属于预期异常类层次结构的新异常，客户端就必须开始直接引用这些异常。而且——更糟的是——每当引入新的异常类型时，客户端都必须随之更新。

相反，重要的是每个接口都应有一个统一的基类异常，将关于错误的必要信息从异常报告者传递给异常处理器。

## 小结

从表面上看，里氏替换原则是 SOLID 原则中较为复杂的方面之一。它要求具备契约与变体的基础知识，才能构建出引导你编写更具适应性代码的规则。

默认情况下，接口不会向客户端传达前置条件或后置条件的规则。创建在运行时终止应用程序的守卫子句，会进一步缩小参数允许的有效值范围。LSP 提供了指导原则，使得类层次结构中的每个子类都不能强化前置条件或弱化后置条件。

类似地，LSP 也为子类型中的变体提出了规则：子类型中的方法参数应当逆变，子类型中的返回值应当协变。此外，任何新引入的异常——也许是在创建新的接口实现时引入的——都应继承自现有的基类异常。否则，就可能使现有客户端错过 catch——实际上就是漏掉异常，并让它导致应用程序崩溃。

如果针对这些规则违反了 LSP，客户端就更难对类层次结构中的所有类型一视同仁。理想情况下，客户端应能持有对基类型或接口的引用，并且不会根据运行时实际使用的具体子类来改变自身行为。这种混杂的关注点会在最好保持分离的代码部分之间制造依赖。任何对 LSP 的违反都应被视为技术债务，而且正如前几章所示，这笔债务应当尽快偿还，而不是拖到以后。

## 第 8 章 接口隔离

完成本章学习后，你将能够：

- 理解接口隔离的重要性。
- 以客户端代码的需求为首要关注点来编写接口。
- 创建更小、目的更明确的接口。
- 识别可以使用接口隔离的场景。
- 根据其实现的依赖关系来拆分接口。

如前几章所述，接口是现代面向对象程序员工具箱中的关键工具。接口代表了客户端代码的需求与该需求被实现的方式之间的边界。接口隔离原则指出，接口应当保持小型化。

接口的每个成员都需要被完整地实现：属性、事件和方法。除非接口的每个客户端都需要每个成员，否则要求每个实现都履行如此庞大的契约是没有意义的。考虑到单一职责原则以及开发者如何自由地使用装饰器模式，对于接口中存在的每个成员，都需要有一个有效的对应物，以便为其实现装饰。

在最简单的情况下，接口包含服务于单一用途的单个方法。在这种粒度级别上，它们类似于委托，但拥有许多额外的好处。

## 一个隔离示例

本章将完成一个完整的示例，从单一的整体式接口逐步演进到多个更小的接口。在此过程中，将创建各种装饰器，以详细阐述广泛使用接口隔离所带来的一个关键好处。

## 一个简单的 CRUD 接口

这个接口本身非常简单，只有五个方法。它用于允许客户端通过传统的 CRUD 操作与实体的持久化存储进行交互。CRUD 代表创建（create）、读取（read）、更新（update）和删除（delete）。这些都是客户端为维护实体的持久化存储而需要的常见操作。图 8-1 显示了一个 UML 类图，说明了 ICreateReadUpdateDelete 接口可用的操作。

![](img/65c1bad7a6b3cffae8cbb79664f0708b_279_0.png)

## 图 8-1 隔离之前的初始接口。

读取操作被拆分为两个方法：一个用于从存储中检索单条记录，另一个用于读取所有记录。在代码中，该接口如清单 8-1 所示。

## 清单 8-1 用于对实体进行 CRUD 操作的简单接口。

单击此处查看代码图片

```
public interface ICreateReadUpdateDelete<TEntity>
{
    void Create(TEntity entity);

    TEntity ReadOne(Guid identity);

    IEnumerable<TEntity> ReadAll();

    void Update(TEntity entity);

    void Delete(TEntity entity);
}
```

ICreateReadUpdateDelete 接口是泛型的，允许在不同的实体类型之间复用。然而，通过让接口成为泛型，而不是让每个单独的方法成为泛型，你迫使客户端预先声明要处理的是哪个 TEntity，从而明确了其依赖关系。如果客户端想对多个实体执行 CRUD 操作，就必须请求多个 ICreateReadUpdateDelete<TEntity> 实例，每种实体类型一个。

### 注意

尽管客户端每个实体都需要一个 ICreateReadUpdateDelete<TEntity> 实例，但仍然可以只有一个 ICreateReadUpdateDelete<TEntity> 实现，它就能满足所有具体的 TEntity 类型。这个实现也应当是泛型的。

每个 ICreateReadUpdateDelete 的实现都要执行 CRUD 的每一项操作
