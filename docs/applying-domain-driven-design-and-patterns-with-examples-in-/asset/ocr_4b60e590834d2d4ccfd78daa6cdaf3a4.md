Well, we have already touched on this subject several times in this chapter since `Order` and `Customer` are examples of Entities, but let's take a step back and focus on the concept.

It is important for us to keep track of some things in the domain over time. No matter whether a customer changes name or address, it's still the same customer, and it's something we are interested in keeping track of. On the other hand, if a customer's reference person changes, it is probably not anything we care to keep track of. A customer is a typical example of an Entity [Evans DDD]. Again, an Entity is something we keep track of by identity rather than all its values.

To take an extreme example of something that isn't an Entity, let's think about the integer 42. I don't care about the identity of 42 at all; I only care about the value. And when the value changes, I no longer think it's the 42 that has changed it's a totally new value with no connection to the old one. Forty-two is a Value Object [Evans DDD] and not an Entity.

If we take that extreme example over to our domain, we might be able to say that it isn't interesting for us to track `ReferencePerson` of a `Customer` by identity. It's only interesting for us to track it by value. We'll get back to Value Objects later on in this chapter.

# Note

Of course, what should be tracked by identity and what should just be thought of as values is highly dependent on the domain. Let's take an example. As I said above, I believe that `ReferencePerson` in this application can be dealt with as a Value Object, but if the application is for, let's say, a sales support application for salesmen, perhaps they see `ReferencePerson` as an Entity instead.

# Back to the Flow Again

Unfortunately, the test `CanFindOrdersViaCustomer()` won't execute successfully after I override `Equals`. The reason is that all customers used in the test have the same `CustomerNumber`, that being zero, and therefore I find five `Orders` that have the right `Customer`, not three. We need to change the test a little bit. I create another little helper method called `_FakeACustomer()` like this:

```
//A test class
private Customer _FakeACustomer(int customerNumber)
{
    Customer c = new Customer();

    RepositoryHelper.SetFieldWhenReconstitutingFromPersistence
    (c, "_customerNumber", customerNumber);

    return c;
}
```