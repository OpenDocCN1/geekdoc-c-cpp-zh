```
```csharp
emplist.Add("Tim");
emplist.Add("Jonathan");
emplist.Add("Tina");

IOrderedEnumerable<string> empArr = from eName
    in emplist.OfType<string>()
    orderby eName
    select eName;

Console.WriteLine("The sorted array is....");
foreach (string name in empArr)
{
    Console.WriteLine(name);
}
```
```

In the preceding program, we have first declared an ArrayList that contains the name of employees in a random order. After that, we have written the LINQ query to get the sorted list by using the *orderby* keyword. The result of this operation is then stored in the type *IEnumerable<string>*. The output of the program is given as follows.

```
```
The sorted array is....
Anne
Johns
Jonathan
Tim
Tina
```
```

# ## Grouping Operators

Grouping operation in LINQ is achieved by using the grouping operators. These operators act similar to the GROUP BY clause in SQL. LINQ has two operators for grouping operation, which are given as follows:

+   - GroupBy
+   - ToLookup

C# provides the `groupby` keyword for the GroupBy operator. This operator returns a sequence of the `IGrouping<Key, Value>` object and based on the Key value, the Value field holds the records that match with the Key value. Listing 19.30 illustrates an example of the Grouping operation by using the `groupby` keyword.

**Listing 19.30:** Showing an Example of Grouping Operation by using the *groupby* Keyword

```
```csharp
using System;
using System.Linq;
using System.Collections;
using System.Collections.Generic;

class Program
{
    public static void Main()
    {
        List<Employee> empList = new List<Employee>();
        empList.Add(new Employee(100, "Mathew", "Canada"));
        empList.Add(new Employee(200, "John", "USA"));
        empList.Add(new Employee(500, "Marry", "UK"));
        empList.Add(new Employee(800, "Joseph", "USA"));
        empList.Add(new Employee(400, "Albert", "Canada"));
```
```