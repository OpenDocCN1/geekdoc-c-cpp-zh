```
Region="South America", Sales=1001 },
    new Customer { ID="T", City="Lima", Country="Peru",
Region="South America", Sales=2002 }
};
```

+   3. In the Main() method, following the initialization of the customers list, enter (or modify) the query as shown here:
+   ```
+   var queryResults = customers.Select(c => c.Region).Distinct();
+   ```
+   4. Finish the remaining code in the Main() method as shown here.
+   ```
+   foreach (var item in queryResults)
+   {
+       WriteLine(item);
+   }
+   Write("Program finished, press Enter/Return to continue:");
+   ReadLine();
+   ```
+   5. Compile and execute the program. You will see the unique regions where customers exist:
+   ```
+   North America
+   Asia
+   South America
+   Europe
+   Africa
+   Program finished, press Enter/Return to continue:
+   ```

# How It Works

The Customer class and customers list initialization are the same as in the previous example. In the query statement, you call the Select() method with a simple lambda expression to select the region from the Customer objects, and then call Distinct() to return only the unique results from Select():

```
var queryResults = customers.Select(c => c.Region).Distinct();
```

Because Distinct() is available only in method syntax, you make the call to Select() using method syntax. However, you can call Distinct() to modify a query made in the query syntax as well:

```
var queryResults = (from c in customers select c.Region).Distinct();
```

Because query syntax is translated by the C# compiler into the same series of LINQ method calls as used in the method syntax, you can mix and match if it makes sense for readability and style.

# ORDERING BY MULTIPLE LEVELS

Now that you are dealing with objects with multiple properties, you might be able to envision a situation where ordering the query results by a single field is not enough. What if you wanted to query your customers and order the results alphabetically by region, but then order alphabetically by country or city name within a region? LINQ makes this very easy, as you will see in the following Try It Out.