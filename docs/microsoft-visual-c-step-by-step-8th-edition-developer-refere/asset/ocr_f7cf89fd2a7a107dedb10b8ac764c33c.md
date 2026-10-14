```
{
    FirstName = cust.FirstName,
    LastName = cust.LastName
} );
```

The second option is arguably preferable, but if this is the only use that your application makes of the Names type, you might prefer to use an anonymous type, as in the following, instead of defining a new type specifically for a single operation:

Click here to view code image

```
var customerNames =
    customers.Select(cust => new { FirstName = cust.FirstName,
LastName = cust.LastName } );
```

Notice the use of the var keyword here to define the type of the enumerable collection. The type of objects in the collection is anonymous, so you do not know the specific type for the objects in the collection.

# Filtering data

With the Select method, you can specify, or project, the fields that you want to include in the enumerable collection. However, you might also want to restrict the rows that the enumerable collection contains. For example, suppose you want to list only the names of companies in the addresses array that are located in the United States. To do this, you can use the Where method, as follows:

Click here to view code image

```
IEnumerable<string> usCompanies =
    addresses.Where(addr => String.Equals(addr.Country, "United States"))
        .Select(usComp => usComp.CompanyName);

foreach (string name in usCompanies)
{
    Console.WriteLine(name);
}
```

Syntactically, the Where method is similar to Select. It expects a parameter that defines a method that filters the data according to whatever criteria you specify. This example makes use of another lambda expression. The variable addr is an alias for a row in the addresses array, and the lambda expression returns all rows where the Country field matches the string “United States”. The Where method returns an enumerable collection of rows containing every field from the original collection. The Select method is then applied to these rows to project only the CompanyName field from this enumerable collection to return another enumerable collection of string objects. (The variable usComp is an alias for the type of each row in the enumerable collection returned by the Where method.) The type of the result of this complete expression is therefore IEnumerable<string>.