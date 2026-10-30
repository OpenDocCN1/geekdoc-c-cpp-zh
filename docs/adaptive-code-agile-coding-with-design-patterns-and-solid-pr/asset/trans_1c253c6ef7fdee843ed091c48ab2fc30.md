

请注意，在此阶段，原来的 Account 类尚未被更改。这些类是作为独立类创建的。这些类的单元测试将反映 CalculateRewardPoints 类的期望，但针对每种账户类型的系统 under test（SUT）不同。用于确定白金账户和黄金账户类应得奖励积分的算法依赖于当前余额；已包含该依赖项以使这些类能够独立编译。Balance 属性也是公开可设置的，这使得可以使用不同的值进行单元测试。图 6-1 中的 UML 类图解释了这些类之间的关系。

![](img/f852e0a12c174e64d91a8e1a05146eab_220_0.png)

图 6-1 Account 类将变为抽象类，并具有抽象的 CalculateRewardPoints 方法。

这只是为完成用继承替换 switch 语句这一目标而设的一个中间目标，当然。重要的是不要一次做太多，以便你可以通过一系列较小的更改来验证自己是否走在正确的轨道上。下一个更改，在清单 6-4 中，是将全部四个类链接到一个继承层次结构中。

## LISTING 6-4 从 Account 类中移除了复杂性。

```
public abstract class AccountBase
{
    public decimal Balance
    {
        get;
        private set;
    }

    public int RewardPoints
    {
        get;
        private set;
    }

    public void AddTransaction(decimal amount)
    {
        RewardPoints += CalculateRewardPoints(amount);
        Balance += amount;
    }

    public abstract int CalculateRewardPoints(decimal amount);
}
```

没有了 switch 语句，这个类就没有理由再意识到自己的“类型”了，因此构造函数也被移除了。该类由于抽象的计算方法而变为抽象，但这意味着你不能再实例化它，从而也不能再对其进行测试。

## Indiana Jones 和激进的重构

在电影《夺宝奇兵：失落的方舟》开头，主人公深入秘鲁的一个洞穴，试图找回一个小偶像。他知道偶像所坐的带重量的开关上设有机关陷阱。他用沙子装满布袋，试图将其作为偶像的替代品。他的理论是，如果他能足够快地用沙袋替换偶像，就能防止开关被触发，机关陷阱就不会启动。

不幸的是，印第的计划失败了，他被巨石从洞穴中追赶出来。作为一个开端事件，这堪称最令人难忘的之一。但其中有一个技巧可以应用于重新设计：并行实现。

金色偶像代表现有的类或方法，而沙袋则类似于新设计。以并行方式实现新设计，允许在最后一刻更新客户端代码，有效地将金色偶像换成沙袋。然后可以安全地完全移除旧设计。

Account 类的重构就是一个需要通过并行实现来达到中间目标的激进重构示例。请注意，并行实现的令人信服的优势在于，在整个过程中，可以随时保存进度以便稍后恢复。重构不应阻止你在源代码控制中定期提交。目标是每 10 到 15 分钟提交一次。

单元测试需要一个对象实例才能工作，因此下一步是将三种账户类型链接为该基类的子类。一个有用的命名约定——类似于接口名称以大写 I 为前缀——是将抽象类后缀命名为 Base。这是一个快速提示，表明该类不能被实例化并且有相关的子类。

当创建三个子类时，你可以从 GoldAccount 和 PlatinumAccount 中移除 Balance 属性，因为它们将从该基类继承 Balance 和 AddTransaction 成员。清单 6-5 显示了此步骤后全部三个类。

## LISTING 6-5 通过继承基类完成重构。

```
public class SilverAccount : AccountBase
{
    public override int CalculateRewardPoints(decimal amount)
    {
        return Math.Max((int)decimal.Floor(amount / SilverTransactionCostPerPoint), 0);
    }

    private const int SilverTransactionCostPerPoint = 10;
}
```

```
{
    AccountBase account = null;
    switch(type)
    {
        case AccountType.Silver:
            account = new SilverAccount();
            break;
        case AccountType.Gold:
            account = new GoldAccount();
            break;
        case AccountType.Platinum:
            account = new PlatinumAccount();
            break;
    }
    return account;
}
```

工厂方法的两个关键特性减轻了客户端的负担。首先，它是静态的，这意味着客户端在类型上调用它，而不是在该类型的实例上调用。其次，返回类型是基类，允许你将子类账户隐藏在客户端之外。事实上，你可以将其隐藏到它们是 internal 的程度，因此在该程序集之外不可见。这不允许客户端直接构造子类，消除了 new 操作符作为潜在的代码异味的可能性（参见第 3 章“依赖关系和分层”）。清单 6-7 比较了重构前后客户端如何与账户交互。

尽管 switch 语句仍然存在，但在此实例中要简单得多，并且促进了之前用多态性替换它的重构。

## LISTING 6-7 重构前后 Account 如何创建新账户。

```
public void CreateAccount(AccountType accountType)
{
    var newAccount = new Account(accountType);
    accountRepository.NewAccount(newAccount);
}
// . . .
public void CreateAccount(AccountType accountType)
{
    var newAccount = AccountBase.CreateAccount(accountType);
    accountRepository.NewAccount(newAccount);
}
```

这段代码是客户端——在此例中为 Account——在重构前后如何构造新账户的示例。区别微不足道，但请注意 new 操作符已被移除并替换为对工厂方法的静态调用。这是一种用更灵活的东西替换非常僵硬的东西的常见方式。工厂方法打开了更多可能性，因为它们可以返回的内容比总是返回相同类型的方法要多。

细心的读者会注意到，选择静态工厂方法是不理想的——它更像天钩而非起重机，因此会影响代码的稳定性和适应性。更好的实现会将 CreateAccount 方法放在合适的接口上，如下一节所述。

## 用工厂类替换构造函数

工厂方法有一个替代方案：工厂类。事实上，你不需要将客户端耦合到独立工厂的实现；你只需给他们接口，如清单 6-8 所示。

**LISTING 6-8** 账户工厂隐藏了创建账户实例的实现细节。

```
public interface IAccountFactory
{
    AccountBase CreateAccount(AccountType accountType);
}
```

该方法的接口实际上与工厂方法的接口相同，只是它是实例方法。实现可以与之前的方法体相同，这意味着它对所有不同类型的账户都有完美的了解。Account 以及其他客户端随后会将此接口作为构造函数参数需要，如清单 6-9 所示。

**LISTING 6-9** 服务现在接收工厂作为构造函数参数并用它来创建账户。

```
public class Account
{
    public Account(IAccountFactory accountFactory, IAccountRepository
    accountRepository)
    {
        this.accountFactory = accountFactory;
        this.accountRepository = accountRepository;
    }

    public void CreateAccount(AccountType accountType)
    {
        var newAccount = accountFactory.CreateAccount(accountType);
        accountRepository.NewAccount(newAccount);
    }

    private readonly IAccountRepository accountRepository;
    private readonly IAccountFactory accountFactory;
}
```

这个服务开始看起来应该是的样子：由更细粒度的接口编排而成，以实现用户界面层的更大目标。出于简洁和清晰的考虑，它缺少构造函数上的一些保护子句，以防止空依赖，以及 CreateAccount 方法上的一些 try/catch 块，以将领域异常编排为服务异常。

