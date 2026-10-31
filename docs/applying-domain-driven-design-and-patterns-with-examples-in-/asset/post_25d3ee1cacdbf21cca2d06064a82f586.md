
we don't get inconsistent data (and *especially* not without being notified).

From [Fowler PoEAA], we find the following solutions to the problem:

- **Coarse-Grained Lock**
  
  Instead of locking on the instance level, this pattern suggests locking a more coarse-grained unit. We can, for example, use it on the Aggregate root level, thereby implicitly locking all the parts of the Aggregate.
  
- **Optimistic Offline Lock**
  
  *Expect no conflict, but check before commit.*
  
- **Pessimistic Offline Lock**
  
  *Prevent conflicts by an exclusive check-out mechanism.*

This reminds me that I now want to add some versioning information to the Domain Model as a way of stating where we need to deal with controlling concurrency, for dealing with feature 4, "Concurrency conflict detection is important." I think my Aggregate roots should get a `Version` field to support Optimistic Offline Lock. It's *not* an automatic action. Instead, you add it where you need it. You'll find the change in *Figure 8-2*.

## Figure 8-2. Added Version fields to some of the Aggregate roots

![](img/89fb3513cb9b6343875aadbfd042005d_331_0.png)

It's not too much of a problem if your O/R Mapper doesn't support Pessimistic Offline Lock. First of

## Summary

Now we have discussed the need for persistent infrastructure to some extent. After having introduced the subject and defined some requirements on the needed persistent infrastructure, we discussed the subject from different angles such as classifications and some of the PoEAA patterns.

But the whole discussion was pretty abstract. Some examples would help make it more concrete. That's the intention of the next chapter. There we will use NHibernate for the examples.

## Why NHibernate?

You might wonder why I chose NHibernate. Well, it's not because NHibernate is necessarily the best solution available. What is the best car? That's a silly question, right? It's always the standard answer: "It depends."

These are my motivations for choosing NHibernate for this chapter:

- **Java heritage**
  
  NHibernate is a port of the popular Hibernate [Hibernate]; therefore, many people know it, and there are a great deal of books and lots of other resources available for it. Furthermore, Object Relational Mapping is pretty mature in Java-land, contrary to .NET-land.
- **Open source**
  
  NHibernate is open source, and that makes it very approachable and easy to try.

In no way is this chapter intended to be an exhaustive guide to NHibernate. The purpose is just to make the discussions in Chapter 8 less abstract. I will also avoid getting into enumerating feature after feature; that's not very interesting, and that aspect of this book wouldn't be current for more than a few weeks after writing this chapter.

A possible effect, although not one of my main intentions, might be that the chapter could easily be written for any other Persistence Framework as well, therefore making it a little easier to compare different solutions. Let's see if that happens. (Hopefully there will then be a separate section entitled "What else should have been included in the comparison?")

I will also not be discussing NHibernate in the context of an abstraction layer, such as NWorkspace [Nilsson Workspace]. The focus here will be on NHibernate itself and its API.

Let's start with an introduction to NHibernate.

## A Short Introduction to NHibernate

What we are about to discuss here is a product that deals with Metadata Mapping [Fowler PoEAA], an O/R Mapper, which is called NHibernate.

As I said, NHibernate is a port from the very popular O/R Mapper in Java-land called Hibernate, originally created by Gavin King [Bauer/King HiA]. The port is based on version 2.1 of Hibernate, which is considered a pretty old version, but the port doesn't strictly just move the code base for that particular Hibernate version. Instead, features from later versions of Hibernate as well as other features have been added here and there.

NHibernate (and Hibernate) is open source. As I write, NHibernate is released as version 1.0. You can download it from here: [NHibernate].

The proof of the pudding is in the eating, so let's see how NHibernate is used.

## Preparations

Let's assume you have a Domain Model and you now want to write some consumer code against the Domain Model.

## Note

One more requirement is that you want to make the Domain Model persistent. Therefore, you also have a database product, but don't think about the database schema for the moment.

First, you need to set a reference in the consumer to the NHibernate framework (namely nhibernate.dll). That wasn't too hard.

Then you need to configure the usage of NHibernate in the consumer of the Domain Model. You can either do that in code or in a .config file. Typically a .config file is used, so let's assume that. Some things that are configured can be what the database product in question is, the connection string to the database, and logging. You will find lots of examples of .config files to copy and paste from at the NHibernate site, so I won't go into detail here, but I'll just take it for granted that you have a suitable .config file in place.

What you then try to do just once per application execution is to set up a SessionFactory. The reason for not creating several is that the cost is fairly high. The SessionFactory will analyze all metadata and build up memory-based structures for that. As you might guess from its name, the SessionFactory is then used for instantiating new instances that implement ISession.

ISession is the thing to pull in order to get work done against the database and is also the interface that you will interact with all the time from the consumer perspective.

Next, it's nice if you can use a helper for the ISession management. This can be done with different levels of sophistication, but here a simple attempt would be good enough for our purpose. If we assume that our Domain Model is called ADDP.Ordering.DomainModel, a simplified helper called NHConfig could look like this:

```
```csharp
public class NHConfig
{
    private static ISessionFactory _sessionFactory;

    static NHConfig()
    {
        Configuration config = new Configuration();
        config.AddAssembly("ADDP.Ordering.DomainModel");
        _sessionFactory = config.BuildSessionFactory();
    }

    public static ISessionFactory GetSessionFactory()
    {
        return _sessionFactory;
    }
}
```
```

Making more assumptions, we are now working with a rich client application; therefore, we think it's enough to have a single ISession instance. At least, let's start that way. Then the following code might be suitable for the start of the application, or perhaps for a single form:

```
```csharp
_session = NHConfig.GetSessionFactory().OpenSession();
_session.Disconnect();
```
```

So when you want to get an ISession to act on, you can use the following little snippet over and over again:

```
```csharp
_session.Reconnect();

//Do stuff...

_session.Disconnect();
```
```

And finally, when the application terminates (or the form is closed, depending upon your chosen strategy), you close the ISession like this:

```
```csharp
_session.Close();
```
```

With that in place, I can regenerate the development database as often as I like, even before every test execution (if it's not becoming too slow).

Let's take it piece by piece. First, you need to describe the document, something like this for

```
Customer.hbm.xml:

<?xml version="1.0" encoding="utf-8" ?>
<hibernate-mapping xmlns="urn:nhibernate-mapping-2.0"
        namespace="ADDP.Ordering.DomainModel"
        assembly="ADDP.Ordering.DomainModel">
```

I provided the `namespace` and `assembly` tags here, so the rest of the mapping information can be expressed less verbosely because that information won't have to be repeated.

## Note

If you want the metadata to be within the assembly, don't forget to set the property of the XML file to be an Embedded Resource.

Then you describe the name of the class for the Entity and the name of the table. For example, like this:

```
<class name="Customer" table="Customers">
```

Then you describe the Identity Field [Fowler PoEAA], not only the name in the class and the table (in the upcoming example the property name and the column name are the same, so the `column` tag isn't needed), but also the strategy that is used for creating a new value. It could look like this:

```
<id name="Id" access="field.camelcase-underscore"
        unsaved-value="00000000-0000-0000-0000-000000000000" >
        <generator class="guid" />
</id>
```

In this specific example, a `guid` is generated by NHibernate when a new instance is associated with the `ISession`.

Then the simple properties are mapped, such as `Name`, like this:

```
<property name="Name" type="AnsiString" length="100"
        not-null="true" />
```
