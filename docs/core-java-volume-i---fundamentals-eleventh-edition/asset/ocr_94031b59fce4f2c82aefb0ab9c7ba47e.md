```
```java
// print out information about all Employee objects
for (Employee e : staff)
    System.out.println("name=" + e.getName() + ", salary=" + e.getSalary());
}
}
```
```

# **Listing 6.2** `interfaces/Employee.java`

```
```java
package interfaces;

public class Employee implements Comparable<Employee>
{
    private String name;
    private double salary;

    public Employee(String name, double salary)
    {
        this.name = name;
        this.salary = salary;
    }

    public String getName()
    {
        return name;
    }

    public double getSalary()
    {
        return salary;
    }

    public void raiseSalary(double byPercent)
    {
        double raise = salary * byPercent / 100;
        salary += raise;
    }

    /**
     * Compares employees by salary
     * @param other another Employee object
     * @return a negative value if this employee has a lower salary than
     * otherObject, 0 if salaries are the same, a positive value otherwise
     */
    public int compareTo(Employee other)
    {
        return Double.compare(salary, other.salary);
    }
}
```
```