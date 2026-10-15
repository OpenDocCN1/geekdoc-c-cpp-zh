
As you can see, here the error from the SqlRepository class disappeared. Now, when you use this repo variable, you have here the Add method that takes a Manager, and you have the Remove method that also takes a Manager. So, when you call the Add method, for example, with a new Manager, that Manager is passed to the SqlRepository's Add method that can handle employees. As a manager is an employee, this works fine.

```csharp
var employeeRepository = new SqlRepository<Employee>(new StorageAppDbContext());
AddEmployees(employeeRepository);
AddManagers(employeeRepository);
GetEmployeeById(employeeRepository);
WriteAllToConsole(employeeRepository);

var organizationRepository = new ListRepository<Organization>();
AddOrganizations(organizationRepository);
WriteAllToConsole(organizationRepository);

Console.ReadLine();
}

private static void AddManagers(IRepository<Manager> managerRepository)
{
    managerRepository.Add(new Manager { FirstName = "Sara" });
    managerRepository.Add(new Manager { FirstName = "Henry" });
    managerRepository.Save();
}
```

Now let's remove these code lines again here. Let's continue with our AddManagers method down here. Instead of taking now an IRepository of Manager, let's take here an IWriteRepository of Manager, and now you see the error here is gone. You can pass now a SqlRepository of Employee or also a list repository of Employee to this AddManagers method, and it will just work. But inside this method, you can only add managers, as the managerRepository parameter here has the generic type argument, Manager.

```csharp
var employeeRepository = new SqlRepository<Employee>(new StorageAppDbContext());
AddEmployees(employeeRepository);
AddManagers(employeeRepository);
GetEmployeeById(employeeRepository);
WriteAllToConsole(employeeRepository);

var organizationRepository = new ListRepository<Organization>();
AddOrganizations(organizationRepository);
WriteAllToConsole(organizationRepository);

Console.ReadLine();
}

private static void AddManagers(IWriteRepository<Manager> managerRepository)
{
    managerRepository.Add(new Manager { FirstName = "Sara" });
    managerRepository.Add(new Manager { FirstName = "Henry" });
    managerRepository.Save();
}
```

Now let's see this in action, and let's run our application. You see the three employees, and here, you see the two managers. As you can see, the managers are not ordered by their ID.

```
Employee with Id 2: Anna
Id: 1, FirstName: Julia
Id: 2, FirstName: Anna
Id: 3, FirstName: Thomas
Id: 5, FirstName: Henry (Manager)
Id: 4, FirstName: Sara (Manager)
```

Now let's change this. I open here the SqlRepository class, and I scroll down to the GetAll method. Here, on the dbSet, before calling the ToList method, let's use the OrderBy method from the System.Linq namespace.

```csharp
public class SqlRepository<T> : IRepository<T> where T : class, IEntity
{
    private readonly DbContext _dbContext;
    private readonly DbSet<T> _dbSet;

    public SqlRepository(DbContext dbContext)
    {
        _dbContext = dbContext;
        _dbSet = _dbContext.Set<T>();
    }

    public IEnumerable<T> GetAll()
    {
        return _dbSet.OrderBy(item => item.Id).ToList();
    }

    public T GetById(int id)
    {
        return _dbSet.Find(id);
    }
}
```

Let's pass in a function that grabs from the item the ID. You can use here the ID, as we have here this generic type constraint with the IEntity interface. This means now that you will get the items ordered by ID. Let's run the application, and now you'll see all the employees and managers are ordered now by their ID. In the next chapter, you will learn more about working with interface inheritance.

## Chapter 13 How to Work with Interface Inheritance

In this demonstration, you will learn how to work with interface inheritance. Previously, you learned already how to inherit this IRepository interface from these two generic interfaces. So you see, like with class inheritance, you just pass the generic type parameter to the base interfaces. You can also define more generic type parameters on a subinterface, or you can also inherit an interface from a generic interface. Now let me show you a few more things in this file. Let's create here another interface, and let's call it ISuperRepository, and let's inherit that one from IRepository.

```csharp
public interface IWriteRepository<in T>
{
    void Add(T item);
    void Remove(T item);
    void Save();
}

public interface IReadRepository<out T>
{
    IEnumerable<T> GetAll();
    T GetById(int id);
}

public interface IRepository<T> : IReadRepository<T>, IWriteRepository<T>
    where T : IEntity
{
}
```

As you can see, it is underlined in red, and when you hover it, you see here the error that the type 'T' cannot be used as a type parameter 'T' in the generic type or method IRepository. There is no conversion from T to IEntity. This is because in IRepository, T must be an IEntity, so you also have to add here this type constraint where T is IEntity. Now, what you can also do, of course, is defining other type parameters on a subinterface. So here, I could create here, for example, a Key property in this interface that is of type TKey. But what you can also do, you can also inherit an interface from a generic interface. So let's remove here the type constraint, and let's say you want to inherit from IRepository.

![](img/0155736aec718cf18821e9f10a5d308d_1141_0.png)

Then the interface might have the name IEmployeeRepository. So you see, you can inherit generic interfaces from generic interfaces, and you can also inherit interfaces from generic interfaces. Of course, you can also inherit a generic interface from an interface. When you look, for example, at the IEnumerable interface, you will see that. Let's open this interface, and let's select here Go To Definition from the context menu. As you can see, this generic interface has a covariant type parameter, and it inherits from the IEnumerable interface. Now let's close this again.

```csharp
public interface IRepository<T> : IReadRepository<T>, IWriteRepository<T>
    where T : IEntity
{
}

public interface IEmployeeRepository : IRepository<Employee>
{
}
```

The same concepts apply also to classes. So let's change here the interface to an EmployeeRepository class that implements the generic IRepository interface. When you put the cursor here on this IRepository interface, you can press Ctrl+., and Visual Studio suggests to you here to implement the interface. Let's do this. And now you see you have here an Add method that takes an Employee, a GetAll method that returns an IEnumerable, and so on. Now let me remove the members again from this Employee repository class.

```csharp
namespace System.Collections.Generic
{
    public interface IEnumerable<out T> : IEnumerable
    {
        IEnumerator<T> GetEnumerator();
    }
}
```

Let's delete them, and now the class is empty again. Instead of implementing the interface on a class, you can also create a GenericSuperRepository class. Let's add a type parameter here, and let's inherit from IRepository. And you need again then the generic type constraint. Now again here, you can put the cursor on the interface, and I press Ctrl+. to implement the interface, and you see now here an Add method that has a T parameter, a GetAll method that returns an IEnumerable, and so on.

```csharp
public class EmployeeRepository : IRepository<Employee>
{
    public void Add(Employee item)
    {
        throw new System.NotImplementedException();
    }

    public IEnumerable<Employee> GetAll()
    {
        throw new System.NotImplementedException();
    }

    public Employee GetById(int id)
    {
        throw new System.NotImplementedException();
    }

    public void Remove(Employee item)
    {
        throw new System.NotImplementedException();
    }
}
```

You could also define here on the generic class multiple type parameters, if you need them, and then you'll just pass that single one that is needed by the IRepository interface to that interface. Now let's remove this class again.
