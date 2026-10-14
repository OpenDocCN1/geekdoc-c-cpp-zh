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

## Filtering data

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

It is important to understand this sequence of operations—the Where method is applied first to filter the rows, followed by the Select method to specify the fields. The foreach statement that iterates through this collection displays the following companies:

```
Coho Winery
Trey Research
```

## Ordering, grouping, and aggregating data

If you are familiar with SQL, you are aware that it makes it possible for you to perform a wide variety of relational operations besides simple projection and filtering. For example, you can specify that you want data to be returned in a specific order, you can group the rows returned according to one or more key fields, and you can calculate summary values based on the rows in each group. LINQ provides the same functionality.

To retrieve data in a particular order, you can use the OrderBy method. Like the Select and Where methods, OrderBy expects a method as its argument. This method identifies the expressions that you want to use to sort the data. For example, you can display the name of each company in the addresses array in ascending order, like this:

Click here to view code image

```
IEnumerable<string> companyNames =
    addresses.OrderBy(addr => addr.CompanyName).Select(comp =>
comp.CompanyName);

foreach (string name in companyNames)
{
    Console.WriteLine(name);
}
```

This block of code displays the companies in the addresses table in alphabetical order.

```
Alpine Ski House
Coho Winery
Trey Research
Wide World Importers
Wingtip Toys
```

If you want to enumerate the data in descending order, you can use the OrderByDescending method instead. If you want to order by more than one key value, you can use the ThenBy or ThenByDescending method after OrderBy or OrderByDescending.

To group data according to common values in one or more fields, you can use the GroupBy method. The following example shows how to group the companies in the addresses array by country:

Click here to view code image

```
var companiesGroupedByCountry =
    addresses.GroupBy(addrs => addrs.Country);

foreach (var companiesPerCountry in companiesGroupedByCountry)
{
    Console.WriteLine(
        $"Country:
{companiesPerCountry.Key}\t{companiesPerCountry.Count()} companies");
    foreach (var companies in companiesPerCountry)
    {
        Console.WriteLine($"\t{companies.CompanyName}");
    }
}
```

By now, you should recognize the pattern. The *GroupBy* method expects a method that specifies the fields by which to group the data. However, there are some subtle differences between the *GroupBy* method and the other methods that you have seen so far.

The main point of interest is that you don’t need to use the *Select* method to project the fields to the result. The enumerable set returned by *GroupBy* contains all the fields in the original source collection, but the rows are ordered into a set of enumerable collections based on the field identified by the method specified by *GroupBy*. In other words, the result of the *GroupBy* method is an enumerable set of groups, each of which is an enumerable set of rows. In the example just shown, the enumerable set *companiesGroupedByCountry* is a set of countries. The items in this set are themselves enumerable collections containing the companies for each country in turn. The code that displays the companies in each country uses a *foreach* loop to iterate through the *companiesGroupedByCountry* set to yield and display each country in turn, and then it uses a nested *foreach* loop to iterate through the set of companies in each country. Notice in the outer *foreach* loop that you can access the value you are grouping by using the *Key* field of each item, and you can also calculate summary data for each group by using methods such as *Count*, *Max*, *Min*, and many others. The output generated by the example code looks like this:

Click here to view code image

```
Country: Switzerland    1 companies
    Alpine Ski House
Country: United States  2 companies
    Coho Winery
    Trey Research
Country: United Kingdom 2 companies
    Wingtip Toys
    Wide World Importers
```

You can use many of the summary methods such as *Count*, *Max*, and *Min*

directly over the results of the Select method. If you want to know how many companies there are in the addresses array, you can use a block of code such as this:

Click here to view code image

```
int numberOfCompanies = addresses.Select(addr =>
addr.CompanyName).Count();
Console.WriteLine($"Number of companies: {numberOfCompanies}");
```

Notice that the result of these methods is a single scalar value rather than an enumerable collection. The output from the preceding block of code looks like this:

```
Number of companies: 5
```

I should utter a word of caution at this point. These summary methods do not distinguish between rows in the underlying set that contain duplicate values in the fields you are projecting. This means that, strictly speaking, the preceding example shows you only how many rows in the addresses array contain a value in the CompanyName field. If you wanted to find out how many different countries are mentioned in this table, you might be tempted to try this:

Click here to view code image

```
int numberOfCountries = addresses.Select(addr =>
addr.Country).Count();
Console.WriteLine($"Number of countries: {numberOfCountries}");
```

The output looks like this:

```
Number of countries: 5
```

In fact, the addresses array includes only three different countries—it just so happens that United States and United Kingdom both occur twice. You can eliminate duplicates from the calculation by using the Distinct method, like this:

Click here to view code image

```
int numberOfCountries =
    addresses.Select(addr => addr.Country).Distinct().Count();
Console.WriteLine($"Number of countries: {numberOfCountries}");
```

The Console.WriteLine statement now outputs the expected result:

```
Number of countries: 3
```

## Joining data

Just like SQL, LINQ gives you the ability to join together multiple sets of data over one or more common key fields. The following example shows how to display the first and last names of each customer, together with the name of the country where the customer is located:
