
So here the result won't have Customer instances, but CustomerSnapshot instances. For it to work, you need to provide a matching constructor on the Value Object (CustomerSnapshot in the previous case) and to mention CustomerSnapshot in a mapping file via an import directive like this:

```
<import class="CustomerSnapshot" />
```

Note that CustomerSnapshot just holds on to flat data (typically read-only) according to NHibernate. Identities won't be tracked in the Identity Map, and no changes will be tracked in the Unit of Work.

Talking about querying, that's actually exactly what the next category is about as well.

## Advanced Database Support

The examples I provided in Chapter 8 for "advanced database support" (not advanced for a database guy, but perhaps for an object guy) follow:

- Aggregates
- Ordering
- Group by
- Scalar queries

All four of these are supported by both HQL and Criteria objects in NHibernate. Let's take an example of each, beginning with an aggregate query finding the number of instances of Customer. In HQL, it could look like this:

```
//A consumer
string hql = "select count(*) from Customer";
int numberOfCustomers =
    (int)_session.CreateQuery(hql).UniqueResult();
```

## Note

Again, note that it's not table names but classes that are used in HQL.

The second example, to order the result set in the database so that it doesn't have to be done in the Domain Model (which might often be a good thing), could look like this in HQL. In this case we are ordering the fetch operation of all customers by Name.

```
select from Customer order by Name
```

- **What backends are supported?**

  This is a typical example of something that could become a long and tedious feature enumeration, so I won't go into detail here. Let's just say that NHibernate supports several different databases (most of the major commercial and open source databases). Check the site [NHibernate] for current information. You can also write your own plugin if you miss the database you need to work with.

- **Not just an O/R Mapper**

  NHibernate is pretty focused on being an O/R Mapper and nothing else. The philosophy is to do one thing and do it well.

## Note

Of course, NHibernate does other things as well, but those other things are just not the focus. And they are not too many or too big either.

- **Advanced caching**

  Advanced caching is one area where NHibernate isn't really up to par when compared to Hibernate, but I think it's rapidly becoming better. On the other hand, to me that's not usually a big deal. There are many problems with second-level caching, so that option is often ruled out.

- **Advanced support for controlling transactions**

  Support for manual transaction control is pretty good in NHibernate. There are situations where you might be taken by surprise if you don't watch out (for instance, when you execute a query in the middle of a transaction, NHibernate will then `flush()` changes to the database before executing the query). That's a tradeoff between querying not going "through" the cache or ordinary transaction control. The good news is that it's controllable by your code.

  To bind this to Chapter 8, the typical way of dealing with transactions in NHibernate is "manual control."

## Note

On top of that, you can also build something that uses any of the more automatic approaches mentioned in Chapter 8.

- **Open source**

  As I've said already, NHibernate is an open source project, so you can investigate the source code and even build your own branch.

- **Version (generation)**

  It's hard to decide what version NHibernate is in. At the time of writing, it's called version 1 by the team building it, but at the same time, I would say that the quality is higher than with typical first versions. NHibernate is also a port from Hibernate, which is second generation or actually third now, but that's not reflected in NHibernate. Anyway, let's call it generation 1.

Let's have a look at how NHibernate positions itself in the classifications from a totally different angle: the infrastructure patterns angle.

## Another Classification: Infrastructure Patterns

Without further ado, let's get started with type of metadata.

## Metadata Mapping: Type of Metadata

In Chapter 8, I defined three different types of metadata for the Metadata Mapping pattern [Fowler PoEAA]:

- XML document(s) or other document formats
- Attributes
- Source code

This category was simple regarding NHibernate because its metadata is typically XML documents. You can describe the metadata in source code as well in the works, but that's not the mainstream thing to do at all.

There are attribute-based approaches as well, but they generate metadata as XML documents.

## Identity Field

I have already touched on the matter of how you deal with Identity Fields in NHibernate, but I'd like to go a little deeper. Earlier I showed how to map an Identity Field that is of the Guid type. Let's take a look at the Product Entity, which has an int for the Identity Field, and the value is generated with an IDENTITY (auto incrementing column) in the database. It could then look like this:

```
<id name="Id" access="field.camelcase-underscore"
unsaved-value="0" >
    <generator class="identity" />
</id>
```

As I said in Chapter 8, when it comes to new entities, the values for Identity Fields can be generated in at least four different layers:

- Consumer
- Domain Model
- Database
- O/R Mapper

In the case of the guid, you can generate it in all the layers, but it's recommended that you do it in the O/R Mapper. In the example with IDENTITY just shown, the value is generated in the database, and that actually affects the programming model a lot. First, there will be a database jump earlier than you expect. Second, there might be an INSERT just to grab the IDENTITY value. Both examples are something I consider to be problems, and therefore I don't like to use IDENTITY s more than is necessary.

## NHibernate Supports COMBs

As a matter of fact, Guid s are often a very nice solution. But perhaps some of you have read my article about a possible cost of INSERT s when you use Guid s as primary keys [Nilsson COMB]. The problem is that the INSERT throughput might be many times lower for tables with Guid s for primary keys than if you use int s. That's not a problem you will typically get, but it might come and bite you if you have very large tables and a high INSERT load. I suggested a solution to the problem in the article I called "COMB." It's basically a Guid , but kind of a sequential one. I was very surprised to see that NHibernate added support for COMB in a specific alpha version. To use the COMB generator, the metadata could look like this (the only difference is that generator is guid.comb and not just guid ):

```
<id name="Id" access="field.camelcase-underscore"
unsaved-value="00000000-0000-0000-0000-000000000000" >
    <generator class="guid.comb" />
</id>
```

It is easiest for you if you let NHibernate generate the Guids for you, but that's not always possible, of course. Sometimes you must use assigned Identity Fields instead, which makes it quite a bit harder. For example, you can't let NHibernate determine using UPDATE or INSERT by looking at unsaved-value . Instead, you will typically tell NHibernate what to do with explicit calls to Save() or Update() instead of SaveOrUpdate() .

## Note

As I said earlier in this chapter, you can use the version tag-unsaved-value tag for helping you out when you prefer to set the Identity Field values on your own.

These were just a few examples of strategies for Identity Fields. NHibernate supports many more. You can also plug in your own strategies quite easily.

## Foreign Key Mapping

