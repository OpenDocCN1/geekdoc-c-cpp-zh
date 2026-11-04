However, this statement results in a runtime error (see Figure 13-4) because the Sort() method does not know how Employee objects should be sorted.

```
employees.Sort();
```

![](bbox=[0.25, 0.27, 0.82, 0.54])

Figure 13-4

To solve this problem, the Employee class needs to implement the IComparable<T> interface and then implement the CompareTo() method:

```
public class Employee : IComparable<Employee>
{
    public string FirstName
    { get; set; }

    public string LastName
    { get; set; }

    public int Salary
    { get; set; }

    public override string ToString()
    {
        return FirstName + ", " + LastName +
            " $" + Salary;
    }

    public int CompareTo(Employee emp)
    {
        return this.FirstName.CompareTo(emp.FirstName);
    }
}
```

The CompareTo() method takes an Employee parameter, and you compare the current instance (represented by this) of the Employee class's FirstName property to the parameter's FirstName property. Here, you use the CompareTo() method of the String class (FirstName is of String type) to perform the comparison.