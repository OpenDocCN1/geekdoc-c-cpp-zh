# Chapter 6: Classes

For purposes of elucidation, these warnings are ignored and, in fact, disabled with #pragma directives in the accompanying source code until the concepts are fully developed later in the chapter.

# Accessing an Instance Field

You can set and retrieve the data within fields. However, the fact that a field does not include a static modifier indicates that it is an instance field. You can access an instance field only from an instance of the containing class (an object). You cannot access it from the class directly (without first creating instance, in other words).

Listing 6.6 shows an updated look at the Program class and its utilization of the Employee class, and Output 6.1 shows the results.

Listing 6.6: Accessing Fields

```
public class Program {
    public static void Main() {
        Employee employee1 = new Employee();
        Employee employee2;
        employee2 = new Employee();
        
        employee1.FirstName = "Inigo";
        employee1.LastName = "Montoya";
        employee1.Salary = "Too Little";
        IncreaseSalary(employee1);
        Console.WriteLine($"{
            employee1.FirstName} {
            employee1.LastName}: {
            employee1.Salary}
        }");
        // ...
    }

    public static void IncreaseSalary(Employee employee) {
        employee.Salary = "Enough to survive on";
    }
}
```