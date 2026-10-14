```
};

var addresses = new[] {
    new { CompanyName = "Alpine Ski House", City = "Berne",
          Country = "Switzerland"},
    new { CompanyName = "Coho Winery", City = "San Francisco",
          Country = "United States"},
    new { CompanyName = "Trey Research", City = "New York",
          Country = "United States"},
    new { CompanyName = "Wingtip Toys", City = "London",
          Country = "United Kingdom"},
    new { CompanyName = "Wide World Importers", City = "Tetbury",
          Country = "United Kingdom"}
};
```

# Note

The sections "Selecting data," "Filtering data," "Ordering, grouping, and aggregating data," and "Joining data" that follow show you the basic capabilities and syntax for querying data by using LINQ methods. The syntax can become a little complex at times, and you will see when you reach the section "Using query operators" that it is not actually necessary to remember how all the syntax works. However, it is useful for you to at least take a look at these sections so that you can fully appreciate how the query operators provided with C# perform their tasks.

# Selecting data

Suppose that you want to display a list consisting of the first name of each customer in the customers array. You can achieve this task with the following code:

Click here to view code image

```
IEnumerable<string> customerFirstNames =
    customers.Select(cust => cust.FirstName);

foreach (string name in customerFirstNames)
{
    Console.WriteLine(name);
}
```

Although this block of code is quite short, it does a lot, and it requires a degree of explanation, starting with the use of the Select method of the customers array.

Using the Select method, you can retrieve specific data from the array—in this case, just the value in the FirstName field of each item in the array. How does it work? The parameter to the Select method is actually another method that takes a row from the customers array and returns the selected data from that row. You can define your own custom method to perform this task, but the simplest mechanism