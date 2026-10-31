# Focus on Domain-Related Rules

Let's work with the remaining feature requirements from Chapter 4, one by one. We started out with the feature requirement number 6, which was called "An order may not have a total value of more than one million SEK," but we got interrupted when we realized that the context was missing from the sketched API. Let's see if we can transform the test a bit. It looked like this before:

```
[Test]
public void CantExceedMaxAmountForOrder()
{
    Order o = new Order(new Customer());

    OrderLine ol;

    ol = new OrderLine(new Product());
    ol.NumberOfUnits = 2000000;
    ol.Price = 1;
    o.AddOrderLine(ol);

    Assert.IsFalse(o.IsValid);
}
```

As you know by now, I think there are several problems with this snippet. To follow the ideas discussed so far, we could add a transition method to Ordered state; for example, the method could be called OrderNow(). But I would still not be happy with that, because OrderNow() would most probably throw an exception before we get a chance to check.

Again, I'd like to leave the focus of what is persisted and what is not for now. The interesting part here is that when we try to transition to Ordered, we can't do that. Let's reflect that with some changes to the test.

```
[Test]
public void CantGoToOrderedStateWithExceededMaxAmount()
{
    Order o = new Order(new Customer());

    OrderLine ol = new OrderLine(new Product());
    ol.NumberOfUnits = 2000000;
    ol.Price = 1;
    o.AddOrderLine(ol);

    try
    {
        o.OrderNow();
        Assert.Fail();
    }
}
```