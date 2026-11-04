# Part I: C# Fundamentals

Manager is a class containing information about managers:

```
public class Manager
{
    public string Name { get; set; }
    public DateTime DateOfBirth { get; set; }
    public ushort Age()
    {
        return (ushort)(DateTime.Now.Year - this.DateOfBirth.Year);
    }
    public Employee[] subordinates { get; set; }
}
```

The key difference between the Manager class and the Employee class is that Manager has an additional property, subordinates, that contains an array of employees under the supervision of a manager. In fact, a manager is actually an employee, except that he has some additional roles. In this example, the Manager class could inherit from the Employee class and then add the additional subordinates property that it requires, like this:

```
public class Manager: Employee
{
    public Employee[] subordinates { get; set; }
}
```

By inheriting from the Employee class, the Manager class has all the members defined in the Employee class made available to it. The relationships between the Employee and Manager classes can be represented using a class diagram as shown in Figure 6-1.

![](bbox=[0.35, 0.73, 0.65, 0.88])

Employee is known as the base class and Manager is a derived class. In object-oriented programming, inheritance is classified into two types: implementation and interface. This chapter explores both.

# Implementation Inheritance

Implementation inheritance is when a class derives from another base class, inheriting all the base class's members. To add new members to a class, you can define another class that derives from the existing base class. Using implementation inheritance, the new derived class inherits all of the implementation provided in the base class.