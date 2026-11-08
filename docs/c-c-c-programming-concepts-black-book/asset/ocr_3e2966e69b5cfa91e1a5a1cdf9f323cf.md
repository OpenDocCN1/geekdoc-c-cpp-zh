# # LINQ to Object

Object in this respect defines the in-memory collection of items. As C# is an object-oriented language, it mainly deals with the class objects. Therefore, LINQ to Object is used to query the information in the object types of a class. In this case, LINQ is of type IEnumerable<T>. Listing 19.11 demonstrates the implementation of LINQ to Object.

**Listing 19.11:** Showing the Implementation of LINQ to Object

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
        empList.Add(new Employee(100, "James", "Scott"));
        empList.Add(new Employee(200, "Jonathan", "Jackson"));
        empList.Add(new Employee(300, "Keith", "Scott"));
        empList.Add(new Employee(400, "Jonny", "Lee"));
        empList.Add(new Employee(500, "Amy", "John"));
        empList.Add(new Employee(600, "Leonardo", "Scott"));

        IEnumerable<Employee> empSel = from emp in empList
                                      where emp.lastName.Equals("Scott")
                                      select emp;

        foreach (Employee e in empSel)
        {
            Console.WriteLine("Employee ID: {0} Employee Name: {1}",
                              e.empID, e.firstName + " " + e.lastName);
        }
    }
}

class Employee
{
    public int empID;
    public string firstName;
    public string lastName;

    public Employee()
    {
    }

    public Employee(int id, string firstName, string lastName)
    {
        this.empID = id;
        this.firstName = firstName;
        this.lastName = lastName;
    }
}
```
```