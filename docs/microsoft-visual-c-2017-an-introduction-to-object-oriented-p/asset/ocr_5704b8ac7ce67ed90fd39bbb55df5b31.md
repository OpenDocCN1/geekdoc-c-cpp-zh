# Understanding Constructors

as long as their parameter lists do not cause ambiguity. A class can contain only one parameterless constructor: the default constructor, which can be the automatically-provided one or one that you write. If you create any number of constructors but do not create a parameterless version, they would be ambiguous. then the class does not have a default constructor.

For example, the Employee class in Figure 9-24 contains four constructors. The Main() method within the CreateSomeEmployees class in Figure 9-25 shows how different types of Employees might be instantiated. Notice that not even one of the Employee constructor—one that supports a character parameter—doesn’t even use the Employee; sometimes you might create a constructor with a specific parameter type simply to force that constructor to be the one that executes. The output of the CreateSomeEmployees program is shown in Figure 9-26.

```
class Employee
{
    public int IdNumber {get; set;}

    public double Salary {get; set;}
    public Employee()
{
        IdNumber = 999;
        Salary = 0;
    }
    public Employee(int empId)
{
        IdNumber = empId;
        Salary = 0;
    }
    public Employee(int empId, double sal)
{
        IdNumber = empId;
        Salary = sal;
    }
    public Employee(char code)
{
        IdNumber = 111;
        Salary = 100000;
    }
}
```

Figure 9-24 Employee class with four constructors

![](bbox=[0.476, 0.458, 0.715, 0.508])