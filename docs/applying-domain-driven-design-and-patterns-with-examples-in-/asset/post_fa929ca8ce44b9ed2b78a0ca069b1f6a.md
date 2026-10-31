
This was a change that was very much needed for the infrastructure and is therefore a typical example of a distraction. It was not anything I did for the sole purpose of just one specific O/R Mapper, but rather as a simplification for more or less all O/R Mappers.

### Note

It's ironic. When we built Valhalla, we decided that using Guids should be compulsory. We weren't altogether happy with that decision because it put a "must" on the developer, and it was on our list for future changes. Now when I'm using other persistence frameworks, I'm free to choose. Nevertheless, I still think it's often a good idea to use a Guid as the Identity Field.

Let's get back to the metadata with another example of what it contains.

## Foreign Key Mapping

Another thing that typically appears in metadata is the Foreign Key Mapping pattern [Fowler PoEAA]. It's a description of the foreign keys and the related associations in the Domain Model.

Unlike the Identity Fields, this isn't about copied values in the Domain Model. Instead, it's just a metadata thing.

There are a variety of relationships that can be used, and the ones that are supported by the O/R Mappers can differ quite a lot. In my experience, most of the time you will only use relatively few types of relationships, but when you need something more esoteric, you are glad if you find support for it.

## Embedded Value

One very important way of bridging the Impedance Mismatch is the possibility of having coarse-grained tables and fine-grained classes in the Domain Model. That's where the Embedded Value pattern [Fowler PoEAA] comes in.

It means that you should be able to store a customer in a single Customers table in the database, but work with the customer as a Customer object and an Address object in the Domain Model. (This example was very simplistic; in reality, the difference is often very large.)

In the simplest form (let's call it level one), you are able to just describe the relationship between the Embedded Value and the columns in the database table. Level two is where you might have to write assisting code that helps out with the translation for advanced cases.

## Inheritance Solutions

Inheritance hierarchies in the Domain Model don't have a perfect match in the relational database because inheritance isn't a relational database concept (at least not before SQL:1999, which few database products support at the time of this writing). Furthermore, inheritance in the Domain Model is probably less commonly used than many would expect. That said, when you need to use it, you should be able to support it with the O/R Mapper.

There are three different type solutions to the problem. They are Single Table Inheritance, Class Table Inheritance, and Concrete Table Inheritance [Fowler PoEAA]. I have chosen to group them together because they are just different solutions to the same problem.

The main difference is regarding how many tables are used for storing an inheritance hierarchy. Assume `Person` as base class and `Student` and `Teacher` as subclasses. Then the different patterns will lead to the following typical tables, as shown in Table 8-3. From there you can probably easily deduce what columns will go where.

### Table 8-3. Patterns for Persistence of Inheritance Hierarchies and What Tables Are Needed

| Pattern | Tables in the Database |
|---|---|
| Single Table Inheritance | `People` |
| Class Table Inheritance | `People, Students, Teachers` |
| Concrete Table Inheritance | `Student, Teachers` |

If the O/R Mapper only supports one of those, your flexibility in the database design has decreased compared to if you had all three from which to choose. You have to decide whether that's important or not.

## Identity Map

In my early attempts to create an O/R Mapper, I first thought I could skip the Identity Map, but I came to the conclusion that it gets too complex and there is too much responsibility for the consumer programmer.

On the other hand, a lot also depends on your Domain Model design. If you never have relationships between entities in different Aggregates, the need for the Identity Map decreases. So DDD ideas, such as simplification and decoupling within the Domain Model, make it easier to live life without an Identity Map. That said, I still think it's useful to have an active Identity Map.

### Note

If you think about O/R Mapping as a work horse that goes between database and object, the Identity Map might not be important. But that's not what we are talking about here, because then we would need to do more work. Here we'd like to just support the Domain Model with as simple (or rather as good) a solution as possible.

The Identity Map can be used for other things as well and not only for controlling the object graph the consumer knows about. For instance, it can be used for dealing with building M:N relationships of objects in the Domain Model when reading from the database.

### Note

M:N describes the relationship regarding cardinality/multiplicity between objects by saying it is many-to-many. For example, a house has many people staying there, and at the same time every person can own several houses.

It's also often considered a cache for performance reasons, but as you know, I'm not overly cache-friendly, so I see the Identity Map as a convenience for the programming model rather than as a means to improve performance.

Different O/R Mappers differ regarding what "session" level you can/must have the Identity Map for. It can be machine, a process, and/or a session.

Another pattern often goes hand in hand with the Identity Map. I'm thinking about Unit of Work.

## Unit of Work

Most O/R Mappers use, or at least have support for, the Unit of Work pattern. The main difference is really how transparent the Unit of Work is for the consumer. Where the O/R Mapper is of "runtime-Persistence Ignorant" style, the consumer might have to talk to the Unit of Work explicitly for registering a new instance to be inserted at next persist. Other O/R Mappers are more transparent, but then you probably will have to instantiate with a factory supplied by the O/R Mapper. There are pros and cons to these approaches.

The "session" level might also differ for the Unit of Work, at least in theory, just as I said for the Identity Map.

## Lazy Load/Eager Load

I've said before that my Domain Model style isn't using Lazy Load [Fowler PoEAA] a lot within my Aggregates [Evans DDD]. Even so, it's a piece of the puzzle that we need to have in the persistence infrastructure, and we need to be able to use it as an optimization.

Instead, as the default strategy for my Aggregates, I use load eagerly. Or aggressively, or greedily, or span loading, or pre-load, or whatever you like to call it. I will from now on call it Eager Load.

Eager Load is pretty much the opposite of Lazy Load; you load the complete graph immediately instead of delaying loading parts of the graph until later.

As I see it, Eager Load goes hand in hand with Aggregates [Evans DDD], at least as the default solution.

### Note

To some I might have put too much emphasis on Aggregates when it comes to reading scenarios. I have been using Aggregates as the default load scheme and optimized when I have found the need for it.

After all, Aggregates are most important for write scenarios. When seeing it that way, adding a need for something like a `GetForWrite()` to the protocol before making changes to an Aggregate instance might make sense. The `GetForWrite()` would load everything from the Aggregate, possibly with read consistency.

If you do have a concept that is spanning many instances and you want to treat it as a unit, Aggregates is the thing, and it has implications.

I also think the read-only/writable distinction is often something nice for users, who have to actively choose to move into write mode. Another good thing about it is that the user won't start making changes to an already stale object when optimistic concurrency control is used, which means that the risk of collisions becomes smaller. This approach also translates nicely to pessimistic concurrency control schemes.

There are many different implementation variants for Eager Load. It's often solved with `OUTER JOINS` in SQL, and the resultset is then broken down to the graph. The other most common solution is to batch several `SELECT` statements after each other.

A competent O/R Mapper should support both Lazy Load and different Eager Load strategies, which goes both for lists and single instances. It may even apply for Lazy Loading groups of fields of a single instance, even if I don't consider that crucial. Such a group of attributes could always be factored out into a Value Object instead, which would make a lot of sense in most situations. And then we are back to Lazy Load/Eager Load of instances again.

## Controlling Concurrency

As I've said several times already, the Aggregate pattern is a good tool for controlling concurrency. Thanks to it, I get the unit I want to use and work with as a single whole. Yet that's not the complete solution. I also need to avoid collisions or detect whether collisions have occurred so that
