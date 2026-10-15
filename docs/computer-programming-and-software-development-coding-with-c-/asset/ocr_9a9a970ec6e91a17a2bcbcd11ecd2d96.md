method with the name AddManagers. I pass in as an argument the employeeRepository. Now you can press, again, Ctrl + dot to generate this AddManagers method in the Program class. Here, you see it. First, let me change the parameter type from `SqlRepository` to `IRepository` so that this method would also work with a list repository of Employee. Now, in this method, let's add two managers to the repository. So let's call the Add method, and let's pass in here a manager with the first name Sara. I press Ctrl + C to copy this line, and I paste it again.

![](bbox=[0.12, 0.345, 0.91, 0.594])

```
```csharp
private static void AddManagers(SqlRepository<Employee> employeeRepository)
{
    throw new NotImplementedException();
}
```
```

And let's create another manager with the first name Henry. After this, let's call on the employeeRepository the Save method. But as you might have noticed, the employeeRepository.Add method takes an Employee, so passing in an Employee instead of a Manager is also valid here in this AddManagers method. But now, maybe inside of this AddManagers method, you only want to allow to add managers. To do this, you could change here the generic type argument on this IRepository interface from Employee to Manager. Now you see Employee is not a valid option anymore for the Add method. When you hover it, you see here the error, cannot convert from Employee