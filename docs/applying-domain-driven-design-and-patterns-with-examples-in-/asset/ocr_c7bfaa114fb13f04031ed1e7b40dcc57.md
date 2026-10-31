order (but two different instances) in both Repositories.

As far as risks are concerned, what it boils down to is which risk you prefer. The risk of committing instances that you weren't done with because a `PersistAll()` call will deal with more instances than you expected? Or the risk of forgetting to commit a change because you'll have to remember what Repositories to ask to do `PersistAll()`.

I'm not saying that it's a solution without problems, but again, I prefer the Identity Map and the Unit of Work to belong to the scenario.

# Note

Deciding on what programming model you want is up to you, as usual. There are pros and cons to each.

I have mentioned Unit of Work and Identity Map together over and over again. It's such a common combination, not only in my text, but in products as well. For example, there is Persistence Manager in JDO [Jordan/Russell JDO] and Session in Hibernate [Bauer/King HiA].

I thought it might deserve a pattern, and I was thinking about writing it up, but when I discussed it with Martin Fowler he notified me that he discusses that in [Fowler PoEAA] when he talks about Identity Map and Unit of Work. That's more than enough, so I decided not to repeat more about that.

OK, now there's been a lot of talk and no action. Let's start building the Fake mechanism and see where we end up.