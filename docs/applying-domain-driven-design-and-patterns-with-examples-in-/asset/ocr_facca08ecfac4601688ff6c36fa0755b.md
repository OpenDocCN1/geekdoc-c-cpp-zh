Of course, I haven't forgotten the TDD mantra of red, green, refactor, red, green, refactor. I just didn't want to slow down your reading rhythm here.

OK, that works. Let's take a copy of the test (clipboard inheritance), change the name, and expand it a bit:

```
[Test]
public void TryingIdeasWithTheRulesAPI()
{
    Order o = new Order(new Customer());
    o.Note = "012345678901234567890123456789";
    Assert.IsTrue(o.IsValidRegardingPersistence);

    o.OrderDate = DateTime.Today.AddDays(1);
    Assert.IsFalse(o.IsValidRegardingPersistence);

    o.OrderDate = DateTime.Today;
    Assert.IsTrue(o.IsValidRegardingPersistence);

    o.Note += "012345";
    Assert.IsFalse(o.IsValidRegardingPersistence);
}
```

As you saw, I added one more rule stating that the OrderDate can't be a future date, and for some reason (not too much of a stretch) that rule was mandatory regarding persistence.

# Note

To make the OrderDate rule obviously and mandatory connected to infrastructure, it shouldn't be allowed to be smaller/larger than what your database can store in a DATETIME (if there is such a difference for your database).

In order to get a green test, we need to change IsValidRegardingPersistence a little bit, as follows:

```
//Order
public bool IsValidRegardingPersistence
{
    get
    {
        if (Note.Length > 30)
            return false;

        if (OrderDate > DateTime.Today)
```