# LISTING 5.8: Accessing Fields from outside the Containing Class

```
class Program
{
    static void Main()
    {
        Employee employee1 = new Employee();
        Employee employee2;
        employee2 = new Employee();

        employee1.FirstName = "Inigo";
        employee1.LastName = "Montoya";
        employee1.Salary = "Too Little";
        IncreaseSalary(employee1);
        Console.WriteLine(
            $"{ employee1.GetName() }: { employee1.Salary }");
        // ...
    }
    // ...
}
```

# OUTPUT 5.2

```
Inigo Montoya: Enough to survive on
```

# Using the this Keyword

You can obtain the reference to a class from within instance members that belong to the class. To indicate explicitly that the field or method accessed is an instance member of the containing class in C#, you use the keyword this. Use of this is implicit when calling any instance member, and it returns an instance of the object itself.

For example, consider the SetName() method shown in Listing 5.9.

# LISTING 5.9: Using this to Identify the Field's Owner Explicitly

```
class Employee
{
    public string FirstName;
    public string LastName;
    public string Salary;

    public string GetName()
    {
        return $"{ FirstName } { LastName }";
    }

    public void SetName(
```