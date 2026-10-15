```
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
        return _dbSet.ToList();
    }

    public T GetById(int id)
    {
        return _dbSet.Find(id);
    }
```

Now, you have also implemented this GetAll method of the IRepository of T interface in the SqlRepository class. Now, let's use this GetAll method in our application. So let's open here the Program.cs file. Here, after the call of the GetEmployeeById method, let's call a new method with the name WriteAllToConsole. And as an argument, let's pass in the employeeRepository. I press Ctrl+dot to generate this method in the Program class. Let's change the parameter type from SqlRepository to IRepository so that it can be used also with the ListRepository of Employee. Now, in this method, let's grab all employees from the repository.