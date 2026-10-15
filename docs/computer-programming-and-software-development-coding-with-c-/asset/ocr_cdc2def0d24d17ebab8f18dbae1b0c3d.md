from Employee, now won't be able to access the name field any longer. You'll even get a compile error saying that, indeed, name is private and cannot be accessed from a DerivedClass. However, making name protected again does allow the Manager class to access it. Protected behaves like public for inheriting types. For anything else, it behaves like private, so the member will not be accessible. We've been talking for quite a while now about inheritance. Time to see it in action. Let's head back to Visual Studio and see how we can turn our employee into a base class. Then, we'll create an inheriting class, and finally, we'll learn about the access modifiers and what influence they have. So far, we've used the employeeType variable and the EmployeeType property to distinguish between the different types an employee could be.

```
```csharp
public enum EmployeeType
{
    Sales,
    Manager,
    Research,
    StoreManager
}
```
```

And we used for that the EmployeeType enumeration. But now in this demonstration, we're going to introduce, well, different types, different classes, really, to represent the different types of employee such as a manager, a salesperson, and so on. So, I'm going to refactor my class first. Refactoring means, well, changing things a bit so that I don't need that employeeType variable anymore. That is going to give me some errors.