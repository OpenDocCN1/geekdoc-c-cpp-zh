
# Chapter 9 Introduction to LINQ and the List Collection

The queries in lines 48–50 and 62–65 generate the same results, but in different ways. Lines 48–50 uses LINQ to sort the query filtered then 22–24. The second query uses both the where and order by. Because queries operate on the results of other queries, it's possible to build a query one step at a time, passing the results of queries between further processing.

## 9.2.6 Interface IEnumerable<T>

As mentioned, the foreach statement can iterate through the contents of arrays, collections and LINQ query results. Actually, it iterates over any so-called IEnumerable<T> object, which happens to be what most LINQ query returns. Interfaces define and standardize the ways in which people and systems can interact with one another. For example, the controls on a radio serve as an interface between radio users and the radio's internal components. The controls allow users to perform a limited set of operations (e.g., changing the station, adjusting the volume, and choosing between AM and FM), and different radios may implement the controls in different ways (e.g., using push buttons, dials or voice commands). The interface specifies what radio performs but does not specify how the operations are implemented. The interface between a driver and a car with a manual transmission includes the steering wheel, the gear shift, the clutch, the gas pedal and the brake pedal. This same interface is found in nearly all manual-transmission cars, ensuring everyone knows how to drive one manual-transmission car to drive another.

Software objects also communicate via interfaces. A C# interface describes a set of methods and properties that can be called on an object—tell the object, for example, to perform some task or return some piece of information. The IEnumerable<T> interface describes the functionality of any object that can be iterated over and offers methods to access each. A class that implements an interface must declare all the methods and properties described by that interface.

Most LINQ queries return an IEnumerable<T> object—some queries return a single value (e.g., the sum of an int array). For queries that return an IEnumerable<T> object, you can use a foreach statement to iterate over the query results. The notation <T> indicates that the interface can be used with any type of data (for example, ints, strings or Employees). You will learn more about the <T> notation in Section 9.4. In Section 12.7, we'll discuss interfaces and show how to define your own interfaces. In Chapter 20, we'll cover generics in detail.

## 9.3 Querying an Array of Employee Objects Using LINQ

LINQ is not limited to querying arrays of simple types as int. It can be used with arrays of any type, including strings and user-defined classes. It cannot be used when a query does not have a defined meaning—for example, you cannot use orderby on values that are not comparable. Comparable types in .NET are all built-in types that implement the ever interface, which is discussed in Section 20.4. Built-in types, such as string, int and double implement IComparable. Figure 9.3 presents an Employee class. Figure 9.4 uses LINQ to query an array of Employee objects.

```csharp
// Fig. 9.3: Employee.cs
// Employee class with FirstName, LastName and MonthlySalary properties.
class Employee
{
    public string FirstName { get; } // read-only-auto-implemented property
    public string LastName { get; } // read-only-auto-implemented property
    private decimal MonthlySalary; // monthly salary of employee

    // constructor initializes first name, last name and monthly salary
    public Employee(string firstName, string lastName, decimal monthlySalary)
    {
        FirstName = firstName;
        LastName = lastName;
        this.MonthlySalary = monthlySalary;
    }

    // property that gets and sets the employee's monthly salary
    public decimal MonthlySalary
    {
        get { return MonthlySalary; }
        set
        {
            if (value >= 0) // validate that salary is nonnegative
                MonthlySalary = value;
        }
    }

    // return a string containing the employee's information
    public override string ToString()
    {
        return $"{FirstName} {LastName}";
    }
}
```

**Fig. 9.3** | Employee class with FirstName, LastName and MonthlySalary properties.

