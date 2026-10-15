
Let's make the StorageAppDbContext class inherit from DbContext. I press Esc to close IntelliSense and Ctrl+. to add a using for Microsoft.EntityFrameworkCore. Now, let's also make this class a public class, and let's put the cursor on the usings here, and I press Ctrl+. to remove the unnecessary usings. Now, in this class we need a property for the Employees. In Entity Framework Core, this is a DbSet. As you can see, this is a generic class that takes the entity type as a generic type argument. So let's create here a DbSet. I press Ctrl+. to add a using for the Entities namespace that contains the Employee class. Now let's call this property Employees. As you can see, it is underlined in green because we have enabled nullable reference types in the .csproj file. When you hover it, you can see here the warning that the property Employees must contain a value when exiting constructor. Consider declaring the property as nullable. So you could declare here the property with a question mark as nullable, and then the warning disappears. But on a DbContext, the DbSet property is usually not null, as it is initialized in the constructor of the DbContext base class.

![](img/0155736aec718cf18821e9f10a5d308d_1108_0.png)

Instead of using here the question mark, you can do a different thing. You can use here an expression body, and you can use the generic Set method that is defined in the DbContext base class, and you can see this method returns a DbSet of TEntity. To use this generic Set method, you have to pass in a generic type argument. In this case, let's pass in the type Employee, and then this Set method will return a DbSet exactly like we needed for this property.

![](img/0155736aec718cf18821e9f10a5d308d_1109_0.png)

I copy this DbSet property, and we also create one for the organizations. So here let's call the property Organizations, and let's call this generic Set method with the Organization type. Now besides these two properties, let's override here the OnConfiguring method. On the optionsBuilder, you'll find an extension method that is called UseInMemoryDatabase. You have to specify a database name with this method. Let's call the database StorageAppDb. Now this Entity Framework DbContext is set up, and you can implement the SqlRepository class, so let's open this class. First, let me remove here this _items field, as we don't need that list.

```csharp
public class StorageAppDbContext : DbContext
{
    public DbSet<Employee> Employees => Set<Employee>();
    public DbSet<Organization> Organizations => Set<Organization>();

    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
    {
        base.OnConfiguring(optionsBuilder);
        optionsBuilder.UseInMemoryDatabase("StorageAppDb");
    }
}
```

> ▲ 1 of 2 ▼ (extension) DbContextOptionsBuilder DbContextOptionsBuilder.UseInMemoryDatabase(string databaseName, [System.Action<Microsoft.EntityFrameworkCore.Infrastructure.InMemoryDbContextOptionsBuilder>] inMemoryOptionsAction = null)
> Configures the context to connect to a named in-memory database. The in-memory database is shared anywhere the same
> databaseName: The name of the in-memory database. This allows the scope of the in-memory database to be controlled

Next, let's create a constructor, and the constructor takes as a parameter a DbContext instance. I press Ctrl+. to add a using for Microsoft.EntityFrameworkCore. Let's call the parameter dbContext, and I press Ctrl+. to create and assign a field _dbContext. In addition, I also want to grab the DbSet from the dbContext, and I want to store that in an _dbSet field. So on the dbContext, I use the generic Set method that we have used already in the context, and as an entity, I specify the type T. Now I press Ctrl+. to create that DbSet field in our class. Here is the created _dbSet field, but as you can see it is underlined in red. When you hover it, you see here the error that the type T must be a reference type in order to use it as a parameter TEntity in the generic type or method DbSet<TEntity>.

```csharp
public class SqlRepository<T> where T : IEntity
{
    private readonly DbContext _dbContext;

    public SqlRepository(DbContext dbContext)
    {
        _dbContext = dbContext;
    }

    public T GetById(int id)
    {
        return _items.Single(item => item.Id == id);
    }
}
```

This means here we need to adjust the generic type constraint, as T must be a reference type so that it can be used with Entity Framework Core. To do this, let's use here the class constraint before the IEntity interface. Now you see the error is gone. So next, you can implement now the methods. GetById is a very simple one. On the dbSet, you can call the Find method with the id, and this will return the object by its ID. The Add method is also quite simple. On the dbSet you call the Add method with the item of type T.

```csharp
public class SqlRepository<T> where T : class, IEntity
{
    private readonly DbContext _dbContext;
    private readonly DbSet<T> _dbSet;

    public SqlRepository(DbContext dbContext)
    {
        _dbContext = dbContext;
        _dbSet = _dbContext.Set<T>();
    }

    public T GetById(int id)
    {
        return _items.Single(item => item.Id == id);
    }

    public void Add(T item)
```

The Remove method is also simple. On the dbSet you call the Remove method with the item. In the Save method you don't need a foreach loop. Instead, you use the dbContext instance, and you call its SaveChanges method. That's it. Now you have implemented a generic SqlRepository class that uses an Entity Framework DbContext to store the items. Now let's go to the Solution Explorer and let's open the Program.cs file, and here instead of a ListRepository, let's use the SqlRepository.

```csharp
public void Add(T item)
{
    _dbSet.Add(item);
}

public void Remove(T item)
{
    _dbSet.Remove(item);
}

public void Save()
{
    _dbContext.SaveChanges();
}
```

The constructor of the SqlRepository takes a DbContext instance, so let's create here a new instance of our StorageAppDbContext class. I press Ctrl+. to add a using for the Data namespace that contains this class. So now you have here a SqlRepository instance, but as you can see it is underlined here in red, as it is not a valid argument for these two methods. This is because these methods take ListRepositories and not SqlRepositories. So when you hover here the employeeRepository argument, you can see the error cannot convert SqlRepository to ListRepository. Let's fix this in the next chapter by creating a generic interface.

## Chapter 10 How to Create Generic Interface

In this demonstration, you will learn how to create a generic interface. Here, I've opened the Program.cs file of the StorageApp. Previously, you have created the SqlRepository class, but it does not work with these methods, as these methods have a ListRepository parameter. Now let's introduce a generic IRepository interface so that these methods work not only with list repositories, but also with SQL repositories. To do this, let's open here the SqlRepository class. First, let me put the cursor on the usings, and let's press Ctrl+. to remove unnecessary usings. Now, let's put the cursor on the SqlRepository class name, and let's press Ctrl+., and you can see Visual Studio suggests extracting an interface here.

![](img/0155736aec718cf18821e9f10a5d308d_1114_0.png)

Let's press Enter to select this option. In this dialog, let's call the new interface just IRepository, and I want to create it in the new file name IRepository.cs. Next, you can select here the public members to form the interface. I keep all members selected, and I click the OK button. Now you can see the SqlRepository class implements this generic IRepository interface. Let's go to the Solution Explorer, and you can see here the IRepository.cs file. Let's open the .cs file until you see the generic IRepository interface. Like a generic class, it has here a generic type parameter and also a type constraint for the type parameter. Then the type parameter is used for the methods that are defined in this interface. When you define type constraints like here, it means that generic classes that implement this interface also must define these type constraints for their generic type parameter. Let me show you this by implementing the interface now on the ListRepository class. Let's expand this class, and here, let's implement the new IRepository interface.

![](img/0155736aec718cf18821e9f10a5d308d_1115_0.png)

```csharp
public interface IRepository<T> where T : class, IEntity
{
    void Add(T item);
    T GetById(int id);
    void Remove(T item);
    void Save();
}
```

As you can see, the ListRepository class is underlined in red. When I hover it, you can see that the type 'T' must be a reference type in order to use it as a parameter T in the generic type or method 'IRepository'. This means also here in this class we need now this class type constraint, but maybe this makes not so much sense, as this is an implementation detail of this ListRepository class that is
