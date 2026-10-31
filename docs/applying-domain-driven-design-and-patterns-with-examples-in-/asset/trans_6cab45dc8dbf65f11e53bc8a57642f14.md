

## 关于保存的一些话

我之前提到过保存数据。`AddOrder()` 并不是真正的保存；它只是把 `Order` 添加到 `Repository` 中。还是说它也应该意味着保存？不，我不认为我想要那样的行为。我希望 `AddOrder()` 做的是，从那一刻起，`Repository`（以及底层基础设施）应该知道该实例，并在当我请求 `PersistAll()` 时对它进行处理。

我需要让基础设施来处理保存功能。现在的问题是，我是否应该将 `PersistAll()` 声明给 `Repository` 实例，还是声明给一个更高层的、监控所有 `Repositories` 实例的东西。再说一次，我觉得我正在偏离领域模型，进入基础设施部分。我很高兴这个问题被提出来，但部分讨论必须等到下一章。就这一点而言，我们有很多东西需要讨论。目前，我对 `AddOrder()` 作为让 `Repository` 知道该实例的方式感到满意。到目前为止所写的测试而言，该实例是瞬态的（但已准备好被持久化）并且在那个时间点不是持久的，这一点并不重要。

好的，我和你一样渴望写更多的测试。清单上有什么？嗯，在功能 2“查看特定客户时列出订单”中，我已经处理了大部分内容。我没有处理的是显示每个订单的总金额、订单类型和联系人。

我们一个一个来，先看每个订单的总金额。

## 每个订单的总金额

起初这似乎是一项微不足道的任务。我需要创建一个 `OrderLine` 类，作为列表挂接到 `Order` 类中。然后我就可以遍历 `OrderLine` 集合并计算总金额。当然，我实际上可以从消费代码中这样做，但我不想那样。那会把算法暴露给消费方，而且那样也不够清晰或没有目的性。实际上，随着时间的推移，算法会变得难得多，例如添加许多不同种类的折扣。相反，我想要在 `Order` 类上有一个名为 `TotalAmount` 的只读属性。同样，它可以在内部遍历 `OrderLine` 集合并计算值。

但作为“过早优化的人”（尽管我努力不这样），这对我来说有点太过分了。为了能够显示订单的 `TotalAmount` 而为每个 `Customer` 的每个 `Order` 实例化所有 `OrderLines`，这拉响了警报。这可能不会成为问题，具体取决于执行环境和所选的基础设施。另一方面，在分布式系统的情况下，这是一个问题，而且可能是一个大问题，会伤害数据库服务器、网络和垃圾回收器。

我必须承认，我必须强迫自己不要立即处理这个优化。直接修复很简单，但现在当我琢磨领域模型应该是什么样子的时候，这并不是真正重要的。现在更重要的是为了简单和清晰而设计，之后再用性能分析器来看它是否是一个*真正的*性能问题。所以我从最简单的解决方案开始，如果性能特性不够好，以后可以重构 `TotalAmount` 属性。

啊，我做到了！我现在跳过了一个优化。此刻感觉真好。

既然我们已经对 `TotalAmount` 有了一些思考，让我们退一步。是时候写一个测试了（迟到总比没有好）。我从我能想到的最简单的测试开始。

```csharp
[Test]
public void EmptyOrderHasZeroForTotalAmount()
{
    Order o = new Order(new Customer());

    Assert.AreEqual(0, o.TotalAmount);
}
```

让这个测试编译很简单。我只需在 `Order` 类中添加一个名为 `TotalAmount` 的公共只读属性，并让它返回 -1。它编译了，然后我得到了红灯。我把它改成返回 0，就得到了绿灯。

我现在可以暂时不管它，但因为上下文已经为我准备好了，我继续一点。下面是另一个测试：

```csharp
[Test]
public void OrderWithLinesHasTotalAmount()
{
    Order o = new Order(new Customer());

    OrderLine ol = new OrderLine(new Product("Chair", 52.00));
    ol.NoOfUnits = 2;

    o.AddOrderLine(ol);

    Assert.AreEqual(104.00, o.TotalAmount);
}
```

