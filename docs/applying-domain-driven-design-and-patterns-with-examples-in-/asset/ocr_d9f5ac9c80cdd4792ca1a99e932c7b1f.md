account, which means that a holiday calendar is an optional dependency. With constructor dependency injection, we express this by providing two constructors, one for each valid set of dependencies.

```
public class BondPricer {
    private readonly IDiscountCurve curve;
    private readonly IHolidayCalendar calendar;

    public BondPricer(IDiscountCurve aCurve) {
        curve = aCurve;
    }
    public BondPricer(IDiscountCurve aCurve
        , IHolidayCalendar aCalendar) : this(aCurve) {
        calendar = aCalendar;
    }
}
```

It would also be possible to use a constructor with all arguments and pass in null for the optional ones, but this makes the contract less explicit, especially when the number of dependencies increases. It is therefore advisable to always provide one constructor for each valid set of dependencies and, if possible, to chain the constructors. If this seems impossible, it is probable that the class in question has too many dependencies and should be broken up.

# Setter Dependency Injection

As the aptly chosen name suggests, Setter Dependency Injection uses setters rather than the constructor to inject the dependencies. Consequently, the pricer has a default constructor but requires an additional property with a setter.

```
public class BondPricer {
    private IDiscountCurve curve;

    public BondPricer() {
    }
    public IDiscountCurve DiscountCurve {
        set { curve = value; }
    }
}
```

Setter injection provides the same degree of decoupling as constructor injection, and it is easy to see that creating pricer objects in unit tests is as straightforward as with constructor injection. An important difference is that the pricer is in an invalid state until the setter method has been called, something that is not possible with constructor injection. Additionally, we cannot declare the curve variable as readonly because it is not initialized in the constructor and, finally, with setter injection it is a little more tricky and error-prone to implement final initialization functionality that needs to be run after all the dependencies have been injected.

Setter injection has its uses despite these shortcomings because it scales better to components with