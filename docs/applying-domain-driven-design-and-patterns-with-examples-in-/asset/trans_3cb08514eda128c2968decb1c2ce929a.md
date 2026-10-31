

### 在其他测试中的重用机会

你在开发过程中编写的测试在集成测试中也会派上用场。根据我的经验，许多生产环境中的问题都是由生产环境与预期之间的差异引起的。如果你有一套全面的测试，你也可以用它们来检查已完成应用程序的部署。你只需付出一次，却能多次收获好处。

总而言之，测试友好的设计（即可测试性）是当今一个非常重要的设计目标。当你做出设计选择时，它或许是主要因素。

### 问题

我听起来像推销员已经有一阵子了。然而，也存在问题。让我们看看下面这些：

### 用户界面（UI）

TDD很难用于UI。TDD更容易且更好地适用于领域模型和核心逻辑，尽管这未必是坏事。它有助于你严格地将UI与领域模型分离，这是一项基本的设计最佳实践（所以无论如何都应该这样做，但TDD会促进它）。确保你编写非常薄的UI，并将逻辑从表单中分离出来。

### 持久化数据

数据库确实给TDD带来了一个棘手的问题，因为一旦你在一个测试中写入了数据库，当下一个测试开始时数据库就处于另一种状态，这会给隔离带来麻烦。你可以编写代码在每次测试之间将数据库设置为已知状态，但这会增加测试人员的负担，而且测试运行会慢得多。

你也可以编写测试使其不受状态变化的影响，这可能会稍微降低测试的效力。另一种解决方案是使用存根或模拟对象来模拟数据库，但在集成测试期间除外，此时需要在测试前恢复数据库的备份。

还有一种方法纯粹为了测试而使用事务。当然，如果你的测试关注事务语义，这就不是一个有用的解决方案。

## 注意

我们将在第6章“准备基础设施”中更详细地讨论数据库绑定测试。

### 虚假的安全感

仅仅因为得到绿色条并不意味着你没有bug；这只是意味着你的测试没有检测到任何bug。所以TDD不会让你陷入虚假的安全感。记住，一个通过的测试并不能证明没有bug，只能证明那个特定的测试在执行时没有发现问题。

另一方面，仅仅因为你的测试不完美并不意味着你不应该使用它们。它们仍然会帮助你大大提高质量！

正如我的朋友Mats Helander曾经说过的，价值不在于绿色，而在于红色！

### 失去全局视野

TDD可以被看作是一种自下而上的方法，你必须意识到你可能会时不时地失去全局视野。例如，时不时地将你的代码可视化为UML，绝对是一个非常好的主意，这样你可以获得鸟瞰视角。你几乎肯定会发现一些应该应用的重构，以便为未来准备好你的代码。

### 更多需要维护的代码

维护方面是一把双刃剑。测试对于维护工作来说非常棒，但你也需要维护更多的代码。

我刚才说过TDD很难应用于UI和数据库，而这正是领域模型模式大放异彩的又一个原因，因为与其他逻辑结构相比，你通常可以在不接触数据库和UI的情况下运行更有意义的测试！话虽如此，我们将在后面的章节中讨论数据库测试和UI测试。

总之，我认为TDD是工具箱中的一个伟大工具！

## 下一阶段？

以上只是对基本概念的介绍，我们只是稍微触及了表面。当你开始应用TDD时，一旦克服了最初的启动问题，它可能会顺畅地工作。

然后过一段时间，你可能会发现设置某些测试变得过于复杂，并且至少对于测试本身而言，过于依赖无趣的部分/无趣的测试细节。这是一个好迹象，表明你已经进入了TDD的下一个阶段。我的朋友Claudio Perrone将在下一节“模拟对象与存根”中详细讨论这个问题。

![](img/89fb3513cb9b6343875aadbfd042005d_110_0.png)

![](img/89fb3513cb9b6343875aadbfd042005d_110_1.png)

