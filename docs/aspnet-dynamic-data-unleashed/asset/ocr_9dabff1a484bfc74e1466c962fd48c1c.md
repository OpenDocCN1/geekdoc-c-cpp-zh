the business logic in multiple applications. Separation of business logic from presentation is especially important in ASP.NET Dynamic Data applications. Because virtually the entire user interface of a web application can be generated dynamically, embedding the business logic directly in the web pages of the application is not only less attractive but also more cumbersome. To take advantage of the productivity improvements Dynamic Data offers, you as a web developer need to know how to implement business logic *outside* of the web pages.

# Entity Design

Entities are abstractions of things in the business domain. They are implemented as classes in the application and as tables in the database. Although some similarities exist (class properties are similar to table columns for instance), the object-oriented and relational models are very different. The ADO.NET Entity Framework, LINQ to SQL, and other frameworks attempt to bridge the gap between these two radically different ways of representing information by implementing object-relational mapping.

Good entity design requires application of both object-oriented and relational design principles. It would be foolish to try addressing both of these vast topics in this chapter, or even in this book. It is assumed that you already know how to create a class that represents a real-world object or person and use encapsulation and abstraction principles to expose its key attributes as properties. It is also assumed that you know how to create a table to store this information in the database and use normalization techniques to reduce duplication. With these assumptions in mind, this section focuses on practical application of the object-oriented and relational design principles and some of the common pitfalls developers encounter with the Entity Framework.

# Measure Impact of Inheritance on Query Performance

Inheritance is one of the most powerful concepts in object-oriented design, allowing a much higher level of reuse and encapsulation than the relational model provides. With the Entity Framework supporting *table-per-type*, *table-per-type*, *table-per-concrete type*, and *table-per-hierarchy* methods of mapping class hierarchies to database tables, using inheritance in your entity model becomes a very attractive option.

Beware! Although the Entity Framework makes LINQ queries over type hierarchies look deceptively simple, there are significant performance costs associated with the use of inheritance in your conceptual model. Consider the conceptual model shown in Figure 9.1, where you have an abstract base class called User and two concrete classes inheriting from it—Customer and Employee. The Entity Framework allows you to select both Customer and Employee entities by writing a simple LINQ query like this:

```
```csharp
var users = from u in context.Users
            select u;
```
```