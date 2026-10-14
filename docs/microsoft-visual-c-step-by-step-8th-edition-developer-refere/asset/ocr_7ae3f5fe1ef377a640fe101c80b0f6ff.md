It is important to understand this sequence of operations—the Where method is applied first to filter the rows, followed by the Select method to specify the fields. The foreach statement that iterates through this collection displays the following companies:

```
Coho Winery
Trey Research
```

# Ordering, grouping, and aggregating data

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