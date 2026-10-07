when generating CIL, but why is it useful to the developer to have an object representing that analysis at execution time? Let's take a look at an example.

# Using Lambda Expressions as Data

Consider the lambda expression in the following:

```
persons.Where(
  person => person.Name.ToUpper() == "INIGO MONTOYA");
```

Suppose persons is an array of Persons, and the formal parameter of the Where method corresponds to the lambda expression argument is of the delegate type Func<Person, bool>. The compiler emits a method that contains the code in the body of the lambda. It generates a delegate to the emitted method. The Where method returns a query object that, when executed, applies the delegate to each member of the array to determine the query results.

Now suppose persons is not an array of Persons, but rather an object that represents a remote database table containing data on millions of people. Information about each row in the table can be streamed from the server to the client, and the client can then create a Person object corresponding to that row. The call to Where on the client, how are the results determined? When the results of that query are requested how are the results determined?

One technique would be to transmit millions of rows of data from the server to the client. You could create a Person object from each row, create a delegate from the lambda, and execute the delegate on every Person. This is conceptually different from the array scenario, but it is, far more expensive.

A second, much better technique is to somehow send the meaning of the lambda ("filter out row that names a person other than Inigo Montoya") to the server. Database servers are optimized to rapidly perform this sort of filtering. The server can then stream only the tiny number of matching rows to the client. Thus, instead of creating millions of Person objects and rejecting almost all of them, the client creates only those objects that already match the query, as determined by the server. But how does the meaning of the lambda get sent to the server?