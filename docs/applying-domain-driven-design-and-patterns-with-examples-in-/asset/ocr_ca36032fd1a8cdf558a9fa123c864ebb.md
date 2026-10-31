The Register() method on NewOrder is also pretty simple. At least it can focus on its own state, and that makes the code clean and clear. It could look like this:

```
public void Register()
{
    _parent._Register();
    _parent._currentState = new Registered(_parent);
}
```

Before changing the state, there was kind of a callback to the parent (_parent._Register()) telling it to do its thing before the state was changed. (Note that the "callback" went to the internal method _Register() and not the public Register().) This is just one example of an option, of course. Other examples would be to put the code in the OrderState base class or in the NewOrder class itself. It should go wherever it's best located.

As you saw, if I want to do things before or after the state transformation, it's simple and very well encapsulated. If I want to disallow a certain transformation in the NewOrder class, I just skip implementing that method and use the implementation of the base class OrderState for that method. The implementation of the base class throws an exception saying it was an illegal state transformation, if that's the wanted behavior. Another typical default implementation is to do nothing.

# Note

If you need more context-aware exceptions, you can of course implement the methods in the subclasses just as well, even if all they will do is raise exceptions.

This also implies that instead of using a base class for OrderState you could use an interface instead. I guess that if the GoF book had been written today, many of the patterns would have used interfaces instead of (or at least together with) abstract base classes. The State pattern isn't the most typical example of this, but it still is a possible example.

# More Comments

When using the State pattern, we were actually swapping a single field into a bunch of separate classes. That doesn't sound like a very good idea at first, but what we then get is the nice effect of moving the behavior to where it belongs and good alignment to the Single Responsibility Principle (SRP).

There are drawbacks, of course, and a typical one is that the program can potentially be flooded with small classes when we use a solution such as State.

Which solution you prefer is indeed up for debate, but I think the State pattern is one that should be seriously considered here. You might find that it solves your problem with the least amount of