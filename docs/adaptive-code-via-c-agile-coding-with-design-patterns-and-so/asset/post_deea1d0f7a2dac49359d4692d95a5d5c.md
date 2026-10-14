
There is a problem with the AsyncComponent class: its dependency on the Task class is implicit, meaning that it is hard to test this class. Unit testing code with static dependencies is difficult, so you would be better off replacing this skyhook with a crane.

## The limitations of asynchronous decorators

Not all conceivable methods can make use of the Decorator pattern to create asynchronous versions that clients do not know about. In fact, the only asynchronous methods to which this approach is applicable are fire-and-forget methods.

A fire-and-forget method has no return value, and clients do not need to know when such a method returns. When it is implemented as an asynchronous decorator, clients cannot know when a method call truly was completed because the call returns immediately—while the real work being performed is probably still in progress.

Request-response methods are common data-retrieval methods that are often very usefully implemented asynchronously, because they tend to take a while and block the UI thread. Clients need to know that the method is asynchronous, so that they can be coded explicitly to accept a callback when the asynchronous method is complete. Therefore, request-response methods cannot be implemented by using asynchronous decorators.

## Decorating properties and events

So far, you have learned how to decorate the methods of an interface, but what about properties and events? Both of those syntactic elements can also be decorated, as long as you do not use auto-properties or auto-events: you need to explicitly define both in order to decorate them properly.

Listing 5-33 shows the manual creation of a property, but rather than having a backing field, for both the getter and the setter this code delegates to the decorated instance of the interface.

### LISTING 5-33 Properties can also use the Decorator pattern, just like methods.

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

Listing 5-34 shows the manual creation of an event, but rather than having a backing field, for both the adder and remover this code delegates to the decorated instance of the interface.

### LISTING 5-34 Events can also use the Decorator pattern, just like methods.

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

## Using the Strategy pattern instead of switch

To understand when the Strategy pattern is best applied, you can look at instances of conditional branching. Whenever you use switch statements, you can use the Strategy pattern to simplify the client so that it delegates complexity to dependent interfaces. Listing 5-35 shows an example of a switch statement that could be replaced with the Strategy pattern.

### LISTING 5-35 This method uses a switch statement, but the Strategy pattern would be more adaptive.

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

In the example, for each case of the switch statement, the behavior of the class changes. This presents a code maintenance problem because the addition of a new case option requires a change to this class. If, instead, you replace each case statement with a new implementation of an interface, further implementations can be created to encapsulate new functionality—and the client would not need to change. This is shown in Listing 5-36.

### LISTING 5-36 After the switch statement is replaced, the client looks far more adaptive to change.

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

In the tradition of object-oriented programming, this code has objectified the different payment types into various classes, each of which implements the IPaymentStrategy interface. In this example, the OnlineCart class has a private dictionary that maps each value of the PaymentType enumeration onto an instance of the strategy interface. This simplifies the CheckOut method significantly. The switch statement has been removed and, along with it, the knowledge of how to process each different

type of payment. The OnlineCart class did not need to know how to process the payments, which could vary greatly and introduce many unnecessary dependencies on this class. Now its job is to select the right payment strategy and delegate the processing to it.

There is still a maintenance burden here for adding new payment strategy implementations. If you want to add support for WePay, for example, the constructor will need to be updated to map the new WePayPaymentStrategy class to the associated WePay enumeration value.

## Conclusion

The single responsibility principle has a hugely positive impact on the adaptability of code. Compared to equivalent code that does not adhere to the principle, SRP-compliant code leads to a greater number of classes that are smaller and more directed in scope. Where there would otherwise have been a single class or suite of classes with interdependencies and a confusion of responsibility, the SRP introduces order and clarity.

The SRP is primarily achieved through abstracting code behind interfaces and delegating responsibility for unrelated functionality to whichever implementation happens to be behind the interface at run time. Some design patterns are excellent at supporting efforts to strictly regiment the SRP—in particular, the Adapter pattern and the Decorator pattern. The former enables much of your code to maintain first-party references to interfaces under your direct control, although in reality utilizing a third-party library. The latter can be applied whenever some of a class’s functionality needs to be removed but it is too tightly coupled with the intent of the class to stand alone.

What this chapter did not cover is how all of these classes are orchestrated at run time. Passing interfaces into constructors was taken for granted in this chapter, but Chapter 9 describes a variety of ways in which this can be accomplished.
