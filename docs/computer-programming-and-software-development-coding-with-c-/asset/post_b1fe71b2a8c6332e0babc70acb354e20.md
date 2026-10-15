
This means now that T is, by default, not nullable. Let's see this in action. Let's go to the Programs.cs file, and let's try to use here the GenericRepository with a nullable Employee. As you can see, it gets underlined in green because you get here a warning. When you hover it, you can see that the type Employee cannot be used as a type parameter 'T' in the generic type 'GenericRepository'. Nullability of type argument does not match 'class' constraint. The same warning exists also for the IEntity constraint. So, let's go back to the GenericRepository. You can also add here a question mark to the class constraint to say that T can be a nullable reference type. In addition, you also add the question mark to the IEntity interface to say that it can be a nullable IEntity. Now, when you look again at the Program.cs file, you can see that this nullable Employee reference type is now okay as a type argument for the GenericRepository class.

```
public class GenericRepository<T> where T : class?, IEntity?
{
    private readonly List<T> _items = new();

    public T? GetById(int id)
    {
        //return _items.Single(item => item.Id == id);

        return null;
    }

    public void Add(T item)
    {
        item.Id = _items.Count + 1;
        _items.Add(item);
    }

    public void Remove(T item)
    {
```

Now let's remove here the question mark again, let's save this file, and let's close it. When you look at the item in the Add method,
you can also see that it is underlined in green because the compiler warns you here that item can be null because you have marked T as a nullable reference type. But you don't want to store null values in the GenericRepository, so let's remove here the question marks from the IEntity constraint and from the class constraint.

```
public void Add(T item)
{
    item.Id = _items.Count + 1;
    _items.Add(item);
}
```

Now T is a reference type, and you can see the item parameter here is not underlined in green anymore. Beside the class constraint, you can also define here the struct constraint to say that T must be a value type, and you can also define other base classes like, for example, System.Enum to say that T is an enum. But now let's remove this, and let's say, in our case, T should be a class.

```
public class GenericRepository<T> where T : class, IEntity
{
    private readonly List<T> _items = new();

    public T? GetById(int id)
    {
        //return _items.Single(item => item.Id == id);

        return null;
    }

    public void Add(T item)
    {
        item.Id = _items.Count + 1;
        _items.Add(item);
    }

    public void Remove(T item)
    {
```

Now let's remove here this return null from the GetById method, and let's uncomment here our Single call, and the return value cannot be null anymore.

```
public class GenericRepository<T> where T : class, IEntity
{
    private readonly List<T> _items = new();

    public T GetById(int id)
    {
        return _items.Single(item => item.Id == id);
    }

    public void Add(T item)
    {
        item.Id = _items.Count + 1;
        _items.Add(item);
    }

    public void Remove(T item)
    {
        _items.Remove(item);
    }
```

So far to the class constraint. In the next chapter, you will learn about the new constraint that allows you to call a parameterless constructor.

## Chapter 8 How to Use the New() Constraint

In this demonstration you will learn how to use the new() constraint to call the parameterless constructor of your generic type parameter. Here, I've opened the GenericRepository class. Let's create in this GenericRepository class, a method that I call CreateItem, and from that method, let's return the new instance of type T. As you can see, this code line is underlined in red. When you hover over it, you can see here the error, Cannot create an instance of the variable type "T" because it does not have the new() constraint.

![](img/0155736aec718cf18821e9f10a5d308d_1098_0.png)

To call the constructor, you must ensure that the type T has actually a parameterless constructor. And to ensure this, you will add the new() constraint. This constraint must be the last constraint that you define here. So the order works like normal inheritance in C#. You define here the class name like Entity base, or you use the keywords class or struct. Then you define all the interfaces that you need on
your generic type parameter, and at the end, you can define the new() constraint if you need to create instances of type T by calling the parameterless constructor. Now with this new() constraint and this CreateItem method, this means now that in the Program.cs file on that GenericRepository you have now this CreateItem method that returns the new employee instance.

![](img/0155736aec718cf18821e9f10a5d308d_1099_0.png)

Now let's see what happens when you add a constructor with the parameter to the Employee class. So let's open here the Employee class, and let's create here a constructor with the ctor snippet. I press the Tab key twice, and let's add on that constructor the firstName parameter. Now let's go back to the Program.cs file. As you can see, the Employee is underlined in red. When you hover over it, you can see the error that the employee must be a type with the public parameterless constructor in order to use it as a parameter "T" in the generic type or method GenericRepository.

```
static void Main(string[] args)
{
    var employeeRepository = new GenericRepository<Employee>();
    AddEmployees(employeeRepository);
    GetEmployeeById(employeeRepository);
    var organizationRepository = new GenericRepository<Organization>();
    AddOrganizations(organizationRepository);
    Console.ReadLine();
}

private static void GetEmployeeById(GenericRepository<Employee> employeeRepository)
{
    var employee = employeeRepository.GetById(2);
    Console.WriteLine($"Employee with Id 2: {employee.FirstName}");
}
```

When you go back to the GenericRepository class, and when you remove here this new() constraint, it means you cannot implement here the CreateItem method, because no parameterless constructor exists, so let's remove that one, and now let's go back to the Program.cs file, and now you see everything is fine again, even with that constructor in the Employee class. Let's remove here this empty line, and let's remove again the constructor here from the Employee class; we don't need that one. Now let's go back to the GenericRepository class, and let me show you one more thing. When you have multiple type parameters, let's add here another one with the name TKey, then you can define multiple wheres for the different type parameters.

```
public class Employee : EntityBase
{
    public string? FirstName { get; set; }
    public override string ToString() => $"Id: {Id}, FirstName: {FirstName}";
}
```

So here, I could say for example, that TKey needs to be a struct. You can even do more advanced things. You can say, for example even that TKey needs to be the subtype of T. So you see, you can play around with these generic type constraints to ensure that the generic type arguments that are passed to your class have the shape that you need.

```
public class GenericRepository<T, TKey>
    where T : class, IEntity
    where TKey : T
{
    private readonly List<T> _items = new();

    public T GetById(int id)
    {
        return _items.Single(item => item.Id == id);
    }

    public void Add(T item)
    {
        item.Id = _items.Count + 1;
        _items.Add(item);
    }

    public void Remove(T item)
    {
```

Now in our case, you just need to ensure that T is of type IEntity, as we need the Id property in our class. So let's remove the rest here, and let's also remove that second generic type parameter. Now let's run the application and let's see if everything still works. We have here the three employees, we have here the employee with Id 2, and then we have here the two organizations. Now let's wrap up what you have learned in this chapter. You learned in this chapter
