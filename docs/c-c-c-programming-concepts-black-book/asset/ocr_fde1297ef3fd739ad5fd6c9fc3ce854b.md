selected those elementsfrom the array that come in the range of 50 to 100 using the *SkipWhile()* and *TakeWhile()* methods. The output of the program is given as follows:

```
```text
Skipping the first 5 elements...
60
100
Taking the first 2 elements...
10
20
Printing the values whose values are between 50 and 100...
50
60
100
```
```

# Equality Operator

In LINQ, *SequenceEqual* is the main equality operator. The *SequenceEqual* operator checks the sequence of two collections and returns true only if one set is exactly the duplicate of another; otherwise, it returns false. Listing 19.36 shows an example of equality operator:

Listing 19.36: Showing an Example of Equality operator

```
```csharp
using System;
using System.Linq;
using System.Collections;
using System.Collections.Generic;

class program
{
    public static void Main()
    {
        Employee e1 = new Employee(100, "Mathew", "Canada");
        Employee e2 = new Employee(200, "John", "USA");
        Employee e3 = new Employee(500, "Marry", "UK");

        List<Employee> set1 = new List<Employee>{ e2, e3, e1 };
        List<Employee> set2 = new List<Employee>{ e1, e2, e3 };

        bool isMatched = set1.SequenceEqual(set2);
        if (isMatched)
        {
            Console.WriteLine("The sets are of same sequence");
        }
        else
        {
            Console.WriteLine("The sets are of different sequence");
        }
    }
}

class Employee
{
    public int empID;
    public string empName;
    public string empCity;

    public Employee()
```
```