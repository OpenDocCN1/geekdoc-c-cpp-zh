```
Customer c = new Customer();
c.Name = "Volvo";

_session.Reconnect();
_session.Save(c);
_session.Flush();
_session.Disconnect();
```

In this case, I was specific and told the ISession that it should lead to an INSERT (because I called Save()). I could have called SaveOrUpdate() instead, and then NHibernate would have decided on its own whether it should be an INSERT or an UPDATE. The information used in that case is the value of the Identity Field, and it's compared to what you indicated for unsaved-value in the mapping file ("00000000-0000-0000-0000-000000000000" in the case of Guids). If the Identity Field matches the unsaved-value, it's time for an INSERT; otherwise, it would be an UPDATE.

It is also important pointing out that the INSERT is delayed and won't happen when you say Save(), but rather when you say Flush(). The reason for this is that you should be able to make many changes in the consumer and then get them all persisted together and as late as possible.

Did we succeed in writing to the database? The easiest way to check that is to read the instance back, so let's do that.

# CRUD-R (One): Read One

The second example is to read one instance (row in the database) by its Identity Field. From now on, let's assume that we use the ordinary reconnect/disconnect snippet and just focus on the specific code instead.

As usual, you talk to the ISession instance. You call Load()/Get() and say what type you are looking for and its Identity Field value. It could go like this:

```
Customer c = (Customer)_session.Load(typeof(Customer), theId);
```

But beware. This didn't necessarily prove anything if you didn't close the ISession since the last Flush(), because the ISession will provide you with the instance from the Identity Map [Fowler PoEAA] when you call Load()/Get() instead of going to the database. What you can do to force a database jump (instead of opening a new ISession) is to call Evict() on the instance by saying that you don't want the Identity Map to keep track of the instance any longer. It could look like this:

```
_session.Evict(customer);
```

That was good, but what if you don't know the identity value? Perhaps you only know part of the name of the customer and want to fetch all instances that match that name pattern. This takes us over to the next example, that of read many.