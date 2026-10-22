The result will be an array of all the matching rows, each neatly wrapped in an Order object. If no orders match the criteria, the array will be empty.

That's fine if our condition is predefined, but how do we handle the situation where the name of the customer is set externally (perhaps coming from a web form)? One way is to substitute the value of that variable into the condition string:

```
# get the name from the form
name = params[:name]
# DON'T DO THIS!!
pos = Order.find(:all,
  :conditions => "name = '#{name}' and pay_type = 'po'")
```

As the comment suggests, this really isn't a good idea. Why? It leaves the database wide open to something called a SQL injection attack, which we describe in more detail in Chapter 27, Securing Your Rails Application, on page 637. For now, take it as a given that substituting a string from an external source into a SQL statement is effectively the same as publishing your entire database to the whole online world.

Instead, the safe way to generate dynamic SQL is to let Active Record handle it. Wherever we can pass in a string containing SQL, we can also pass in an array or a hash. Doing this allows Active Record to create properly escaped SQL, which is immune from SQL injection attacks. Let's see how this works.

If we pass an array when Active Record is expecting SQL, it treats the first element of that array as a template for the SQL to generate. Within this SQL, we can embed placeholders, which will be replaced at runtime by the values in the rest of the array.

One way of specifying placeholders is to insert one or more question marks in the SQL. The first question mark is replaced by the second element of the array, the next question mark by the third, and so on. For example, we could rewrite the previous query as this:

```
name = params[:name]
pos = Order.find(:all,
  :conditions => ["name = ? and pay_type = 'po'", name])
```

We can also use named placeholders. Each placeholder is of the form :name, and the corresponding values are supplied as a hash, where the keys correspond to the names in the query:

```
name     = params[:name]
pay_type = params[:pay_type]
pos = Order.find(:all,
  :conditions => ["name = :name and pay_type = :pay_type",
                  {:pay_type => pay_type, :name => name}])
```