```csharp
Assert.IsTrue(
        IsUserInsertedInDataBase(
            "Claudio", "Perrone", "MyUniqueLogin", "MyPassword"));
}
```

## 注意

`Rollback` 属性目前尚未在当前的NUnit中提供（尽管它在其路线图中）。我使用了由Roy Osherove编写的修改版本，可在此处找到：[http://weblogs.asp.net/rosherove/archive/2004/07/12/180189.aspx](http://weblogs.asp.net/rosherove/archive/2004/07/12/180189.aspx)。

因为 `UserBC` 业务组件接收一个业务实体并将其保存到数据库，所以测试通过创建实体、将其作为参数传递给 `SaveUser()` 方法，并验证该实体是否已持久化到数据存储来检查其行为。

## 独立宣言

这种测试风格的一个潜在问题是，对象很少独立运作。被测对象所依赖的其他对象通常会完成部分工作。

为了用我们的示例说明这个问题，我们可以按如下方式实现 `UserBC` 类（为方便起见，省略了所有异常处理代码）：

```csharp
public class UserBC
{
    public void SaveUser(IUserInfo user)
    {
        user.Validate();
        UserDao daoUser = new UserDao();
        if (user.IsNew)
            daoUser.Insert(user);
        else
            daoUser.Update(user);
    }
}
```

在这种情况下，`UserBC` 将用户验证委托给 `UserInfo` 业务实体。如果一个或多个业务规则被违反，`UserInfo` 将抛出一个包含验证错误集合的自定义异常。`UserBC` 还将业务实体的持久化委托给 `UserDao` 数据访问对象，该对象负责抽象所有数据库实现细节。

由于 `UserInfo` 是 `SaveUser()` 方法的显式参数，我们可以说 `UserBC` 显式声明了对 `IUserInfo` 接口（由 `UserInfo` 类实现）的依赖。然而，对 `UserDao` 的依赖在某种程度上隐藏在 `UserBC` 类的实现内部。

```
}
. . .
}
```

此时有几个重要的方面需要考虑。

首先，我们最初的测试对调用 SaveUser() 方法后 IUserInfo 对象的状态设置了一些预期。如果我们修改测试，使其使用 UserDaoStub 对象，我们还需要在 Insert() 方法执行之前通过设置 UserResult 属性来设置预期结果。

需要考虑的第二个方面是，对数据库的依赖现在完全消除了，我们最初的测试现在快得多。

然而，因为 SaveUser() 委托了它的大部分行为，这样的测试实际上几乎毫无价值。实际上，再想一想，我还要补充一点，我们正在犯一个致命的（但不幸的是常见的）错误：对从存根返回的值进行断言。所以我们实际上是在测试我们的存根，而不是 UserBC！

另一方面，如果我们想知道当数据访问层抛出诸如 DalUniqueConstraintException 之类的异常（这种情况可能发生在数据库已存在该用户登录名时），我们的 UserBC 类会如何反应，那就是另一回事了。

存根类中的 Insert() 方法现在变成：

```csharp
//UserDaoStub
public void Insert(IUserInfo user)
{
    if (ThrowDalUniqueConstraintExceptionOnInsert)
        throw new DalUniqueConstraintException();
    
    user.ID = UserResult.ID;
    user.Name = UserResult.Name;
    // etc
}
```

假设我们希望 UserBC 捕获 DalUniqueConstraintException 并抛出一个适当的业务异常，以保持各层的抽象。下面的测试说明了这种情况：

```csharp
[Test] // Note no database is needed anymore!
[ExpectedException(
    typeof(BusinessException),
    "The provided login already exists.")]
public void TestUserBCSaveUserThrowsBusinessException()
{
    // Setting stubs to remove all dependencies
    IUserInfo user = new UserInfoStub (
        "Claudio", "Perrone", "Login", "MyPassword");
    
    UserDaoStub daoUser = new UserDaoStub();
```

