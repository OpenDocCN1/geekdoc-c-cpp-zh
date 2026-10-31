When I talk about cache here, I'm mostly thinking about the Identity Map [Fowler PoEAA].

Let's focus some more on transitions.

# Trying to Transition when We Shouldn’t

I used different states for increasing the fulfillment of the "always savable" principle before. But a
"critical" passage is when the user wants to make a transition in the state graph. Sure, we could
deal with this in a similar way to what we discussed before so that we move to a temporary state
and then a Service takes responsibility for moving to the real state or to a failure state. I guess
there are situations where this makes sense, but for feature 11, "Orders have an acceptance status
that is changed by the user," it might just feel ridiculous, depending on what the context is.

# Note

Did you notice how it all came together? I talked about `OrderNow()` before, and that might
have seemed to be kind of a technical solution to the problem of "always savable," but it
was core to the requirements. And according to the requirements, `Accept()` might make
more sense.

OK, "ridiculous" is too strong a word, but if we assume that the rules for checking are just a couple
of simple constraints without the cross Aggregate broader problems, I would prefer to apply the
principle discussed earlier: that is, letting the user make a proactive check, and if the result is
positive, the state-changing method will execute successfully. A picture, I mean code, says more
than a thousand words:

```
```csharp
[Test]
public void CanMakeStateTransitionSafely()
{
    Order o = new Order(new Customer());

    Assert.IsTrue(o.IsOKToAccept);

    //We can now safely do this without getting an exception...
    o.Accept();
}
```
```

Checking the `IsOKToAccept` property is optional, but not doing it and then calling `Accept()` at a time
when we shouldn't is exceptional, and we will get an exception. Exceptions are for exceptional
problems; for "expected problems" `bool` is fine.

We often don’t just wonder if it will be OK or not, but we also want to get a list of reasons why it's