This way, during test execution it will be clearly signaled that it’s just a temporary ignore.

Finally, if you "never" plan to support the test in the subclass, you can write it like this in the subclass:

```
```csharp
[Test]
public override void CanAddCustomer()
{
    Console.WriteLine
        ("CanAddCustomer() isn't supported by Fake.");
}
```
```

OK, you still can forget a test if you do your best. You'd have to write code like this, skipping the `Test`-attribute:

```
```csharp
public override void CanAddCustomer() { }
```
```

There's a solution to this, but I find the style I have shown you to be a good balance of amount of code and the risk of "forgetting" tests.

I know, this wasn't YAGNI, because right now we don't have any implementation other than the Fake implementation, but see this just as a quick indicator for what will happen later on.

# Note

This style could just as well be used in the case of multiple implementations for each Repository.

For many applications, it might be close to impossible to deal with the whole system in this way, especially later on in the life cycle. For many applications, it's perhaps only useful for early development testing and early demos, but even so, if it helps with this, it's very nice. If it works all the way, it's even nicer.

In real life, the basics (there are always exceptions) are that I'm focusing on writing the core of the tests against the Fake implementation. I also write CRUD tests against the Fake implementation, but in those cases I also inherit to tests for using the database. That way, I test out the mapping details.

That said, no matter if you use something like the ideas of the abstraction layer or not, you will sooner or later run into the problems of database testing. I asked my friend Philip Nelson to write a section about it. Here goes.

![](bbox=[0.11, 0.806, 0.186, 0.823])

![](bbox=[0.833, 0.806, 0.907, 0.823])