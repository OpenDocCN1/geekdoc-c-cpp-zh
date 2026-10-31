
notifying the Unit of Work that there is a new instance for persisting at next `PersistAll()` call. I’m referring to the life cycle I want to have for a persistent instance (I touched on this in Chapter 5, so I won’t repeat it here).

What I think is worth pointing out is that if I expect it to be enough to associate the Aggregate root with the Unit of Work, the instances that are part of the Aggregate and that the Aggregate root reaches will get persisted to the database as well when we say `PersistAll()`.

Again, Aggregates assist us well; they provide a tool for knowing the size of graph that will be persisted because the Aggregate root is marked for being persisted. Again, Aggregates make for simplification.

## Note

O/R Mappers are often able to be configured for how far the reach of persist by reachability should go. But even when they are configured that way, the Aggregates are a very good guide in my opinion. What I mean is that I use the Aggregates for determining how far the reachability should reach, when I do the configuration.

Let's take a closer look at the reasoning behind the decisions discussed so far.

## Reasons for the Decisions

Why did I choose as I did? First, I want to use the Unit of Work pattern. I want its characteristics: to create a logical Unit of Work.

So you can make lots of changes to the Domain Model, collect the information in the Unit of Work, and then ask the Unit of Work to save the collected changes to the database.

There are several styles of Unit of Work to use. The one I prefer is to make it as transparent as possible for the consumer and therefore the only message needed is to say `Add()` to the Repository (which in turn will talk to the Unit of Work).

If the reconstitution is done via the Repository, the Unit of Work-implementation can inject some object that can collect information about changes. Otherwise, there can be a snapshot taken at read time that will be used to control the changes by the Unit of Work at persist time.

I also chose to control save or not save (`PersistAll()`) outside of the Repositories. In this particular example, I could just as well have had `PersistAll()` directly on the `CustomerRepository`, but I chose not to. Why? Why not let Repositories hide Unit of Work completely? Well, I could, but I often find that I want to synchronize changes to several Aggregates (and therefore also to several different Repositories) in a single logical unit, and that's the reason. So code like this is not only possible to write, but also very typical:

```csharp
Customer c = new Customer();
_customerRepository.Add(c);
Order o = new Order();
_orderRepository.Add(o);

_ws.PersistAll();
```

One alternative might be the following:

```csharp
Customer c = new Customer();
_customerRepository.Add(c);
_customerRepository.PersistAll();

Order o = new Order();
_orderRepository.Add(o);
_orderRepository.PersistAll();
```

But then I have two different Unit of Work instances and two Identity Maps (it doesn't have to be that way, but let's assume it for the sake of the discussion), which can give pretty strange effects if we aren't very careful. After all, all five lines in the first example were one scenario, and because of that I find it most intuitive and appropriate to treat it like one scenario regarding how I deal with the Unit of Work and Identity Map as well. I mean, the scenario should just have one Unit of Work and one Identity Map.

Another thing that might be a problem is that when the Repository hid the Unit of Work it probably meant that there were two database transactions. That in turn means that you might have to prepare to add compensating operations when the outcome of a scenario isn't as expected. In the previous case, it's probably not too disastrous if the Customer is added to the database but not the Order. However, it can be a problem, depending upon your Aggregate design.

That said, Aggregates "should" be designed so that they are in a consistent state at PersistAll() time. But the loose relationship between Aggregates doesn't typically live under such strict requirements. That might make you like the second solution. On the other hand, the second solution would store two totally unrelated customers in the same PersistAll() if both of those customers were associated to the Repository. That is actually less important than grouping a customer and its orders together. Aggregates are about objects, not classes.

What speaks for the solution in the second example is if one Aggregate comes from one database and the other Aggregate is stored in another database at another database server. Then it's probably easiest to have two Unit of Work-instances anyway, one for each database. So, solution two is slightly less coupled.

## Note

I could even let Add() fulfill the transaction, but then I have different semantics from those I have discussed and expressed so far. It would be crucial to call Add() at the right point in time. This is less important with the solution I have chosen, as long as the call is done before PersistAll().

With `Add()` fulfilling the transaction, it would also mean that it's certainly not a matter of "gather all changes and persist them all at `PersistAll()`," which again is very different from my current solution.

While we're at it, why not then encapsulate the whole thing in the Entity instead so that you can write the following code?

```csharp
Customer c = new Customer()
c.Name = "Saab";
c.Save();
```

I think it's moving away from the style I like. I think it breaks the *Single Responsibility Principle* (SRP) [Martin PPP], and it's low PI-level. I think I'm also moving into "matter of taste" territory.

I also have a problem with inconsistency if one save goes well and others do not. (You could argue that physical transaction and Unit of Work don't have to be the same, but that increases complexity in my opinion. The way I see it is if you don't have to do something, you shouldn't.)

However, by using my favorite technique, there's nothing to stop me from getting the same effects of storing one Aggregate at a time if I really want to by letting the Repositories hide the Unit of Work and Identity Map. It could then look like this:

```csharp
Customer c = new Customer();
_customerRepository.Add(c);
_ws1.PersistAll();

Order o = new Order();
_orderRepository.Add(o);
_ws2.PersistAll();
```

## Note

For the previous scenario, the end result would be the same with a single `_ws`, but that depended on the specific example.

What I mean is that I can have one Unit of Work/Identity Map when I so wish, and several when I so wish. I think this is slightly more flexible, which I like a lot, and this is one more reason for my choice; namely that I currently prefer to see the Unit of Work as something belonging to the consumer of the Domain Model (that is the Application layer or the presentation layer) rather than the Domain Model itself.

If we assume that each Repository has its own Identity Map, it can get a bit messy if the same order is referenced from two different Repositories, at least if you make changes to the same logical order (but two different instances) in both Repositories.

As far as risks are concerned, what it boils down to is which risk you prefer. The risk of committing instances that you weren't done with because a `PersistAll()` call will deal with more instances than you expected? Or the risk of forgetting to commit a change because you'll have to remember what Repositories to ask to do `PersistAll()`.

I'm not saying that it's a solution without problems, but again, I prefer the Identity Map and the Unit of Work to belong to the scenario.

## Note

Deciding on what programming model you want is up to you, as usual. There are pros and cons to each.

I have mentioned Unit of Work and Identity Map together over and over again. It's such a common combination, not only in my text, but in products as well. For example, there is Persistence Manager in JDO [Jordan/Russell JDO] and Session in Hibernate [Bauer/King HiA].

I thought it might deserve a pattern, and I was thinking about writing it up, but when I discussed it with Martin Fowler he notified me that he discusses that in [Fowler PoEAA] when he talks about Identity Map and Unit of Work. That's more than enough, so I decided not to repeat more about that.

OK, now there's been a lot of talk and no action. Let's start building the Fake mechanism and see where we end up.
