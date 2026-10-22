
All the aggregation functions take a hash of options, very similar to the hash that can be passed to find. (The count function is anomalous—we’ll look at it separately.)

:conditions
Limits the function to the matched rows. Conditions can be specified in the same format as for the find method.

:joins
Specifies joins to additional tables.

:limit
Restricts the result set to the given number of rows. This is useful only when grouping results (which we’ll talk about shortly).

:order
Orders the result set (useful only with :group).

:having
Specifies the SQL HAVING ... clause.

:select
Nominates a column to be used in the aggregation (but this can simply be specified as the first parameter to the aggregation functions).

:distinct (for count only)
Counts only distinct values in the column.

These options can be combined:

```
Order.minimum :amount
Order.minimum :amount, :conditions => "amount > 20"
```

These functions aggregate values. By default, they return a single result, producing, for example, the minimum order amount for orders meeting some condition. However, if you include the :group clause, the functions instead produce a series of results, one result for each set of records where the grouping expression has the same value. For example, the following calculates the maximum sale amount for each state:

```
result = Order.maximum :amount, :group => "state"
puts result  #=> [["TX", 12345], ["NC", 3456], ...]
```

This code returns an ordered hash. You index it using the grouping element ("TX", "NC", ... in our example). You can also iterate over the entries in order using each. The value of each entry is the value of the aggregation function.

The :order and :limit parameters come into their own when using groups.

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

## Reloading Data

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

## Updating Existing Rows

After such a long discussion of finder methods, you'll be pleased to know that there's not much to say about updating records with Active Record.

If you have an Active Record object (perhaps representing a row from our orders table), you can write it to the database by calling its save method. If this object

## Deleting Rows

Active Record supports two styles of row deletion. First, it has two class-level methods, delete and delete_all, that operate at the database level. The delete method takes a single id or an array of ids and deletes the corresponding row(s) in the underlying table. delete_all deletes rows matching a given condition (or all rows if no condition is specified). The return values from both calls depend on the adapter but are typically the number of rows affected. An exception is not thrown if the row doesn’t exist prior to the call.

```
Order.delete(123)
User.delete([2,3,4,5])
Product.delete_all(["price > ?", @expensive_price])
```

The various destroy methods are the second form of row deletion provided by Active Record. These methods all work via Active Record model objects.

The destroy instance method deletes from the database the row corresponding to a particular model object. It then freezes the contents of that object, preventing future changes to the attributes.

```
order = Order.find_by_name("Dave")
order.destroy
# ... order is now frozen
```

There are two class-level destruction methods, destroy (which takes an id or an array of ids) and destroy_all (which takes a condition). Both read the corresponding rows in the database table into model objects and call the instance-level destroy method of those objects. Neither method returns anything meaningful.

```
Order.destroy_all(["shipped_at < ?", 30.days.ago])
```

Why do we need both the delete and the destroy class methods? The delete methods bypass the various Active Record callback and validation functions, while the destroy methods ensure that they are all invoked. (We talk about callbacks starting on page 407.) In general, it is better to use the destroy methods if you want to ensure that your database is consistent according to the business rules defined in your model classes.

## 18.6 Aggregation and Structured Data

(This section contains material you can safely skip on first reading.)

## Storing Structured Data

It is sometimes helpful to store attributes containing arbitrary Ruby objects directly into database tables. One way that Active Record supports this is by serializing the Ruby object into a string (in YAML format) and storing that string in the database column corresponding to the attribute. In the schema, this column must be defined as type text.

Because Active Record normally maps a character or text column to a plain Ruby string, you need to tell Active Record to use serialization if you want to take advantage of this functionality. For example, we might want to record the last five purchases made by our customers. We'll create a table containing a text column to hold this information:

```
create_table :purchases, :force => true do |t|
  t.string :name
  t.text   :last_five
end
```

In the Active Record class that wraps this table, we'll use the serialize declaration to tell Active Record to marshal objects into and out of this column:

```
class Purchase < ActiveRecord::Base
  serialize :last_five
  # ...
end
```

When we create new Purchase objects, we can assign any Ruby object to the last_five column. In this case, we set it to an array of strings:

```
purchase = Purchase.new
purchase.name = "Dave Thomas"
purchase.last_five = [ 'shoes', 'shirt', 'socks', 'ski mask', 'shorts' ]
purchase.save
```

When we later read it in, the attribute is set back to an array:

```
purchase = Purchase.find_by_name("Dave Thomas")
pp purchase.last_five
pp purchase.last_five[3]
```

This code outputs the following:

```
["shoes", "shirt", "socks", "ski mask", "shorts"]
"ski mask"
```

Although powerful and convenient, this approach is problematic if we ever need to be able to use the information in the serialized columns outside a Ruby application. Unless that application understands the YAML format, the column contents will be opaque to it. In particular, it will be difficult to use the structure inside these columns in SQL queries. For these reasons, object aggregation using composition is normally the better approach to use.
