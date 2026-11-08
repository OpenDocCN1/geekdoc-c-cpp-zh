| Class Name | Data Type | Description |
|---|---|---|
| **Category: Other** |  |  |
| Char | char | Represents 16-bit Unicode character |
| Decimal | decimal | Represents a decimal value (128-bit) |
| Object | object | Represents the root of the object hierarchy |
| String | string | Represents a fixed length string of Unicode characters |

**Table 17.1: Built-In Data Types in C#**

Now, let’s learn how the built-in data types are declared in a C# program. Listing 17.4 shows the declaration of different built-in data types:

# Listing 17.4: Showing the Declaration of Built-In Data Types

```
```csharp
using System;
class Program
{
    public static void Main()
    {
        Employee e = new Employee(100, "Mr. Scott", 20000, 'M', true);
        e.PrintEmployeeDetails();
    }
}
class Employee
{
    public int empID;
    public string empName;
    public long empSalary;
    public char empGender;
    public bool empIsMarried;
    public Employee()
    {
    }
    public Employee(int ID, string name, long salary, char gender, bool isMarried)
    {
        this.empID = ID;
        this.empName = name;
        this.empSalary = salary;
        this.empGender = gender;
        this.empIsMarried = isMarried;
    }
    public void PrintEmployeeDetails()
    {
        Console.WriteLine("The Employee details are....");
        Console.WriteLine("Employee ID is {0}", this.empID);
        Console.WriteLine("Employee name is {0}", this.empName);
        Console.WriteLine("Employee salary is {0}", this.empSalary);
        Console.WriteLine("Employee gender is {0}", this.empGender);
        Console.WriteLine("Employee marital status is {0}", this.empIsMarried);
    }
}
```
```