![](bbox=[0.358, 0.074, 0.638, 0.196])

This might grow on me, but right now I prefer the more specific interface in Figure 5-8, as it clearly states exactly what is needed. The generic `IRepository` requires more casts when being used and might be incorrectly trying to gather all upcoming Repositories in one and the same shape.

Another solution might be to use generics in the `IRepository`-interface + a base class and thereby at least get the type safety (and avoid code duplication) and avoid extra type casts. One problem then is that I might add a `Delete()` method to the Repository, even though not all Repositories will need it. And even with generics, the `GetListByParent(parent)` is troublesome because what if an Entity has several parents? Well, it's an early sketch and that can be solved of course. But I can't help thinking that it's better to let the code "speak as clearly as possible for now" and skip generalizations like that. It's just not feeling important yet. As usual, no decisions are carved in stone. I can challenge the decisions again later on when I can more easily see what pieces can be generalized, but for now, I'll stay with `OrderRepository`.

Because of that, I rename the `OrderRepository` class to `OrderRepositoryFake` and let the class implement the `IRepository`. I also need to change the `[SetUp]` code in my test class. It currently looks like this:

```
```text
//A test class, the [SetUp]

_repository = new OrderRepository();
```
```

**It could now look like this:**

```
```text
//A test class, the [SetUp]

_repository = new OrderRepositoryFake();
```
```

The declaration of `_repository` must use `IOrderRepository` as the type.

And the tests still work.

I guess pure XP'ers would groan a little bit at the refactoring I just did. I actually didn't have to make that change now; it was a change for preparing for the future, when I need a real Repository instead of the faked one. OK, I can agree with that, but I can't help thinking a little bit about the future (read: later chapters) when I will be hooking in infrastructure.

I cross my fingers that this preparation will prove to be good. I fell back into old habits of early guessing.... On the other hand, we are of course free to choose our own balance and don't have to