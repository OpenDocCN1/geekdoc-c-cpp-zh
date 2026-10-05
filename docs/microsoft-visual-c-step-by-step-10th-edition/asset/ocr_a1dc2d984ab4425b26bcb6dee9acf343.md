eliminate duplicates from the calculation by using the Distinct method, like this:

Click here to view code image

```
int numberOfDistinctCountries = addresses
.Select(addr => addr.Country).Distinct().Count();
Console.WriteLine("Number of distinct countries:\{numberOfDistinctCountries}");n
```

The Console.WriteLine statement now outputs the expected result:

Number of countries: 3

# Joining data

Just like SQL, LINQ gives you the ability to join multiple sets of data over one or more common key fields. The following example shows how to display the first and last names of each customer, with the name of the country where the customer is located:

Click here to view code image

```
var companiesAndCustomers = customers
.Select(c => new { c.FirstName, c.LastName, c.CompanyName })
.Join(addresses, custs => custs.CompanyName, addrs => addrs.Country),
(custs, addrs) => new { custs.FirstName, custs.LastName, addrs.Country });
```

```
foreach (var row in companiesAndCustomers)
{
    Console.WriteLine(row);
}
```

The customers' first and last names are available in the customers array, but the country for each company that work for is stored in the addresses array. The common key between the customers array and the addresses array is the company name (CompanyName). The Select method specifies the fields of interest in the customers array (FirstName and LastName) and the field containing the common key (CompanyName).