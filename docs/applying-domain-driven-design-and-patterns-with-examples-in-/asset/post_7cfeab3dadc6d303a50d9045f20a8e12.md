
[Test]
public void OrderNumberCantBeZeroAfterReconstitution()
{
    int theOrderNumber = 42;
    _FakeAnOrder(theOrderNumber);

    Order o =
        _repository.GetOrder(theOrderNumber);

    Assert.AreEqual(theOrderNumber, o.OrderNumber);
}

As usual, the whole thing won't compile. I don't have an OrderRepository class, so I write one with just a signature for the GetOrder() method and no code. The test code still won't compile, so I have to stub the _FakeAnOrder() in the test class. I get a red bar.

I'm just getting further and further away from the problem I thought I wanted to focus on. To be able to write the _FakeAnOrder() method, I need to make it possible for the Repository to know about an Order. I could go ahead and implement a new method in the OrderRepository that is only there for supporting other tests, but I think this is a good sign of my needing to write another test instead. I need to test saving Orders, or at least make the Repository aware of Orders.

## Note

I have to admit that I have quite a lot of ideas about how the saving should really happen, but I'll move on slowly here and write simple code that I will refactor a lot now. Please don't get upset about this; it's not the final solution.

So, I add the Ignore attribute to the OrderNumberCantBeZeroAfterReconstitution() test so that it won't give me a red bar right now. Then I write another test that looks like this:

[Test]
public void CanAddOrder()
{
    _repository.AddOrder(new Order(new Customer()));
}

As usual, it won't compile. I need to add the AddOrder() method to the OrderRepository. And as usual, I just add the signature, but this is not enough to get a red bar. As a matter of fact, there is no test code at all in the CanAddOrder() method. The reason is that I'm not keen on the idea of letting the Repository publish any methods for the sole purpose of an external test class for checking the inner state of the Repository. Sure, I could use the GetOrder() method, but then it's the chicken or the egg scenario. The implementation of this method is far from being started yet.

```csharp
public void AddOrder(Order order)
{
    int theNumberOfOrdersBefore +1 = _theOrders.Count;

    _theOrders.Add(order);

    MyTrace.Assert(theNumberOfOrdersBefore
        == _theOrders.Count);
}
```

And we now have a green bar. We are writing some strange code here and there, but we are moving forward, and we are creating tests that aren't weird at all along the way, so let's continue.

## Note

I could have also worked with a mock to verify that the System Under Test (SUT) worked as expected, but you can probably envision how from Chapter 3, "TDD and Refactoring," so let's move forward.

Now it's time to go back to the OrderNumberCantBeZeroAfterReconstitution(), and what I stumbled on the last time was the help method for the test that I called _FakeAnOrder(). It could look like this:

```csharp
//A test class
public void _FakeAnOrder(int orderNumber)
{
    Order o = new Order(new Customer());

    _repository.AddOrder(o);
}
```

Ouch, we are now experiencing another problem. Do you see it? Yep, how can we get the faked OrderNumber into the order instance? The OrderNumber property was read-only (which makes sense), so using that one won't work.

As a matter of fact, this is a generic problem. It can be expressed like this: How can we from the outside (such as in a Repository) set values in instances that are being reconstituted from persistence?

## Reconstituting an Entity from Persistence: How to Set Values from the Outside

I mentioned the generic problem of setting values in an instance that is being recreated by reading from persistence. Well, we have already touched on this subject several times in this chapter since `Order` and `Customer` are examples of Entities, but let's take a step back and focus on the concept.

It is important for us to keep track of some things in the domain over time. No matter whether a customer changes name or address, it's still the same customer, and it's something we are interested in keeping track of. On the other hand, if a customer's reference person changes, it is probably not anything we care to keep track of. A customer is a typical example of an Entity [Evans DDD]. Again, an Entity is something we keep track of by identity rather than all its values.

To take an extreme example of something that isn't an Entity, let's think about the integer 42. I don't care about the identity of 42 at all; I only care about the value. And when the value changes, I no longer think it's the 42 that has changed it's a totally new value with no connection to the old one. Forty-two is a Value Object [Evans DDD] and not an Entity.

If we take that extreme example over to our domain, we might be able to say that it isn't interesting for us to track `ReferencePerson` of a `Customer` by identity. It's only interesting for us to track it by value. We'll get back to Value Objects later on in this chapter.

## Note

Of course, what should be tracked by identity and what should just be thought of as values is highly dependent on the domain. Let's take an example. As I said above, I believe that `ReferencePerson` in this application can be dealt with as a Value Object, but if the application is for, let's say, a sales support application for salesmen, perhaps they see `ReferencePerson` as an Entity instead.

## Back to the Flow Again

Unfortunately, the test `CanFindOrdersViaCustomer()` won't execute successfully after I override `Equals`. The reason is that all customers used in the test have the same `CustomerNumber`, that being zero, and therefore I find five `Orders` that have the right `Customer`, not three. We need to change the test a little bit. I create another little helper method called `_FakeACustomer()` like this:

```csharp
//A test class
private Customer _FakeACustomer(int customerNumber)
{
    Customer c = new Customer();

    RepositoryHelper.SetFieldWhenReconstitutingFromPersistence
    (c, "_customerNumber", customerNumber);

    return c;
}
```

![](img/89fb3513cb9b6343875aadbfd042005d_188_0.png)

This might grow on me, but right now I prefer the more specific interface in Figure 5-8, as it clearly states exactly what is needed. The generic `IRepository` requires more casts when being used and might be incorrectly trying to gather all upcoming Repositories in one and the same shape.

Another solution might be to use generics in the `IRepository`-interface + a base class and thereby at least get the type safety (and avoid code duplication) and avoid extra type casts. One problem then is that I might add a `Delete()` method to the Repository, even though not all Repositories will need it. And even with generics, the `GetListByParent(parent)` is troublesome because what if an Entity has several parents? Well, it's an early sketch and that can be solved of course. But I can't help thinking that it's better to let the code "speak as clearly as possible for now" and skip generalizations like that. It's just not feeling important yet. As usual, no decisions are carved in stone. I can challenge the decisions again later on when I can more easily see what pieces can be generalized, but for now, I'll stay with `OrderRepository`.

Because of that, I rename the `OrderRepository` class to `OrderRepositoryFake` and let the class implement the `IRepository`. I also need to change the `[SetUp]` code in my test class. It currently looks like this:

```text
//A test class, the [SetUp]

_repository = new OrderRepository();
```

It could now look like this:

```text
//A test class, the [SetUp]

_repository = new OrderRepositoryFake();
```

The declaration of `_repository` must use `IOrderRepository` as the type.

And the tests still work.

I guess pure XP'ers would groan a little bit at the refactoring I just did. I actually didn't have to make that change now; it was a change for preparing for the future, when I need a real Repository instead of the faked one. OK, I can agree with that, but I can't help thinking a little bit about the future (read: later chapters) when I will be hooking in infrastructure.

I cross my fingers that this preparation will prove to be good. I fell back into old habits of early guessing.... On the other hand, we are of course free to choose our own balance and don't have to
