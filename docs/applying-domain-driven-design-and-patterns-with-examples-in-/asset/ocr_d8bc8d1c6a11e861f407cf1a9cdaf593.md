# Note

Evans talks a lot about this too... [Evans DDD]. There is a splendid explanation for this, so be sure to read it. The same goes for Jordan/Russell [Jordan/Russell JDO]. JDO has more complex (and flexible) semantics, but of course I might discover later that the simple semantics I sketched previously are not enough.

Don't mix this up with how the infrastructure (for example NHibernate) sees the transient/persistent. What I talk about here is the way I want the life cycle semantics for my Domain Model instances. It's then up to the infrastructure to help me with the wanted semantics behind the scenes. This will be discussed a lot more in later chapters.

Talking about the infrastructure, the hawk-eyed reader might wonder what I meant with `x.Persistent()` in [Table 5-1](#). I tried to symbolize that unknown infrastructure with x. Again, we can forget about that for now.

Back to feature 2, listing orders for a customer. The next sub-feature was that an order must have an ordertype.

# Type of Order

A simple solution here would be to add an `OrderType` instance to each `Order`, as shown in [Figure 5-14](#).

![](bbox=[0.33, 0.593, 0.592, 0.67])

I considered whether the `OrderType` is really an Entity [Evans DDD], and I don't think it is a Value Object [Evans DDD]. The set of possible values are "global" for the whole application and are very small and static.

I'm probably on the wrong track here. Sure, I could implement `OrderType` as a Value Object, but much is pointing in the direction that an enum is good enough, and especially good enough for now, so I define an `orderType` enum and add such a field to the `Order`.