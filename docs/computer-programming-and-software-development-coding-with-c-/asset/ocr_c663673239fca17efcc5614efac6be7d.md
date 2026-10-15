```
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

The Remove method is also simple. On the dbSet you call the Remove method with the item. In the Save method you don't need a for each loop. Instead, you use the dbContext instance, and you call it's SaveChanges method. that's it. Now you have implemented a generic SqlRepository class that uses an Entity Framework DbContext to store the items. Now let's go to the Solution Explorer and let's open the program.cs file, and here instead of a ListRepository, let's use the SqlRepository.