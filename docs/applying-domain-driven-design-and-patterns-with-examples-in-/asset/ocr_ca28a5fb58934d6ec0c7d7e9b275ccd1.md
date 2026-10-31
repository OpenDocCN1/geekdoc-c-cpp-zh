Add to that metaphor the element that the engine could also be fetched from another location, such as from the shelf of a local or a central stock; that is, an old instance should be reconstituted by fetching it from the database and materializing it. This is totally different from creating the instance in the first place, both for a real, physical engine and for an Order instance in software.

We are close to the pattern solution now. Let's use a solution similar to the second proposal, but factor out the creational behavior into a class of its own, forgetting about the "fetch from database" for now (which is dealt with by another Domain Pattern called Repository, which we will discuss a lot in later chapters).

# Solution Proposal Three

So now we have come to using the Factory pattern as the Domain Pattern. Let's start with a diagram, found in Figure 2-7.

# Figure 2-7. An instance diagram for the Factory pattern

![](bbox=[0.25, 0.58, 0.85, 0.68])

The code could look like this from a consumer perspective to obtain a ready-made new Order instance:

```
anOrder = OrderFactory.Create(aCustomer);
aReservation = OrderFactory.CreateReservation(aCustomer);

aCredit = OrderFactory.CreateCredit(anOldOrder);
aRepeat = OrderFactory.CreateRepeat(anOldOrder);
```

This is not much harder for the consumer than it is using an ordinary constructor. It's a little bit more intrusive, but not much.

In order for the consumer to get to an old Order, the consumer must talk to something else (not the Factory, but a Repository). That's clearer and expressive, but it's another story for later on.

To avoid the instantiation of orders via the constructor from other classes in the Domain Model if the Factory code is in an external class is not possible, but you can make it a little less of a problem by making the constructor internal, and hopefully because the Factory is there, the Domain Model developers themselves understand that that's the way of instantiating the class and not using the constructor of the target class directly.