哎呀，仅仅这一个测试就做了很多设计，我现在需要创建两个类，并在旧类中添加新方法，才能让它编译。我想我最好暂时注释掉那个测试，从更简单的地方开始，专注于 `OrderLine` 类。

首先，我希望 `OrderLine` 默认从所选产品获取价格。让我们写一个测试。

```csharp
[Test]
public void OrderLineGetsDefaultPrice()
{
    Product p = new Product("Chair", 52.00);

    OrderLine ol = new OrderLine(p);

    Assert.AreEqual(52.00, ol.Price);
}
```

返回 0。它能编译，但红灯。然后我把 `TotalAmount` 改成这样：

```csharp
//OrderLine
public decimal TotalAmount
{
    get {return Price * NumberOfUnits;}
}
```

又绿灯了。

让我们看看刚刚做了什么。在*图 5-10*中，你可以看到 `OrderLine` 和 `Product` 的图示。

### 图 5-10. `OrderLine` 和 `Product`

![](img/89fb3513cb9b6343875aadbfd042005d_192_0.png)

是时候回到我之前注释掉的测试了。你会在这里再次看到它，但这次我把它做得“大”了一点点，处理两个 `OrderLines`。

```csharp
[Test]
public void OrderWithLinesHasTotalAmount()
{
    Order o = new Order(new Customer());

    OrderLine ol = new OrderLine(new Product("Chair", 52.00));
    ol.NoOfUnits = 2;
    o.AddOrderLine(ol);

    OrderLine ol2 = new OrderLine(new Product("Desk", 115.00));
    ol2.NoOfUnits = 3;
    o.AddOrderLine(ol2);

    Assert.AreEqual(104.00 + 345.00, o.TotalAmount);
}
```

为了让它编译，我需要将 `AddOrderLine()` 和 `TotalAmount` 添加到 `Order`。我让只读属性 `TotalAmount` 暂时只返回 0。然后我在 `OrderWithLinesHasTotalAmount()` 测试上设置 `[Ignore]`。相反，我写另一个测试来专注于 `AddOrderLine()`。该测试可能如下所示：

```
theSum += ol.TotalAmount;

    return theSum;
}
}
```

简单、直接，而且绿灯。你注意到我抵制住了优化的冲动吗？我只是用我能想到的最简单的方式写了它，我甚至几乎没有抱怨地完成了它。毕竟，我目前将 Order 及其 OrderLines 视为聚合，因此也将其视为默认加载单元。

## 历史客户信息

我想是时候进行一些重构了。有什么坏味道吗？我不太喜欢的一点是 Order 与 Customer 存在关系。当然，Order 有一个 Customer，这没问题，但如果我在一年后查看一个 Order，我可能希望看到的是创建该 Order 时的客户信息，而不是现在的客户信息。

另一个问题是构造函数将 Customer 作为参数。这意味着 Order 可能会直接进入持久化对象图，而无需调用 `IOrderRepository.AddOrder()`，这可能不是一个好主意。（嗯，这也取决于你的基础设施，但很明显存在一个边界。）`AddOrder()` 是一种表明该订单在保存时应该被持久化的方式。

这些问题都不难处理，但我该如何清楚地传达这一点呢？我写一个测试，来尝试一个提议：

```
[Test]
public void OrderHasSnapshotOfRealCustomer()
{
    Customer c = new Customer();
    c.Name = "Volvo";

    Customer aHistoricCustomer = c.TakeSnapshot();

    Order o = new Order(aHistoricCustomer);

    c.Name = "Saab";
    Assert.AreEqual("Saab", c.Name);
    Assert.AreEqual("Volvo", o.Customer.Name);
}
```

但我不太确定这个解决方案……目前，Customer 是一个相当小的类型，但它可能会增长很多。即使它现在很小，跟踪 Customer 在那个时候有哪些联系人真的有意义吗？

我认为创建另一个只包含有意义的属性的类型可能是一个好的解决方案，因为它也会在聚合之间创建明确的边界，但尤其是因为这是底层模型所指示的。让我们创建一个 CustomerSnapshot（有点

