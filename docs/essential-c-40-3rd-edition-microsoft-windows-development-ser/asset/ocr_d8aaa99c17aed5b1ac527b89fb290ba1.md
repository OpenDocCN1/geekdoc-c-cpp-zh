With these fields added, it is possible to store some fundamental data with every Employee instance. In this case, you prefix the fields with an access modifier of public. public on a field indicates that the data within the field is accessible from classes other than Employee (see the section Access Modifiers, later in this chapter).

As with local variable declarations, a field declaration includes the data type to which the field refers. Furthermore, it is possible to assign fields an initial value at declaration time, as demonstrated with the Salary field in Listing 5.5.

# LISTING 5.5: Setting Initial Values of Fields at Declaration Time

```
class Employee
{
    public string FirstName;
    public string LastName;
    public string Salary = "Not enough";
}
```

# Accessing an Instance Field

You can set and retrieve the data within fields. However, the fact that the field does not include a static modifier indicates that it is an instance field. You can access an instance field only from an instance of the containing class (an object). You cannot access it from the class directly (without first creating an instance, in other words).

Listing 5.6 shows an updated look at the Program class and its utilization of the Employee class. Output 5.1 shows the results.

# LISTING 5.6: Accessing Fields

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
        employee1.Salary = "Too little";
        IncreaseSalary(employee1);
}
```