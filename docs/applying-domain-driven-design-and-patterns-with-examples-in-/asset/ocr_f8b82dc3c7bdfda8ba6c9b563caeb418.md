> > both because it makes usage of the full power of object orientation possible and because it is easier to be true to the domain. Usage of the Domain Model pattern isn't without problems, of course. A typical one is the steep learning curve for being able to use it effectively.

# Domain-Driven Design Focus

The real eye-opener for me regarding the usage of use cases was *Domain-Driven Design* (DDD) [Evans DDD]. (We will talk a lot about DDD soon, but for now, let’s just say it’s about focusing on the domain and letting it affect the software very much.) I still think that the use case technique is a great way of communicating with users, but DDD has made me think it can help a lot if we can manage to actively involve the users in discussions about the core model. It can head off mistakes very early and help the developers understand the domain better.

# Note

"Model" is one of those extremely overloaded terms in software. I think we all have an intuitive idea about what it is, but I'd like to describe how I think about it. Instead of trying to come up with *the* definition, here in all simplicity (this could fill a book of its own by the right author) are a few properties of a model that you can compare to your own understanding of the term. A model is

+   - Partial
+   - For a certain purpose
+   - A system of abstractions
+   - A cognitive tool

Also,

+   - A model has several presentations (for example: language, code, and diagrams).
+   - There are several models in play in a system.

If you would like to read more, very much has been written about what a model is. A good place to start is the first pages in Eric Evans’ book [Evans DDD]. (A special thanks to Anders Hesselund and Eric Evans for inspiration.)

The model is a great tool for communication between developers and users, and the better the communication is between those groups, the better the software will become, both in the short and the long run.

We (including me) have been using models forever, of course, but the difference between one of my old models and those that have been built with the ideas of DDD is that my old models had