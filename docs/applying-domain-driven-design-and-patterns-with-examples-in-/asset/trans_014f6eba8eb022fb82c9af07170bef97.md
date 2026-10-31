

## 3. 一个订单可以有许多不同的订单行

特性3非常简单。图4-5描述了增强后的模型。

**图4-5. 订单和订单行**

![](img/89fb3513cb9b6343875aadbfd042005d_145_0.png)

注意，我这里也考虑的是单向关系。如果我知道某个逻辑片段需要同时使用 `OrderLine` 及其所属的 `Order`，那么我或许可以接受同时发送它们。把某个订单和另一个订单的订单行一起发送的风险很可能非常小。

```csharp
[Test]
public void CanIterateOverOrderLines()
{
    Customer newCustomer = _CreateACustomerAndAnOrder
        ("Ronny", 420);

    Order newOrder = (Order)_repository.GetOrders
        (newCustomer)[0];

    foreach (OrderLine orderLine in newOrder.OrderLines)
        return;

    Assert.Fail("I shouldn't get this far");
}
```

还要注意图4-5中展示的模型与描述同一事物的关系模型之间的巨大差异。在关系模型中，会有一个从 `Product` 到 `OrderLine` 的一对多关系，以及一个多对一关系，但到目前为止，我们认为在这个特定的领域模型中，一对多关系并不真正值得关注。

## 4. 并发冲突检测很重要

嗯...特性4有点棘手。我认为一个合理的解决方案是：`Customer` 独立存在，而 `Order` 连同 `OrderLines` 作为它自己的并发单元。这与让领域模型能够用来支持后续特性所需的逻辑非常契合。为此，我使用了称为“聚合”（Aggregate）的模式[Evans DDD]，这意味着你要决定哪些对象属于通常作为单个单元处理的特定对象簇，一起加载（至少在写场景下默认如此），一起评估规则，等等。

不过，重要的是要指出，聚合模式首先不是一个技术模式，而应该用在它为模型增添意义的地方。

并发单元是聚合的用途之一。（见图4-6。）

**图4-6. 聚合**

![](img/89fb3513cb9b6343875aadbfd042005d_146_0.png)

## 5. 客户欠我们的钱不能超过一定金额

特性5同样相当棘手。脑海中浮现的第一个解决方案可能是在 `Customer` 上添加一个 `TotalCredit` 属性。但这有问题，因为它有点过于透明，消费者调用该属性时看不到任何成本。这也是一致性问题。我甚至不认为 `Customer` 聚合包含 `Orders`，所以我并不期望这个单元适合用来直接在领域模型中处理一致性，这很好地说明我应该另寻他法。

我认为我需要领域模型中的一个服务（Service）[Evans DDD]，它能告诉我某个客户当前的信用总额。你会在图4-7中看到这个描述。

**图4-7. `TotalCreditService`**

![](img/89fb3513cb9b6343875aadbfd042005d_147_0.png)

对 `TotalCreditService` 的 `GetCurrentCredit()` 进行重载的原因是，我认为能够在不考虑当前正在创建或更改的订单的情况下，检查当前信用额度有多大，这会很好。至少这是想法。让我们看看这个服务实际运行起来会是什么样子（这里跳过不同部分之间的交互）。

```csharp
[Test]
public void CanGetTotalCreditForCustomerExcludingCurrentOrder()
{
    Customer newCustomer = _CreateACustomerAndAnOrder
        ("Ronneby", 22);
```

## 8. 在一位新客户被视为合格之前，他的信用会向信用机构查询

因此，我们需要领域模型中的另一个服务（Service）[Evans DDD]，用于封装我们与信用机构的通信方式。它的效果可以参见图4-10。

**图4-10：*CreditService***

![](img/89fb3513cb9b6343875aadbfd042005d_150_0.png)

再说一次，这种想法是让实体（这里的 Customer）与服务协作，以便实体能够回答问题。让我们看看这种协作如何在测试中处理。（另外要注意，真正的服务可能会使用客户的组织机构代码（OrganizationNumber），这和客户编号（CustomerNumber）不同，而是注册公司从官方机构获得的正式标识。）

```csharp
[Test]
public void CantSetTooHighCreditLimitForCustomer()
{
    Customer newCustomer = _CreateACustomer("Ronney");

    //Inject a stubbed version of CreditService
    //that won't allow a credit of more than 300.
    newCustomer.CreditService = new StubCreditService(300);

    newCustomer.CreditLimit = 1000;

    Assert.IsFalse(newCustomer.HasOKCreditLimit);
}
```

### 备注

Gregory Young指出这是一个代码坏味道。问题很可能在于该操作不是原子的。该值首先被设置（因此旧值被覆盖），然后才被检查（如果还记得检查的话）。也许类似 `Customer.RequestCreditLimit(1000)` 的做法会是更好的解决方案。我们会在第7章“规则至上”中回到类似的讨论。

## 9. 订单必须有一个客户；订单行必须有一个订单

特性9是一个常见且合理的要求，我认为最简单也是最好的处理方式是通过数据库的引用完整性约束。我们也可以在领域模型中测试这一点，而且应该测试。如果领域模型存在这种明显的错误，那么将其变更提交到持久化层就没有意义。不过，作为第一次尝试，我没有去显式检查，而是使用一个 `OrderFactory` 类来创建 `Order`，这使其在某种程度上成为强制性的；同时我用同样的方式处理 `OrderLines`，所以一个 `OrderLine` 必须拥有 `Order` 和 `Product`（见图4-11）。

**图4-11. OrderFactory 和增强的 Order**

![](img/89fb3513cb9b6343875aadbfd042005d_151_0.png)

像往常一样，我们来看看测试中各个部分之间的交互。

```
[Test]
```

一个名为 Accept() 的方法。我暂时不决定是否在内部使用状态模式（GoF设计模式），这留到以后再说。像这样的实现决策最好在重构期间做出。

**图4-12. Order 和 Status**

![](img/89fb3513cb9b6343875aadbfd042005d_153_0.png)

当我们讨论 Order 的其他状态时，我们会添加更多方法。目前，没有其他明确要求，所以我们只保留 Accept()。

当前的想法可能如下：

```csharp
[Test]
public void CanAcceptOrder()
{
    Customer newCustomer = _CreateACustomer("Karlskrona");
    Order newOrder = OrderFactory.CreateOrder(newCustomer);
    
    Assert.IsFalse(newOrder.Status == OrderStatus.Accepted);
    
    newOrder.Accept();
    
    Assert.IsTrue(newOrder.Status == OrderStatus.Accepted);
}
```

## 到目前为止的领域模型

因此，如果我们总结刚才讨论的领域模型，它可能如图4-13所示。

**图4-13. 一个草拟的领域模型，展示了我现在打算如何处理功能列表**

[查看全尺寸图片]

![](img/89fb3513cb9b6343875aadbfd042005d_154_0.png)

### 备注

`ReferencePerson` 类在 *图4-13* 中出现在两个不同的聚合中，但实例并不是。这说明了静态类图在表现力上的不足，但也可以通过一句简短的注释来解释。

什么？很乱？好吧，我同意，确实乱。当我们进一步深入细节时，我们会把模型划分得更好。

### 备注

*图4-13* 中显示的模型以及所有模型片段都是预先创建的，当我继续开发应用程序时，它们必定会得到大量改进。

另外需要说明的是，我只展示了核心领域模型，而没有展示更多与基础设施相关的内容，比如之前提到的工作单元（Unit of Work）[Fowler PoEAA]。当然，这完全是故意的。我们会在本书后面回到基础设施。现在我专注于领域模型。