```csharp
// Fig. 9.4: LINQWithArrayOfObjects.cs
// LINQ to Objects querying an array of Employee objects.
using System;
using System.Linq;

class LINQWithArrayOfObjects
{
    static void Main()
    {
        // initialize array of employees
        var employees = new[] {
            new Employee("Jason", "Red", 5000M),
            new Employee("Ashley", "Green", 7600M),
            new Employee("Matthew", "Indigo", 3587.5M),
            new Employee("James", "Indigo", 4700.77M),
            new Employee("Luke", "Indigo", 6200M),
            new Employee("Jason", "Blue", 3200M),
            new Employee("Wendy", "Brown", 4236.4M),
        };

        // display all employees
        Console.WriteLine("Original array");
        foreach (var element in employees)
        {
            Console.WriteLine(element);
        }

        // filter a range of salaries && in a LINQ query
        var between = from e in employees
                      where (e.MonthlySalary >= 4000) && (e.MonthlySalary <= 6000)
                      select e;

        // display employees making between 4000 and 6000 per month
        Console.WriteLine("\nemployees earning in the range " +
            $"{0:C} - {1:C} per month:");
        foreach (var element in between)
        {
            Console.WriteLine(element);
        }

        // order the employees by last name, then first name with LINQ
        var nameSorted = from e in employees
                          orderby e.LastName, e.FirstName
                          select e;

        // header
        Console.WriteLine("\nfirst employee when sorted by name:");

        // attempt to display the first result of the above LINQ query
        if (nameSorted.Any())
        {
            Console.WriteLine(nameSorted.First());
        }
        else
        {
            Console.WriteLine("not found");
        }

        // use LINQ to select employee list names
        var lastNames = from e in employees
                         select e.LastName;

        // use Method Distinct to select unique last names
        Console.WriteLine("\nUnique employee last names:");
        foreach (var name in lastNames.Distinct())
        {
            Console.WriteLine(name);
        }
    }
}
```

**Fig. 9.4** | LINQ to Objects querying an array of Employee objects. (Part 1 of 3).

| Original array: | Salary |
|---|---|
| Jason Red | $5,000.00 |
| Ashley Green | $7,600.00 |
| Matthew Indigo | $3,587.50 |
| James Indigo | $4,700.77 |
| Luke Indigo | $6,200.00 |
| Jason Blue | $3,000.00 |
| Wendy Brown | $4,236.40 |

Employees earning in the range $4,000.00-$6,000.00 per month:
Jason Red $5,500.00
James Indigo $4,700.77
Wendy Brown $4,236.40

First employee when sorted by name:
Ashley Green

Unique last names:
Red
Green
Indigo
Blue
Brown

**Fig. 9.4** | LINQ to Objects querying an array of Employee objects. (Part 2 of 3.)

### 9.3.1 Accessing the Properties of an Object

The clause in line 30 accesses the range variable's properties. The compiler infers that the range variable is of type Employee; because employees was defined as an array of Employee objects (lines 11–18). Any bool expression can be used in where clause. Use line 30 with the && (conditional AND) operator to combine conditions. Here, only employees are included.

### 9.3.2 Sorting LINQ’s Results by Multiple Properties

Line 44 uses orderby to sort the results according to multiple properties—specified in comma-separated list. Here, the employees are sorted alphabetically by name.

### 9.3.3 Any, First and Count Extension Methods

Line 51 indicates that Any method, which returns true if the query at least one element. The query result’s First method (line 53) returns the first element in the. The query result is not empty (line 51) before calling First, which throws an InvalidOperationException if the collection is.

We’ve not specified that the methods First and Any. Your input previously tells you they are methods of IEnumerable<T>. They aren’t. They are actually extension methods that enhance a class’s capabilities without modifying the class’s definition. Section 10.14 shows how to create extension methods.

LINQ defines more extension methods, such as Count, which returns the number of elements in the results. Rather than using Any, we could have checked that Count was nonzero, but it’s more efficient to determine whether there’s at least one element to count all the elements. The LINQ query syntax is actually transformed by the compiler into extension methods, with results of method call used in the It also allows queries to be run on the results of previous queries, as simple involves passing the result of a method call to another method. For a complete list of enumerable<T> extension methods, visit:

### 9.3.4 Selecting a Property of an Object

Line 63 uses the select clause to select the range variable’s Lastname rather than the range interval itself. This causes the results of the query to consist of only the names (strings), instead of Employee objects. Lines 67–70 display the last names. The Distinct extension method (line 67) removes duplicate elements, causing elements in the resulting collection to be unique.

### 9.3.5 Creating New Types in the select Clause of a LINQ Query

The last LINQ query in the example (lines 74–75) selects the properties FirstName and Lastname. The syntax

```csharp
new {FirstName, e.LastName}
```
