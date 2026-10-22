Scopes can also be combined. Finding the last week's worth of orders that were paid by check is just as easy:

```
orders = Orders.checks.last_n_days(7)
```

In addition to making your application code easier to write and easier to read, named scopes can make your code more efficient. The previous statement, for example, is implemented as a single SQL query.

Anonymous scopes can be created using the scope named scoped:

```
in_house = Orders.scoped(:conditions => 'email LIKE "%@pragprog.com"')
```

Of course, anonymous scopes can also be combined:

```
in_house.checks.last_n_days(7)
```

Scopes aren't limited to conditions; we can do pretty much anything we can do in a find call: :limit, :order, :join, and so on. Just be aware that Rails doesn't know how to handle multiple order or limit clauses, so be sure to use these only once per call chain.

Rails even provides a scope named all, which is functionally equivalent to find(:all).

# Reloading Data

In an application where the database is potentially being accessed by multiple processes (or by multiple applications), there's always the possibility that a fetched model object has become stale—someone may have written a more recent copy to the database.

To some extent, this issue is addressed by transactional support (which we describe on page 418). However, there'll still be times where you need to refresh a model object manually. Active Record makes this easy—simply call its reload method, and the object's attributes will be refreshed from the database:

```
stock = Market.find_by_ticker("RUBY")
loop do
  puts "Price = #{stock.price}"
  sleep 60
  stock.reload
end
```

In practice, reload is rarely used outside the context of unit tests.

# Updating Existing Rows

After such a long discussion of finder methods, you'll be pleased to know that there's not much to say about updating records with Active Record.

If you have an Active Record object (perhaps representing a row from our orders table), you can write it to the database by calling its save method. If this object