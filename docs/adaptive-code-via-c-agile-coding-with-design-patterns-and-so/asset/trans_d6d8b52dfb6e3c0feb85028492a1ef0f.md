

AsyncComponent 类存在一个问题：它对 Task 类的依赖是隐式的，这意味着很难测试这个类。使用静态依赖进行单元测试代码很困难，因此最好用起重机替换这个 skyhook。

## 异步装饰器的局限性

并非所有可想象的方法都可以使用装饰器模式来创建客户端不知道的异步版本。事实上，这种方法适用的唯一异步方法就是 fire-and-forget 方法。

fire-and-forget 方法没有返回值，并且客户端不需要知道此类方法何时返回。当它被实现为异步装饰器时，客户端无法知道方法调用何时真正完成，因为调用会立即返回——而实际执行的工作可能仍在进行中。

请求-响应方法是常见的数据检索方法，通常非常适合异步实现，因为它们往往耗时较长并阻塞 UI 线程。客户端需要知道该方法是异步的，以便它们可以显式编码以在异步方法完成后接受回调。因此，请求-响应方法不能通过使用异步装饰器来实现。

## 装饰属性和事件

到目前为止，你已经了解了如何装饰接口的方法，但属性和事件呢？只要你不使用自动属性或自动事件，这两种语法元素也可以被装饰：你需要显式定义它们才能正确装饰它们。

清单 5-33 显示了属性的手动创建，但对于 getter 和 setter 而言，它没有使用 backing field，而是将调用委托给接口的被装饰实例。

### LISTING 5-33 属性也可以使用装饰器模式，就像方法一样。

Click here to view code image

```
public class ComponentDecorator : IComponent
{
    public ComponentDecorator(IComponent decoratedComponent)
    {
        this.decoratedComponent = decoratedComponent;
    }

    public string Property
    {
        get
        {
            // We can do some mutation here after retrieving the value
            return decoratedComponent.Property;
        }
    }

    set
    {
        // And/or here, before we set the value
        decoratedComponent.Property = value;
    }
}

private readonly IComponent decoratedComponent;
}
```

清单 5-34 显示了事件的手动创建，但对于 adder 和 remover 而言，它没有使用 backing field，而是将调用委托给接口的被装饰实例。

### LISTING 5-34 事件也可以使用装饰器模式，就像方法一样。

Click here to view code image

```
public class ComponentDecorator : IComponent
{
    public ComponentDecorator(IComponent decoratedComponent)
    {
        this.decoratedComponent = decoratedComponent;
    }

    public event EventHandler Event
    {
        add
        {
            // We can do something here, when the event handler is registered
            decoratedComponent.Event += value;
        }
        remove
        {
            // And/or here, when the event handler is deregistered
            decoratedComponent.Event -= value;
        }
    }

    private readonly IComponent decoratedComponent;
}
```

## 使用策略模式代替 switch

要了解策略模式最适合应用的时机，可以查看条件分支的实例。每当你使用 switch 语句时，都可以使用策略模式来简化客户端，使其将复杂性委托给依赖接口。清单 5-35 显示了一个可以使用策略模式替换的 switch 语句示例。

### LISTING 5-35 此方法使用 switch 语句，但策略模式会更具适应性。

Click here to view code image

```
public class OnlineCart
{
    public void CheckOut(PaymentType paymentType)
    {
        switch(paymentType)
        {
            case PaymentType.CreditCard:
                ProcessCreditCardPayment();
                break;
            case PaymentType.Paypal:
                ProcessPaypalPayment();
                break;
            case PaymentType.GoogleCheckout:
                ProcessGooglePayment();
                break;
            case PaymentType.AmazonPayments:
                ProcessAmazonPayment();
                break;
        }
    }

    private void ProcessCreditCardPayment()
    {
        Console.WriteLine("Credit card payment chosen");
    }

    private void ProcessPaypalPayment()
    {
        Console.WriteLine("Paypal payment chosen");
    }

    private void ProcessGooglePayment()
    {
        Console.WriteLine("Google payment chosen");
    }

    private void ProcessAmazonPayment()
    {
        Console.WriteLine("Amazon payment chosen");
    }
}
```

在示例中，对于 switch 语句的每一种情况，类的行为都会发生变化。这带来了代码维护问题，因为添加新的 case 选项需要更改此类。如果相反，你用接口的新实现替换每个 case 语句，则可以创建进一步的实现来封装新功能——而客户端无需更改。这在清单 5-36 中显示。

### LISTING 5-36 在 switch 语句被替换后，客户端看起来对变化更具适应性。

Click here to view code image

```
public class OnlineCart
{
    public OnlineCart()
    {
        paymentStrategies = new Dictionary<PaymentType, IPaymentStrategy>();
        paymentStrategies.Add(PaymentType.CreditCard, new PaypalPaymentStrategy());
        paymentStrategies.Add(PaymentType.GoogleCheckout, new GoogleCheckoutPaymentStrategy());
        paymentStrategies.Add(PaymentType.AmazonPayments, new AmazonPaymentsPaymentStrategy());
        paymentStrategies.Add(PaymentType.Paypal, new PaypalPaymentStrategy());
    }

    public void CheckOut(PaymentType paymentType)
    {
        paymentStrategies[paymentType].ProcessPayment();
    }

    private IDictionary<PaymentType, IPaymentStrategy> paymentStrategies;
}
```

按照面向对象编程的传统，这段代码将不同的支付类型对象化为各个类，每个类都实现了 IPaymentStrategy 接口。在此示例中，OnlineCart 类有一个私有字典，将 PaymentType 枚举的每个值映射到策略接口的一个实例。这大大简化了 CheckOut 方法。switch 语句已被移除，连同它一起被移除的是如何处理每种不同

支付类型的知识。OnlineCart 类不需要知道如何处理支付，而支付处理方式可能差异很大，并在此类上引入许多不必要的依赖。现在它的工作是选择正确的支付策略并将处理委托给它。

这里仍然存在添加新支付策略实现时的维护负担。如果你想添加对 WePay 的支持，例如，构造函数将需要更新以将新的 WePayPaymentStrategy 类映射到关联的 WePay 枚举值。

## 结论

单一职责原则对代码的适应性有极其积极的影响。与不遵循该原则的等效代码相比，符合 SRP 的代码会导致数量更多、范围更小且更具针对性的类。在本应存在一个类或一组具有相互依赖关系和职责混淆的类的地方，SRP 引入了秩序和清晰。

SRP 主要通过在接口后面抽象代码并将不相关功能的责任委托给运行时接口后面的实现来实现。一些设计模式非常擅长支持严格规范 SRP 的努力——特别是适配器模式和装饰器模式。前者使你的大部分代码能够维护对你直接控制的接口的第一方引用，尽管实际上使用的是第三方库。后者可应用于任何需要移除类的一部分功能但又与类的意图紧密耦合而无法独立存在的情况。

本章未涵盖的是所有这些类在运行时如何编排。在本章中，将接口传递给构造函数被视为理所当然，但第 9 章描述了实现此操作的多种方法。

